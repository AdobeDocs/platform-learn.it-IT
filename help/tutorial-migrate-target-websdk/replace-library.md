---
title: Sostituire la libreria | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come migrare un’implementazione Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono la panoramica della libreria, le differenze di implementazione e altri callout importanti.
source-git-commit: 63edfc214c678a976fbec20e87e76d33180e61f1
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 1%

---

# Sostituire la libreria at.js con Platform Web SDK

Scopri come sostituire l’implementazione Adobe Target on-page per migrare da at.js a Platform Web SDK. Un sostituto di base è costituito dai seguenti passaggi:

* Controlla le impostazioni di amministrazione di Target e prendi nota del tuo ID organizzazione IMS
* Sostituire la libreria at.js con l’SDK per web di Platform
* Aggiorna il frammento pre-hiding per le implementazioni della libreria sincrona
* Configurare l’SDK web della piattaforma sulla pagina

>[!NOTE]
>
>Gli esempi forniti sono a scopo illustrativo e l’implementazione effettiva di Target può variare. Se l’implementazione di Target esistente utilizza il gestore di tag di raccolta dati di Adobe, puoi anche fare riferimento alla [Esercitazione sull’implementazione di Platform Web SDK Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) per ulteriori informazioni.


## Controlla le impostazioni di amministrazione di Target

Il primo passaggio per migrare Target all’SDK per web di Platform è quello di esaminare le impostazioni nell’interfaccia di Target **[!UICONTROL Amministrazione]** sezione .

### [!UICONTROL Implementazione]

#### [!UICONTROL Dettagli account]

* **[!UICONTROL ID organizzazione IMS]** - Tieni presente questo valore in quanto è necessario per configurare l’SDK per web di Platform.
* **[!UICONTROL Decisioning su dispositivo]** - Questa funzione non è supportata dall’SDK per web di Platform. Questa impostazione può essere disabilitata dopo la migrazione e se non utilizzi più at.js su nessuno dei tuoi siti web o se disponi di casi d’uso lato server per On-Device Decisioning.

#### [!UICONTROL Metodi di implementazione]

Tutte le impostazioni modificabili nel **[!UICONTROL Metodi di implementazione]** si applica solo a at.js. Queste impostazioni vengono utilizzate per generare una libreria at.js personalizzata per la tua implementazione. Controlla queste impostazioni per verificare se disponi di codice personalizzato o se stai impostando cookie di prima e terze parti per casi di utilizzo tra domini diversi.

La **[!UICONTROL Durata del profilo]** L’impostazione può essere modificata solo dall’Assistenza clienti di Adobe. La durata del profilo visitatore di Target non è influenzata dall’approccio di implementazione. Sia at.js che Platform Web SDK utilizzano la stessa durata del profilo visitatore.

#### [!UICONTROL Privacy]

* **[!UICONTROL Indirizzi IP offuscati del visitatore]** - Questa impostazione ha un impatto sulle funzionalità di geotargeting. Sia at.js che Platform Web SDK utilizzano le stesse impostazioni di offuscamento dell’IP di backend per il geotargeting.

### [!UICONTROL Ambienti]

L’SDK per web di Platform utilizza una configurazione del datastream che ti consente di definire in modo esplicito un [!UICONTROL ID ambiente] per flussi di dati di sviluppo, staging e produzione separati. Il caso d’uso principale di questa configurazione è per le implementazioni di app mobili in cui gli URL non esistono per distinguere facilmente gli ambienti. L’impostazione è facoltativa, ma può essere utilizzata per garantire che tutte le richieste siano correttamente associate all’ambiente specificato. Ciò è diverso da un’implementazione at.js in cui è necessario assegnare ambienti Target in base a domini e regole del gruppo host.

>[!NOTE]
>
>Se un ID ambiente non è specificato nella configurazione del datastream, Target utilizza la mappatura da dominio a ambiente come specificato nel **Host** sezione .

Per ulteriori informazioni, consulta la [configurazione di datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) Guida e Target [Host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) documentazione.

## Implementare l’SDK per web di Platform

La funzionalità di Target è fornita sia da at.js che da Platform Web SDK. Se entrambe le librerie vengono utilizzate contemporaneamente, potrebbero verificarsi problemi di rendering e tracciamento. Per eseguire correttamente la migrazione a Platform Web SDK, il primo passaggio consiste nel rimuovere at.js e sostituirlo con Platform Web SDK (alloy.js).

Supponiamo una semplice implementazione di Target con at.js:

* Un livello dati vicino alla parte superiore della pagina fornisce informazioni per Target e altre applicazioni
* Una o più librerie helper di terze parti le cui funzionalità possono essere utilizzate nelle attività di Target (ad esempio, jQuery)
* Un frammento pre-hiding per attenuare la visualizzazione momentanea di altri contenuti
* La libreria at.js di Target viene caricata in modo asincrono con le impostazioni predefinite per richiedere e eseguire automaticamente il rendering delle attività:

+++esempio at.js di un’implementazione in una pagina HTML

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Per aggiornare Target per utilizzare l’SDK per web di Platform, rimuovi prima at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

E sostituisci con la versione supportata corrente di Platform Web SDK (alloy.js):

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

La versione standalone predefinita richiede un &quot;codice base&quot; aggiunto direttamente alla pagina, che crea una funzione globale denominata alloy. Usa questa funzione per interagire con l&#39;SDK. Se si desidera assegnare alla funzione globale un nome diverso, modificare la `alloy` nome.

>[!TIP]
>
> Quando si utilizza la funzione tag (precedentemente Launch) per implementare l’SDK per web, la libreria alloy.js viene aggiunta alla libreria tag aggiungendo l’estensione Adobe Experience Platform Web SDK.


Fai riferimento a [Installazione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=it) documentazione per ulteriori dettagli e opzioni di distribuzione.


## Aggiorna l’approccio di pre-hiding del contenuto

L’implementazione dell’SDK per web di Platform può richiedere un frammento pre-hiding a seconda che la libreria venga caricata in modo asincrono o sincrono.

### Implementazione asincrona

Come con at.js, se la libreria SDK per web Platform viene caricata in modo asincrono, il rendering della pagina potrebbe terminare prima che Target abbia eseguito uno scambio di contenuto. Questo comportamento può causare il cosiddetto &quot;sfarfallio&quot;, in cui il contenuto predefinito viene visualizzato brevemente prima di essere sostituito dal contenuto personalizzato specificato da Target. Se desideri evitare questo sfarfallio, Adobe consiglia di aggiungere uno snippet speciale per il pre-hiding immediatamente prima del riferimento allo script SDK web per la piattaforma asincrona.

Se l’implementazione è asincrona come l’esempio precedente, sostituisci il frammento pre-hiding di at.js con la versione seguente compatibile con l’SDK per web di Platform:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

Il frammento pre-hiding crea un tag di stile nella parte superiore della pagina con la definizione CSS di tua scelta. Questo tag stile viene rimosso quando viene ricevuta una risposta da Target o viene raggiunto il timeout.

Il comportamento di pre-hiding è controllato da due configurazioni alla fine del frammento.

* `body { opacity: 0 !important }` specifica la definizione CSS da utilizzare per il pre-hiding fino al caricamento di Target. Per impostazione predefinita, l’intera pagina è nascosta. Puoi aggiornare questa definizione ai selettori che desideri nascondere in anteprima insieme a come desideri nasconderli. È possibile includere più definizioni in quanto questo valore è semplicemente ciò che viene inserito nel tag di stile pre-hiding. Se disponi di un elemento contenitore facilmente identificabile che racchiude il contenuto sotto la navigazione, puoi utilizzare questa impostazione per limitare il pre-hiding per quell’elemento contenitore.

* `3000` specifica il timeout in millisecondi per il pre-hiding. Se non viene ricevuta una risposta da Target prima del timeout, il tag di stile pre-hiding viene rimosso. Il raggiungimento di questo timeout dovrebbe essere raro.

>[!NOTE]
>
>Assicurati di utilizzare lo snippet corretto per l’SDK per web di Platform in quanto utilizza un ID di stile diverso di `alloy-prehiding`. Se si utilizza il frammento pre-hiding per at.js, potrebbe non funzionare correttamente.

### Implementazione sincrona

Adobe consiglia di implementare l’SDK per web di Platform in modo asincrono per ottenere le migliori prestazioni complessive della pagina. Tuttavia, se la libreria viene caricata in modo sincrono, lo snippet per il pre-hiding non è necessario. Lo stile del pre-hiding viene invece specificato nella configurazione SDK per web di Platform.

Lo stile di pre-hiding per le implementazioni sincrone può essere configurato utilizzando il [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) opzione . La configurazione dell’SDK per web di Platform è descritta nella sezione successiva.

Per ulteriori informazioni su come Platform Web SDK può gestire la visualizzazione momentanea di altri contenuti, consulta la sezione della guida :  [gestione della visualizzazione momentanea di altri contenuti per esperienze personalizzate](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Configurare l’SDK web per Platform

L’SDK per web di Platform deve essere configurato a ogni caricamento di pagina. L’esempio seguente presuppone che l’intero sito sia in fase di aggiornamento a Platform Web SDK in un’unica implementazione:

>[!BEGINTABS]

>[!TAB JavaScript]

La `configure` deve sempre essere il primo comando SDK chiamato. La `edgeConfigId` è [!UICONTROL ID Datastream]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Tag]

Nelle implementazioni dei tag, molti campi vengono compilati automaticamente o possono essere selezionati dai menu a discesa. Tieni presente che una piattaforma diversa [!UICONTROL sandbox] e [!UICONTROL datastreams] può essere selezionato per ogni ambiente. Il datastream cambierà in base allo stato della libreria di tag nel processo di pubblicazione.

![configurazione dell’estensione tag SDK per web](assets/tags-config.png){zoomable=&quot;yes&quot;}
>[!ENDTABS]

Se prevedi di migrare da at.js a Platform Web SDK a livello di pagina, sono necessarie le seguenti opzioni di configurazione:


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB Tag]

![configurazione delle opzioni di migrazione dell’estensione del tag SDK per web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}
>[!ENDTABS]

Le opzioni di configurazione valide per Target sono descritte di seguito:

| Opzione | Descrizione | Esempio di valore |
| --- | --- | --- |
| `edgeConfigId` | ID datastream | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID organizzazione Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Utilizza questa opzione per abilitare l’SDK per web per la lettura e scrittura dei cookie mbox e mboxEdgeCluster legacy utilizzati da at.js. In questo modo puoi mantenere il profilo del visitatore mentre passi da una pagina che utilizza l’SDK per web a una pagina che utilizza la libreria at.js e viceversa. | `true` |
| `idMigrationEnabled` | Se true, l&#39;SDK legge e imposta i cookie AMCV precedenti. Questa opzione aiuta nella transizione all’utilizzo di Platform Web SDK, mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Abilita l’impostazione di cookie di terze parti di Adobe. L&#39;SDK può mantenere l&#39;ID visitatore in un contesto di terze parti per consentire l&#39;utilizzo dello stesso ID visitatore nei diversi siti. Utilizzare questa opzione se si dispone di più siti; tuttavia, a volte questa opzione non è desiderata per motivi di privacy. | `true` |
| `prehidingStyle` | Utilizzato per creare una definizione di stile CSS che nasconde le aree contenuto della pagina web mentre il contenuto personalizzato viene caricato dal server. Viene utilizzato solo con le distribuzioni sincrone dell’SDK. | `body { opacity: 0 !important }` |

Per un elenco completo delle opzioni, fai riferimento alla sezione [configurazione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it) guida.

## Esempio di implementazione

Una volta che Platform Web SDK è stato implementato correttamente, la pagina di esempio sarà simile a questa.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB Tag]

Codice pagina:

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

Nei tag, aggiungi l’estensione Adobe Experience Platform Web SDK:

![Aggiungere l’estensione Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

E aggiungi le configurazioni desiderate:
![configurazione delle opzioni di migrazione dell’estensione del tag SDK per web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}


>[!ENDTABS]



È importante notare che la semplice inclusione e configurazione della libreria Platform Web SDK come mostrato sopra non esegue chiamate di rete alla rete Adobe Edge.

Quindi, scopri come [richiedere e applicare attività basate su VEC](render-vec-activities.md) alla pagina.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
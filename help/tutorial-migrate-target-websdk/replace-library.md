---
title: Sostituire la libreria - Migrare Target da at.js 2.x a Web SDK
description: Scopri come migrare un’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono panoramica della libreria, differenze di implementazione e altri callout degni di nota.
exl-id: dfafa132-376a-475d-a467-9bc2f0a414cf
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# Sostituire la libreria at.js con Platform Web SDK

Scopri come sostituire l’implementazione on-page di Adobe Target per la migrazione da at.js a Platform Web SDK. Una sostituzione di base è costituita dai seguenti passaggi:

* Verifica le impostazioni di amministrazione di Target e annota l’ID organizzazione IMS
* Sostituire la libreria at.js con Platform Web SDK
* Aggiorna il frammento pre-hiding per le implementazioni della libreria sincrona
* Configurare l’SDK web per Platform

>[!NOTE]
>
>Gli esempi forniti sono a scopo illustrativo e la tua effettiva implementazione di Target può variare. Se l&#39;implementazione di Target esistente utilizza il gestore di tag di Adobe Data Collection, puoi anche fare riferimento all&#39;esercitazione sull&#39;implementazione di [Platform Web SDK Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=it) per ulteriori informazioni.


## Verifica impostazioni di amministrazione di Target

Il primo passaggio per migrare Target a Platform Web SDK consiste nel rivedere le impostazioni nella sezione **[!UICONTROL Amministrazione]** dell&#39;interfaccia di Target.

### [!UICONTROL Implementazione]

#### [!UICONTROL Dettagli account]

* **[!UICONTROL ID organizzazione IMS]** - Prendere nota di questo valore poiché è necessario per configurare l&#39;SDK Web di Platform.
* **[!UICONTROL Decisioning sul dispositivo]** - Questa funzionalità non è supportata da Platform Web SDK. Questa impostazione può essere disabilitata dopo la migrazione e se non utilizzi più at.js su nessuno dei tuoi siti web o hai casi di utilizzo lato server per On-Device Decisioning.

#### [!UICONTROL Metodi di implementazione]

Tutte le impostazioni modificabili nella sezione **[!UICONTROL Metodi di implementazione]** sono valide solo per at.js. Queste impostazioni vengono utilizzate per generare una libreria at.js personalizzata per l’implementazione. Controlla queste impostazioni per verificare se hai un codice personalizzato o se stai impostando cookie di prima e terza parte per casi di utilizzo tra domini diversi.

L&#39;impostazione **[!UICONTROL Durata profilo]** può essere modificata solo dall&#39;Assistenza clienti Adobe. La durata del profilo del visitatore di Target non è influenzata dall’approccio di implementazione. Sia at.js che Platform Web SDK utilizzano la stessa durata del profilo visitatore.

#### [!UICONTROL Privacy]

* **[!UICONTROL Offusca indirizzi IP visitatore]** - Questa impostazione influisce sulle funzionalità di geotargeting. Sia at.js che Platform Web SDK utilizzano le stesse impostazioni di offuscamento dell’IP di back-end ai fini del geotargeting.

### [!UICONTROL Ambienti]

Platform Web SDK utilizza una configurazione dello stream di dati che ti consente di definire esplicitamente un [!UICONTROL ID ambiente] per flussi di dati di sviluppo, staging e produzione separati. Il caso d’uso principale per questa configurazione è per le implementazioni di app mobili in cui gli URL non esistono per distinguere facilmente gli ambienti. L’impostazione è facoltativa, ma può essere utilizzata per garantire che tutte le richieste siano associate correttamente all’ambiente specificato. Questo differisce da un’implementazione at.js in cui devi assegnare ambienti Target basati su domini e regole del gruppo di host.

>[!NOTE]
>
>Se nella configurazione dello stream di dati non è specificato un ID ambiente, Target utilizza la mappatura da dominio a ambiente specificata nella sezione **Host**.

Per ulteriori informazioni, consulta la [guida alla configurazione dello stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=it#target) e la documentazione di Target [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=it).

## Distribuire l’SDK web per Platform

La funzionalità di Target è fornita sia da at.js che da Platform Web SDK. Se entrambe le librerie vengono utilizzate contemporaneamente, potrebbero verificarsi problemi di rendering e tracciamento. Per eseguire correttamente la migrazione a Platform Web SDK, il primo passaggio consiste nel rimuovere at.js e sostituirlo con Platform Web SDK (alloy.js).

Supponiamo una semplice implementazione di Target con at.js:

* Un livello dati nella parte superiore della pagina fornisce informazioni per Target e altre applicazioni
* Una o più librerie helper di terze parti le cui funzionalità possono essere utilizzate nelle attività di Target (ad esempio, jQuery)
* Frammento pre-hiding per attenuare lo sfarfallio
* La libreria at.js di Target viene caricata in modo asincrono con le impostazioni predefinite per richiedere ed eseguire il rendering automatico delle attività:

+++Implementazione di esempio di at.js su una pagina HTML

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

Per aggiornare Target per utilizzare Platform Web SDK, rimuovi prima at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

E sostituisci con la libreria JavsScript di lega o con il codice da incorporare dei tag e l’estensione Adobe Experience Platform Web SDK:

>[!BEGINTABS]

>[!TAB JavaScript]

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

>[!TAB Tag]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

Nella proprietà tag, aggiungi l’estensione Adobe Experience Platform Web SDK:

![Aggiungere l&#39;estensione Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable="yes"}


>[!ENDTABS]

La versione standalone precompilata richiede un &quot;codice di base&quot; aggiunto direttamente alla pagina, che crea una funzione globale denominata alloy. Utilizza questa funzione per interagire con l’SDK. Se si desidera assegnare un altro nome alla funzione globale, modificare il nome `alloy`.

Per ulteriori informazioni e opzioni di distribuzione, consultare la documentazione [Installazione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=it).


## Aggiornamento dell’approccio per pre-hiding dei contenuti

L’implementazione di Platform Web SDK può richiedere uno snippet per nascondere il contenuto, a seconda che la libreria venga caricata in modo asincrono o sincrono.

### Implementazione asincrona

Proprio come con at.js, se la libreria dell’SDK web di Platform viene caricata in modo asincrono, il rendering della pagina potrebbe terminare prima che Target abbia eseguito uno scambio di contenuti. Questo comportamento può causare il cosiddetto &quot;sfarfallio&quot;, in cui il contenuto predefinito viene visualizzato brevemente prima di essere sostituito dal contenuto personalizzato specificato da Target. Per evitare questo sfarfallio, l’Adobe consiglia di aggiungere uno speciale frammento pre-hiding immediatamente prima del riferimento asincrono allo script di Platform Web SDK o del codice di incorporamento dei tag.

Se l’implementazione è asincrona come negli esempi precedenti, sostituisci il frammento pre-hiding di at.js con la versione seguente compatibile con Platform Web SDK:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Il frammento pre-hiding crea un tag di stile nella parte superiore della pagina con la definizione CSS desiderata. Questo tag di stile viene rimosso quando viene ricevuta una risposta da Target o quando viene raggiunto il timeout.

Il comportamento di pre-hiding è controllato da due configurazioni alla fine del frammento.

* `body { opacity: 0 !important }` specifica la definizione CSS da utilizzare per il pre-hiding fino al caricamento di Target. Per impostazione predefinita, l’intera pagina è nascosta. È possibile aggiornare questa definizione ai selettori che si desidera prenascondere e alla modalità di visualizzazione. Puoi includere più definizioni poiché questo valore è semplicemente ciò che viene inserito nel tag di stile pre-hiding. Se il contenuto sottostante la navigazione è racchiuso in un elemento contenitore facilmente identificabile, puoi utilizzare questa impostazione per limitare il pre-hiding per tale elemento contenitore.

* `3000` specifica il timeout in millisecondi per il pre-hiding. Se una risposta da Target non viene ricevuta prima del timeout, il tag di stile pre-hiding viene rimosso. Il raggiungimento di questo timeout dovrebbe essere raro.

>[!IMPORTANT]
>
>Assicurarsi di utilizzare lo snippet corretto per Platform Web SDK poiché utilizza un ID di stile diverso di `alloy-prehiding`. Se si utilizza il frammento pre-hiding per at.js, potrebbe non funzionare correttamente.

### Implementazione sincrona

L’Adobe consiglia di implementare Platform Web SDK in modo asincrono, per ottenere le migliori prestazioni complessive della pagina. Tuttavia, se la libreria alloy.js o il codice di incorporamento dei tag viene caricato in modo sincrono, lo snippet per nascondere il contenuto non è necessario. Invece, lo stile di pre-hiding è specificato nella configurazione di Platform Web SDK.

Lo stile di pre-hiding per le implementazioni sincrone può essere configurato utilizzando l&#39;opzione [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it#prehidingStyle). La configurazione di Platform Web SDK è descritta nella sezione successiva.

Per ulteriori informazioni su come Platform Web SDK può gestire la visualizzazione momentanea di altri contenuti, consulta la sezione guida: [gestione della visualizzazione momentanea di altri contenuti per esperienze personalizzate](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html?lang=it)

## Configurare l’SDK web per Platform

Platform Web SDK deve essere configurato a ogni caricamento di pagina. L’esempio seguente presuppone che l’intero sito venga aggiornato a Platform Web SDK in una singola implementazione:

>[!BEGINTABS]

>[!TAB JavaScript]

Il comando `configure` deve essere sempre il primo comando SDK chiamato. `edgeConfigId` è l&#39;[!UICONTROL ID Datastream]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Tag]

Nelle implementazioni dei tag, molti campi sono compilati automaticamente o possono essere selezionati dai menu a discesa. Per ogni ambiente è possibile selezionare [!UICONTROL sandbox] e [!UICONTROL flussi di dati] diversi per Platform. Lo stream di dati cambia in base allo stato della libreria di tag nel processo di pubblicazione.

![configurazione dell&#39;estensione tag Web SDK](assets/tags-config.png){zoomable="yes"}
>[!ENDTABS]

Se prevedi di migrare da at.js a Platform Web SDK pagina per pagina, sono necessarie le seguenti opzioni di configurazione:


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

![configurazione delle opzioni di migrazione dell&#39;estensione tag Web SDK](assets/tags-config-migration.png){zoomable="yes"}

>[!ENDTABS]

Di seguito sono descritte le opzioni di configurazione rilevanti relative a Target:

| Opzione | Descrizione | Esempio di valore |
| --- | --- | --- |
| `edgeConfigId` | ID dello stream di dati | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID organizzazione Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Utilizza questa opzione per abilitare Web SDK per leggere e scrivere i cookie mbox e mboxEdgeCluster legacy utilizzati da at.js. Questo ti aiuta a mantenere il profilo visitatore mentre ti sposti da una pagina che utilizza l’SDK per web a una pagina che utilizza la libreria at.js e viceversa. | `true` |
| `idMigrationEnabled` | Se true, l&#39;SDK legge e imposta i cookie AMCV precedenti. Questa opzione facilita la transizione all’utilizzo di Platform Web SDK, mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Abilita l’impostazione di cookie di terze parti Adobe. L&#39;SDK può rendere persistente l&#39;ID visitatore in un contesto di terze parti per consentire l&#39;utilizzo dello stesso ID visitatore in più siti. Utilizza questa opzione se hai più siti; tuttavia, a volte questa opzione non è desiderata per motivi di privacy. | `true` |
| `prehidingStyle` | Utilizzato per creare una definizione di stile CSS che nasconde le aree di contenuto della pagina web mentre il contenuto personalizzato viene caricato dal server. Viene utilizzato solo con le distribuzioni sincrone dell’SDK. | `body { opacity: 0 !important }` |

Per un elenco completo delle opzioni, consulta la guida [configurazione di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it).

## Esempio di implementazione

Una volta che Platform Web SDK è correttamente posizionato, la pagina di esempio si presenta così.

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

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
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

In tag, aggiungi l’estensione Adobe Experience Platform Web SDK:

![Aggiungere l&#39;estensione Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable="yes"}

E aggiungi le configurazioni desiderate:
![configurazione delle opzioni di migrazione dell&#39;estensione tag Web SDK](assets/tags-config-migration.png){zoomable="yes"}


>[!ENDTABS]



È importante notare che l’inclusione e la configurazione della libreria Platform Web SDK, come mostrato sopra, non eseguono chiamate di rete alla rete Adobe Edge.

Quindi, scopri come [richiedere e applicare alla pagina le attività basate sul Compositore esperienza visivo](render-vec-activities.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=it#M463).

---
title: Configurare Adobe Target con Platform Web SDK
description: Scopri come implementare Adobe Target utilizzando Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
solution: Data Collection, Target
exl-id: 9084f572-5fec-4a26-8906-6d6dd1106d36
source-git-commit: 13f2c87d7c4cfe21f04a945b9e11dc64e9bf6e0c
workflow-type: tm+mt
source-wordcount: '3801'
ht-degree: 1%

---

# Configurare Adobe Target con Platform Web SDK

Scopri come implementare Adobe Target utilizzando Platform Web SDK. Scopri come distribuire esperienze e come trasmettere parametri aggiuntivi a Target.

[Adobe Target](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) è l’applicazione Adobe Experience Cloud che offre tutto il necessario per adattare e personalizzare l’esperienza dei clienti in modo da massimizzare i ricavi sui siti web e mobili, applicazioni e altri canali digitali.


## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Scopri come aggiungere il frammento pre-hiding dell’SDK per web Platform per evitare sfarfallii durante l’utilizzo di Target con codici di incorporamento tag asincroni
* Configurare un datastream per abilitare la funzionalità di Target
* Prendere decisioni di personalizzazione visiva al caricamento della pagina (precedentemente denominata &quot;mbox globale&quot;)
* Trasmettere i dati XDM a Target e comprendere la mappatura ai parametri di Target
* Trasmettere dati personalizzati a Target, ad esempio parametri di profilo ed entità
* Convalidare un’implementazione di Target con Platform Web SDK

>[!TIP]
>
>Consulta le nostre [Migrare Target da at.js 2.x a Platform Web SDK](/help/tutorial-migrate-target-websdk/introduction.md) tutorial per una guida dettagliata per migrare l’implementazione at.js esistente.


## Prerequisiti

Per completare le lezioni in questa sezione, devi prima:

* Completa tutte le lezioni per la configurazione iniziale dell’SDK per web di Platform, inclusa l’impostazione di elementi dati e regole.
* Assicurati di disporre di un [Ruolo editor o approvatore](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80).
* Installa il [Estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) se utilizzi il browser Google Chrome.
* Scopri come impostare le attività in Target. Se hai bisogno di un aggiornamento, le seguenti esercitazioni e guide sono utili per questa lezione:
   * [Utilizzare l’estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)
   * [Utilizzare il Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Utilizzare il Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Creare attività di targeting delle esperienze](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

## Aggiunta dell&#39;attenuazione della visualizzazione momentanea di altri contenuti

Prima di iniziare, determina se è necessaria una soluzione di gestione della visualizzazione momentanea di altri contenuti a seconda di come viene caricata la libreria di tag.

>[!NOTE]
>
>Questa esercitazione utilizza la funzione [Sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) che dispone di un’implementazione asincrona dei tag e della mitigazione della visualizzazione momentanea di altri contenuti. Questa sezione è utile per comprendere come funziona l’attenuazione della visualizzazione momentanea di altri contenuti con Platform Web SDK.


### Implementazione asincrona

Quando una libreria di tag viene caricata in modo asincrono, la pagina potrebbe terminare il rendering prima che Target abbia eseguito uno scambio di contenuto. Questo comportamento può causare il cosiddetto &quot;sfarfallio&quot;, in cui il contenuto predefinito viene visualizzato brevemente prima di essere sostituito dal contenuto personalizzato specificato da Target. Per evitare questo sfarfallio, Adobe consiglia di aggiungere uno speciale frammento pre-hiding immediatamente prima del codice di incorporamento del tag asincrono .

Questo frammento è già presente sul sito Luma, ma diamo un&#39;occhiata più da vicino per capire cosa fa questo codice:

```html
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

* `body { opacity: 0 !important }` specifica la definizione CSS da utilizzare per il pre-hiding fino al caricamento di Target. Per impostazione predefinita, l’intera pagina è nascosta. Puoi aggiornare questa definizione ai selettori che desideri nascondere anticipatamente, insieme a come desideri nasconderli. È possibile includere più definizioni, in quanto questo valore è semplicemente ciò che viene inserito nel tag di stile pre-hiding. Se disponi di un elemento contenitore facilmente identificabile che racchiude il contenuto sotto la navigazione, puoi utilizzare questa impostazione per limitare il pre-hiding per quell’elemento contenitore.
* `3000` specifica il timeout in millisecondi per il pre-hiding. Se una risposta da Target non viene ricevuta prima del timeout, il tag di stile pre-hiding viene rimosso. Il raggiungimento di questo timeout dovrebbe essere raro.

>[!NOTE]
>
>Il frammento pre-hiding per Platform Web SDK è leggermente diverso da quello utilizzato con la libreria at.js di Target. Assicurati di utilizzare lo snippet corretto per l’SDK per web di Platform in quanto utilizza un ID di stile diverso di `alloy-prehiding`. Se si utilizza il frammento pre-hiding per at.js, potrebbe non funzionare correttamente.

Il frammento pre-hiding è disponibile anche all’interno dei tag :

1. Vai a **[!UICONTROL Estensioni]** sezione tag
1. Seleziona **[!UICONTROL Configura]** per l&#39;estensione Adobe Experience Platform Web SDK
1. Seleziona la **[!UICONTROL Copia frammento pre-hiding negli Appunti]** pulsante

   ![Frammento pre-hiding di Target per le implementazioni asincrone](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >Lo snippet predefinito copiato dall’estensione Platform Web SDK può includere una definizione CSS non esistente sul sito, ad esempio `.personalization-container { opacity: 0 !important }`. Controlla e modifica il frammento pre-hiding in modo appropriato per il tuo sito.

### Implementazione sincrona

Adobe consiglia di implementare i tag in modo asincrono, come illustrato sul sito Luma. Tuttavia, se la libreria di tag viene caricata in modo sincrono, lo snippet per nascondere il contenuto non è necessario. Lo stile pre-hiding viene invece specificato nelle impostazioni dell’estensione Platform Web SDK.

Lo stile pre-hiding per le implementazioni sincrone può essere configurato come segue:

1. Vai a **[!UICONTROL Estensioni]** sezione tag
1. Seleziona la **[!UICONTROL Configura]** per l’estensione Platform Web SDK
1. Seleziona la **[!UICONTROL Modificare lo stile pre-hiding]** pulsante

   ![Frammento pre-hiding di Target per le implementazioni asincrone](assets/target-flicker-sync.png)

1. Modifica il CSS in modo da includere i selettori e i metodi di eliminazione desiderati, ad esempio: `body { opacity: 0 !important }` per nascondere anticipatamente l’intero corpo della pagina.
1. Salvare le modifiche e generarle in una libreria

>[!NOTE]
>
>L’impostazione dello stile pre-hiding è destinata solo alle implementazioni sincrone. Se utilizzi un’implementazione asincrona dei tag, questo stile deve essere vuoto o commentato.

Per ulteriori informazioni su come Platform Web SDK può gestire la visualizzazione momentanea di altri contenuti, consulta la sezione della guida : [gestione della visualizzazione momentanea di altri contenuti per esperienze personalizzate](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).


## Configurare il datastream

Target deve essere abilitato nella configurazione del datastream prima che qualsiasi attività Target possa essere distribuita dall’SDK per web di Platform.

Per configurare Target nel datastream:

1. Vai a [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"} interfaccia
1. Nella navigazione a sinistra, seleziona **[!UICONTROL Datastreams]**
1. Seleziona il creato in precedenza `Luma Web SDK` datastream

   ![Seleziona il datastream Luma Web SDK](assets/datastream-luma-web-sdk.png)

1. Seleziona **[!UICONTROL Aggiungi servizio]**

   ![Aggiungi un servizio al datastream](assets/target-datastream-addService.png)
1. Seleziona **[!UICONTROL Adobe Target]** come **[!UICONTROL Servizio]**
1. Immetti i dettagli facoltativi sull’implementazione di Target, se desiderato, seguendo le indicazioni riportate di seguito.
1. Seleziona **[!UICONTROL Salva]**

   ![Configurazione del datastream di Target](assets/target-datastream.png)

### Token di proprietà

I clienti Target Premium possono gestire le autorizzazioni utente con le proprietà. Le proprietà di Target ti consentono di stabilire limiti intorno ai quali gli utenti possono eseguire attività di Target. Fai riferimento a [Autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) per ulteriori informazioni, consulta la sezione della documentazione di Target .

Per impostare o trovare i token di proprietà, passa a **Adobe Target** > **[!UICONTROL Amministrazione]** > **[!UICONTROL Proprietà]**. La `</>` visualizza il codice di implementazione. La `at_property` value è il token di proprietà da utilizzare nel datastream.

![Token di proprietà di Target](assets/target-admin-properties.png)

>[!NOTE]
>
>È possibile specificare un solo token di proprietà per ogni datastream.


### ID ambiente di destinazione

[Ambienti](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) in Target puoi gestire la tua implementazione in tutte le fasi di sviluppo. Questa impostazione opzionale specifica l’ambiente Target da utilizzare con ogni datastream.

Adobe consiglia di impostare l’ID dell’ambiente di Target in modo diverso per ogni datastreams di sviluppo, staging e produzione, in modo da semplificare le operazioni.

Per impostare o trovare gli ID ambiente, passa a **Adobe Target** > **[!UICONTROL Amministrazione]** > **[!UICONTROL Ambienti]**.

![Ambienti di destinazione](assets/target-admin-environments.png)

>[!NOTE]
>
>Se non viene specificato alcun ID ambiente di Target, viene assunto l&#39;ambiente di produzione di Target.

### Spazio dei nomi ID di terze parti di Target

Questa impostazione opzionale consente di specificare quale simbolo di identità utilizzare per l’ID di terze parti di Target. Target supporta solo la sincronizzazione dei profili su un singolo simbolo di identità o spazio dei nomi. Per ulteriori informazioni, consulta la sezione [Sincronizzazione dei profili in tempo reale per mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) della guida di Target.

I Simboli di identità si trovano nell&#39;elenco delle identità in **Raccolta dati** > **[!UICONTROL Cliente]** > **[!UICONTROL Identità]**.

![Elenco identità](assets/target-identities.png)

Ai fini di questa esercitazione tramite il sito Luma, utilizza il simbolo di identità `lumaCrmId` durante la lezione [Identità](configure-identities.md).


## Decisioni relative alla personalizzazione visiva del rendering

In primo luogo, è necessario comprendere la terminologia utilizzata nelle interfacce Target e tag.

* **Attività**: Un set di esperienze mirate per uno o più tipi di pubblico. Ad esempio, un semplice test A/B potrebbe essere un’attività con due esperienze.
* **Esperienza**: Un insieme di azioni mirate a una o più posizioni o ambiti decisionali.
* **Campo di applicazione**: Una posizione in cui viene distribuita l’esperienza Target. Gli ambiti decisionali equivalgono a &quot;mbox&quot; se hai dimestichezza con l’utilizzo di versioni precedenti di Target.
* **Decisione di personalizzazione**: Deve essere applicata un&#39;azione determinata dal server. Queste decisioni possono essere basate su criteri di pubblico e sulla definizione delle priorità delle attività di Target.
* **Proposta**: Il risultato delle decisioni prese dal server e distribuite nella risposta Platform Web SDK. Ad esempio, lo scambio di un&#39;immagine del banner sarebbe una proposta.

### Aggiorna la regola di caricamento della pagina

Le decisioni di personalizzazione visiva da Target vengono distribuite dall’SDK per web di Platform, se Target è abilitato nel datastream. Tuttavia, _non vengono riprodotti automaticamente_. Per abilitare il rendering automatico, devi modificare la regola di caricamento della pagina globale.

1. In [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"} , apri la proprietà tag utilizzata per questa esercitazione.
1. Apri `all pages - library load - AA & AT` regola
1. Seleziona la `Adobe Experience Platform Web SDK - Send event` action
1. Abilita **[!UICONTROL Decisioni relative alla personalizzazione visiva del rendering]** con la casella di controllo

   ![Abilitare il rendering delle decisioni di personalizzazione visiva](assets/target-rule-enable-visual-decisions.png)

1. Salva le modifiche e genera nella libreria

L’impostazione relativa alle decisioni di personalizzazione visiva del rendering fa sì che Platform Web SDK applichi automaticamente tutte le modifiche specificate utilizzando il Compositore esperienza visivo di Target o la &quot;mbox globale&quot;.

>[!NOTE]
>
>In genere, il [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] deve essere abilitata solo per una singola azione Invia evento per caricamento completo della pagina. Se questa impostazione è abilitata per più azioni Invia evento , le richieste di rendering successive vengono ignorate.

Se preferisci eseguire il rendering o intervenire direttamente su queste decisioni utilizzando il codice personalizzato, puoi lasciare la [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] impostazione disabilitata. L’SDK per web di Platform è flessibile e offre questa funzionalità per consentirti di esercitare un controllo completo. Per ulteriori informazioni su , consulta la guida [rendering manuale di contenuti personalizzati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html).

### Configurare un’attività Target con il Compositore esperienza visivo

Una volta completata la porzione di implementazione di base, crea un’attività Targeting esperienza (XT) in Target per verificare che tutto funzioni correttamente. È possibile fare riferimento all’esercitazione di Target per [creazione di attività di targeting delle esperienze](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html) se hai bisogno di assistenza.

>[!NOTE]
>
>Se utilizzi Google Chrome come browser, la [Estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) è necessario caricare correttamente il sito per la modifica nel Compositore esperienza visivo.

1. Passa a Target
1. Creare un’attività Targeting esperienze (XT) utilizzando la home page Luma per l’URL attività

   ![Creare una nuova attività Targeting esperienza](assets/target-xt-create-activity.png)

1. Modificare la pagina, ad esempio modificare il testo nel banner della home page

   ![Modifica del Compositore esperienza visivo di Target](assets/target-xt-vec-modification.png)

1. Scegli Adobe Analytics come origine per la generazione di rapporti con la suite di rapporti appropriata e la metrica Ordini come obiettivo

   >[!NOTE]
   >
   >Se non utilizzi Adobe Analytics, seleziona Target come origine per la generazione di rapporti e scegli una metrica diversa come **Coinvolgimento > Visualizzazioni pagina** invece. È necessaria una metrica di obiettivo per salvare e visualizzare in anteprima l’attività.

1. Salva l’attività
1. Se hai familiarità con le modifiche, puoi attivare l’attività. In caso contrario, se desideri visualizzare un’anteprima dell’esperienza senza attivarla, puoi copiare il [URL anteprima controllo qualità](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Carica la home page di Luma e dovresti vedere le modifiche applicate
1. Dopo alcune ore, dovresti essere in grado di visualizzare i dati e le conversioni delle attività di Target in Adobe Analytics. Per informazioni dettagliate su [Reporting di Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/reporting.html?lang=en).



### Convalida con Debugger

Se imposti un’attività , dovresti visualizzare il rendering del contenuto nella pagina. Tuttavia, anche se non sono presenti attività, puoi anche guardare la chiamata di rete Invia evento per confermare che Target è configurato correttamente.

>[!CAUTION]
>
>Se utilizzi Google Chrome e hai [Estensione helper del Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) installati, assicurarsi che **Inserisci librerie di Target** è disabilitata. L’abilitazione di questa impostazione darà luogo a richieste Target aggiuntive.

1. Apri l’estensione del browser Adobe Experience Platform Debugger.
1. Vai a [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e utilizza il debugger per [imposta la proprietà tag del sito sulla proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Ricarica la pagina
1. Seleziona la **[!UICONTROL Rete]** strumento nel debugger
1. Filtra per **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleziona il valore nella riga eventi per la prima chiamata

   ![Chiamata di rete nel debugger di Adobe Experience Platform](assets/target-debugger-network.png)

1. Tieni presente che sono presenti le chiavi in `query` > `personalization` e  `decisionScopes` ha un valore di `__view__`. Questo ambito equivale alla &quot;mbox globale&quot; di Target. Questa chiamata Platform Web SDK ha richiesto le decisioni da Target.

   ![__visualizzare__ richiesta decisionScope](assets/target-debugger-view-scope.png)

1. Chiudi la sovrapposizione e seleziona i dettagli dell’evento per la seconda chiamata di rete. Questa chiamata è presente solo se Target ha restituito un’attività .
1. Tieni presente che esistono dettagli sull’attività e sull’esperienza restituite da Target. Questa chiamata Platform Web SDK invia una notifica che informa che è stato eseguito il rendering di un’attività Target per l’utente e incrementa un’impression.

   ![Immagine dell’attività di Target](assets/target-debugger-activity-impression.png)

## Impostare ed eseguire il rendering di un ambito decisionale personalizzato

Gli ambiti decisionali personalizzati (precedentemente noti come &quot;mbox&quot;) possono essere utilizzati per distribuire contenuti HTML o JSON in modo strutturato utilizzando il Compositore esperienza basato su moduli di Target. Il contenuto consegnato a uno di questi ambiti personalizzati non viene rappresentato automaticamente dall’SDK per web di Platform.

### Aggiungi un ambito alla regola di caricamento della pagina

Modifica la regola di caricamento della pagina per aggiungere un ambito decisionale personalizzato:

1. Apri `all pages - library load - AA & AT` regola
1. Seleziona la `Adobe Experience Platform Web SDK - Send Event` action
1. Aggiungi uno o più ambiti da utilizzare. Per questo esempio, utilizza `homepage-hero`.

   ![Ambito personalizzato](assets/target-rule-custom-scope.png)

1. Salva le modifiche e genera nella libreria

>[!TIP]
>
>Per questa esercitazione, utilizzerai un singolo ambito definito manualmente a scopo dimostrativo. Se si decide di utilizzare diversi ambiti decisionali destinati a pagine specifiche, è consigliabile utilizzare un elemento dati che restituisce un array di ambiti in modo condizionato a seconda del percorso della pagina. Questo approccio consente di mantenere l’implementazione semplice e scalabile.

### Elabora la risposta da Target

Ora che hai configurato Platform Web SDK per richiedere il contenuto per `homepage-hero` obbiettivo, devi fare qualcosa con la risposta. L’estensione tag SDK per web di Platform fornisce un [!UICONTROL Invia evento completato] evento che può essere utilizzato per attivare immediatamente una nuova regola quando una risposta da un [!UICONTROL Invia evento] viene ricevuta un&#39;azione.

1. Creare una regola denominata `homepage - send event complete - render homepage-hero`.
1. Aggiungi un evento alla regola. Utilizza la **Adobe Experience Platform Web SDK** e **[!UICONTROL Invia evento completato]** tipo di evento.
1. Aggiungi una condizione per limitare la regola alla home page di Luma (il percorso senza stringa di query è uguale a `/content/luma/us/en.html`).
1. Aggiungi un&#39;azione alla regola. Utilizza la **Core** estensione e **Codice personalizzato** tipo di azione.

   ![Rendering della regola eroe della homepage](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >Assegna nomi descrittivi agli eventi, alle condizioni e alle azioni della regola anziché utilizzare i nomi predefiniti. I nomi affidabili dei componenti delle regole rendono i risultati di ricerca molto più utili.

1. Immetti un codice personalizzato per leggere e intervenire sulle proposte restituite dalla risposta Platform Web SDK. Il codice personalizzato in questo esempio utilizza l’approccio descritto nella guida per [rendering manuale di contenuti personalizzati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#manually-rendering-content). Il codice è stato adattato per `homepage-hero` ambito di esempio utilizzando un&#39;azione regola di tag.

   ```javascript
   var propositions = event.propositions;
   
   var heroProposition;
   if (propositions) {
      // Find the hero proposition, if it exists.
      for (var i = 0; i < propositions.length; i++) {
         var proposition = propositions[i];
         if (proposition.scope === "homepage-hero") {
            heroProposition = proposition;
            break;
         }
      }
   }
   
   var heroHtml;
   if (heroProposition) {
      // Find the item from proposition that should be rendered.
      // Rather than assuming there a single item that has HTML
      // content, find the first item whose schema indicates
      // it contains HTML content.
      for (var j = 0; j < heroProposition.items.length; j++) {
         var heroPropositionItem = heroProposition.items[j];
         if (heroPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
            heroHtml = heroPropositionItem.data.content;
            break;
         }
      }
   }
   
   if (heroHtml) {
      // Hero HTML exists. Time to render it.
      var heroElement = document.querySelector(".heroimage");
      heroElement.innerHTML = heroHtml;
      // For this example, we assume there is only a signle place to update in the HTML.
   }
   
   // Send a "display" event 
   alloy("sendEvent", {
      xdm: {
         eventType: "propositionDisplay",
         _experience: {
            decisioning: {
               propositions: [
                  {
                     id: heroProposition.id,
                     scope: heroProposition.scope,
                     scopeDetails: heroProposition.scopeDetails
                  }
               ]
            }
         }
      }
   });
   ```

1. Salva le modifiche e genera nella libreria
1. Carica la home page di Luma alcune volte, che dovrebbe essere sufficiente per creare il nuovo `homepage-hero` registro dell’ambito decisionale nell’interfaccia di Target.

### Configurare un’attività Target con il Compositore esperienza basato su moduli

Ora che disponi di una regola per eseguire manualmente il rendering di un ambito decisionale personalizzato, puoi creare un’altra attività Targeting esperienza (XT) in Target. Questa volta utilizza il Compositore esperienza basato su moduli.

1. Apri [Adobe Target](https://experience.adobe.com/target)
1. Disattiva l’attività utilizzata per la lezione precedente
1. Creare un’attività Targeting esperienza (XT) utilizzando l’opzione Compositore esperienza basato su moduli

   ![Creare una nuova attività Targeting esperienza](assets/target-xt-create-form-activity.png)

1. Seleziona la **`homepage-hero`** dal menu a discesa posizione e **[!UICONTROL Crea offerta HTML]** dall’elenco a discesa del contenuto . Se la posizione non è disponibile, puoi immetterla. Target compila periodicamente nuovi nomi di posizione dopo aver ricevuto richieste per tale posizione o ambito.

   ![Creare una nuova attività Targeting esperienza](assets/target-xt-form-activity.png)

1. Incolla il seguente codice nella casella del contenuto. Questo codice è un banner eroe di base con un&#39;immagine di sfondo diversa:

   ```html
   <div class="we-HeroImage jumbotron" style="background-image: url('/content/luma/us/en/women/_jcr_content/root/hero_image.coreimg.jpeg');">
      <div class="container cq-dd-image">
         <div class="we-HeroImage-wrapper">
            <p class="h3">New Luma Yoga Collection</p>
            <strong class="we-HeroImage-title h1">Be active with style&nbsp;</strong>
            <p>
               <a class="btn btn-primary btn-action" href="/content/luma/us/en/products.html" role="button">Shop Now</a>
            </p>
         </div>
      </div>
   </div>
   ```

1. Sulla [!UICONTROL Obiettivi e impostazioni] scegli Adobe Target come origine per la generazione di rapporti e [!UICONTROL Coinvolgimento] > [!UICONTROL Visualizzazioni pagina] come obiettivo
1. Salva l’attività
1. Se hai familiarità con le modifiche, puoi attivare l’attività. In caso contrario, se desideri visualizzare un’anteprima dell’esperienza senza attivarla, puoi copiare il [URL anteprima controllo qualità](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Carica la home page di Luma e dovresti vedere le modifiche applicate

>[!NOTE]
>
>L’obiettivo di conversione &quot;Click on mbox&quot; non funziona automaticamente. Poiché Platform Web SDK non esegue automaticamente il rendering degli ambiti personalizzati, non tiene traccia dei clic sulle posizioni selezionate per applicare il contenuto. Puoi creare un tracciamento dei clic personalizzato per ogni ambito utilizzando il &quot;clic&quot; `eventType` con il `_experience` i dettagli utilizzando `sendEvent` azione.

### Convalida con Debugger

Se hai attivato l’attività, dovresti visualizzare il rendering del contenuto nella pagina. Tuttavia, anche se non sono presenti attività, puoi anche esaminare [!UICONTROL Invia evento] chiamata di rete per confermare che Target richiede contenuto per gli ambiti personalizzati.

1. Apri l’estensione del browser Adobe Experience Platform Debugger.
1. Vai a [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e utilizza il debugger per [imposta la proprietà tag del sito sulla proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Ricarica la pagina
1. Seleziona la **[!UICONTROL Rete]** strumento nel debugger
1. Filtra per **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleziona il valore nella riga eventi per la prima chiamata

   ![Chiamata di rete nel debugger di Adobe Experience Platform](assets/target-debugger-network.png)

1. Tieni presente che sono presenti le chiavi in `query` > `personalization` e  `decisionScopes` ha un valore di `__view__` come prima, ma ora c&#39;è anche un `homepage-hero` ambito di applicazione incluso. Questa chiamata Platform Web SDK ha richiesto a Target le decisioni relative alle modifiche effettuate utilizzando il Compositore esperienza visivo e il `homepage-hero` posizione.

   ![__visualizzare__ richiesta decisionScope](assets/target-debugger-view-scope.png)

1. Chiudi la sovrapposizione e seleziona i dettagli dell’evento per la seconda chiamata di rete. Questa chiamata è presente solo se Target ha restituito un’attività .
1. Tieni presente che esistono dettagli sull’attività e sull’esperienza restituite da Target. Questa chiamata Platform Web SDK invia una notifica che informa che è stato eseguito il rendering di un’attività Target per l’utente e incrementa un’impression.

   ![Immagine dell’attività di Target](assets/target-debugger-activity-impression.png)

## Trasmettere dati aggiuntivi a Target

In questa sezione, trasmetterai dati specifici di Target e analizzerai più da vicino come i dati XDM vengono mappati ai parametri di Target.

Ci sono alcuni punti di dati che possono essere utili per Target che non sono mappati dall&#39;oggetto XDM. Questi parametri speciali di Target includono:

* [Attributi del profilo](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/in-page-profile-attributes.html?lang=en)
* [Attributi di entità Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en)
* [Parametri riservati Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=en#pass-behavioral)
* Valori delle categorie per [affinità tra categorie](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=en)

### Creare elementi dati per i parametri di Target

Innanzitutto, imposterai alcuni elementi di dati aggiuntivi per un attributo di profilo, un attributo di entità, un valore di categoria e quindi costruirai `data` oggetto utilizzato per trasmettere dati non XDM:

* **`target.entity.id`** mappato su `digitalData.product.0.productInfo.sku`
* **`target.entity.name`** mappato su `digitalData.product.0.productInfo.title`
* **`target.user.categoryId`** utilizzando il seguente codice personalizzato per analizzare l’URL del sito per la categoria di livello principale:

   ```javascript
   var cat = location.pathname.split(/[/.]+/);
   if (cat[5] == 'products') {
      return (cat[6]);
   } else if (cat[5] != 'html') { 
      return (cat[5]);
   }
   ```

* **`data.content`** utilizzando il seguente codice personalizzato:

   ```javascript
   var data = {
      __adobe: {
         target: {
            "entity.id": _satellite.getVar("target.entity.id"),
            "entity.name": _satellite.getVar("target.entity.name"),
            "profile.loggedIn": _satellite.getVar("user.profile.attributes.loggedIn"),
            "user.categoryId": _satellite.getVar("target.user.categoryId")
         }
      }
   }
   return data;
   ```

### Aggiorna la regola di caricamento della pagina

Per trasmettere dati aggiuntivi per Target al di fuori dell’oggetto XDM è necessario aggiornare tutte le regole applicabili. Per questo esempio, l’unica modifica da apportare è quella di includere il nuovo **data.content** elemento dati alla regola di caricamento pagina generica e alla regola di visualizzazione pagina prodotto.

1. Apri `all pages - library load - AA & AT` regola
1. Seleziona la `Adobe Experience Platform Web SDK - Send event` action
1. Aggiungi il `data.content` elemento dati nel campo Dati

   ![Aggiungere dati di Target alla regola](assets/target-rule-data.png)

1. Salva le modifiche e genera nella libreria
1. Ripetere i passaggi da 1 a 4 per **visualizzazione prodotto - Caricamento libreria - AA** regola

>[!NOTE]
>
>L&#39;esempio precedente utilizza un `data` oggetto non completamente popolato su tutti i tipi di pagina. I tag gestiscono in modo appropriato questa situazione e omettono le chiavi con un valore non definito. Ad esempio: `entity.id` e `entity.name` non verranno trasmesse su alcuna pagina oltre ai dettagli del prodotto.

### Convalida con il debugger

Ora che le regole vengono aggiornate, puoi verificare se i dati vengono passati correttamente utilizzando il debugger di Adobe.

1. Passa a [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e accedi con l’e-mail `test@adobe.com` e password `test`
1. Passa a una pagina dei dettagli del prodotto
1. Apri l’estensione del browser Adobe Experience Platform Debugger e [cambia la proprietà tag nella proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Ricarica la pagina
1. Seleziona la **Rete** nel debugger e filtra per **Adobe Experience Platform Web SDK**
1. Seleziona il valore nella riga eventi per la prima chiamata
1. Tieni presente che sono presenti le chiavi in `data` > `__adobe` > `target` e vengono compilati con informazioni sul prodotto, la categoria e lo stato di accesso.

   ![__visualizzare__ richiesta decisionScope](assets/target-debugger-data.png)

### Convalida nell’interfaccia di Target

Quindi, consulta l’interfaccia di Target per confermare che i dati sono stati ricevuti e sono disponibili per l’utilizzo in tipi di pubblico e attività. I dati XDM vengono mappati automaticamente su parametri di Target personalizzati. Puoi verificare che i dati XDM siano stati ricevuti da Target ed siano disponibili creando un pubblico.

1. Apri [Adobe Target](https://experience.adobe.com/target)
1. Passa a **[!UICONTROL Tipi di pubblico]** sezione
1. Crea un pubblico e scegli la **[!UICONTROL Personalizzato]** tipo di attributo
1. Cerca nel **[!UICONTROL Parametro]** campo per `web`. Il menu a discesa deve essere compilato con tutti i campi XDM relativi ai dettagli della pagina web.

Successivamente, verifica che l&#39;attributo di profilo dello stato di accesso sia stato passato correttamente.

1. Scegli la **[!UICONTROL Profilo visitatore]** tipo di attributo
1. Cerca `loggedIn`. Se l&#39;attributo è disponibile nel menu a discesa, l&#39;attributo è stato passato correttamente a Target. I nuovi attributi potrebbero richiedere alcuni minuti per diventare disponibili nell’interfaccia utente di Target.

Se disponi di Target Premium, puoi anche verificare che i dati delle entità siano stati passati correttamente e che i dati dei prodotti siano stati scritti nel catalogo dei prodotti Recommendations.

1. Passa a **[!UICONTROL Recommendations]** sezione
1. Seleziona **[!UICONTROL Ricerca nel catalogo]** nella navigazione a sinistra
1. Cerca lo SKU del prodotto o il nome del prodotto visitato in precedenza sul sito Luma. Il prodotto deve essere visualizzato nel catalogo del prodotto. La ricerca di nuovi prodotti potrebbe richiedere alcuni minuti nel catalogo dei prodotti Recommendations.

Dopo aver completato questa lezione, devi disporre di un’implementazione funzionante di Adobe Target tramite l’SDK per web di Platform.

[Avanti: ](setup-consent.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)

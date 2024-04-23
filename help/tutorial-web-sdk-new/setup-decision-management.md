---
title: Configurare la gestione delle decisioni con Platform Web SDK
description: Scopri come implementare la gestione delle decisioni utilizzando Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
exl-id: f7852ef4-44b0-49df-aec8-cb211726247d
source-git-commit: e9e5e1dec8a0595bb789f0324c3263cf914dec31
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 0%

---

# Configurare la gestione delle decisioni con Platform Web SDK

Scopri come implementare la gestione delle decisioni utilizzando Platform Web SDK. Questa guida descrive i prerequisiti fondamentali per la gestione delle decisioni, i passaggi dettagliati per la configurazione e un approfondimento del caso d’uso incentrato sullo stato di fedeltà.

Seguendo questa esercitazione, gli utenti di Journey Optimizer sono in grado di applicare in modo efficace le funzioni offer decisioning, migliorando la personalizzazione e la rilevanza delle interazioni con i clienti.


![SDK per web e diagramma di Adobe Analytics](assets/dc-websdk-ajo.png)

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Acquisisci i concetti fondamentali della gestione delle decisioni in Adobe Journey Optimizer e la sua integrazione con Adobe Experience Platform Web SDK.

* Scopri la procedura dettagliata per configurare l’SDK per web, ad Offer decisioning, garantendo un’integrazione perfetta con Journey Optimizer.

* Esplora un caso d’uso dettagliato incentrato sulle offerte di stato della fedeltà, acquisendo informazioni sulla creazione e la gestione efficaci di offerte, decisioni e posizionamenti.

* Acquisisci i termini essenziali e le loro implicazioni nel framework di gestione delle decisioni.

* Comprendi l’importanza delle regole di decisione, dei qualificatori di raccolta e delle offerte di fallback nella distribuzione dell’offerta giusta all’utente giusto.

* Approfondisci argomenti avanzati come simulazioni e raccolta dati di eventi personalizzati, per testare, convalidare e migliorare i meccanismi di consegna delle offerte.

## Prerequisiti

Per completare le lezioni in questa sezione, devi prima:

* Assicurati che la tua organizzazione abbia accesso a Adobe Journey Optimizer Ultimate (Journey Optimizer e Offer Decisioning) o Adobe Experience Platform e al componente aggiuntivo del servizio applicativo Offer Decisioning.

* Completa tutte le lezioni per la configurazione iniziale di Platform Web SDK.

* Abilita la tua organizzazione per Edge Decisioning.

* Scopri come configurare un posizionamento e creare istanze degli ID posizionamento e attività nel JSON dell’ambito decisionale.

## Limitazioni

Prendi nota della seguente limitazione:

* Le offerte basate su eventi non sono attualmente supportate in Adobe Journey Optimizer. Se crei una regola di decisione basata su un evento, non puoi applicarla a un’offerta.

## Concedere l’accesso alla gestione delle decisioni

Per concedere l’accesso alla funzionalità di gestione delle decisioni, devi creare un’ **Profilo di prodotto** e assegna le autorizzazioni corrispondenti ai tuoi utenti. [Ulteriori informazioni sulla gestione di utenti e autorizzazioni di Journey Optimizer in questa sezione](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

## Configurare lo stream di dati

L’Offer decisioning deve essere abilitato in **flusso di dati** prima che Platform Web SDK possa distribuire qualsiasi attività di Gestione delle decisioni.

Per configurare Offer Decisioning nello stream di dati:

1. Vai a [Raccolta dati](https://experience.adobe.com/#/data-collection) di rete.

1. Nel menu di navigazione a sinistra, seleziona **Flussi di dati**.

1. Seleziona lo stream di dati Luma Web SDK creato in precedenza.

   ![Seleziona flusso di dati](assets/decisioning-datastream-select.png)

1. Seleziona **Modifica** all&#39;interno del **Servizio Adobe Experience Platform**.

   ![Modifica servizio](assets/decisioning-edit-datastream.png)

1. Controlla la **Offer decisioning** casella.

   ![AGGIUNGI SCHERMATA](assets/decisioning-check-offer-box.png)

1. Seleziona **Salva**.

In questo modo gli eventi in entrata per Journey Optimizer vengono gestiti correttamente da **Adobe Experience Platform Edge**.

## Configurare l’SDK per la gestione delle decisioni

La gestione delle decisioni richiede passaggi SDK aggiuntivi, a seconda del tipo di implementazione dell’SDK web. Sono disponibili due opzioni per configurare l’SDK per la gestione delle decisioni.

* Installazione autonoma SDK
   1. Configurare `sendEvent` azione con `decisionScopes`.

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* Installazione dei tag SDK
   1. Passa all’interfaccia di Data Collection.

   1. Nel menu di navigazione a sinistra, seleziona **Tag**.

      ![Seleziona tag](assets/decisioning-data-collection-tags.png)

   1. Seleziona la **Tag, proprietà**.

   1. Crea **Regole**.
      * Aggiungere un Platform Web SDK **Azione Invia evento** e aggiungi le `decisionScopes` alla configurazione di tale azione.

   1. Creare e pubblicare un **Libreria** contenente tutte le **Regole**, **Elementi dati**, e **Estensioni** hai configurato.

## Terminologia

Innanzitutto, devi comprendere la terminologia utilizzata nell’interfaccia di Gestione delle decisioni.

* **Limitazione**: vincolo che determina la frequenza con cui viene visualizzata un’offerta. Due tipi:
   * Limiti totali: il numero massimo di volte in cui un’offerta può essere visualizzata nel pubblico di destinazione.
   * Limite profilo: orari in cui è possibile mostrare un’offerta a un particolare utente.
* **Raccolte**: sottoinsiemi di offerte raggruppati per condizioni specifiche impostate da un addetto marketing, ad esempio categoria di offerta.
* **Decisione**: logica che determina la scelta di un’offerta.
* **Regola di decisione**: vincoli sulle offerte per determinare l’idoneità di un utente.
* **Offerta idonea**: offerta che corrisponde ai vincoli predefiniti e che può essere mostrata a un utente.
* **Gestione delle decisioni**: il sistema di creazione e distribuzione di offerte personalizzate utilizzando la logica di business e le regole decisionali.
* **Offerte di fallback**: l’offerta predefinita visualizzata quando un utente non è idoneo per nessuna offerta in una raccolta.
* **Offerta**: messaggio di marketing con potenziali regole di idoneità che ne determinano i visualizzatori.
* **Libreria di offerte**: archivio centrale che gestisce offerte, decisioni e regole associate.
* **Offerte personalizzate**: messaggi di marketing personalizzati personalizzati in base ai vincoli di idoneità.
* **Posizionamenti**: impostazione o scenario in cui un’offerta viene visualizzata da un utente.
* **Priorità**: metrica di classificazione per le offerte che considera vari vincoli come idoneità e limiti.
* **Rappresentazioni**: informazioni specifiche per il canale, ad esempio posizione o lingua, che guidano la visualizzazione di un’offerta.

## Panoramica del caso d’uso: premi fedeltà

In questa lezione viene implementato un caso di utilizzo di esempio dei premi fedeltà per comprendere la gestione delle decisioni tramite Web SDK.

Questo caso d’uso consente di comprendere meglio in che modo Journey Optimizer può contribuire a fornire la migliore offerta ai clienti, utilizzando la libreria di offerte centralizzata e il motore di decisione delle offerte.

>[!NOTE]
>
> Poiché questo tutorial è destinato agli implementatori, vale la pena notare che questa lezione richiede un notevole lavoro sull’interfaccia in Journey Optimizer. Anche se tali attività di interfaccia sono in genere gestite dagli esperti di marketing, può essere utile che i responsabili dell’implementazione possano acquisire informazioni approfondite sul processo, anche se non sono responsabili della creazione di campagne di gestione delle decisioni nel lungo periodo.

## Componenti

Prima di iniziare a creare le offerte, devi definire diversi componenti prerequisiti.

### Creare un posizionamento per le offerte fedeltà

**Posizionamenti** sono contenitori utilizzati per presentare le offerte. In questo esempio, crei un posizionamento nella parte superiore del sito Luma.

L’elenco dei posizionamenti è accessibile nella sezione **Componenti** menu. I filtri sono disponibili per aiutarti a recuperare i posizionamenti in base a un canale o a un contenuto specifico.

![Visualizzare i posizionamenti](assets/decisioning-placements-list.png)

Per creare il posizionamento, effettuate le seguenti operazioni:

1. Clic **Crea posizionamento**.

   ![Crea posizionamento](assets/decisioning-create-placement.png)

1. Definite le proprietà del posizionamento:
   * **Nome**: nome del posizionamento. Chiamiamo il posizionamento dell’esempio *&#39;Banner homepage&#39;*.
   * **Tipo di canale**: canale per il quale viene utilizzato il posizionamento. Utilizziamo *&#39;Web&#39;* poiché le offerte vengono visualizzate sul sito web Luma.
   * **Tipo di contenuto**: tipo di contenuto che il posizionamento può visualizzare: Testo, HTML, Collegamento immagine o JSON. È possibile utilizzare *&#39;HTML&#39;* per l’offerta.
   * **Descrizione**: descrizione del posizionamento (facoltativo).

   ![Aggiungi dettagli](assets/decisioning-placement-details.png)

1. Fai clic su **Salva**.
1. Una volta creato, il posizionamento viene visualizzato nell’elenco dei posizionamenti.
1. Seleziona la riga contenente il nuovo posizionamento e prendi nota dell’ID posizionamento, in quanto potrebbe essere necessario per la configurazione all’interno dell’ambito decisionale.

   ![Consulta ID posizionamento ](assets/decisioning-placement-id.png)

### Regole di decisione per lo stato di fedeltà

**Regole di decisione** specificare le condizioni di presentazione delle offerte. In questo esempio, puoi creare regole di decisione per distribuire offerte diverse a seconda dello stato di Fedeltà di un utente.

L’elenco delle regole di decisione è accessibile nella sezione **Componenti** menu.

Per creare le regole di decisione, segui questi passaggi:

1. Accedi a **Regole** e fai clic su **Crea regola**.

   ![Creare la regola](assets/decisioning-create-rule.png)

1. Diamo un nome alla prima regola &#39;*Regola stato Gold Loyalty*&quot;. Puoi utilizzare i campi XDM per definire la regola. Adobe Experience Platform **Generatore di segmenti** è un’interfaccia intuitiva che puoi utilizzare per creare le condizioni della regola.

   ![Definire la regola](assets/decisioning-define-rule.png)

1. Clic **Salva** per confermare la condizione della regola.
1. Il nuovo salvato &#39;*Regola stato Gold Loyalty*&#39; verrà visualizzato nel **Elenco delle regole**. Selezionala per visualizzarne le proprietà.

   ![Visualizza regola creata](assets/decisioning-view-rules.png)

1. Ora crea le condizioni della regola di offerta fedeltà rimanenti per il caso d’uso.


### Qualificatori raccolta

**Qualificatori di raccolta** consente di organizzare e cercare facilmente le offerte all’interno della libreria di offerte. In questo esempio, aggiungi i qualificatori di raccolta alle offerte di premi fedeltà per migliorare l’organizzazione dell’offerta.

L’elenco dei qualificatori di raccolta è accessibile nella sezione **Componenti** menu.

Per creare il qualificatore per la raccolta Premi fedeltà, effettua le seguenti operazioni:

1. Accedi a **Qualificatori di raccolta** e fai clic su **Crea qualificatore raccolta**.

   ![Crea qualificatore raccolta](assets/decisioning-create-collection-qualifier.png)

1. Denominiamo il qualificatore della raccolta &#39;*Premi fedeltà*&#39;

   ![Denomina la raccolta](assets/decisioning-name-collection.png)

1. Il nuovo qualificatore di raccolta deve ora essere visualizzato in **Qualificatore raccolta** scheda

## Offerte

Ora è il momento di creare le offerte di Premi fedeltà.

L’elenco delle offerte è accessibile nella sezione **Offerte** menu.

![Visualizza il menu delle offerte](assets/decisioning-offers-menu.png)


### Creazione di offerte per diversi livelli di fedeltà

Inizia creando offerte personalizzate per i diversi livelli di fedeltà Luma.

Per creare il primo **offerta**, effettua le seguenti operazioni:

1. Clic **Crea offerta**, quindi seleziona **Offerta personalizzata**.

1. Diamo un nome alla prima offerta &#39;*Livello fedeltà Luma - Oro*&quot;. È necessario specificare una data e un’ora di inizio/fine per questa offerta. È inoltre necessario associare **qualificatore raccolta** &#39;*Premi fedeltà*&#39; all&#39;offerta, che consente di organizzare meglio all&#39;interno del **Libreria di offerte**. In seguito, fai clic su **Successivo**.

   ![Aggiungi dettagli offerta](assets/decisioning-add-offer-details.png)

1. Ora è necessario aggiungere **rappresentazioni** per definire la posizione di visualizzazione dell’offerta. Scegli il **canale web**. Scegli anche il &#39;*Banner homepage*&#39; **posizionamento** configurato in precedenza. Il valore selezionato **posizionamento** è di tipo HTML, per cui puoi aggiungere contenuti HTML, JSON o TEXT direttamente all&#39;editor per creare l&#39;offerta utilizzando **Personalizzato** pulsante di opzione.

   ![Aggiungi dettagli rappresentazione](assets/decisioning-add-representation-details.png)

1. Modificare il contenuto dell’offerta direttamente con **Editor espressioni**. Ricorda che puoi aggiungere contenuti HTML, JSON o TEXT a questo posizionamento. Accertati di selezionare la **modalità** nella parte inferiore dell’editor, a seconda del tipo di contenuto. Puoi anche premere **convalida** per garantire che non vi siano errori.

   ![Aggiungi HTML offerta](assets/decisioning-add-offer-html.png)

1. Inoltre, puoi utilizzare l’editor espressioni per recuperare gli attributi memorizzati in Adobe Experience Platform. Aggiungiamo il nome di un profilo al contenuto dell’offerta per personalizzarlo meglio per i membri fedeltà su un livello 1:1.

   ![Aggiungere personalizzazione delle offerte](assets/decisioning-add-offer-personalization.png)

1. Aggiungi vincoli per mostrare l’offerta solo ai profili idonei per il &quot;*Regola stato Gold Loyalty*&quot;.

   ![Aggiungi vincolo regola](assets/decisioning-add-rule-constraint.png)

1. Dopo aver esaminato l’offerta, fai clic su **Fine**. Seleziona **Salva e approva**.

Ora crea il resto delle offerte per i vari livelli di fedeltà Luma

### Offerte di fallback

Desideri comunque distribuire un’offerta ai visitatori del sito Luma non fedeltà. A questo scopo, puoi configurare una **offerta di fallback** per la campagna.

Per creare l’offerta di fallback, effettua le seguenti operazioni:

1. Clic **Crea offerta**, quindi seleziona **Offerta di fallback**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Chiamiamo l’offerta di fallback &quot;*Fedeltà non Luma*&quot;. È inoltre possibile associare il **qualificatore raccolta**, &#39;*Premi fedeltà*&#39; all&#39;offerta di fallback per semplificare l&#39;organizzazione delle offerte.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Aggiungi il contenuto dell’offerta di fallback a **Editor espressioni**. Ricorda che puoi aggiungere contenuto HTML, JSON o TEXT a questo posizionamento. Accertati di selezionare la **modalità** nella parte inferiore dell’editor, a seconda del tipo di contenuto. Puoi anche premere **convalida** per garantire che non vi siano errori.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Se tutto è configurato correttamente, premi **Fine** e poi **Salva e approva**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Decisioni

**Decisioni** sono contenitori per le offerte che scelgono la migliore offerta disponibile per un cliente, a seconda della destinazione.

L&#39;elenco delle decisioni è disponibile nella **Decisioni** scheda di **Offerte** menu.
<!--
   ![ADD SCREENSHOT](#)
-->

### Creazione di una decisione per le offerte fedeltà

Creiamo una decisione per il caso d’uso Luma Loyalty Rewards.

Per creare la decisione, segui questi passaggi:

1. Clic **Crea decisione**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Chiamiamo la decisione &quot;.*Offerte fedeltà Luma dicembre*&quot;. Le offerte devono avere una durata di 1 mese, quindi specifichiamole qui.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ora è necessario definire **ambiti decisionali**. Selezionate un posizionamento. È possibile utilizzare la funzione &#39; creata in precedenza *Banner homepage*&quot;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ora devi aggiungere **criteri di valutazione** per l&#39;ambito della decisione. Clic **Aggiungi** e scegli il creato in precedenza &#39;*Premi fedeltà*&#39; **raccolta** che contiene tutte le offerte fedeltà da considerare.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. All’interno di &quot;*Premi fedeltà*&quot;, puoi utilizzare il campo di idoneità per limitare la consegna dell’offerta a un sottoinsieme di visitatori Luma. Tuttavia, per questo caso d’uso desideri che ogni visitatore riceva una delle offerte. Ricorda che hai configurato un **offerta di fallback** per tutti i visitatori non fidelizzati. Imposta l’idoneità su &quot;Nessuno&quot;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Inoltre, è possibile utilizzare **metodo di classificazione** per selezionare l’offerta migliore per ogni visitatore Luma, se più offerte sono idonee per la combinazione utente/posizionamento. Per questo caso d’uso, puoi utilizzare **Priorità offerta** , che utilizza i valori definiti nelle offerte per fornire l’offerta migliore.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ora aggiungi **offerta di fallback** alla decisione. Promemoria del fatto che l’offerta di fallback è l’offerta predefinita visualizzata ai visitatori Luma se non rientrano in nessuno dei tipi di pubblico Fedeltà Luma. Seleziona &#39;*Fedeltà non Luma*&quot; dall’elenco delle offerte di fallback disponibili per &quot;*Banner homepage* posizionamento di &#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Prima di attivare la decisione, esaminiamo l’ambito della decisione, le offerte di fallback, l’anteprima delle offerte disponibili e stimiamo i profili qualificati. Quando tutto si presenta correttamente, puoi fare clic su **Fine** e **Salva e attiva**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Simulazioni

Come best practice, è necessario convalidare la logica decisionale della fidelizzazione Luma per garantire che le offerte corrette vengano consegnate al pubblico fedeltà corretto. Per farlo, utilizza **profili di test**. È inoltre consigliabile testare le modifiche apportate alle offerte tramite i profili di test prima di inviare nuove versioni di offerta alla produzione.

Per iniziare il test, seleziona la **Simulazioni** scheda da **Offerte** menu.

### Verifica delle offerte fedeltà

1. Seleziona un profilo di test da utilizzare per la simulazione. Clic **Gestisci profilo**. [Per creare o designare un nuovo profilo di test per il test dell’offerta, segui questa guida](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html?lang=en#create-test-profiles-csv).
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Aggiungi uno o più profili di test alla simulazione e salva la selezione. Per il test del caso d’uso, assicurati di disporre di profili di test configurati per ogni pubblico di premi fedeltà Luma.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Seleziona l’ambito della decisione da testare. Seleziona **Aggiungi ambito decisione**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Seleziona il creato in precedenza &#39;*Banner homepage* posizionamento di &#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vengono visualizzate le decisioni disponibili, seleziona la creata in precedenza *Offerte fedeltà Luma dicembre*&#39; e fai clic su **Aggiungi**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dopo aver selezionato un profilo di test, fai clic su **Visualizza risultati**. La migliore offerta disponibile viene visualizzata nel profilo di test selezionato per il &quot;*Offerte fedeltà Luma dicembre*&quot;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Seleziona un profilo di test diverso e fai clic su **Visualizza risultati**. Idealmente, dovresti vedere un’offerta simulata diversa, corrispondente al livello di fedeltà del profilo di test.

## Convalida della gestione delle decisioni tramite Adobi Experience Platform Debugger

Il **Adobe Experience Platform Debugger** L’estensione, disponibile sia per Chrome che per Firefox, analizza le pagine web per identificare i problemi nell’implementazione delle soluzioni Adobe Experience Cloud.

Puoi utilizzare il debugger sul sito Luma per convalidare la logica decisionale in produzione. Questa è una buona pratica una volta che il caso di utilizzo dei premi fedeltà è attivo e in esecuzione, per garantire che tutto sia configurato correttamente.

[Scopri come configurare il debugger nel browser utilizzando la guida qui](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html?lang=en).

Per iniziare la convalida tramite il debugger:

1. Passa alla pagina web Luma con il posizionamento dell’offerta.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Nella pagina web, apri **Adobe Experience Platform Debugger**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Accedi a **Riepilogo**. Verificare che **ID flusso di dati** corrisponde al **flusso di dati** in **Raccolta dati di Adobe** per il quale hai attivato Offer Decisioning.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sotto **Soluzioni** passa a **Experienci Platform Web SDK**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. All&#39;interno del **Configurazione** , Attiva **Abilita debug**. Questo abilita la registrazione per la sessione all’interno di un **Adobe Experience Platform Assurance** sessione.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Puoi quindi accedere al sito con vari account fedeltà Luma e utilizzare il debugger per convalidare le richieste inviate al **Adobe Experience Platform Edge Network**. Tutte queste richieste devono essere acquisite in **Assurance** per il tracciamento dei registri.
<!--
   ![ADD SCREENSHOT](#)
-->

[Successivo: ](setup-consent.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)

---
title: Configurare il canale web Journey Optimizer con Platform Web SDK
description: Scopri come implementare il canale web Journey Optimizer utilizzando Platform Web SDK. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
jira: KT-15411
exl-id: ab83ce56-7f54-4341-8750-b458d0db0239
source-git-commit: 1feddab414a8a7e49f04b8886c275d06516d0114
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 1%

---


# Configurare il canale web Journey Optimizer con Web SDK

Scopri come implementare il [canale web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/get-started-web) di Adobe Journey Optimizer utilizzando Adobe Experience Platform Web SDK. Questa lezione descrive i prerequisiti fondamentali per il canale web, i passaggi dettagliati per la configurazione e un approfondimento su un caso d’uso incentrato sullo stato di fedeltà.

Seguendo questa lezione, gli utenti di Journey Optimizer possono utilizzare il canale web per la personalizzazione online avanzata utilizzando il web designer di Journey Optimizer.



![Diagramma Web SDK e Adobe Analytics](assets/dc-websdk-ajo.png)

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendi la funzione e il significato di Web SDK nella distribuzione dell’esperienza del canale web.
* Comprendi il processo di creazione di una campagna per canale web dall’inizio alla fine utilizzando il caso d’uso dei premi fedeltà Luma di esempio.
* Configura le proprietà, le azioni e le pianificazioni della campagna all’interno dell’interfaccia.
* Scopri le funzionalità e i vantaggi dell’estensione Adobe Experience Cloud Visual Editing Helper.
* Scopri come modificare il contenuto delle pagine web, incluse immagini, intestazioni e altri elementi, utilizzando la finestra di progettazione web.
* Scopri come inserire le offerte in una pagina web utilizzando il componente Decisione offerta.
* Acquisisci familiarità con le best practice per garantire la qualità e il successo di una campagna canale web.

## Prerequisiti

Per completare le lezioni in questa sezione, devi prima:

* Completa tutte le lezioni per la configurazione iniziale di Platform Web SDK, inclusa la configurazione di elementi dati e regole.
* Assicurati che la versione dell’estensione tag Adobe Experience Platform Web SDK sia 2.16 o successiva.
* Completare la lezione Configurazione di Experience Platform, incluso l&#39;esercizio per la creazione del pubblico `Luma Loyalty Rewards – Gold Status`.
* Scaricata e abilitata l&#39;estensione del browser [Adobe Experience Cloud Visual Editing Helper](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
* Se utilizzi il web designer Journey Optimizer per creare l’esperienza del canale web, accertati di utilizzare i browser Google Chrome o Microsoft® Edge.
* Assicurati che i cookie di terze parti siano consentiti nel browser. Potrebbe essere necessario disattivare anche i blocchi degli annunci nel browser.

  >[!CAUTION]
  >
  > In Journey Optimizer Web Designer, alcuni siti Web potrebbero non essere aperti in modo affidabile per uno dei motivi seguenti:
  > 
  > 1. Il sito web dispone di criteri di sicurezza rigorosi.
  > 1. Il sito web è incorporato in un iframe.
  > 1. Il sito per il controllo qualità o il sito di staging del cliente non è accessibile esternamente (è un sito interno).

* Durante la creazione di esperienze web e l&#39;inclusione di contenuto dalla libreria Adobe Experience Manager Assets Essentials, è necessario [configurare il sottodominio per la pubblicazione di questo contenuto](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/configure-web-channel/web-delegated-subdomains).
* Se utilizzi la funzione di sperimentazione dei contenuti, assicurati che il set di dati web sia incluso anche nella configurazione di reporting.
* Attualmente, sono supportati due tipi di implementazioni per abilitare l’authoring e la distribuzione di campagne canale web sulle proprietà web:
   * Solo lato client: per modificare il sito Web, è necessario implementare Adobe Experience Platform Web SDK.
   * Modalità ibrida: puoi utilizzare l’API server di Platform Edge Network per richiedere la personalizzazione lato server. La risposta dall’API viene quindi fornita a Adobe Experience Platform Web SDK per il rendering delle modifiche sul lato client. Per ulteriori informazioni, consulta la documentazione sulle API del server Adobe Experience Platform Edge Network. Ulteriori dettagli ed esempi di implementazione per la modalità ibrida sono disponibili in questo post di blog.

  >[!NOTE]
  >
  >L’implementazione solo lato server non è attualmente supportata.




## Terminologia

Innanzitutto, devi comprendere la terminologia utilizzata nelle campagne del canale web.

* **Canale Web**: mezzo di comunicazione o per la distribuzione di contenuti tramite il Web. Nel contesto di questa guida, si riferisce al meccanismo attraverso il quale i contenuti personalizzati vengono consegnati ai visitatori del sito web utilizzando Platform Web SDK, all’interno di Adobe Journey Optimizer.
* **Superficie Web**: fa riferimento a una proprietà Web identificata da un URL in cui viene distribuito il contenuto. Può includere una o più pagine web.
* **Web Designer di Journey Optimizer**: strumento o interfaccia specifica all&#39;interno di Journey Optimizer in cui gli utenti possono progettare le esperienze del canale Web.
* **Helper per editing video Adobe Experience Cloud**: estensione del browser per la modifica e la progettazione visiva delle esperienze dei canali Web.
* **Datastream**: una configurazione all&#39;interno del servizio Adobe Experience Platform che garantisce la consegna delle esperienze del canale web.
* **Criterio di unione**: configurazione che garantisce l&#39;attivazione e la pubblicazione accurate delle campagne in entrata.
* **Pubblico**: un segmento specifico di utenti o visitatori del sito che soddisfano determinati criteri.
* **Web designer**: interfaccia o strumento che consente di modificare e progettare le esperienze Web in modo visivo senza immergersi nel codice.
* **Editor espressioni**: strumento all&#39;interno della finestra di progettazione Web che consente agli utenti di aggiungere personalizzazioni al contenuto Web, potenzialmente basate su attributi di dati o altri criteri.
* **Componente decisione offerta**: componente nella finestra di progettazione Web che consente di decidere quale offerta è più adatta per essere visualizzata a un visitatore specifico in base alla gestione delle decisioni.
* **Esperimento sui contenuti**: un metodo per testare diverse varianti di contenuto per individuare quella che offre le migliori prestazioni in termini di metrica desiderata, ad esempio i clic in entrata.
* **Trattamento**: nel contesto di esperimenti di contenuto, un trattamento si riferisce a una specifica variante di contenuto in fase di test rispetto a un altro.
* **Simulazione**: meccanismo di anteprima per visualizzare l&#39;esperienza del canale web prima di attivarla per i tipi di pubblico live.

## Configurare lo stream di dati

Il servizio Adobe Experience Platform è già stato aggiunto allo stream di dati. Ora devi abilitare l’opzione Adobe Journey Optimizer per poter fornire esperienze di canale web.

Per configurare Adobe Journey Optimizer nello stream di dati:

1. Passare all&#39;interfaccia [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"}.
1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Flussi di dati]**.
1. Seleziona lo stream di dati di Luma Web SDK creato in precedenza.

   ![Seleziona flusso di dati](assets/web-channel-select-datastream.png)

1. Seleziona **[!UICONTROL Modifica]** nel servizio Adobe Experience Platform.

   ![Modifica flusso di dati](assets/web-channel-edit-datastream.png)

1. Selezionare la casella **[!UICONTROL Adobe Journey Optimizer]**.

1. **[!UICONTROL Salva]** la configurazione aggiornata.

   ![Casella AJO](assets/web-channel-check-ajo-box.png)


In questo modo gli eventi in entrata per Journey Optimizer vengono gestiti correttamente da Adobe Experience Platform Edge Network.

## Configurare il criterio di unione

Verificare che sia definito un criterio di unione con l&#39;opzione **[!UICONTROL Criterio di unione attivo su Edge]** abilitata. Questa opzione dei criteri di unione viene utilizzata dai canali in entrata di Journey Optimizer per garantire l’attivazione e la pubblicazione accurate delle campagne in entrata sul server Edge di.

Per configurare l’opzione nel criterio di unione:

1. Vai alla pagina **[!UICONTROL Cliente]** > **[!UICONTROL Profili]** nell&#39;interfaccia di Experience Platform o Journey Optimizer.
1. Assicurati di trovarti nella sandbox utilizzata per l’esercitazione
1. Seleziona la scheda **[!UICONTROL Criteri di unione]**.
1. Seleziona il criterio (in genere è meglio utilizzare il criterio [!UICONTROL Basato su tempo predefinito]) e attiva/disattiva l&#39;opzione **[!UICONTROL Criterio di unione attivo su Edge]** nel passaggio **[!UICONTROL Configura]**.

   ![Attiva/Disattiva criterio di unione](assets/web-channel-active-on-edge-merge-policy.png)

## Configurare il set di dati web per la sperimentazione dei contenuti

Per utilizzare esperimenti sui contenuti nelle campagne per canali web, devi assicurarti che il set di dati web utilizzato sia incluso anche nella configurazione di reporting. Il sistema di reporting di Journey Optimizer utilizza il set di dati in modalità di sola lettura per popolare i rapporti di sperimentazione dei contenuti preconfigurati.

[L&#39;aggiunta di set di dati per il reporting dell&#39;esperimento sui contenuti è descritta in questa sezione](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting-configuration#add-datasets).

## Panoramica del caso d’uso: premi fedeltà

In questa lezione, un esempio di caso di utilizzo dei premi fedeltà viene utilizzato per descrivere nel dettaglio l’implementazione di un’esperienza di canale web utilizzando Web SDK.

Questo caso d’uso consente di comprendere meglio in che modo Journey Optimizer può contribuire a fornire ai clienti le migliori esperienze in entrata, utilizzando le campagne Journey Optimizer e il web designer.

Poiché questo tutorial è destinato agli implementatori, vale la pena notare che questa lezione richiede un notevole lavoro sull’interfaccia in Journey Optimizer. Anche se tali attività di interfaccia sono tipicamente gestite dagli esperti di marketing, può essere utile per gli implementatori acquisire insight nel processo, anche se in genere non sono responsabili della creazione delle campagne per i canali web.

### Crea campagna di premi fedeltà

Dopo aver acquisito i dati di esempio sulla fedeltà e creato il segmento, crea la campagna per il canale web Loyalty Rewards in Adobe Journey Optimizer.

Per creare la campagna di esempio:

1. Apri l&#39;interfaccia [Journey Optimizer](https://experience.adobe.com/journey-optimizer/home){target="_blank"}

   >[!NOTE]
   >
   > Schema, set di dati e tipi di pubblico possono essere generati anche nell’interfaccia di Journey Optimizer in quanto sono tutti costrutti comuni di Experience Platform.

1. Passa a **[!UICONTROL Gestione Percorsi]** > **[!UICONTROL Campagne]** nel menu di navigazione a sinistra
1. Fai clic su **[!UICONTROL Crea campagna]** in alto a destra.
1. Scegli il tipo di campagna. Per il caso d&#39;uso Premi fedeltà, scegli **Pianificato - Marketing**.

   ![Campagna pianificata](assets/web-channel-campaign-properties-scheduled.png)

1. Aggiungi alcuni dettagli aggiuntivi alla nuova campagna per canale web. Innanzitutto, assegna un nome alla campagna. Chiamalo `Luma Loyalty Rewards – Gold Status`. Facoltativamente, puoi aggiungere una descrizione alla campagna. Aggiungi anche **[!UICONTROL Tag]** per migliorare la tassonomia complessiva della campagna.

   ![Denomina la campagna](assets/web-channel-campaign-name.png)

1. Passa alla scheda **[!UICONTROL Azioni]**
1. Scegli **[!UICONTROL Web]** come **[!UICONTROL Nome azione]**.
1. Selezionare **[!UICONTROL Crea nuova configurazione]** come **[!UICONTROL Configurazione Web]**.
1. Come dettagli della configurazione del canale, immetti quanto segue:
   1. `LumaHomepage` come **[!UICONTROL Nome]**.
   1. **[!UICONTROL Web]** come **[!UICONTROL Canale]**.
   1. **[!UICONTROL Personalization in loco]** come **[!UICONTROL azione di marketing]**.
   1. **[!UICONTROL Pagina singola]** come **[!UICONTROL Impostazioni Web]**.
   1. `https://newluma.enablementadobe.com/index.html` come **[!UICONTROL URL pagina]**.
1. **[!UICONTROL Invia]** la nuova configurazione del canale

   ![Configurare il canale Web](assets/web-channel-configuration.png)
1. Nella scheda del browser con la tua Campagna, seleziona la nuova configurazione `LumaHomepage`

   >[!TIP]
   >
   > Se la nuova configurazione non viene visualizzata nel menu a discesa, vai alla scheda [!UICONTROL Proprietà], quindi torna alla scheda [!UICONTROL Azioni] e controlla nuovamente il menu a discesa.


## Sperimentazione con contenuti di premi fedeltà

Dopo aver selezionato la [!UICONTROL configurazione Web], nella sezione **[!UICONTROL Azione]** puoi facoltativamente creare un esperimento per verificare quale contenuto funziona meglio per il pubblico `Luma Loyalty Rewards – Gold Status`. Creiamo e testiamo due trattamenti come componente della configurazione della campagna.

Per creare l’esperimento sui contenuti:

1. Fai clic su **[!UICONTROL Crea esperimento]**.

   ![Crea esperimento](assets/web-channel-create-content-experiment.png)

1. Scegli una **[!UICONTROL metrica di successo]**. Questa è la metrica per determinare l’efficacia dei contenuti. Scegli **[!UICONTROL Clic univoci]** per vedere quale trattamento del contenuto genera più clic sul CTA dell&#39;esperienza Web.

1. Facoltativamente, puoi designare un **[!UICONTROL Holdout]** che non riceve nessuno dei due trattamenti. Lascia questa opzione deselezionata per il momento.

1. Se necessario, scegliere anche di **[!UICONTROL distribuire uniformemente]**. Selezionare questa opzione per assicurarsi che le divisioni del trattamento siano sempre divise in modo uniforme.

1. Seleziona **[!UICONTROL Aggiungi trattamento]** per avere due trattamenti nell&#39;esperimento.

1. Seleziona **[!UICONTROL Crea]**.

   ![Scegli la metrica di successo](assets/web-channel-content-experiment-metric.png)


[Ulteriori informazioni sugli esperimenti di contenuto nel canale web Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/content-management/content-experiment/get-started-experiment).



### Modificare il contenuto con Visual Helper

Ora creiamo l’esperienza del canale web. Installa innanzitutto l&#39;estensione del browser [Adobe Experience Cloud Visual Editing Helper](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) per Google Chrome e Microsoft® Edge, se non lo hai già fatto. Una volta installata, procedere con i passaggi descritti nell’interfaccia di Journey Optimizer:

1. Seleziona **[!UICONTROL Modifica contenuto]** (oppure passa alla scheda Contenuto della campagna). Poiché hai inserito come superficie un URL a pagina singola, dovresti essere pronto per iniziare a lavorare nel compositore.

   ![Modificare i contenuti](assets/web-channel-edit-content.png)

1. Ora fai clic su **[!UICONTROL Modifica pagina Web]** per iniziare a creare il Trattamento A dell&#39;esperienza.

   ![Modifica pagina Web](assets/web-channel-edit-web-page.png)

1. Inizia modificando alcuni elementi utilizzando il compositore web. Utilizza il menu contestuale per modificare l’intestazione dell’immagine protagonista Luma. Regola lo stile del riquadro contestuale a destra.

   ![Aggiungi modifiche contestuali](assets/web-channel-some-contextual-edit.png)



1. Aggiungi anche la personalizzazione al contenitore utilizzando **[!UICONTROL Editor espressioni]**.

   ![Apri editor espressioni](assets/web-channel-open-expression-editor.png)
   ![Aggiungere la personalizzazione](assets/web-channel-add-basic-personalization.png)

1. Assicurati che l’esperienza sia correttamente tracciata per i clic. Scegliere **[!UICONTROL Selezionare l&#39;elemento di traccia]** dal menu contestuale.

   ![Traccia dei clic](assets/web-channel-click-tracking.png)

Sono disponibili molte opzioni per personalizzare i messaggi.

### Modifiche alla progettazione di HTML

Sono disponibili alcuni metodi per apportare modifiche più avanzate o personalizzate al sito come componente della campagna Premi fedeltà. Esplora alcuni di questi nel Trattamento B.

Utilizza il riquadro **[!UICONTROL Componenti]** per aggiungere HTML o altri contenuti direttamente al sito Luma.

![Esplora il riquadro dei componenti](assets/web-channel-components-pane.png)

Aggiungi un nuovo componente HTML nella parte superiore della pagina. Apri di nuovo l&#39;**[!UICONTROL editor espressioni]** per modificare HTML.

![Apri editor espressioni](assets/web-channel-open-expression-editor-html.png)


In alternativa, aggiungi le modifiche di HTML dal riquadro **[!UICONTROL Modifiche]**. Questo riquadro consente di selezionare un componente nella pagina e modificarlo dall’interfaccia di progettazione.

Nell&#39;editor, aggiungi il HTML per il pubblico `Luma Loyalty Rewards – Gold Status`. Seleziona **[!UICONTROL Convalida]**.

![Convalida HTML](assets/web-channel-add-custom-html-validate.png)

Ora, controlla il nuovo componente HTML personalizzato per adattarlo alle tue esigenze.

### Eseguire il targeting della campagna per un pubblico

Per impostazione predefinita, la campagna è attiva per tutti i visitatori del sito. Ai fini di questo caso d’uso, solo i membri che ricevono un premio in oro devono visualizzare l’esperienza. Per indirizzare il contenuto a questo pubblico:

1. Passa alla scheda **[!UICONTROL Pubblico]**

1. Nel campo **[!UICONTROL Spazio dei nomi identità]**, seleziona lo spazio dei nomi per identificare i singoli utenti all&#39;interno del segmento scelto. Poiché stai distribuendo la campagna sul sito Luma, puoi scegliere lo spazio dei nomi ECID. I profili all&#39;interno del pubblico `Luma Loyalty Rewards – Gold Status` privi dello spazio dei nomi ECID tra le loro varie identità non sono presi in considerazione dalla campagna del canale web.

1. **[!UICONTROL Selezionare il pubblico]**

   ![Selezionare il pubblico](assets/web-channel-select-audience.png)

1. Scegli il pubblico `Luma Loyalty Rewards - Gold Status` creato nella lezione [Configurare Experience Platform](setup-experience-platform.md).
1. **[!UICONTROL Salva]** il pubblico nella campagna

   ![Salva pubblico](assets/web-channel-save-audience.png)


<!--
### Simulate Loyalty Rewards Content

Look at a preview of the modified web page before activating the campaign. Keep in mind that you must have test profiles configured to simulate web channel experiences.

To simulate the experience:

1. Select **[!UICONTROL Simulate content]** within the campaign.

    ![Simulate content](assets/web-channel-simulate-content.png)

1. Choose a test profile to receive the simulation. Keep in mind that the test profile should be in the `Luma Loyalty Rewards – Gold Status` audience to receive the proper treatment.

1. The preview is displayed for the test profile.

1. Select the [!UICONTROL Content] tab

1. Choose the **[!UICONTROL Page URL]** web surface option to deploy the experience on one page for this campaign. Enter the URL for the Luma page, `https://newluma.enablementadobe.com`

1. Once the web surface is defined, select **[!UICONTROL Create]**.

    ![Select web surface](assets/web-channel-web-surface.png)
-->

### Pianificare la campagna

Per impostazione predefinita, le campagne vengono avviate e interrotte quando vengono attivate e disattivate manualmente. Tuttavia, puoi pianificarli in modo che inizino e si fermino in date e ore specifiche. Lascia le impostazioni predefinite e seleziona **Verifica per attivare**:

![Pianificazione campagna](assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>Tieni presente che, per le campagne per canali web, l’esperienza web viene visualizzata quando il visitatore apre la pagina. Pertanto, a differenza di altri tipi di campagne in Adobe Journey Optimizer, la sezione **[!UICONTROL Action triggers]** non è configurabile.



### Attivazione della campagna Premi fedeltà

Ti viene chiesto di confermare un’ultima volta i dettagli della campagna. Seleziona **[!UICONTROL Attiva]**. Potrebbero essere necessari fino a 15 minuti perché la campagna diventi live sul sito.

![Attiva la campagna](assets/web-channel-campaign-activate.png)

### Premi fedeltà QA

Sono disponibili alcuni accessi che puoi utilizzare per simulare gli utenti con stato &quot;gold&quot; e che si qualificano per la tua campagna. È necessario aver caricato i dati di esempio in [Configura Experience Platform](setup-experience-platform.md) e creare account utilizzando queste credenziali sul sito Web affinché funzionino.

1. `cleavlandeuler@emailsim.io`/`test`
1. `leftybeagen@emailsim.io`/`test`
1. `jenimartinho@emailsim.io`/`test`

Come best practice, monitora le statistiche della campagna **[!UICONTROL Web]** nella schermata di panoramica della campagna dopo l&#39;avvio oppure fai clic su **[!UICONTROL Rapporti]** per ottenere rapporti più approfonditi:

![Visualizza report Web](assets/web-channel-web-report.png)

### Convalida del canale web tramite Adobe Experience Platform Debugger

L’estensione Adobe Experience Platform Debugger, disponibile sia per Chrome che per Firefox, analizza le pagine web per identificare i problemi nell’implementazione delle soluzioni Adobe Experience Cloud.

Puoi utilizzare il debugger sul sito Luma per convalidare l’esperienza del canale web in produzione. Si tratta di una best practice una volta che il caso di utilizzo Fedeltà e premi è attivo e in esecuzione, per garantire che tutto sia configurato correttamente.

[Scopri come configurare il debugger nel browser utilizzando la guida qui](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Per iniziare la convalida tramite il debugger:

1. Passa alla pagina web Luma con l’esperienza del canale web.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Nella pagina Web, apri **[!UICONTROL Adobe Experience Platform Debugger]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Passa a **Riepilogo**. Verificare che l&#39;**[!UICONTROL ID Datastream]** corrisponda allo **[!UICONTROL stream di dati]** nella **[!UICONTROL Raccolta dati di Adobe]** per cui è stato abilitato Adobe Journey Optimizer.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Puoi quindi accedere al sito con vari account fedeltà Luma e utilizzare il debugger per convalidare le richieste inviate all’Edge Network di Adobe Experience Platform.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. In **[!UICONTROL Soluzioni]** passa a **[!UICONTROL Experience Platform Web SDK]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Nella scheda **Configurazione**, attiva **[!UICONTROL Abilita debug]**. In questo modo viene abilitata la registrazione per la sessione in una sessione **[!UICONTROL Adobe Experience Platform Assurance]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Accedi al sito con vari account fedeltà Luma e utilizza il debugger per convalidare le richieste inviate alla **[!UICONTROL rete Adobe Experience Platform Edge]**. Tutte queste richieste devono essere acquisite in **[!UICONTROL Assurance]** per il tracciamento del registro.
<!--
   ![ADD SCREENSHOT](#)
-->

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)

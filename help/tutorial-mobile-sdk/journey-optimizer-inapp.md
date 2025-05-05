---
title: Creare e inviare messaggi in-app con Platform Mobile SDK
description: Scopri come creare e inviare messaggi in-app a un’app mobile con Platform Mobile SDK e Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
jira: KT-14639
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: f73f0fc345fc605e60b19be1abe2e328795898aa
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# Creare e inviare messaggi in-app

Scopri come creare messaggi in-app per le app mobili con Experience Platform Mobile SDK e Journey Optimizer.

Journey Optimizer consente di creare campagne per inviare messaggi in-app a tipi di pubblico mirati. Le campagne in Journey Optimizer vengono utilizzate per fornire contenuti una tantum a un pubblico specifico utilizzando vari canali. Con le campagne, le azioni vengono eseguite simultaneamente, immediatamente o in base a una pianificazione specifica. Quando si utilizzano i percorsi (consulta la lezione [Notifiche push di Journey Optimizer](journey-optimizer-push.md)), le azioni vengono eseguite in sequenza.

![Architettura](assets/architecture-ajo.png)

Prima di inviare messaggi in-app con Journey Optimizer, è necessario assicurarsi che siano presenti le configurazioni e le integrazioni corrette. Per informazioni sul flusso di dati dei messaggi in-app in Journey Optimizer, consulta [la documentazione](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=it).

>[!NOTE]
>
>Questa lezione è facoltativa e si applica solo agli utenti di Journey Optimizer che desiderano inviare messaggi in-app.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Configura l’app per Adobe Experience Platform.
* Accedi a Journey Optimizer e alle autorizzazioni sufficienti come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=it). È inoltre necessaria un&#39;autorizzazione sufficiente per le seguenti funzioni di Journey Optimizer.
   * Gestire le campagne.
* Dispositivo fisico iOS o simulatore per test.


## Obiettivi di apprendimento

In questa lezione, potrai

* Crea una superficie app in AJO.
* Installa e configura l’estensione tag Journey Optimizer.
* Aggiorna l’app per registrare l’estensione tag Journey Optimizer.
* Convalida la configurazione in Assurance.
* Definisci la tua esperienza di campagna e messaggio in-app in Journey Optimizer.
* Invia il tuo messaggio in-app dall’app.

## Configurazione

>[!TIP]
>
>Se l&#39;ambiente è già stato configurato nell&#39;ambito della lezione [Messaggi push di Journey Optimizer](journey-optimizer-push.md), è possibile che siano già stati eseguiti alcuni dei passaggi descritti in questa sezione di installazione.


### Creare una configurazione di canale in Journey Optimizer

Per iniziare, devi creare una configurazione di canale per poter inviare notifiche di messaggi app da Journey Optimizer.

1. Nell&#39;interfaccia di Journey Optimizer aprire il menu **[!UICONTROL Canali]** > **[!UICONTROL Impostazioni generali]** > **[!UICONTROL Configurazioni canale]**, quindi selezionare **[!UICONTROL Crea configurazione canale]**.

   ![Creare una configurazione di canale](assets/push-config-9.png)

1. Immetti un nome e una descrizione (facoltativa) per la configurazione.

   >[!NOTE]
   >
   > I nomi devono iniziare con una lettera (A-Z). Può contenere solo caratteri alfanumerici. È inoltre possibile utilizzare i caratteri trattino basso `_`, punto `.` e trattino `-`.


1. Per assegnare etichette di utilizzo dei dati personalizzate o di base alla configurazione, è possibile selezionare **[!UICONTROL Gestisci accesso]**. [Ulteriori informazioni sul controllo degli accessi a livello di oggetto](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/access-control/object-based-access).

1. Seleziona il canale **Messaggistica in-app**.

1. Seleziona **[!UICONTROL Azione di marketing]** per associare i criteri di consenso ai messaggi utilizzando questa configurazione. Tutti i criteri di consenso associati all’azione di marketing vengono utilizzati per rispettare le preferenze dei clienti. [Ulteriori informazioni sulle azioni di marketing](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions).

1. Seleziona la Piattaforma per la quale vuoi definire le impostazioni. Questo consente di specificare l’app di destinazione per ogni piattaforma e garantisce la distribuzione coerente dei contenuti su più piattaforme.

   >[!NOTE]
   >
   >Per le piattaforme iOS e Android, la consegna si basa esclusivamente sull’ID app. Se entrambe le app condividono lo stesso ID app, il contenuto verrà distribuito a entrambi, indipendentemente dalla piattaforma selezionata nella **[!UICONTROL configurazione canale]**.

1. Seleziona **[!UICONTROL Invia]** per salvare le modifiche.

   ![Configurare il canale in-app](assets/inapp_config_10.png)

### Aggiorna configurazione dello stream di dati

Per fare in modo che i dati inviati dalla tua app mobile ad Edge Network vengano inoltrati a Journey Optimizer, aggiorna la configurazione di Experience Edge.



1. Nell&#39;interfaccia utente di Data Collection, seleziona **[!UICONTROL Datastreams]** e quindi il tuo datastream, ad esempio **[!DNL Luma Mobile App]**.
1. Seleziona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) per **[!UICONTROL Experience Platform]** e seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifica]** dal menu di scelta rapida.
1. Nella schermata **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**, assicurati che sia selezionato **[!UICONTROL Adobe Journey Optimizer]**. Per ulteriori informazioni, vedere [Impostazioni di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=it#aep).
1. Per salvare la configurazione dello stream di dati, seleziona **[!UICONTROL Salva]**.


   ![Configurazione dello stream di dati di AEP](assets/datastream-ajo-inapp-configuration.png)


### Installare l’estensione dei tag di Journey Optimizer

Affinché l&#39;app funzioni con Journey Optimizer, devi aggiornare la proprietà del tag.

1. Passa a **[!UICONTROL Tag]** > **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**.
1. Apri la proprietà, ad esempio **[!DNL Luma Mobile App Tutorial]**.
1. Seleziona **[!UICONTROL Catalogo]**.
1. Cerca l&#39;estensione **[!UICONTROL Adobe Journey Optimizer]**.
1. Installa l’estensione.

Quando *solo* utilizza i messaggi in-app nell&#39;app, in **[!UICONTROL Installa estensione]** o **[!UICONTROL Configura estensione]**, non è necessario configurare nulla. Tuttavia, se hai già seguito la lezione [Notifiche push](journey-optimizer-push.md) nell&#39;esercitazione, vedrai che per l&#39;ambiente **[!UICONTROL Sviluppo]**, il set di dati **[!UICONTROL AJO Push Tracking Experience Event]** è selezionato dall&#39;elenco **[!UICONTROL Set di dati evento]**.


### Implementare Journey Optimizer nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. A questo punto è necessario installare e registrare il SDK di messaggistica. Se questi passaggi non sono chiari, controlla la sezione [Installare gli SDK](install-sdks.md).

>[!NOTE]
>
>Se hai completato la sezione [Installare gli SDK](install-sdks.md), SDK è già installato e puoi saltare questo passaggio.
>

1. In Xcode, accertati che [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios) sia aggiunto all&#39;elenco dei pacchetti nelle dipendenze dei pacchetti. Consulta [Gestione pacchetti Swift](install-sdks.md#swift-package-manager).
1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** nel Navigatore progetti Xcode.
1. Assicurarsi che `AEPMessaging` faccia parte dell&#39;elenco delle importazioni.

   `import AEPMessaging`

1. Assicurarsi che `Messaging.self` faccia parte dell&#39;array di estensioni che si sta registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```


## Convalidare la configurazione con Assurance

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Nell&#39;interfaccia utente di Assurance, seleziona **[!UICONTROL Configura]**.
   ![configura clic](assets/push-validate-config.png)
1. Seleziona il pulsante ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto a **[!UICONTROL Messaggistica in-app]**.
1. Seleziona **[!UICONTROL Salva]**.
   ![salva](assets/assurance-in-app-config.png)
1. Seleziona **[!UICONTROL Messaggistica in-app]** dal menu di navigazione a sinistra.
1. Selezionare la scheda **[!UICONTROL Convalida]**. Verifica che non siano presenti errori.

   ![Convalida in-app](assets/assurance-in-app-validate.png)


## Creare un messaggio in-app personalizzato

Per creare un messaggio in-app personalizzato, devi definire una campagna in Journey Optimizer che attivi un messaggio in-app in base agli eventi che si verificano. Questi eventi possono essere:

* dati inviati a Adobe Experience Platform,
* eventi di tracciamento di base, come azioni, oppure stato o raccolta di dati PII, tramite le API generiche core mobile,
* eventi del ciclo di vita dell&#39;applicazione, ad esempio avvio, installazione, aggiornamento, chiusura o arresto anomalo,
* eventi di geolocalizzazione, come l’ingresso o l’uscita da un punto di interesse.

In questo tutorial, utilizzerai le API generiche core per dispositivi mobili e indipendenti dalle estensioni (consulta [API generiche core per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) per facilitare il tracciamento degli eventi di schermate utente, azioni e dati PII. Gli eventi generati da queste API vengono pubblicati nell’hub eventi di SDK e sono disponibili per l’utilizzo da parte delle estensioni. L’hub eventi SDK fornisce la struttura dati di base associata a tutte le estensioni SDK di Mobile Platform, mantenendo un elenco di estensioni registrate e moduli interni, un elenco di listener di eventi registrati e un database a stato condiviso.

L’hub eventi di SDK pubblica e riceve i dati dell’evento da estensioni registrate per semplificare le integrazioni con Adobe e soluzioni di terze parti. Ad esempio, quando è installata l’estensione Optimize, tutte le richieste e le interazioni con il motore di offerta Journey Optimizer - Decision Management vengono gestite dall’hub eventi.

1. Nell&#39;interfaccia utente di Journey Optimizer, seleziona **[!UICONTROL Campagne]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Crea campagna]**.
1. Nella schermata **[!UICONTROL Crea campagna]**:
   1. Seleziona **[!UICONTROL Messaggio in-app]** e seleziona una superficie app dall&#39;elenco **[!UICONTROL Superficie app]**, ad esempio **[!DNL Luma Mobile App]**.
   1. Seleziona **[!UICONTROL Crea]**

      ![Proprietà campagna](assets/ajo-campaign-properties.png)
1. Nella schermata Definizione campagna, in **[!UICONTROL Proprietà]**, immetti un **[!UICONTROL Nome]** per la campagna, ad esempio `Luma - In-App Messaging Campaign`, e una **[!UICONTROL Descrizione]**, ad esempio `In-app messaging campaign for Luma app`.
   ![Nome campagna](assets/ajo-campaign-properties-name.png)
1. Scorri verso il basso fino a **[!UICONTROL Azione]** e seleziona **[!UICONTROL Modifica contenuto]**.
1. Nella schermata **[!UICONTROL Messaggio in-app]**:
   1. Seleziona **[!UICONTROL Modale]** come **[!UICONTROL Layout messaggio]**.
   2. Immetti `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` per **[!UICONTROL URL file multimediale]**.
   3. Immetti un **[!UICONTROL Intestazione]**, ad esempio `Welcome to this Luma In-App Message`, e un **[!UICONTROL Corpo]**, ad esempio `Triggered by pushing that button in the app...`.
   4. Immetti **[!UICONTROL Ignora]** come **[!UICONTROL pulsante #1 testo (primario)]**.
   5. Nota come viene aggiornata l’anteprima.
   6. Seleziona **[!UICONTROL Rivedi per attivare]**.

      ![Editor in-app](assets/ajo-in-app-editor.png)
1. Nella schermata **[!UICONTROL Rivedi per attivare (Luma - Campagna di messaggistica in-app)]**, seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) nella sezione **[!UICONTROL Pianifica]**.
   ![Rivedi pianificazione seleziona pianificazione](assets/ajo-review-select-schedule.png)
1. Nella schermata **[!DNL Luma - In-App Messaging Campaign]**, seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifica trigger]**.
1. Nella finestra di dialogo **[!UICONTROL Attivatore messaggio in-app]**, configura i dettagli dell&#39;azione di tracciamento che attiva il messaggio in-app:
   1. Per rimuovere **[!UICONTROL Evento di avvio applicazione]**, selezionare ![Chiudi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg).
   1. Utilizza ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi condizione]** ripetutamente per generare la logica seguente per **[!UICONTROL Mostra messaggio se]**.
   1. Fai clic su **[!UICONTROL Fine]**.

      ![Logica di attivazione](assets/ajo-trigger-logic.png)

   Hai definito un&#39;azione di tracciamento, in cui **[!UICONTROL Azione]** è uguale a `in-app` e **[!UICONTROL Dati contestuali]** con l&#39;azione è una coppia chiave valore di `"showMessage" : "true"`.

1. Nella schermata **[!DNL Luma - In-App Messaging Campaign]**, seleziona **[!UICONTROL Verifica per attivare]**.
1. Nella schermata **[!UICONTROL Revisione da attivare (Luma - Campagna di messaggistica in-app)]**, seleziona **[!UICONTROL Attiva]**.
1. Vedi **[!DNL Luma - In-App Messaging Campaign]** con stato **[!UICONTROL Live]** nell&#39;elenco **[!UICONTROL Campagne]**.
   ![Elenco delle campagne](assets/ajo-campaign-list.png)


## Attivare il messaggio in-app

Disponi di tutti gli ingredienti necessari per inviare un messaggio in-app. Ciò che rimane è come attivare questo messaggio in-app nella tua app.

1. Vai a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore progetti Xcode. Trovare la funzione `func sendTrackAction(action: String, data: [String: Any]?)` e aggiungere il codice seguente, che chiama la funzione [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction), in base ai parametri `action` e `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Vai a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** in Xcode Project Navigator. Trova il codice per il pulsante Messaggio in-app e aggiungi il seguente codice:

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Convalida tramite l’app

1. Rigenera ed esegui l&#39;app nel simulatore o su un dispositivo fisico da Xcode, utilizzando ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Passa alla scheda **[!UICONTROL Impostazioni]**.

1. Tocca **[!UICONTROL Messaggio In-App]**. Il messaggio in-app viene visualizzato nell’app.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Convalidare l’implementazione in Assurance

Puoi convalidare i messaggi in-app nell’interfaccia utente di Assurance.

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Selezionare **[!UICONTROL Messaggistica in-app]**.
1. Seleziona **[!UICONTROL Elenco eventi]**.
1. Selezionare una voce **[!UICONTROL Messaggio visualizzato]**.
1. Controllare l&#39;evento non elaborato, in particolare `html`, che contiene il layout completo e il contenuto del messaggio in-app.
   ![Messaggio In-App Di Assurance](assets/assurance-in-app-display-message.png)


## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere messaggi in-app, laddove opportuno e applicabile. Ad esempio, la promozione di prodotti in base a interazioni specifiche che tieni traccia nell’app.

>[!SUCCESS]
>
>Hai abilitato l’app per la messaggistica in-app e aggiunto una campagna di messaggistica in-app tramite Journey Optimizer e l’estensione Journey Optimizer per Experience Platform Mobile SDK.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Creare e visualizzare le offerte](journey-optimizer-offers.md)**

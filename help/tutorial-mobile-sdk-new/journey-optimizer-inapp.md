---
title: Messaggistica in-app Adobe Journey Optimizer
description: Scopri come creare messaggi in-app per un’app mobile con Platform Mobile SDK e Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
source-git-commit: 5f0fa0b524cd4a12aaab8c8c0cd560a31003fbd8
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---

# Messaggistica in-app Journey Optimizer

Scopri come creare messaggi in-app per le app mobili con Platform Mobile SDK e Journey Optimizer.

Journey Optimizer consente di creare campagne per inviare messaggi in-app a tipi di pubblico mirati. Prima di inviare messaggi in-app con Journey Optimizer, è necessario assicurarsi che siano presenti le configurazioni e le integrazioni corrette. Per informazioni sul flusso di dati dei messaggi in-app in Journey Optimizer, consulta [la documentazione](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Questa lezione è facoltativa e si applica solo agli utenti di Journey Optimizer che desiderano inviare messaggi in-app.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Accesso a Journey Optimizer e autorizzazioni sufficienti come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). È inoltre necessaria un&#39;autorizzazione sufficiente per le seguenti funzioni di Journey Optimizer.
   * Gestire le campagne.
* Account sviluppatore Apple a pagamento con accesso sufficiente per creare certificati, identificatori e chiavi.
* Dispositivo fisico iOS o simulatore per test.
* ID app registrato con il servizio di notifica push di Apple
* Sono state aggiunte le credenziali app push in Raccolta dati
* Estensione tag Journey Optimizer installata
* Implementato Journey Optimizer nell’app


## Finalità di apprendimento

In questa lezione, potrai

* Registra l’ID app con il servizio di notifica push di Apple (APN).
* Crea una superficie app in AJO.
* Installa e configura l’estensione tag Journey Optimizer.
* Aggiorna l’app per includere l’estensione tag Journey Optimizer.
* Convalidare l&#39;impostazione in Assurance.
* Definisci la tua esperienza di campagna e messaggio in-app in Journey Optimizer.
* Invia il tuo messaggio in-app dall’app.

## Configurare l’app

>[!TIP]
>
>Se hai già configurato l&#39;app come parte del [Messaggi push di Journey Optimizer](journey-optimizer-push.md) esercitazione, puoi saltare questa sezione.

### Registra ID app con APNS

I passaggi seguenti non sono specifici per Adobe Experience Cloud e sono progettati per guidarti nella configurazione di APNS.

### Creare una chiave privata

1. Nel portale per sviluppatori di Apple, vai a **[!UICONTROL Chiavi]**.
1. Per creare una chiave, seleziona **[!UICONTROL +]**.
   ![crea nuova chiave](assets/mobile-push-apple-dev-new-key.png)

1. Fornisci un **[!UICONTROL Nome chiave]**.
1. Seleziona la **[!UICONTROL Servizio di notifica push di Apple] (APN)** casella di controllo.
1. Seleziona **[!UICONTROL Continua]**.
   ![configura nuova chiave](assets/mobile-push-apple-dev-config-key.png)
1. Rivedi la configurazione e seleziona **[!UICONTROL Registrati]**.
1. Scarica il file `.p8` chiave privata. Viene utilizzato nella configurazione della superficie dell’app.
1. Prendi nota di **[!UICONTROL ID chiave]**. Viene utilizzato nella configurazione della superficie dell’app.
1. Prendi nota di **[!UICONTROL ID team]**. Viene utilizzato nella configurazione della superficie dell’app.
   ![Dettagli chiave](assets/push-apple-dev-key-details.png)

La documentazione aggiuntiva può essere [trovato qui](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Aggiungere le credenziali push dell’app in Raccolta dati

1. Dalla sezione [Interfaccia di Data Collection](https://experience.adobe.com/data-collection/), seleziona **[!UICONTROL Superfici app]** nel pannello a sinistra.
1. Per creare una configurazione, seleziona **[!UICONTROL Crea superficie app]**.
   ![app surface home](assets/push-app-surface.png)
1. Immetti un **[!UICONTROL Nome]** per la configurazione, ad esempio `Luma App Tutorial`  .
1. Da **[!UICONTROL Configurazione applicazione mobile]**, seleziona **[!UICONTROL Apple iOS]**.
1. Immetti l’ID del bundle dell’app mobile in **[!UICONTROL ID app (ID bundle iOS)]** campo. Ad esempio,  `com.adobe.luma.tutorial.swiftui`.
1. Accendere il **[!UICONTROL Credenziali push]** per aggiungere le credenziali.
1. Trascina il file `.p8` **Chiave di autenticazione per notifica push Apple** file.
1. Fornisci **[!UICONTROL ID chiave]**, stringa di 10 caratteri assegnata durante la creazione di `p8` tasto auth. Si trova sotto **[!UICONTROL Chiavi]** scheda in **Certificati, identificatori e profili** delle pagine del portale Apple Developer. Vedi anche [Creare una chiave privata](#create-a-private-key).
1. Fornisci **[!UICONTROL ID team]**. L’ID team è un valore che si trova nella sezione **Iscrizione** o nella parte superiore della pagina del portale Apple Developer. Vedi anche [Creare una chiave privata](#create-a-private-key).
1. Seleziona **[!UICONTROL Salva]**.

   ![configurazione della superficie dell&#39;app](assets/push-app-surface-config.png)

### Installare l’estensione dei tag di Journey Optimizer

Affinché l’app funzioni con Journey Optimizer, devi aggiornare la proprietà del tag.

1. Accedi a **[!UICONTROL Tag]** > **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**,
1. Apri la proprietà, ad esempio **[!UICONTROL Tutorial sull’app mobile Luma]**.
1. Seleziona **[!UICONTROL Catalogo]**.
1. Cerca **[!UICONTROL Adobe Journey Optimizer]** estensione.
1. Installa l’estensione.
1. In **[!UICONTROL Installa estensione]** finestra di dialogo
   1. Seleziona un ambiente, ad esempio **[!UICONTROL Sviluppo]**.
   1. Seleziona la **[!UICONTROL Set di dati evento di tracciamento push AJO]** set di dati da **[!UICONTROL Set di dati evento]** elenco.
   1. Seleziona **[!UICONTROL Salva nella libreria e genera]**.
      ![Impostazioni estensione AJO](assets/push-tags-ajo.png)

>[!NOTE]
>
>Se non vedi `AJO Push Tracking Experience Event Dataset` contatta l’assistenza clienti come opzione.
>

### Implementare Journey Optimizer nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. Ora devi installare e registrare l’SDK di messaggistica. Se questi passaggi non sono chiari, rivedi [Installare gli SDK](install-sdks.md) sezione.

>[!NOTE]
>
>Se hai completato il [Installare gli SDK](install-sdks.md) , l&#39;SDK è già installato e puoi saltare questo passaggio.
>

1. In Xcode, assicurati che [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios.git) viene aggiunto all’elenco dei pacchetti in Dipendenze dai pacchetti. Consulta [Gestione pacchetti Swift](install-sdks.md#swift-package-manager).
1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** nel Navigatore progetti Xcode.
1. Assicurare `AEPMessaging` fa parte dell’elenco delle importazioni.

   `import AEPMessaging`

1. Assicurare `Messaging.self` fa parte dell’array di estensioni che si stanno registrando.

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

1. Aggiungi il `MobileCore.setPushIdentifier` al `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)` funzione.

   ```swift
   // Send push token to Experience Platform
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Questa funzione recupera il token del dispositivo univoco per il dispositivo su cui è installata l’app. Quindi imposta il token per la consegna delle notifiche push utilizzando la configurazione impostata e che si basa sul servizio APN (Push Notification Service) di Apple.


## Convalidare la garanzia di installazione

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app sul dispositivo fisico o sul simulatore.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Nell’interfaccia utente Assurance, seleziona **[!UICONTROL Configura]**.
   ![configura clic](assets/push-validate-config.png)
1. Seleziona la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) pulsante accanto a **[!UICONTROL Messaggistica in-app]**.
1. Seleziona **[!UICONTROL Salva]**.
   ![salva](assets/assurance-in-app-config.png)
1. Seleziona **[!UICONTROL Messaggistica in-app]** dal menu di navigazione a sinistra.
1. Seleziona la **[!UICONTROL Convalida]** scheda.
1. Verifica che non siano presenti errori.
   ![Convalida in-app](assets/assurance-in-app-validate.png)


## Creare un messaggio in-app personalizzato

Per creare un messaggio in-app personalizzato, devi definire una campagna in Journey Optimizer che attivi un messaggio in-app in base agli eventi che si verificano. Questi eventi possono essere:

* dati inviati a Adobe Experience Platform,
* eventi di tracciamento di base, come azioni, oppure stato o raccolta di dati PII, tramite le API generiche core mobile,
* eventi del ciclo di vita dell&#39;applicazione, ad esempio avvio, installazione, aggiornamento, chiusura o arresto anomalo,
* eventi di geolocalizzazione, come l’ingresso o l’uscita da un punto di interesse.

In questo tutorial, utilizzerai le API generiche core per dispositivi mobili e indipendenti dalle estensioni per facilitare il tracciamento degli eventi relativi a schermate utente, azioni e dati PII. Gli eventi generati da queste API vengono pubblicati nell’hub eventi SDK e sono disponibili per l’utilizzo da parte delle estensioni. Ad esempio, quando è installata l’estensione Analytics, tutti i dati relativi agli eventi delle azioni utente e delle schermate dell’app vengono inviati agli endpoint di reporting di Analytics appropriati.

1. Nell’interfaccia utente di Journey Optimizer, seleziona **[!UICONTROL Campagne]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Crea campagna]**.
1. In **[!UICONTROL Crea campagna]** schermata:
   1. Seleziona **[!UICONTROL Messaggio in-app]** e seleziona una superficie di app dalla sezione **[!UICONTROL Superficie app]** elenco, ad esempio **[!UICONTROL App mobile Luma]**.
   1. Seleziona **[!UICONTROL Crea]**
      ![Proprietà campagna](assets/ajo-campaign-properties.png)
1. Nella schermata di definizione di Campaign, in **[!UICONTROL Proprietà]**, immetti un **[!UICONTROL Nome]** per la campagna, ad esempio `Luma - In-App Messaging Campaign`, e un **[!UICONTROL Descrizione]**, ad esempio `In-app messaging campaign for Luma app`.
   ![Nome della campagna](assets/ajo-campaign-properties-name.png)
1. Scorri verso il basso fino a **[!UICONTROL Azione]**, e seleziona **[!UICONTROL Modifica contenuto]**.
1. In **[!UICONTROL Messaggio in-app]** schermata:
   1. Seleziona **[!UICONTROL Modale]** come **[!UICONTROL Layout messaggio]**.
   2. Invio `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` per **[!UICONTROL URL contenuto multimediale]**.
   3. Immetti un **[!UICONTROL Intestazione]**, ad esempio `Welcome to this Luma In-App Message` e inserisci un **[!UICONTROL Corpo]**, ad esempio `Triggered by pushing that button in the app...`.
   4. Invio **[!UICONTROL Ignora]** come **[!UICONTROL Testo #1 pulsante (primario)]**.
   5. Nota come viene aggiornata l’anteprima.
   6. Seleziona **[!UICONTROL Controlla per attivare]**.
      ![Editor in-app](assets/ajo-in-app-editor.png)
1. In **[!UICONTROL Revisione per l’attivazione (Luma - Campagna di messaggistica in-app)]** schermata, seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) nel **[!UICONTROL Pianificazione]** affiancare.
   ![Rivedi pianificazione seleziona Pianificazione](assets/ajo-review-select-schedule.png)
1. Torna in **[!UICONTROL Luma - Campagna di messaggistica in-app]** schermata, seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifica trigger]**.
1. In **[!UICONTROL Attivatore messaggio in-app]** nella finestra di dialogo, configura i dettagli dell’azione di tracciamento che attiva il messaggio in-app:
   1. Da rimuovere **[!UICONTROL Evento di avvio dell’applicazione]**, seleziona ![Chiudi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Utilizzare ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi condizione]** ripetutamente per generare la logica seguente per **[!UICONTROL Mostra messaggio se]**.
   1. Fai clic su **[!UICONTROL Fine]**.
      ![Logica di attivazione](assets/ajo-trigger-logic.png)

   È stata definita un&#39;azione di tracciamento, in cui **[!UICONTROL Azione]** è uguale a `in-app` e **[!UICONTROL Dati contestuali]** con l&#39;azione è una coppia chiave-valore di `"showMessage" : "true"`.

1. Torna in **[!UICONTROL Luma - Campagna di messaggistica in-app]** schermata, seleziona **[!UICONTROL Controlla per attivare]**.
1. In **[!UICONTROL Revisione per l’attivazione (Luma - Campagna di messaggistica in-app)]** schermata, seleziona **[!UICONTROL Attiva]**.
1. Vedi il tuo **[!UICONTROL Luma - Campagna di messaggistica in-app]** con stato **[!UICONTROL Live]** nel **[!UICONTROL Campagne]** elenco.
   ![Elenco delle campagne](assets/ajo-campaign-list.png)


## Attivazione del messaggio in-app

Disponi di tutti gli ingredienti necessari per inviare un messaggio in-app. Ciò che rimane è come attivare questo messaggio in-app nella tua app.

1. Vai a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode. Trova il `func sendTrackAction(action: String, data: [String: Any]?)` e aggiungi il seguente codice, che chiama il `MobileCore.track` funzione, in base ai parametri `action` e `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Vai a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Generale]** > **[!UICONTROL ConfigView]** nel Navigatore progetti Xcode. Trova il codice per il pulsante Messaggio in-app e aggiungi il seguente codice:

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Convalida tramite l’app

1. Apri l’app su un dispositivo o nel simulatore.

1. Vai a **[!UICONTROL Impostazioni]** scheda.

1. Tocca **[!UICONTROL Messaggio in-app]**. Il messaggio in-app viene visualizzato nell’app.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Convalida implementazione in Assurance

Puoi convalidare i messaggi in-app nell’interfaccia utente Assurance.

1. Seleziona **[!UICONTROL Messaggistica in-app]**.
1. Seleziona **[!UICONTROL Elenco eventi]**.
1. Seleziona un **[!UICONTROL Visualizza messaggio]** voce.
1. Inspect l’evento non elaborato, in particolare `html`, che contiene il layout completo e il contenuto del messaggio in-app.
   ![Messaggio in-app Assurance](assets/assurance-in-app-display-message.png)


## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere messaggi in-app, laddove pertinente e applicabile, all’app Luma. Ad esempio, promuovendo prodotti in base a interazioni specifiche tracciate nell’app.

>[!SUCCESS]
>
>Hai abilitato l’app per la messaggistica in-app e aggiunto una campagna di messaggistica in-app tramite Journey Optimizer e l’estensione Journey Optimizer per l’SDK di Mobile di Experience Platform.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Visualizzare le offerte con Journey Optimizer](journey-optimizer-offers.md)**

---
title: Messaggi push di Adobe Journey Optimizer
description: Scopri come creare messaggi push in un’app mobile con Platform Mobile SDK e Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '2173'
ht-degree: 2%

---

# Messaggi push di Journey Optimizer

Scopri come creare messaggi push per le app mobili con Platform Mobile SDK e Journey Optimizer.

Journey Optimizer consente di creare percorsi e inviare messaggi a tipi di pubblico mirati. Prima di inviare le notifiche push con Journey Optimizer, devi verificare che siano presenti le configurazioni e le integrazioni corrette. Per informazioni sul flusso di dati delle notifiche push in Journey Optimizer, consulta [documentazione](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Questa lezione è facoltativa e si applica solo agli utenti di Journey Optimizer che desiderano inviare messaggi push.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Accesso a Journey Optimizer e autorizzazioni sufficienti come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). È inoltre necessaria un&#39;autorizzazione sufficiente per le seguenti funzioni di Journey Optimizer.
   * Crea una superficie app.
   * Creare un percorso
   * Crea un messaggio.
   * Creare predefiniti per messaggi.
* Account sviluppatore Apple a pagamento con accesso sufficiente per creare certificati, identificatori e chiavi.
* Dispositivo fisico iOS o simulatore per test.

## Finalità di apprendimento

In questa lezione, potrai

* Registra l’ID app con il servizio APNS (Apple Push Notification Service).
* Crea una superficie app in AJO.
* Aggiorna lo schema per includere i campi di messaggistica push.
* Installa e configura l’estensione tag Journey Optimizer.
* Aggiorna l’app per includere l’estensione tag Journey Optimizer.
* Convalidare l&#39;impostazione in Assurance.
* Invia un messaggio di prova da Assurance
* Definisci in Journey Optimizer l’evento, il percorso e l’esperienza della notifica push.
* Invia una notifica push personalizzata dall’app.


## Configurazione

>[!TIP]
>
>Se hai già configurato l’ambiente come parte del [Messaggistica in-app Journey Optimizer](journey-optimizer-inapp.md) esercitazione, puoi saltare questa sezione.

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
1. Seleziona ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto a **[!UICONTROL Debug push]**.
1. Seleziona **[!UICONTROL Salva]**.
   ![salva](assets/push-validate-save.png)
1. Seleziona **[!UICONTROL Debug push]** dal menu di navigazione a sinistra.
1. Seleziona la **[!UICONTROL Convalida configurazione]** scheda.
1. Selezionare il dispositivo dalla **[!UICONTROL Client]** elenco.
1. Verifica che non siano presenti errori.
   ![convalida](assets/push-validate-confirm.png)
1. Seleziona la **[!UICONTROL Invia messaggio push di prova]** scheda.
1. (facoltativo) Modifica dei dettagli predefiniti per **[!UICONTROL Titolo]** e **[!UICONTROL Corpo]**
1. Seleziona ![Bug](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Invia notifica push di prova]**.
1. Controlla la **[!UICONTROL Risultati del test]**.
1. Dovresti visualizzare nell’app la notifica push di prova.

   <img src="assets/luma-app-push.png" width="300" />


## Creare una notifica push personalizzata

Per creare una notifica push personalizzata, devi definire un evento in Journey Optimizer che attivi un percorso che si occupi di inviare una notifica push.

### Aggiornare lo schema

Stai per definire un nuovo tipo di evento, non ancora disponibile, come parte dell’elenco degli eventi definiti nello schema. Questo tipo di evento verrà utilizzato successivamente quando si attivano le notifiche push.

1. Nell’interfaccia utente di Journey Optimizer, seleziona **[!UICONTROL Schemi]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Sfoglia]** nella barra delle schede.
1. Seleziona lo schema, ad esempio **[!UICONTROL Schema evento app mobile Luma]** per aprirlo.
1. Nell’editor schema:
   1. Seleziona la **[!UICONTROL eventType]** campo.
   1. In **[!UICONTROL Proprietà campo]** , scorri verso il basso per visualizzare l’elenco dei valori possibili per il tipo di evento. Seleziona **[!UICONTROL Aggiungi riga]**, e aggiungi `application.test` come **[!UICONTROL VALORE]** e **[!UICONTROL Evento di test per notifica push]** come `DISPLAY NAME`.
   1. Seleziona **[!UICONTROL Applica]**.
   1. Seleziona **[!UICONTROL Salva]**.
      ![Aggiungi valore ai tipi di evento](assets/ajo-update-schema-eventtype-enum.png)

### Definire un evento

Gli eventi in Journey Optimizer ti consentono di attivare i percorsi in modo unitario per inviare messaggi, ad esempio notifiche push. Consulta [Informazioni sugli eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en) per ulteriori informazioni.

1. Nell’interfaccia utente di Journey Optimizer, seleziona **[!UICONTROL Configurazioni]** dalla barra a sinistra.

1. In **[!UICONTROL Dashboard]** , seleziona la **[!UICONTROL Gestisci]** pulsante in **[!UICONTROL Eventi]** affiancare.

1. In **[!UICONTROL Eventi]** schermata, seleziona **[!UICONTROL Crea evento]**.

1. In **[!UICONTROL Modifica evento 1]** riquadro:

   1. Invio `LumaTestEvent` come **[!UICONTROL Nome]** dell’evento.
   1. Fornisci un **[!UICONTROL Descrizione]**, ad esempio `Test event to trigger push notifications in Luma app`.

   1. Seleziona lo schema evento esperienza app mobile creato in precedenza in [Creare uno schema XDM](create-schema.md) dal **[!UICONTROL Schema]** elenco, ad esempio **[!UICONTROL Schema evento app mobile Luma v.1]**.
   1. Seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) accanto al **[!UICONTROL Campi]** elenco.

      ![Modifica passaggio evento 1](assets/ajo-edit-event1.png)

      In **[!UICONTROL Campi]** , accertati che siano selezionati i seguenti campi (oltre ai campi predefiniti sempre selezionati (**[!UICONTROL _id]**, **[!UICONTROL id]**, e **[!UICONTROL timestamp]**). Utilizzando l’elenco a discesa puoi alternare tra **[!UICONTROL Selezionato]**, **[!UICONTROL Tutti]** e **[!UICONTROL Principale]** o utilizza ![Ricerca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) campo.

      * **[!UICONTROL Identificato dall’applicazione (ID)]**,
      * **[!UICONTROL Tipo evento (eventType)]**,
      * **[!UICONTROL Principale (principale)]**.

      ![Modifica campi evento](assets/ajo-event-fields.png)

      Quindi seleziona **[!UICONTROL Ok]**.

   1. Seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) accanto al **[!UICONTROL Condizione ID evento]** campo.

      1. In **[!UICONTROL Aggiungi una condizione per l’ID evento]** finestra di dialogo, trascinamento della selezione **[!UICONTROL Tipo evento (eventType)]** su a **[!UICONTROL Trascina qui un elemento]**.
      1. Nel popover, scorri verso il basso e seleziona **[!UICONTROL application.test]** (tipo di evento aggiunto in precedenza all&#39;elenco dei tipi di evento come parte di [Aggiornare lo schema](#update-your-schema)). Quindi scorri verso l’alto e seleziona **[!UICONTROL Ok]**.
      1. Seleziona **[!UICONTROL Ok]** per salvare la condizione.
         ![Modifica condizione evento](assets/ajo-edit-condition.png)

   1. Seleziona **[!UICONTROL ECID (ECID)]** dal **[!UICONTROL Namespace]** elenco. Automaticamente il **[!UICONTROL Identificatore profilo]** il campo è compilato con **[!UICONTROL ID del primo elemento dell’ECID chiave per la mappa identityMap]**.
   1. Seleziona **[!UICONTROL Salva]**.
      ![Modifica passaggio evento 2](assets/ajo-edit-event2.png)

Hai appena creato una configurazione dell’evento basata sullo schema degli eventi di esperienza per app mobile creato in precedenza come parte di questa esercitazione. Questa configurazione dell’evento filtrerà gli eventi di esperienza in arrivo utilizzando l’identificatore dell’app mobile. In questo modo, assicurati che solo gli eventi avviati dall’app mobile attiveranno il percorso che creerai nel passaggio successivo. In uno scenario reale, potrebbe essere utile inviare notifiche push da un servizio esterno, tuttavia si applicano gli stessi concetti: dall’applicazione esterna invia un evento esperienza in Experienci Platform che ha campi specifici che puoi utilizzare per applicare condizioni su prima che questi eventi attivino un percorso.

### Creazione del percorso

Il passaggio successivo consiste nel creare il percorso che attiva l’invio della notifica push alla ricezione dell’evento appropriato.

1. Nell’interfaccia utente di Journey Optimizer, seleziona **[!UICONTROL Percorsi]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Crea Percorso]**.
1. In **[!UICONTROL Proprietà percorso]** pannello:

   1. Immetti un **[!UICONTROL Nome]** per il percorso, ad esempio `Luma - Test Push Notification Journey`.
   1. Immetti un **[!UICONTROL Descrizione]** per il percorso, ad esempio `Journey for test push notifications in Luma mobile app`.
   1. Assicurare **[!UICONTROL Consenti rientro]** è selezionato e impostato **[!UICONTROL Periodo di attesa per rientro]** a **[!UICONTROL 30]** **[!UICONTROL Secondi]**.
   1. Seleziona **[!UICONTROL Ok]**.
      ![Proprietà del percorso](assets/ajo-journey-properties.png)

1. Tornando all&#39;area di lavoro del percorso, dal **[!UICONTROL EVENTI]**, trascina ![Evento](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!UICONTROL LumaTestEvent]** nell’area di lavoro in cui viene visualizzato **[!UICONTROL Seleziona un evento di ingresso o un’attività di lettura del pubblico]**.

   * In **[!UICONTROL Eventi: LumaTestEvent]** , immettere un **[!UICONTROL Etichetta]**, ad esempio `Luma Test Event`.

1. Dalla sezione **[!UICONTROL AZIONI]** menu a discesa, trascinamento della selezione ![Push](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Push]** il ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) apparendo a destra del **[!UICONTROL LumaTestEvent]** attività. In **[!UICONTROL Azioni: push]** riquadro:

   1. Fornisci un **[!UICONTROL Etichetta]**, ad esempio `Luma Test Push Notification`, fornisci un **[!UICONTROL Descrizione]**, ad esempio `Test push notification for Luma mobile app`, seleziona **[!UICONTROL Transazionale]** dal **[!UICONTROL Categoria]** elenca e seleziona **[!UICONTROL Luma]** dal **[!UICONTROL Superficie push]**.
   1. Seleziona ![Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifica contenuto]** per iniziare a modificare la notifica push effettiva.
      ![Proprietà push](assets/ajo-push-properties.png)

      In **[!UICONTROL Notifica push]** editor:

      1. Immetti un **[!UICONTROL Titolo]**, ad esempio `Luma Test Push Notification` e inserisci un **[!UICONTROL Corpo]**, ad esempio `Test push notification for Luma mobile app`.
      1. Per salvare e lasciare l’editor, seleziona ![Freccia sinistra](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Editor push](assets/ajo-push-editor.png)

   1. Per salvare e terminare la definizione della notifica push, seleziona **[!UICONTROL Ok]**.

1. Il percorso deve essere simile al seguente. Seleziona **[!UICONTROL Pubblica]** per pubblicare e attivare il percorso.
   ![Percorso finito](assets/ajo-journey-finished.png)


## Attivazione della notifica push

Sono disponibili tutti gli ingredienti per inviare una notifica push. Ciò che rimane è come attivare questa notifica push. In sostanza, è lo stesso che hai visto prima: invia semplicemente un evento di esperienza con il payload corretto (come in ![Eventi](events.md)).

Questa volta l’evento esperienza che stai per inviare non è costruito per creare un semplice dizionario XDM. Stai per utilizzare uno struct che rappresenta un payload di notifica push. La definizione di un tipo di dati dedicato rappresenta un modo alternativo di implementare la costruzione dei payload dell’evento esperienza nell’applicazione.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Modello]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** nel Navigatore progetti Xcode ed esamina il codice.

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   Il codice è una rappresentazione del seguente semplice payload che stai per inviare per attivare il percorso di notifica push di prova

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]** nel Navigator del progetto Xcode e aggiungi il seguente codice a `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```swift
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   Questo codice crea un `testPushPayload` che utilizza i parametri forniti alla funzione (`applicationId` e `eventType`) e quindi chiamate `sendExperienceEvent` durante la conversione del payload in un dizionario. Questo codice, questa volta, prende in considerazione anche gli aspetti asincroni della chiamata all’SDK di Adobe Experience Platform utilizzando il modello di concorrenza di Swift basato su `await` e `async`.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Generale]** > **[!UICONTROL ConfigView]** nel Navigatore progetti Xcode. Nella definizione del pulsante di notifica push, aggiungi il seguente codice per inviare il payload dell’evento di esperienza di notifica push di prova in modo da attivare il percorso ogni volta che il pulsante viene toccato.

   ```swift
   // Setting parameters and calling function to send push notification
   let eventType = "mobileapp.testpush"
   let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
   await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)   
   ```


## Convalida tramite l’app

1. Apri l’app su un dispositivo o nel simulatore.

1. Vai a **[!UICONTROL Impostazioni]** scheda.

1. Tocca **[!UICONTROL Notifica push]**. Nell’app viene visualizzata la notifica push.
   <img src="assets/ajo-test-push.png" width="300" />


## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare a creare percorsi che inviano notifiche push e per gestire le notifiche push in app da Journey Optimizer. Ad esempio, dare il benvenuto all’utente quando effettua l’accesso all’app.

>[!SUCCESS]
>
>Ora hai abilitato l’app per le notifiche push tramite Journey Optimizer e l’estensione Journey Optimizer per l’SDK di Experienci Platform Mobile.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Messaggistica in-app con Journey Optimizer](journey-optimizer-inapp.md)**


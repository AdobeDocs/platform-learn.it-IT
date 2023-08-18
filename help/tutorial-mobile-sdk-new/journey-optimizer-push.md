---
title: Messaggi push di Adobe Journey Optimizer
description: Scopri come creare messaggi push in un’app mobile con Platform Mobile SDK e Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# Messaggi push di Adobe Journey Optimizer

Scopri come creare messaggi push per le app mobili con Platform Mobile SDK e Adobe Journey Optimizer.

Journey Optimizer consente di creare percorsi e inviare messaggi a tipi di pubblico mirati. Prima di inviare le notifiche push con Journey Optimizer, devi verificare che siano presenti le configurazioni e le integrazioni corrette. Per informazioni sul flusso di dati delle notifiche push in Adobe Journey Optimizer, consulta [la documentazione](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Questa lezione è facoltativa e si applica solo agli utenti di Adobe Journey Optimizer che desiderano inviare messaggi push.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Accesso a Adobe Journey Optimizer e autorizzazioni sufficienti come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Inoltre, è necessario disporre di autorizzazioni sufficienti per le seguenti funzionalità di Adobe Journey Optimizer.
   * Crea una superficie app.
   * Creare un percorso
   * Crea un messaggio.
   * Creare predefiniti per messaggi.
* Account sviluppatore Apple a pagamento con accesso sufficiente per creare certificati, identificatori e chiavi.
* Dispositivo iOS fisico da testare.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Registra l’ID app con il servizio di notifica push di Apple (APN).
* Creare un **[!UICONTROL Superficie app]** in AJO.
* Aggiorna il tuo **[!UICONTROL schema]** per includere i campi dei messaggi push.
* Installare e configurare **[!UICONTROL Adobe Journey Optimizer]** estensione tag.
* Aggiorna l’app per includere l’estensione tag AJO.
* Convalidare l&#39;impostazione in Assurance.
* Invia un messaggio di prova.


## Registra ID app con APN

I passaggi seguenti non sono specifici per Adobe Experience Cloud e sono progettati per guidarti nella configurazione di APN.

### Creare una chiave privata

1. Nel portale per sviluppatori di Apple, vai a **[!UICONTROL Chiavi]**.
1. Per creare una chiave, seleziona **[!UICONTROL +]**.
   ![crea nuova chiave](assets/mobile-push-apple-dev-new-key.png)

1. Fornisci un **[!UICONTROL Nome chiave]**.
1. Seleziona la **[!UICONTROL APN]** casella di controllo.
1. Seleziona **[!UICONTROL Continua]**.
   ![configura nuova chiave](assets/mobile-push-apple-dev-config-key.png)
1. Rivedi la configurazione e seleziona **[!UICONTROL Registrati]**.
1. Scarica il file `.p8` chiave privata. Viene utilizzato nella configurazione della superficie dell’app.
1. Prendi nota di [!UICONTROL ID chiave]. Viene utilizzato nella configurazione della superficie dell’app.
1. Prendi nota di [!UICONTROL ID team]. Viene utilizzato nella configurazione della superficie dell’app.
   ![Dettagli chiave](assets/push-apple-dev-key-details.png)

La documentazione aggiuntiva può essere [trovato qui](https://help.apple.com/developer-account/#/devcdfbb56a3).

## Aggiungere le credenziali push dell’app in Raccolta dati

1. Dalla sezione [Interfaccia di Data Collection](https://experience.adobe.com/data-collection/), seleziona **[!UICONTROL Superfici app]** nel pannello a sinistra.
1. Per creare una configurazione, seleziona **[!UICONTROL Creare superfici dell&#39;app]**.
   ![app surface home](assets/push-app-surface.png)
1. Immetti un **[!UICONTROL Nome]** per la configurazione, ad esempio `Luma App Tutorial`  .
1. Da Mobile Application Configuration (Configurazione applicazione mobile), seleziona **[!UICONTROL Apple iOS]**.
1. Immetti l’ID del bundle per app mobile nel campo ID app (ID bundle iOS). Se segui insieme all’app Luma, tale valore è `com.adobe.luma.tutorial.swiftui`.
1. Accendere il **[!UICONTROL Credenziali push]** per aggiungere le credenziali.
1. Trascina il file `.p8` **Chiave di autenticazione per notifica push Apple** file.
1. Fornisci **[!UICONTROL ID chiave]**, stringa di 10 caratteri assegnata durante la creazione di `p8` tasto auth. È disponibile in **[!UICONTROL Chiavi]** scheda in **Certificati, identificatori e profili** delle pagine del portale Apple Developer.
1. Fornisci **[!UICONTROL ID team]**. L’ID team è un valore che si trova nella sezione **Iscrizione** o nella parte superiore delle pagine del portale Apple Developer.
1. Seleziona **[!UICONTROL Salva]**.

   ![configurazione della superficie dell&#39;app](assets/push-app-surface-config.png)

## Installare l’estensione dei tag di Adobe Journey Optimizer

1. Accedi a **[!UICONTROL Tag]** > **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**,
1. Apri la proprietà, ad esempio **[!UICONTROL Tutorial sull’app mobile Luma]**.
1. Seleziona **[!UICONTROL Catalogo]**.
1. Cerca **[!UICONTROL Adobe Journey Optimizer]** estensione.
1. Installa l’estensione.
1. In **[!UICONTROL Installa estensione]** finestra di dialogo
   1. Seleziona un ambiente, ad esempio **[!UICONTROL Sviluppo]**.
   1. Seleziona la **[!UICONTROL Set di dati evento di tracciamento push AJO]** set di dati da **[!UICONTROL Set di dati evento]** elenco a discesa.
      ![Impostazioni estensione AJO](assets/push-tags-ajo.png)
   1. Seleziona **[!UICONTROL Salva nella libreria e genera]**.

>[!NOTE]
>
>Se non vedi `AJO Push Tracking Experience Event Dataset` contatta l’assistenza clienti come opzione.
>

## Implementare Adobe Journey Optimizer nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. Ora devi installare e registrare l’SDK di messaggistica. Se questi passaggi non sono chiari, rivedi [Installare gli SDK](install-sdks.md) sezione.

>[!NOTE]
>
>Se hai completato il [Installare gli SDK](install-sdks.md) , l&#39;SDK è già installato e puoi passare al passaggio #7.
>

1. In Xcode, assicurati che [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios.git) viene aggiunto all’elenco dei pacchetti in Dipendenze dai pacchetti. Consulta [Gestione pacchetti Swift](install-sdks.md#swift-package-manager).
1. Apri Xcode e passa a **[!UICONTROL AppDelegate]**.
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

1. Aggiungi il `MobileCore.setPushIdentifier` al `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` funzione.

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   Questa funzione recupera il token del dispositivo univoco per il dispositivo su cui è installata l’app e invia il token ad Adobe Apple per la consegna dei messaggi push.

## Convalidare inviando un messaggio push di prova

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app sul dispositivo fisico o sul simulatore.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Nell’interfaccia utente Assurance, seleziona **[!UICONTROL Configura]**.
   ![configura clic](assets/push-validate-config.png)
1. Seleziona la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) pulsante accanto a **[!UICONTROL Debug push]**.
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
1. Dovresti visualizzare la notifica push nell’app.

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>Ora hai abilitato l’app per le notifiche push tramite l’estensione Adobe Journey Optimizer per l’SDK di Adobe Experience Platform Mobile.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Conclusione e prossime tappe](conclusion.md)**

---
title: Messaggi push di Adobe Journey Optimizer
description: Scopri come creare messaggi push in un’app mobile con Platform Mobile SDK e Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '881'
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

### Creare un `.p8` chiave privata

1. Nel portale per sviluppatori di Apple, vai a **[!UICONTROL Chiavi]**.
1. Seleziona l’icona + per creare una chiave.
   ![crea nuova chiave](assets/mobile-push-apple-dev-new-key.png)

1. Fornisci un **[!UICONTROL Nome chiave]**.
1. Seleziona la **[!UICONTROL APN]** casella di controllo.
1. Seleziona **[!UICONTROL Continua]**.
   ![configura nuova chiave](assets/mobile-push-apple-dev-config-key.png)
1. Rivedi la configurazione e seleziona **[!UICONTROL Registrati]**.
1. Scarica il file `.p8` chiave privata. Viene utilizzato nella configurazione della superficie dell’app.
1. Prendi nota di **[!UICONTROL ID chiave]**. Viene utilizzato nella configurazione della superficie dell’app.

La documentazione aggiuntiva può essere [trovato qui](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Recupera l’ID del team di sviluppo di Apple

1. Nel portale per sviluppatori di Apple, vai a **[!UICONTROL Iscrizione]**.
1. Il tuo **[!UICONTROL ID team]** viene elencato insieme alle altre informazioni di iscrizione. Viene utilizzato nella configurazione della superficie dell’app.

## Aggiungere le credenziali push dell’app in Raccolta dati

1. Dalla sezione [Interfaccia di Data Collection](https://experience.adobe.com/data-collection/), seleziona la scheda Superfici app nel pannello a sinistra.
1. Seleziona **[!UICONTROL Creare superfici dell&#39;app]** per creare una configurazione.
   ![app surface home](assets/mobile-push-app-surface.png)
1. Immetti un **[!UICONTROL Nome]** per la configurazione, ad esempio `Luma App Tutorial`  .
1. Da Mobile Application Configuration (Configurazione applicazione mobile), seleziona **[!UICONTROL Apple iOS]**.
1. Immetti l’ID del bundle per app mobile nel campo ID app (ID bundle iOS). Se segui insieme all’app Luma, tale valore è `com.adobe.luma.tutorial`.
1. Accendere il **[!UICONTROL Credenziali push]** per aggiungere le credenziali.
1. Trascina il file `.p8` **Chiave di autenticazione per notifica push Apple** file.
1. Specifica l&#39;ID chiave, una stringa di 10 caratteri assegnata durante la creazione di `p8` tasto auth. Si trova nella scheda Chiavi in **Certificati, identificatori e profili** pagina.
1. Immetti l’ID del team. Si tratta di un valore stringa che si trova sotto **Iscrizione** scheda.
1. Seleziona **[!UICONTROL Salva]**.
   ![configurazione della superficie dell&#39;app](assets/mobile-push-app-surface-config.png)

## Installare l’estensione dei tag di Adobe Journey Optimizer

1. Accedi a [!UICONTROL Tag] > [!UICONTROL Estensioni] > [!UICONTROL Catalogo], e trovare il **[!UICONTROL Adobe Journey Optimizer]** estensione.
1. Installa l’estensione.
   ![installare l’estensione ajo](assets/mobile-push-tags-install.png)
1. Seleziona `CJM Push Tracking Experience Event Dataset` il set di dati di Adobe Experience Platform.
   ![Impostazioni estensione AJO](assets/mobile-push-tags-ajo.png)
1. Seleziona **[!UICONTROL Salva nella libreria e genera]**.

>[!NOTE]
>Se non vedi &quot;Set di dati evento di tracciamento push CJM&quot; come opzione, contatta l’assistenza clienti.
>

## Implementare Adobe Journey Optimizer nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. Ora devi installare e registrare l’SDK di messaggistica. Se questi passaggi non sono chiari, rivedi il [Installare gli SDK](install-sdks.md) sezione.

>[!NOTE]
>
>Se hai completato il [Installare gli SDK](install-sdks.md) , l&#39;SDK è già installato e puoi passare al passaggio #7.

1. Apri il `Podfile` e aggiungi la riga seguente e salva il file.

   `pod 'AEPMessaging', '~>1'`
1. Apri il terminale e passa alla cartella contenente il tuo `Podfile`.
1. Installare l’SDK eseguendo il comando `pod install`.
   ![convalida consenso](assets/mobile-push-terminal-install.png)
1. Apri Xcode e passa a `AppDelegate.swift`.
1. Aggiungi quanto segue all’elenco delle importazioni.

   `import AEPMessaging`
1. Aggiungi `Messaging.self` all’array di estensioni che si stanno registrando.
1. Aggiungi la seguente funzione al file.

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   Questa funzione recupera il token del dispositivo univoco per il dispositivo su cui è installata l’app e lo invia ad Adobe/Apple per la consegna dei messaggi push.

## Convalidare inviando un messaggio push di prova

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app sul dispositivo fisico.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Invia l&#39;app in background.
1. Nell’interfaccia utente Assurance, seleziona **[!UICONTROL Configura]**.
   ![configura clic](assets/mobile-push-validate-config.png)
1. Seleziona la **[!UICONTROL +]** pulsante accanto a **[!UICONTROL Debug push]**.
1. Seleziona **[!UICONTROL Salva]**.
   ![salva](assets/mobile-push-validate-save.png)
1. Seleziona **[!UICONTROL Debug push]** dal menu di navigazione a sinistra.
1. Selezionare il dispositivo dalla **[!UICONTROL Elenco client]**.
1. Verifica che non siano presenti errori.
   ![convalida](assets/mobile-push-validate-confirm.png)
1. Scorri verso il basso e seleziona **[!UICONTROL Invia notifica push di prova]**.
1. Conferma di non ricevere ed errori e di ricevere il messaggio sul dispositivo.
   ![invia push di prova](assets/mobile-push-validate-send-test.png)

Successivo: **[Conclusione e prossime tappe](conclusion.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
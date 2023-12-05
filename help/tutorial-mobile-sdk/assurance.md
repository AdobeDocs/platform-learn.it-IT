---
title: Configurare Assurance per le implementazioni dell’SDK di Platform Mobile
description: Scopri come implementare l’estensione Assurance in un’app mobile.
feature: Mobile SDK,Assurance
jira: KT-14628
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 6%

---

# Configura Assurance

Scopri come configurare Adobe Experience Platform Assurance in un’app mobile.

Assurance, formalmente noto come Project Griffon, è progettato per aiutarti a ispezionare, verificare, simulare e convalidare come raccolgi dati o distribuisci esperienze nella tua app mobile.

Assurance consente di controllare gli eventi SDK non elaborati generati da Adobe Experience Platform Mobile SDK. Tutti gli eventi raccolti dall’SDK sono disponibili per il controllo. Gli eventi SDK vengono caricati in una vista a elenco, ordinati in ordine cronologico. Ogni evento dispone di una vista dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili viste aggiuntive per sfogliare la configurazione dell’SDK, gli elementi dati, gli stati condivisi e le versioni delle estensioni SDK. Ulteriori informazioni su [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) nella documentazione del prodotto.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata configurata.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Conferma che la tua organizzazione disponga dell’accesso (e richiedilo in caso contrario).
* Imposta l’URL di base.
* Aggiungi il codice iOS specifico richiesto.
* Connettersi a una sessione.

## Conferma accesso

Assicurati che la tua organizzazione abbia accesso a Assurance. Come utente, devi essere aggiunto al profilo per Adobe Experience Platform. Consulta [Accesso utente](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) nella guida Assurance per ulteriori informazioni.

## Implementazione

Oltre al generale [Installazione SDK](install-sdks.md), hai completato la lezione precedente, iOS richiede anche la seguente aggiunta per avviare la sessione Assurance per la tua app.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** nel Navigatore progetti di Xcode.

1. Aggiungi il codice seguente a `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Questo codice avvia una sessione di garanzia quando l’app è in background e viene aperta utilizzando un collegamento profondo.

Ulteriori informazioni sono disponibili [qui](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

<!-- not initially required

## Signing

Signing the application is only required for the [Create and send push notifications](journey-optimizer-push.md) and the [Create and send in-app messages](journey-optimizer-inapp.md) lessons in this tutorial. These lessons require an Apple provisioning profile which **requires a paid Apple developer account**.

To update the signing for the lessons that require that you sign the application:

1. Open the project in Xcode.
1. Select **[!DNL Luma]** in the Project navigator.
1. Select the **[!DNL Luma]** target.
1. Select the **Signing & Capabilities** tab.
1. Configure **[!UICONTROL Automatic manage signing]**, **[!UICONTROL Team]**, and **[!UICONTROL Bundle Identifier]**, or use your specific Apple development provisioning details. 
 
   >[!IMPORTANT]
   >
   >Ensure you use a _unique_ bundle identifier and replace the `com.adobe.luma.tutorial.swiftui` bundle identifier, as each bundle identifier needs to be unique. Typically, you use a reverse-DNS format for bundle ID strings, like `com.organization.brand.uniqueidentifier`. The Finished version of this tutorial, for example, uses `com.adobe.luma.tutorial.swiftui`.


    ![Xcode signing capabilities](assets/xcode-signing-capabilities.png){zoomable="yes"}

-->

## Configurare un URL di base

1. Vai al progetto in Xcode.
1. Seleziona **[!DNL Luma]** nel Navigatore progetti.
1. Seleziona la **[!DNL Luma]** target.
1. Seleziona la **Info** scheda.
1. Per aggiungere un URL di base, scorri verso il basso fino a **Tipi di URL** e seleziona la **+** pulsante.
1. Imposta **Identificatore** all&#39;identificatore del bundle desiderato e imposta un **Schemi URL** di tua scelta.

   ![url di garanzia](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >Assicurati di utilizzare un’ _univoco_ identificatore del bundle e sostituisci il `com.adobe.luma.tutorial.swiftui` identificatore del bundle, in quanto ogni identificatore del bundle deve essere univoco. In genere si utilizza il formato DNS inverso per le stringhe ID bundle, come `com.organization.brand.uniqueidentifier`.<br/>Allo stesso modo, utilizza uno schema URL univoco e sostituisci quello già fornito `lumatutorialswiftui` con il tuo schema URL univoco.

Per ulteriori informazioni sugli schemi URL in iOS, consulta [Documentazione di Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

Assurance funziona aprendo un URL, tramite il browser o il codice QR. Tale URL inizia con l’URL di base che apre l’app e contiene parametri aggiuntivi. Questi parametri univoci vengono utilizzati per connettere la sessione.


## Connessione a una sessione

In Xcode:

1. Genera o rigenera ed esegui l’app nel simulatore o su un dispositivo fisico da Xcode, utilizzando ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

   >[!TIP]
   >
   >Facoltativamente, potresti voler &quot;ripulire&quot; la build, soprattutto quando vengono visualizzati risultati imprevisti. A questo scopo, seleziona **[!UICONTROL Pulisci cartella di compilazione...]** da Xcode **[!UICONTROL Prodotto]** menu.


1. In **[!UICONTROL Consenti a &quot;App Luma&quot; di utilizzare la tua posizione]** finestra di dialogo, seleziona **[!UICONTROL Consenti durante l&#39;utilizzo dell&#39;app]**.

   <img src="assets/geolocation-permissions.png" width="300">

1. In **[!UICONTROL &quot;App Luma&quot; desidera inviarti notifiche]** finestra di dialogo, seleziona **[!UICONTROL Consenti]**.

   <img src="assets/notification-permissions.png" width="300">

1. Seleziona **[!UICONTROL Continua...]** per consentire all&#39;app di tenere traccia dell&#39;attività.

   <img src="assets/tracking-continue.png" width="300">

1. In **[!UICONTROL Consenti a &quot;App Luma&quot; di tracciare la tua attività tra app e siti web di altre aziende]** finestra di dialogo, seleziona **[!UICONTROL Consenti]**.

   <img src="assets/tracking-allow.png" width="300">


Nel browser:

1. Passa all’interfaccia utente di Data Collection.
1. Seleziona **[!UICONTROL Assurance]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Crea sessione]**.
1. Seleziona **[!UICONTROL Inizio]**.
1. Fornisci un **[!UICONTROL Nome sessione]** come `Luma Mobile App Session` e **[!UICONTROL URL di base]**, che è lo schema URL immesso in Xcode, seguito da `://` Ad esempio: `lumatutorialswiftui://`
1. Seleziona **[!UICONTROL Avanti]**.
   ![sessione di creazione della garanzia di affidabilità](assets/assurance-create-session.png)
1. In **[!UICONTROL Crea nuova sessione]** finestra di dialogo modale:

   Se si utilizza un dispositivo fisico:

   * Seleziona **[!UICONTROL Scansiona codice QR]**. Per aprire l&#39;app, usa la fotocamera sul tuo dispositivo fisico per scansionare il codice QR e toccare il collegamento.

     ![codice di controllo qualità assicurazione](assets/assurance-qr-code.png)

   Se utilizzi un simulatore:

   1. Seleziona **[!UICONTROL Copia collegamento]**.
   1. Copia il collegamento profondo tramite ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  e utilizza il collegamento profondo per aprire l’app con Safari nel simulatore.
      ![Collegamento per la copia di Assurance](assets/assurance-copy-link.png)

1. Al caricamento dell’app, viene visualizzata una finestra di dialogo modale in cui viene richiesto di immettere il PIN illustrato al punto 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Inserisci il PIN e seleziona **[!UICONTROL Connetti]**.


1. Se la connessione ha avuto esito positivo, vengono visualizzati i seguenti elementi:
   * Un’icona Assurance mobile sopra l’app.

     <img src="assets/assurance-modal.png" width="300">

   * Experienci Cloud di aggiornamenti disponibili nell’interfaccia utente Assurance, che mostrano:

      1. Eventi esperienza provenienti dall’app.
      1. Dettagli di un evento selezionato.
      1. Il dispositivo e la timeline.

         ![eventi di garanzia](assets/assurance-events.png)

In caso di problemi, consulta [tecnico](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.


## Verificare le estensioni

Per verificare se l’app utilizza le estensioni più aggiornate:

1. Seleziona **[!UICONTROL Configura]**.

1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) per ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versioni dell&#39;estensione]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Configurare le versioni delle estensioni](assets/assurance-configure-extension-versions.png)

1. Seleziona ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Versioni dell&#39;estensione]** per visualizzare una panoramica delle ultime estensioni disponibili e delle estensioni utilizzate nella tua versione dell’app.

   ![Versioni delle estensioni](assets/assurance-extension-versions.png)

1. Per aggiornare le versioni dell’estensione (ad esempio, **[!UICONTROL Messaggistica]** e **[!UICONTROL Ottimizza]**) seleziona il pacchetto (estensione) da **[!UICONTROL Dipendenze pacchetto]** (ad esempio, **[!UICONTROL AEPMessaging]**) e dal menu di scelta rapida selezionare **[!UICONTROL Aggiorna pacchetto]**. Xcode aggiornerà le dipendenze del pacchetto.


>[!NOTE]
>
>Dopo aver aggiornato le estensioni (pacchetti) in Xcode, chiudi ed elimina la sessione corrente e ripeti tutti i passaggi da [Connessione a una sessione](#connecting-to-a-session) e [Verificare le estensioni](#verify-extensions) affinché Assurance segnali correttamente le estensioni corrette in una nuova sessione Assurance.





>[!SUCCESS]
>
>Ora hai configurato l’app per utilizzare Assurance per il resto dell’esercitazione.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Successivo: **[Implementare il consenso](consent.md)**

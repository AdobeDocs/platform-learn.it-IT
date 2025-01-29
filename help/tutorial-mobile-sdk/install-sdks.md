---
title: Installare gli SDK di Adobe Experience Platform Mobile
description: Scopri come implementare Adobe Experience Platform Mobile SDK in un’app mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 3dd9c68203d0021e87caaa82bd962b3f9160a397
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Installare gli SDK di Adobe Experience Platform Mobile {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Installare gli SDK di Adobe Experience Platform Mobile"
>abstract="Scopri come implementare Adobe Experience Platform Mobile SDK in un’app mobile."

Scopri come implementare Adobe Experience Platform Mobile SDK in un’app mobile.

## Prerequisiti

* Creazione di una libreria di tag con le estensioni descritte nella [lezione precedente](configure-tags.md) completata.
* ID del file dell&#39;ambiente di sviluppo dalle [istruzioni di installazione per dispositivi mobili](configure-tags.md#generate-sdk-install-instructions).
* Scarica l&#39;[app di esempio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} vuota.
* Esperienza con [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Aggiungi gli SDK richiesti al progetto utilizzando Gestione pacchetti Swift.
* Registra le estensioni.

>[!NOTE]
>
>In un’implementazione per app mobile, i termini &quot;estensioni&quot; e &quot;SDK&quot; sono quasi intercambiabili.

## Gestione pacchetti Swift

Invece di utilizzare i CocoaPods e un file Pod (come descritto in [Generare istruzioni di installazione di SDK](./configure-tags.md#generate-sdk-install-instructions)), puoi aggiungere singoli pacchetti utilizzando il gestore di pacchetti Swift nativo di Xcode. Nel progetto Xcode sono già state aggiunte tutte le dipendenze dei pacchetti. La schermata **[!UICONTROL Dipendenze pacchetto]** di Xcode deve essere simile alla seguente:

![Dipendenze pacchetto Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


In Xcode puoi utilizzare **[!UICONTROL File]** > **[!UICONTROL Aggiungi pacchetti...]** per aggiungere pacchetti. La tabella seguente fornisce i collegamenti agli URL da utilizzare per aggiungere pacchetti. I collegamenti ti indirizzano anche a ulteriori informazioni su ciascun pacchetto specifico.

| Pacchetto | Descrizione |
|---|---|
| [Core AEP](https://github.com/adobe/aepsdk-core-ios) | Le estensioni `AEPCore`, `AEPServices` e `AEPIdentity` rappresentano le basi di Adobe Experience Platform SDK. Ogni app che utilizza SDK deve includerle. Questi moduli contengono un set comune di funzionalità e servizi richiesti da tutte le estensioni SDK.<br/><ul><li>`AEPCore` contiene l&#39;implementazione dell&#39;hub eventi. L’hub eventi è il meccanismo utilizzato per la consegna degli eventi tra l’app e SDK. L’hub eventi viene utilizzato anche per condividere i dati tra le estensioni.</li><li>`AEPServices` fornisce diverse implementazioni riutilizzabili necessarie per il supporto della piattaforma, tra cui rete, accesso al disco e gestione del database.</li><li>`AEPIdentity` implementa l&#39;integrazione con i servizi Adobe Experience Platform Identity.</li><li>`AEPSignal` rappresenta l&#39;estensione Segnale degli SDK di Adobe Experience Platform che consente agli addetti al marketing di inviare un &quot;segnale&quot; alle proprie app per inviare dati a destinazioni esterne o per aprire URL.</li><li>`AEPLifecycle` rappresenta l&#39;estensione del ciclo di vita degli SDK di Adobe Experience Platform che consente di raccogliere le metriche del ciclo di vita dell&#39;applicazione, ad esempio le informazioni relative all&#39;installazione o all&#39;aggiornamento dell&#39;applicazione, all&#39;avvio e alla sessione dell&#39;applicazione, alle informazioni sul dispositivo e a qualsiasi dato di contesto aggiuntivo fornito dallo sviluppatore dell&#39;applicazione.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Edge Network (`AEPEdge`) consente di inviare dati alla rete Adobe Edge da un&#39;app mobile. Questa estensione consente di implementare le funzionalità di Adobe Experience Cloud in modo più affidabile, distribuire più soluzioni Adobe tramite una chiamata di rete e inoltrare simultaneamente queste informazioni a Adobe Experience Platform.<br/>L&#39;estensione Edge Network per dispositivi mobili è un&#39;estensione per Adobe Experience Platform SDK e richiede le estensioni `AEPCore` e `AEPServices` per la gestione degli eventi, nonché l&#39;estensione `AEPEdgeIdentity` per il recupero delle identità, ad esempio ECID. |
| [Identità Edge AEP](https://github.com/adobe/aepsdk-edgeidentity-ios) | L&#39;estensione AEP Edge Identity per dispositivi mobili (`AEPEdgeIdentity`) consente la gestione dei dati di identità utente da un&#39;app mobile quando si utilizza Adobe Experience Platform SDK e l&#39;estensione Edge Network. |
| [Consenso AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | L&#39;estensione per dispositivi mobili AEP Consent Collection (`AEPConsent`) abilita la raccolta delle preferenze di consenso dall&#39;app mobile quando si utilizza Adobe Experience Platform SDK e l&#39;estensione Edge Network. |
| [Profilo utente AEP](https://github.com/adobe/aepsdk-userprofile-ios) | L&#39;estensione Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) è un&#39;estensione per la gestione dei profili utente per Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | L&#39;estensione AEP Places (`AEPPlaces`) consente di tenere traccia degli eventi di geolocalizzazione definiti nell&#39;interfaccia di Adobe Places e nelle regole dei tag di raccolta dati di Adobe. |
| [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios) | L&#39;estensione AEP Messaging (`AEPMessaging`) consente di inviare token di notifica push e feedback click-through di notifica push a Adobe Experience Platform. |
| [Ottimizzazione AEP](https://github.com/adobe/aepsdk-optimize-ios) | L&#39;estensione AEP Optimize (`AEPOptimize`) fornisce API per abilitare i flussi di lavoro di personalizzazione in tempo reale negli SDK di Adobe Experience Platform Mobile tramite Adobe Target o Adobe Journey Optimizer Offer Decisioning. Sono necessarie le estensioni `AEPCore` e `AEPEdge` per inviare eventi di query di personalizzazione alla rete Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (alias progetto Griffon) è una nuova estensione innovativa (`AEPAssurance`) che consente di verificare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze nell&#39;app mobile. Questa estensione abilita l&#39;app per Assurance. |


## Importare estensioni

In Xcode, passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** e assicurati che le seguenti importazioni facciano parte di questo file di origine.

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

Effettua le stesse operazioni per **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Aggiorna AppDelegate

Passa a **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** nel Navigatore progetti Xcode.

1. Sostituire il valore `YOUR_ENVIRONMENT_ID_GOES_HERE` di `@AppStorage` per `environmentFileId` con il valore ID file dell&#39;ambiente di sviluppo recuperato dai tag nelle [istruzioni per l&#39;installazione di SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Aggiungere il codice seguente alla funzione `application(_, didFinishLaunchingWithOptions)`.

   ```swift
   // Define extensions
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
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

Il codice di cui sopra esegue le seguenti operazioni:

1. Registra le estensioni richieste.
1. Configura MobileCore e altre estensioni per utilizzare la configurazione della proprietà tag.
1. Abilita la registrazione di debug. Ulteriori dettagli e opzioni sono disponibili nella [documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Avvia il monitoraggio del ciclo di vita. Per ulteriori dettagli, vedi il passaggio [Ciclo di vita](lifecycle-data.md) nell&#39;esercitazione.
1. Imposta il consenso predefinito su sconosciuto. Consulta il passaggio [Consenso](consent.md) nell&#39;esercitazione per ulteriori dettagli.

>[!IMPORTANT]
>
>Assicurati di aggiornare `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` in base a `environmentFileId` dall&#39;ambiente di tag che stai creando per (sviluppo, staging o produzione).
>

>[!SUCCESS]
>
>Ora hai installato i pacchetti necessari e aggiornato il progetto per registrare correttamente le estensioni Adobe Experience Platform Mobile SDK richieste che stai per utilizzare per il resto dell’esercitazione.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Configura Assurance](assurance.md)**

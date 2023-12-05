---
title: Installare gli SDK di Adobe Experience Platform Mobile
description: Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Installare gli SDK di Adobe Experience Platform Mobile

Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.

## Prerequisiti

* È stata creata una libreria di tag con le estensioni descritte in [lezione precedente](configure-tags.md).
* ID file dell’ambiente di sviluppo da [Istruzioni di installazione per dispositivi mobili](configure-tags.md#generate-sdk-install-instructions).
* Scaricato il vuoto [app di esempio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Esperienza con [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Aggiungi gli SDK richiesti al progetto utilizzando Gestione pacchetti Swift.
* Registra le estensioni.

>[!NOTE]
>
>In un’implementazione per app mobile, i termini &quot;estensioni&quot; e &quot;SDK&quot; sono quasi intercambiabili.

## Gestione pacchetti Swift

Invece di utilizzare CocoaPods e un file Pod (come descritto in [Generare istruzioni di installazione SDK](./configure-tags.md#generate-sdk-install-instructions)), puoi aggiungere singoli pacchetti utilizzando il gestore di pacchetti Swift nativo di Xcode. Nel progetto Xcode sono già state aggiunte tutte le dipendenze dei pacchetti. Xcode **[!UICONTROL Dipendenze pacchetto]** la schermata dovrebbe avere un aspetto simile a:

![Dipendenze pacchetto Xcode](assets/xcode-package-dependencies.png){zoomable=&quot;yes&quot;}


In Xcode puoi utilizzare **[!UICONTROL File]** > **[!UICONTROL Aggiungi pacchetti...]** per aggiungere pacchetti. La tabella seguente fornisce i collegamenti agli URL da utilizzare per aggiungere pacchetti. I collegamenti ti indirizzano anche a ulteriori informazioni su ciascun pacchetto specifico.

| Pacchetto | Descrizione |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Il `AEPCore`, `AEPServices`, e `AEPIdentity` Le estensioni rappresentano le basi dell&#39;SDK di Adobe Experience Platform: ogni app che utilizza l&#39;SDK deve includerle. Questi moduli contengono un set comune di funzionalità e servizi richiesti da tutte le estensioni SDK.<br/><ul><li>`AEPCore` contiene l’implementazione dell’hub eventi. L’hub eventi è il meccanismo utilizzato per la trasmissione degli eventi tra l’app e l’SDK. L’hub eventi viene utilizzato anche per condividere i dati tra le estensioni.</li><li>`AEPServices` fornisce diverse implementazioni riutilizzabili necessarie per il supporto della piattaforma, tra cui rete, accesso al disco e gestione del database.</li><li>`AEPIdentity` implementa l’integrazione con i servizi Adobe Experience Platform Identity.</li><li>`AEPSignal` rappresenta l’estensione Segnale degli SDK di Adobe Experience Platform che consente agli esperti di marketing di inviare un &quot;segnale&quot; alle loro app per inviare dati a destinazioni esterne o per aprire URL.</li><li>`AEPLifecycle` rappresenta l’estensione del ciclo di vita degli SDK di Adobe Experience Platform che consente di raccogliere metriche del ciclo di vita dell’applicazione quali informazioni sull’installazione o l’aggiornamento dell’applicazione, informazioni sull’avvio e sulla sessione dell’applicazione, informazioni sul dispositivo ed eventuali dati contestuali aggiuntivi forniti dallo sviluppatore dell’applicazione.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Edge Network (`AEPEdge`) consente di inviare dati ad Adobe Edge Network da un’app mobile. Questa estensione consente di implementare le funzionalità di Adobe Experience Cloud in modo più affidabile, distribuire più soluzioni di Adobe tramite una chiamata di rete e inoltrare simultaneamente queste informazioni a Adobe Experience Platform.<br/>L&#39;estensione per dispositivi mobili Edge Network è un&#39;estensione per Adobe Experience Platform SDK e richiede `AEPCore` e `AEPServices` estensioni per la gestione degli eventi, nonché `AEPEdgeIdentity` estensione per il recupero delle identità, ad esempio ECID. |
| [Identità AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | Estensione AEP Edge Identity per dispositivi mobili (`AEPEdgeIdentity`) consente di gestire i dati di identità utente da un’app mobile quando si utilizzano l’SDK di Adobe Experience Platform e l’estensione Edge Network. |
| [Consenso AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | Estensione AEP Consent Collection per dispositivi mobili (`AEPConsent`) abilita la raccolta delle preferenze di consenso dall’app mobile quando si utilizza l’SDK di Adobe Experience Platform e l’estensione Edge Network. |
| [Profilo utente AEP](https://github.com/adobe/aepsdk-userprofile-ios) | Estensione Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) è un&#39;estensione per gestire i profili utente per l&#39;SDK di Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | Estensione AEP Places (`AEPPlaces`) consente di tenere traccia degli eventi di geolocalizzazione come definito nell’interfaccia Adobe Places e nelle regole tag di raccolta dati di Adobe. |
| [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios) | Estensione AEP Messaging (`AEPMessaging`) consente di inviare al Adobe Experience Platform i token di notifica push e il feedback click-through per la notifica push. |
| [Ottimizzazione AEP](https://github.com/adobe/aepsdk-optimize-ios) | Estensione AEP Optimize (`AEPOptimize`) fornisce API per abilitare i flussi di lavoro di personalizzazione in tempo reale negli SDK di Adobe Experience Platform Mobile tramite Adobe Target o Adobe Journey Optimizer Offer Decisioning. Richiede `AEPCore` e `AEPEdge` estensioni per inviare eventi di query di personalizzazione alla rete Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (alias progetto Griffon) è una nuova estensione innovativa (`AEPAssurance`) per aiutarti a ispezionare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile. Questa estensione abilita l’app per Assurance. |


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

Effettua la stessa operazione per **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Aggiorna AppDelegate

Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** nel Navigatore progetti Xcode.

1. Sostituisci il `@AppStorage` valore `YOUR_ENVIRONMENT_ID_GOES_HERE` per `environmentFileId` al valore ID file dell’ambiente di sviluppo recuperato dai tag in [Generare istruzioni di installazione SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Aggiungi il seguente codice al `application(_, didFinishLaunchingWithOptions)` funzione.

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
1. Abilita la registrazione di debug. Ulteriori dettagli e opzioni sono disponibili nella sezione [Documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Avvia il monitoraggio del ciclo di vita. Consulta [Ciclo di vita](lifecycle-data.md) per ulteriori dettagli, consulta l’esercitazione.
1. Imposta il consenso predefinito su sconosciuto. Consulta [Consenso](consent.md) per ulteriori dettagli, consulta l’esercitazione.

>[!IMPORTANT]
>
>Assicurati di aggiornare `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` in base al `environmentFileId` dall’ambiente di tag per cui stai creando (sviluppo, staging o produzione).
>

>[!SUCCESS]
>
>Ora hai installato i pacchetti necessari e aggiornato il progetto per registrare correttamente le estensioni SDK di Adobe Experience Platform Mobile richieste che stai per utilizzare per il resto dell’esercitazione.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Configura Assurance](assurance.md)**

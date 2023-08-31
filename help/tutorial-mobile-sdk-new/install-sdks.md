---
title: Installare gli SDK di Adobe Experience Platform Mobile
description: Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.
hide: true
source-git-commit: 6cc58d3d40112b14b1c1b8664c5e7aeb0880b59c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---

# Installare gli SDK di Adobe Experience Platform Mobile

Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.

## Prerequisiti

* La libreria di tag è stata creata con le estensioni descritte in [lezione precedente](configure-tags.md).
* ID file dell’ambiente di sviluppo da [Istruzioni di installazione per dispositivi mobili](configure-tags.md#generate-sdk-install-instructions).
* Scaricato, vuoto [app di esempio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Esperienza con [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Aggiungi gli SDK richiesti al progetto utilizzando Gestione pacchetti Swift.
* Registra le estensioni.

>[!NOTE]
>
>In un’implementazione per app mobile, i termini &quot;estensioni&quot; e &quot;SDK&quot; sono quasi intercambiabili.

## Gestione pacchetti Swift

Invece di utilizzare CocoaPods e utilizzare un file Pod (come descritto nelle istruzioni di installazione per dispositivi mobili, consulta [Generare istruzioni di installazione SDK](./configure-tags.md#generate-sdk-install-instructions)), puoi aggiungere singoli pacchetti utilizzando il gestore di pacchetti Swift nativo di Xcode.

In Xcode, utilizza **[!UICONTROL File]** > **[!UICONTROL Aggiungi pacchetti...]** e installare tutti i pacchetti elencati nella tabella seguente. Seleziona il collegamento del pacchetto nella tabella per ottenere l’URL completo del pacchetto specifico.

| Pacchetto | Descrizione |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | Il `AEPCore`, `AEPServices`, e `AEPIdentity` Le estensioni rappresentano le basi dell&#39;SDK di Adobe Experience Platform: ogni app che utilizza l&#39;SDK deve includerle. Questi moduli contengono un set comune di funzionalità e servizi richiesti da tutte le estensioni SDK.<br/>`AEPCore` contiene l’implementazione dell’hub eventi. L’hub eventi è il meccanismo utilizzato per la trasmissione degli eventi tra l’app e l’SDK. L’hub eventi viene utilizzato anche per condividere i dati tra le estensioni.<br/>`AEPServices` fornisce diverse implementazioni riutilizzabili necessarie per il supporto della piattaforma, tra cui rete, accesso al disco e gestione del database.<br/>`AEPIdentity` implementa l’integrazione con i servizi Adobe Experience Platform Identity.<br/>`AEPSignal` rappresenta l’estensione Signal dell’SDK Adobe Experience Platform che consente agli addetti al marketing di inviare un &quot;segnale&quot; alle proprie app per inviare dati a destinazioni esterne o per aprire URL.<br/>`AEPLifecycle` rappresenta l&#39;estensione del ciclo di vita di Adobe Experience Platform SDK che consente di raccogliere le metriche del ciclo di vita dell&#39;applicazione, ad esempio le informazioni relative all&#39;installazione o all&#39;aggiornamento dell&#39;applicazione, all&#39;avvio e alla sessione dell&#39;applicazione, al dispositivo e a qualsiasi dato contestuale aggiuntivo fornito dallo sviluppatore dell&#39;applicazione. |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | L’estensione per dispositivi mobili Adobe Experience Platform Edge Network consente di inviare dati ad Adobe Edge Network da un’app mobile. Questa estensione consente di implementare le funzionalità di Adobe Experience Cloud in modo più affidabile, distribuire più soluzioni di Adobe tramite una chiamata di rete e inoltrare simultaneamente queste informazioni a Adobe Experience Platform.<br/>L&#39;estensione per dispositivi mobili Edge Network è un&#39;estensione per Adobe Experience Platform SDK e richiede `AEPCore` e `AEPServices` estensioni per la gestione degli eventi, nonché `AEPEdgeIdentity` estensione per il recupero delle identità, ad esempio ECID. |
| [Identità AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | L’estensione per dispositivi mobili AEP Edge Identity consente di gestire i dati di identità dell’utente da un’app mobile quando si utilizzano l’SDK di Adobe Experience Platform e l’estensione della rete Edge. |
| [Consenso AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | L’estensione per dispositivi mobili AEP Consent Collection abilita la raccolta delle preferenze di consenso dall’app mobile quando si utilizzano l’SDK di Adobe Experience Platform e l’estensione Edge Network. |
| [Profilo utente AEP](https://github.com/adobe/aepsdk-userprofile-ios.git) | L’estensione Adobe Experience Platform User Profile Mobile è un’estensione per la gestione dei profili utente per l’SDK di Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | L’estensione Adobe Experience Platform Places è un’estensione per l’SDK di Adobe Experience Platform Swift. L’estensione AEPPlaces consente di tenere traccia degli eventi di geolocalizzazione come definito nell’interfaccia utente di Adobe Places e nelle regole di Adobe Launch. |
| [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios.git) | L&#39;estensione AEP Messaging è un&#39;estensione per l&#39;SDK di Adobe Experience Platform Swift. L&#39;estensione AEP Messaging consente di inviare token di notifica push e feedback click-through di notifica push al Adobe Experience Platform. |
| [Ottimizzazione AEP](https://github.com/adobe/aepsdk-optimize-ios) | L&#39;estensione AEP Optimize fornisce API per abilitare i flussi di lavoro di personalizzazione in tempo reale negli SDK Adobe Experience Platform Mobile tramite Adobe Target o Adobe Journey Optimizer Offer Decisioning. Richiede `AEPCore` e `AEPEdge` estensioni per inviare eventi di query di personalizzazione alla rete Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance (alias progetto Griffon) è un nuovo prodotto innovativo per aiutarti a ispezionare, verificare, simulare e convalidare il modo in cui raccogli dati o distribuisci esperienze nella tua app mobile. |


Dopo aver installato tutti i pacchetti, il tuo Xcode **[!UICONTROL Dipendenze pacchetto]** la schermata dovrebbe avere un aspetto simile a:

![Dipendenze pacchetto Xcode](assets/xcode-package-dependencies.png)


## Importare estensioni

In Xcode, passa a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** e aggiungi le seguenti importazioni.

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

Effettua la stessa operazione per **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]**.

## Aggiorna AppDelegate

Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **AppDelegate** nel Navigatore progetti Xcode.

1. Imposta il `@AppStorage` valore per `environmentFileId` al valore ID file dell’ambiente di sviluppo recuperato dai tag nel passaggio 6 in [Generare istruzioni di installazione SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. Aggiungi il seguente codice al `application(_, didFinishLaunchingWithOptions)` funzione.

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
   
       // update version and build
       Logger.configuration.info("Luma - Updating version and build number...")
       SettingsBundleHelper.setVersionAndBuildNumber()
   })
   ```

Il codice di cui sopra esegue le seguenti operazioni:

1. Registra le estensioni richieste.
1. Configura MobileCore e altre estensioni per utilizzare la configurazione della proprietà tag.
1. Abilita la registrazione di debug. Ulteriori dettagli e opzioni sono disponibili nella sezione [Documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>
>Assicurati di aggiornare `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` in base al `environmentFileId` dall’ambiente di tag per cui stai creando (sviluppo, staging o produzione).
>

>[!SUCCESS]
>
>Ora hai installato i pacchetti necessari e aggiornato il progetto per registrare correttamente le estensioni SDK di Adobe Experience Platform Mobile richieste che stai per utilizzare per il resto dell’esercitazione.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Configura Assurance](assurance.md)**

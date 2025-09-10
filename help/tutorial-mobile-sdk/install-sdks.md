---
title: Installare Adobe Experience Platform Mobile SDK
description: Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 3%

---

# Installare Adobe Experience Platform Mobile SDK {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Installare Adobe Experience Platform Mobile SDK"
>abstract="Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile."

Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.

## Prerequisiti

* Creazione di una libreria di tag con le estensioni descritte nella [lezione precedente](configure-tags.md) completata.
* ID del file dell&#39;ambiente di sviluppo dalle [istruzioni di installazione per dispositivi mobili](configure-tags.md#generate-sdk-install-instructions).
* È stata scaricata l&#39;[app di esempio per iOS](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) o [app di esempio per Android](https://github.com/adobe/Luma-Android).
* Esperienza con [Xcode](https://developer.apple.com/xcode/) (iOS) o [Android Studio](https://developer.android.com/studio/intro?utm_source=android-studio) (Android)

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Aggiungi gli SDK richiesti al progetto.
* Registra le estensioni.

>[!NOTE]
>
>In un&#39;implementazione di app mobile, i termini *estensioni* e *SDK* sono quasi intercambiabili.

>[!BEGINTABS]

>[!TAB iOS]

## Gestione pacchetti Swift

Invece di utilizzare i CocoaPods e un file Pod (come descritto in [Generare istruzioni di installazione di SDK](./configure-tags.md#generate-sdk-install-instructions)), puoi aggiungere singoli pacchetti utilizzando il gestore di pacchetti Swift nativo di Xcode. Nel progetto Xcode sono già state aggiunte tutte le dipendenze dei pacchetti. La schermata **[!UICONTROL Dipendenze pacchetto]** di Xcode deve essere simile alla seguente:

![Dipendenze pacchetto Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


In Xcode puoi utilizzare **[!UICONTROL File]** > **[!UICONTROL Aggiungi pacchetti...]** per aggiungere pacchetti. La tabella seguente fornisce i collegamenti agli URL da utilizzare per aggiungere pacchetti. I collegamenti ti indirizzano anche a ulteriori informazioni su ciascun pacchetto specifico.

| Pacchetto | Descrizione |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Le estensioni `AEPCore`, `AEPServices` e `AEPIdentity` rappresentano le basi di Adobe Experience Platform SDK. Ogni app che utilizza SDK deve includerle. Questi moduli contengono un set comune di funzionalità e servizi che tutte le estensioni SDK richiedono.<br/><ul><li>`AEPCore` contiene l&#39;implementazione dell&#39;hub eventi. L’hub eventi è il meccanismo utilizzato per la consegna degli eventi tra l’app e SDK. L’hub eventi viene utilizzato anche per condividere i dati tra le estensioni.</li><li>`AEPServices` fornisce diverse implementazioni riutilizzabili necessarie per il supporto della piattaforma, tra cui rete, accesso al disco e gestione del database.</li><li>`AEPIdentity` implementa l&#39;integrazione con i servizi Adobe Experience Platform Identity.</li><li>`AEPSignal` rappresenta l&#39;estensione Segnale degli SDK di Adobe Experience Platform che consente agli addetti al marketing di inviare un &quot;segnale&quot; alle proprie app per inviare dati a destinazioni esterne o per aprire URL.</li><li>`AEPLifecycle` rappresenta l&#39;estensione del ciclo di vita degli SDK di Adobe Experience Platform che consente di raccogliere le metriche del ciclo di vita dell&#39;applicazione, ad esempio le informazioni relative all&#39;installazione o all&#39;aggiornamento dell&#39;applicazione, all&#39;avvio e alla sessione dell&#39;applicazione, alle informazioni sul dispositivo e a qualsiasi dato di contesto aggiuntivo fornito dallo sviluppatore dell&#39;applicazione.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Edge Network (`AEPEdge`) consente di inviare dati ad Adobe Edge Network da un&#39;app mobile. Questa estensione consente di implementare le funzionalità di Adobe Experience Cloud in modo più affidabile, distribuire più soluzioni Adobe tramite una chiamata di rete e inoltrare simultaneamente queste informazioni a Adobe Experience Platform.<br/>L&#39;estensione Edge Network per dispositivi mobili è un&#39;estensione per Adobe Experience Platform SDK. L&#39;estensione richiede le estensioni `AEPCore` e `AEPServices` per la gestione degli eventi, nonché l&#39;estensione `AEPEdgeIdentity` per il recupero delle identità, ad esempio ECID. |
| [Identità AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Edge Identity (`AEPEdgeIdentity`) consente la gestione dei dati di identità utente da un&#39;app mobile quando si utilizza Adobe Experience Platform SDK e l&#39;estensione Edge Network. |
| [Consenso AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Consent Collection (`AEPConsent`) abilita la raccolta delle preferenze di consenso dall&#39;app mobile quando si utilizza Adobe Experience Platform SDK e l&#39;estensione Edge Network. |
| [Profilo utente AEP](https://github.com/adobe/aepsdk-userprofile-ios) | L&#39;estensione Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) è un&#39;estensione per la gestione dei profili utente per Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | L&#39;estensione Adobe Experience Platform Places (`AEPPlaces`) consente di tenere traccia degli eventi di geolocalizzazione definiti nell&#39;interfaccia di Adobe Places e nelle regole dei tag di raccolta dati di Adobe. |
| [Messaggistica AEP](https://github.com/adobe/aepsdk-messaging-ios) | L&#39;estensione Messaggistica Adobe Experience Platform (`AEPMessaging`) consente di inviare token di notifica push e feedback click-through di notifica push a Adobe Experience Platform. |
| [Ottimizzazione AEP](https://github.com/adobe/aepsdk-optimize-ios) | L&#39;estensione Adobe Experience Platform Optimize (`AEPOptimize`) fornisce API per abilitare i flussi di lavoro di personalizzazione in tempo reale negli SDK Adobe Experience Platform Mobile tramite Adobe Target o Adobe Journey Optimizer Offer Decisioning. Richiede le estensioni `AEPCore` e `AEPEdge` per inviare eventi di query di personalizzazione a Experience Edge Network. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Adobe Experience Platform Assurance è un prodotto di Adobe Experience Cloud che consente di ispezionare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile. |


## Importare estensioni

Apri in Xcode il progetto nella cartella **[!UICONTROL Start]** dell&#39;app di esempio.

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

1. Sostituire il valore `@AppStorage` di `YOUR_ENVIRONMENT_ID_GOES_HERE` per `environmentFileId` con il valore ID file di ambiente recuperato dai tag nelle [istruzioni per l&#39;installazione di SDK](configure-tags.md#generate-sdk-install-instructions).

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

Assicurati di aggiornare `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` in base a `environmentFileId` dall&#39;ambiente di tag che stai creando per (sviluppo, staging o produzione).

>[!TAB Android]

## Gradle

Le dipendenze vengono utilizzate dalle [istruzioni di installazione di Generate SDK](./configure-tags.md#generate-sdk-install-instructions) per aggiungere singoli pacchetti mediante l&#39;integrazione di Gradle con Android Studio. Il progetto Android Studio presenta già tutte le dipendenze dei pacchetti aggiunte automaticamente.

1. Selezionare ![FolderOutline](/help/assets/icons/FolderOutline.svg) come strumento.
1. Seleziona la visualizzazione **[!UICONTROL Android]**.
1. Seleziona **[!UICONTROL Script Gradle]** > **[!UICONTROL build.gradle.kts (Modulo :app)]** dal riquadro a sinistra. Quindi, nel riquadro di destra, scorrere fino a visualizzare `dependencies`.

   ![Dipendenze livello Android](assets/androidstudio-package-dependencies.png){zoomable="yes"}

In Android Studio è possibile utilizzare **[!UICONTROL File]** > **[!UICONTROL Struttura di progetto...]** per aggiungere dipendenze del modulo. Seleziona **[!UICONTROL Dipendenze]**, quindi utilizza **[!UICONTROL Moduli]** ![Aggiungi](/help/assets/icons/Add.svg) per aggiungere moduli. La tabella seguente fornisce collegamenti agli URL da utilizzare per aggiungere moduli di dipendenza. I collegamenti ti indirizzano anche a ulteriori informazioni su ciascun modulo specifico.

| Pacchetto<br/>com.adobe.<br/>marketing.mobile: | Descrizione |
|---|---|
| [core](https://github.com/adobe/aepsdk-core-android) | Le estensioni `MobileCore` e `Identity` rappresentano le basi di Adobe Experience Platform SDK. Ogni app che utilizza SDK deve includerli. Questi moduli contengono un set comune di funzionalità e servizi richiesti da tutte le estensioni SDK.<ul><li>`MobileCore` contiene l&#39;implementazione dell&#39;hub eventi. L’hub eventi è il meccanismo utilizzato per la consegna degli eventi tra l’app e SDK. L’hub eventi viene utilizzato anche per condividere i dati tra estensioni e fornisce diverse implementazioni riutilizzabili necessarie per il supporto della piattaforma, tra cui rete, accesso al disco e gestione del database.</li><li>`Identity` implementa l&#39;integrazione con i servizi Adobe Experience Platform Identity.</li><li>`Signal` rappresenta l&#39;estensione Signal di Adobe Experience Platform SDK che consente agli addetti marketing di inviare un &quot;segnale&quot; alle proprie app per inviare dati a destinazioni esterne o per aprire URL.</li><li>`Lifecycle` rappresenta l&#39;estensione del ciclo di vita di Adobe Experience Platform SDK che consente di raccogliere le metriche del ciclo di vita dell&#39;applicazione, ad esempio le informazioni relative all&#39;installazione o all&#39;aggiornamento dell&#39;applicazione, all&#39;avvio e alla sessione dell&#39;applicazione, alle informazioni sul dispositivo e a qualsiasi dato di contesto aggiuntivo fornito dallo sviluppatore dell&#39;applicazione.</li></ul> |
| [edge](https://github.com/adobe/aepsdk-edge-android) | L&#39;estensione per dispositivi mobili Adobe Experience Platform Edge Network (`AEPEdge`) consente di inviare dati ad Adobe Edge Network da un&#39;app mobile. Questa estensione consente di implementare le funzionalità di Adobe Experience Cloud in modo più affidabile, distribuire più soluzioni Adobe tramite una chiamata di rete e inoltrare simultaneamente queste informazioni a Adobe Experience Platform.<br/>L&#39;estensione Edge Network per dispositivi mobili è un&#39;estensione per Adobe Experience Platform SDK. L&#39;estensione richiede le estensioni `Mobile Core` e `Services` per la gestione degli eventi. E l&#39;estensione `Identity for Edge Network` per recuperare le identità, ad esempio ECID. |
| [edgeidentity](https://github.com/adobe/aepsdk-edgeidentity-android) | L’estensione per dispositivi mobili Adobe Experience Platform Edge Identity consente di gestire i dati di identità dell’utente da un’app mobile quando si utilizzano Adobe Experience Platform SDK e l’estensione Edge Network. |
| [edgeconsent](https://github.com/adobe/aepsdk-edgeconsent-android) | L’estensione per dispositivi mobili Adobe Experience Platform Consent Collection abilita la raccolta delle preferenze di consenso dall’app mobile quando si utilizzano Adobe Experience Platform SDK e l’estensione Edge Network. |
| [profilo utente](https://github.com/adobe/aepsdk-userprofile-android) | L&#39;estensione Adobe Experience Platform User Profile Mobile è un&#39;estensione per la gestione dei profili utente per Adobe Experience Platform SDK. |
| [aepplaces](https://github.com/adobe/aepsdk-places-android) | Adobe Places Service è un servizio di geolocalizzazione che consente alle app mobili di riconoscere la posizione. E capire il contesto della posizione utilizzando interfacce SDK avanzate e facili da usare, associate a un database flessibile di punti di interesse (POI). Per ulteriori informazioni, consulta la documentazione di Places Service.<br/>Questo servizio è l&#39;estensione mobile Luoghi per Android 2.x Adobe Experience Platform SDK e richiede l&#39;estensione Core per la gestione degli eventi. |
| [messaggistica](https://github.com/adobe/aepsdk-messaging-android) | L&#39;estensione Adobe Experience Platform Messaging potenzia le notifiche push, i messaggi in-app e le esperienze basate su codice per le app mobili. Questa estensione consente inoltre di raccogliere i token push degli utenti e di gestire la misurazione delle interazioni con i servizi Adobe Experience Platform. |
| [ottimizza](https://github.com/adobe/aepsdk-optimize-android) | L&#39;estensione Adobe Experience Platform Optimize fornisce API per abilitare i flussi di lavoro di personalizzazione in tempo reale negli SDK di Adobe Experience Platform tramite Adobe Target o Adobe Journey Optimizer Offer Decisioning. Dipende dal core mobile e richiede l’estensione Edge per inviare eventi di query di personalizzazione a Experience Edge Network. |
| [assicurazione](https://github.com/adobe/aepsdk-assurance-android) | Assurance (alias progetto Griffon) è un’estensione per dispositivi mobili per Adobe Experience Platform che consente l’integrazione con Adobe Experience Platform Assurance. L’estensione consente di verificare, verificare, simulare e convalidare la modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile. Questa estensione richiede MobileCore. |

## Importare estensioni

In Android Studio, passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** e assicurati che le seguenti importazioni facciano parte del file di origine.

```kotlin
import com.adobe.marketing.mobile.Assurance
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.Lifecycle
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.Messaging
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.MobilePrivacyStatus
import com.adobe.marketing.mobile.Places
import com.adobe.marketing.mobile.Signal
import com.adobe.marketing.mobile.UserProfile
import com.adobe.marketing.mobile.edge.consent.Consent
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.optimize.Optimize
```

Fai lo stesso per **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL modelli]** > **[!UICONTROL MobileSDK]**.


## Aggiorna applicazione Luma

Nella visualizzazione **[!UICONTROL Android]**, passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** in Android Studio.

1. Sostituisci `"YOUR_ENVIRONMENT_FILE_ID"` in `private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"` con il valore ID file di ambiente recuperato dai tag in [Genera istruzioni di installazione di SDK](configure-tags.md#generate-sdk-install-instructions).

   ```kotlin
   private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Aggiungere il codice seguente alla funzione `override fun onCreate()` in `class LumaApplication : Application()`.

   ```kotlin
   // Define extensions
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   
   // Register extensions
   MobileCore.registerExtensions(extensions) {
   // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
     Log.i("Luma", "Using mobile config: $environmentFileId")
     MobileCore.configureWithAppID(environmentFileId)
   
     // set this to true when testing on your device, default is false.
     //MobileCore.updateConfiguration(mapOf("messaging.useSandbox" to true))
   
     // assume unknown, adapt to your needs.
     MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN)
   }
   ```

   Il codice di cui sopra esegue le seguenti operazioni:

   1. Registra le estensioni richieste.
   1. Configura MobileCore e altre estensioni per utilizzare la configurazione della proprietà tag.
   1. Abilita la registrazione di debug. Ulteriori dettagli e opzioni sono disponibili nella [documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
   1. Avvia il monitoraggio del ciclo di vita. Per ulteriori dettagli, vedi il passaggio [Ciclo di vita](lifecycle-data.md) nell&#39;esercitazione.
   1. Imposta il consenso predefinito su sconosciuto. Consulta il passaggio [Consenso](consent.md) nell&#39;esercitazione per ulteriori dettagli.

Assicurati di aggiornare `MobileCore.configureWith(environmentFileId)` con `environmentFileId` in base all&#39;ID file di ambiente dall&#39;ambiente di tag che stai creando per (sviluppo, staging o produzione).


>[!ENDTABS]

>[!SUCCESS]
>
>Ora hai installato i pacchetti necessari e aggiornato il progetto per registrare le estensioni Adobe Experience Platform Mobile SDK richieste che utilizzerai per il resto dell’esercitazione.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Configura Assurance](assurance.md)**

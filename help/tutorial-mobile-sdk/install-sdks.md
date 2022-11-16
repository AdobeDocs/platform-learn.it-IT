---
title: Installare gli SDK di Adobe Experience Platform Mobile
description: Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Installare gli SDK di Adobe Experience Platform Mobile

Scopri come implementare l’SDK di Adobe Experience Platform Mobile in un’app mobile.

## Prerequisiti

* La libreria dei tag è stata creata con le estensioni descritte in [lezione precedente](configure-tags.md).
* ID file dell&#39;ambiente di sviluppo dal [Istruzioni di installazione per dispositivi mobili](configure-tags.md#generate-sdk-install-instructions).
* Scaricato, vuoto [app di esempio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;}.
* Esperienza con [XCode](https://developer.apple.com/xcode/){target=&quot;_blank&quot;}.
* Base [riga di comando](https://en.wikipedia.org/wiki/Command-line_interface)Conoscenza di {target=&quot;_blank&quot;}.

## Finalità di apprendimento

In questa lezione:

* Aggiorna il tuo file CocoaPod.
* Importa gli SDK richiesti.
* Registra le estensioni.

>[!NOTE]
>
>Nell’implementazione di un’app mobile, i termini &quot;estensioni&quot; e &quot;SDK&quot; sono quasi intercambiabili.


## Aggiorna PodFile

>[!NOTE]
>
> Se non hai familiarità con CocoaPods, consulta il funzionario [guida introduttiva](https://guides.cocoapods.org/using/getting-started.html).

L&#39;installazione è solitamente un semplice comando sudo:

```console
sudo gem install cocoapods
```

Una volta installato CocoaPods, apri il Podfile .

![podfile iniziale](assets/mobile-install-initial-podfile.png)

Aggiorna il file per includere i seguenti pod:

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` è richiesto solo se intendi implementare i messaggi push utilizzando Adobe Journey Optimizer. Leggi l&#39;esercitazione su [implementazione dei messaggi push con Adobe Journey Optimizer](journey-optimizer-push.md) per ulteriori informazioni.

Dopo aver salvato le modifiche al tuo Podfile, passa alla cartella con il tuo progetto ed esegui il `pod install` per installare le modifiche.

![installazione del pod](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Se ottieni il &quot;Nessun Podfile trovato nella directory del progetto&quot;. errore, il terminale si trova nella cartella sbagliata. Passa alla cartella con il Podfile aggiornato e riprova.

Se desideri eseguire l’aggiornamento alla versione più recente, esegui la `pod update` comando.

>[!INFO]
>
>Se non sei in grado di utilizzare CocoaPods nelle tue app, puoi saperne di più [implementazioni supportate](https://github.com/adobe/aepsdk-core-ios#binaries) nel progetto GitHub.

## Costruire CocoaPods

Per costruire CocoaPods, apri `Luma.xcworkspace`, quindi seleziona **Prodotto**, seguita da **Rimuovi cartella build**.

>[!NOTE]
>
> Potrebbe essere necessario impostare **Genera solo architettura attiva** a **No**. A questo scopo, seleziona il progetto Pods dal navigatore del progetto, quindi seleziona **Impostazioni build** e imposta la **Creare un’architettura attiva** a **No**.

Ora puoi creare ed eseguire il progetto.

![impostazioni di compilazione](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Il progetto Luma è stato costruito con Xcode v12.5 su un chipset M1 ed è eseguito sul simulatore iOS. Se utilizzi una configurazione diversa, potrebbe essere necessario modificare le impostazioni di build per riflettere la tua architettura.
>
>Se la build non ha avuto successo, prova a ripristinare la **Creare un’architettura attiva** > **Debug** impostazione su **Sì**.
>
>Configurazione del simulatore &quot;iPod touch (7a generazione)&quot; utilizzata durante l’authoring di questa esercitazione.

## Importare estensioni

In ciascuno dei `.swift` file, aggiungi le seguenti importazioni. Inizia aggiungendo a `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## Aggiorna AppDelegate

In `AppDelegate.swift` aggiungi il seguente codice a `didFinishLaunchingWithOptions`. Sostituisci currentAppId con il valore ID del file dell&#39;ambiente di sviluppo recuperato dai tag in [lezione precedente](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` è richiesto solo se intendi implementare i messaggi push tramite Adobe Journey Optimizer come descritto [qui](journey-optimizer-push.md).

Il codice di cui sopra effettua le seguenti operazioni:

* Registra le estensioni richieste.
* Configura MobileCore e altre estensioni per utilizzare la configurazione della proprietà tag.
* Abilita la registrazione di debug. Maggiori dettagli e opzioni sono disponibili nella sezione [Documentazione di Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging).

>[!IMPORTANT]
>In un’app di produzione, devi passare ad AppId in base all’ambiente corrente (dev/stag/prod).

Avanti: **[Imposta garanzia](assurance.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
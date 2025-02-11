---
title: Sostituire SDK - Migrare da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning Mobile
description: Scopri come sostituire SDK durante la migrazione da Adobe Target all’estensione Adobe Journey Optimizer - Decisioning Mobile.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 62afd1f41b3d20c04782a2b18423683ed3b49d1f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---

# Sostituire il SDK di Target con il SDK di ottimizzazione

Scopri come sostituire gli SDK di Adobe Target con gli SDK di ottimizzazione nell’implementazione mobile. Una sostituzione di base è costituita dai seguenti passaggi:

* Aggiornare le dipendenze nel Podfile o nel file `build.gradle`
* Aggiorna importazioni
* Aggiorna codice applicazione

>[!INFO]
>
>Nell’ecosistema di Adobe Experience Platform Mobile SDK, le estensioni vengono implementate dagli SDK importati nelle applicazioni che possono avere nomi diversi:
>
> * **Target SDK** implementa l&#39;estensione **Adobe Target**
> * **Ottimizza SDK** implementa l&#39;estensione **Adobe Journey Optimizer - Decisioning**

## Aggiorna dipendenze

+++Esempio di Android

>[!BEGINTABS]

>[!TAB Ottimizza SDK]

`build.gradle` dipendenze dopo la migrazione

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:edgeconsent'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:assurance'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!TAB SDK di destinazione]

`build.gradle` dipendenze prima della migrazione

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ Esempio di iOS

>[!BEGINTABS]


>[!TAB Ottimizza SDK]

`Podfile` dipendenze dopo la migrazione

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK di destinazione]

`Podfile` dipendenze prima della migrazione

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## Aggiorna importazioni e codice

+++ Esempio di Android

>[!BEGINTABS]

>[!TAB Ottimizza SDK]

Codice di inizializzazione Java dopo la migrazione

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Assurance;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
import com.adobe.marketing.mobile.edge.consent.Consent;
import com.adobe.marketing.mobile.edge.identity.Identity;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Consent.EXTENSION,
            com.adobe.marketing.mobile.edge.identity.Identity.EXTENSION,
            com.adobe.marketing.mobile.Identity.EXTENSION,
            Edge.EXTENSION,
            Assurance.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!TAB SDK di destinazione]

Codice di inizializzazione Java prima della migrazione

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB Ottimizza SDK]

Codice di inizializzazione Swift dopo la migrazione

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Consent.self,
            AEPEdgeIdentity.Identity.self,
            AEPIdentity.Identity.self,
            Edge.self,
            Assurance.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!TAB SDK di destinazione]

Codice di inizializzazione Swift prima della migrazione

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## Confronto delle funzioni

Molte funzioni di estensione di Target hanno un approccio equivalente che utilizza l’estensione Decisioning descritta nella tabella seguente. Per ulteriori dettagli sulle [funzioni](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| Estensione Target | Estensione Decisioning | Note |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Quando si utilizza l&#39;API `getPropositions`, non viene effettuata alcuna chiamata remota per recuperare ambiti non memorizzati in cache in SDK. |
| `displayedLocations` | Offerta -> `displayed()` | È inoltre possibile utilizzare il metodo di offerta `generateDisplayInteractionXdm` per generare XDM per la visualizzazione degli elementi. Successivamente, l’API sendEvent della rete Edge SDK può essere utilizzata per allegare dati XDM aggiuntivi in formato libero e inviare un evento esperienza al remoto. |
| `clickedLocation` | Offerta -> `tapped()` | Inoltre, è possibile utilizzare il metodo di offerta `generateTapInteractionXdm` per generare XDM per il tocco dell&#39;elemento. Successivamente, l’API sendEvent della rete Edge SDK può essere utilizzata per allegare dati XDM aggiuntivi in formato libero e inviare un evento esperienza al remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/d | Utilizza l&#39;API `removeIdentity` dell&#39;estensione Identity for Edge Network per SDK per interrompere l&#39;invio dell&#39;identificatore visitatore alla rete Edge. Per ulteriori dettagli, consulta [la documentazione dell&#39;API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Nota: l&#39;API `resetIdentities` del core mobile cancella tutte le identità memorizzate in SDK, incluso l&#39;Experience Cloud ID (ECID), e dovrebbe essere utilizzata con moderazione. |
| `getSessionId` | n/d | L&#39;handle di risposta `state:store` contiene informazioni relative alla sessione. L’estensione di rete Edge consente di gestirla allegando elementi dell’archivio di stato non scaduti alle richieste successive. |
| `setSessionId` | n/d | L&#39;handle di risposta `state:store` contiene informazioni relative alla sessione. L’estensione di rete Edge consente di gestirla allegando elementi dell’archivio di stato non scaduti alle richieste successive. |
| `getThirdPartyId` | n/d | Utilizza l’API updateIdentities dall’estensione Identity for Edge Network per fornire il valore dell’ID di terze parti. Quindi, configura lo spazio dei nomi ID di terze parti nello stream di dati. Per ulteriori dettagli, consulta [la documentazione mobile sull&#39;ID di terze parti di Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/d | Utilizza l’API updateIdentities dall’estensione Identity for Edge Network per fornire il valore dell’ID di terze parti. Quindi, configura lo spazio dei nomi ID di terze parti nello stream di dati. Per ulteriori dettagli, consulta [la documentazione mobile sull&#39;ID di terze parti di Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/d | L&#39;handle di risposta `locationHint:result` contiene le informazioni dell&#39;hint di posizione di destinazione. Si presume che Target Edge sarà posizionato in modo congiunto con Experience Edge. <br> <br>L&#39;estensione di rete Edge utilizza l&#39;hint di posizione EdgeNetwork per determinare il cluster di rete Edge a cui inviare le richieste. Per condividere l&#39;hint di posizione di rete Edge tra gli SDK (app ibride), utilizza le API `getLocationHint` e `setLocationHint` dell&#39;estensione Edge Network. Per ulteriori dettagli, consulta [la documentazione dell&#39;API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/d | L&#39;handle di risposta `locationHint:result` contiene le informazioni dell&#39;hint di posizione di destinazione. Si presume che Target Edge sarà posizionato in modo congiunto con Experience Edge. <br> <br>L&#39;estensione di rete Edge utilizza l&#39;hint di posizione EdgeNetwork per determinare il cluster di rete Edge a cui inviare le richieste. Per condividere l&#39;hint di posizione di rete Edge tra gli SDK (app ibride), utilizza le API `getLocationHint` e `setLocationHint` dell&#39;estensione Edge Network. Per ulteriori dettagli, consulta [la documentazione dell&#39;API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |


Quindi, scopri come [richiedere ed eseguire il rendering delle attività](render-activities.md) sulla pagina.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).

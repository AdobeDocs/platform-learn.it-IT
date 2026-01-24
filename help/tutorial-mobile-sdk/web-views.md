---
title: Gestire WebViews con Platform Mobile SDK
description: Scopri come gestire la raccolta dati con WebViews in un’app mobile.
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 49d8c53d2ba2f9dcecf2470d855ad22f44763f6f
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# Gestisci visualizzazioni Web

Scopri come gestire la raccolta dati con WebViews in un’app mobile.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Scopri perché è necessario prestare particolare attenzione alle visualizzazioni Web nell’app.
* Comprendi il codice necessario per evitare problemi di tracciamento.

## Potenziali problemi di tracciamento

Gli ECID separati (Experience Cloud Identity) vengono generati quando invii dati dalla parte nativa dell’app e da un WebView all’interno dell’app. Questi ECID separati generano hit disconnessi e dati gonfiati su visite e visitatori. Ulteriori informazioni sull&#39;ECID sono disponibili nella [panoramica ECID](https://experienceleague.adobe.com/it/docs/experience-platform/identity/features/ecid).

Per risolvere gli hit disconnessi e i dati gonfiati, devi passare l’ECID dell’utente dalla parte nativa dell’app a un WebView che potresti voler utilizzare nell’app.

L’estensione AEP Edge Identity utilizzata all’interno di WebView raccoglie l’ECID corrente e lo aggiunge all’URL invece di inviare una richiesta ad Adobe per un nuovo ID. L’implementazione utilizza quindi questo ECID per richiedere l’URL.

## Implementazione

Per implementare la visualizzazione Web:

>[!BEGINTABS]

>[!TAB iOS]

Passare a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]** e individuare la funzione `func loadUrl()` nella classe `final class SwiftUIWebViewModel: ObservableObject`. Aggiungi la seguente chiamata per gestire la visualizzazione web:

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

L&#39;API [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) imposta le variabili per l&#39;URL in modo che contengano tutte le informazioni rilevanti, come ECID e altro ancora. Nell’esempio si utilizza un file locale, ma gli stessi concetti si applicano alle pagine remote.

Ulteriori informazioni sull&#39;API `Identity.getUrlVariables` sono disponibili nella guida di riferimento dell&#39;API dell&#39;estensione [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).


>[!TAB Android]

Passa a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL views]** > **[!DNL WebViewModel]** e individua la funzione `fun loadUrl()` in `class WebViewModel: ViewModel()`. Aggiungi la seguente chiamata per gestire la visualizzazione web:

```kotlin
// Handle web view
Identity.getUrlVariables {
    urlVariables = it
    val baseUrl = getHtmlFileUrl("tou.html")

    val finalUrl = if (urlVariables.isNotEmpty()) {
        "$baseUrl?$urlVariables"
    } else {
        baseUrl
    }

    Handler(Looper.getMainLooper()).post {
        webView.loadUrl(finalUrl)
    }
    MobileSDK.shared.logInfo("TermsOfServiceSheet - loadUrl: Successfully loaded WebView with URL: $finalUrl")
}
```

L&#39;API [`Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) imposta le variabili per l&#39;URL in modo che contengano tutte le informazioni rilevanti, come ECID e altro ancora. Nell’esempio si utilizza un file locale, ma gli stessi concetti si applicano alle pagine remote.

Ulteriori informazioni sull&#39;API `Identity.getUrlVariables` sono disponibili nella guida di riferimento dell&#39;API dell&#39;estensione [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

>[!ENDTABS]

## Convalida nell’app

Per eseguire il codice:

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Vai a **[!UICONTROL Impostazioni]** nell&#39;app
1. Tocca il pulsante **[!DNL View...]** per visualizzare **[!DNL Terms of Use]**.

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/tou1.png" width="300"> <img src="./assets/tou2.png" width="300">

>[!TAB Android]

<img src="./assets/tou1-android.png" width="300"> <img src="./assets/tou2-android.png" width="300">

>[!ENDTABS]


## Convalidare con Assurance

1. Nell&#39;interfaccia utente di Assurance, cerca l&#39;evento **[!UICONTROL Variabili URL di risposta identità di Edge]** dal fornitore **[!UICONTROL com.adobe.griffon.mobile]**.
1. Selezionare l&#39;evento e rivedere il campo **[!UICONTROL urlvariable]** nell&#39;oggetto **[!UICONTROL ACPExtensionEventData]**, confermando la presenza dei seguenti parametri nell&#39;URL: `adobe_mc`, `mcmid` e `mcorgid`.

   ![convalida visualizzazione Web](assets/webview-validation.png){zoomable="yes"}

   Di seguito è riportato un esempio di campo `urvariables`:

   * Originale (con caratteri di escape)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Bellissimo

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

Sfortunatamente, il debug della sessione web è limitato. Ad esempio, non è possibile utilizzare Adobe Experience Platform Debugger nel browser per continuare il debug della sessione di visualizzazione Web.

>[!NOTE]
>
>L&#39;unione dei visitatori tramite questi parametri URL è supportata in Platform Web SDK (versioni 2.11.0 o successive) e quando si utilizza `VisitorAPI.js`.


>[!SUCCESS]
>
>Ora hai configurato l’app per visualizzare il contenuto in base a un URL in una visualizzazione web utilizzando lo stesso ECID già rilasciato dal SDK mobile di Adobe Experience Platform.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=it)

Successivo: **[Identità](identity.md)**

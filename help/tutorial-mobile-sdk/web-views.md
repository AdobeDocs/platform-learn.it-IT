---
title: Gestire WebViews con Platform Mobile SDK
description: Scopri come gestire la raccolta dati con WebViews in un’app mobile.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Gestisci visualizzazioni Web

Scopri come gestire la raccolta dati con WebViews in un’app mobile.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Scopri perché è necessario prestare particolare attenzione alle visualizzazioni Web nell’app.
* Comprendi il codice necessario per evitare problemi di tracciamento.

## Potenziali problemi di tracciamento

Se invii dati dalla parte nativa dell’app e da un WebView all’interno dell’app, ciascuno di essi genera il proprio ID Experience Cloud (ECID), che si traduce in hit disconnessi e dati gonfiati relativi a visite/visitatori. Ulteriori informazioni sull’ECID sono disponibili nella sezione [Panoramica di ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Per risolvere questa situazione indesiderata, è importante passare l’ECID dell’utente dalla parte nativa dell’app a una WebView che potrebbe essere utile utilizzare nell’app.

L&#39;estensione AEP Edge Identity utilizzata all&#39;interno di WebView raccoglie l&#39;ECID corrente e lo aggiunge all&#39;URL invece di inviare una richiesta all&#39;Adobe per un nuovo ID. L’implementazione utilizza quindi questo ECID per richiedere l’URL.

## Implementazione

Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]**, e individuare `func loadUrl()` funzione in `final class SwiftUIWebViewModel: ObservableObject` classe. Aggiungi la seguente chiamata per gestire la visualizzazione web:

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

Il [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) API imposta le variabili per l’URL in modo che contengano tutte le informazioni rilevanti, come ECID e altro ancora. Nell’esempio si utilizza un file locale, ma gli stessi concetti si applicano alle pagine remote.

Puoi saperne di più sulle `Identity.getUrlVariables` API in [Guida di riferimento API dell’estensione Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Convalida

Per eseguire il codice:

1. Rivedi [istruzioni di configurazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Vai a **[!UICONTROL Impostazioni]** nell’app
1. Tocca il **[!DNL View...]** per visualizzare **[!DNL Terms of Use]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. Nell’interfaccia utente Assurance, cerca **[!UICONTROL Variabili URL di risposta dell’identità Edge]** evento da **[!UICONTROL com.adobe.griffon.mobile]** fornitore.
1. Seleziona l’evento e controlla **[!UICONTROL urlvariable]** campo in **[!UICONTROL ACPExtensionEventData]** , a conferma della presenza dei seguenti parametri nell&#39;URL: `adobe_mc`, `mcmid`, e `mcorgid`.

   ![convalida webview](assets/webview-validation.png)

   Un esempio `urvariables` di seguito:

   * Originale (con caratteri di escape)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Bellissimo

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

Sfortunatamente, il debug della sessione web è limitato. Non è possibile, ad esempio, utilizzare l&#39;Adobe Experience Platform Debugger nel browser per continuare il debug della sessione di visualizzazione Web.

>[!NOTE]
>
>L’unione dei visitatori tramite questi parametri URL è supportata in Platform Web SDK (versioni 2.11.0 o successive) e quando si utilizza `VisitorAPI.js`.


>[!SUCCESS]
>
>Ora hai configurato l’app per visualizzare il contenuto in base a un URL in una visualizzazione web utilizzando lo stesso ECID già emesso dall’SDK di Adobe Experience Platform Mobile.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Identità](identity.md)**

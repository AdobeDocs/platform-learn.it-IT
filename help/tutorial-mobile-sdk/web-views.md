---
title: Gestisci visualizzazioni Web
description: Scopri come gestire la raccolta dati con WebViews in un’app mobile.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---

# Gestisci visualizzazioni Web

Scopri come gestire la raccolta dati con WebViews in un’app mobile.

>[!INFO]
>
> Questo tutorial verrà sostituito da un nuovo tutorial che utilizzerà una nuova app mobile di esempio a fine novembre 2023

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Comprendere il motivo per cui è necessario tenere in considerazione le visualizzazioni Web.
* Comprendi il codice necessario per evitare problemi di tracciamento.

## Potenziali problemi di tracciamento

Se invii dati dalla parte nativa dell’app e da un WebView, ciascuno di essi genera il proprio ID Experience Cloud (ECID). Questo comporta risultati disconnessi e dati gonfiati su visite/visitatori. Ulteriori informazioni sull’ECID sono disponibili nella sezione [Panoramica di ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Per risolvere questa situazione indesiderata, è importante passare l’ECID dell’utente dalla parte nativa a WebView.

L&#39;estensione JavaScript del servizio ID Experience Cloud in WebView estrae l&#39;ECID dall&#39;URL invece di inviare una richiesta all&#39;Adobe per un nuovo ID. Il servizio ID utilizza questo ECID per monitorare il visitatore.

## Implementazione

Nell’app di esempio Luma, individua `TermsOfService.swift` file (in `Intro-Login_SignUp` cartella ) e individuare il codice seguente:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Questo è un modo semplice per caricare una WebView. In questo caso, si tratta di un file locale, ma gli stessi concetti si applicano alle pagine remote.

Effettua il refactoring del codice della visualizzazione Web come mostrato di seguito:

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

Puoi saperne di più sulle `Identity.getUrlVariables` API in [Guida di riferimento API dell’estensione Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Convalida

Dopo aver esaminato [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance, caricare WebView e cercare il `Edge Identity Response URL Variables` evento da `com.adobe.griffon.mobile` fornitore.

Per caricare WebView, vai alla schermata iniziale dell’app Luma, seleziona l’icona &quot;account&quot;, seguita dalle &quot;Condizioni d’uso&quot; nel piè di pagina.

Dopo aver caricato WebView, selezionare l&#39;evento e rivedere `urlvariables` campo in `ACPExtensionEventData` , a conferma della presenza dei seguenti parametri nell&#39;URL: `adobe_mc`, `mcmid`, e `mcorgid`.

![convalida webview](assets/mobile-webview-validation.png)

Un esempio `urvariables` di seguito:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>L’unione di visitatori tramite questi parametri URL è attualmente supportata in Platform Web SDK (versioni 2.11.0 o successive) e `VisitorAPI.js`.


Successivo: **[Identità](identity.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
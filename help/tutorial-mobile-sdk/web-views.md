---
title: Gestisci WebViews
description: Scopri come gestire la raccolta dati con WebViews in un’app mobile.
kt: 6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Gestisci WebViews

Scopri come gestire la raccolta dati con WebViews in un’app mobile.

## Prerequisiti

* L’app è stata generata ed eseguita correttamente con gli SDK installati e configurati.

## Finalità di apprendimento

In questa lezione:

* Comprendere perché è necessario prendere considerazioni speciali per WebViews.
* Comprendi il codice necessario per evitare problemi di tracciamento.

## Potenziali problemi di tracciamento

Se invii dati dalla parte nativa dell&#39;app e da una WebView, ciascuno genera il proprio ID Experience Cloud (ECID). Questo determina hit disconnessi e dati gonfiati di visite/visitatori. Ulteriori informazioni sull&#39;ECID sono disponibili nella sezione [Panoramica ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Per risolvere questa situazione indesiderabile, è importante passare l&#39;ECID dell&#39;utente dalla parte nativa a WebView.

L&#39;estensione JavaScript del servizio Experience Cloud ID nel WebView estrae l&#39;ECID dall&#39;URL invece di inviare una richiesta ad Adobe per un nuovo ID. Il servizio ID utilizza questo ECID per tenere traccia del visitatore.

## Implementazione

Nell’app di esempio Luma, trova la `TermsOfService.swift` (nel `Intro-Login_SignUp` e individua il seguente codice:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Questo è un modo semplice per caricare un WebView. In questo caso, si tratta di un file locale ma gli stessi concetti si applicano alle pagine remote.

Refactorizza il codice della visualizzazione web come mostrato di seguito:

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

Puoi saperne di più sul `Identity.getUrlVariables` API in [Guida di riferimento per l’API di Identity for Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables).

## Convalida

Dopo aver esaminato la [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo a Assurance, caricare WebView e cercare il `Edge Identity Response URL Variables` evento dal `com.adobe.griffon.mobile` fornitore.

Per caricare WebView, passa alla schermata iniziale dell’app Luma, seleziona l’icona &quot;account&quot;, seguita da &quot;Condizioni d’uso&quot; nel piè di pagina.

Dopo aver caricato WebView, selezionare l&#39;evento e rivedere il `urlvariables` nel campo `ACPExtensionEventData` oggetto , confermando i seguenti parametri sono presenti nell&#39;URL: `adobe_mc`, `mcmid`e `mcorgid`.

![convalida webview](assets/mobile-webview-validation.png)

Un campione `urvariables` di seguito è possibile vedere il campo :

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>L’unione dei visitatori tramite questi parametri URL è attualmente supportata in Platform Web SDK (versione 2.11.0 o successiva) e `VisitorAPI.js`.


Avanti: **[Identità](identity.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
---
title: Imposta garanzia
description: Scopri come implementare l’estensione Assurance in un’app mobile.
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---

# Assurance

Scopri come configurare Adobe Experience Platform Assurance in un’app mobile.

Assurance, formalmente noto come Project Griffon, è progettato per aiutarti a controllare, provare, simulare e convalidare il modo in cui raccogli dati o distribuisci esperienze nella tua app mobile.

Questa funzione consente di controllare gli eventi SDK non elaborati generati dall’SDK di Adobe Experience Platform Mobile. Tutti gli eventi raccolti dall’SDK sono disponibili per l’ispezione. Gli eventi SDK vengono caricati in una vista a elenco, ordinati per ora. Ogni evento ha una visualizzazione dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili visualizzazioni aggiuntive per sfogliare la configurazione SDK, gli elementi dati, gli stati condivisi e le versioni di estensione SDK. Ulteriori informazioni sulle [Affidabilità](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance) nella documentazione del prodotto.


## Prerequisiti

* Creazione ed esecuzione dell&#39;app di esempio con SDK installati e configurati correttamente.

## Finalità di apprendimento

In questa lezione:

* Conferma che l’organizzazione dispone dell’accesso (e, in caso contrario, richiedi l’accesso).
* Imposta l&#39;URL di base.
* Aggiungi il codice specifico iOS richiesto.
* Connettiti a una sessione.

## Conferma accesso

Conferma che la tua organizzazione abbia accesso ad Assurance completando i seguenti passaggi:

1. Visita [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon){target=&quot;_blank&quot;}
1. Accedi utilizzando le tue credenziali Adobe ID per l&#39;Experience Cloud.
1. Se vieni portato al **[!UICONTROL Sessioni]** screen, quindi hai accesso. Se vieni portato alla pagina di accesso beta, seleziona **[!UICONTROL Registro]**.

## Implementazione

Oltre al generale [Installazione SDK](install-sdks.md) completato nella lezione precedente, iOS richiede anche l’aggiunta seguente. Aggiungi il codice seguente al file `AppDelegate.swift`:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

Il Luma di esempio fornito per questa esercitazione utilizza iOS 12.0. Se segui con la tua applicazione basata su scene utilizzando iOS 13 e versioni successive, utilizza il `UISceneDelegate's scene(_:openURLContexts:)` come segue:

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

Ulteriori informazioni sono disponibili [qui](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance#implement-aep-assurance-session-start-apis-ios-only){target=&quot;_blank&quot;}.

## Impostare un URL di base

1. Apri XCode e seleziona il nome del progetto.
1. Passa a **Info** scheda .
1. Scorri verso il basso fino a **Tipi di URL** e seleziona la **+** per aggiungerne uno nuovo.
1. Imposta **Identificatore** e **Schemi URL** a &quot;lumadeeplink&quot;.
1. Crea ed esegui l’app.

![url di garanzia](assets/mobile-assurance-url-type.png)

Per ulteriori informazioni sugli schemi URL in iOS, consulta [Documentazione di Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=&quot;_blank&quot;}.

Questa funzione consente di aprire un URL tramite browser o codice QR e inizia con l’URL di base che apre l’app e contiene parametri aggiuntivi. Questi parametri univoci vengono utilizzati per collegare la sessione.

## Connessione a una sessione

1. Passa a [Interfaccia utente di controllo](https://experience.adobe.com/griffon){target=&quot;_blank&quot;}.
1. Seleziona **[!UICONTROL Crea sessione]**.
1. Fornire **[!UICONTROL Nome sessione]** quali `Luma App QA` e **[!UICONTROL URL di base]** `lumadeeplink://default`
1. Seleziona **[!UICONTROL Avanti]**.
   ![sessione di creazione del controllo](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL Digitalizza codice QR]** se utilizzi un dispositivo fisico. Se utilizzi il simulatore, allora **[!UICONTROL Copia collegamento]** e aprilo con Safari nel simulatore.
   ![codice QA di garanzia](assets/mobile-assurance-qr-code.png)
1. Quando l&#39;app viene caricata ti viene presentato un modale che ti chiede di inserire il PIN dal passaggio precedente.
   ![spillo di sicurezza](assets/mobile-assurance-enter-pin.png)
1. Se la connessione ha avuto esito positivo, nell’app verranno visualizzati gli eventi nell’interfaccia utente Web di Assurance e un’icona di Controllo mobile.
   * Icona di garanzia mobile.
      ![modale di garanzia](assets/mobile-assurance-modal.png)
   * Experience Cloud di eventi in arrivo nell’interfaccia utente web.
      ![eventi di assicurazione](assets/mobile-assurance-events.png)

In caso di problemi, consulta la sezione [tecnico](https://aep-sdks.gitbook.io/docs/foundation-extensions/adobe-experience-platform-assurance){target=&quot;_blank&quot;} e [documentazione generale](https://aep-sdks.gitbook.io/docs/beta/project-griffon){target=&quot;_blank&quot;}.

Avanti: **[Consenso](consent.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
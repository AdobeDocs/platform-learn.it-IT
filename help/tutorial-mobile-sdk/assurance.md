---
title: Configura Assurance
description: Scopri come implementare l’estensione Assurance in un’app mobile.
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---

# Assurance

Scopri come configurare Adobe Experience Platform Assurance in un’app mobile.

Assurance, formalmente noto come Project Griffon, è progettato per aiutarti a ispezionare, verificare, simulare e convalidare come raccolgi dati o distribuisci esperienze nella tua app mobile.

Assurance consente di esaminare gli eventi SDK non elaborati generati dall’SDK di Adobe Experience Platform Mobile. Tutti gli eventi raccolti dall’SDK sono disponibili per l’ispezione. Gli eventi SDK vengono caricati in una vista a elenco, ordinati in base all’ora. Ogni evento ha una vista dettagliata che fornisce ulteriori dettagli. Sono inoltre disponibili viste aggiuntive per sfogliare la configurazione dell’SDK, gli elementi dati, gli stati condivisi e le versioni delle estensioni SDK. Ulteriori informazioni su [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) nella documentazione del prodotto.


## Prerequisiti

* L&#39;app di esempio con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Conferma che la tua organizzazione disponga dell’accesso (e richiedilo in caso contrario).
* Configurare l&#39;URL di base.
* Aggiungi il codice iOS specifico richiesto.
* Connettersi a una sessione.

## Conferma accesso

Conferma che la tua organizzazione abbia accesso a Assurance completando i seguenti passaggi:

1. Visita [https://experience.adobe.com/#/assurance](https://experience.adobe.com/griffon){target="_blank"}
1. Accedi con le credenziali Adobe ID per l’Experience Cloud.
1. Se si viene portati al **[!UICONTROL Sessioni]** , quindi puoi accedere a. Se vieni reindirizzato alla pagina di accesso beta, seleziona **[!UICONTROL Registrati]**.

## Implementazione

Oltre al generale [Installazione SDK](install-sdks.md) hai completato la lezione precedente, iOS richiede anche la seguente aggiunta. Aggiungi il codice seguente al file `AppDelegate.swift`:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

Il Luma di esempio fornito per questa esercitazione utilizza iOS 12.0. Se segui insieme all’applicazione basata sulla scena utilizzando iOS 13 e versioni successive, utilizza `UISceneDelegate's scene(_:openURLContexts:)` metodo come segue:

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

Ulteriori informazioni sono disponibili [qui](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## Configurare un URL di base

1. Apri Xcode e seleziona il nome del progetto.
1. Accedi a **Info** scheda.
1. Scorri verso il basso fino a **Tipi di URL** e seleziona la **+** per aggiungerne uno nuovo.
1. Imposta **Identificatore** e **Schemi URL** su &quot;lumadeeplink&quot;.
1. Crea ed esegui l’app.

![url di garanzia](assets/mobile-assurance-url-type.png)

Per ulteriori informazioni sugli schemi URL in iOS, consulta [Documentazione di Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

La garanzia funziona aprendo un URL, tramite browser o codice QR, che inizia con l’URL di base che apre l’app e contiene parametri aggiuntivi. Questi parametri univoci vengono utilizzati per connettere la sessione.

## Connessione a una sessione

1. Accedi a [Interfaccia utente Assurance](https://experience.adobe.com/griffon){target="_blank"}.
1. Seleziona **[!UICONTROL Crea sessione]**.
1. Fornire **[!UICONTROL Nome sessione]** come `Luma App QA` e **[!UICONTROL URL di base]** `lumadeeplink://default`
1. Seleziona **[!UICONTROL Avanti]**.
   ![sessione di creazione della garanzia di affidabilità](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL Scansiona codice QR]** se utilizzi un dispositivo fisico. Se utilizzi il simulatore, allora **[!UICONTROL Copia collegamento]** e aprilo con Safari nel simulatore.
   ![codice di controllo qualità assicurazione](assets/mobile-assurance-qr-code.png)
1. Al caricamento dell’app, viene visualizzata una finestra modale in cui viene richiesto di immettere il PIN del passaggio precedente.
   ![pin immissione garanzia](assets/mobile-assurance-enter-pin.png)
1. Se la connessione ha avuto esito positivo, nell’interfaccia utente web di Assurance verranno visualizzati gli eventi e un’icona mobile Assurance nell’app.
   * Icona Assurance mobile.
      ![assicurazione modale](assets/mobile-assurance-modal.png)
   * Eventi di Experience Cloud che arrivano nell’interfaccia web.
      ![eventi di garanzia](assets/mobile-assurance-events.png)

In caso di problemi, consulta [tecnico](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

Successivo: **[Consenso](consent.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

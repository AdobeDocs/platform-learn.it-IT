---
title: Profilo
description: Scopri come raccogliere i dati di profilo in un’app mobile.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Profilo

Scopri come raccogliere i dati di profilo in un’app mobile.

Puoi utilizzare l’estensione Profilo per memorizzare sul client gli attributi relativi all’utente. Queste informazioni possono essere utilizzate in un secondo momento per eseguire il targeting e personalizzare i messaggi durante scenari online o offline, senza dover connettersi a un server per ottenere prestazioni ottimali. L’estensione Profilo gestisce il profilo operativo lato client (CSOP), fornisce un modo di reagire alle API, aggiorna gli attributi del profilo utente e condivide gli attributi del profilo utente con il resto del sistema come un evento generato.

I dati del profilo vengono utilizzati da altre estensioni per eseguire azioni relative al profilo. Un esempio è l’estensione Rules Engine che consuma i dati del profilo ed esegue le regole in base ai dati del profilo. Ulteriori informazioni sulle [Estensione del profilo](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) nella documentazione

>[!IMPORTANT]
>
>La funzionalità Profilo descritta in questa lezione è separata dalla funzionalità Profilo cliente in tempo reale nelle applicazioni Adobe Experience Platform e basate su Platform.


## Prerequisiti

* L’app è stata generata ed eseguita correttamente con gli SDK installati e configurati.
* È stato importato l’SDK del profilo.

   ```swift
   import AEPUserProfile
   ```

## Finalità di apprendimento

In questa lezione:

* Impostare o aggiornare gli attributi utente.
* Recupera gli attributi utente.


## Imposta e aggiorna

Sarebbe utile che il targeting e/o la personalizzazione sapessero rapidamente se un utente ha effettuato un acquisto nell’app in precedenza. Configuriamola nell’app Luma.

1. Passa a `Cart.swift`

1. Aggiungi il codice seguente al `processOrder() `funzione .

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Il team di personalizzazione potrebbe anche voler eseguire il targeting in base al livello di fedeltà dell’utente. Configuriamola nell’app Luma.

1. Passa a `Account.swift`

1. Aggiungi il codice seguente al `showUserInfo()` funzione .

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Aggiuntivo `updateUserAttributes` la documentazione è disponibile [qui](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## Ottenere

Dopo aver aggiornato l’attributo di un utente, questo sarà disponibile per altri SDK di Adobe, ma puoi anche recuperare gli attributi in modo esplicito.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Aggiuntivo `getUserAttributes` la documentazione è disponibile [qui](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## Convalida con affidabilità

1. Consulta la sezione [istruzioni di configurazione](assurance.md) sezione .
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato per l’affidabilità.
1. Seleziona l’icona Account , quindi seleziona Accesso. Nota: non è necessario fornire credenziali.
1. Chiudi i menu di accesso e seleziona nuovamente l’icona Account . Questo ti porta alla schermata dei dettagli dell’account dove `loyaltyLevel` è impostato.
1. Dovresti visualizzare un **[!UICONTROL AggiornamentoProfiloUtente]** nell’interfaccia utente di Assurance con l’aggiornamento `profileMap` valore.
   ![convalida profilo](assets/mobile-profile-validate.png)

Avanti: **[Mappatura di dati su Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
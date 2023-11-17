---
title: Profilo
description: Scopri come raccogliere i dati del profilo in un’app mobile.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Profilo

Scopri come raccogliere i dati del profilo in un’app mobile.

>[!INFO]
>
> Questo tutorial verrà sostituito da un nuovo tutorial che utilizzerà una nuova app mobile di esempio a fine novembre 2023

Puoi utilizzare l’estensione Profilo per memorizzare gli attributi dell’utente sul client. Queste informazioni possono essere utilizzate in un secondo momento per eseguire il targeting e personalizzare i messaggi durante scenari online o offline, senza dover connettersi a un server per ottenere prestazioni ottimali. L’estensione Profile gestisce il profilo operativo lato client (CSOP, Client-Side Operation Profile), fornisce un modo per reagire alle API, aggiorna gli attributi del profilo utente e condivide gli attributi del profilo utente con il resto del sistema come evento generato.

I dati di profilo vengono utilizzati da altre estensioni per eseguire azioni relative al profilo. Un esempio è l’estensione Rules Engine che utilizza i dati del profilo ed esegue le regole in base ai dati del profilo. Ulteriori informazioni su [Estensione profilo](https://developer.adobe.com/client-sdks/documentation/profile/) nella documentazione di

>[!IMPORTANT]
>
>La funzionalità di profilo descritta in questa lezione è distinta dalla funzionalità Profilo cliente in tempo reale nelle applicazioni basate su Adobe Experience Platform e Platform.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Importazione dell’SDK del profilo.

  ```swift
  import AEPUserProfile
  ```

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Imposta o aggiorna gli attributi utente.
* Recuperare gli attributi utente.


## Imposta e aggiorna

Sarebbe utile per il targeting e/o la personalizzazione sapere rapidamente se un utente ha effettuato un acquisto nell’app in precedenza. Impostiamolo nell’app Luma.

1. Passa a `Cart.swift`

1. Aggiungi il codice seguente al `processOrder() `funzione.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Il team di personalizzazione potrebbe anche eseguire il targeting in base al livello di fedeltà dell’utente. Impostiamolo nell’app Luma.

1. Passa a `Account.swift`

1. Aggiungi il codice seguente al `showUserInfo()` funzione.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Aggiuntivo `updateUserAttributes` La documentazione è disponibile [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Ottenere

Dopo aver aggiornato l’attributo di un utente, questo sarà disponibile per altri SDK Adobe, ma puoi anche recuperare esplicitamente gli attributi.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Aggiuntivo `getUserAttributes` La documentazione è disponibile [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Fai clic sull’icona Account, quindi seleziona Login. Nota: non si dispone di credenziali.
1. Chiudere i menu di accesso, quindi selezionare nuovamente l&#39;icona Account. Viene visualizzata la schermata dei dettagli dell&#39;account in cui `loyaltyLevel` è impostato.
1. Dovresti vedere un **[!UICONTROL UserProfileUpdate]** nell’interfaccia utente Assurance con il `profileMap` valore.
   ![convalida profilo](assets/mobile-profile-validate.png)

Successivo: **[Mappare i dati su Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
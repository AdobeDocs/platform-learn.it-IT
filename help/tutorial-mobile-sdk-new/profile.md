---
title: Profilo
description: Scopri come raccogliere i dati del profilo in un’app mobile.
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# Profilo

Scopri come raccogliere i dati del profilo in un’app mobile.

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


## Imposta e aggiorna attributi utente

Sarebbe utile per il targeting e/o la personalizzazione sapere rapidamente se un utente ha effettuato un acquisto nell’app in precedenza. Impostiamolo nell’app Luma.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** >  **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode e trovare il `func updateUserAttribute(attributeName: String, attributeValue: String)` funzione. Aggiungi il seguente codice:

   ```swift
   // Create a profile map
   var profileMap = [String: Any]()
   // Add attributes to profile map
   profileMap[attributeName] = attributeValue
   // Use profile map to update user attributes
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Questo codice:

   1. Imposta un dizionario vuoto denominato `profileMap`.

   1. Aggiunge un elemento al dizionario utilizzando `attributeName` (ad esempio `isPaidUser`), e `attributeValue` (ad esempio `yes`).

   1. Utilizza il `profileMap` dizionario come valore per `attributeDict` parametro di `UserProfile.updateUserAttributes` Chiamata API.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Prodotti]** > **[!UICONTROL ProductView]** nel Navigator del progetto Xcode e trova la chiamata a `updateUserAttributes` (all&#39;interno del codice per gli acquisti <img src="assets/purchase.png" width="15" /> pulsante):

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
   ```

È possibile trovare ulteriore documentazione [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Ottieni attributi utente

Dopo aver aggiornato l’attributo di un utente, questo è disponibile per altri SDK di Adobe, ma puoi anche recuperare esplicitamente gli attributi.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > Generale > **[!UICONTROL HomeView]** nel Navigatore progetti Xcode e trovare il `.onAppear` modificatore. Aggiungi il seguente codice:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   Questo codice:

   1. Chiama il `UserProfile.getUserAttributes` chiusura con il `iPaidUser` nome attributo come singolo elemento nel `attributeNames` array.
   1. Quindi controlla il valore di `isPaidUser` attributo e quando `yes`, posiziona un badge sul <img src="assets/paiduser.png" width="20" /> nella barra degli strumenti in alto a destra.

È possibile trovare ulteriore documentazione [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Esegui l’app per accedere e interagire con un prodotto.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede.
   1. Per aprire il foglio di accesso, selezionare <img src="assets/login.png" width="15" /> pulsante.
   1. Per inserire un’e-mail casuale e un ID cliente, seleziona la <img src="assets/insert.png" width="15" /> pulsante .
   1. Seleziona **[!UICONTROL Login]**.
   1. Seleziona **[!UICONTROL Prodotti]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona <img src="assets/saveforlater.png" width="15" />.
   1. Seleziona <img src="assets/addtocart.png" width="20" />.
   1. Seleziona <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">
   1. Torna a **[!UICONTROL Home]** schermo. Dovresti vedere un distintivo aggiunto <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="200">



1. Nell’interfaccia utente Assurance, dovresti visualizzare un’ **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** eventi con aggiornato `profileMap` valore.
   ![convalida profilo](assets/profile-validate.png)

>[!SUCCESS]
>
>Ora hai configurato l’app per aggiornare gli attributi dei profili nella rete Edge e (se configurata) con Adobe Experience Platform.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Mappare i dati su Adobe Analytics](analytics.md)**

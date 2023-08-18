---
title: Profilo
description: Scopri come raccogliere i dati del profilo in un’app mobile.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

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


## Imposta e aggiorna

Sarebbe utile per il targeting e/o la personalizzazione sapere rapidamente se un utente ha effettuato un acquisto nell’app in precedenza. Impostiamolo nell’app Luma.

1. Accedi a **[!UICONTROL ProductView]** (in **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Prodotti]**) nel progetto app Xcode Luma e trova la chiamata a `updateUserAttributes` (nel pulsante Acquisti ):

   ```swift {highlight="8-9"}
   Button {
       Task {
           if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send purchase commerce experience event
               MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
               // Update attributes
               MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
           }
       }
       showPurchaseDialog.toggle()
   } label: {
       Label("", systemImage: "creditcard")
   }
   .alert(isPresented: $showPurchaseDialog, content: {
       Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
   })
   ```

2. Accedi a **[!UICONTROL MobileSDK]** e trovare `updateUserAttributes` funzione. Aggiungi il seguente codice evidenziato:

   ```swift {highlight="2-4"}
   func updateUserAttributes(attributeName: String, attributeValue: String) {
       var profileMap = [String: Any]()
       profileMap[attributeName] = attributeValue
       UserProfile.updateUserAttributes(attributeDict: profileMap)
   }
   ```

   Questo codice:

   1. Imposta un dizionario vuoto denominato `profileMap`.

   1. Aggiunge un elemento al dizionario utilizzando `attributeName` (ad esempio `isPaidUser`), e `attributeValue` (ad esempio `yes`).

   1. Utilizza il `profileMap` dizionario come valore per `attributeDict` parametro di `UserProfile.updateUserAttributes` Chiamata API.


Aggiuntivo `updateUserAttributes` La documentazione è disponibile [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Ottenere

Dopo aver aggiornato l’attributo di un utente, questo è disponibile per altri SDK di Adobe, ma puoi anche recuperare esplicitamente gli attributi.

1. Accedi a **[!UICONTROL HomeView]** (in **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Generale]**) e trovare il `.onAppear` modificatore. Aggiungi il seguente codice:

   ```swift {highlight="3-11"}
   .onAppear {
       // Track view screen
       MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: home")
       // Get attributes
       UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
           if attributes?["isPaidUser"] as! String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Questo codice:

   1. Chiama il `UserProfile.getUserAttributes` chiusura con il `iPaidUser` nome attributo come singolo elemento nel `attributeNames` array.
   1. Quindi controlla il valore di `isPaidUser` attributo e quando `yes`, posiziona un badge sull’icona Persona in alto a destra.

Aggiuntivo `getUserAttributes` La documentazione è disponibile [qui](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md) sezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Esegui l’app per accedere e interagire con un prodotto.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede.
   1. Per aprire il foglio di accesso, selezionare **[!UICONTROL Login]** pulsante.
   1. Per inserire un’e-mail casuale e un ID cliente, seleziona la **[!UICONTROL A|]** pulsante .
   1. Seleziona **[!UICONTROL Login]**.
   1. Seleziona **[!UICONTROL Prodotti]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona **[!UICONTROL Salva per dopo]**.
   1. Seleziona **[!UICONTROL Aggiungi al carrello]**.
   1. Seleziona **[!UICONTROL Acquisto]**.
   1. Torna a **[!UICONTROL Home]** schermo. Dovresti trovare un pulsante di accesso aggiornato.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200"> <img src="./assets/personbadges.png" width="200">

1. Dovresti vedere un **[!UICONTROL UserProfileUpdate]** e **[!UICONTROL getUserAttributes]** nell&#39;interfaccia utente Assurance con gli eventi aggiornati `profileMap` valore.
   ![convalida profilo](assets/profile-validate.png)

>[!SUCCESS]
>
>Ora hai configurato l’app per aggiornare gli attributi dei profili nella rete Edge e (se configurata) con Adobe Experience Platform.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Mappare i dati su Adobe Analytics](analytics.md)**

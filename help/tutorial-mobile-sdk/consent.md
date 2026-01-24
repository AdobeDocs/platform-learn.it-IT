---
title: Implementazione del consenso per le implementazioni di Platform Mobile SDK
description: Scopri come implementare il consenso in un’app mobile.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Implementare il consenso

Scopri come implementare il consenso in un’app mobile.

L’estensione per dispositivi mobili Adobe Experience Platform Consent abilita la raccolta delle preferenze di consenso dalla tua app mobile quando utilizzi Adobe Experience Platform Mobile SDK e l’estensione Edge Network. Ulteriori informazioni sull&#39;[estensione del consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) sono disponibili nella documentazione.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Richiedere il consenso all&#39;utente.
* Aggiorna l&#39;estensione in base alla risposta dell&#39;utente.
* Scopri come ottenere lo stato di consenso corrente.

## Richiedi consenso

Se hai seguito l&#39;esercitazione fin dall&#39;inizio, ricorda di aver impostato il consenso predefinito nell&#39;estensione Consenso su **[!UICONTROL In sospeso - Eventi di coda che si verificano prima che l&#39;utente fornisca le preferenze di consenso.]**

Per iniziare a raccogliere i dati, devi ottenere il consenso dell’utente. In un’app reale, vorresti consultare le best practice sul consenso per la tua regione. In questa esercitazione, ottieni il consenso dell’utente semplicemente richiedendolo con un avviso:

>[!BEGINTABS]

>[!TAB iOS]

1. Desideri chiedere all’utente il consenso solo una volta. Il consenso per Mobile SDK viene combinato con l&#39;autorizzazione richiesta per il tracciamento tramite il [framework per la trasparenza del tracciamento delle app](https://developer.apple.com/documentation/apptrackingtransparency) di Apple. In questa app, si presume che quando l’utente autorizza il tracciamento, acconsente alla raccolta di eventi.

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode.

   Aggiungere il codice alla funzione `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisclaimerView]** nel Navigatore progetti di Xcode. Il Navigatore progetti Xode è la visualizzazione che viene mostrata dopo l’installazione o la reinstallazione dell’applicazione e il primo avvio dell’app. All&#39;utente viene richiesto di autorizzare il tracciamento in base al [framework per la trasparenza del tracciamento delle app](https://developer.apple.com/documentation/apptrackingtransparency) di Apple. Se l’utente autorizza, aggiorna anche il consenso.

   Aggiungere il codice seguente alla chiusura di `ATTrackingManager.requestTrackingAuthorization { status in`.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

>[!TAB Android]

1. Desideri chiedere all’utente il consenso solo una volta. In questa app, si presume che quando l’utente autorizza il tracciamento, acconsente alla raccolta di eventi.

1. Passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL modelli]** > **[!UICONTROL MobileSDK]** nel navigatore di Android Studio.

   Aggiungere il codice alla funzione `updateConsent(value: String)`.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL visualizzazioni]** > **[!UICONTROL DisclaimerView.kt]** nel navigatore di Android Studio.

   Aggiungere il codice seguente alla funzione `DisclaimerView(navController: NavController)` sotto `// Set content to yes` e `// Set content to no`.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## Ottieni lo stato di consenso corrente

L’estensione per dispositivi mobili Consenso sopprime/termina/consente automaticamente il tracciamento in base al valore di consenso corrente. Puoi anche accedere autonomamente allo stato di consenso corrente:

>[!BEGINTABS]

>[!TAB iOS]

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti di Xcode.

   Aggiungere il codice seguente alla funzione `getConsents`:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** nel Navigatore progetti di Xcode.

   Aggiungere il codice seguente al modificatore `.task`:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Nell’esempio precedente, stai semplicemente registrando lo stato del consenso nella console in Xcode. In uno scenario reale, è possibile utilizzarlo per modificare i menu o le opzioni visualizzati all&#39;utente.

>[!TAB Android]

1. Passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL modelli]** > **[!UICONTROL MobileSDK]** nel navigatore di Android Studio.

   Aggiungere il codice seguente alla funzione `getConsents()`:

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Passa a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL visualizzazioni]** > **[!UICONTROL HomeView.kt]** nel navigatore di Android Studio.

   Aggiungi il seguente codice a `LaunchedEffect(unit)`:

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Nell’esempio precedente, stai semplicemente registrando lo stato di consenso nella console in Android Studio. In uno scenario reale, è possibile utilizzarlo per modificare i menu o le opzioni visualizzati all&#39;utente.

>[!ENDTABS]

## Convalidare con Assurance

1. Elimina l’applicazione dal dispositivo o simulatore per reimpostare e inizializzare correttamente il tracciamento e il consenso.
1. Per collegare il simulatore o il dispositivo ad Assurance, consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session).
1. Quando si passa nell&#39;app dalla schermata **[!UICONTROL Home]** alla schermata **[!UICONTROL Products]** e si torna alla schermata **[!UICONTROL Home]**, nell&#39;interfaccia utente di Assurance dovrebbe essere visualizzato un evento **[!UICONTROL Get Consents Response]**.
   ![convalida consenso](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>Ora hai abilitato l’app per richiedere all’utente, al suo avvio iniziale dopo l’installazione (o la reinstallazione), di acconsentire all’utilizzo di Adobe Experience Platform Mobile SDK.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=it)

Successivo: **[Raccolta dei dati del ciclo di vita](lifecycle-data.md)**

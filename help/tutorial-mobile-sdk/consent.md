---
title: Implementare il consenso per le implementazioni dell’SDK di Platform Mobile
description: Scopri come implementare il consenso in un’app mobile.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Implementare il consenso

Scopri come implementare il consenso in un’app mobile.

L’estensione per dispositivi mobili Adobe Experience Platform Consent abilita la raccolta delle preferenze di consenso dalla tua app mobile quando utilizzi l’SDK di Adobe Experience Platform Mobile e l’estensione di Edge Network. Ulteriori informazioni sull&#39;[estensione del consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) sono disponibili nella documentazione.

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

1. Desideri chiedere all’utente il consenso solo una volta. Per farlo, combina il consenso Mobile SDK con l&#39;autorizzazione necessaria per il tracciamento tramite il [framework per la trasparenza del tracciamento delle app](https://developer.apple.com/documentation/apptrackingtransparency) di Apple. In questa app, si presume che quando l’utente autorizza il tracciamento, acconsente alla raccolta di eventi.

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode.

   Aggiungere il codice alla funzione `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisclaimerView]** nel Navigatore progetti di Xcode, che è la visualizzazione visualizzata dopo l&#39;installazione o la reinstallazione dell&#39;applicazione e il primo avvio dell&#39;app. All&#39;utente viene richiesto di autorizzare il tracciamento in base al [framework per la trasparenza del tracciamento delle app](https://developer.apple.com/documentation/apptrackingtransparency) di Apple. Se l’utente autorizza, aggiorna anche il consenso.

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

## Ottieni lo stato di consenso corrente

L’estensione per dispositivi mobili Consenso sopprime/termina/consente automaticamente il tracciamento in base al valore di consenso corrente. Puoi anche accedere autonomamente allo stato di consenso corrente:

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

## Convalidare con Assurance

1. Elimina l’applicazione dal dispositivo o simulatore per reimpostare e inizializzare correttamente il tracciamento e il consenso.
1. Per collegare il simulatore o il dispositivo ad Assurance, consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session).
1. Quando si passa nell&#39;app dalla schermata **[!UICONTROL Home]** alla schermata **[!UICONTROL Products]** e si torna alla schermata **[!UICONTROL Home]**, nell&#39;interfaccia utente di Assurance dovrebbe essere visualizzato un evento **[!UICONTROL Get Consents Response]**.
   ![convalida consenso](assets/consent-update.png)


>[!SUCCESS]
>
>Ora hai abilitato l’app per richiedere all’utente il consenso all’utilizzo dell’SDK di Adobe Experience Platform Mobile al suo avvio iniziale dopo l’installazione (o reinstallazione).
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Raccolta dei dati del ciclo di vita](lifecycle-data.md)**

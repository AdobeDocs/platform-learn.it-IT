---
title: Implementare il consenso per le implementazioni dell’SDK di Platform Mobile
description: Scopri come implementare il consenso in un’app mobile.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Implementare il consenso

Scopri come implementare il consenso in un’app mobile.

L’estensione per dispositivi mobili Adobe Experience Platform Consent abilita la raccolta delle preferenze di consenso dalla tua app mobile quando utilizzi l’SDK di Adobe Experience Platform Mobile e l’estensione Edge Network. Ulteriori informazioni su [Estensione del consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) nella documentazione di.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Richiedere il consenso all&#39;utente.
* Aggiorna l&#39;estensione in base alla risposta dell&#39;utente.
* Scopri come ottenere lo stato di consenso corrente.

## Richiedi consenso

Se hai seguito l’esercitazione fin dall’inizio, ricorda di aver impostato il consenso predefinito nell’estensione Consenso su **[!UICONTROL In sospeso: mette in coda eventi che si verificano prima che l’utente fornisca le preferenze di consenso.]**

Per iniziare a raccogliere i dati, devi ottenere il consenso dell’utente. In un’app reale, vorresti consultare le best practice sul consenso per la tua regione. In questa esercitazione, ottieni il consenso dell’utente semplicemente richiedendolo con un avviso:

1. Desideri chiedere all’utente il consenso solo una volta. Per farlo, combina il consenso Mobile SDK con l’autorizzazione necessaria per il tracciamento tramite Apple [Framework trasparenza tracciamento app](https://developer.apple.com/documentation/apptrackingtransparency). In questa app, si presume che quando l’utente autorizza il tracciamento, acconsente alla raccolta di eventi.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode.

   Aggiungi questo codice al `updateConsent` funzione.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL Visualizzazione disclaimer]** nel Navigatore progetti di Xcode, che è la visualizzazione mostrata dopo l’installazione o la reinstallazione dell’applicazione e il primo avvio dell’app. All’utente viene richiesto di autorizzare il tracciamento in base ai requisiti di Apple [Framework trasparenza tracciamento app](https://developer.apple.com/documentation/apptrackingtransparency). Se l’utente autorizza, aggiorna anche il consenso.

   Aggiungi il seguente codice al `ATTrackingManager.requestTrackingAuthorization { status in` chiusura.

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

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti di Xcode.

   Aggiungi il seguente codice al `getConsents` funzione:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** nel Navigatore progetti di Xcode.

   Aggiungi il seguente codice al `.task` modificatore:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Nell’esempio precedente, stai semplicemente registrando lo stato del consenso nella console in Xcode. In uno scenario reale, è possibile utilizzarlo per modificare i menu o le opzioni visualizzati all&#39;utente.

## Convalida con garanzia

1. Elimina l’applicazione dal dispositivo o simulatore per reimpostare e inizializzare correttamente il tracciamento e il consenso.
1. Per collegare il simulatore o il dispositivo a Assurance, controlla [istruzioni di configurazione](assurance.md#connecting-to-a-session) sezione.
1. Quando si sposta nell’app da **[!UICONTROL Home]** screen to **[!UICONTROL Prodotti]** schermata e torna a **[!UICONTROL Home]** schermo, dovresti vedere un **[!UICONTROL Ottieni risposta consenso]** nell’interfaccia utente Assurance.
   ![convalida consenso](assets/consent-update.png)


>[!SUCCESS]
>
>Ora hai abilitato l’app per richiedere all’utente il consenso all’utilizzo dell’SDK di Adobe Experience Platform Mobile al suo avvio iniziale dopo l’installazione (o reinstallazione).
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Raccogliere dati del ciclo di vita](lifecycle-data.md)**

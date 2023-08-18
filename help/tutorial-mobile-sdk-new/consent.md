---
title: Consenso
description: Scopri come implementare il consenso in un’app mobile.
feature: Mobile SDK,Consent
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# Consenso

Scopri come implementare il consenso in un’app mobile.

L’estensione per dispositivi mobili Adobe Experience Platform Consent abilita la raccolta delle preferenze di consenso dalla tua app mobile quando utilizzi l’SDK di Adobe Experience Platform Mobile e l’estensione Edge Network. Ulteriori informazioni su [Estensione del consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), nella documentazione di.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Richiedere il consenso all&#39;utente.
* Aggiorna l&#39;estensione in base alla risposta dell&#39;utente.
* Scopri come ottenere lo stato di consenso corrente.

## Richiedi consenso

Se hai seguito l’esercitazione fin dall’inizio, ricorda di aver impostato il consenso predefinito nell’estensione Consenso su **[!UICONTROL In sospeso: mette in coda eventi che si verificano prima che l’utente fornisca le preferenze di consenso.]**

Per iniziare a raccogliere i dati, devi ottenere il consenso dell’utente. In questa esercitazione, ottieni il consenso dell’utente semplicemente richiedendolo con un avviso. In un’app reale, vorresti consultare le best practice sul consenso per la tua area geografica.

1. Si desidera chiedere all&#39;utente una sola volta. Pertanto, vuoi combinare il consenso Mobile SDK con le autorizzazioni necessarie per il tracciamento tramite Apple [Framework trasparenza tracciamento app](https://developer.apple.com/documentation/apptrackingtransparency). In questa app, si presuppone che quando l’utente autorizza il tracciamento, l’utente acconsenta anche alla raccolta degli eventi.

1. Accedi a `MobileSDK`, struttura statica generica in cui tutte le chiamate API all’SDK di Adobe Experience Platform sono incluse per un facile riutilizzo.

   Aggiungi questo codice al `updateConsent` funzione.

   ```swift
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accedi a `DisclaimerView.swift`, che è la visualizzazione mostrata dopo l’installazione o la reinstallazione dell’applicazione e il primo avvio dell’app. All’utente viene richiesto di autorizzare il tracciamento in base ai requisiti di Apple [Framework trasparenza tracciamento app](https://developer.apple.com/documentation/apptrackingtransparency). Se l’utente autorizza, aggiorna anche il consenso.

   Aggiungi il seguente codice al `ATTrackingManager.requestTrackingAuthorization { status in` chiusura.

   ```swift {highlight="3,6"}
   if status == .authorized {
       // Set consent to yes
       MobileSDK.shared.updateConsent(value: "y")
   }
   else {
       MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Ottieni lo stato di consenso corrente

L’estensione per dispositivi mobili Consenso sopprime/termina/consente automaticamente il tracciamento in base al valore di consenso corrente. Puoi anche accedere autonomamente allo stato di consenso corrente:

1. Passa a `MobileSDK.swift`.

   Aggiungi il seguente codice al `getConsents` funzione:

   ```swift
   Consent.getConsents { consents, error in
            guard error == nil, let consents = consents else { return }
            guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
            guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
            Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
        }
   ```

2. Accedi a **[!UICONTROL HomeView]**.

   Aggiungi il seguente codice evidenziato al `.task` modificatore:

   ```swift {highlight="3"}
   .task {
        // Ask status of consents
        MobileSDK.shared.getConsents()   
   }
   ```

Nell’esempio precedente, stai semplicemente registrando lo stato del consenso nella console in Xcode. In uno scenario reale, è possibile utilizzarlo per modificare i menu o le opzioni visualizzati all&#39;utente.

## Convalida con garanzia

1. Rivedi [Assurance](assurance.md) lezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Se hai aggiunto correttamente il codice precedente, ti viene richiesto di fornire il consenso.

   Seleziona **[!UICONTROL Continua...]** e quindi seleziona **[!UICONTROL Consenti]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Dovresti vedere un **[!UICONTROL Ottieni risposta consenso]** nell’interfaccia utente Assurance.
   ![convalida consenso](assets/consent-update.png)



>[!SUCCESS]
>
>Ora hai abilitato l’app per richiedere all’utente il consenso all’utilizzo dell’SDK di Adobe Experience Platform Mobile al suo avvio iniziale dopo l’installazione (o reinstallazione).<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Raccogliere dati del ciclo di vita](lifecycle-data.md)**

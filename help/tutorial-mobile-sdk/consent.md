---
title: Consenso
description: Scopri come implementare il consenso in un’app mobile.
feature: Mobile SDK,Consent
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 7%

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

Se hai seguito il tutorial dall’inizio, ti ricorderai di aver impostato **[!UICONTROL Livello di consenso predefinito]** su &quot;In sospeso&quot;. Per iniziare a raccogliere i dati, devi ottenere il consenso dell’utente. In questa esercitazione, ottieni il consenso semplicemente chiedendo con un avviso, in un’app reale che vorresti consultare le best practice per il consenso per la tua regione.

1. Si desidera chiedere all&#39;utente una sola volta. Un modo semplice per gestirlo è utilizzare semplicemente `UserDefaults`.
1. Passa a `Home.swift`.
1. Aggiungi il codice seguente a `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Se l’utente non ha visto l’avviso prima, visualizzalo e aggiorna il consenso in base alla risposta. Aggiungi il codice seguente a `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## Ottieni lo stato di consenso corrente

L’estensione per dispositivi mobili Consenso eliminerà/sospenderà/consentirà automaticamente il tracciamento in base al valore di consenso corrente. Puoi anche accedere autonomamente allo stato di consenso corrente:

1. Passa a `Home.swift`.
1. Aggiungi il codice seguente a `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

Nell’esempio precedente, stai semplicemente stampando lo stato di consenso sulla console. In uno scenario reale, è possibile utilizzarlo per modificare i menu o le opzioni visualizzati all&#39;utente.

## Convalida con garanzia

1. Rivedi [Assurance](assurance.md) lezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato da Assurance.
1. Se hai aggiunto correttamente il codice precedente, ti verrà richiesto di fornire il consenso. Seleziona **Sì**.
   ![finestra a comparsa consenso](assets/mobile-consent-validate.png)
1. Dovresti vedere un **[!UICONTROL Preferenze di consenso aggiornate]** nell’interfaccia utente Assurance.
   ![convalida consenso](assets/mobile-consent-update.png)

Successivo: **[Raccogliere dati del ciclo di vita](lifecycle-data.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
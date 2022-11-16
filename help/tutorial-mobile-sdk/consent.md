---
title: Consenso
description: Scopri come implementare il consenso in un’app mobile.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 7%

---

# Consenso

Scopri come implementare il consenso in un’app mobile.

L’estensione Adobe Experience Platform Consent mobile abilita la raccolta delle preferenze di consenso dalla tua app mobile quando utilizzi Adobe Experience Platform Mobile SDK e l’estensione Edge Network. Ulteriori informazioni sulle [Estensione del consenso](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network), nella documentazione.

## Prerequisiti

* L’app è stata generata ed eseguita correttamente con gli SDK installati e configurati.

## Finalità di apprendimento

In questa lezione:

* Richiedi il consenso all&#39;utente.
* Aggiorna l&#39;estensione in base alla risposta dell&#39;utente.
* Scopri come ottenere lo stato di consenso corrente.

## Chiedi il consenso

Se hai seguito l’esercitazione dall’inizio, ricorda di impostare la **[!UICONTROL Livello di consenso predefinito]** in &quot;In sospeso&quot;. Per iniziare a raccogliere i dati, devi ottenere il consenso dell’utente. In questa esercitazione, ottieni il consenso chiedendo semplicemente un avviso, in un’app reale desideri consultare le best practice per il consenso per la tua area geografica.

1. Vuoi chiedere all&#39;utente solo una volta. Un modo semplice per gestirlo è semplicemente utilizzando `UserDefaults`.
1. Passa a `Home.swift`.
1. Aggiungi il codice seguente a `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Se l’utente non ha mai visualizzato l’avviso prima, visualizzalo e aggiorna il consenso in base alla risposta. Aggiungi il codice seguente a `viewDidLoad()`.

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


## Ottieni stato consenso corrente

L’estensione per dispositivi mobili Consent sopprime/pend/allow automaticamente il tracciamento in base al valore del consenso corrente. Puoi anche accedere personalmente allo stato di consenso corrente:

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

Nell’esempio precedente, stai semplicemente stampando lo stato del consenso sulla console. In uno scenario reale, puoi utilizzarlo per modificare i menu o le opzioni che vengono mostrati all’utente.

## Convalida con affidabilità

1. Consulta la sezione [Affidabilità](assurance.md) lezione.
1. Installa l’app.
1. Avvia l’app utilizzando l’URL generato dall’affidabilità.
1. Se hai aggiunto correttamente il codice di cui sopra, ti verrà richiesto di fornire il consenso. Seleziona **Sì**.
   ![finestra a comparsa del consenso](assets/mobile-consent-validate.png)
1. Dovresti visualizzare un **[!UICONTROL Preferenze di consenso aggiornate]** nell’interfaccia utente di Assurance.
   ![convalidare il consenso](assets/mobile-consent-update.png)

Avanti: **[Raccogliere dati sul ciclo di vita](lifecycle-data.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
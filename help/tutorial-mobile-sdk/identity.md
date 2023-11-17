---
title: Identità
description: Scopri come raccogliere i dati di identità in un’app mobile.
feature: Mobile SDK,Identities
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 4%

---

# Identità

Scopri come raccogliere i dati di identità in un’app mobile.

>[!INFO]
>
> Questo tutorial verrà sostituito da un nuovo tutorial che utilizzerà una nuova app mobile di esempio a fine novembre 2023

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e dei loro comportamenti collegando le identità tra dispositivi e sistemi, consentendo di offrire esperienze digitali personali e di impatto in tempo reale. I campi di identità e gli spazi dei nomi sono l’associazione che unisce diverse origini di dati per creare il profilo cliente in tempo reale a 360 gradi.

Ulteriori informazioni su [Estensione identità](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) e [servizio identità](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) nella documentazione di.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Aggiornare un’identità standard.
* Imposta un’identità personalizzata.
* Aggiornare un’identità personalizzata.
* Convalida il grafico delle identità.
* Ottieni ECID e altre identità.

## Aggiornare un’identità standard

Per prima cosa, aggiorna la mappa delle identità dell’utente al momento dell’accesso.

1. Accedi a `Login.swift` se l’app Luma e trova la funzione denominata `loginButt`.

   Nell’app di esempio Luma non è presente alcuna convalida del nome utente o della password. È sufficiente toccare i pulsanti per accedere.

1. Creare `IdentityMap` e `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. Aggiungi il `IdentityItem` al `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. Chiamata `updateIdentities` per inviare i dati alla rete Edge di Platform.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>Puoi inviare più identità in una singola chiamata updateIdentities. Puoi anche modificare le identità inviate in precedenza.


## Impostare uno spazio dei nomi di identità personalizzato

Gli spazi dei nomi delle identità sono componenti di [Servizio identità](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) che fungono da indicatori del contesto a cui si riferisce un’identità. Ad esempio, distinguono un valore di &quot;name@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.

1. Nell’interfaccia di Data Collection, seleziona **[!UICONTROL Identità]** dalla barra di navigazione a sinistra.
1. Seleziona **[!UICONTROL Crea uno spazio dei nomi delle identità]**.
1. Fornisci un **[!UICONTROL Nome visualizzato]** di `Luma CRM ID` e un **[!UICONTROL Simbolo di identità]** valore di `lumaCrmId`.
1. Seleziona **[!UICONTROL ID multi-dispositivo]**.
1. Seleziona **[!UICONTROL Crea]**.

![crea spazio dei nomi delle identità](assets/mobile-identity-create.png)

## Aggiornare un’identità personalizzata

Dopo aver creato un’identità personalizzata, inizia a raccoglierla modificando la `updateIdentities` codice aggiunto nel passaggio precedente. È sufficiente creare un elemento IdentityItem e aggiungerlo a IdentityMap. Ecco come dovrebbe apparire il blocco di codice completo:

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## Rimuovere un’identità

È possibile utilizzare `removeIdentity` per rimuovere l’identità dalla IdentityMap memorizzata lato client. L’estensione Identity interrompe l’invio dell’identificatore alla rete Edge. L’utilizzo di questa API non rimuove l’identificatore dal grafico dei profili utente o dal grafico delle identità lato server.

Aggiungi quanto segue `removeIdentity` codice per il pulsante logout click in `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>Negli esempi precedenti, `crmId` e `emailAddress` sono codificati, ma in un’app reale i valori sarebbero dinamici.

## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance.
1. Nell’app, seleziona l’icona Account in basso a destra.

   ![account app luma](assets/mobile-identity-login.png)
1. Seleziona la **Accedi** pulsante.
1. Hai la possibilità di inserire un nome utente e una password; entrambi sono opzionali e puoi semplicemente selezionare **Accedi**.

   ![accesso all’app luma](assets/mobile-identity-login-final.png)
1. Cerca nell’interfaccia web di Assurance per `Edge Identity Update Identities` evento da `com.adobe.griffon.mobile` fornitore.
1. Seleziona l’evento e rivedi i dati in `ACPExtensionEventData` oggetto. Dovresti visualizzare le identità aggiornate.
   ![convalida aggiornamento identità](assets/mobile-identity-validate-assurance.png)

## Convalida con grafico delle identità

Una volta completati i passaggi in [lezione di Experience Platform](platform.md), potrai anche confermare l’acquisizione dell’identità nel visualizzatore del grafico dell’identità di Platform:

![convalida grafo identità](assets/mobile-identity-validate.png)


Successivo: **[Profilo](profile.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
---
title: Raccogliere dati di identità
description: Scopri come raccogliere i dati di identità in un’app mobile.
feature: Mobile SDK,Identities
hide: true
exl-id: e6ec9a4f-3163-47fd-8d5c-6e640af3b4ba
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 5%

---

# Raccogliere dati di identità

Scopri come raccogliere i dati di identità in un’app mobile.

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e dei loro comportamenti collegando le identità tra dispositivi e sistemi, consentendo di offrire esperienze digitali personali e di impatto in tempo reale. I campi di identità e gli spazi dei nomi sono l’associazione che unisce diverse origini di dati per creare il profilo cliente in tempo reale a 360 gradi.

Ulteriori informazioni su [Estensione identità](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) e [servizio identità](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) nella documentazione di.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Imposta uno spazio dei nomi di identità personalizzato.
* Aggiornare le identità.
* Convalida il grafico delle identità.
* Ottieni ECID e altre identità.


## Impostare uno spazio dei nomi di identità personalizzato

Gli spazi dei nomi delle identità sono componenti di [Servizio identità](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) che fungono da indicatori del contesto a cui si riferisce un’identità. Ad esempio, distinguono un valore di `name@email.com` come indirizzo e-mail o `443522` come ID CRM numerico.

>[!NOTE]
>
>Quando l’app viene installata, l’SDK di Mobile genera un’identità univoca nel proprio spazio dei nomi, denominata ID Experience Cloud (ECID). Questo ECID viene memorizzato nella memoria persistente del dispositivo mobile e inviato con ogni hit. L’ECID viene rimosso quando l’utente disinstalla l’app o quando imposta lo stato di privacy globale dell’SDK di Mobile in modo che la rinuncia venga negata. Nell’app Luma di esempio, devi rimuovere e reinstallare l’app per creare un nuovo profilo con il proprio ECID univoco.


Per creare un nuovo spazio dei nomi dell’identità:

1. Nell’interfaccia di Data Collection, seleziona **[!UICONTROL Identità]** dalla barra di navigazione a sinistra.
1. Seleziona **[!UICONTROL Crea uno spazio dei nomi delle identità]**.
1. Fornisci un **[!UICONTROL Nome visualizzato]** di `Luma CRM ID` e un **[!UICONTROL Simbolo di identità]** valore di `lumaCRMId`.
1. Seleziona **[!UICONTROL ID multi-dispositivo]**.
1. Seleziona **[!UICONTROL Crea]**.

   ![crea spazio dei nomi delle identità](assets/identity-create.png)




## Aggiorna identità

Desideri aggiornare sia l’identità standard (e-mail) che quella personalizzata (ID CRM Luma) quando l’utente accede all’app.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode e trovare il `func updateIdentities(emailAddress: String, crmId: String)` implementazione di funzioni. Aggiungi il codice seguente alla funzione.

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
   ```

   Questo codice:

   1. Crea un elemento vuoto `IdentityMap` oggetto.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configura `IdentityItem` oggetti per e-mail e ID CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Aggiunge questi `IdentityItem` oggetti al `IdentityMap` oggetto.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Invia il `IdentityItem` oggetto come parte del `Identity.updateIdentities` Chiamata API alla rete Edge.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL FoglioAccesso]** nel Navigatore progetti Xcode e trova il codice da eseguire quando selezioni il **[!UICONTROL Login]** pulsante. Aggiungi il seguente codice:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Puoi inviare più identità in un singolo `updateIdentities` chiamare. Puoi anche modificare le identità inviate in precedenza.


## Rimuovere un’identità

È possibile utilizzare [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) API per rimuovere l&#39;identità dalla mappa di identità lato client memorizzata. L’estensione Identity interrompe l’invio dell’identificatore alla rete Edge. L’utilizzo di questa API non rimuove l’identificatore dal grafico delle identità lato server. Consulta [Visualizzare i grafici delle identità](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) per ulteriori informazioni sui grafici delle identità.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigator del progetto Xcode e aggiungi il seguente codice al `func removeIdentities(emailAddress: String, crmId: String)` funzione:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL FoglioAccesso]** nel Navigatore progetti Xcode e trova il codice da eseguire quando selezioni il **[!UICONTROL Disconnetti]** pulsante. Aggiungi il seguente codice:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Nell’app Luma
   1. Seleziona la **[!UICONTROL Home]** e spostare l&#39;icona Assurance a sinistra.
   1. Seleziona <img src="assets/login.png" width="15" /> in alto a destra.

      <img src="./assets/identity1.png" width="300">

   1. Specifica un indirizzo e-mail e un ID del sistema di gestione delle relazioni con i clienti, oppure
   1. Seleziona <img src="assets/insert.png" width="15" /> per generare in modo casuale un **[!UICONTROL E-mail]** e **[!UICONTROL ID CRM]**.
   1. Seleziona **[!UICONTROL Login]**.

      <img src="./assets/identity2.png" width="300">


1. Cerca nell’interfaccia web Assurance per **[!UICONTROL Identità aggiornamento identità Edge]** evento da **[!UICONTROL com.adobe.griffon.mobile]** fornitore.
1. Seleziona l’evento e rivedi i dati in **[!UICONTROL ACPExtensionEventData]** oggetto. Dovresti visualizzare le identità aggiornate.
   ![convalida aggiornamento identità](assets/identity-validate-assurance.png)

## Convalida con grafico delle identità

Una volta completati i passaggi in [lezione di Experience Platform](platform.md), puoi confermare l’acquisizione delle identità nel visualizzatore del grafico delle identità di Platform:

1. Seleziona **[!UICONTROL Identità]** nell’interfaccia utente di Data Collection.
1. Seleziona **[!UICONTROL Grafico delle identità]** dalla barra superiore.
1. Invio `Luma CRM ID` come **[!UICONTROL Spazio dei nomi dell’identità]** e il tuo ID CRM (ad esempio `24e620e255734d8489820e74f357b5c8`) come **[!UICONTROL Valore identità]**.
1. Vedete la **[!UICONTROL Identità]** in elenco.

   ![convalida grafo identità](assets/identity-validate-graph.png)

>[!INFO]
>
>L’app non contiene codice per reimpostare l’ECID, il che significa che puoi reimpostare l’ECID (e creare effettivamente un nuovo profilo con un nuovo ECID) solo tramite una disinstallazione e una reinstallazione dell’applicazione. Per implementare il ripristino degli identificatori, vedi la sezione [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) e [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) Chiamate API. Tuttavia, quando utilizzi un identificatore di notifica push, tieni presente quanto segue (vedi [Invio di notifiche push](journey-optimizer-push.md)), tale identificatore diventa un altro identificatore di profilo &quot;permanente&quot; sul dispositivo.


>[!SUCCESS]
>
>Ora hai configurato l’app per aggiornare le identità in Edge Network e (se configurata) in Adobe Experience Platform.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Raccogliere dati profilo](profile.md)**

---
title: Raccogliere dati di identità in un’app mobile con Mobile SDK
description: Scopri come raccogliere i dati di identità in un’app mobile.
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Raccogliere dati di identità

Scopri come raccogliere i dati di identità in un’app mobile.

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e dei loro comportamenti collegando le identità tra dispositivi e sistemi, consentendo di offrire esperienze digitali personali e di impatto in tempo reale. I campi di identità e gli spazi dei nomi sono l’associazione che unisce diverse origini di dati per creare il profilo cliente in tempo reale a 360 gradi.

Ulteriori informazioni sull&#39;[estensione Identity](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) e sul [servizio Identity](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) sono disponibili nella documentazione.

## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Imposta uno spazio dei nomi di identità personalizzato.
* Aggiornare le identità.
* Convalida il grafico delle identità.
* Ottieni ECID e altre identità.


## Impostare uno spazio dei nomi di identità personalizzato

Gli spazi dei nomi delle identità sono componenti di [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it) che fungono da indicatori del contesto a cui si riferisce un&#39;identità. Ad esempio, distinguono un valore di `name@email.com` come indirizzo e-mail o `443522` come ID CRM numerico.

>[!NOTE]
>
>Quando l’app viene installata, l’SDK di Mobile genera un’identità univoca nel proprio spazio dei nomi, denominata ID Experience Cloud (ECID). Questo ECID viene memorizzato nella memoria persistente del dispositivo mobile e inviato con ogni hit. L’ECID viene rimosso quando l’utente disinstalla l’app o quando imposta lo stato di privacy globale dell’SDK di Mobile in modo che la rinuncia venga negata. Nell’app Luma di esempio, devi rimuovere e reinstallare l’app per creare un nuovo profilo con il proprio ECID univoco.


Per creare un nuovo spazio dei nomi dell’identità:

1. Nell&#39;interfaccia di Data Collection, seleziona **[!UICONTROL Identità]** dalla navigazione nella barra a sinistra.
1. Seleziona **[!UICONTROL Crea uno spazio dei nomi delle identità]**.
1. Fornisci un **[!UICONTROL Nome visualizzato]** di `Luma CRM ID` e un **[!UICONTROL Valore]** del simbolo di identità`lumaCRMId`.
1. Seleziona **[!UICONTROL ID multi-dispositivo]**.
1. Seleziona **[!UICONTROL Crea]**.

   ![crea spazio dei nomi identità](assets/identity-create.png)




## Aggiorna identità

Desideri aggiornare sia l’identità standard (e-mail) che quella personalizzata (ID CRM Luma) quando l’utente accede all’app.

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore progetti Xcode e trova l&#39;implementazione della funzione `func updateIdentities(emailAddress: String, crmId: String)`. Aggiungi il codice seguente alla funzione.

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

   1. Crea un oggetto `IdentityMap` vuoto.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Imposta `IdentityItem` oggetti per l&#39;ID di posta elettronica e CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Aggiunge questi oggetti `IdentityItem` all&#39;oggetto `IdentityMap`.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Invia l&#39;oggetto `IdentityItem` come parte della chiamata API `Identity.updateIdentities` all&#39;Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** nel navigatore progetti Xcode e trova il codice da eseguire quando selezioni il pulsante **[!UICONTROL Login]**. Aggiungi il seguente codice:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>È possibile inviare più identità in una singola chiamata `updateIdentities`. Puoi anche modificare le identità inviate in precedenza.


## Rimuovere un’identità

È possibile utilizzare l&#39;API [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) per rimuovere l&#39;identità dalla mappa delle identità lato client archiviata. L’estensione Identity non invia più l’identificatore all’Edge Network. L’utilizzo di questa API non rimuove l’identificatore dal grafico delle identità lato server. Per ulteriori informazioni sui grafici delle identità, vedere [Visualizza grafici delle identità](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en).

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore progetti Xcode e aggiungi il seguente codice alla funzione `func removeIdentities(emailAddress: String, crmId: String)`:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** nel Navigator dei progetti Xcode e trova il codice da eseguire quando selezioni il pulsante **[!UICONTROL Logout]**. Aggiungi il seguente codice:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Convalidare con Assurance

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Nell’app Luma
   1. Selezionare la scheda **[!UICONTROL Home]** e spostare l&#39;icona Assurance a sinistra.
   1. Seleziona la Icona <img src="assets/login.png" width="15" /> in alto a destra.

      <img src="./assets/identity1.png" width="300">

   1. Specifica un indirizzo e-mail e un ID del sistema di gestione delle relazioni con i clienti, oppure
   1. Seleziona <img src="assets/insert.png" width="15" /> per generare in modo casuale **[!UICONTROL E-mail]** e **[!UICONTROL ID CRM]**.
   1. Seleziona **[!UICONTROL Accesso]**.

      <img src="./assets/identity2.png" width="300">


1. Cerca nell&#39;interfaccia Web Assurance l&#39;evento **[!UICONTROL Identità aggiornamento identità di Edge]** dal fornitore **[!UICONTROL com.adobe.griffon.mobile]**.
1. Selezionare l&#39;evento e rivedere i dati nell&#39;oggetto **[!UICONTROL ACPExtensionEventData]**. Dovresti visualizzare le identità aggiornate.
   ![convalida aggiornamento identità](assets/identity-validate-assurance.png)

## Convalida con grafico delle identità

Dopo aver completato i passaggi della [lezione di Experience Platform](platform.md), puoi confermare l&#39;acquisizione delle identità nel visualizzatore del grafico delle identità di Platform:

1. Seleziona **[!UICONTROL Identità]** nell&#39;interfaccia utente di Data Collection.
1. Seleziona **[!UICONTROL Grafico identità]** dalla barra superiore.
1. Immetti `Luma CRM ID` come **[!UICONTROL Spazio dei nomi identità]** e l&#39;ID del sistema di gestione delle relazioni con i clienti (ad esempio `24e620e255734d8489820e74f357b5c8`) come **[!UICONTROL Valore identità]**.
1. Sono elencate le **[!UICONTROL identità]**.

   ![convalida grafo identità](assets/identity-validate-graph.png)

>[!INFO]
>
>L’app non contiene codice per reimpostare l’ECID, il che significa che puoi reimpostare l’ECID (e creare effettivamente un nuovo profilo con un nuovo ECID) solo tramite una disinstallazione e una reinstallazione dell’applicazione. Per implementare il ripristino degli identificatori, vedere le chiamate API [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) e [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities). Tieni presente, tuttavia, che quando utilizzi un identificatore di notifica push (vedi [Invio di notifiche push](journey-optimizer-push.md)), tale identificatore diventa un altro identificatore di profilo &quot;permanente&quot; sul dispositivo.


>[!SUCCESS]
>
>Ora hai configurato l’app per aggiornare le identità nell’Edge Network e (se configurata) con Adobe Experience Platform.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Raccolta dati profilo](profile.md)**

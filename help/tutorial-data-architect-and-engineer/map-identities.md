---
title: Mappare le identità
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Mappare le identità
description: In questa lezione, creeremo spazi dei nomi di identità e aggiungeremo campi di identità ai nostri schemi.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 73645b8b088cfdfe6f256c187b3c510dcc2386fc
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 6%

---

# Mappare le identità

<!-- 30 min-->

In questa lezione, creeremo spazi dei nomi di identità e aggiungeremo campi di identità ai nostri schemi. In seguito, saremo anche in grado di completare le relazioni tra schemi della lezione precedente.

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e dei loro comportamenti collegando le identità tra dispositivi e sistemi, consentendo di offrire esperienze digitali personali e di impatto in tempo reale. I campi di identità e gli spazi dei nomi sono l’associazione che unisce diverse origini di dati per creare il profilo cliente in tempo reale a 360 gradi.

**Gli architetti di dati** dovranno mappare le identità all&#39;esterno di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sull’identità in Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/3422773?learn=on&enablevpops&captions=ita)

>[!NOTE]
>
>I campi di identità sono necessari solo se si creano profili cliente in tempo reale. Non sono necessarie se si acquisiscono solo dati nel data lake.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Autorizzazioni richieste

Nella lezione [Configurare le autorizzazioni](configure-permissions.md) è possibile impostare tutti i controlli di accesso necessari per completare la lezione.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Crea spazio dei nomi identità

In questo esercizio creeremo spazi dei nomi di identità per i campi di identità personalizzati di Luma, `loyaltyId`, `crmId` e `productSku`. Gli spazi dei nomi delle identità svolgono un ruolo fondamentale nella creazione di profili cliente in tempo reale, in quanto due valori corrispondenti nello stesso spazio dei nomi consentono a due origini di dati di formare un grafo identità.


### Creare spazi dei nomi nell’interfaccia utente

Iniziamo creando uno spazio dei nomi per lo schema Fedeltà Luma:

1. Nell&#39;interfaccia utente di Platform, vai a **[!UICONTROL Identità]** nell&#39;area di navigazione a sinistra
1. Sono disponibili diversi spazi dei nomi di identità predefiniti. Seleziona il pulsante **[!UICONTROL Crea spazio dei nomi identità]**
1. Fornisci i dettagli come segue

   | Campo | Valore |
   |---------------|-----------|
   | Nome visualizzato | ID fedeltà Luma |
   | Simbolo di identità | lumaLoyaltyId |
   | Tipo | Cross-Device |

1. Seleziona **[!UICONTROL Crea]**

   ![Creare spazi dei nomi](assets/identity-createNamespace.png)

Ora imposta un altro spazio dei nomi per lo schema del catalogo prodotti Luma con i seguenti dettagli:

| Campo | Valore |
|---------------|-----------|
| Nome visualizzato | SKU prodotto Luma |
| Simbolo di identità | lumaProductSKU |
| Tipo | Identificatore non di persone |



## Creare lo spazio dei nomi dell’identità tramite API

Creeremo il nostro spazio dei nomi CRM tramite API.

>[!NOTE]
>
>Se preferisci saltare gli esercizi API, puoi creare lo spazio dei nomi CRM tramite il metodo di interfaccia utente utilizzato con i seguenti dettagli:
>
> 1. Come **[!UICONTROL Nome visualizzato]**, utilizza `Luma CRM Id`
> 1. Come **[!UICONTROL simbolo di identità]**, utilizza `lumaCrmId`
> 1. Come **[!UICONTROL Tipo]**, utilizza Cross-Device

Creiamo lo spazio dei nomi dell&#39;identità `Luma CRM Id`:

1. Scarica [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) nella cartella `Luma Tutorial Assets`
1. Importa la raccolta in [!DNL Postman]
1. Se non disponi di un token di accesso, apri la richiesta **[!DNL OAuth: Request Access Token]** e seleziona **Invia** per richiedere un nuovo token di accesso.
1. Seleziona la richiesta **[!UICONTROL Identity Service] > [!UICONTROL Identity Namespace] > [!UICONTROL Crea un nuovo spazio dei nomi delle identità].**
1. Incolla quanto segue come [!DNL Body] della richiesta:

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Premi il pulsante **Invia** e dovresti ricevere una risposta di **200 OK**:

   ![Spazio dei nomi identità](assets/identity-createUsingApi.png)

Se torni all’interfaccia utente, ora dovresti visualizzare i tre nuovi spazi dei nomi personalizzati:
![Spazio dei nomi identità ](assets/identity-newIdentities.png)


## Etichettare i campi di identità negli schemi

Ora che disponiamo dei nostri namespace, il passaggio successivo è aggiornare gli schemi per etichettare i campi di identità.


### Etichettare i campi XDM per l’identità primaria

Ogni schema utilizzato con Real-Time Customer Profile deve disporre di un’identità primaria specificata. E ogni record acquisito deve avere un valore per quel campo.

Aggiungiamo un&#39;identità primaria a `Luma Loyalty Schema`:

1. Apri `Luma Loyalty Schema`
1. Seleziona `Luma Identity profile field group`
1. Seleziona il campo `loyaltyId`
1. Seleziona la casella **[!UICONTROL Identità]**
1. Seleziona anche la casella **[!UICONTROL Identità primaria]**
1. Seleziona lo spazio dei nomi `Luma Loyalty Id` dal menu a discesa **[!UICONTROL Spazi dei nomi identità]**
1. Seleziona **[!UICONTROL Applica]**
1. Seleziona **[!UICONTROL Salva]**

   ![Identità primaria ](assets/identity-loyalty-primary.png)

Ripeti il processo per alcuni degli altri schemi:

1. In `Luma CRM Schema`, etichettare il campo `crmId` come identità primaria utilizzando lo spazio dei nomi `Luma CRM Id`
1. In `Luma Offline Purchase Events Schema`, etichettare il campo `loyaltyId` come identità primaria utilizzando lo spazio dei nomi `Luma Loyalty Id`
1. In `Luma Product Catalog Schema`, etichettare il campo `productSku` come identità primaria utilizzando lo spazio dei nomi `Luma Product SKU`

>[!NOTE]
>
>I dati raccolti con il Web SDK sono un’eccezione alla pratica tipica di etichettare i campi di identità nello schema. Web SDK utilizza Identity Map per etichettare le identità *sul lato dell&#39;implementazione*. Pertanto, determineremo le identità per `Luma Web Events Schema` quando implementeremo Web SDK sul sito Web Luma. In questa lezione successiva, raccoglieremo l’ID visitatore di Experience Cloud (ECID) come ID primario e il crmId come ID secondario.

Con la selezione delle identità primarie da parte nostra, è chiaro come `Luma Loyalty Schema` può connettersi a `Luma Offline Purchase Events Schema` poiché entrambi utilizzano loyaltyId come identificatore. Ma come può il CRM connettersi agli eventi di acquisto offline? Come possiamo collegare i nostri acquisti offline al comportamento online? E come possiamo classificare i prodotti acquistati con il nostro catalogo di prodotti? Utilizzeremo campi di identità e relazioni di schema aggiuntivi.

<!--use a visual-->

### Etichettare i campi XDM per l’identità secondaria

È possibile aggiungere più campi di identità a uno schema. Le identità non primarie sono spesso indicate come identità secondarie. Per collegare gli acquisti offline al comportamento online, aggiungeremo il crmId come identificatore secondario a `Luma Loyalty Schema` e successivamente nei dati degli eventi Web. Aggiorniamo `Luma Loyalty Schema`:

1. Apri `Luma Loyalty Schema`
1. Seleziona `Luma Identity Profile Field group`
1. Seleziona campo `crmId`
1. Seleziona la casella **[!UICONTROL Identità]**
1. Seleziona lo spazio dei nomi `Luma CRM Id` dal menu a discesa **[!UICONTROL Spazi dei nomi identità]**
1. Seleziona **[!UICONTROL Applica]**, quindi seleziona il pulsante **[!UICONTROL Salva]** per salvare le modifiche

   ![Identità secondaria](assets/identity-loyalty-secondaryId.png)

## Completa le relazioni tra schemi

Ora che abbiamo i campi di identità etichettati, possiamo completare la configurazione delle relazioni di schema tra il catalogo dei prodotti Luma e gli schemi dell’evento:

1. Apri `Luma Offline Purchase Events Schema`
1. Seleziona gruppo di campi **[!UICONTROL Dettagli Commerce]**
1. Seleziona il campo **[!UICONTROL productListItems]** > **[!UICONTROL SKU]**
1. Seleziona la casella **[!UICONTROL Relazione]**
1. Seleziona `Luma Product Catalog Schema` come **[!UICONTROL Schema di riferimento]**
1. `Luma Product SKU` deve essere compilato automaticamente come **[!UICONTROL Spazio dei nomi identità di riferimento]**
1. Seleziona **[!UICONTROL Applica]**
1. Seleziona **[!UICONTROL Salva]**

   ![Campo di riferimento](assets/identity-offlinePurchase-relationship.png)

Ripetere questo processo per creare una relazione tra `Luma Web Events Schema` e `Luma Product Catalog Schema`.

Dopo aver definito la relazione, questa viene indicata sia nella sezione **[!UICONTROL Composizione]** che nella sezione **[!UICONTROL Struttura]** dell&#39;editor schema.

![Visualizzazione relazioni nell&#39;editor schema](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Risorse aggiuntive

* [Documentazione del servizio Identity](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it)
* [API del servizio Identity](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Ora che le nostre identità sono attive, possiamo [creare i nostri set di dati](create-datasets.md).

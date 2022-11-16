---
title: Creare uno schema
description: Creare uno schema
exl-id: 0256b358-0c2c-4c59-ab23-5fe0d38880d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Creare uno schema

Come discusso in [Strutturazione dei dati](../structuring-your-data.md), i dati inviati a Adobe Experience Platform devono essere in XDM. In particolare, i dati devono corrispondere a un _schema_. Uno schema è fondamentalmente una descrizione dell’aspetto dei dati. Descrive i nomi dei campi e la loro posizione all’interno dei dati. Descrive inoltre il tipo di valore che ogni campo deve avere (ad esempio, un valore booleano, una stringa con una lunghezza di 12 caratteri, un array di numeri).

Adobe Experience Platform fornisce alcuni blocchi predefiniti noti come gruppi di campi comuni nel settore. Ad esempio, per il settore dei servizi finanziari esistono gruppi di settori per i trasferimenti di saldo e le richieste di prestiti. Per l&#39;industria dei viaggi e dell&#39;ospitalità, ci sono gruppi sul campo per voli e prenotazioni.

È consigliabile utilizzare i gruppi di campi incorporati, laddove possibile, durante la creazione dello schema. Sappiamo anche che potresti aver bisogno di campi specifici per la tua azienda. Per questo motivo, puoi creare gruppi di campi personalizzati da utilizzare all’interno degli schemi creati.

Passiamo ora alla creazione di uno schema per un tipico sito web di e-commerce.

1. Seleziona **[!UICONTROL Schemi]** sotto [!UICONTROL Gestione dati] dal menu a sinistra nell’interfaccia di Adobe Experience Platform.
1. Seleziona **[!UICONTROL Creare uno schema]** nell&#39;angolo in alto a destra, e **[!UICONTROL ExperienceEvent XDM]** dal menu a discesa.

Ora ti trovi nell’area di lavoro del generatore di schemi.
![Vista Schemi](../assets/schemas-view.png)

## Aggiungi gruppi di campi

1. In **[!UICONTROL Gruppi di campi]** sul lato sinistro del **[!UICONTROL Struttura]** area, selezionare **[!UICONTROL + Aggiungi]** link. A questo punto, verrà visualizzato un modale per scegliere i gruppi di campi da aggiungere allo schema.
1. Per prima cosa, selezionare il gruppo di campi denominato **[!UICONTROL ExperienceEvent AEP Web SDK]**. Questo gruppo di campi aggiunge un set di campi che ospita i dati raccolti automaticamente dall’SDK Web di Adobe Experience Platform.
   ![Mixer AEP Web SDK](../assets/aep-web-sdk-mixin.png)
1. Quindi, poiché il sito web per questa esercitazione è un sito web di e-commerce, seleziona il **[!UICONTROL Dettagli Commerce]** gruppo di campi. Questo gruppo di campi ti consente di inviare dati di e-commerce tipici, quali prodotti vengono visualizzati, aggiunti al carrello e acquistati.
1. Seleziona la **[!UICONTROL Aggiungi gruppi di campi]** in alto a destra nella finestra di dialogo.
   ![Mixin dettagli commerciali](../assets/commerce-details-mixin.png)
1. A questo punto, dovresti visualizzare la struttura dello schema.
   ![Schema con mixins](../assets/schema-with-mixins.png)

## Salva lo schema

1. Infine, fornisci un nome e una descrizione a destra della schermata e seleziona **[!UICONTROL Salva]**.
   ![Schema con nome e descrizione](../assets/schema-name-description.png)

Lo schema è stato creato. Quindi, impariamo a creare un set di dati per memorizzare i dati.

Per ulteriori informazioni sulla creazione degli schemi, consulta [Creare schemi](/help/platform/schemas/create-schemas.md).

[Avanti: ](create-a-dataset.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

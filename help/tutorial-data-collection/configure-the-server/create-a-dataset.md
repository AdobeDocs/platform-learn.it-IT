---
title: Creare un set di dati
description: Creare un set di dati
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Creare un set di dati

Oltre a descrivere i dati inviati in Adobe Experience Platform, è necessario un luogo in cui conservare i dati. In Adobe Experience Platform, questi bucket in cui puoi inserire i dati sono denominati set di dati.

>[!NOTE]
>
>I set di dati non sono necessari se utilizzi solo Platform Web SDK per l’invio di dati ad Adobe Analytics, Adobe Target e Adobe Audience Manager o se utilizzi Event Forwarding. Se utilizzi solo l’SDK per web per questi scopi, puoi saltare questa pagina dell’esercitazione.

1. Seleziona **[!UICONTROL Set di dati]** sotto [!UICONTROL Gestione dati] dal menu a sinistra in Adobe Experience Platform.
1. Quindi, seleziona la **[!UICONTROL Creare un set di dati]** nell&#39;angolo in alto a destra.
   ![Visualizzazione set di dati](../assets/datasets-view.png)

## Creare un set di dati da uno schema

1. Da [!UICONTROL Flusso di lavoro] interfaccia, seleziona il primo riquadro, **[!UICONTROL Creare un set di dati dallo schema]**.
1. Cerca il [lo schema creato in precedenza](create-a-schema.md) e selezionalo.
   ![Selezione dello schema](../assets/schema-selection.png)
1. Seleziona **[!UICONTROL Successivo]** e fornire un nome e una descrizione.
   ![Nome e descrizione del set di dati](../assets/dataset-name-description.png)
1. Seleziona **[!UICONTROL Fine]**. Il set di dati è stato creato ed è pronto per ricevere i dati.

Quando inizi a inviare dati in un set di dati, Adobe Experience Platform verifica che i dati che stai tentando di inserire nel set di dati siano conformi allo schema applicato. Se i dati non sono conformi allo schema, vengono rifiutati e non vengono inseriti nel set di dati. Come risultato di questa fase di convalida, i consumatori del set di dati (prodotti di Adobe, terze parti o la tua azienda) possono avere un certo livello di certezza sulla struttura e la pulizia dei dati del set di dati.

Per ulteriori informazioni sulla creazione dei set di dati, consulta [Creare set di dati e acquisire dati](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[Avanti: ](create-a-datastream.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)


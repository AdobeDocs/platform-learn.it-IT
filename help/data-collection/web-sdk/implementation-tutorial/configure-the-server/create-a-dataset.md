---
title: Creare un set di dati
description: Creare un set di dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# Creare un set di dati

Oltre a descrivere i dati che invierai a Adobe Experience Platform, devi disporre di un luogo in cui conservare i dati. In Adobe Experience Platform, questi bucket in cui puoi inserire i dati sono denominati set di dati.

Per creare un set di dati, passa alla [!UICONTROL Set di dati] visualizzazione in Adobe Experience Platform.

![Visualizzazione set di dati](../../../assets/implementation-strategy/datasets-view.png)

Fai clic su [!UICONTROL Creare un set di dati] nell&#39;angolo in alto a destra.

Durante il processo di creazione del set di dati, seleziona [!UICONTROL Creare un set di dati dallo schema] e seleziona [lo schema creato in precedenza](create-a-schema.md).

![Selezione dello schema](../../../assets/implementation-strategy/schema-selection.png)

Fai clic su [!UICONTROL Successivo] e fornire un nome e una descrizione.

![Nome e descrizione del set di dati](../../../assets/implementation-strategy/dataset-name-description.png)

Fai clic su [!UICONTROL Fine]. Il set di dati è stato creato ed è pronto per ricevere i dati.

Quando inizi a inviare dati in un set di dati, Adobe Experience Platform verifica che i dati che stai tentando di inserire nel set di dati siano conformi allo schema applicato. Se i dati non sono conformi allo schema, vengono rifiutati e non vengono inseriti nel set di dati. Come risultato di questa fase di convalida, i consumatori del set di dati (prodotti di Adobe, terze parti o la tua azienda) possono avere un certo livello di certezza sulla struttura e la pulizia dei dati del set di dati.

Per ulteriori informazioni sulla creazione dei set di dati, consulta [Guida all’interfaccia utente dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=it).

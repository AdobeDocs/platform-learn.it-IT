---
title: Creare un set di dati
description: Creare un set di dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# Creare un set di dati

Oltre a descrivere i dati che invierai a Adobe Experience Platform, è necessario specificare una posizione in cui salvare i dati in modo permanente. In Adobe Experience Platform, questi bucket in cui è possibile inserire i dati sono denominati set di dati.

Per creare un set di dati, passa a [!UICONTROL Set di dati] in Adobe Experience Platform.

![Vista Set di dati](../../../assets/implementation-strategy/datasets-view.png)

Clic [!UICONTROL Crea set di dati] in alto a destra.

Durante il processo di creazione del set di dati, seleziona [!UICONTROL Crea set di dati dallo schema] e seleziona [lo schema creato in precedenza](create-a-schema.md).

![Selezione schema](../../../assets/implementation-strategy/schema-selection.png)

Clic [!UICONTROL Successivo] e fornisci un nome e una descrizione.

![Nome e descrizione del set di dati](../../../assets/implementation-strategy/dataset-name-description.png)

Fai clic su [!UICONTROL Fine]. Il set di dati è stato creato ed è pronto per ricevere i dati.

Quando inizi a inviare dati a un set di dati, Adobe Experience Platform verifica che i dati che tenti di inserire nel set di dati siano conformi allo schema applicato. Se i dati non sono conformi allo schema, vengono rifiutati e non vengono inseriti nel set di dati. In seguito a questa fase di convalida, i consumatori del set di dati (prodotti di Adobe, terze parti o la tua società) possono avere un certo livello di certezza riguardo alla struttura e alla pulizia dei dati del set di dati.

Per ulteriori informazioni sulla creazione dei set di dati, consulta [Guida all’interfaccia utente dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=it).

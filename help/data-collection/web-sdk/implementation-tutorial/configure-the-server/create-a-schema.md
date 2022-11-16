---
title: Creare uno schema
description: Creare uno schema
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Creare uno schema

Come discusso in [Strutturazione dei dati](../structuring-your-data.md), i dati inviati a Adobe Experience Platform devono essere in XDM. In particolare, i dati devono corrispondere a un _schema_. Uno schema è fondamentalmente una descrizione dell’aspetto dei dati. Descrive i nomi dei campi e la loro posizione all’interno dei dati. Descrive inoltre il tipo di valore che ogni campo deve avere (ad esempio, un valore booleano, una stringa con una lunghezza di 12 caratteri, un array di numeri).

Adobe Experience Platform fornisce alcuni blocchi predefiniti noti come gruppi di campi comuni nel settore. Ad esempio, per il settore dei servizi finanziari esistono gruppi di settori per i trasferimenti di saldo e le richieste di prestiti. Per l&#39;industria dei viaggi e dell&#39;ospitalità, ci sono gruppi sul campo per voli e prenotazioni.

È consigliabile utilizzare i gruppi di campi incorporati, laddove possibile, durante la creazione dello schema. Sappiamo anche che potresti aver bisogno di campi specifici per la tua azienda. Per questo motivo, puoi creare gruppi di campi personalizzati da utilizzare all’interno degli schemi creati.

Passiamo ora alla creazione di uno schema per un tipico sito web di e-commerce.

Per prima cosa, passa alla [!UICONTROL Schemi] visualizzazione in Adobe Experience Platform.

![Vista Schemi](../../../assets/implementation-strategy/schemas-view.png)

Seleziona [!UICONTROL Creare uno schema] nell&#39;angolo in alto a destra. Viene visualizzato un menu. Seleziona [!UICONTROL ExperienceEvent XDM].

A questo punto, dovrebbe essere visualizzata una finestra di dialogo in cui viene richiesto quali gruppi di campi si desidera aggiungere allo schema. Il primo gruppo di campi da selezionare è il gruppo di campi denominato [!UICONTROL ExperienceEvent AEP Web SDK]. Questo gruppo di campi aggiunge un set di campi che ospita i dati raccolti automaticamente dall’SDK Web di Adobe Experience Platform.

![Mixer AEP Web SDK](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

Poiché il sito web di questa esercitazione è un sito web di e-commerce, è necessario selezionare anche il [!UICONTROL Dettagli Commerce] gruppo di campi. Questo gruppo ti consente di inviare dati di e-commerce tipici come quali prodotti vengono visualizzati, aggiunti al carrello e acquistati.

![Mixin dettagli commerciali](../../../assets/implementation-strategy/commerce-details-mixin.png)

Fai clic sul pulsante [!UICONTROL Aggiungi gruppi di campi] in alto a destra nella finestra di dialogo. A questo punto, dovresti visualizzare la struttura dello schema.

![Schema con mixins](../../../assets/implementation-strategy/schema-with-mixins.png)

I gruppi di campi aggiunti sono elencati a sinistra. Quando si seleziona un gruppo di campi, vengono evidenziati i campi a destra forniti dal gruppo. Esplorare i campi disponibili.

Infine, seleziona [!UICONTROL Schema senza titolo] verso sinistra dello schermo, fornire un nome e una descrizione a destra dello schermo, quindi fare clic su [!UICONTROL Salva].

![Schema con nome e descrizione](../../../assets/implementation-strategy/schema-name-description.png)

Lo schema è stato creato. Quindi, impariamo a creare un set di dati per contenere i tuoi dati.

Per ulteriori informazioni sulla creazione degli schemi, consulta [Creare uno schema (interfaccia utente)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=it).

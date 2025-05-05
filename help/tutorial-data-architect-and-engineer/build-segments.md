---
title: Generare segmenti
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Generare segmenti
description: In questa lezione, creeremo alcuni segmenti basati sui dati del profilo che abbiamo acquisito nelle lezioni precedenti.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# Generare segmenti

<!-- 30 min-->
In questa lezione, creeremo alcuni segmenti basati sui dati del profilo che abbiamo acquisito nelle lezioni precedenti.

Una volta che disponi di Profili cliente in tempo reale, puoi creare segmenti di individui che condividono caratteristiche simili e che potrebbero rispondere in modo simile alle strategie di marketing. I blocchi predefiniti di questi segmenti sono i campi XDM creati in precedenza.

**Gli architetti di dati** dovranno creare segmenti al di fuori di questo tutorial e supportare i colleghi con questa attività.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sulla creazione di segmenti:
>[!VIDEO](https://video.tv.adobe.com/v/36265?learn=on&enablevpops&captions=ita)


## Autorizzazioni richieste

Nella lezione [Configurare le autorizzazioni](configure-permissions.md) è possibile impostare tutti i controlli di accesso necessari per completare la lezione, in particolare:

* Elementi di autorizzazione **[!UICONTROL Gestione profilo]** > **[!UICONTROL Gestione segmenti]**, **[!UICONTROL Visualizzazione segmenti]** e **[!UICONTROL Esporta segmento di pubblico]**
* Autorizzazioni **[!UICONTROL Gestione profili]** > **[!UICONTROL Visualizza profili]** e **[!UICONTROL Gestisci profili]**
* Elemento di autorizzazione **[!UICONTROL Sandbox]** > `Luma Tutorial`
* Accesso utente al profilo di prodotto `Luma Tutorial Platform`
* Accesso con ruolo sviluppatore al profilo di prodotto `Luma Tutorial Platform` (per API)

## Creare un segmento di base

Creiamo un segmento semplice per i clienti del programma fedeltà con uno stato Gold o Platinum

1. Nell&#39;interfaccia utente di Platform, vai a **[!UICONTROL Segmenti]** nell&#39;area di navigazione a sinistra
1. Seleziona il pulsante **[!UICONTROL Crea segmento]**
1. A sinistra del generatore di schemi sono presenti tre schede per Attributi (dati record), Eventi (dati di serie temporali) e Tipi di pubblico
1. Seleziona l’icona a forma di ingranaggio per notare come il generatore di segmenti visualizzi per impostazione predefinita solo i campi con dati e ti consente di modificare il criterio di unione
1. Nella scheda Attributi, passa alla cartella **Profilo individuale XDM > Fedeltà** (puoi anche cercare &quot;Fedeltà&quot;)
1. Trascina e rilascia, `Tier` dal menu dei campi attributo nell’area di lavoro del generatore di segmenti
1. Seleziona `Tier` è uguale a `Gold` o `Platinum`
1. Seleziona **[!UICONTROL Aggiorna stima]** per vedere quanti profili sono idonei per il tuo segmento
1. Come **[!UICONTROL Nome]**, immetti `Luma customers with level Gold or Above`
1. Seleziona **[!UICONTROL Salva]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Creare un segmento dinamico

In questo esercizio creeremo un segmento per i clienti che hanno acquistato lo stesso prodotto due volte entro 30 giorni. I segmenti dinamici ti consentono di ridimensionare la segmentazione utilizzando i campi come variabili.

1. Vai a **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra
1. Seleziona il pulsante **[!UICONTROL Crea segmento]**
1. Seleziona la scheda **[!UICONTROL Eventi]**
1. Filtra l&#39;elenco in `purchases`
1. Trascina il tipo di evento **[!UICONTROL Acquisti]** nell&#39;area di lavoro _due volte_
1. Seleziona l&#39;icona dell&#39;orologio tra i due eventi **[!UICONTROL Acquisti]** e scegli &quot;entro 30 giorni&quot;
1. Conferma che la definizione del segmento a questo punto legge **&quot;Includi il pubblico che ha almeno 1 evento di acquisto e quindi entro 30 giorni ha almeno 1 evento di acquisto&quot;**
   ![Due acquisti entro 30 giorni](assets/segment-twoPurchases.png)
1. Ora modifica il filtro eventi in `sku`
1. Trascina il campo SKU al secondo evento di acquisto
   ![Due acquisti entro 30 giorni con SKU](assets/segment-twoPurchases-addSku.png)
1. Cancellare il filtro eventi
1. Nella sezione **[!UICONTROL Sfoglia variabili]** sono presenti cartelle per i due eventi di acquisto. Fai clic per esplorare **[!UICONTROL Acquisti 1]**\
   ![Due acquisti entro 30 giorni con SKU, sfoglia il primo acquisto](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Espandere nella cartella **[!UICONTROL Elementi elenco prodotti]**, selezionare il campo **[!UICONTROL SKU]** e trascinarlo a destra dell&#39;operando **[!UICONTROL equals]**. Quando passi il cursore sopra l’area, rilasciala nella sezione &quot;Aggiungi per confrontare operandi&quot;
1. Denomina il segmento `Bought same product within 30 days`
1. Conferma che la definizione del pubblico è **&quot;Includi il pubblico che ha almeno 1 evento Acquisti e che entro 30 giorni ha almeno 1 evento Acquisti in cui ((SKU è uguale a Purchases1 SKU))&quot;**
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-boughtSameProduct.png)

## Creare un segmento con più entità

Ricordare come è stata creata la relazione tra `Luma Offline Purchase Events Schema` e `Luma Product Catalog Schema` nelle lezioni precedenti? L’abbiamo fatto in modo da poter utilizzare la relazione nel nostro schema utilizzando la segmentazione con più entità.

Con la funzione di segmentazione avanzata con più entità, puoi creare segmenti utilizzando più classi XDM per estendere gli schemi. Di conseguenza, il generatore di segmenti può accedere a campi aggiuntivi come se fossero nativi per l’archivio dati del profilo

Verrà creato il segmento successivo applicando la relazione creata tra `Luma Product Catalog Schema` e `Luma Offline Purchase Events Schema`.

1. Vai a **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra
1. Seleziona il pulsante **[!UICONTROL Crea segmento]**
1. Seleziona la scheda **[!UICONTROL Eventi]**
1. Filtra l&#39;elenco in `purchases`
1. Trascina il tipo di evento **[!UICONTROL Acquisti]** nell&#39;area di lavoro
1. Seleziona l&#39;elenco a discesa dell&#39;orologio sopra l&#39;evento e scegli **[!UICONTROL negli ultimi 30 giorni]**
1. Filtra l&#39;elenco **[!UICONTROL Eventi]** in `category`, quindi trascina il campo **[!UICONTROL Categoria prodotto]** in **[!UICONTROL Acquisti]**
1. Cambia l&#39;operatore in **[!UICONTROL inizia con]** e immetti `men` nella casella di testo
1. Come **[!UICONTROL Nome]**, immetti `Purchased a Men's product in the last 30 days`
1. Conferma la definizione del pubblico `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-purchasedMens.png)

## Segmentazione in batch e in streaming

Fai clic su **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra e soffermiamoci a esaminare i nostri tre segmenti:

* Due dei nostri segmenti sono segmenti batch e uno è un segmento di streaming.
* Platform utilizza per impostazione predefinita la segmentazione in streaming quando possibile, qualificando il cliente per un segmento non appena soddisfa i criteri. Quando le definizioni dei segmenti sono troppo complesse per lo streaming, vengono automaticamente convertite in batch. In questo caso, i due segmenti vengono automaticamente raggruppati in batch perché l’intervallo di lookback degli eventi di acquisto è superiore a sette giorni. Per un elenco completo e aggiornato delle limitazioni dello streaming, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=it).
* I processi batch vengono eseguiti su una pianificazione giornaliera, che può essere disattivata.

![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-review.png)

## Risorse aggiuntive

* [Documentazione del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=it)
* [Riferimento API servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/)

La segmentazione è più complessa, soprattutto con l’attivazione dei segmenti. Questi argomenti verranno trattati in un&#39;altra esercitazione.

Hai superato tutti gli esercizi! Procedi alla [conclusione](conclusion.md).

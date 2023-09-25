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
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Generare segmenti

<!-- 30 min-->
In questa lezione, creeremo alcuni segmenti basati sui dati del profilo che abbiamo acquisito nelle lezioni precedenti.

Una volta che disponi di Profili cliente in tempo reale, puoi creare segmenti di individui che condividono caratteristiche simili e che potrebbero rispondere in modo simile alle strategie di marketing. I blocchi predefiniti di questi segmenti sono i campi XDM creati in precedenza.

**Architetti di dati** dovrà creare segmenti al di fuori di questo tutorial e supportare i colleghi con questa attività.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sulla creazione di segmenti:
>[!VIDEO](https://video.tv.adobe.com/v/27254?learn=on)


## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari, in particolare:

* Autorizzazioni **[!UICONTROL Gestione profilo]** > **[!UICONTROL Gestire segmenti]**, **[!UICONTROL Visualizzare segmenti]**, e **[!UICONTROL Esporta segmento di pubblico]**
* Autorizzazioni **[!UICONTROL Gestione profilo]** > **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Gestisci profili]**
* Elemento di autorizzazione **[!UICONTROL Sandbox]** > `Luma Tutorial`
* Accesso utente al `Luma Tutorial Platform` profilo prodotto
* Accesso al ruolo Sviluppatore `Luma Tutorial Platform` profilo di prodotto (per API)

## Creare un segmento di base

Creiamo un segmento semplice per i clienti del programma fedeltà con uno stato Gold o Platinum

1. Nell’interfaccia utente di Platform, vai a **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea segmento]** pulsante
1. A sinistra del generatore di schemi sono presenti tre schede per Attributi (dati record), Eventi (dati di serie temporali) e Tipi di pubblico
1. Seleziona l’icona a forma di ingranaggio per notare come il generatore di segmenti visualizzi per impostazione predefinita solo i campi con dati e ti consente di modificare il criterio di unione
1. Nella scheda Attributi, passa a **Profilo individuale XDM > Fedeltà** cartella (puoi anche cercare &quot;fedeltà&quot;)
1. Trascina e rilascia, `Tier` dal menu dei campi attributo all’area di lavoro del generatore di segmenti
1. Seleziona `Tier` è uguale a `Gold` o `Platinum`
1. Seleziona **[!UICONTROL Aggiorna stima]** per vedere quanti profili sono idonei per il segmento
1. Come **[!UICONTROL Nome]**, immetti `Luma customers with level Gold or Above`
1. Seleziona **[!UICONTROL Salva]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Creare un segmento dinamico

In questo esercizio creeremo un segmento per i clienti che hanno acquistato lo stesso prodotto due volte entro 30 giorni. I segmenti dinamici ti consentono di ridimensionare la segmentazione utilizzando i campi come variabili.

1. Vai a **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea segmento]** pulsante
1. Seleziona la **[!UICONTROL Eventi]** scheda
1. Filtra l’elenco in base a `purchases`
1. Trascina **[!UICONTROL Acquisti]** tipo di evento nell’area di lavoro _due orari distinti_
1. Seleziona l’icona dell’orologio tra i due **[!UICONTROL Acquisti]** e scegliere &quot;entro 30 giorni&quot;
1. Conferma che la definizione del segmento a questo punto legga **&quot;Includi il pubblico che ha almeno 1 evento Acquisti e che entro 30 giorni ha almeno 1 evento Acquisti&quot;**
   ![Due acquisti entro 30 giorni](assets/segment-twoPurchases.png)
1. Ora modifica il filtro eventi in `sku`
1. Trascina il campo SKU al secondo evento di acquisto
   ![Due acquisti entro 30 giorni con SKU](assets/segment-twoPurchases-addSku.png)
1. Cancellare il filtro eventi
1. Dovresti vedere nel **[!UICONTROL Sfoglia variabili]** , sono disponibili cartelle per i due eventi di acquisto. Fai clic per esplorare **[!UICONTROL Acquisti 1]**\
   ![Due acquisti entro 30 giorni con SKU, sfoglia il primo acquisto](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Approfondisci in **[!UICONTROL Elementi dell’elenco prodotti]** cartella, seleziona la **[!UICONTROL SKU]** e trascinarlo a destra del **[!UICONTROL è uguale a]** operando. Quando passi il cursore sopra l’area, rilasciala nella sezione &quot;Aggiungi per confrontare operandi&quot;
1. Assegna un nome al segmento `Bought same product within 30 days`
1. Conferma che la definizione del pubblico sia **&quot;Includi il pubblico che ha almeno 1 evento Acquisti e che entro 30 giorni ha almeno 1 evento Acquisti in cui ((SKU è uguale a Purchases1 SKU))&quot;**
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-boughtSameProduct.png)

## Creare un segmento con più entità

Ricorda come abbiamo creato la relazione tra `Luma Offline Purchase Events Schema` e `Luma Product Catalog Schema` nelle lezioni precedenti? L’abbiamo fatto in modo da poter utilizzare la relazione nel nostro schema utilizzando la segmentazione con più entità.

Con la funzione di segmentazione avanzata con più entità, puoi creare segmenti utilizzando più classi XDM per estendere gli schemi. Di conseguenza, il generatore di segmenti può accedere a campi aggiuntivi come se fossero nativi per l’archivio dati del profilo

Creerai il segmento successivo applicando la relazione creata tra `Luma Product Catalog Schema` e il tuo `Luma Offline Purchase Events Schema`.

1. Vai a **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea segmento]** pulsante
1. Seleziona la **[!UICONTROL Eventi]** scheda
1. Filtra l’elenco in base a `purchases`
1. Trascina **[!UICONTROL Acquisti]** tipo di evento nell’area di lavoro
1. Seleziona il menu a discesa dell’orologio sopra l’evento e scegli **[!UICONTROL negli ultimi 30 giorni]**
1. Filtra il **[!UICONTROL Eventi]** elenca a `category` e quindi trascina **[!UICONTROL Categoria di prodotto]** campo su **[!UICONTROL Acquisti]**
1. Modifica l’operatore in **[!UICONTROL inizia con]** e immetti `men` nella casella di testo
1. Come **[!UICONTROL Nome]**, immetti `Purchased a Men's product in the last 30 days`
1. Conferma la definizione del pubblico `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-purchasedMens.png)

## Segmentazione in batch e in streaming

Fai clic su **[!UICONTROL Segmenti]** nella barra di navigazione a sinistra, soffermiamoci a esaminare i nostri tre segmenti:

* Due dei nostri segmenti sono segmenti batch e uno è un segmento di streaming.
* Platform utilizza per impostazione predefinita la segmentazione in streaming quando possibile, qualificando il cliente per un segmento non appena soddisfa i criteri. Quando le definizioni dei segmenti sono troppo complesse per lo streaming, vengono automaticamente convertite in batch. In questo caso, i due segmenti vengono automaticamente raggruppati in batch perché l’intervallo di lookback degli eventi di acquisto è superiore a sette giorni. Per un elenco completo e aggiornato delle limitazioni dello streaming, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* I processi batch vengono eseguiti su una pianificazione giornaliera, che può essere disattivata.

![Ha acquistato lo stesso prodotto negli ultimi 30 giorni](assets/segment-review.png)

## Risorse aggiuntive

* [Documentazione del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=it)
* [Riferimento API del servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/)

La segmentazione è più complessa, soprattutto con l’attivazione dei segmenti. Questi argomenti verranno trattati in un&#39;altra esercitazione.

Hai superato tutti gli esercizi! Passare alla [conclusione](conclusion.md).

---
title: Generare segmenti
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Generare segmenti
description: In questa lezione verranno creati alcuni segmenti in base ai dati di profilo acquisiti nelle lezioni precedenti.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Generare segmenti

<!-- 30 min-->
In questa lezione verranno creati alcuni segmenti in base ai dati di profilo acquisiti nelle lezioni precedenti.

Una volta disponibili i profili cliente in tempo reale, puoi creare segmenti di singoli utenti che condividono caratteristiche simili e possono rispondere in modo simile alle strategie di marketing. Gli elementi di base di questi segmenti sono i campi XDM creati in precedenza.

**Architetti dei dati** dovrà creare segmenti al di fuori di questa esercitazione e supportare i colleghi con questa attività.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sulla creazione dei segmenti:
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## Autorizzazioni necessarie

In [Configurare le autorizzazioni](configure-permissions.md) lezione, è possibile impostare tutti i controlli di accesso necessari per completare la lezione, in particolare:

* Voci di autorizzazione **[!UICONTROL Gestione dei profili]** > **[!UICONTROL Gestire i segmenti]**, **[!UICONTROL Visualizzare i segmenti]** e **[!UICONTROL Esportare il segmento di pubblico]**
* Voci di autorizzazione **[!UICONTROL Gestione dei profili]** > **[!UICONTROL Visualizza profili]** e **[!UICONTROL Gestisci profili]**
* Voce di autorizzazione **[!UICONTROL Sandbox]** > `Luma Tutorial`
* Accesso al ruolo dell&#39;utente `Luma Tutorial Platform` profilo di prodotto
* Accesso ai ruoli sviluppatore per `Luma Tutorial Platform` profilo di prodotto (per API)

## Creare un segmento di base

Creiamo un segmento semplice per i clienti di programmi fedeltà con uno stato Gold o Platinum

1. Nell’interfaccia utente di Platform, passa a **[!UICONTROL Segmenti]** nella navigazione a sinistra
1. Seleziona la **[!UICONTROL Creare un segmento]** pulsante
1. A sinistra del generatore di schemi sono presenti tre schede per Attributi (dati di record), Eventi (dati di serie temporale) e Tipi di pubblico
1. Seleziona l’icona a forma di ingranaggio per notare come il Generatore di segmenti visualizza per impostazione predefinita solo i campi con dati e consente di modificare i criteri di unione
1. Nella scheda Attributi , passa alla **Profilo individuale XDM > Fedeltà** cartella (puoi anche cercare &quot;fedeltà&quot;)
1. Trascina e rilascia, `Tier` dal menu campi attributo all’area di lavoro del generatore di segmenti
1. Seleziona `Tier` è `Gold` o `Platinum`
1. Seleziona **[!UICONTROL Aggiorna stima]** per vedere quanti profili si qualificano per il segmento
1. Come **[!UICONTROL Nome]**, inserisci `Luma customers with level Gold or Above`
1. Seleziona **[!UICONTROL Salva]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Creare un segmento dinamico

In questo esercizio, creeremo un segmento per i clienti che hanno acquistato lo stesso prodotto due volte entro 30 giorni. I segmenti dinamici ti consentono di ridimensionare la segmentazione utilizzando i campi come variabili.

1. Vai a **[!UICONTROL Segmenti]** nella navigazione a sinistra
1. Seleziona la **[!UICONTROL Creare un segmento]** pulsante
1. Seleziona la **[!UICONTROL Eventi]** scheda
1. Filtrare l’elenco in `purchases`
1. Trascina **[!UICONTROL Acquisti]** tipo di evento sull&#39;area di lavoro _due volte diverse_
1. Selezionare l&#39;icona dell&#39;orologio tra i due **[!UICONTROL Acquisti]** eventi e scegli &quot;entro 30 giorni&quot;
1. Conferma la lettura della definizione del segmento a questo punto **&quot;Includi il pubblico che ha almeno 1 evento Purchases e entro 30 giorni ha almeno 1 evento Purchases&quot;**

   ![Due acquisti entro 30 giorni](assets/segment-twoPurchases.png)
1. Ora cambia il filtro eventi in `sku`
1. Trascina il campo SKU al secondo evento di acquisto
   ![Due acquisti entro 30 giorni con SKU](assets/segment-twoPurchases-addSku.png)
1. Ora cancella il filtro eventi
1. Dovresti vedere nella **[!UICONTROL Sfoglia variabili]** sono presenti cartelle per i due eventi di acquisto. Fai clic per esplorare **[!UICONTROL Acquisti 1]**\
   ![Due acquisti entro 30 giorni con SKU, sfoglia il primo acquisto](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Drill giù nella **[!UICONTROL Voci elenco prodotti]** seleziona la cartella **[!UICONTROL SKU]** e trascinarlo a destra del **[!UICONTROL è]** operando. Quando passi il cursore sull’area, rilasciala nella sezione &quot;Aggiungi a confronto operandi&quot;
1. Denomina il segmento `Bought same product within 30 days`
1. Conferma che la definizione del pubblico sia **&quot;Includi il pubblico che ha almeno 1 evento Purchases e entro 30 giorni ha almeno 1 evento Purchases dove (SKU è uguale a Purchases1 SKU)&quot;**
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Acquistato lo stesso prodotto nel segmento degli ultimi 30 giorni](assets/segment-boughtSameProduct.png)

## Creare un segmento con più entità

Ricordare come abbiamo creato la relazione tra `Luma Offline Purchase Events Schema` e `Luma Product Catalog Schema` nelle lezioni precedenti? L’abbiamo fatto in modo da poter utilizzare la relazione nel nostro schema utilizzando la segmentazione su più entità.

Con la funzione avanzata di segmentazione multi-entità, puoi creare segmenti utilizzando più classi XDM per estendere gli schemi. Di conseguenza, il generatore di segmenti può accedere a campi aggiuntivi come se fossero nativi nell’archivio dati del profilo

Puoi creare il segmento successivo applicando la relazione creata tra `Luma Product Catalog Schema` e le `Luma Offline Purchase Events Schema`.

1. Vai a **[!UICONTROL Segmenti]** nella navigazione a sinistra
1. Seleziona la **[!UICONTROL Creare un segmento]** pulsante
1. Seleziona la **[!UICONTROL Eventi]** scheda
1. Filtrare l’elenco in `purchases`
1. Trascina **[!UICONTROL Acquisti]** tipo di evento sull&#39;area di lavoro
1. Seleziona il menu a discesa dell’orologio sopra l’evento e scegli **[!UICONTROL negli ultimi 30 giorni]**
1. Filtrare **[!UICONTROL Eventi]** elenco a `category` e quindi trascinare il **[!UICONTROL Categoria di prodotti]** campo su **[!UICONTROL Acquisti]**
1. Modifica l’operatore in **[!UICONTROL inizia con]** e immetti `men` nella casella di testo
1. Come **[!UICONTROL Nome]**, inserisci `Purchased a Men's product in the last 30 days`
1. Conferma la definizione del pubblico `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Acquistato lo stesso prodotto nel segmento degli ultimi 30 giorni](assets/segment-purchasedMens.png)

## Segmentazione in batch e in streaming

Fai clic su **[!UICONTROL Segmenti]** nella navigazione a sinistra e esaminiamo i nostri tre segmenti:

* Due dei nostri segmenti sono segmenti batch e uno è un segmento in streaming.
* La piattaforma utilizza per impostazione predefinita la segmentazione in streaming quando possibile, qualificando il cliente per un segmento non appena soddisfa i criteri. Quando le definizioni dei segmenti sono troppo complesse per lo streaming, vengono automaticamente convertite in batch. In questo caso, per impostazione predefinita i due segmenti sono in batch perché l’intervallo di look-back degli eventi di acquisto era maggiore di sette giorni. Per un elenco completo e corrente delle limitazioni dello streaming, vedi [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* I processi batch vengono eseguiti su una pianificazione giornaliera, che può essere disattivata.

![Acquistato lo stesso prodotto nel segmento degli ultimi 30 giorni](assets/segment-review.png)

## Risorse aggiuntive

* [Documentazione del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Riferimento API del servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/)

La segmentazione è molto più complessa, soprattutto con l’attivazione dei segmenti. Tali argomenti verranno affrontati in un’altra esercitazione.

L&#39;hai fatto attraverso tutti gli esercizi! Si prega di procedere alla [conclusione](conclusion.md).

---
title: Che cos'è un livello di dati?
description: Che cos'è un livello di dati?
exl-id: a53572c1-1295-4ed4-8a3d-aafff3235138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Che cos&#39;è un livello di dati?

Quando implementi le tecnologie di marketing sul sito, è probabile che tu disponga di importanti dati sparsi nell’interfaccia utente. Ad esempio, il nome di un prodotto potrebbe trovarsi in un&#39;intestazione sulla pagina e il prezzo potrebbe essere inferiore sulla pagina sotto l&#39;immagine del prodotto. Se desideri inviare tali dati ad Adobe o a un altro fornitore, individua gli elementi di HTML che contengono i dati necessari, estrae i dati da tali elementi e inviali. Ma cosa succede quando il team di progettazione decide di spostare il nome del prodotto dall’intestazione a una barra laterale? L’implementazione non funziona. L’implementazione non riesce più a trovare l’intestazione o, peggio, trova l’intestazione e invia dati irrilevanti al server.

Uno degli obiettivi principali di un livello dati è quello di risolvere questo problema. Nel modo più semplice, un livello dati è un oggetto JavaScript o una matrice che contiene i dati sul prodotto nella pagina. Include tutti i dati pertinenti richiesti dalle tecnologie di marketing per raggiungere gli obiettivi. Non affidandoci agli elementi dell’interfaccia utente per fornire questi dati, la nostra implementazione diventa più solida. Il livello dati contiene i dati e deve essere considerato un contratto. Questo contratto si trova in genere tra il team di progettazione, che inserisce dati nel livello dati, e il team di marketing, che recupera dati dal livello dati.

Se un ingegnere sta per modificare la struttura del livello dati, è molto più probabile che prenda in considerazione l’idea di lavorare con il team marketing in modo da poter apportare modifiche appropriate all’implementazione di marketing. Comunicazione e cooperazione _deve_ è stabilito nella tua organizzazione per garantire un’implementazione affidabile.

## Contenitore e contenuto

Nel settore, il termine &quot;livello dati&quot; viene usato un po&#39; liberamente e spesso può portare a confusione e a discomunicazioni. Considerate una scatola di biglie. Sono disponibili due parti: il contenitore (la casella) e il contenuto (le palline). Analogamente, un livello dati è spesso considerato avere due parti: il contenitore (l&#39;oggetto o la matrice JavaScript) e il contenuto (le parti di dati come `priceTotal`, `currencyCode`e `purchaseOrderNumber` ).

Poiché questa esercitazione si riferisce ad Adobe Client Data Layer, si riferisce al contenitore e non al contenuto. Quando si riferisce a XDM, si riferisce al contenuto e non al contenitore . Quando si utilizza Adobe Client Data Layer, non importa se il contenuto è XDM o il proprio modello dati. A Livello dati client di Adobe non interessa. È solo una scatola. Ma... _è_ una scatola con poteri speciali...

## Comunicazione delle modifiche

Quando utilizzi un livello dati, puoi modificare il contenuto in qualsiasi momento. Questa è una bella caratteristica, perché i dati possono diventare disponibili in momenti diversi. Ad esempio, alcuni dati sull’utente potrebbero essere immediatamente disponibili, ma potrebbe essere necessario effettuare una richiesta asincrona a una terza parte per ulteriori informazioni. Ciò richiede un&#39;attenzione particolare. Se ad un certo punto devi inviare questi dati asincroni a Adobe Experience Platform, come possono le tecnologie di marketing sapere quando determinate parti di dati sono state aggiunte al livello dati e sono pronte per essere inviate? È necessario un livello dati più intelligente, un livello dati basato su eventi.

Un livello di dati basato su eventi è in grado di comunicare che il suo contenuto è cambiato in modo che le tecnologie di marketing possano reagire ai cambiamenti. Utilizzato correttamente, questo può aiutare a evitare problemi di temporizzazione che spesso si verificano con i livelli di dati che non hanno mezzi per comunicare quando si verificano modifiche.

Adobe Client Data Layer è un livello dati basato su eventi.

[Avanti: ](how-to-use-the-adobe-client-data-layer.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

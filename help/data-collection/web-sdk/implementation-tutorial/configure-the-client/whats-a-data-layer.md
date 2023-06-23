---
title: Cos'è un livello dati?
description: Cos'è un livello dati?
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Cos&#39;è un livello dati?

Quando implementi tecnologie di marketing sul sito, è probabile che tu abbia parti importanti di dati disperse in tutta l’interfaccia utente. Ad esempio, il nome di un prodotto potrebbe trovarsi in un’intestazione della pagina e il prezzo potrebbe essere inferiore nella pagina sotto l’immagine del prodotto. Se desideri inviare tali dati a Adobe o ad un altro fornitore, puoi certamente trovare gli elementi HTML che contengono i dati cercando tag o attributi HTML specifici, estrarre i dati da tali elementi e inviarli. Ma cosa succede quando il team di progettazione decide di spostare il nome del prodotto dall’intestazione a una barra laterale? Interruzioni dell’implementazione. L’implementazione non riesce più a trovare l’intestazione o, peggio ancora, trova l’intestazione e invia dati irrilevanti al server.

Uno degli obiettivi principali di un livello dati è la risoluzione di questo problema. In parole povere, un livello dati è un oggetto JavaScript (o, come vedremo più avanti, un array) che contiene dati sul prodotto nella pagina o qualsiasi altro dato rilevante su cui le tecnologie di marketing si basano per raggiungere gli obiettivi. Non affidandoci agli elementi dell’interfaccia utente per fornire questi dati, la nostra implementazione diventa più solida. Il livello dati contiene i dati e deve essere considerato un contratto. In genere, questo contratto è stipulato tra il team di progettazione, che inserisce i dati nel livello dati, e il team di marketing, che recupera i dati dal livello dati.

Se un ingegnere sta per modificare la struttura del livello dati, molto più probabilmente prenderà in considerazione la possibilità di lavorare con il team di marketing in modo da poter apportare modifiche appropriate all’implementazione di marketing. La presente comunicazione e cooperazione _deve_ essere stabiliti nella tua organizzazione per garantire una solida implementazione.

## Contenitore e contenuto

Nel settore, il termine &quot;livello dati&quot; viene usato in modo un po’ approssimativo e spesso può portare a confusione e comunicazione errata. Considera una scatola di biglie. Sono disponibili due parti: il contenitore (la casella) e il contenuto (le biglie). Analogamente, un livello dati è spesso considerato come composto da due parti: il contenitore (l’oggetto o l’array JavaScript) e il contenuto (le parti di dati come `priceTotal`, `currencyCode`, e `purchaseOrderNumber` ).

Poiché questa esercitazione fa riferimento al livello dati client di Adobe, si riferisce al contenitore e non al contenuto. Quando si riferisce a XDM, si riferisce al contenuto e non al contenitore. Nel caso di Adobe Client Data Layer, non importa se il contenuto è XDM o il tuo modello di dati. Adobe Client Data Layer non si preoccupa. È solo una scatola. Ma... _è_ una scatola con poteri speciali...

## Comunicazione delle modifiche

Quando utilizzi un livello dati, puoi modificarne il contenuto in qualsiasi momento. Questa è una bella caratteristica, perché i dati possono diventare disponibili in momenti diversi. Ad esempio, alcuni dati sull’utente potrebbero essere immediatamente disponibili, ma potrebbe essere necessario effettuare una richiesta asincrona a terze parti per ottenere ulteriori informazioni. Ciò richiede un&#39;attenzione particolare. Se a un certo punto devi inviare questi dati asincroni a Adobe Experience Platform, in che modo le tecnologie di marketing sanno quando alcuni dati sono stati aggiunti al livello dati e sono pronti per essere inviati? È necessario un livello dati più intelligente, un livello dati basato su eventi.

Un livello dati basato su eventi è in grado di comunicare che il suo contenuto è cambiato, in modo che le tecnologie di marketing possano reagire al cambiamento. Se utilizzato correttamente, questo può aiutare a evitare problemi di temporizzazione che spesso si verificano con i livelli di dati che non dispongono di mezzi per comunicare quando si verificano modifiche.

Adobe Client Data Layer è un livello dati basato su eventi.

---
title: Come utilizzare Adobe Client Data Layer
description: Come utilizzare Adobe Client Data Layer
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Come utilizzare Adobe Client Data Layer

In [Che cos&#39;è un livello di dati?](whats-a-data-layer.md), hai imparato che ci sono due parti da considerare quando si parla dei livelli dati: il contenitore e il contenuto. Il Livello dati client di Adobe è il contenitore . Non importa come lei [strutturare i dati](../structuring-your-data.md) o quali informazioni si sceglie di inserire nei propri dati. I dati possono essere strutturati come [XDM](../structuring-your-data.md#xdm), come mostrano gli esempi seguenti, o puoi creare completamente la tua struttura.

Idealmente, il team di progettazione della tua azienda è responsabile di inserire nel livello dati tutti i dati necessari attraverso il codice on-page. Il team marketing recupera quindi i dati dal livello dati, preferibilmente utilizzando i tag Adobe Experience Platform.

## Invio di dati al livello dati

Adobe Client Data Layer è un array JavaScript. Quando crei l’Adobe Livello dati client, questo viene lasciato vuoto:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Per inserire i dati nel livello dati, chiama il `push` sull&#39;array del livello dati:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Puoi inviare dati aggiuntivi al livello dati in qualsiasi momento chiamando `push` di nuovo.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## Dare un senso ai dati push

Se hai implementato le due precedenti `push` le chiamate, finireste con due voci nella matrice del livello dati. Il livello dati non è particolarmente utile in questo stato. In genere, si desidera accedere allo stato di unione del livello dati o, in altre parole, a un singolo oggetto che è il risultato combinato di tutti i dati inviati al livello dati. Scopriremo come accedere a questo stato unito in seguito nell’esercitazione. Per il momento, è sufficiente capire che lo stato calcolato del livello dati dopo i nostri due `push` le chiamate sono le seguenti:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Rimozione dei dati

A volte è necessario rimuovere parti di dati dal livello dati. Ciò è particolarmente comune nelle applicazioni a pagina singola quando l’utente passa da una visualizzazione all’altra. Ad esempio, se l’utente passa dalla visualizzazione di un prodotto a quella di un contatto, potrebbe essere utile cancellare tutti i dati di prodotto sul livello dati in quanto non sono più pertinenti alla visualizzazione attiva.

È possibile rimuovere una parte di dati premendo un valore di `undefined` per la chiave da rimuovere. Basandosi sugli esempi precedenti, se desideri rimuovere `status` dal livello dati, il codice sarà simile al seguente:

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

Lo stato calcolato del livello dati non includerebbe più `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Invio di eventi al livello dati

Adobe Client Data Layer è utilizzato non solo per memorizzare i dati, ma anche per comunicare quali eventi si verificano sulla pagina. In realtà, in genere i dati vengono inviati al livello dati _come risultato_ di un evento che si verifica sulla pagina. Questi eventi includono (1) eventi di interazione, come l&#39;apertura di una chat bot o la digitazione di un termine di ricerca in una barra di ricerca o (2) eventi di non interazione, come l&#39;impressione di un annuncio o il completamento dei calcoli delle prestazioni della pagina web.

Per comunicare che un evento si è verificato sulla pagina, includi un `event` nell’oggetto inviato al livello dati. Ad esempio, è possibile comunicare che un utente ha inserito una query di ricerca in un campo di ricerca.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Successivamente, scoprirai come attivare le regole all’interno di Adobe Experience Platform Tags quando un particolare evento viene inviato al livello dati. Tieni presente che `event` chiave _not_ incluso nello stato calcolato. Riceve un trattamento speciale dal livello dati.

## Invio di eventi e dati al livello dati

È utile notificare agli ascoltatori che l’utente ha immesso una query di ricerca, ma se si desidera fornire ulteriori informazioni sull’evento? Ad esempio, potrebbe essere utile includere la query di ricerca dell’utente. Puoi fornire questi dati in uno dei due modi seguenti:

1. Fornire i dati in modo che **viene mantenuto** nel livello dati come parte dello stato calcolato del livello dati.
2. Fornire i dati in modo che **non viene conservato** nel livello dati come parte dello stato calcolato del livello dati.

Se desideri mantenere i dati nel livello dati in genere dipende da se intendi fare riferimento a tali dati per tutta la durata dell’utente che si trova sulla pagina. In caso contrario, il mantenimento dei dati all’interno del livello dati potrebbe causare un livello dati disordinato.

Ecco un esempio di invio di un evento con dati aggiuntivi che **viene mantenuto** nel livello dati:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

Dopo `push` ha luogo, `siteKnowledge` viene sempre visualizzato nello stato calcolato del livello dati fino a quando la pagina non viene scaricata (a meno che tu non rimuovi o sovrascrivi intenzionalmente) `siteKnowledge`).

Al contrario, ecco un esempio di invio di un evento con dati aggiuntivi che **non viene conservato** nel livello dati:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

In questo esempio si noti che `siteKnowledge` è avvolto all&#39;interno `eventInfo`. La `eventInfo` key riceve un trattamento speciale dal livello dati. Indica al livello dati che questi dati _dovrebbe_ essere incluso con l&#39;evento che viene inviato ai listener, ma _non_ all’interno del livello dati. Dopo che gli ascoltatori (come Adobe Experience Platform Tags) ricevono una notifica dell’evento, questi dati vengono essenzialmente dimenticati. La `siteKnowledge` key non verrà mai visualizzato all&#39;interno dello stato di calcolo del livello dati.

Ogni volta che chiami `push`, Adobe Client Data Layer notifica tutti i listener. Successivamente, impareremo come ascoltare queste notifiche dai tag Adobe Experience Platform e attivare le regole di conseguenza.

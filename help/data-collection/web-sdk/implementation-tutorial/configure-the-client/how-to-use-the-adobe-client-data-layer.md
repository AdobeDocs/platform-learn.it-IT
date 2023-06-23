---
title: Come utilizzare Adobe Client Data Layer
description: Come utilizzare Adobe Client Data Layer
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Come utilizzare Adobe Client Data Layer

In entrata [Cos&#39;è un livello dati?](whats-a-data-layer.md)Tuttavia, hai imparato che quando si parla dei livelli di dati è necessario considerare due parti: il contenitore e il contenuto. Adobe Client Data Layer è il contenitore. Non importa come [strutturare i dati](../structuring-your-data.md) o quali informazioni inserire nei dati. I dati possono essere strutturati come [XDM](../structuring-your-data.md#xdm), come mostrano gli esempi di seguito, oppure puoi creare una struttura completamente personalizzata.

Idealmente, il team di progettazione della tua azienda è responsabile di inviare tutti i dati necessari al livello di dati tramite il codice su pagina. Il team marketing recupera quindi i dati dal livello dati, preferibilmente utilizzando i tag di Adobe Experience Platform.

## Invio di dati al livello dati

Adobe Client Data Layer è un array JavaScript. Quando crei Adobe Client Data Layer, questo inizia per essere vuoto:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Per inserire dati nel livello dati, chiama il `push` metodo sull’array di livello dati:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Puoi inviare dati aggiuntivi al livello dati in qualsiasi momento richiamando `push` di nuovo.

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

## Rilevamento dei dati inviati

Se hai implementato i due `push` chiamate, alla fine si otterrebbero due voci nell’array di livello dati. Il livello dati non è particolarmente utile in questo stato. In genere, si desidera accedere allo stato unito del livello dati o, in altre parole, a un singolo oggetto che è il risultato combinato di tutti i dati inviati al livello dati. Scopri come accedere a questo stato unito più avanti nell’esercitazione. Per ora, è sufficiente comprendere che lo stato calcolato del livello dati dopo i nostri due `push` le chiamate sarebbero le seguenti:

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

A volte, è necessario rimuovere parti di dati dal livello dati. Ciò è particolarmente comune nelle applicazioni a pagina singola quando l’utente passa da una visualizzazione all’altra. Ad esempio, se l’utente passa da una visualizzazione prodotto a una visualizzazione contatto, potrebbe essere utile cancellare tutti i dati di prodotto sul livello dati, in quanto non sono più pertinenti per la visualizzazione attiva.

Per rimuovere dei dati, premi un valore di `undefined` per la chiave da rimuovere. Basandoti sugli esempi precedenti, se desideri rimuoverli `status` dal livello dati, il codice si presenterà come segue:

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

Lo stato calcolato del livello dati non include più `status`:

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

Adobe Client Data Layer viene utilizzato non solo per memorizzare i dati, ma anche per comunicare quali eventi si verificano sulla pagina. In genere, infatti, i dati vengono inviati al livello dati _come risultato_ di un evento che si verifica sulla pagina. Questi eventi includono (1) eventi di interazione, come l’apertura di un bot di chat o la digitazione di un termine di ricerca in una barra di ricerca oppure (2) eventi di non interazione, come l’impression di un annuncio o il completamento dei calcoli delle prestazioni della pagina web.

Per comunicare che si è verificato un evento sulla pagina, includi un `event` nell’oggetto inviato al livello dati. Ad esempio, è possibile comunicare che un utente ha inserito una query di ricerca in un campo di ricerca.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Successivamente, scoprirai come attivare le regole nei tag Adobe Experience Platform quando un particolare evento viene inviato al livello dati. Si noti inoltre che la `event` la chiave è _non_ incluso nello stato calcolato. Riceve un trattamento speciale dal livello dati.

## Invio di eventi e dati al livello dati

È utile avvisare i listener che l’utente ha inserito una query di ricerca, ma cosa succede se si desidera fornire informazioni aggiuntive sull’evento? Ad esempio, potrebbe essere utile includere la query di ricerca dell’utente. Puoi fornire questi dati in uno dei due modi seguenti:

1. Fornisci dati in modo che **viene conservato** nel livello dati come parte dello stato calcolato del livello dati.
2. Fornisci dati in modo che **non viene conservato** nel livello dati come parte dello stato calcolato del livello dati.

Se desideri conservare i dati nel livello dati in genere dipende dal fatto che intendi fare riferimento a tali dati per tutta la durata della permanenza dell’utente sulla pagina. In caso contrario, la conservazione dei dati all’interno del livello dati potrebbe semplicemente causare un livello dati disordinato.

Ecco un esempio di invio di un evento con dati aggiuntivi che **viene conservato** nel livello dati:

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

Dopo questo `push` ha luogo, `siteKnowledge` viene sempre visualizzato nello stato calcolato del livello dati fino a quando la pagina non viene scaricata (a meno che tu non la rimuova intenzionalmente o non la sostituisca) `siteKnowledge`).

Invece, ecco un esempio di invio di un evento con dati aggiuntivi che **non viene conservato** nel livello dati:

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

Osserva in questo esempio che `siteKnowledge` è avvolto all&#39;interno `eventInfo`. Il `eventInfo` La chiave riceve un trattamento speciale dal livello dati. Indica al livello di dati che questi dati _dovrebbe_ essere incluso nell&#39;evento che viene inviato ai listener, ma _non deve_ essere mantenuti all’interno del livello dati. Dopo che l’evento è stato notificato ai listener (come Adobe Experience Platform Tags), questi dati vengono essenzialmente dimenticati. Il `siteKnowledge` La chiave non verrà mai visualizzata all’interno dello stato calcolato del livello dati.

Ogni volta che chiami `push`, Adobe Client Data Layer invia una notifica a tutti i listener. Successivamente, impareremo ad ascoltare queste notifiche dai tag di Adobe Experience Platform e a attivare le regole di conseguenza.

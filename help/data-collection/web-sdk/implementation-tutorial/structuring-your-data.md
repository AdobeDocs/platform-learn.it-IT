---
title: Strutturazione dei dati
description: Strutturazione dei dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Strutturazione dei dati

Le aziende hanno un proprio linguaggio per comunicare sul proprio dominio. I concessionari di automobili si occupano di marche, modelli e cilindri. Le compagnie aeree si occupano di numeri di volo, classe di servizio e assegnazione di posti. Alcuni di questi termini sono specifici per un&#39;azienda specifica, altri sono condivisi tra un settore verticale e altri sono condivisi da quasi tutte le aziende. Per i termini condivisi in un settore verticale o anche più ampio, puoi iniziare a fare cose potenti con i tuoi dati quando denomini e strutturi questi termini in un modo comune.

Ad esempio, molte aziende gestiscono gli ordini. Cosa succederebbe se queste aziende decidessero collettivamente di modellare un ordine in modo simile? Ad esempio, cosa succede se il modello dati è costituito da un oggetto con un `priceTotal` proprietà che rappresentava il prezzo totale dell’ordine. Cosa succede se l’oggetto aveva anche proprietà denominate `currencyCode` e `purchaseOrderNumber`. È possibile che l&#39;oggetto order contenga una proprietà denominata `payments` si tratta di una matrice di oggetti di pagamento. Ogni oggetto rappresenta un pagamento per l&#39;ordine. Ad esempio, un cliente ha pagato parte dell’ordine con una gift card e il resto con una carta di credito. Puoi iniziare a costruire un modello simile al seguente:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Se tutte le aziende che gestiscono gli ordini decidessero di modellare i dati degli ordini in modo coerente per i termini comuni nel settore, le cose magiche potrebbero iniziare ad accadere. Lo scambio di informazioni all’interno e all’esterno dell’organizzazione può essere più fluido, invece di continuare a interpretare e tradurre i dati (prop ed evar, qualcuno?). L’apprendimento automatico potrebbe capire più facilmente quali sono i tuoi dati _significa_ e fornire informazioni fruibili. Le interfacce utente per la visualizzazione di dati rilevanti potrebbero diventare più intuitive. I dati possono essere integrati direttamente con partner e fornitori che seguono lo stesso modello.

## XDM

Questo è l&#39;obiettivo di Adobe [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM fornisce una modellazione prescrittiva per i dati comune nel settore, consentendo al contempo di estendere il modello in base alle tue esigenze specifiche. Adobe Experience Platform è basato su XDM e, come tale, i dati inviati ad Experience Platform dovranno essere in XDM. Invece di pensare a dove e come trasformare i modelli di dati correnti in XDM prima di inviare i dati ad Experience Platform, considera l’adozione più diffusa di XDM all’interno dell’organizzazione, in modo che la traduzione abbia raramente bisogno di avvenire.

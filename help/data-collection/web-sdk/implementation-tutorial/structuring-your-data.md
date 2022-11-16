---
title: Strutturazione dei dati
description: Strutturazione dei dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Strutturazione dei dati

Le aziende hanno il proprio linguaggio per comunicare il proprio dominio. I concessionari di auto si occupano di marche, modelli e cilindri. Le compagnie aeree si occupano di numeri di volo, classe di servizio e assegnazioni di posti a sedere. Alcuni di questi termini sono unici per una specifica azienda, alcuni sono condivisi tra un settore verticale, altri sono condivisi da quasi tutte le aziende. Per i termini condivisi in un settore verticale o persino più ampio, puoi iniziare a fare cose potenti con i tuoi dati quando definisci e strutturi questi termini in modo comune.

Ad esempio, molte aziende trattano gli ordini. E se collettivamente queste aziende decidessero di modellare un ordine in un modo simile. Ad esempio, cosa succede se il modello dati è costituito da un oggetto con un `priceTotal` proprietà che rappresenta il prezzo totale dell&#39;ordine. Cosa succede se anche quell&#39;oggetto ha proprietà denominate `currencyCode` e `purchaseOrderNumber`. Forse l&#39;oggetto order contiene una proprietà denominata `payments` sarebbe un array di oggetti di pagamento. Ciascun oggetto rappresenterebbe un pagamento per l&#39;ordine. Ad esempio, forse un cliente ha pagato una parte dell&#39;ordine con una carta regalo e ha pagato il resto utilizzando una carta di credito. Potete iniziare a costruire un modello che ha un aspetto simile al seguente:

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

Se tutte le aziende che si occupano di ordini decidessero di modellare i propri dati degli ordini in modo coerente per i termini comuni nel settore, potrebbero iniziare ad accadere cose magiche. Le informazioni potrebbero essere scambiate più fluidamente all&#39;interno e all&#39;esterno della tua organizzazione invece di interpretare e tradurre costantemente i dati (prop e evar, qualcuno?). L&#39;apprendimento automatico potrebbe capire più facilmente i dati _mezzi_ e fornire informazioni utili. Le interfacce utente per la visualizzazione dei dati rilevanti potrebbero diventare più intuitive. I tuoi dati potrebbero essere perfettamente integrati con partner e fornitori che seguono lo stesso modello.

## XDM

Questo è l&#39;obiettivo del Adobe [Modello dati esperienza](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM fornisce modelli prescrittivi per i dati comuni al settore, consentendo al contempo di estendere il modello per le esigenze specifiche. Adobe Experience Platform è basato su XDM e, come tale, i dati inviati in Experience Platform devono essere in XDM. Invece di pensare a dove e come trasformare i modelli di dati correnti in XDM prima di inviare i dati ad Experience Platform, considera l’adozione più diffusa di XDM all’interno dell’organizzazione, in modo che raramente la traduzione debba avvenire.

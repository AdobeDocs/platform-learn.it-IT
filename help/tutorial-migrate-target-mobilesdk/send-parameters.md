---
title: Parametri di invio - Migrazione da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning Mobile
description: Scopri come inviare parametri mbox, di profilo ed entità ad Adobe Target utilizzando Experience Platform Web SDK.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Inviare parametri a Target utilizzando l’estensione Adobe Journey Optimizer - Decisioning Mobile

Le implementazioni di Target differiscono tra i siti web a causa dell’architettura del sito, dei requisiti di business e delle funzionalità utilizzate. La maggior parte delle implementazioni di Target include il passaggio di vari parametri per informazioni contestuali, tipi di pubblico e consigli sui contenuti.

Utilizziamo una semplice pagina dei dettagli del prodotto e una pagina di conferma dell’ordine per dimostrare le differenze tra le estensioni quando si trasmettono i parametri a Target.


| Esempio di parametro at.js | Opzione Platform Web SDK | Note |
| --- | --- | --- |
| `at_property` | N/D | I token di proprietà sono configurati nello stream di dati [1} e non possono essere impostati nella chiamata `sendEvent`.](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) |
| `pageName` | `xdm.web.webPageDetails.name` | Tutti i parametri mbox di Target devono essere passati come parte dell&#39;oggetto `xdm` e devono essere conformi a uno schema utilizzando la classe ExperienceEvent XDM. I parametri mbox non possono essere passati come parte dell&#39;oggetto `data`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Tutti i parametri di profilo di Target devono essere passati come parte dell&#39;oggetto `data` e con prefisso `profile.` per essere mappati in modo appropriato. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parametro riservato utilizzato per la funzionalità Affinità tra categorie di Target che deve essere passata come parte dell&#39;oggetto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OR<br> `xdm.productListItems[0].SKU` | Gli ID entità vengono utilizzati per i contatori comportamentali di Target Recommendations. Questi ID entità possono essere passati come parte dell&#39;oggetto `data` o mappati automaticamente dal primo elemento nell&#39;array `xdm.productListItems` se l&#39;implementazione utilizza tale gruppo di campi. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Gli ID categoria entità possono essere passati come parte dell&#39;oggetto `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | I parametri di entità personalizzati vengono utilizzati per aggiornare il catalogo dei prodotti Recommendations. Questi parametri personalizzati devono essere passati come parte dell&#39;oggetto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Utilizzato per gli algoritmi di consigli basati sul carrello di Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Utilizzato per evitare che ID di entità specifici vengano restituiti in una progettazione di consigli. |
| `mbox3rdPartyId` | Impostato nell&#39;oggetto `xdm.identityMap` | Utilizzato per sincronizzare i profili Target tra dispositivi e Attributi del cliente. Lo spazio dei nomi da utilizzare per l&#39;ID cliente deve essere specificato nella configurazione [Target dello stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Utilizzato per identificare un ordine univoco per il tracciamento delle conversioni di Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Utilizzato per tenere traccia dei totali degli ordini per gli obiettivi di conversione e ottimizzazione di Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OR<br> `xdm.productListItems[0-n].SKU` | Utilizzato per il tracciamento delle conversioni di Target e gli algoritmi di consigli. Per ulteriori informazioni, consulta la sezione [parametri entità](#entity-parameters) di seguito. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Utilizzato per l&#39;obiettivo dell&#39;attività [punteggio personalizzato](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}

## Parametri personalizzati

I parametri mbox personalizzati devono essere passati come XDM o utilizzare l&#39;oggetto dati con il comando `sendEvent`. È importante assicurarsi che lo schema XDM includa tutti i campi necessari per l’implementazione di Target.


## Parametri del profilo

I parametri del profilo di destinazione devono essere trasmessi...

## Parametri di entità

I parametri di entità vengono utilizzati per trasmettere dati comportamentali e informazioni di catalogo supplementari per Target Recommendations. Tutti i [parametri di entità](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) supportati da at.js sono supportati anche da Platform Web SDK. Analogamente ai parametri di profilo, tutti i parametri di entità devono essere passati sotto l&#39;oggetto `data.__adobe.target` nel payload del comando `sendEvent` di Platform Web SDK.

I parametri di entità per un elemento specifico devono avere il prefisso `entity.` per l&#39;acquisizione dei dati corretta. I parametri riservati `cartIds` e `excludedIds` per gli algoritmi dei consigli non devono avere un prefisso e il valore di ciascuno deve contenere un elenco separato da virgole di ID entità.



## Parametri di acquisto

I parametri di acquisto vengono trasmessi in una pagina di conferma dell’ordine dopo che quest’ultimo è stato completato correttamente e vengono utilizzati per gli obiettivi di conversione e ottimizzazione di Target. Con un&#39;implementazione Platform Mobile SDK che utilizza l&#39;estensione Decisioning, questi parametri e vengono mappati automaticamente dai dati XDM passati come parte del gruppo di campi `commerce`.


Le informazioni di acquisto vengono passate a Target quando il gruppo di campi `commerce` ha `purchases.value` impostato su `1`. L&#39;ID ordine e il totale ordine vengono mappati automaticamente dall&#39;oggetto `order`. Se l&#39;array `productListItems` è presente, i valori `SKU` vengono utilizzati per `productPurchasedId`.


## ID cliente (mbox3rdPartyId)

Target consente la sincronizzazione dei profili tra dispositivi e sistemi utilizzando un singolo ID cliente.



Successivamente, scopri come [tenere traccia degli eventi di conversione di Target](track-events.md) con Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).

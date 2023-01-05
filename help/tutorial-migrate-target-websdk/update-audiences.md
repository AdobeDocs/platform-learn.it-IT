---
title: Aggiornare tipi di pubblico e script di profilo | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come aggiornare i tipi di pubblico e gli script di profilo di Adobe Target per garantire la compatibilità con Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# Aggiornare i tipi di pubblico e gli script di profilo di Target per la compatibilità con l’SDK per web di Platform

Dopo aver completato gli aggiornamenti tecnici per la migrazione di Target all’SDK per web di Platform, potrebbe essere necessario aggiornare alcuni dei tipi di pubblico, gli script di profilo e le attività per garantire una transizione senza problemi.

Tutti i parametri mbox di Target devono essere trasmessi in formato XDM con un’implementazione Platform Web SDK. Prima di pubblicare le modifiche in produzione, devi:

* Aggiorna i tipi di pubblico che utilizzano parametri mbox
* Aggiornare gli script di profilo che utilizzano parametri mbox
* Aggiorna offerte e attività utilizzando la sostituzione del token del parametro mbox (ad esempio, `${mbox.parameter_name}`)

## Regolare il pubblico

Eventuali tipi di pubblico che utilizzano parametri mbox personalizzati devono essere aggiornati per utilizzare i nuovi nomi dei parametri XDM. Ad esempio, un parametro personalizzato per `page_name` probabilmente verrà mappato su `web.webpagedetails.pageName`.

Un approccio per garantire la compatibilità sia con at.js che con Platform Web SDK consiste nell’aggiornare tutti i tipi di pubblico rilevanti in modo che `OR` vengono utilizzate le seguenti condizioni:

![Come visualizzare l’aggiornamento di un pubblico Target per la compatibilità dell’SDK per web di Platform](assets/target-audience-update.png)

## Modificare gli script di profilo

Gli script di profilo devono essere aggiornati per fare riferimento ai nuovi nomi di parametri XDM, simili ai tipi di pubblico. A parte la modifica dei nomi dei parametri mbox, non c’è differenza nel modo in cui gli script di profilo funzionano tra un’implementazione at.js e un’implementazione SDK per web di Platform.

Un approccio per garantire la compatibilità è quello di utilizzare `OR` condizioni nel codice dello script del profilo.

Esempio di script di profilo:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

È stato aggiornato lo script di profilo per la compatibilità dell’SDK per web di Platform:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('page.webpagedetails.pageName') =='Product Details')){
  return true
}
```

Per ulteriori informazioni e best practice, consulta la documentazione dedicata sulle [script di profilo](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Aggiornamento dei token dei parametri per il contenuto dinamico

Se hai offerte, progettazioni di consigli o attività che utilizzano [sostituzione di contenuti dinamici](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html), potrebbe essere necessario aggiornarli di conseguenza per tenere conto dei nuovi nomi di parametri XDM.

A seconda di come utilizzi la sostituzione del token per i parametri mbox, puoi migliorare la configurazione esistente per tenere conto dei nomi dei parametri vecchi e nuovi. Tuttavia, in situazioni in cui il codice JavaScript personalizzato non è possibile, come nelle offerte JSON, devi creare copie e effettuare aggiornamenti al termine della migrazione e live sul sito di produzione.

Esempio di offerta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Esempio di offerta JSON utilizzando i nomi dei parametri SDK per web di Platform:

```JSON
{
  "pageName" : "${mbox.web.webpagedetails.pageName}",
  "layoutVariation" : "grid"
}
```

Se scegli di effettuare regolazioni dopo la migrazione per tenere conto dei nuovi nomi di parametri mbox XDM, assicurati di mettere in pausa tutte le attività interessate durante l’evento di migrazione per evitare errori di visualizzazione dell’attività ai visitatori.

Quindi, scopri come [convalidare l’implementazione di Target](validate.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
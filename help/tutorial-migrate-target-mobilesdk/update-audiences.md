---
title: Aggiornare i tipi di pubblico e gli script di profilo di Target - Migra l’implementazione di Adobe Target nell’app mobile a Adobe Journey Optimizer - Estensione Decisioning
description: Scopri come aggiornare i tipi di pubblico e gli script di profilo di Adobe Target per verificarne la compatibilità con l’estensione Decisioning.
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Aggiorna i tipi di pubblico e gli script di profilo di Target per la compatibilità con le estensioni per dispositivi mobili Decisioning


Dopo aver completato gli aggiornamenti tecnici per la migrazione di Target all’estensione Decisioning, potrebbe essere necessario aggiornare alcuni tipi di pubblico, script di profilo e attività per garantire una transizione senza problemi.

>[!INFO]
>
>Se esegui la migrazione di tutti i parametri mbox all&#39;oggetto `data.__adobe.target`, non dovrai aggiornare i tipi di pubblico, gli script di profilo e le attività come mostrato di seguito.


Se esegui la migrazione dei parametri mbox all&#39;oggetto `xdm`, prima di pubblicare le modifiche nell&#39;ambiente di produzione dovresti:

* Aggiornare i tipi di pubblico che utilizzano i parametri mbox
* Aggiornare gli script di profilo che utilizzano i parametri mbox
* Aggiorna offerte e attività che utilizzano la sostituzione del token di parametro mbox (ad esempio, `${mbox.parameter_name}`)

## Regolare i tipi di pubblico

Se esegui la migrazione dei parametri mbox all&#39;oggetto `xdm`, i tipi di pubblico che utilizzano parametri mbox personalizzati devono essere aggiornati per utilizzare i nuovi nomi dei parametri XDM. Ad esempio, è probabile che un parametro personalizzato per `page_name` venga mappato a `web.webpagedetails.pageName`.

Un approccio per garantire la compatibilità sia con l&#39;estensione Target che con l&#39;estensione Decisioning consiste nell&#39;aggiornare tutti i tipi di pubblico rilevanti in modo che vengano utilizzate `OR` condizioni, come illustrato di seguito:

![Come visualizzare l&#39;aggiornamento di un pubblico Target per la compatibilità dell&#39;estensione Decisioning](assets/target-audience-update.png){zoomable="yes"}

## Modificare gli script di profilo

Se esegui la migrazione dei parametri mbox all&#39;oggetto `xdm`, gli script di profilo devono essere aggiornati per fare riferimento ai nuovi nomi dei parametri XDM, in modo simile ai tipi di pubblico. A parte la modifica dei nomi dei parametri mbox, non vi è alcuna differenza nel modo in cui gli script di profilo funzionano tra un’implementazione Target e Decisioning.

Un approccio per garantire la compatibilità consiste nell&#39;utilizzare le condizioni `OR` nel codice dello script di profilo.

Esempio di script di profilo:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

È stato aggiornato lo script di profilo per la compatibilità con Platform Web SDK:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Per ulteriori informazioni e best practice, consulta la documentazione dedicata su [script di profilo](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/profile-parameters).

## Aggiornare i token dei parametri per il contenuto dinamico

Se esegui la migrazione dei parametri mbox all&#39;oggetto `xdm` e disponi di offerte, progettazioni di consigli o attività che utilizzano [sostituzione dinamica dei contenuti](https://experienceleague.adobe.com/en/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer), potrebbe essere necessario aggiornarli di conseguenza per tenere conto dei nuovi nomi dei parametri XDM.

A seconda di come utilizzi la sostituzione del token per i parametri mbox, potresti essere in grado di migliorare la configurazione esistente per tenere conto dei nomi dei parametri vecchi e nuovi. Tuttavia, in situazioni in cui il codice JavaScript personalizzato non è possibile, ad esempio nelle offerte JSON, devi creare copie e apportare aggiornamenti dopo che la migrazione è stata completata e pubblicata sul sito di produzione.

Esempio di offerta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Esempio di offerta JSON con nomi di parametri di oggetti XDM:

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Se scegli di apportare modifiche dopo la migrazione per tenere conto dei nuovi nomi dei parametri mbox XDM, assicurati di mettere in pausa le attività interessate durante l’evento di migrazione per evitare errori di visualizzazione delle attività per i visitatori.


Quindi, scopri come [convalidare l&#39;implementazione di Target](validate.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).

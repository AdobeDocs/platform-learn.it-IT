---
title: Pianificazione | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come pianificare l’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Pianificare la migrazione da at.js a Platform Web SDK

Prima di eseguire l’aggiornamento a Platform Web SDK sul sito, è necessario valutare l’implementazione corrente.

## Valutare l’implementazione corrente di at.js

Il primo passo per una migrazione di successo è quello di avere una chiara comprensione dell’implementazione di at.js Target corrente. È possibile utilizzare funzioni, funzioni e codice personalizzato che richiedono aggiornamenti. Considera quanto segue durante la valutazione:

### Quali funzioni sono supportate?

L’SDK per web di Platform è in continuo sviluppo attivo e le funzioni e i miglioramenti vengono aggiunti regolarmente. Quando valuta l’implementazione corrente di at.js, fai riferimento alla sezione [casi di utilizzo supportati](https://github.com/orgs/adobe/projects/18/views/1) per informazioni aggiornate.

### Quali funzioni utilizzate oggi?

Platform Web SDK è una nuova libreria che consolida tutte le soluzioni Adobe per i siti web in un unico SDK. Ciò consente un&#39;integrazione più stretta e offre nuove funzionalità esclusive di Adobe Experience Platform. Tuttavia, ciò significa anche che le funzioni at.js non sono compatibili con l’SDK per web di Platform. Quando valuti l’implementazione corrente, prendi nota di quanto segue:

- funzioni di at.js come `getOffer()` e `applyOffer()`
- Modifiche alle impostazioni globali di Target
- Integrazione con Adobe Analytics
- Utilizzo di uno script di mitigazione della visualizzazione momentanea di altri contenuti
- Utilizzo dei token di risposta
- Utilizzo di parametri mbox, di profilo e di entità
- Codice personalizzato univoco per la tua implementazione

### Quale approccio di migrazione adotterà?

Dopo aver rivisto l’implementazione di at.js, devi determinare un approccio di migrazione. Sono disponibili due opzioni:

- Migrazione simultanea di tutte le applicazioni Adobe nell&#39;intero sito
- Eseguire la migrazione pagina per pagina

Poiché Platform Web SDK combina e abilita più applicazioni di Adobe, devi coordinare la migrazione di Target di altre applicazioni di Adobe come Analytics e Audience Manager. Tutte le librerie di Adobi in una determinata pagina devono essere migrate contemporaneamente. Non è supportata un’implementazione mista di Platform Web SDK per Target e AppMeasurement per Analytics in una particolare pagina. Tuttavia, è supportata un’implementazione mista tra pagine diverse, ad esempio Platform Web SDK a pagina A e at.js con AppMeasurement a pagina B.

Durante la migrazione, devi pianificare il seguito del processo aziendale per il test e il rilascio di nuovo codice e utilizzare elementi come lo sviluppo, il controllo qualità e gli ambienti di staging prima del rilascio in produzione.

>[!CAUTION]
>
>Le offerte di reindirizzamento non sono supportate nelle migrazioni pagina per pagina se si esegue il reindirizzamento da una pagina con una libreria a una pagina con una libreria diversa


Quindi, rivedi il [confronto tra at.js e Platform Web SDK](detailed-comparison.md) per comprendere meglio le differenze tecniche e individuare le aree che richiedono un&#39;ulteriore attenzione.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).

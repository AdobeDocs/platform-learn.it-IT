---
title: Planning - Migrazione di Target da at.js 2.x a Web SDK
description: Scopri come pianificare l’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Pianificare la migrazione da at.js a Platform Web SDK

Prima di eseguire l’aggiornamento a Platform Web SDK sul sito, è necessario valutare l’implementazione corrente.

## Valuta l’implementazione at.js corrente

Il primo passaggio per una migrazione di successo consiste nel comprendere a fondo l’attuale implementazione di Target at.js. Potresti utilizzare funzioni, funzioni e codice personalizzato che richiedono aggiornamenti. Durante la valutazione, considera quanto segue:

### Quali funzioni sono supportate?

Platform Web SDK è in fase di sviluppo continuo attivo e vengono aggiunte regolarmente funzionalità e miglioramenti. Durante la valutazione dell&#39;implementazione at.js corrente, consulta la pagina [casi d&#39;uso supportati](https://github.com/orgs/adobe/projects/18/views/1) per informazioni aggiornate.

### Quali funzioni utilizza oggi?

Platform Web SDK è una nuova libreria che consolida in un unico SDK tutte le soluzioni Adobe per i siti web. Ciò consente una maggiore integrazione e nuove funzionalità esclusive di Adobe Experience Platform. Tuttavia, significa anche che le funzioni di at.js non sono compatibili con le versioni precedenti di Platform Web SDK. Nel valutare l’implementazione corrente, prendi nota di quanto segue:

- Funzioni di at.js come `getOffer()` e `applyOffer()`
- Modifiche alle impostazioni globali di Target
- Integrazione con Adobe Analytics
- Utilizzo di uno script di mitigazione dello sfarfallio
- Utilizzo dei token di risposta
- Utilizzo di parametri mbox, di profilo ed entità
- Codice personalizzato univoco per l’implementazione

### Quale approccio di migrazione adotterai?

Dopo aver rivisto l’implementazione di at.js, devi determinare un approccio di migrazione. Sono disponibili due opzioni:

- Eseguire la migrazione di tutte le applicazioni Adobe contemporaneamente in tutto il sito
- Eseguire la migrazione pagina per pagina

Poiché Platform Web SDK combina e abilita più applicazioni Adobe, è necessario coordinare la migrazione di Target di altre applicazioni Adobe come Analytics e Audience Manager. Tutte le librerie di Adobi in una determinata pagina devono essere migrate contemporaneamente. Non è supportata un’implementazione mista di Platform Web SDK per Target e AppMeasurement per Analytics su una pagina particolare. Tuttavia, è supportata un’implementazione mista in diverse pagine, ad esempio Platform Web SDK a pagina A e at.js con AppMeasurement a pagina B.

Durante la migrazione, prima di rilasciare il codice in produzione, è necessario pianificare il rispetto del processo aziendale per il test e il rilascio del nuovo codice e l&#39;utilizzo di elementi quali gli ambienti di sviluppo, controllo qualità e staging.

>[!CAUTION]
>
>Le offerte di reindirizzamento non sono supportate nelle migrazioni pagina per pagina se si esegue il reindirizzamento da una pagina con una libreria a una pagina con una libreria diversa


Quindi, controlla il [confronto dettagliato di at.js con Platform Web SDK](detailed-comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un ulteriore approfondimento.

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=it#M463).

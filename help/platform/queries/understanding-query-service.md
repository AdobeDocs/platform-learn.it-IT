---
title: Panoramica di Query Service e Data Distiller
description: Adobe Experience Platform Query Service consente agli utenti di esplorare, convalidare e trasformare i dati sull’esperienza del cliente memorizzati nel data lake utilizzando SQL, con funzionalità avanzate come output e pianificazione dei dati disponibili tramite il componente aggiuntivo Data Distiller. Questo video fornisce una panoramica delle funzioni di base per aiutare gli utenti a comprendere come sfruttare Query Service in diverse applicazioni basate su Platform.
feature: Queries
role: Data Engineer, Developer
level: Beginner
jira: KT-3139
last-substantial-update: 2025-06-23T00:00:00Z
exl-id: 988bc316-9eec-4dca-8049-95c2d613379d
source-git-commit: b0466e114d657c2584b23bfd76e4f6c185c83c06
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 13%

---

# Panoramica di Query Service e Data Distiller

Adobe Experience Platform Query Service consente agli utenti di esplorare, convalidare e trasformare i dati sull’esperienza del cliente memorizzati nel data lake utilizzando SQL, con funzionalità avanzate come output e pianificazione dei dati disponibili tramite il componente aggiuntivo Data Distiller. Questo video fornisce una panoramica delle funzioni di base per aiutare gli utenti a comprendere come sfruttare Query Service in diverse applicazioni basate su Platform. Per ulteriori informazioni, visitare la [documentazione di Query Service](https://experienceleague.adobe.com/it/docs/experience-platform/query/home).

>[!VIDEO](https://video.tv.adobe.com/v/39649?learn=on&enablevpops&captions=ita)

## Utilizzo di base

<!-- CARDS
* query-service-ui.md
* query-service-api.md
* adobe-defined-functions.md
* run-queries.md
* understanding-data-usage-patterns-with-query-service.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service UI">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-ui.md" title="Interfaccia utente di Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333403?format=jpeg&nocache=1740415310696" alt="Interfaccia utente di Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-ui.md" target="_blank" rel="referrer" title="Interfaccia utente di Query Service">Interfaccia utente di Query Service</a>
                    </p>
                    <p class="is-size-6">Scopri come scrivere ed eseguire le query, visualizzare le query eseguite in precedenza e accedere a quelle salvate da altri utenti nell’organizzazione IMS in Adobe Experience Platform Query Service.</p>
                </div>
                <a href="query-service-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service API">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-api.md" title="API servizio query" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3414086?format=jpeg&nocache=1740415310716&captions=ita" alt="API servizio query"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-api.md" target="_blank" rel="referrer" title="API servizio query">API servizio query</a>
                    </p>
                    <p class="is-size-6">Scopri come scrivere ed eseguire query, creare query di pianificazione e creare un modello di query utilizzando l’API di Adobe Experience Platform Query Service.</p>
                </div>
                <a href="query-service-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe Defined Functions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="adobe-defined-functions.md" title="Funzioni definite da Adobe" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3414050?format=jpeg&nocache=1740415310668&captions=ita" alt="Funzioni definite da Adobe"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="adobe-defined-functions.md" target="_blank" rel="referrer" title="Funzioni definite da Adobe">Funzioni definite da Adobe</a>
                    </p>
                    <p class="is-size-6">Scopri come utilizzare le funzioni definite da Adobe in Adobe Experience Platform Query Service per eseguire attività di business comuni sui dati degli eventi delle esperienze.</p>
                </div>
                <a href="adobe-defined-functions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Run Queries with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="run-queries.md" title="Eseguire query con Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/39842?format=jpeg&nocache=1740415310683&captions=ita" alt="Eseguire query con Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="run-queries.md" target="_blank" rel="referrer" title="Eseguire query con Query Service">Esegui query con Query Service</a>
                    </p>
                    <p class="is-size-6">Questo video mostra come eseguire query nell’interfaccia di Adobe Experience Platform e in un client PSQL. Inoltre, è dimostrato l’utilizzo di singole proprietà in un oggetto XDM, utilizzando le funzioni definite da Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).</p>
                </div>
                <a href="run-queries.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Informazioni sui pattern di utilizzo dei dati con Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/39589?format=jpeg&nocache=1740415310706&captions=ita" alt="Informazioni sui pattern di utilizzo dei dati con Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Informazioni sui pattern di utilizzo dei dati con Query Service">Informazioni sui pattern di utilizzo dei dati con Query Service</a>
                    </p>
                    <p class="is-size-6">Questo video offre suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor delle query, nei client PSQL, nelle soluzioni di business intelligence (BI) e nell’API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Convalida ed esplorazione dei dati

<!-- CARDS
* explore-data.md
* validate-data-in-the-datalake.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Explore data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="explore-data.md" title="Esplora i dati" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3414056?format=jpeg&nocache=1740415312087&captions=ita" alt="Esplora i dati"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="explore-data.md" target="_blank" rel="referrer" title="Esplora i dati">Esplora dati</a>
                    </p>
                    <p class="is-size-6">Scopri come convalidare i dati acquisiti, visualizzarli in anteprima ed esplorarne le proprietà statistiche e analitiche utilizzando le funzioni SQL.</p>
                </div>
                <a href="explore-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Validate data in the datalake with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="validate-data-in-the-datalake.md" title="Convalidare i dati nel datalake con Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3445685?format=jpeg&nocache=1740415312076&captions=ita" alt="Convalidare i dati nel datalake con Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" title="Convalidare i dati nel datalake con Query Service">Convalida dati nel datalake con Query Service</a>
                    </p>
                    <p class="is-size-6">Scopri come verificare se i dati sono stati correttamente acquisiti nel datalake utilizzando Adobe Experience Platform Query Service.</p>
                </div>
                <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Trasformazione dei dati con Data Distiller

<!-- CARDS
* 
* prepare-data.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Prepare data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="prepare-data.md" title="Prepara i dati" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3414068?format=jpeg&nocache=1740415313086&captions=ita" alt="Prepara i dati"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="prepare-data.md" target="_blank" rel="referrer" title="Prepara i dati">Preparare i dati</a>
                    </p>
                    <p class="is-size-6">Scopri come pulire, preparare e combinare dati da più set di dati per creare un nuovo set di dati utilizzando le funzioni CTAS (Create Table AS) e Spark SQL per il reporting e il dashboard.</p>
                </div>
                <a href="prepare-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Casi d’uso

<!-- CARDS
* understanding-data-usage-patterns-with-query-service.md
* psql-client-tableau.md
* analyze-and-visualize.md
* recharge-your-customer-data.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Informazioni sui pattern di utilizzo dei dati con Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/39589?format=jpeg&nocache=1740415313190&captions=ita" alt="Informazioni sui pattern di utilizzo dei dati con Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Informazioni sui pattern di utilizzo dei dati con Query Service">Informazioni sui pattern di utilizzo dei dati con Query Service</a>
                    </p>
                    <p class="is-size-6">Questo video offre suggerimenti e best practice per l’esecuzione di query nell’interfaccia dell’editor delle query, nei client PSQL, nelle soluzioni di business intelligence (BI) e nell’API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Connect Tableau to Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="psql-client-tableau.md" title="Connettere Tableau a Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3414044?format=jpeg&nocache=1740415313229&captions=ita" alt="Connettere Tableau a Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="psql-client-tableau.md" target="_blank" rel="referrer" title="Connettere Tableau a Query Service">Connettere Tableau a Query Service</a>
                    </p>
                    <p class="is-size-6">Scopri come connettersi a Query Service da diverse applicazioni client desktop che supportano il protocollo PostgreSQL e come utilizzare gli strumenti e i driver PostgreSQL per connettersi e scrivere query.</p>
                </div>
                <a href="psql-client-tableau.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Analyze and visualize omni-channel insights in Tableau using Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="analyze-and-visualize.md" title="Analizzare e visualizzare informazioni omni-channel in Tableau utilizzando Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342115?format=jpeg&nocache=1740415313204" alt="Analizzare e visualizzare informazioni omni-channel in Tableau utilizzando Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="analyze-and-visualize.md" target="_blank" rel="referrer" title="Analizzare e visualizzare informazioni omni-channel in Tableau utilizzando Query Service">Analizzare e visualizzare informazioni omni-channel in Tableau utilizzando Query Service</a>
                    </p>
                    <p class="is-size-6">Con un esempio di churn analysis, scopri come utilizzare il servizio query dell'Adobe Experience Platform con strumenti di visualizzazione dei dati esterni.</p>
                </div>
                <a href="analyze-and-visualize.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Recharge your customer data to deliver electrifying experiences">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="recharge-your-customer-data.md" title="Ricarica i dati dei tuoi clienti per offrire esperienze elettrizzanti" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3454954?format=jpeg&nocache=1740415313218&captions=ita" alt="Ricarica i dati dei tuoi clienti per offrire esperienze elettrizzanti"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" title="Ricarica i dati dei tuoi clienti per offrire esperienze elettrizzanti">Ricarica i dati del cliente per fornire esperienze elettrizzanti</a>
                    </p>
                    <p class="is-size-6">Scopri come mitigare l’impatto di dati di bassa qualità, ridurre il time-to-value e moltiplicare il ROI utilizzando gli stessi dati per molti casi d’uso.</p>
                </div>
                <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Ulteriori informazioni</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

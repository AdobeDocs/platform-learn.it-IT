---
title: Igiene dei dati in Adobe Experience Platform
description: Scopri le opzioni degli strumenti per l’igiene dei dati in Adobe Experience Platform
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
feature: Data Hygiene
role: Developer
level: Intermediate
source-git-commit: 9c15708f7300672caa963c0635179dd2855e5fed
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 22%

---

# Tutorial sull’igiene dei dati

Scopri le funzionalità di igiene dei dati di Adobe Experience Platform, che includono:

* Abilitazione dei principi di minimizzazione dei dati durante l’acquisizione dei dati
* Adeguamento dei dati già presenti nel sistema
* Rimozione di dati dal sistema

<!--
Data hygiene:

* Enables citizen data stewards working in Privacy or IT teams to manage customer data lifecycle.
* Provides foundational workflows for setting expiration of datasets based on corporate policies, partner
arrangements, customer commitments or regulatory needs.
* Provides foundational workflows for managing targeted treatment of identities and data belonging to consumers in a
holistic fashion.
* Provides monitoring, work order management and notifications of tasks.
* Provides the ability to log the lifecyle management tasks for auditing purposes.
-->

## Minimizzazione dei dati durante l’acquisizione

La funzione di preparazione dei dati consente di acquisire solo i campi necessari da un’origine dati.

<!-- CARDS
{cta=Watch}
* data-prep-for-data-hygiene.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Data prep for data hygiene">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="data-prep-for-data-hygiene.md" title="Preparazione dei dati per l’igiene dei dati" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429485/?format=jpeg&nocache=1740251397387" alt="Preparazione dei dati per l’igiene dei dati"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" title="Preparazione dei dati per l’igiene dei dati">Preparazione dei dati per l’igiene</a>
                    </p>
                    <p class="is-size-6">Scopri come supportare i principi di minimizzazione dei dati con la funzione di preparazione dei dati di Experience Platform. Scopri come acquisire solo i campi necessari e aggiungere hash ai dati durante l’acquisizione.</p>
                </div>
                <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Rimozione dei dati dal sistema

Esistono molte funzionalità per rimuovere i dati dal sistema. Puoi eliminare interi set di dati su richiesta o secondo una pianificazione, scadere record e profili con impostazioni di time-to-live, eliminare singoli profili e rispettare le richieste di privacy.
<!-- CARDS
{cta=Watch}
* delete-datasets-and-batches.md
* ../data-lifecycle/expire-datasets.md
* pseudonymous-profile-and-event-expiration.md
* ../profiles/delete-profiles.md{description=Learn how to delete data from the Profile Store using the Real-Time Customer Profile API. By using the Profile API, you can remove data from the profile store without affecting the data lake or identity graph.}
* ../privacy/introduction-to-privacy-services.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete datasets and batches">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-datasets-and-batches.md" title="Eliminare set di dati e batch" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429790/?format=jpeg&nocache=1740251397681" alt="Eliminare set di dati e batch"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" title="Eliminare set di dati e batch">Eliminare set di dati e batch</a>
                    </p>
                    <p class="is-size-6">Scopri come eliminare i set di dati e batch in Adobe Experience Platform.</p>
                </div>
                <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Schedule dataset deletes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../data-lifecycle/expire-datasets.md" title="Pianificare le eliminazioni dei set di dati" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/345065?format=jpeg&nocache=1740251397716" alt="Pianificare le eliminazioni dei set di dati"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" title="Pianificare le eliminazioni dei set di dati">Pianifica eliminazioni set di dati</a>
                    </p>
                    <p class="is-size-6">Scopri come eliminare i set di dati utilizzando la funzione di igiene dei dati di Adobe Experience Platform.</p>
                </div>
                <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Pseudonymous profile and Experience Event expirations">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="pseudonymous-profile-and-event-expiration.md" title="Scadenze di profili pseudonimi ed eventi esperienza" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3428361?format=jpeg&nocache=1740251397705" alt="Scadenze di profili pseudonimi ed eventi esperienza"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" title="Scadenze di profili pseudonimi ed eventi esperienza">Scadenze di profili ed eventi esperienza sotto pseudonimo</a>
                    </p>
                    <p class="is-size-6">Scopri come configurare le impostazioni di scadenza per profili ed eventi sotto pseudonimo in Experience Platform e i relativi vantaggi.</p>
                </div>
                <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/delete-profiles.md" title="Eliminare i profili" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740251397692" alt="Eliminare i profili"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" title="Eliminare i profili">Elimina profili</a>
                    </p>
                    <p class="is-size-6">Scopri come eliminare i dati dall’archivio profili di utilizzando l’API Profilo cliente in tempo reale. Utilizzando l’API di profilo, puoi rimuovere i dati dall’archivio profili senza influire sul data lake o sul grafico delle identità.</p>
                </div>
                <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Introduction to Privacy Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../privacy/introduction-to-privacy-services.md" title="Introduzione a Privacy Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336074?format=jpeg&nocache=1740251397727" alt="Introduzione a Privacy Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" title="Introduzione a Privacy Service">Introduzione a Privacy Service</a>
                    </p>
                    <p class="is-size-6">Scopri le normative sulla privacy e i loro effetti sulle operazioni relative ai dati. Inoltre, scopri come Privacy Service gestisce queste sfide.</p>
                </div>
                <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->





## Adeguamento dei dati nel sistema

<!-- CARDS
{cta=Watch}
* ../profiles/update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/update-a-specific-attribute-with-upsert.md" title="Aggiornare attributi di profilo specifici utilizzando &quot;upsert&quot;" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740251398874" alt="Aggiornare attributi di profilo specifici utilizzando &quot;upsert&quot;"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="Aggiornare attributi di profilo specifici utilizzando &quot;upsert&quot;">Aggiorna attributi di profilo specifici utilizzando 'upsert'</a>
                    </p>
                    <p class="is-size-6">Scopri come aggiornare un attributo specifico di un profilo utilizzando la funzione "upsert" di Adobe Experience Platform.</p>
                </div>
                <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Osserva</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

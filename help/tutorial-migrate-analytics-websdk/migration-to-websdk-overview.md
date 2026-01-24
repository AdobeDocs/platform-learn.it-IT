---
title: Migrazione da Adobe Analytics a Web SDK tramite tag
description: Scopri i passaggi da eseguire durante la migrazione a Web SDK e le decisioni da prendere lungo il percorso.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: d6471c8e383e22fed4ad5870952d0d0470f593db
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Migrazione da Adobe Analytics a Web SDK tramite tag

Scopri i passaggi per migrare un’implementazione di Adobe Analytics utilizzando l’estensione Analytics in Experience Platform Tags (precedentemente nota come Launch) a Web SDK, utilizzando l’estensione Web SDK anche in Tags. Quando si utilizza l’estensione Adobe Analytics nei Tag, viene utilizzato il codice &quot;AppMeasurement.js&quot; in background. Di conseguenza, puoi considerare questo come un’esercitazione per la migrazione di AppMeasurement a Web SDK, ma questa esercitazione si trova completamente all’interno di Tag e NON riguarda lo spostamento da o verso un’implementazione di JavaScript (ad eccezione del codice JavaScript utilizzato all’interno dell’interfaccia utente di Tags). Per la migrazione delle implementazioni di JavaScript, consulta la [documentazione](https://experienceleague.adobe.com/it/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk).

>[!NOTE]
>
>Esercitazioni simili sulla migrazione sono disponibili per:
>
> * [Adobe Target](../tutorial-migrate-target-websdk/introduction.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/it/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Poiché Platform Web SDK supporta più applicazioni Adobe, è necessario eseguire la migrazione di tutte le librerie Adobe di una determinata pagina contemporaneamente. Non è supportata, ad esempio, un&#39;implementazione mista di Web SDK for Target e AppMeasurement for Analytics su una singola pagina __. Tuttavia, è supportata un’implementazione mista in pagine diverse, ad esempio Web SDK alla pagina A e at.js con AppMeasurement alla pagina B.

## Cosa otterrai da questa esercitazione

Prima di passare ai passaggi per la migrazione dell&#39;implementazione di Analytics, è importante che tu capisca esattamente cosa farai, ovvero modificare/aggiornare l&#39;_implementazione_ per Analytics. Alla fine di questa esercitazione, quando andate nei vostri rapporti e quando tutto è uguale, vi chiederete, &quot;Ora, perché ho fatto tutto questo?&quot; Esistono altri documenti per delineare i vantaggi dell’utilizzo di Web SDK per l’implementazione di Analytics, ma alcuni sono:

1. Supporto per ID dispositivo di prime parti
1. Prestazioni migliori
1. Garantire la validità futura dell’implementazione man mano che si procede all’utilizzo delle applicazioni Adobe Experience Platform (abilitazione di nuovi casi d’uso)

Per ulteriori informazioni su come utilizzare il Web SDK, rivolgiti al tuo rappresentante Adobe Analytics. Continuando con questa esercitazione, ci concentreremo su _come_ eseguire la migrazione.

>[!IMPORTANT]
>
>È importante notare che uno dei motivi principali per cui stai eseguendo questa migrazione dell’implementazione è quello di prepararti all’utilizzo di applicazioni Adobe Experience Platform, come Customer Journey Analytics, Real-Time CDP o Journey Optimizer (come indicato in #3 sopra). L’utilizzo dei dati del sito web a questo scopo includerà passaggi aggiuntivi non inclusi in questa esercitazione, ma questa esercitazione sarà sicuramente un prerequisito per quell’ulteriore avanzamento dell’implementazione. Pertanto, completa questa esercitazione e poi puoi eseguire i passaggi necessari per inviare gli stessi dati del sito web all’Experience Platform.

## Metodo di migrazione

Ci sono probabilmente molti modi per eseguire questo processo di migrazione, ma dobbiamo parlarne due proprio qui:

**Metodo 1:** Aggiorna la proprietà Tags esistente in Web SDK, creando nuovi elementi dati e apportando modifiche alle regole già esistenti nella proprietà.

**Metodo 2:** è inoltre possibile creare una nuova proprietà copiando quella esistente o creandone una nuova e quindi configurarla con Web SDK anziché con l&#39;estensione Adobe Analytics.

**Per questa esercitazione sulla migrazione verrà utilizzato il metodo 1.** In questo modo i codici di incorporamento associati alla proprietà sono già incorporati nei siti di sviluppo, staging e produzione, quindi non sarà necessario modificare alcun codice di incorporamento. Se decidi di utilizzare il metodo 2, non dimenticare di ottenere i nuovi codici di incorporamento per ogni ambiente dalla sezione **Ambienti** della nuova proprietà e inserirli nella sezione head del sito.

>[!NOTE]
>
>Anche se modificheremo semplicemente la nostra proprietà esistente in Tag durante questa migrazione, è comunque una buona idea stare attenti. Pertanto, ti consigliamo vivamente di creare una copia della proprietà corrente prima di avviare la migrazione. In questo modo, si può sempre andare nella copia e vedere come erano le cose prima di cambiarle, estrarre il codice da esso, ecc.
>È bene stare attenti, nel caso. Procedi e crea la copia della proprietà. Aspetterò qui finché non ritorni.

## Passaggi per migrare l’implementazione di Analytics al Web SDK

Durante l’esecuzione dei passaggi, è importante comprendere alcune avvertenze:

1. Innanzitutto, tutti questi passaggi possono essere necessari o meno. Ad esempio, esiste una lezione sulla migrazione del codice personalizzato. Se disponi di un’implementazione di Tag che non utilizza codice personalizzato (incluso l’utilizzo di plug-in), questa lezione non sarà necessaria. Abbiamo cercato di includere le lezioni che sarebbero state necessarie alla maggior parte degli utenti, quindi leggi almeno le lezioni per vedere se è necessario apportare modifiche al sito durante la migrazione.
1. Inoltre, non c’è modo di creare un tutorial sulla migrazione che copra il 100% dei casi d’uso che tutti utilizzano. Come affermato nell&#39;articolo precedente, abbiamo cercato di includere le lezioni di cui la maggior parte delle persone avrà bisogno, e che riguarderanno la maggior parte dei casi d&#39;uso principali. Tuttavia, ci saranno sicuramente casi d’uso non trattati in questa esercitazione. In questo caso, verifica se le lezioni incluse ti danno una buona idea di come eseguire la migrazione per il tuo caso d’uso. Puoi anche chiedere ai tuoi colleghi della [Community Experience League di raccogliere dati](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community?profile.language=it).

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Crea una suite di rapporti per la convalida della migrazione.
1. Crea e configura un flusso di dati.
1. Aggiungi e configura l’estensione Web SDK in Tag (precedentemente Adobe Launch).
1. Crea un nuovo elemento dati per inviare dati in tramite Web SDK.
1. Esegui la migrazione della regola di caricamento pagina predefinita per utilizzare l&#39;elemento dati e le azioni di Web SDK.
1. Esegui la migrazione del codice personalizzato nelle regole o per i plug-in.
1. Modifiche all’implementazione di Publish.
1. Scopri come eseguire il debug e convalidare le modifiche e convalidare la regola di caricamento pagina predefinita e le variabili associate. La convalida deve quindi continuare per tutta la migrazione man mano che apporti modifiche.
1. Eseguire la migrazione di altre regole di caricamento della pagina.
1. Eseguire la migrazione delle regole di collegamento personalizzate.
1. Dopo la convalida completa, rimuovi i riferimenti all’estensione Analytics e l’estensione stessa.
1. Dopo aver apportato tutte le modifiche, invia la libreria allo staging e quindi alla produzione.
1. Dopo aver completato tutto, verifica di nuovo. Ciò è necessario perché hai apportato modifiche rimuovendo i riferimenti al vecchio codice Analytics e desideri che tutto funzioni ancora correttamente.

>[!NOTE]
>
>Ci impegniamo per aiutarti a completare con successo la migrazione di Analytics a Web SDK. Se incontri ostacoli con la migrazione o ritieni che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308?profile.language=it#M604){target="_blank"}.


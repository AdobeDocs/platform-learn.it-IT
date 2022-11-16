---
title: Servizio query - Guida introduttiva
description: Servizio query - Guida introduttiva
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dae257d2-8c94-4558-b9ce-eca38a88667b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 4.1 Guida introduttiva

## 4.1.1 Acquisire familiarità con l&#39;interfaccia utente di Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--module7sandbox--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](../module2/images/sb1.png)


## 4.1.2 Esplorare i dati sulla piattaforma

Portare dati da diversi canali è un compito difficile per qualsiasi marchio. E in questo esercizio, i clienti Citi Signal sono coinvolti con Citi Signal sul suo sito web, sulla sua app mobile, i dati di acquisto sono raccolti dal sistema Punti di Vendita di Citi Signal, e hanno i dati CRM e Fedeltà. Citi Signal utilizza Adobe Analytics e Adobe Launch per acquisire dati dal sito web, dall’app mobile e dal sistema POS, pertanto questi dati stanno già scorrendo in Adobe Experience Platform. Cominciamo con l&#39;esplorazione di tutti i dati per Citi Signal già esistenti in Adobe Experience Platform.

Nel menu a sinistra, vai a **Set di dati**.

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

Citi Signal sta eseguendo lo streaming dei dati in Adobe Experience Platform ed è disponibile nella `Demo System - Event Dataset for Website (Global v1.1)` set di dati. Cerca `Demo System - Event Dataset for Website`.

![emea-callcenter-actions-dataset.png](./images/emea-website-interaction-dataset1.png)

I dati di interazione del Callcenter di Citi Signal vengono catturati nella `Demo System - Event Dataset for Call Center (Global v1.1)` set di dati. Cerca `Demo System - Event Dataset for Call Center` dati nella casella di ricerca. Fai clic sul nome del set di dati per aprirlo.

![emea-callcenter-actions-dataset.png](./images/emea-callcenter-interaction-dataset.png)

Dopo aver fatto clic sul set di dati, otterrai una panoramica dell’attività del set di dati, ad esempio i batch acquisiti e non riusciti.

![preview-action-dataset.png](./images/preview-interaction-dataset.png)

Fai clic su **Anteprima set di dati** per visualizzare un esempio dei dati memorizzati in `Demo System - Event Dataset for Call Center (Global v1.1)` set di dati. Il pannello a sinistra mostra la struttura dello schema per questo set di dati.

![expl-interazione-dataset.png](./images/explore-interaction-dataset.png)

Fai clic sul pulsante **Chiudi** per chiudere il pulsante **Anteprima set di dati** finestra.

## 4.1.3 Introduzione al servizio query

È possibile accedere a Adobe Experience Platform Query Service facendo clic su **Query** nel menu a sinistra.

![select-query.png](./images/select-queries.png)

Per **Registro** viene visualizzata la pagina Elenco query, che fornisce un elenco di tutte le query eseguite in questa organizzazione, con le ultime in alto.

![query-list.png](./images/query-list.png)

Fai clic su una query SQL dall’elenco e osserva i dettagli forniti nella barra a destra.

![click-sql-query.png](./images/click-sql-query.png)

È possibile scorrere la finestra per visualizzare l&#39;intera query oppure fare clic sull&#39;icona evidenziata di seguito per copiare l&#39;intera query sul blocco note. Al momento non è necessario copiare la query.

![click-copy-query.png](./images/click-copy-query.png)

Non è possibile visualizzare solo le query eseguite, questa interfaccia utente consente di creare nuovi set di dati dalle query. Questi set di dati possono essere collegati al Profilo cliente in tempo reale di Adobe Experience Platform o possono essere utilizzati come input per Adobe Experience Platform Data Science Workspace.

## 4.1.4 Connettere il client PSQL al servizio query

Query Service supporta i client con un driver per PostgreSQL. In questo utilizzeremo PSQL, un&#39;interfaccia a riga di comando, e Power BI o Tableau. Connettiamoci a PSQL.

Fai clic su **Credenziali**.

![query-select-configuration.png](./images/queries-select-configuration.png)

Verrà visualizzata la schermata sottostante. La schermata Configurazione fornisce le informazioni e le credenziali del server per l’autenticazione al servizio query. Per il momento, ci concentreremo sul lato destro dello schermo che contiene un comando di connessione per PSQL. Fai clic sul pulsante Copia per copiare il comando negli Appunti.

![copy-psql-connection.png](./images/copy-psql-connection.png)

Per Windows: Aprire la riga di comando premendo il tasto Windows e digitando cmd, quindi facendo clic sul risultato del prompt dei comandi.

![open-command-prompt.png](./images/open-command-prompt.png)

Per macOS: Apri Terminal.app tramite la ricerca Spotlight:

![open-terminal-osx.png](./images/open-terminal-osx.png)

Incolla il comando di connessione copiato dall’interfaccia utente del servizio query e premi Invio nella finestra del prompt dei comandi:

Windows:

![command-prompt-connection.png](./images/command-prompt-connected.png)

MacOS:

![command-prompt-paste-osx.png](./images/command-prompt-paste-osx.png)

È ora disponibile una connessione a Query Service tramite PSQL.

Negli esercizi successivi, ci sarà una certa interazione con questa finestra. Lo considereremo come il tuo **Interfaccia della riga di comando PSQL**.

Ora puoi iniziare a inviare le query.

Passaggio successivo: [4.2 Utilizzo del servizio Query](./ex2.md)

[Torna al modulo 4](./query-service.md)

[Torna a tutti i moduli](../../overview.md)

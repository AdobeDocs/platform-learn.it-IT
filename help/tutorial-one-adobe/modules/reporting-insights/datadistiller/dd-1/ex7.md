---
title: 'Query Service: esplora il set di dati con Tableau'
description: 'Query Service: esplora il set di dati con Tableau'
kt: 5342
doc-type: tutorial
exl-id: 33ab854d-fad7-497c-affa-f58e4299c0b3
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 2.1.7 Query Service e Tableau

Apri Tableau.

![start-tableau.png](./images/starttableau.png)

In **Connetti a un server**, fare clic su **Altro** e quindi su **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Se non hai ancora utilizzato PostgeSQL con Tableau, potresti vedere questo. Fare clic su **Scarica driver**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress1.png)

Seguire le istruzioni per scaricare e installare il driver PostgreSQL.

![tableau-connect-postgress.png](./images/tableauconnectpostgress2.png)

Al termine dell&#39;installazione del driver, uscire e riavviare Tableau Desktop. Dopo il riavvio, passare di nuovo a **Connetti a un server**, fare clic su **Altro** e quindi di nuovo su **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Poi vedrai questo.

![tableau-connect-postgress.png](./images/tableauconnectpostgress3.png)

Vai a Adobe Experience Platform, **Query** e **Credenziali**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Dalla pagina **Credenziali** in Adobe Experience Platform, copia **Host** e incollalo nel campo **Server**, copia il **Database** e incollalo nel campo **Database** in Tableau, copia la **Porta** e incollala nel campo **Porta** in Tableau, esegui le stesse operazioni per **Nome utente** e **Password**. Fare clic su **Accedi**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

Nell&#39;elenco delle tabelle disponibili individuare la tabella creata nell&#39;esercizio precedente, denominata `--aepUserLdap--_callcenter_interaction_analysis`. Trascinalo nell’area di lavoro.

![tableau-drag-table.png](./images/tableaudragtable.png)

Poi vedrai questo. Fai clic su **Aggiorna**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

Vedrai poi i dati da AEP che diventano disponibili in Tableau. Fare clic su **Foglio 1** per iniziare a utilizzare i dati.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Per visualizzare i dati sulla mappa è necessario convertire longitudine e latitudine in dimensioni. In **Misure**, fare clic con il pulsante destro del mouse su **Latitudine**, selezionare **Converti in Dimension** nel menu. Ripetere l&#39;operazione per la misura **Longitudine**.

![tableau-convert-dimension.png](./images/tableauconvertdimension.png)

Trascina la misura **Longitudine** nelle **Colonne** e la misura **Latitudine** nelle **Righe**. Automaticamente la mappa di **Belgio** verrà visualizzata con piccoli punti che rappresentano le città nel set di dati.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Seleziona **Nomi misure**, fai clic su **Aggiungi al foglio**.

![tableau-select-measure-names.png](./images/selectmeasurenames.png)

Ora avrai una mappa, con punti di varie dimensioni. La dimensione indica il numero di interazioni del call center per quella città specifica. Per variare le dimensioni dei punti, passa al pannello di destra e apri **Valori di misura** (utilizzando l&#39;icona a discesa). Dall&#39;elenco a discesa selezionare **Modifica dimensioni**. Gioca con dimensioni diverse.

![tableau-vary-size-dots.png](./images/tableauvarysizedots.png)

Per visualizzare ulteriormente i dati per **Argomento chiamata**, trascina la dimensione **Argomento chiamata** in **Pagine**. Naviga tra i diversi **argomenti di chiamata** utilizzando **Argomento di chiamata** sul lato destro della schermata:

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Hai terminato questo esercizio.

## Passaggi successivi

Vai a [2.1.8 API servizio query](./ex8.md){target="_blank"}

Torna a [Servizio query](./query-service.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}

---
title: 'Query Service: esplora il set di dati con Tableau'
description: 'Query Service: esplora il set di dati con Tableau'
kt: 5342
doc-type: tutorial
exl-id: 29525740-fe1f-4770-bcc9-f2ad499a2cb5
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.7 Query Service e Tableau

Apri Tableau.

![start-tableau.png](./images/start-tableau.png)

In **Connetti a un server** selezionare **PostgreSQL**:

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Vai a Adobe Experience Platform, **Query** e **Credenziali**.

![query-service-credentials.png](./images/query-service-credentials.png)

Dalla pagina **Credenziali** in Adobe Experience Platform, copia **Host** e incollalo nel campo **Server**, copia il **Database** e incollalo nel campo **Database** in Tableau, copia la **Porta** e incollala nel campo **Porta** in Tableau, esegui le stesse operazioni per **Nome utente** e **Password**. Fare clic su **Accedi**.

Accesso:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Fai clic su Cerca (1) e immetti **ldap** nel campo di ricerca, identifica la tabella dal set di risultati e trascinala (3) nel percorso denominato **Trascina qui le tabelle**. Al termine, fare clic su **Foglio 1** (3).

![tableau-drag-table.png](./images/tableau-drag-table.png)

Per visualizzare i nostri dati sulla mappa dobbiamo convertire longitudine e latitudine in dimensioni. In **Misure** selezionare **Latitudine** (1), aprire il menu a discesa del campo e selezionare **Converti in Dimension** (2). Ripetere l&#39;operazione per la misura **Longitudine**.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

Trascina la misura **Longitudine** nelle **Colonne** e la misura **Latitudine** nelle **Righe**. Automaticamente la mappa di **Belgio** verrà visualizzata con piccoli punti che rappresentano le città nel set di dati.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Seleziona **Nomi misure** (1), apri il menu a discesa e seleziona **Aggiungi al foglio** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Ora avrai una mappa, con punti di varie dimensioni. La dimensione indica il numero di interazioni del call center per quella città specifica. Per variare le dimensioni dei punti, passa al pannello di destra e apri **Valori di misura** (utilizzando l&#39;icona a discesa). Dall&#39;elenco a discesa selezionare **Modifica dimensioni**. Gioca con dimensioni diverse.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Per visualizzare ulteriormente i dati per **Argomento chiamata**, trascina (1) la dimensione **Argomento chiamata** in **Pagine**. Naviga tra i diversi **argomenti di chiamata** utilizzando **Argomento di chiamata** (2) sul lato destro della schermata:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Hai terminato questo esercizio.

Passaggio successivo: [5.1.8 API servizio query](./ex8.md)

[Torna al modulo 5.1](./query-service.md)

[Torna a tutti i moduli](../../../overview.md)

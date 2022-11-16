---
title: Servizio query - Esplora il set di dati con Tableau
description: Servizio query - Esplora il set di dati con Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6 Query Service e Tableau

Apri Tableau.

![start-tableau.png](./images/start-tableau.png)

In **Connessione a un server** select **PostgreSQL**:

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Vai a Adobe Experience Platform, a **Query** e **Credenziali**.

![query-service-credentials.png](./images/query-service-credentials.png)

Da **Credenziali** in Adobe Experience Platform, copia la **Host** e incollalo nel **Server** campo , copia il **Database** e incollalo nel **Database** campo in Tableau, copia il **Porta** e incollarlo nel campo **Porta** a Tableau, fare lo stesso per **Nome utente** e **Password**. Quindi, fai clic su **Accesso**.

Accesso:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Fai clic su Ricerca (1) e immetti il tuo **ldap** nel campo di ricerca, identifica la tabella dal set di risultati e trascinala (3) nella posizione denominata **Trascina qui le tabelle**. Al termine, fai clic su **Foglio 1** (3)

![tableau-drag-table.png](./images/tableau-drag-table.png)

Per visualizzare i dati sulla mappa dobbiamo convertire longitudine e latitudine in dimensioni. In **Misure** select **Latitudine** (1) apri il menu a discesa del campo e seleziona **Converti in Dimension** (2) Fai lo stesso per il **Longitudine** misurare.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

Trascina **Longitudine** la misura **Colonne** e **Latitudine** misura **Righe**. Mappa automatica di **Belgio** appariranno con puntini piccoli che rappresentano le città nel set di dati fuori.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Seleziona **Nomi delle misure** (1), apri il menu a discesa e seleziona **Aggiungi al foglio** (2)

![tableau-select-measurement-names.png](./images/tableau-select-measure-names.png)

Ora avrete una mappa, con punti di varie dimensioni. La dimensione indica il numero di interazioni del call center per la città specifica. Per variare le dimensioni dei punti, accedi al pannello di destra e apri **Valori delle misure** (utilizzando l’icona a discesa). Dall’elenco a discesa seleziona **Modifica dimensioni**. Gioca con diverse dimensioni.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Per visualizzare ulteriormente i dati per **Argomento della chiamata**, trascinare (1) **Argomento della chiamata** dimensione su **Pagine**. Navigare tra le diverse **Argomenti della chiamata** utilizzando **Argomento della chiamata** (2) sul lato destro dello schermo:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Ora avete finito questo esercizio.

Passaggio successivo: [API del servizio query 4.7](./ex7.md)

[Torna al modulo 4](./query-service.md)

[Torna a tutti i moduli](../../overview.md)

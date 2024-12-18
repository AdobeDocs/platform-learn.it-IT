---
title: Intelligent Services - Preparazione dei dati di IA per l’analisi dei clienti (acquisizione)
description: 'IA per l’analisi dei clienti: preparazione dei dati (acquisizione)'
kt: 5342
doc-type: tutorial
exl-id: 71405859-cfc6-4991-a0b0-11c94818a0fa
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---

# 2.2.1 IA per l’analisi dei clienti - Preparazione dei dati (acquisizione)

Affinché Intelligent Services possa scoprire informazioni provenienti dai dati degli eventi di marketing, i dati devono essere arricchiti semanticamente e mantenuti in una struttura standard. Per ottenere questo risultato, Intelligent Services sfrutta gli schemi Experience Data Model (XDM) di Adobe.
In particolare, tutti i set di dati utilizzati in Intelligent Services devono essere conformi allo schema XDM **Consumer Experience Event**.

## Crea schema

In questo esercizio creerai uno schema contenente il mixin **Consumer Experience Event**, richiesto dal servizio intelligente **Customer AI**.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](../../datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](../../datacollection/module1.2/images/sb1.png)

Dal menu a sinistra, fai clic su **Schemi** e passa a **Sfoglia**. Fare clic su **Crea schema**.

![Crea nuovo schema](./images/createschemabutton.png)

Nel popup, selezionare **Manuale** e fare clic su **Seleziona**.

![Crea nuovo schema](./images/schmanual.png)

Quindi, seleziona **Evento esperienza** e fai clic su **Avanti**.

![Crea nuovo schema](./images/xdmee.png)

È necessario specificare un nome per lo schema. Come nome dello schema, utilizzare `--aepUserLdap-- - Demo System - Customer Experience Event` e fare clic su **Fine**.

![Crea nuovo schema](./images/schname.png)

Poi vedrai questo. Fare clic su **+ Aggiungi** in Gruppi di campi.

![Crea nuovo schema](./images/xdmee1.png)

Cerca e seleziona i **Gruppi di campi** seguenti da aggiungere a questo schema:

- Evento esperienza del consumatore
- Dettagli dell’ID dell’utente finale

Fare clic su **Aggiungi gruppi di campi**.

![Nuovo schema CEE](./images/cee.png)

Poi vedrai questo. Fare clic sul gruppo di campi **Dettagli ID utente finale**.

![Crea nuovo schema](./images/eui1.png)

Passa al campo **endUserIDs._experience.emailid.id**.

![Crea nuovo schema](./images/eui2.png)

Nel menu a destra per il campo **endUserIDs._experience.emailid.id**, scorri verso il basso e seleziona la casella di controllo per **Identità**, seleziona la casella di controllo per **Identità primaria** e seleziona **Spazio dei nomi identità** di **E-mail**. Fare clic su **Applica**.

![Crea nuovo schema](./images/eui3.png)

Passa al campo **endUserIDs._experience.mcid.id**. Selezionare la casella di controllo per **Identity** e selezionare **Identity namespace** di **ECID**. Fare clic su **Applica**.

![Crea nuovo schema](./images/eui4.png)

Allora avrai questo. Quindi, seleziona il nome dello schema. Abilitare ora lo schema per il **profilo** facendo clic sull&#39;interruttore **profilo**.

![Crea nuovo schema](./images/xdmee3.png)

Poi vedrai questo. Fare clic su **Abilita**.

![Crea nuovo schema](./images/xdmee4.png)

Ora dovresti avere questo. Fai clic su **Salva** per salvare lo schema.

![Crea nuovo schema](./images/xdmee5.png)

## Crea set di dati

Dal menu a sinistra, fai clic su **Set di dati** e passa a **Sfoglia**. Fare clic su **Crea set di dati**.

![Set di dati](./images/createds.png)

Fai clic su **Crea set di dati dallo schema**.

![Set di dati](./images/createdatasetfromschema.png)

Nella schermata successiva, seleziona il set di dati creato nell&#39;esercizio precedente, denominato **[!UICONTROL ldap - Demo System - Customer Experience Event]**. Fai clic su **Avanti**.

![Set di dati](./images/createds1.png)

Come nome per il set di dati, utilizza `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`. Fai clic su **Fine**.

![Set di dati](./images/createds2.png)

Il set di dati è stato creato. Attiva/disattiva **Profilo**.

![Set di dati](./images/createds3.png)

Fare clic su **Abilita**.

![Set di dati](./images/createds4.png)

Ora dovresti disporre di:

![Set di dati](./images/createds5.png)

Ora puoi iniziare a acquisire i dati di Consumer Experience Event e iniziare a utilizzare il servizio Customer AI.

## Scarica dati di prova di Experience Event

Una volta configurati lo **Schema** e il **Set di dati**, puoi acquisire i dati di Experience Event. Poiché IA per l&#39;analisi dei clienti richiede dati per almeno **2 trimestri**, dovrai acquisire dati preparati esternamente.

I dati preparati per gli eventi esperienza devono essere conformi ai requisiti e allo schema del [mixin XDM per evento esperienza del consumatore](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Scarica il file contenente i dati di esempio da questa posizione: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Fai clic sul pulsante **Scarica**.

![Set di dati](./images/dsn1.png)

In alternativa, se non è possibile accedere al collegamento precedente, è possibile scaricare il file anche da questa posizione: [https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip](https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip).

È stato scaricato il file **retail-v1-dec2020-xl.json.zip**. Posiziona il file sul desktop del computer e decomprimi, dopodiché visualizzerai il file denominato **retail-v1.json**. Questo file sarà necessario nell&#39;esercizio successivo.

![Set di dati](./images/ingest.png)

## Acquisire i dati di prova di Experience Event

In Adobe Experience Platform, vai a **Set di dati** e apri il set di dati, denominato **[!UICONTROL ldap - Demo System - Set di dati evento esperienza cliente]**.

![Set di dati](./images/ingest1.png)

Nel set di dati, fai clic su **Scegli i file** per aggiungere i dati.

![Set di dati](./images/ingest2.png)

Nel popup, selezionare il file **retail-v1.json** e fare clic su **Apri**.

![Set di dati](./images/ingest3.png)

Vedrai quindi i dati in fase di importazione e verrà creato un nuovo batch nello stato **Caricamento**. Non allontanarti da questa pagina finché il file non viene caricato.

![Set di dati](./images/ingest4.png)

Una volta caricato il file, lo stato del batch passerà da **Caricamento** a **Elaborazione**.

![Set di dati](./images/ingest5.png)

L’acquisizione e l’elaborazione dei dati potrebbero richiedere 10-20 minuti.

Una volta completata l&#39;acquisizione dei dati, lo stato del batch passerà a **Operazione completata**.

![Set di dati](./images/ingest7.png)

![Set di dati](./images/ingest8.png)

Passaggio successivo: [2.2.2 Customer AI - Crea una nuova istanza (Configura)](./ex2.md)

[Torna al modulo 2.2](./intelligent-services.md)

[Torna a tutti i moduli](./../../../overview.md)

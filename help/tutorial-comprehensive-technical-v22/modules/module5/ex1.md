---
title: Servizi intelligenti - Preparazione dei dati di Customer AI (Ingest)
description: Customer AI - Preparazione dei dati (acquisizione)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 60996e70-b033-4932-b614-b37014232f6e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# 5.1 Customer AI - Preparazione dei dati (acquisizione)

Affinché i servizi intelligenti possano scoprire informazioni dai dati degli eventi di marketing, i dati devono essere arricchiti e mantenuti in una struttura standard in modo semantico. Per ottenere questo risultato, Intelligent Services sfrutta gli schemi Experience Data Model (XDM) di Adobe.
In particolare, tutti i set di dati utilizzati in Intelligent Services devono essere conformi alla **Evento esperienza consumatore** Schema XDM.

## 5.1.1 Creare uno schema

In questo esercizio, creerai uno schema che contiene **Mixin evento esperienza consumatore**, richiesto dalla **Customer AI** Servizio intelligente

Accedi a Adobe Experience Platform andando a questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--module10sandbox--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato la sandbox appropriata, visualizzerai la modifica dello schermo e ora ti trovi nella sandbox dedicata.

![Acquisizione dei dati](../module2/images/sb1.png)

Dal menu a sinistra, fai clic su **Schemi** e vai a **Sfoglia**. Fai clic su **Crea schema**.

![Crea nuovo schema](./images/create-schema-button.png)

Nella finestra a comparsa, seleziona **ExperienceEvent XDM**.

![Crea nuovo schema](./images/xdmee.png)

Vedrete questo.

![Crea nuovo schema](./images/xdmee1.png)

Cerca e seleziona quanto segue **Mixins** per aggiungere a questo schema:

- Evento esperienza consumatore

   ![Nuovo schema CEE](./images/cee.png)

- Dettagli ID utente finale

   ![Nuovo schema CEE](./images/identitymap.png)

Fai clic su **Aggiungi gruppi di campi**.

![Definizione chiave di identità](./images/addmixin.png)

Vedrete questo. Selezionare il mixin **Dettagli ID utente finale**.

![Crea nuovo schema](./images/eui1.png)

Passa al campo . **endUserIDs._experience.emailid.id**.

![Crea nuovo schema](./images/eui2.png)

Nel menu a destra del campo **endUserIDs._experience.emailid.id**, scorri verso il basso e seleziona la casella di controllo **Identità**, seleziona la casella di controllo **Identità principale** e seleziona la **Spazio dei nomi identità** di **E-mail**.

![Crea nuovo schema](./images/eui3.png)

Passa al campo . **endUserIDs._experience.mcid.id**. Seleziona la casella di controllo per **Identità** e seleziona la **Spazio dei nomi identità** di **ECID**. Fai clic su **Applica**.

![Crea nuovo schema](./images/eui4.png)

Assegna un nome allo schema.

Come nome del nostro schema, utilizzerai questo:

- `--demoProfileLdap-- - Demo System - Customer Experience Event`

Ad esempio, per ldap **vangeluw**, deve essere il nome dello schema:

- **vangeluw - Demo System - Customer Experience Event**

Dovrebbe darvi qualcosa del genere. Fai clic sul pulsante **+ Aggiungi** pulsante per aggiungere nuovo **Mixins**.

![Crea nuovo schema](./images/xdmee2.png)

Seleziona il nome dello schema. A questo punto, abilita lo schema per **Profilo**, facendo clic sul pulsante **Profilo** alternare.

![Crea nuovo schema](./images/xdmee3.png)

Vedrete questo. Fai clic su **Abilita**.

![Crea nuovo schema](./images/xdmee4.png)

Dovrebbe avere questo ora. Fai clic su **Salva** per salvare lo schema.

![Crea nuovo schema](./images/xdmee5.png)

## 5.1.2 Creare un set di dati

Dal menu a sinistra, fai clic su **Set di dati** e vai a **Sfoglia**. Fai clic su **Creare un set di dati**.

![Set di dati](./images/createds.png)

Fai clic su **Creare un set di dati dallo schema**.

![Set di dati](./images/createdatasetfromschema.png)

Nella schermata successiva, seleziona il set di dati creato nell’esercizio precedente, denominato **[!UICONTROL ldap - Demo System - Evento esperienza cliente]**. Fai clic su **Avanti**.

![Set di dati](./images/createds1.png)

Come nome per il set di dati, utilizza `--demoProfileLdap-- - Demo System - Customer Experience Event Dataset`. Fai clic su **Fine**.

![Set di dati](./images/createds2.png)

Il set di dati viene ora creato. Abilita la **Profilo** alternare.

![Set di dati](./images/createds3.png)

Fai clic su **Abilita**.

![Set di dati](./images/createds4.png)

Ora dovresti avere questo:

![Set di dati](./images/createds5.png)

Ora puoi iniziare a acquisire i dati dell’evento esperienza del consumatore e a utilizzare il servizio Customer AI.

## 5.1.3 Scaricare i dati del test di Experience Event

Una volta che **Schema** e **Set di dati** Sono configurati, ora sei pronto per acquisire i dati di Experience Event. Poiché Customer AI richiede dati attraverso **almeno 2 quarti**, dovrai inserire dati preparati esternamente.

I dati preparati per gli eventi di esperienza devono essere conformi ai requisiti e allo schema del [Mixin XDM evento esperienza consumatore](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Scarica il file contenente i dati di esempio da questa posizione: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Fai clic sul pulsante **Scarica** pulsante .

![Set di dati](./images/dsn1.png)

Ora hai scaricato un file denominato **retail-v1-dec2020-xl.json.zip**. Posizionare il file sul desktop del computer e decomprimerlo, dopodiché verrà visualizzato un file denominato **retail-v1.json**. Avrai bisogno di questo file nel prossimo esercizio.

![Set di dati](./images/ingest.png)

## 5.1.4 Dati del test dell’esperienza di acquisizione

In Adobe Experience Platform, vai a **Set di dati** e apri il set di dati, denominato **[!UICONTROL ldap - Sistema di demo - Dataset dell’evento di esperienza del cliente]**.

![Set di dati](./images/ingest1.png)

Nel set di dati, fai clic su **Scegliere i file** per aggiungere dati.

![Set di dati](./images/ingest2.png)

Nella finestra a comparsa, seleziona il file **retail-v1.json** e fai clic su **Apri**.

![Set di dati](./images/ingest3.png)

Verranno quindi visualizzati i dati importati e verrà creato un nuovo batch nel **Caricamento** stato. Non allontanarti da questa pagina fino a quando il file non viene caricato.

![Set di dati](./images/ingest4.png)

Una volta caricato il file, lo stato del batch cambia da **Caricamento** a **Elaborazione**.

![Set di dati](./images/ingest5.png)

L’assimilazione ed elaborazione dei dati potrebbe richiedere 10-20 minuti.

Una volta completata l’acquisizione dei dati, lo stato del batch cambia in **Completato**.

![Set di dati](./images/ingest7.png)

![Set di dati](./images/ingest8.png)

Passaggio successivo: [5.2 Customer AI - Creare una nuova istanza (Configura)](./ex2.md)

[Torna al modulo 5](./intelligent-services.md)

[Torna a tutti i moduli](./../../overview.md)

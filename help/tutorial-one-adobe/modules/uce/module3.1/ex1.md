---
title: Raccolta dati - FAC - Configurare l’account di Snowflake
description: Foundation - FAC - Configurare l’account di Snowflake
kt: 5342
doc-type: tutorial
exl-id: e72cdbfc-5b42-411f-9c63-e886776deabe
source-git-commit: d26d4735c92498d56beb7859ec67a0c3e174fc25
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 3.1.1 Configurare l’ambiente del Snowflake

## 3.1.1.1 Creare l’account

Vai a [https://snowflake.com](https://snowflake.com). Fai clic su **INIZIA GRATUITAMENTE**.

![FAC](./images/sf1.png)

Immetti i tuoi dettagli e fai clic su **Continua**.

![FAC](./images/sf2.png)

Immetti i tuoi dettagli, scegli il provider di cloud e fai clic su **Inizia**.

![FAC](./images/sf3.png)

Inserisci i tuoi dettagli o fai clic su **Ignora** (x2).

![FAC](./images/sf4.png)

Poi vedrai questo. Controlla l’e-mail e fai clic sull’e-mail di conferma che ti è stata inviata.

![FAC](./images/sf5.png)

Fai clic sul collegamento nell’e-mail di conferma per attivare l’account, definire il nome utente e la password. Fai clic su **Inizia**. Nel prossimo esercizio dovrai usare questo nome utente e questa password.

![FAC](./images/sf6.png)

In seguito potrai accedere al Snowflake. Fai clic su **Ignora per il momento**.

![FAC](./images/sf7.png)

## 3.1.1.2 Creare il database

Vai a **Dati > Database**. Fare clic su **+ Database**.

![FAC](./images/db1.png)

Utilizza il nome **CITISIGNAL** per il database. Fare clic su **CREA**.

![FAC](./images/db2.png)

## 3.1.1.3 Creare le tabelle

È ora possibile iniziare a creare le tabelle in Snowflake. Di seguito sono riportati gli script da eseguire per creare le tabelle.

### Tabella CK_PERSONS

Fare clic su **+ Crea**, quindi su **Tabella** e infine su **Standard**.

![FAC](./images/tb1.png)

Poi vedrai questo. Copia la query seguente e incollala nel Snowflake. Prima di creare la tabella, assicurati di selezionare il database **CITISIGNAL** nell&#39;angolo in alto a sinistra dello schermo.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_PERSONS (
	PERSON_ID NUMBER(38,0) NOT NULL,
	NAME VARCHAR(255),
	AGE NUMBER(38,0),
	EMAIL VARCHAR(255),
	PHONE_NUMBER VARCHAR(20),
	GENDER VARCHAR(10),
	OCCUPATION VARCHAR(100),
	ISATTMOBILESUB BOOLEAN,
	primary key (PERSON_ID)
);
```

Fare clic su **Crea tabella**.

![FAC](./images/tb2.png)

Una volta eseguito lo script, è possibile trovare la tabella in **Database > CITISIGNAL > PUBLIC**.

![FAC](./images/tb3.png)

### Tabella CK_HOUSEHOLDS

Fare clic su **+ Crea**, quindi su **Tabella** e infine su **Standard**.

![FAC](./images/tb1.png)

Poi vedrai questo. Copia la query seguente e incollala nel Snowflake. Prima di creare la tabella, assicurati di selezionare il database **CITISIGNAL** nell&#39;angolo in alto a sinistra dello schermo.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_HOUSEHOLDS (
	HOUSEHOLD_ID NUMBER(38,0) NOT NULL,
	ADDRESS VARCHAR(255),
	CITY VARCHAR(100),
	STATE VARCHAR(50),
	POSTAL_CODE VARCHAR(20),
	COUNTRY VARCHAR(100),
	ISELIGIBLEFORFIBER BOOLEAN,
	PRIMARY_PERSON_ID NUMBER(38,0),
	ISFIBREENABLED BOOLEAN,
	primary key (HOUSEHOLD_ID)
);
```

Fare clic su **Crea tabella**.

![FAC](./images/tb4.png)

Una volta eseguito lo script, è possibile trovare la tabella in **Database > CITISIGNAL > PUBLIC**.

![FAC](./images/tb5.png)

### Tabella CK_USERS

Fare clic su **+ Crea**, quindi su **Tabella** e infine su **Standard**.

![FAC](./images/tb1.png)

Poi vedrai questo. Copia la query seguente e incollala nel Snowflake. Prima di creare la tabella, assicurati di selezionare il database **CITISIGNAL** nell&#39;angolo in alto a sinistra dello schermo.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_USERS (
	USER_ID NUMBER(38,0) NOT NULL,
	PERSON_ID NUMBER(38,0),
	HOUSEHOLD_ID NUMBER(38,0),
	primary key (USER_ID),
	foreign key (PERSON_ID) references CITISIGNAL.PUBLIC.CK_PERSONS(PERSON_ID),
	foreign key (HOUSEHOLD_ID) references CITISIGNAL.PUBLIC.CK_HOUSEHOLDS(HOUSEHOLD_ID)
);
```

Fare clic su **Crea tabella**.

![FAC](./images/tb6.png)

Una volta eseguito lo script, è possibile trovare la tabella in **Database > CITISIGNAL > PUBLIC**.

![FAC](./images/tb7.png)

### Tabella CK_MONTHLY_DATA_USAGE

Fare clic su **+ Crea**, quindi su **Tabella** e infine su **Standard**.

![FAC](./images/tb1.png)

Poi vedrai questo. Copia la query seguente e incollala nel Snowflake. Prima di creare la tabella, assicurati di selezionare il database **CITISIGNAL** nell&#39;angolo in alto a sinistra dello schermo.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MONTHLY_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	MONTH DATE,
	DATA_USAGE_GB NUMBER(10,2),
	primary key (USAGE_ID)
);
```

Fare clic su **Crea tabella**.

![FAC](./images/tb8.png)

Una volta eseguito lo script, è possibile trovare la tabella in **Database > CITISIGNAL > PUBLIC**.

![FAC](./images/tb9.png)

### Tabella CK_MOBILE_DATA_USAGE

Fare clic su **+ Crea**, quindi su **Tabella** e infine su **Standard**.

![FAC](./images/tb1.png)

Poi vedrai questo. Copia la query seguente e incollala nel Snowflake. Prima di creare la tabella, assicurati di selezionare il database **CITISIGNAL** nell&#39;angolo in alto a sinistra dello schermo.


```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MOBILE_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	DATE DATE,
	TIME TIME(9),
	APP_NAME VARCHAR(255),
	DATA_USAGE_MB NUMBER(10,2),
	NETWORK_TYPE VARCHAR(50),
	DEVICE_TYPE VARCHAR(50),
	COUNTRY_CODE VARCHAR(10),
	primary key (USAGE_ID)
);
```

Fare clic su **Crea tabella**.

![FAC](./images/tb10.png)

Una volta eseguito lo script, è possibile trovare la tabella in **Database > CITISIGNAL > PUBLIC**.

![FAC](./images/tb11.png)

Tutte le tabelle sono state create.


## 3.1.1.4 Inserire i dati del campione

Ora puoi iniziare a caricare dati di esempio nel database.

...

La configurazione è stata completata in Snowflake.


Passaggio successivo: [3.1.2 Creare schemi, modelli dati e collegamenti](./ex2.md)

[Torna al modulo 3.1](./fac.md)

[Torna a tutti i moduli](../../../overview.md)

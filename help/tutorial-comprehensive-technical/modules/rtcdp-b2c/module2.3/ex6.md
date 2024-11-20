---
title: Real-time CDP - Pubblico esterno
description: Real-time CDP - Pubblico esterno
kt: 5342
doc-type: tutorial
exl-id: c7e4960f-4007-4c27-b5ba-7b21cd52c2f7
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# 2.3.6 Pubblico esterno

In molti casi, la tua azienda potrebbe voler utilizzare i tipi di pubblico esistenti di altre applicazioni per arricchire il profilo cliente in Adobe Experience Platform.
Tali tipi di pubblico esterni possono essere stati definiti in base a un modello di scienza dei dati o utilizzando piattaforme di dati esterne.

La funzione dei tipi di pubblico esterni di Adobe Experience Platform consente di concentrarsi sull’acquisizione dei tipi di pubblico esterni e sulla loro attivazione senza dover ridefinire in dettaglio la definizione del pubblico corrispondente in Adobe Experience Platform.

Il processo complessivo si articola in tre fasi principali:

- Importare i metadati del pubblico esterno: questo passaggio ha lo scopo di acquisire in Adobe Experience Platform i metadati del pubblico esterno, come il nome del pubblico.
- Assegnare la appartenenza al pubblico esterno al profilo cliente: questo passaggio ha lo scopo di arricchire il profilo cliente con l’attributo di appartenenza al pubblico esterno.
- Creare i tipi di pubblico in Adobe Experience Platform: questo passaggio ha lo scopo di creare tipi di pubblico utilizzabili in base all’iscrizione a tipi di pubblico esterni.

## Metadati

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

>[!IMPORTANT]
>
>La sandbox da utilizzare per questo esercizio è ``--aepSandboxName--``.

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./images/sb1.png)

Mentre i dati sul pubblico definiscono la condizione affinché un profilo faccia parte di un pubblico, i metadati del pubblico sono informazioni sul pubblico, come il nome, la descrizione e lo stato del pubblico. Poiché i metadati dei tipi di pubblico esterni verranno memorizzati in Adobe Experience Platform, è necessario utilizzare uno spazio dei nomi delle identità per acquisire i metadati in Adobe Experience Platform.

## 2.3.6.1.1 Namespace Identity per tipi di pubblico esterni

È già stato creato uno spazio dei nomi delle identità per l&#39;utilizzo con **tipi di pubblico esterni**.
Per visualizzare l&#39;identità già creata, passa a **Identità** e cerca **Esterna**. Fai clic sull’elemento &quot;Pubblico esterno&quot;.

Nota:

- Il simbolo di identità **externalaudiences** verrà utilizzato nei passaggi successivi per fare riferimento all&#39;identità dei tipi di pubblico esterni.
- Per questo spazio dei nomi delle identità viene utilizzato il tipo **Identificatore non persone**, in quanto questo spazio dei nomi non è destinato a identificare i profili dei clienti ma i tipi di pubblico.

![Identità pubblico esterno](images/extAudIdNS.png)

## 2.3.6.1.2 Creare lo schema metadati per tipi di pubblico esterni

I metadati dei tipi di pubblico esterni si basano sullo **schema di definizione del pubblico**. Ulteriori dettagli sono disponibili nell&#39;archivio Github [XDM](https://github.com/adobe/xdm/blob/master/docs/reference/classes/segmentdefinition.schema.md).

Nel menu a sinistra, vai a Schemi. Fare clic su **+ Crea schema** e quindi su **Sfoglia**.

![Schema metadati tipi di pubblico esterni 1](images/extAudMDXDM1.png)

Per assegnare una classe, cerca **definizione pubblico**. Seleziona la classe **Definizione pubblico** e fai clic su **Assegna classe**.

![Schema metadati tipi di pubblico esterni 2](images/extAudMDXDM2.png)

Poi vedrai questo. Fare clic su **Annulla**.

![Schema metadati tipi di pubblico esterni 3](images/extAudMDXDM3.png)

Poi vedrai questo. Seleziona il campo **_id**. Nel menu di destra, scorri verso il basso e abilita le caselle di controllo **Identità** e **Identità primaria**. Seleziona lo spazio dei nomi dell&#39;identità **Tipi di pubblico esterni**. Fare clic su **Applica**.

![Schema metadati tipi di pubblico esterni 4](images/extAudMDXDM4.png)

Selezionare quindi il nome dello schema **Schema senza titolo**. Cambia il nome in `--aepUserLdap-- - External Audiences Metadata`.

![Schema metadati tipi di pubblico esterni 5](images/extAudMDXDM5.png)

Attiva/disattiva **Profilo** e conferma. Infine, fare clic su **Salva**.

![Schema metadati tipi di pubblico esterni 5](images/extAudMDXDM6.png)

## 2.3.6.1.3 Creare il set di dati dei metadati dei tipi di pubblico esterni

In **Schemi**, passa a **Sfoglia**. Cerca e fai clic sullo schema `--aepUserLdap-- - External Audiences Metadata` creato nel passaggio precedente. Fare clic su **Crea set di dati dallo schema**.

![Servizi di dominio pubblico esterno - Metadati DS 1](images/extAudMDDS1.png)

Per il campo **Nome**, immettere `--aepUserLdap-- - External Audience Metadata`. Fare clic su **Crea set di dati**.

![Servizi di dominio pubblico esterno - Metadati DS 2](images/extAudMDDS2.png)

Poi vedrai questo. Non dimenticare di abilitare l&#39;interruttore **Profilo**.

![Servizi di dominio pubblico esterno - Metadati DS 3](images/extAudMDDS3.png)

## 2.3.6.1.4 Creare una connessione HTTP API Source

Successivamente, devi configurare il connettore Source API HTTP che utilizzerai per acquisire i metadati nel set di dati.

Vai a **Origini**. Nel campo di ricerca immettere **HTTP**. Fare clic su **Aggiungi dati**.

![Metadati tipi di pubblico esterni http 1](images/extAudMDhttp1.png)

Immettere le seguenti informazioni:

- **Tipo di account**: seleziona **Nuovo account**
- **Nome account**: immettere `--aepUserLdap-- - External Audience Metadata`
- Seleziona la casella di controllo **casella compatibile con XDM**

Fare clic su **Connetti all&#39;origine**.

![Metadati tipi di pubblico esterni http 2](images/extAudMDhttp2.png)

Poi vedrai questo. Fai clic su **Avanti**.

![Metadati tipi di pubblico esterni http 2](images/extAudMDhttp2a.png)

Selezionare **Set di dati esistente** e nel menu a discesa cercare e selezionare il set di dati `--aepUserLdap-- - External Audience Metadata`.

Verificare i **dettagli del flusso di dati**, quindi fare clic su **Avanti**.

![Metadati tipi di pubblico esterni http 3](images/extAudMDhttp3.png)

Poi vedrai questo.

Il passaggio **Mappatura** della procedura guidata è vuoto perché verrà acquisito un payload conforme a XDM nel connettore Source API HTTP, quindi non è richiesta alcuna mappatura. Fai clic su **Avanti**.

![Metadati tipi di pubblico esterni http 3](images/extAudMDhttp3a.png)

Nel passaggio **Rivedi** puoi facoltativamente rivedere la connessione e i dettagli di mappatura. Fai clic su **Fine**.

![Metadati tipi di pubblico esterni http 4](images/extAudMDhttp4.png)

Poi vedrai questo.

![Metadati tipi di pubblico esterni http 4](images/extAudMDhttp4a.png)

## 2.3.6.1.5 Acquisizione dei metadati di tipi di pubblico esterni

Nella scheda Panoramica di Source Connector, fare clic su **...** e quindi su **Copia payload schema**.

![Str metadati tipi di pubblico esterni 1](images/extAudMDstr1a.png)

Apri l’applicazione Editor di testo sul computer e incolla il payload appena copiato, che si presenta così. Successivamente, devi aggiornare l&#39;oggetto **xdmEntity** in questo payload.

![Str metadati tipi di pubblico esterni 1](images/extAudMDstr1b.png)

L&#39;oggetto **xdmEntity** deve essere sostituito dal codice seguente. Copiare il codice seguente e incollarlo nel file di testo sostituendo l&#39;oggetto **xdmEntity** nell&#39;editor di testo.

```
"xdmEntity": {
    "_id": "--aepUserLdap---extaudience-01",
    "description": "--aepUserLdap---extaudience-01 description",
    "segmentIdentity": {
      "_id": "--aepUserLdap---extaudience-01",
      "namespace": {
        "code": "externalaudiences"
      }
    },
    "segmentName": "--aepUserLdap---extaudience-01 name",
    "segmentStatus": "ACTIVE",
    "version": "1.0"
  }
```

Dovresti quindi vedere quanto segue:

![Str metadati tipi di pubblico esterni 1](images/extAudMDstr1.png)

Aprire quindi una nuova finestra **Terminal**. Copiate tutto il testo nell&#39;Editor di testo e incollatelo nella finestra del terminale.

![Str metadati tipi di pubblico esterni 1](images/extAudMDstr1d.png)

Quindi, premi **Invio**.

Nella finestra Terminal viene quindi visualizzata una conferma dell’inserimento dei dati:

![Str metadati tipi di pubblico esterni 1](images/extAudMDstr1e.png)

Aggiorna la schermata del connettore Source API HTTP, in cui ora vedrai che i dati sono in fase di elaborazione:

![Str metadati pubblico esterno 2](images/extAudMDstr2.png)

## 2.3.6.1.6 Convalidare l’acquisizione dei metadati di tipi di pubblico esterni

Al termine dell’elaborazione, puoi verificare la disponibilità dei dati nel set di dati utilizzando Query Service.

Nel menu a destra, vai a **Set di dati** e seleziona il set di dati `--aepUserLdap-- - External Audience Metadata` creato in precedenza.

![Str metadati pubblico esterno 3](images/extAudMDstr3.png)

Nel menu di destra, vai a Query e fai clic su **Crea query**.

![Str metadati tipi di pubblico esterni 4](images/extAudMDstr4.png)

Immetti il seguente codice, quindi premi **MAIUSC + INVIO**:

```
select * from --aepUserLdap--_external_audience_metadata
```

Nei risultati della query verranno visualizzati i metadati del pubblico esterno che hai acquisito.

![Str metadati pubblico esterno 5](images/extAudMDstr5.png)

## Iscrizione al pubblico

Con i metadati del pubblico esterno disponibili, ora puoi acquisire l’iscrizione del pubblico per un profilo cliente specifico.

Ora devi preparare un set di dati di profilo arricchito in base allo schema di iscrizione al pubblico. Ulteriori dettagli sono disponibili nell&#39;archivio Github [XDM](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/segmentmembership.schema.md).

### Creare lo schema di appartenenza dei tipi di pubblico esterni

Nel menu a destra, vai a **Schemi**. Fare clic su **Crea schema** e quindi su **Profilo individuale XDM**.

![Schema del profilo di tipi di pubblico esterni 1](images/extAudPrXDM1.png)

Nel popup **Aggiungi gruppi di campi**, cerca **Core profilo**. Seleziona il gruppo di campi **Core profilo v2**.

![Schema profilo pubblico esterno 2](images/extAudPrXDM2.png)

Quindi, nel popup **Aggiungi gruppi di campi**, cerca **Appartenenza al segmento**. Selezionare il gruppo di campi **Dettagli appartenenza al segmento**. Fare clic su **Aggiungi gruppi di campi**.

![Schema profilo pubblico esterno 3](images/extAudPrXDM3.png)

Poi vedrai questo. Passare al campo `--aepTenantId--.identification.core`. Fai clic sul campo **crmId**. Nel menu di destra, scorri verso il basso e seleziona le caselle di controllo **Identità** e **Identità primaria**. Per lo spazio dei nomi **Identity**, seleziona **Sistema demo - CRMID**.

Fare clic su **Applica**.

![Schema del profilo di tipi di pubblico esterni 4](images/extAudPrXDM4.png)

Selezionare quindi il nome dello schema **Schema senza titolo**. Nel campo del nome visualizzato, immettere `--aepUserLdap-- - External Audiences Membership`.

![Schema profilo pubblico esterno 5](images/extAudPrXDM5a.png)

Quindi, abilita il **Profilo** e conferma. Fai clic su **Salva**.

![Schema profilo pubblico esterno 5](images/extAudPrXDM5.png)

### Creare il set di dati Appartenenza a tipi di pubblico esterni

In **Schemi**, passa a **Sfoglia**. Cerca e fai clic sullo schema `--aepUserLdap-- - External Audiences Membership` creato nel passaggio precedente. Fare clic su **Crea set di dati dallo schema**.

![Servizi di dominio pubblico esterno - Metadati DS 1](images/extAudPrDS1.png)

Per il campo **Nome**, immettere `--aepUserLdap-- - External Audiences Membership`. Fare clic su **Crea set di dati**.

![Servizi di dominio pubblico esterno - Metadati DS 2](images/extAudPrDS2.png)

Poi vedrai questo. Non dimenticare di abilitare l&#39;interruttore **Profilo**.

![Servizi di dominio pubblico esterno - Metadati DS 3](images/extAudPrDS3.png)

### Creare una connessione Source API HTTP


Successivamente, devi configurare il connettore Source API HTTP che utilizzerai per acquisire i metadati nel set di dati.

Vai a **Origini**. Nel campo di ricerca immettere **HTTP**. Fare clic su **Aggiungi dati**.

![Metadati tipi di pubblico esterni http 1](images/extAudMDhttp1.png)

Immettere le seguenti informazioni:

- **Tipo di account**: seleziona **Nuovo account**
- **Nome account**: immettere `--aepUserLdap-- - External Audience Membership`
- Seleziona la casella di controllo **casella compatibile con XDM**

Fare clic su **Connetti all&#39;origine**.

![Metadati tipi di pubblico esterni http 2](images/extAudPrhttp2.png)

Poi vedrai questo. Fai clic su **Avanti**.

![Metadati tipi di pubblico esterni http 2](images/extAudPrhttp2a.png)

Selezionare **Set di dati esistente** e nel menu a discesa cercare e selezionare il set di dati `--aepUserLdap-- - External Audiences Membership`.

Verificare i **dettagli del flusso di dati**, quindi fare clic su **Avanti**.

![Metadati tipi di pubblico esterni http 3](images/extAudPrhttp3.png)

Poi vedrai questo.

Il passaggio **Mappatura** della procedura guidata è vuoto perché verrà acquisito un payload conforme a XDM nel connettore Source API HTTP, quindi non è richiesta alcuna mappatura. Fai clic su **Avanti**.

![Metadati tipi di pubblico esterni http 3](images/extAudPrhttp3a.png)

Nel passaggio **Rivedi** puoi facoltativamente rivedere la connessione e i dettagli di mappatura. Fai clic su **Fine**.

![Metadati tipi di pubblico esterni http 4](images/extAudPrhttp4.png)

Poi vedrai questo.

![Metadati tipi di pubblico esterni http 4](images/extAudPrhttp4a.png)

### Acquisizione dei dati di appartenenza a tipi di pubblico esterni

Nella scheda Panoramica di Source Connector, fare clic su **...** e quindi su **Copia payload schema**.

![Str metadati tipi di pubblico esterni 1](./images/extAudPrstr1a.png)

Apri l’applicazione Editor di testo sul computer e incolla il payload appena copiato, che si presenta così. Successivamente, devi aggiornare l&#39;oggetto **xdmEntity** in questo payload.

![Str metadati tipi di pubblico esterni 1](images/extAudPrstr1b.png)

L&#39;oggetto **xdmEntity** deve essere sostituito dal codice seguente. Copiare il codice seguente e incollarlo nel file di testo sostituendo l&#39;oggetto **xdmEntity** nell&#39;editor di testo.

```
  "xdmEntity": {
    "_id": "--aepUserLdap---profile-test-01",
    "_experienceplatform": {
      "identification": {
        "core": {
          "crmId": "--aepUserLdap---profile-test-01"
        }
      }
    },
    "personID": "--aepUserLdap---profile-test-01",
    "segmentMembership": {
      "externalaudiences": {
        "--aepUserLdap---extaudience-01": {
          "status": "realized",
          "lastQualificationTime": "2022-03-05T00:00:00Z"
        }
      }
    }
  }
```

Dovresti quindi vedere quanto segue:

![Str metadati tipi di pubblico esterni 1](images/extAudPrstr1.png)

Aprire quindi una nuova finestra **Terminal**. Copiate tutto il testo nell&#39;Editor di testo e incollatelo nella finestra del terminale.

![Str metadati tipi di pubblico esterni 1](images/extAudPrstr1d.png)

Quindi, premi **Invio**.

Nella finestra Terminal viene quindi visualizzata una conferma dell’inserimento dei dati:

![Str metadati tipi di pubblico esterni 1](images/extAudPrstr1e.png)

Aggiorna la schermata del connettore Source API HTTP, in cui dopo un paio di minuti vedrai che i dati vengono elaborati:

![Str metadati pubblico esterno 2](images/extAudPrstr2.png)

### Convalidare l’acquisizione dell’appartenenza a tipi di pubblico esterni

Al termine dell’elaborazione, puoi verificare la disponibilità dei dati nel set di dati utilizzando Query Service.

Nel menu a destra, vai a **Set di dati** e seleziona il set di dati `--aepUserLdap-- - External Audiences Membership ` creato in precedenza.

![Str metadati pubblico esterno 3](images/extAudPrstr3.png)

Nel menu di destra, vai a Query e fai clic su **Crea query**.

![Str metadati tipi di pubblico esterni 4](images/extAudPrstr4.png)

Immetti il seguente codice, quindi premi **MAIUSC + INVIO**:

```
select * from --aepUserLdap--_external_audiences_membership
```

Nei risultati della query verranno visualizzati i metadati del pubblico esterno che hai acquisito.

![Str metadati pubblico esterno 5](images/extAudPrstr5.png)

## Crea un segmento

Ora sei pronto a intervenire sui tipi di pubblico esterni.
In Adobe Experience Platform l’azione si ottiene creando segmenti, popolando i rispettivi tipi di pubblico e condividendoli con le destinazioni.
Ora creerai un segmento utilizzando il pubblico esterno appena creato.

Nel menu a sinistra, vai a **Segmenti** e fai clic su **Crea segmento**.

![SegBuilder tipi di pubblico esterni 1](images/extAudSegUI2.png)

Vai a **Tipi di pubblico**. Poi vedrai questo. Fai clic su **Tipi di pubblico esterni**.

![SegBuilder tipi di pubblico esterni 1](images/extAudSegUI2a.png)

Selezionare il pubblico esterno creato in precedenza, denominato `--aepUserLdap---extaudience-01`. Trascina e rilascia il pubblico nell’area di lavoro.

![SegBuilder tipi di pubblico esterni 1](images/extAudSegUI2b.png)

Assegna un nome al segmento e utilizza `--aepUserLdap-- - extaudience-01`. Fare clic su **Salva e chiudi**.

![SegBuilder tipi di pubblico esterni 1](images/extAudSegUI1.png)

Poi vedrai questo. Noterai inoltre che il profilo per il quale hai acquisito l&#39;appartenenza al segmento ora viene visualizzato nell&#39;elenco dei **Profili di esempio**.

![SegBuilder tipi di pubblico esterni 1](images/extAudSegUI3.png)

Il segmento è pronto ora e può essere inviato a una destinazione per l’attivazione.

## Visualizzare il profilo cliente

Ora puoi anche visualizzare la qualifica del segmento sul tuo profilo cliente. Vai a **Profili**, utilizza lo spazio dei nomi delle identità **Sistema demo - CRMID** e fornisci l&#39;identità `--aepUserLdap---profile-test-01`, che hai utilizzato come parte dell&#39;esercizio 6.6.2.4, quindi fai clic su **Visualizza**. Fare quindi clic su **ID profilo** per aprire il profilo.

![SegBuilder tipi di pubblico esterni 1](images/extAudProfileUI1.png)

Vai a **Iscrizione al segmento**, dove verrà visualizzato il pubblico esterno.

![SegBuilder tipi di pubblico esterni 1](images/extAudProfileUI2.png)

Passaggio successivo: [2.3.7 Destinazioni SDK](./ex7.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)

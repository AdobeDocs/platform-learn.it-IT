---
title: 'Customer Journey Analytics: connettere i set di dati di Adobe Experience Platform nel Customer Journey Analytics'
description: 'Customer Journey Analytics: connettere i set di dati di Adobe Experience Platform nel Customer Journey Analytics'
kt: 5342
doc-type: tutorial
exl-id: 96e7a5b2-9833-430a-8eab-27651a113675
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# 4.1.2 Collegare i set di dati di Adobe Experience Platform nel Customer Journey Analytics

## Obiettivi

- Interfaccia utente di Data Connection
- Inserire dati Adobe Experience Platform in CJA
- Comprendere l’unione di ID persona e dati
- Scopri il concetto di streaming dei dati nel Customer Journey Analytics

## 4.1.2.1 Connessione

Vai a [analytics.adobe.com](https://analytics.adobe.com) per accedere al Customer Journey Analytics.

Nella home page del Customer Journey Analytics, vai a **Connessioni**.

![demo](./images/cja2.png)

Qui puoi vedere tutte le diverse connessioni effettuate tra CJA e Platform. Queste connessioni hanno lo stesso obiettivo delle suite di rapporti in Adobe Analytics. Tuttavia, la raccolta dei dati è totalmente diversa. Tutti i dati provengono dai set di dati di Adobe Experience Platform.

Crea la prima connessione. Fare clic su **Crea nuova connessione**.

![demo](./images/cja4.png)

Verrà visualizzata l&#39;interfaccia utente **Crea connessione**.

![demo](./images/cja5.png)

Ora puoi assegnare un nome alla connessione.

Utilizzare questa convenzione di denominazione: `--aepUserLdap-- – Omnichannel Data Connection`.

È inoltre necessario selezionare la sandbox corretta da utilizzare. Nel menu sandbox, seleziona la sandbox, che dovrebbe essere `--aepSandboxName--`. In questo esempio, la sandbox è **Tech Insiders**. È inoltre necessario impostare il **numero medio di eventi giornalieri** su **meno di 1 milione**.

![demo](./images/cjasb.png)

Dopo aver selezionato la sandbox, puoi iniziare ad aggiungere i set di dati. Fare clic su **Aggiungi set di dati**.

![demo](./images/cjasb1.png)

## 4.1.2.2 Seleziona set di dati Adobe Experience Platform

Cercare il set di dati `Demo System - Event Dataset for Website (Global v1.1)`. Abilita la casella per questo set di dati per aggiungerlo a questa connessione.

![demo](./images/cja7.png)

Rimani nella stessa schermata, quindi cerca e seleziona la casella di controllo per `Demo System - Event Dataset for Call Center (Global v1.1)`.

Allora avrai questo. Fai clic su **Avanti**.

![demo](./images/cja9.png)

## 4.1.2.3 ID persona e unione dei dati

### ID persona

L’obiettivo ora è unire questi set di dati. Per ogni set di dati selezionato, verrà visualizzato un campo denominato **ID persona**. Ogni set di dati ha il proprio campo ID persona.

![demo](./images/cja11.png)

Come puoi vedere, la maggior parte di loro ha l’ID persona selezionato automaticamente. Questo perché in ogni schema di Adobe Experience Platform viene selezionata un’identità primaria. Ad esempio, questo è lo schema per `Demo System - Event Schema for Website (Global v1.1)`, in cui puoi vedere che l&#39;identità primaria è impostata su `ecid`.

![demo](./images/cja13.png)

Tuttavia, puoi ancora influenzare l’identificatore che verrà utilizzato per unire i set di dati per la connessione. Puoi utilizzare qualsiasi identificatore configurato nello schema collegato al set di dati. Fai clic sul menu a discesa per esplorare gli ID disponibili su ciascun set di dati.

![demo](./images/cja14.png)

Come accennato, puoi impostare ID persona diversi per ogni set di dati. Questo consente di unire in CJA diversi set di dati da più origini. Immagina di inserire in NPS o dati di sondaggi che sarebbero molto interessanti e utili per capire il contesto e perché è successo qualcosa.

Il nome del campo ID persona non è importante, purché il valore nei campi ID persona corrisponda. Supponiamo di avere `email` in un set di dati e `emailAddress` in un altro set di dati definito come ID persona. Se `delaigle@adobe.com` è lo stesso valore per il campo ID persona in entrambi i set di dati, CJA sarà in grado di unire i dati.

Consulta le domande frequenti su CJA qui per comprendere le sfumature con l’unione di identità: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).

### Unione dei dati utilizzando l’ID persona

Ora che conosci il concetto di unione dei set di dati utilizzando l&#39;ID persona, scegliamo `email` come ID persona per ogni set di dati.

![demo](./images/cja15.png)

Vai a ogni set di dati per aggiornare l’ID persona. Compilare ora il campo ID persona scegliendo `email` nell&#39;elenco a discesa.

![demo](./images/cja12a.png)

Dopo aver unito i due set di dati, puoi continuare.

| set di dati | ID persona |
| ----------------- |-------------| 
| Sistema di dimostrazione - Set di dati di eventi per il sito web (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | e-mail |

È inoltre necessario assicurarsi che per entrambi i set di dati siano abilitate queste opzioni:

- Importa tutti i nuovi dati
- Recupera tutti i dati esistenti

(Non dimenticare di abilitare entrambe queste opzioni per il secondo set di dati)

È inoltre necessario selezionare un **tipo di origine dati** per ogni set di dati.

Impostazioni per il set di dati **Sistema demo - Set di dati evento per il sito Web (Global v1.1)**.

![demo](./images/cja16a.png)

Impostazioni per il set di dati **Sistema demo - Set di dati evento per il sito Web (Global v1.1)**.

Fare clic su **Aggiungi set di dati**.

![demo](./images/cja16.png)

Fai clic su **Salva** e passa all&#39;esercizio successivo.

Dopo aver creato la **connessione**, potrebbero essere necessarie alcune ore prima che i dati siano disponibili in CJA.

![demo](./images/cja20.png)

Passaggio successivo: [4.1.3 Creare una visualizzazione dati](./ex3.md)

[Torna al modulo 4.1](./customer-journey-analytics-build-a-dashboard.md)

[Torna a tutti i moduli](./../../../overview.md)

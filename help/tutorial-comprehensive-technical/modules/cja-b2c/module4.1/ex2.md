---
title: 'Customer Journey Analytics: connettere i set di dati di Adobe Experience Platform nel Customer Journey Analytics'
description: 'Customer Journey Analytics: connettere i set di dati di Adobe Experience Platform nel Customer Journey Analytics'
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '671'
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

Utilizzare questa convenzione di denominazione: `--demoProfileLdap-- – Omnichannel Data Connection`.

Esempio: `vangeluw - Omnichannel Data Connection`

È inoltre necessario selezionare la sandbox corretta da utilizzare. Nel menu sandbox, seleziona la sandbox, che dovrebbe essere `Bootcamp`. In questo esempio, la sandbox da utilizzare è **Bootcamp**. È inoltre necessario impostare il **numero medio di eventi giornalieri** su **meno di 1 milione**.

![demo](./images/cjasb.png)

Dopo aver selezionato la sandbox, i set di dati disponibili verranno aggiornati.

![demo](./images/cjasb1.png)

## 4.1.2.2 Seleziona set di dati Adobe Experience Platform

Cercare il set di dati `Demo System - Event Dataset for Website (Global v1.1)`. Fai clic su **+** per aggiungere il set di dati a questa connessione.

![demo](./images/cja7.png)

Cerca e seleziona le caselle di controllo per `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Allora avrai questo. Fai clic su **Avanti**.

![demo](./images/cja9.png)

## 4.1.2.3 ID persona e unione dei dati

### ID persona

L’obiettivo ora è unire questi set di dati. Per ogni set di dati selezionato, verrà visualizzato un campo denominato **ID persona**. Ogni set di dati ha il proprio campo ID persona.

![demo](./images/cja11.png)

Come puoi vedere, la maggior parte di loro ha l’ID persona selezionato automaticamente. Questo perché in ogni schema di Adobe Experience Platform viene selezionato un identificatore primario. Ad esempio, questo è lo schema per `Demo System - Event Schema for Call Center (Global v1.1)`, dove puoi vedere che l&#39;identificatore primario è impostato su `phoneNumber`.

![demo](./images/cja13.png)

Tuttavia, puoi ancora influenzare l’identificatore che verrà utilizzato per unire i set di dati per la connessione. Puoi utilizzare qualsiasi identificatore configurato nello schema collegato al set di dati. Fai clic sul menu a discesa per esplorare gli ID disponibili su ciascun set di dati.

![demo](./images/cja14.png)

Come accennato, puoi impostare ID persona diversi per ogni set di dati. Questo consente di unire in CJA diversi set di dati da più origini. Immagina di inserire in NPS o dati di sondaggi che sarebbero molto interessanti e utili per capire il contesto e perché è successo qualcosa.

Il nome del campo ID persona non è importante, purché il valore nei campi ID persona corrisponda. Supponiamo di avere `email` in un set di dati e `emailAddress` in un altro set di dati definito come ID persona. Se `delaigle@adobe.com` è lo stesso valore per il campo ID persona in entrambi i set di dati, CJA sarà in grado di unire i dati.

Al momento ci sono alcune altre limitazioni, come unire il comportamento anonimo a noto. Rivedi le domande frequenti qui: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).

### Unione dei dati utilizzando l’ID persona

Ora che conosci il concetto di unione dei set di dati utilizzando l&#39;ID persona, scegliamo `email` come ID persona per ogni set di dati.

![demo](./images/cja15.png)

Vai a ogni set di dati per aggiornare l’ID persona.

![demo](./images/cja12a.png)

Compilare ora il campo ID persona scegliendo `email` nell&#39;elenco a discesa.

![demo](./images/cja17.png)

Una volta uniti i tre set di dati, siamo pronti a continuare.

| set di dati | ID persona |
| ----------------- |-------------| 
| Sistema di dimostrazione - Set di dati di eventi per il sito web (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per assistenti vocali (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | e-mail |

Inoltre, assicurati che per ogni set di dati siano abilitate queste opzioni:

- Importa tutti i nuovi dati
- Recupera tutti i dati esistenti

Fare clic su **Aggiungi set di dati**.

![demo](./images/cja16.png)

Fai clic su **Salva** e passa all&#39;esercizio successivo.
Dopo aver creato la **connessione**, potrebbero essere necessarie alcune ore prima che i dati siano disponibili in CJA.

![demo](./images/cja20.png)

Passaggio successivo: [4.1.3 Creare una visualizzazione dati](./ex3.md)

[Torna al modulo 4.1](./customer-journey-analytics-build-a-dashboard.md)

[Torna a tutti i moduli](./../../../overview.md)

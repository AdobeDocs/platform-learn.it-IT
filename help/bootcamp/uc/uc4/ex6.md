---
title: Bootcamp - Customer Journey Analytics - Da informazioni all'azione
description: Bootcamp - Customer Journey Analytics - Da informazioni all'azione
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: e5c2ad88967d7f6a45d3a5cc09ca4c9bc9a62a08
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 Da informazioni all&#39;azione

## Obiettivi

- Comprendere come creare un pubblico in base a una visualizzazione raccolta nel Customer Journey Analytics
- Utilizzare questo pubblico in Real-Time CDP e Adobe Journey Optimizer

## 4.6.1 Creare un pubblico e pubblicarlo

Nel progetto hai creato un filtro denominato **Sentimenti di chiamata** e sono stati in grado di visualizzare il numero di utenti che hanno ricevuto le chiamate al call center classificate come **positivo**. Ora potrai creare un segmento con questi utenti e attivarlo in percorsi o canali di comunicazione.

Il primo passo è: Nel pannello creato nell’ultimo esercizio, seleziona riga **1. Sensazione di chiamata - Positivo**, fai clic con il pulsante destro del mouse e seleziona la **Creare un pubblico dalla selezione** opzione:

![demo](./images/aud1.png)

Quindi, assegna un nome al pubblico seguendo il modello **yourLastName - Chiamata al pubblico CJA che si sente positiva**:

![demo](./images/aud2.png)

Tieni presente che è possibile avere un’anteprima del pubblico da creare:

![demo](./images/aud3.png)

Infine, fai clic su **Pubblica**.

![demo](./images/aud4.png)

## 4.6.2 Utilizzare il pubblico come parte di un segmento

Torna alla Adobe Experience Platform, vai alla **Segmenti > Sfoglia** e potrai vedere il tuo segmento creato in CJA pronto e disponibile per essere utilizzato nelle tue attivazioni e nei tuoi percorsi!

![demo](./images/aud5.png)

Ora utilizziamo questo segmento in un’attivazione Facebook e in un percorso cliente!

## 4.6.3 Utilizza il tuo segmento in Real-Time CDP in tempo reale

In Adobe Experience Platform, vai a **Segmenti > Sfoglia** e trova il pubblico che hai creato in CJA:

![demo](./images/aud6.png)

Fai clic sul segmento, quindi fai clic su **Attiva a destinazione**:

![demo](./images/aud7.png)

Seleziona la destinazione denominata **bootcamp-facebook**, quindi fai clic su **Successivo**.

![demo](./images/aud8.png)

Fai clic su **Successivo** di nuovo.

![demo](./images/aud9.png)

Seleziona la **Origine del pubblico** e impostalo su **Direttamente dai clienti**, fai clic su **Successivo**.

![demo](./images/aud10.png)

Fai clic su **Fine**.

![demo](./images/aud11.png)

Il segmento è ora connesso al tipo di pubblico personalizzato di Facebook. Usiamo lo stesso segmento in Adobe Journey Optimizer ora.

## 4.6.4 Utilizzare il segmento in Adobe Journey Optimizer

In Adobe Experience Platform, fai clic su **Journey Optimizer**, quindi fai clic su nel menu a sinistra **Percorsi** e inizia a creare un percorso facendo clic su **Crea Percorso**.

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Quindi, nel menu a sinistra, sotto **Eventi**, seleziona **Qualificazione del segmento** e trascinarlo nel percorso:

![demo](./images/aud23.png)

In Segmento , fai clic su **Modifica** per selezionare un segmento:

![demo](./images/aud24.png)

Seleziona il pubblico creato in precedenza in CJA e fai clic su  **Salva**.

![demo](./images/aud25.png)

Pronti! Da qui puoi creare un percorso per i clienti idonei per questo segmento.

[Torna al flusso utente 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)

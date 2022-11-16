---
title: 'Real-time CDP: creare un segmento e intervenire'
description: 'Real-time CDP: creare un segmento e intervenire'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# 6. Real-time CDP - Creare un segmento e intervenire

**Autore: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto De Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

In questo modulo, configurerai un segmento in streaming e attiverai il segmento in più destinazioni.

## Finalità di apprendimento

- Scopri come creare un segmento e abilitarlo per lo streaming.
- Scopri come configurare una destinazione pubblicitaria utilizzando l’interfaccia utente di Adobe Experience Platform.
- Scopri come collegare un segmento a una destinazione e attivarlo.
- Scopri come utilizzare i segmenti Adobe Experience Platform in Adobe Audience Manager e come utilizzare i segmenti Adobe Audience Manager in Adobe Experience Platform, grazie alla condivisione dei segmenti bidirezionale.

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso ad Adobe Target
- Accesso ad AWS S3

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem11.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--module11sandbox--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[6.1 Creare un segmento](./ex1.md)

Scopri come creare un segmento.

[6.2 Controllare come configurare la destinazione DV360 utilizzando le destinazioni](./ex2.md)

Scopri come configurare una destinazione pubblicitaria utilizzando l’interfaccia utente di Real-Time CDP.

[6.3 Intervenire: inviare il segmento a DV360](./ex3.md)

Collegare il segmento generato nell&#39;esercizio 6.1 alla destinazione DV360.

[6.4 Intervenire: invia il segmento a una destinazione S3](./ex4.md)

Utilizza il segmento generato nell’esercizio 6.1 e invialo a una destinazione S3, tipicamente utilizzato per le destinazioni di E-mail marketing.

[6.5 Intervenire: inviare il segmento ad Adobe Target](./ex5.md)

Utilizza il segmento generato nell’esercizio 6.1 per configurare un’attività Targeting esperienze in Adobe Target.

[6.6 Tipi di pubblico esterni](./ex6.md)

Importa i tipi di pubblico da un sistema sorgente esterno in Adobe Experience Platform.

[6.7 SDK per destinazioni](./ex7.md)

Configura la tua destinazione utilizzando l’SDK per le destinazioni.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)

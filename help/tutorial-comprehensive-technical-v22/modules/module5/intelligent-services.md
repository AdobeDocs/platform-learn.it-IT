---
title: Intelligent Services
description: Intelligent Services
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 5. Servizi intelligenti

**Autori: [Diptiman Badajena](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Questo modulo illustra come configurare, configurare e utilizzare Adobe Experience Platform Intelligent Services.

## Finalità di apprendimento

- Acquisisci familiarità con Adobe Experience Platform
- Configurare schema/set di dati per l’utilizzo con Intelligent Services
- Creare una nuova istanza di Customer AI
- Dashboard di valutazione e segmentazione

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem5.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--module10sandbox--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[5.1 Customer AI - Preparazione dei dati (acquisizione)](./ex1.md)

I dati dei clienti vengono acquisiti e trasformati con Experience Data Model (XDM) in Adobe Experience Platform. In particolare, tutti i set di dati utilizzati in Intelligent Services devono essere conformi allo schema XDM (Consumer Experience Event).

[5.2 Customer AI - Creare una nuova istanza (Configura)](./ex2.md)

L&#39;analista di marketing configura le previsioni desiderate specificando le regole di business e identificando i dati pertinenti. Dopo aver configurato il modello, pianificare le esecuzioni e rivedere i punteggi.

[5.3 Customer AI - Dashboard di valutazione e segmentazione (Predict &amp; Take Action)](./ex3.md)

Una volta completati l’addestramento e il punteggio, i punteggi vengono riscritti in Platform. Puoi decidere quali azioni intraprendere con le previsioni, ad esempio definire i segmenti, creare dashboard personalizzate e così via.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)

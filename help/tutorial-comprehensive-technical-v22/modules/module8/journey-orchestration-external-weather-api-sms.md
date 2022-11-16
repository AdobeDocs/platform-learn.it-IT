---
title: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora
description: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 8. Adobe Journey Optimizer: Origini dati esterne e azioni personalizzate

**Autore: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, utilizzerai Adobe Journey Optimizer per ascoltare il comportamento dei clienti, sia online che offline, e rispondere ad esso in modo intelligente, contestuale e in tempo reale. Hai già avuto una prima esperienza pratica con Adobe Journey Optimizer nel modulo 6. In questo esercizio, approfondirete ed esplorerete un caso d’uso più avanzato in cui le origini dati esterne vengono utilizzate come parte di un percorso.

## Finalità di apprendimento

- Scopri come creare eventi, origini dati esterne e percorsi in Adobe Journey Optimizer
- Scopri come utilizzare le informazioni meteo dall’API Open Weather
- Scopri come utilizzare destinazioni di azioni personalizzate come Twilio e Slack da Adobe Journey Optimizer

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso a Adobe Journey Optimizer
- Accesso all&#39;API Open Weather

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem12.png)

## Contesto aziendale

In qualità di marchio, hai investito molto nella personalizzazione delle esperienze online. Ora vuoi essere contestuale e pertinente per le esperienze offline.
In questo modulo, utilizzerai la presenza di un cliente in un negozio offline per poi offrire un&#39;esperienza personalizzata all&#39;interno dello store presentando contenuti pertinenti a quel cliente sui nostri schermi all&#39;interno del negozio e, allo stesso tempo, vogliamo inviare un messaggio push o SMS personalizzato a quello stesso cliente, il tutto in tempo reale.
In qualità di marchio, puoi anche comprendere che il contesto influisce notevolmente sull’interesse di un cliente, per cui desideri inserire le informazioni meteo correnti sulla posizione del cliente, per decidere quale contenuto o promozione visualizzare.

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[8.1 Definire un evento](./ex1.md)

Scopri come definire un evento personalizzato utilizzando Adobe Journey Optimizer.

[8.2 Definire un’origine dati esterna](./ex2.md)

Scopri come configurare un’origine dati esterna utilizzando Adobe Journey Optimizer.

[8.3 Definire un’azione personalizzata](./ex3.md)

Scopri come definire un’azione esterna utilizzando Adobe Journey Optimizer.

[8.4 Creare percorsi e messaggi](./ex4.md)

Combina eventi, origini dati e azioni in un percorso intelligente e contestuale.

[8.5 Attiva il tuo percorso](./ex5.md)

Attiva il tuo percorso specifico.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)

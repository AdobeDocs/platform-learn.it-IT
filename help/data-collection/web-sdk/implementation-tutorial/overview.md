---
title: Panoramica
description: Panoramica
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Panoramica

La raccolta di dati su eventi che si verificano nel browser di un utente è un principio fondamentale di una strategia di marketing. Adobe ha fornito diversi strumenti per aiutarti a gestire questi dati. Anche se è possibile acquisire familiarità con ciascuno di questi strumenti singolarmente, questa esercitazione tenta di fornire una visione più ampia di ciò che ciascuno di questi strumenti fa e di come lavorano insieme per raggiungere un obiettivo comune.

Questa esercitazione illustra una strategia per (1) strutturare e mantenere i dati in Adobe Experience Platform, (2) gestire i dati nel browser e comunicare che si sono verificati determinati eventi e (3) reagire a tali eventi inviando dati pertinenti a Adobe Experience Platform.

Questa esercitazione utilizza Adobe Client Data Layer, Adobe Experience Platform Web SDK e la funzione tag per un’implementazione più prescrittiva e senza soluzione di continuità, ma consente anche di combinare questi strumenti con strumenti di terze parti o interni per garantire la massima flessibilità.

## Esempio di scenario

Per questa esercitazione, supponiamo che tu stia implementando la raccolta dati per una semplice pagina di prodotto su un sito di e-commerce. La pagina del prodotto viene caricata nel browser. In questo caso, noterai che l’utente ha visualizzato il prodotto. L’utente decide di acquistare il prodotto, quindi fa clic su un pulsante per aggiungere il prodotto al carrello. In questo caso, noterai che l’utente ha aperto un nuovo carrello e aggiunto il prodotto al carrello inviando eventi di esperienza a Adobe Experience Platform. Infine, l&#39;utente fa clic su un _Scaricare l’app_ perché sono interessati alla tua app mobile. L’utente avrà fatto clic sul collegamento.

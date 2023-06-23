---
title: Panoramica
description: Panoramica
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Panoramica

La raccolta di dati sugli eventi che si verificano nel browser di un utente è un principio fondamentale di una strategia di marketing. Adobe ha fornito diversi strumenti per aiutarti a gestire questi dati. Sebbene tu possa acquisire familiarità con ciascuno di questi strumenti singolarmente, questo tutorial tenta di fornire una visione più ampia di ciò che ciascuno di questi strumenti fa e di come lavorano insieme per raggiungere un obiettivo comune.

Questa esercitazione illustra una strategia per (1) strutturare e mantenere i dati in Adobe Experience Platform, (2) gestire i dati nel browser e comunicare che si sono verificati determinati eventi e (3) reagire a tali eventi inviando dati rilevanti a Adobe Experience Platform.

Questa esercitazione utilizza Adobe Client Data Layer, Adobe Experience Platform Web SDK e la funzione tag per un’implementazione più prescrittiva e diretta. Tuttavia, puoi anche combinare e abbinare questi strumenti con strumenti di terze parti o interni per una flessibilità ottimale.

## Esempio di scenario

Per questo tutorial, supponiamo che tu stia implementando la raccolta dati per una semplice pagina di prodotto su un sito di e-commerce. La pagina di prodotto viene caricata nel browser. In questo caso, potrai verificare che l’utente abbia visualizzato il prodotto. L’utente decide di acquistare il prodotto, quindi fa clic su un pulsante per aggiungerlo al carrello. In questo caso, puoi tenere traccia del fatto che l’utente ha aperto un nuovo carrello e aggiunto il prodotto al carrello inviando eventi di esperienza a Adobe Experience Platform. Infine, l’utente fa clic su una _Scaricare l’app_ perché sono interessati alla tua app mobile. Tieni presente che l’utente ha fatto clic sul collegamento.

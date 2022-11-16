---
title: Panoramica
description: Panoramica
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# Utilizza raccolta dati Adobe Experience Platform

La raccolta di dati su eventi che si verificano nel browser di un utente è un principio fondamentale di una strategia di marketing. Adobe ha fornito diversi strumenti per aiutarti a gestire questi dati. Anche se è possibile acquisire familiarità con ciascuno di questi strumenti singolarmente, questa esercitazione tenta di fornire una visione più ampia di ciò che ciascuno di questi strumenti fa e di come lavorano insieme per raggiungere un obiettivo comune.

Questa esercitazione illustra una strategia per:

1. Strutturazione e persistenza dei dati in Adobe Experience Platform,
1. Gestione dei dati nel browser e comunicazione di determinati eventi e
1. Reagire a tali eventi inviando dati pertinenti a Adobe Experience Platform.

Questa esercitazione utilizza Adobe Client Data Layer, Adobe Experience Platform Web SDK e la funzione [!DNL Tags] per un&#39;implementazione più prescrittiva e senza soluzione di continuità, è anche possibile combinare questi strumenti con strumenti di terze parti o interni per garantire la massima flessibilità.

## Esempio di scenario

Durante questa esercitazione, implementa la raccolta dati per una semplice pagina di prodotto su un sito di e-commerce:

1. La pagina del prodotto viene caricata nel browser. Qui si tiene traccia del fatto che l’utente ha visualizzato il prodotto.
1. L’utente decide di acquistare il prodotto, quindi fa clic su un pulsante per aggiungere il prodotto al carrello. In questo caso, tieni traccia del fatto che l’utente ha aperto un nuovo carrello e aggiunto il prodotto al carrello inviando eventi di esperienza a Adobe Experience Platform.
1. Infine, l&#39;utente fa clic su un _Scaricare l’app_ perché sono interessati alla tua app mobile. L’utente ha fatto clic sul collegamento.

Cominciamo.

[Avanti: ](structuring-your-data.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

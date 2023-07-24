---
title: Bootcamp - Blending physical and digital - Test del percorso
description: Bootcamp - Blending physical and digital - Test del percorso
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 3.4 Test del percorso

Per testare il percorso, dovrai utilizzare l’ID evento dell’evento creato nell’esercizio 3.2, che si presenta così.

![ACOP](./images/payloadeventID.png)

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il percorso. In questo esempio, eventID è:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Apri l’app mobile e vai alla home page. Fai clic su **Impostazioni** icona.

![DSN](./images/appsett.png)

Incolla il tuo eventID nel campo **Beacon EventID** e fai clic su **Salva**.

![DSN](./images/beacon1.png)

Prima di continuare, aprire la pagina Web nel computer: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

A questo punto viene visualizzato quanto segue:

![DSN](./images/screen1.png)

Quindi, torna alla home page. Fai clic su **beacon** icona.

![DSN](./images/app23.png)

Poi vedrai questo. Seleziona innanzitutto **Beacon schermo bootcamp** e quindi fare clic su **voce** pulsante. Questo consente di simulare una voce beacon.

![DSN](./images/app21.png)

Dai un&#39;occhiata allo schermo del negozio. Vedrai l’ultimo prodotto visualizzato lì entro 5 secondi.

![DSN](./images/beacon3.png)

Riceverai anche la notifica push.

![DSN](./images/beacon2.png)

Hai terminato questo esercizio.

[Torna a Flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)

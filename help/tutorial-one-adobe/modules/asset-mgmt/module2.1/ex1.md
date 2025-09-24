---
title: Creazione del programma Cloud Manager
description: Creazione del programma Cloud Manager
kt: 5342
doc-type: tutorial
exl-id: fda247eb-1865-4936-b46e-84128ccab357
source-git-commit: 7384eabe00354374f7012be10c24870c68ea7f2c
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# 1.1.1 Creare un programma Cloud Manager

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`. Poi vedrai qualcosa del genere. Fai clic su **Aggiungi programma**.

![AEMCS](./images/aemcs1.png)

Per il **nome programma**, utilizzare `--aepUserLdap-- - CitiSignal AEM+ACCS`. Seleziona l&#39;opzione **Configura una sandbox**. Fai clic su **Continua**.

![AEMCS](./images/aemcs2.png)

Accertati che siano selezionate le seguenti opzioni:

- Siti
- Moduli
- Risorse

Fare clic sulla freccia per **Assets** per aprire l&#39;elenco delle opzioni.

![AEMCS](./images/aemcs3.png)

Accertati che siano selezionate le seguenti opzioni:

- Content Hub

Scorri verso il basso nell’elenco.

![AEMCS](./images/aemcs3a.png)

Accertati che siano selezionate le seguenti opzioni:

- Edge Delivery Services
- Contenuti multimediali dinamici

Fai clic su **Crea**.

![AEMCS](./images/aemcs3b.png)

La creazione dell’ambiente richiede un po’ di tempo, 10-20 minuti.

![AEMCS](./images/aemcs4.png)

Una volta creati gli ambienti e pronti per l’uso, riceverai una conferma e-mail dopo la quale potrai tornare qui.

![AEMCS](./images/aemcs5.png)

Dopo aver ricevuto la conferma e-mail, torna a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Lo stato del programma è cambiato in **Pronto**. Fai clic sul programma per aprirlo.

![AEMCS](./images/aemcs6.png)

Osserva la scheda **Pipeline**. Fare clic sui tre punti **...** e quindi su **Esegui**.

![AEMCS](./images/aemcs7.png)

Fare clic su **Esegui**.

![AEMCS](./images/aemcs8.png)

Fare clic sui tre punti **...** nella scheda **Ambienti** e quindi su **Visualizza dettagli**.

![AEMCS](./images/aemcs9.png)

Potrai quindi visualizzare i dettagli dell&#39;ambiente, incluso l&#39;URL dell&#39;ambiente **Author**, che ti serviranno nel prossimo esercizio.

Osserva la riga **Content Hub** e seleziona **Fai clic per attivare**.

![AEMCS](./images/aemcs10.png)

Fare clic su **Attiva**.

![AEMCS](./images/aemcsact1.png)

Attivazione di **Content Hub** avviata. Questa operazione può richiedere 10 minuti o più.

![AEMCS](./images/aemcsact2.png)

Dopo circa 10 minuti, verrà completata l&#39;attivazione di **Content Hub**.
Dai un&#39;occhiata alla riga **Dynamic Media** e seleziona **Fai clic per attivare**.

![AEMCS](./images/aemcsact3.png)

Fare clic su **Attiva**.

![AEMCS](./images/aemcsact4.png)

Attivazione di **Dynamic Media** avviata. Questa operazione può richiedere 10 minuti o più.

![AEMCS](./images/aemcsact5.png)

Dopo circa 10 minuti verrà eseguita l&#39;attivazione di **Dynamic Media**.

![AEMCS](./images/aemcsact6.png)

Al termine dell’esecuzione della pipeline, puoi continuare con l’esercizio successivo.

Passaggio successivo: [Configurare l&#39;ambiente AEM CS](./ex2.md){target="_blank"}

Torna a [Adobe Experience Manager Cloud Service e Edge Delivery Services](./aemcs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

---
title: Configurare l’endpoint API HTTP in Adobe Experience Platform
description: Configurare l’endpoint API HTTP in Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: a29dd01d-4415-45d6-ad52-7f14aef60565
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 6%

---

# 2.6.3 Configurare l’endpoint di streaming API HTTP in Adobe Experience Platform

Prima di poter configurare il connettore Adobe Experience Platform Sink in Kafka, è necessario creare un connettore Source API HTTP in Adobe Experience Platform. Per configurare il connettore sink di Adobe Experience Platform è necessario specificare l&#39;URL dell&#39;endpoint di streaming API HTTP.

Per creare un connettore Source API HTTP, accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Origini** e scorri verso il basso nel **Catalogo origini** fino a visualizzare **API HTTP**. Fare clic su **Configurazione**.

![Acquisizione dei dati](./images/kaep1.png)

Fai clic su **Nuovo account**. Utilizza `--aepUserLdap-- - Kafka` come nome per la connessione API HTTP, in questo caso **vangeluw - Kafka**. Abilita la casella di controllo per **Compatibile con XDM**. Fare clic su **Connetti all&#39;origine**.

![Acquisizione dei dati](./images/kaep2.png)

Visualizzerai quindi questo elemento, fai clic su **Avanti**.

![Acquisizione dei dati](./images/kaep3.png)

Seleziona **Set di dati esistente**, apri il menu a discesa. Cerca e seleziona il set di dati **Sistema demo - Set di dati evento per Call Center (Global v1.1)**.

Fai clic su **Avanti**.

![Acquisizione dei dati](./images/kaep4.png)

Fai clic su **Fine**.

![Acquisizione dei dati](./images/kaep8.png)

Viene quindi visualizzata una panoramica del connettore Source API HTTP appena creato.

È necessario copiare l&#39;URL dell&#39;**endpoint di streaming**, che è simile a quello riportato di seguito, come sarà necessario nell&#39;esercizio successivo.

`https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`

![Acquisizione dei dati](./images/kaep9.png)

Hai finito questo esercizio.

Passaggio successivo: [2.6.4 Installare e configurare Kafka Connect e il connettore Adobe Experience Platform Sink](./ex4.md)

[Torna al modulo 2.6](./aep-apache-kafka.md)

[Torna a tutti i moduli](../../../overview.md)

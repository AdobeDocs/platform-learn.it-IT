---
title: Attivazione del segmento nell’hub eventi di Microsoft Azure - Attivare il segmento
description: Attivazione del segmento nell’hub eventi di Microsoft Azure - Attivare il segmento
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# 13.4 Attivare il segmento

## 13.4.1 Aggiungere un segmento alla destinazione dell’hub eventi di Azure

In questo esercizio aggiungi il segmento `--demoProfileLdap-- - Interest in Equipment` al tuo `--demoProfileLdap---aep-enablement` Destinazione di Azure Event Hub.

Accedi a Adobe Experience Platform andando a questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato la sandbox appropriata, visualizzerai la modifica dello schermo e ora ti trovi nella sandbox dedicata.

![Acquisizione dei dati](../module2/images/sb1.png)

Vai a **Destinazioni**, quindi fai clic su **Sfoglia**. Verranno visualizzate tutte le destinazioni disponibili. Individua la destinazione e fai clic sul pulsante **+** come indicato di seguito.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Vedrete questo. Cerca il segmento utilizzando il tuo ldap e seleziona `--demoProfileLdap-- - Interest in Equipment` dall’elenco dei segmenti.

Fai clic su **Avanti**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP può distribuire un payload a due tipi di destinazioni, destinazioni di segmenti e destinazioni di profilo.

Le destinazioni dei segmenti riceveranno un payload di qualificazione dei segmenti predefinito che verrà discusso in seguito. Tale payload contiene **tutto** le qualifiche del segmento per un profilo specifico. Anche per i segmenti che non sono nell’elenco di attivazione della destinazione. Un esempio di tale destinazione di segmento sono **Hub eventi di Azure** e **AWS Kinesis**.

Le destinazioni basate su profili ti consentono di scegliere qualsiasi attributo (firstName, lastName, ...) dallo schema dell’Unione profili XDM e di includerlo nel payload di attivazione. Un esempio di destinazione è il **Marketing e-mail**.

Poiché la destinazione dell’hub eventi di Azure è **segmento** destinazione, selezionare ad esempio il campo `--aepTenantId--.identification.core.ecid`.

Fai clic su **Aggiungi nuovo campo**, fai clic su sfoglia schema e seleziona il campo . `--aepTenantId--identification.core.ecid` Elimina tutti gli altri campi che verranno visualizzati automaticamente.

Fai clic su **Avanti**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Fai clic su **Fine**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Il segmento viene ora attivato verso la destinazione Microsoft Event Hub.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Passaggio successivo: [13.5 Creare il progetto Microsoft Azure](./ex5.md)

[Torna al modulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../overview.md)

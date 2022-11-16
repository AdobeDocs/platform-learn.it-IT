---
title: Real-time CDP - Creare un segmento e intraprendere azioni - Configurare una destinazione pubblicitaria come Google DV360
description: Real-time CDP - Creare un segmento e intraprendere azioni - Configurare una destinazione pubblicitaria come Google DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 6.2 Configurare una destinazione pubblicitaria come Google DV360

>[!IMPORTANT]
>
>Il contenuto seguente è destinato all&#39;FYI - Sì **NOT** configurare una nuova destinazione per DV360. La destinazione è già stata creata ed è possibile utilizzarla nell&#39;esercizio successivo.

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](../module2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Vedrai il **Catalogo delle destinazioni**.

![RTCDP](./images/rtcdp.png)

In **Destinazioni**, fai clic su **Display Google e video 360** quindi fai clic su **+ Configurazione**.

![RTCDP](./images/rtcdpgoogle.png)

Vedrete questo. Fai clic su **Connetti alla destinazione**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Nella schermata successiva, è possibile configurare la destinazione su Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Immettere un valore nei campi **Nome** e **Descrizione**.

Il campo **ID account** è **ID inserzionista** dell&#39;account DV360. Puoi trovarlo qui:

![RTCDP](./images/rtcdpgoogledv360advid.png)

La **Tipo di conto** deve essere impostato su **Invita inserzionista**.

Ora avete questo. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google deve consentire l&#39;Adobe dell&#39;elenco per consentire a Adobe Experience Platform di inviare dati a Google DV360. Contatta il tuo Google Account Manager per abilitare questo flusso di dati.

Dopo aver creato la destinazione, verrà visualizzato questo. Facoltativamente, puoi selezionare un criterio di governance dei dati. Quindi, fai clic su **Salva e esci**.

![RTCDP](./images/rtcdpcreatedest1.png)

Verrà quindi visualizzato un elenco delle destinazioni disponibili.
Nell&#39;esercizio successivo, verrà collegato il segmento generato nell&#39;esercizio precedente alla destinazione Google DV360.

Passaggio successivo: [6.3 Intervenire: inviare il segmento a DV360](./ex3.md)

[Torna al modulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../overview.md)

---
title: Real-time CDP - Creare un segmento e intervenire - Configurare una destinazione Advertising come Google DV360
description: Real-time CDP - Creare un segmento e intervenire - Configurare una destinazione Advertising come Google DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 2.3.2 Configurare una destinazione Advertising come Google DV360

>[!IMPORTANT]
>
>Il contenuto seguente è destinato a essere utilizzato come informazione sintetica. **NOT** deve configurare una nuova destinazione per DV360. La destinazione è già stata creata ed è possibile utilizzarla nell&#39;esercizio successivo.

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Verrà quindi visualizzato il **Catalogo destinazioni**.

![RTCDP](./images/rtcdp.png)

In **Destinazioni**, fare clic su **Google Display &amp; Video 360** e quindi su **+ Configurazione**.

![RTCDP](./images/rtcdpgoogle.png)

Poi vedrai questo. Fai clic su **Connetti alla destinazione**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Nella schermata successiva è possibile configurare la destinazione su Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Immettere un valore nei campi **Nome** e **Descrizione**.

Il campo **ID account** è **ID inserzionista** dell&#39;account DV360. Puoi trovarlo qui:

![RTCDP](./images/rtcdpgoogledv360advid.png)

Il tipo di account **Tipo di account** deve essere impostato su **Invita inserzionista**.

Ora ce l&#39;hai. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google deve inserire nell&#39;elenco Consentiti Adobe per consentire a Adobe Experience Platform di inviare dati a Google DV360. Contatta il tuo Google Account Manager per abilitare questo flusso di dati.

Dopo aver creato la destinazione, visualizzerai questo. È possibile selezionare un criterio di governance dei dati. Fare clic su **Salva ed esci**.

![RTCDP](./images/rtcdpcreatedest1.png)

Viene quindi visualizzato un elenco delle destinazioni disponibili.
Nell&#39;esercizio successivo, il segmento creato nell&#39;esercizio precedente verrà collegato alla destinazione di Google DV360.

Passaggio successivo: [2.3.3 Intervenire: inviare il segmento a DV360](./ex3.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)

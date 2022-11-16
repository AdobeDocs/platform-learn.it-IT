---
title: Attivazione del segmento nell’hub eventi di Microsoft Azure - Creare un segmento in streaming
description: Attivazione del segmento nell’hub eventi di Microsoft Azure - Creare un segmento in streaming
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 13.3 Creare un segmento

## 13.3.1 Introduzione

Crea un segmento semplice:

- **Interesse per le attrezzature** per i quali i profili dei clienti si qualificano quando visitano il **Attrezzatura** pagina del sito web dimostrativo Luma.

### Buono a sapere

CDP in tempo reale attiva un’attivazione a una destinazione quando ti qualifichi per un segmento che fa parte dell’elenco di attivazione di tale destinazione. In questo caso, il payload di qualificazione del segmento che verrà inviato a tale destinazione conterrà **tutti i segmenti per i quali il profilo è idoneo**.

L’obiettivo di questo modulo è quello di mostrare che la qualifica del segmento del profilo cliente viene inviata a **le** destinazione dell&#39;hub dell&#39;evento in tempo reale.

### Stato del segmento

La qualificazione dei segmenti in Adobe Experience Platform ha sempre una **status**-property e può essere uno dei seguenti:

- **realizzato**: questo indica una nuova qualificazione del segmento
- **esistente**: indica una qualifica di segmento esistente
- **uscito**: questo indica che il profilo non si qualifica più per il segmento

## 13.3.2 Creare il segmento

La creazione di un segmento viene descritta in dettaglio in [Modulo 6](../module6/real-time-cdp-build-a-segment-take-action.md).

### Crea segmento

Accedi a Adobe Experience Platform andando a questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato la sandbox appropriata, visualizzerai la modifica dello schermo e ora ti trovi nella sandbox dedicata.

![Acquisizione dei dati](../module2/images/sb1.png)

Vai a **Segmenti**. Fai clic sul pulsante **+ Crea segmento** pulsante .

![Acquisizione dei dati](./images/seg.png)

Denomina il segmento `--demoProfileLdap-- - Interest in Equipment` e aggiungi l&#39;evento esperienza nome pagina:

Fai clic su **Eventi**, e trascinare e rilasciare **XDM Experience Event > Web > Dettagli pagina Web > Nome**. Invio **attrezzatura** come valore:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Trascinamento della selezione **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Invio `--demoProfileLdap--` come valore, imposta il parametro di confronto su **contiene** e fai clic su **Salva**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Definizione PQL

Il PQL del segmento si presenta così:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

Passaggio successivo: [13.4 Attivare il segmento](./ex4.md)

[Torna al modulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../overview.md)

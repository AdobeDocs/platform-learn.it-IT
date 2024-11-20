---
title: Attivazione segmento in Microsoft Azure Event Hub - Creazione di un segmento in streaming
description: Attivazione segmento in Microsoft Azure Event Hub - Creazione di un segmento in streaming
kt: 5342
doc-type: tutorial
exl-id: 86bc3afa-16a9-4834-9119-ce02445cd524
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 1%

---

# 2.4.3 Creare un segmento

## 2.4.3.1 Introduzione

Creerai un segmento semplice:

- **Interesse nell&#39;attrezzatura** per il quale i profili dei clienti si qualificheranno quando visitano la pagina **Attrezzatura** del sito Web di dimostrazione Luma.

### Buono a sapersi

Real-Time CDP attiva un&#39;attivazione a una destinazione quando si è qualificati per un segmento che fa parte dell&#39;elenco di attivazione della destinazione. In questo caso, il payload di qualificazione dei segmenti che verrà inviato a tale destinazione conterrà **tutti i segmenti per i quali il profilo è idoneo**.

L&#39;obiettivo di questo modulo è quello di mostrare che la qualificazione del segmento del tuo profilo cliente viene inviata in tempo reale alla **destinazione dell&#39;hub eventi**.

### Stato segmento

Una qualifica di segmento in Adobe Experience Platform ha sempre una proprietà **status** e può essere una delle seguenti:

- **realized**: indica una nuova qualifica del segmento
- **esistente**: indica una qualifica di segmento esistente
- **uscita**: indica che il profilo non è più idoneo per il segmento

## 2.4.3.2 Creare il segmento

La creazione di un segmento è spiegata in dettaglio nel [Modulo 2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md).

### Crea segmento

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Vai a **Segmenti**. Fare clic sul pulsante **+ Crea segmento**.

![Acquisizione dei dati](./images/seg.png)

Assegna un nome al segmento `--aepUserLdap-- - Interest in Equipment` e aggiungi l&#39;evento esperienza nome pagina:

Fai clic su **Eventi** e trascina **XDM ExperienceEvent > Web > Dettagli pagina Web > Nome**. Immetti **apparecchiature** come valore:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Trascina e rilascia **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Immetti `--aepUserLdap--` come valore, imposta il parametro di confronto su **contains** e fai clic su **Salva**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Definizione PQL

Il PQL del segmento si presenta così:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

Passaggio successivo: [2.4.4 Attiva segmento](./ex4.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)

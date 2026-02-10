---
title: Utilizzare il modello Dynamic Media con Adobe Journey Optimizer
description: Utilizzare il modello Dynamic Media con Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 1.4.2 Utilizzare il modello Dynamic Media con Adobe Journey Optimizer

## 1.4.2.1 Crea la tua campagna in Adobe Journey Optimizer

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Ora creerai una campagna. A differenza del percorso basato sugli eventi dell’esercizio precedente, che si basa su eventi di esperienza o entrate o uscite di pubblico in arrivo per attivare un percorso per 1 cliente specifico, le campagne sono indirizzate a un intero pubblico una volta con contenuti univoci come newsletter, promozioni una tantum o informazioni generiche, oppure periodicamente con contenuti simili inviati regolarmente, come ad esempio campagne e promemoria di compleanno.

Nel menu, vai a **Campagne** e fai clic su **Crea campagna**.

![Journey Optimizer](./images/gsemail21.png)

Seleziona **Pianificato - Marketing** e fai clic su **Crea**.

![Journey Optimizer](./images/gsemail22.png)

Nella schermata di creazione della campagna, configura quanto segue:

- **Nome**: `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Fai clic su **Azioni**.

![Journey Optimizer](./images/gsemail23.png)

Fare clic su **+ Aggiungi azione** e quindi selezionare **E-mail**.

![Journey Optimizer](./images/gsemail24.png)

Quindi, selezionare una **configurazione e-mail** esistente e fare clic su **Modifica contenuto**.

![Journey Optimizer](./images/gsemail25.png)

Poi vedrai questo. Per la **riga oggetto**, utilizza:

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Fare clic su **Modifica contenuto**.

![Journey Optimizer](./images/gsemail26.png)

Seleziona **Progettazione da zero**.

![Journey Optimizer](./images/gsemail27.png)

Dovresti vedere questo.

![Journey Optimizer](./images/gsemail28.png)

Aggiungi 2x **1:1 colonna** all&#39;area di lavoro.

![Journey Optimizer](./images/gsemail29.png)

Vai a **Frammenti**, trascina il frammento **header** nella prima colonna 1:1, quindi trascina il frammento **footer** nella seconda colonna 1:1.

![Journey Optimizer](./images/gsemail30.png)

Aggiungere una nuova colonna 1:1 tra i due frammenti, quindi aggiungere una **Immagine** nella colonna 1:1. Quindi fare clic su **Sfoglia**.

![Journey Optimizer](./images/gsemail31.png)

Passa alla cartella in cui è stato memorizzato il modello Dynamic Media. Seleziona il modello Dynamic Media e fai clic su **Seleziona**.

![Journey Optimizer](./images/gsemail32.png)

Dovresti vedere questo.

![Journey Optimizer](./images/gsemail33.png)

## Passaggi successivi

Torna a [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

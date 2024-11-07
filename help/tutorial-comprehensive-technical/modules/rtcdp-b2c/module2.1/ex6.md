---
title: Visualizza Real-time Customer Profile in azione nel call center
description: Visualizza Real-time Customer Profile in azione nel call center
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# 2.1.6 Visualizza il tuo Real-time Customer Profile in azione nel Call Center

In questo esercizio, l’obiettivo è quello di guidarti attraverso il percorso dei clienti e comportarti come un vero cliente.

Su questo sito web è stato implementato Adobe Experience Platform. Ogni azione è considerata un evento esperienza e viene inviata a Adobe Experience Platform in tempo reale, idratando il Profilo cliente in tempo reale.

In un esercizio precedente, hai iniziato come cliente anonimo che stava navigando sul sito e, dopo un paio di passaggi, sei diventato un cliente noto.

Quando lo stesso cliente risponde al telefono e chiama il call center, è fondamentale che le informazioni provenienti da altri canali siano immediatamente disponibili, in modo che l’esperienza del call center possa essere rilevante e personalizzata.

## 2.1.6.1 Utilizzare l’app CX

Come parte del nostro sistema demo, abbiamo creato un modello di app CX che può essere utilizzato per simulare un ambiente di call center. Per creare un progetto di app CX di questo tipo, segui la procedura riportata di seguito.

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Fare clic su **Nuovo progetto**.

Viene quindi visualizzato il progetto dell&#39;app CX. Fai clic sul progetto per aprirlo.

![Demo](./images/cxapp3.png)

Nel progetto dell&#39;app CX, vai a **Integrazioni**. Selezionare la proprietà Raccolta dati di Adobe Experience Platform creata nel modulo 0. Selezionare la proprietà il cui nome contiene **(abilitazione)**. Quindi fare clic su **Esegui**.

![Demo](./images/cxapp4.png)

Poi vedrai questo.

![Demo](./images/cxapp5.png)

Nel pannello Visualizzatore profili puoi vedere le seguenti combinazioni di ID e spazi dei nomi:

![Profilo cliente](./images/identities.png)

| Identità | Namespace |
|:-------------:| :---------------:|
| ID Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| ID e-mail | woutervangeluwe+06022022-01@gmail.com |
| ID numero cellulare | +32473622044+06022022-01 |

Quando il cliente chiama il call center, il numero di telefono può essere utilizzato per identificare il cliente. In questo esercizio utilizzerai il numero di telefono per recuperare il profilo del cliente nell’app CX.

Selezionare **Numero di telefono** nel menu a discesa e immettere il numero di telefono utilizzato nel sito Web. Premi **Invio**.

![Demo](./images/19.png)

Ora vedrai le informazioni che idealmente verrebbero visualizzate nel Call Center, in modo che i dipendenti del Call Center abbiano immediatamente a disposizione tutte le informazioni pertinenti quando parlano con un cliente.

![Demo](./images/20.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.1](./real-time-customer-profile.md)

[Torna a tutti i moduli](../../../overview.md)

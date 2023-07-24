---
title: Bootcamp - Personalizzazione nel call center
description: Bootcamp - Personalizzazione nel call center
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: f7697673-38f9-41f6-ac4d-2561db2ece67
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 2.6 Personalizzazione nel call center

Come discusso più volte durante il bootcamp, la personalizzazione dell’esperienza del cliente è qualcosa che dovrebbe accadere in modo omnicanale. Un call center è spesso abbastanza disconnesso dal resto del percorso di clienti e questo spesso porta a esperienze frustranti per il cliente, ma non è necessario che lo sia. Ecco un esempio di come il call center può essere facilmente collegato a Adobe Experience Platform in tempo reale.

## Flusso di Percorso cliente

Nell’esercizio precedente, utilizzando l’app mobile, hai acquistato un prodotto facendo clic sul pulsante **Acquista** pulsante.

![DSN](./images/app20.png)

Supponiamo che tu abbia una domanda sullo stato del tuo ordine, cosa faresti? In genere si chiama il call center.

Prima di chiamare il call center, è necessario conoscere **ID fedeltà**. Puoi trovare il tuo ID fedeltà nel Visualizzatore profili del sito web.

![DSN](./images/cc1.png)

In questo caso, il **ID fedeltà** è **5863105**. Come parte dell’implementazione personalizzata della funzione call center nell’ambiente demo, devi aggiungere un prefisso al tuo **ID fedeltà**. Il prefisso è **11373**, quindi l’ID fedeltà da utilizzare in questo esempio è **5863105 11373**.

Facciamolo adesso. Usa il telefono e chiama il numero **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Ti verrà chiesto di inserire il tuo ID fedeltà, seguito da **N.**. Immetti il tuo ID fedeltà.

![DSN](./images/cc3.png)

Allora sentirai **Ciao, nome**. Questo nome viene preso dal profilo cliente in tempo reale in Adobe Experience Platform. Sono quindi disponibili 3 opzioni. Premi il numero **1**, **Stato ordine**.

![DSN](./images/cc4.png)

Dopo aver sentito lo stato dell’ordine, potrai scegliere di premere **1** per tornare al menu principale oppure premere 2. Premi **2**.

![DSN](./images/cc5.png)

Ti verrà quindi chiesto di valutare l’esperienza del call center selezionando un numero tra 1 e 5, tra 1 (minimo) e 5 (massimo). Fai la tua scelta.

![DSN](./images/cc6.png)

La chiamata al call center terminerà.

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, è necessario selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella linea blu sopra lo schermo. Dopo aver selezionato la [!UICONTROL sandbox], verrà visualizzata la modifica dello schermo e ora si è nel [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Profili** e a **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Seleziona la **Spazio dei nomi dell’identità** **E-mail** e inserisci l’indirizzo e-mail del tuo profilo cliente. Clic **Visualizza**. Fai clic su per aprire il profilo.

![DSN](./images/cc7.png)

Visualizzerai di nuovo il tuo profilo cliente. Vai a **Eventi**.

![DSN](./images/cc8.png)

In events verranno visualizzati 2 eventi con eventType impostato su **callCenter**. Il primo evento è il risultato della risposta alla domanda **Valuta la soddisfazione della tua chiamata**.

![DSN](./images/cc9.png)

Scorri verso il basso per visualizzare l’evento registrato quando hai selezionato l’opzione per controllare la **Stato ordine**.

![DSN](./images/cc10.png)

Vai a **Iscrizione al segmento**. Ora vedrai che 2 segmenti si qualificano sul tuo profilo, in tempo reale, in base alle interazioni che hai avuto attraverso il call center. Queste appartenenze a segmenti possono e devono quindi essere utilizzate per influire su ciò che avviene nella comunicazione e nella personalizzazione attraverso qualsiasi altro canale.

![DSN](./images/cc11.png)

Hai terminato questo esercizio.

[Torna a Flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)

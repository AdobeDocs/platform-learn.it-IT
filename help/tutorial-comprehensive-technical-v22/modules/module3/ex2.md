---
title: Struttura - Profilo cliente in tempo reale - Visualizza il tuo profilo cliente in tempo reale - Interfaccia utente
description: Struttura - Profilo cliente in tempo reale - Visualizza il tuo profilo cliente in tempo reale - Interfaccia utente
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: ed13e37f-48eb-4668-b828-6c58340a7cc1
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---

# 3.2 Visualizzare il proprio profilo cliente in tempo reale - Interfaccia utente

In questo esercizio, accederai a Adobe Experience Platform e visualizzerai il tuo Profilo cliente in tempo reale nell&#39;interfaccia utente.

## Storia

Nel Profilo del cliente in tempo reale, tutti i dati del profilo vengono visualizzati insieme ai dati dell’evento, nonché alle appartenenze al segmento esistenti. I dati mostrati possono provenire da qualsiasi luogo, da applicazioni di Adobe e soluzioni esterne. Questa è la visione più potente di Adobe Experience Platform, il vero sistema di esperienza di record.

## 3.2.1 Utilizzare la visualizzazione Profilo cliente in Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](../module2/images/sb1.png)

Nel menu a sinistra, vai a **Profili** e **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Nel pannello Visualizzatore profilo del sito web puoi trovare più identità. Ogni identità è collegata a uno spazio dei nomi.

![Profilo cliente](./images/identities.png)

Nel pannello Visualizzatore profilo sono disponibili le seguenti combinazioni di ID e namespace:

| Identità | Namespace |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| ID e-mail | woutervangeluwe+06022022-01@gmail.com |
| ID numero cellulare | +32473622044+06022022-01 |

Con Adobe Experience Platform, tutti gli ID sono ugualmente importanti. In precedenza, l’ECID era l’ID più importante nel contesto di Adobe e tutti gli altri ID erano collegati all’ECID in una relazione gerarchica. Con Adobe Experience Platform questo non succede più e ogni ID può essere considerato un identificatore principale.

In genere, l’identificatore principale dipende dal contesto. Se chiedi al tuo call center, **Qual è l&#39;ID più importante?** probabilmente risponderanno, **il numero di telefono!** Ma se chiedi al tuo team CRM, ti risponderanno, **L&#39;indirizzo e-mail!**  Adobe Experience Platform comprende questa complessità e la gestisce per voi. Ogni applicazione, sia che si tratti di un&#39;applicazione di Adobe o di un&#39;applicazione non di Adobe, parlerà con Adobe Experience Platform facendo riferimento all&#39;ID che considera primario. E funziona semplicemente.

Per il campo **Spazio dei nomi identità**, seleziona **E-mail** e per il campo **Valore identità** inserisci l’indirizzo e-mail utilizzato per la registrazione nell’esercizio precedente. Fai clic su **Visualizza**. Vedrai il tuo profilo nell&#39;elenco. Fai clic sul pulsante **ID profilo** per aprire il profilo.

![Profilo cliente](./images/popupecid.png)

Viene visualizzata una panoramica di un paio di elementi importanti **Attributi del profilo** del tuo profilo cliente.

![Profilo cliente](./images/profile.png)

Se desideri visualizzare tutti gli attributi di profilo disponibili per il tuo profilo, vai a **Attributi**.

![Profilo cliente](./images/profilattr.png)

Vai a **Eventi**, dove puoi visualizzare le voci per ogni evento di esperienza collegato al tuo profilo.

![Profilo cliente](./images/profileee.png)

Infine, vai all&#39;opzione di menu **Iscrizione al segmento**. Ora vedrai tutti i segmenti idonei per questo profilo.

![Profilo cliente](./images/profileseg.png)

Ora che hai imparato a visualizzare il profilo in tempo reale di un cliente utilizzando l’interfaccia utente di Adobe Experience Platform, facciamo la stessa cosa attraverso le API utilizzando Postman e Adobe I/O per eseguire query sulle API di Adobe Experience Platform.

Passaggio successivo: [3.3 Visualizzare il proprio profilo cliente in tempo reale - API](./ex3.md)

[Torna al modulo 3](./real-time-customer-profile.md)

[Torna a tutti i moduli](../../overview.md)

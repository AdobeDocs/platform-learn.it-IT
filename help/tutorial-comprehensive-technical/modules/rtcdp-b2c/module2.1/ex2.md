---
title: Foundation - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
description: Foundation - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# 2.1.2 Visualizza il tuo Real-time Customer Profile - UI

In questo esercizio, accederai a Adobe Experience Platform e visualizzerai il tuo Real-time Customer Profile nell’interfaccia utente di.

## Storia

In Real-time Customer Profile, tutti i dati di profilo vengono visualizzati insieme ai dati di evento, così come le appartenenze ai segmenti esistenti. I dati visualizzati possono provenire da qualsiasi luogo, da applicazioni Adobe e soluzioni esterne. Questa è la visualizzazione più potente di Adobe Experience Platform, il vero sistema di esperienza di registrazione.

## 2.1.2.1 Utilizzare la vista Profilo cliente in Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](../../datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](../../datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Profili** e a **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Nel pannello Visualizzatore profili del sito web, puoi trovare più identità. Ogni identità è collegata a uno spazio dei nomi.

![Profilo cliente](./images/identities.png)

Nel pannello Visualizzatore profili puoi vedere le seguenti combinazioni di ID e spazi dei nomi:

| Identità | Namespace |
|:-------------:| :---------------:|
| ID Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| ID e-mail | woutervangeluwe+06022022-01@gmail.com |
| ID numero cellulare | +32473622044+06022022-01 |

Con Adobe Experience Platform, tutti gli ID sono ugualmente importanti. In precedenza, l’ECID era l’ID più importante nel contesto dell’Adobe e tutti gli altri ID erano collegati all’ECID in una relazione gerarchica. Con Adobe Experience Platform questo non avviene più e ogni ID può essere considerato un identificatore primario.

In genere, l’identificatore primario dipende dal contesto. Se si chiede al call center, **Qual è l&#39;ID più importante?** probabilmente risponderanno, **il numero di telefono!** Ma se chiedi al tuo team di gestione delle relazioni con i clienti, ti risponderanno, **L&#39;indirizzo e-mail!** Adobe Experience Platform è consapevole di questa complessità e la gestisce al meglio. Ogni applicazione, che sia un’applicazione Adobe o non Adobe, parlerà con Adobe Experience Platform facendo riferimento all’ID che considerano primario. E funziona semplicemente.

Per il campo **Spazio dei nomi identità**, seleziona **E-mail** e per il campo **Valore identità** immetti l&#39;indirizzo e-mail utilizzato per la registrazione nell&#39;esercizio precedente. Fare clic su **Visualizza**. Visualizzerai quindi il tuo profilo nell’elenco. Fai clic sul **ID profilo** per aprire il tuo profilo.

![Profilo cliente](./images/popupecid.png)

Ora puoi vedere una panoramica di alcuni importanti **Attributi del profilo** del tuo profilo cliente.

![Profilo cliente](./images/profile.png)

Se desideri visualizzare tutti gli attributi di profilo disponibili per il tuo profilo, passa a **Attributi**.

![Profilo cliente](./images/profilattr.png)

Vai a **Eventi**, dove puoi visualizzare le voci per ogni evento esperienza collegato al tuo profilo.

![Profilo cliente](./images/profileee.png)

Infine, passare all&#39;opzione di menu **Appartenenza al segmento**. Ora vedrai tutti i segmenti idonei per questo profilo.

![Profilo cliente](./images/profileseg.png)

Ora che hai imparato a visualizzare il profilo in tempo reale di un cliente utilizzando l’interfaccia utente di Adobe Experience Platform, facciamo lo stesso attraverso le API utilizzando Postman e Adobe I/O per eseguire query sulle API di Adobe Experience Platform.

Passaggio successivo: [2.1.3 Visualizza il tuo profilo cliente in tempo reale - API](./ex3.md)

[Torna al modulo 2.1](./real-time-customer-profile.md)

[Torna a tutti i moduli](../../../overview.md)

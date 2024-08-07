---
title: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
description: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2 Visualizzare il proprio Real-time Customer Profile - UI

In questo esercizio, accederai a Adobe Experience Platform e visualizzerai il tuo Real-time Customer Profile nell’interfaccia utente di.

## Storia

In Real-time Customer Profile, tutti i dati di profilo vengono visualizzati insieme ai dati dell’evento, così come le iscrizioni al pubblico esistenti. I dati visualizzati possono provenire da qualsiasi luogo, da applicazioni Adobe e soluzioni esterne. Questa è la visualizzazione più potente di Adobe Experience Platform, il vero sistema di esperienza di registrazione.

## 1.2.1 Utilizzare la vista Profilo cliente in Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.



Nel menu a sinistra, vai a **Profili** e a **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Nel pannello Visualizzatore profili del sito web, puoi trovare la panoramica dell’identità. Ogni identità è collegata a uno spazio dei nomi.

![Profilo cliente](./images/identities.png)




Con Adobe Experience Platform, tutti gli ID sono ugualmente importanti. In precedenza, l’ECID era l’ID più importante nel contesto dell’Adobe e tutti gli altri ID erano collegati all’ECID in una relazione gerarchica. Con Adobe Experience Platform questo non avviene più e ogni ID può essere considerato un identificatore primario.

In genere, l’identificatore primario dipende dal contesto. Se si chiede al call center, **Qual è l&#39;ID più importante?** probabilmente risponderanno, **il numero di telefono!** Ma se chiedi al tuo team di gestione delle relazioni con i clienti, ti risponderanno, **L&#39;indirizzo e-mail!** Adobe Experience Platform è consapevole di questa complessità e la gestisce al meglio. Ogni applicazione, che sia un&#39;applicazione di Adobe o non di Adobe, parlerà con Adobe Experience Platform facendo riferimento all&#39;ID che considerano primario. E funziona semplicemente.

Per il campo **Spazio dei nomi identità**, seleziona **ECID** e per il campo **Valore identità** immetti l&#39;ECID che puoi trovare nel pannello Visualizzatore profili del sito Web di bootcamp. Fare clic su **Visualizza**. Visualizzerai quindi il tuo profilo nell’elenco. Fai clic sul **ID profilo** per aprire il tuo profilo.

![Profilo cliente](./images/popupecid.png)

Ora puoi vedere una panoramica di alcuni importanti **Attributi del profilo** del tuo profilo cliente.

![Profilo cliente](./images/profile.png)

Vai a **Eventi**, dove puoi visualizzare le voci per ogni evento esperienza collegato al tuo profilo.

![Profilo cliente](./images/profileee.png)

Infine, passare all&#39;opzione di menu **Appartenenza al pubblico**. Ora vedrai tutti i tipi di pubblico idonei per questo profilo.

![Profilo cliente](./images/profileseg.png)

Ora creiamo un nuovo pubblico che ti consentirà di personalizzare l’esperienza del cliente per un cliente anonimo o noto.

Passaggio successivo: [1.3 Creare un pubblico - Interfaccia utente](./ex3.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)

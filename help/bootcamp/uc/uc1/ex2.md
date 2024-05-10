---
title: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
description: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 47b9c3553bd0dae39f8271446dd15ee2f6df4d41
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 1.2 Visualizzare il proprio Real-time Customer Profile - UI

In questo esercizio, accederai a Adobe Experience Platform e visualizzerai il tuo Real-time Customer Profile nell’interfaccia utente di.

## Storia

In Real-time Customer Profile, tutti i dati di profilo vengono visualizzati insieme ai dati di evento, così come le appartenenze ai segmenti esistenti. I dati visualizzati possono provenire da qualsiasi luogo, da applicazioni Adobe e soluzioni esterne. Questa è la visualizzazione più potente di Adobe Experience Platform, il vero sistema di esperienza di registrazione.

## 1.2.1 Utilizzare la vista Profilo cliente in Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, è necessario selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella linea blu sopra lo schermo. Dopo aver selezionato la [!UICONTROL sandbox], verrà visualizzata la modifica dello schermo e ora si è nel [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Profili** e a **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Nel pannello Visualizzatore profili del sito web, puoi trovare la panoramica dell’identità. Ogni identità è collegata a uno spazio dei nomi.

![Profilo cliente](./images/identities.png)

Con Adobe Experience Platform, tutti gli ID sono ugualmente importanti. In precedenza, l’ECID era l’ID più importante nel contesto dell’Adobe e tutti gli altri ID erano collegati all’ECID in una relazione gerarchica. Con Adobe Experience Platform questo non avviene più e ogni ID può essere considerato un identificatore primario.

In genere, l’identificatore primario dipende dal contesto. Se si chiede al Call Center, **Qual è l’ID più importante?** probabilmente risponderanno, **il numero di telefono!** Ma se chiedi al tuo team di gestione delle relazioni con i clienti, ti risponderanno, **L&#39;indirizzo e-mail!**  Adobe Experience Platform è consapevole di questa complessità e la gestisce al meglio. Ogni applicazione, che sia un&#39;applicazione di Adobe o non di Adobe, parlerà con Adobe Experience Platform facendo riferimento all&#39;ID che considerano primario. E funziona semplicemente.

Per il campo **Spazio dei nomi dell’identità**, seleziona **ECID** e per il campo **Valore identità** immetti l’ECID che puoi trovare nel pannello Visualizzatore profili del sito web di bootcamp. Clic **Visualizza**. Visualizzerai quindi il tuo profilo nell’elenco. Fai clic su **ID profilo** per aprire il profilo.

![Profilo cliente](./images/popupecid.png)

Ora puoi vedere una panoramica di alcuni importanti **Attributi del profilo** del tuo profilo cliente.

![Profilo cliente](./images/profile.png)

Vai a **Eventi**, dove puoi visualizzare le voci per ogni evento esperienza collegato al tuo profilo.

![Profilo cliente](./images/profileee.png)

Infine, vai all’opzione del menu **Iscrizione al segmento**. Ora vedrai tutti i segmenti idonei per questo profilo.

![Profilo cliente](./images/profileseg.png)

Ora creiamo un nuovo segmento che ti consentirà di personalizzare l’esperienza del cliente per un cliente anonimo o noto.

Passaggio successivo: [1.3 Creare un segmento - Interfaccia utente](./ex3.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)

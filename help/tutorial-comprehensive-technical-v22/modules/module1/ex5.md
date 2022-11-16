---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Analytics e Adobe Audience Manager
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Analytics e Adobe Audience Manager
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: e3ef6534-9af9-4b8c-86d0-46f413f4ff6d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---

# 1.5 - Implementare Adobe Analytics e Adobe Audience Manager

## Contesto

Ora sai che i dati XDM scorrono nella piattaforma. Ulteriori informazioni su XDM [Modulo 2](./../module2/data-ingestion.md), nonché come creare uno schema personalizzato per monitorare le variabili personalizzate. Per il momento esaminerai cosa accade quando imposti il tuo Datastream per inoltrare i dati ad Analytics ed Audience Manager.

## 1.5.1 Mappatura delle variabili in Analytics

Adobe Experience Platform [!DNL Web SDK] mappa automaticamente alcuni valori, rendendo più rapida possibile una nuova implementazione di Analytics tramite l’SDK per web. Sono elencate le variabili mappate automaticamente [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

Per i dati XDM a cui non viene mappato automaticamente [!DNL Adobe Analytics], puoi utilizzare [dati contestuali](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=it) per abbinare [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it). Quindi può essere mappato in [!DNL Analytics] utilizzo [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) per popolare [!DNL Analytics] variabili. Le regole di elaborazione e di dati contestuali saranno concetti familiari a quelli che hanno lavorato con Analytics in passato, ma non preoccuparti dei dettagli per il momento se si tratta di nuovi concetti.

Puoi anche utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con AEP [!DNL Web SDK]. Per eseguire questa operazione, vedi [Prodotti](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection).

### Dati contestuali

Da utilizzare [!DNL Analytics], i dati XDM vengono appiattiti utilizzando la notazione del punto e resi disponibili come `contextData`. Il seguente elenco di coppie di valori mostra un esempio di `context data`:

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### Regole di elaborazione

Tutti i dati raccolti dalla rete Edge sono accessibili tramite [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], è possibile utilizzare le regole di elaborazione per incorporare i dati contestuali in [!DNL Analytics] variabili.

## Audience Manager 1.5.2 su Experience Platform Edge Network

L&#39;inoltro lato server non è un nuovo concetto, ad Audience Manager, e si applica lo stesso processo di prima. Puoi anche sincronizzare le identità.

## 1.5.3 Rivedi il tuo Datastream per inviare dati ad Adobe Analytics

Se desideri inviare ad Adobe Analytics e Adobe Audience Manager i dati raccolti dall’SDK per web, procedi come segue.

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vai a **Datastreams**.

Nell’angolo in alto a destra dello schermo, seleziona il nome della sandbox, che deve essere `--aepSandboxId--`. Apri il tuo datastream specifico, denominato `--demoProfileLdap-- - Demo System Datastream`.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1b.png)

Vedrete questo. Per abilitare Adobe Analytics, fai clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Vedrete questo. Selezionare il servizio **Adobe Analytics**, dopodiché devi aggiungere la suite di rapporti in Adobe Analytics per inviare i dati a . In questa esercitazione, non rientra nell’ambito di applicazione. Fai clic su **Annulla**.

![Debugger AEP](./images/aa3.png)

## 1.5.4 Rivedi il tuo Datastream per inviare dati a Adobe Audience Manager

Vedrete questo. Per abilitare Adobe Audience Manager, fai clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Vedrete questo. Selezionare il servizio **Adobe Audience Manager** dopo di che puoi decidere di abilitare o disabilitare le destinazioni cookie Adobe Audience Manager e/o le destinazioni URL. In questa esercitazione, questa configurazione è fuori ambito. Fai clic su **Annulla**.

![Debugger AEP](./images/aam1.png)

Passaggio successivo: [1.6 Implementare Adobe Target](./ex6.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)

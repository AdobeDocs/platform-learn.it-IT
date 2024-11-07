---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementazione di Adobe Analytics e Adobe Audience Manager
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementazione di Adobe Analytics e Adobe Audience Manager
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 1.1.5 - Implementare Adobe Analytics e Adobe Audience Manager

## Contesto

Ora sai che i dati XDM fluiscono in Platform. Ulteriori informazioni su XDM nel [Modulo 2](./../module1.2/data-ingestion.md) e su come creare uno schema personalizzato per tenere traccia delle variabili personalizzate. Per ora vedrai cosa accade quando imposti lo stream di dati per inoltrare i dati ad Analytics e Audience Manager.

## 1.1.5.1 Mappatura delle variabili in Analytics

Adobe Experience Platform [!DNL Web SDK] mappa automaticamente alcuni valori, rendendo più rapida possibile una nuova implementazione di Analytics tramite l&#39;SDK Web. Le variabili mappate automaticamente sono elencate [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

Per i dati XDM che non sono mappati automaticamente a [!DNL Adobe Analytics], puoi utilizzare [dati contestuali](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=it) per far corrispondere il tuo [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it). Quindi può essere mappato in [!DNL Analytics] utilizzando [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) per popolare [!DNL Analytics] variabili. I dati contestuali e le regole di elaborazione saranno concetti familiari a quelli che hanno lavorato con Analytics in passato, ma per il momento non preoccuparti dei dettagli se si tratta di concetti nuovi.

È inoltre possibile utilizzare un set predefinito di azioni ed elenchi di prodotti per inviare o recuperare dati con AEP [!DNL Web SDK]. Per eseguire questa operazione, vedere [Prodotti](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection).

### Dati contestuali

I dati XDM da utilizzare da [!DNL Analytics] vengono appiattiti utilizzando la notazione del punto e resi disponibili come `contextData`. Il seguente elenco di coppie di valori mostra un esempio di `context data`:

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

Tutti i dati raccolti dalla rete Edge sono accessibili tramite [regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics] è possibile utilizzare le regole di elaborazione per incorporare i dati contestuali nelle variabili [!DNL Analytics].

## 1.1.5.2 Audience Manager sull&#39;Edge Network di Experience Platform

L’inoltro lato server, ad Audience Manager, non è un concetto nuovo e si applica la stessa procedura descritta in precedenza. Puoi anche sincronizzare le identità.

## 1.1.5.3 Verifica lo stream di dati per inviare dati ad Adobe Analytics

Se desideri inviare i dati raccolti da Web SDK ad Adobe Analytics e Adobe Audience Manager, segui la procedura riportata di seguito.

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vai a **Datastreams**.

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`. Apri lo stream di dati specifico, denominato `--aepUserLdap-- - Demo System Datastream`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Poi vedrai questo. Per abilitare Adobe Analytics, fare clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Poi vedrai questo. Seleziona il servizio **Adobe Analytics**, dopo il quale devi aggiungere la suite di rapporti in Adobe Analytics per inviare dati in. In questa esercitazione, questo non rientra nell’ambito di applicazione. Fare clic su **Annulla**.

![Debugger AEP](./images/aa3.png)

## 1.1.5.4 Verifica lo stream di dati per inviare dati a Adobe Audience Manager

Poi vedrai questo. Per abilitare Adobe Audience Manager, fare clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Poi vedrai questo. Seleziona il servizio **Adobe Audience Manager** dopo il quale puoi decidere di abilitare o disabilitare le destinazioni dei cookie Adobe Audience Manager e/o le destinazioni degli URL. In questa esercitazione, questa configurazione non rientra nell&#39;ambito. Fare clic su **Annulla**.

![Debugger AEP](./images/aam1.png)

Passaggio successivo: [1.1.6 Implementare Adobe Target](./ex6.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)

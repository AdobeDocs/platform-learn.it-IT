---
title: AEM CS - Blocco personalizzato avanzato
description: AEM CS - Blocco personalizzato avanzato
kt: 5342
doc-type: tutorial
source-git-commit: 2f53c8da2cbe833120fa6555c65b8b753bfa4f8d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 2.1.6 Plug-in MarTech per Edge Delivery Services AEM

Il plug-in AEM MarTech consente di impostare rapidamente uno stack MarTech completo per il progetto AEM.

>[!NOTE]
>
>Questo plug-in è attualmente disponibile per i clienti in collaborazione con AEM Engineering tramite progetti di co-innovazione. Ulteriori informazioni sono disponibili su [https://github.com/adobe-rnd/aem-martech](https://github.com/adobe-rnd/aem-martech).

Passa alla cartella in uso per l&#39;archivio GitHub **citisignal**. Fare clic con il pulsante destro del mouse sul nome della cartella, quindi selezionare **Nuovo terminale nella cartella**.

![AEMCS](./images/mtplugin1.png)

Poi vedrai questo. Incolla il seguente comando e premi **invio**.

```
git subtree add --squash --prefix plugins/martech https://github.com/adobe/aem-experimentation.git main
```

Dovresti vedere questo.

![AEMCS](./images/mtplugin3.png)

Passa alla cartella in uso per l&#39;archivio GitHub **citisignal**, apri la cartella **plugins**. Dovresti ora visualizzare una cartella denominata **martech**.

![AEMCS](./images/mtplugin4.png)


In Visual Studio Code aprire il file **head.html**. Copiare il codice seguente e incollarlo nel file **head.html**.

```javascript
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/index.js"/>
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/alloy.min.js"/>
<link rel="preconnect" href="https://edge.adobedc.net"/>
<!-- change to adobedc.demdex.net if you enable third party cookies -->
```

Salva le modifiche.

![AEMCS](./images/mtplugin5.png)

In Visual Studio Code, passare alla cartella **scripts** e aprire il file **scripts.js**. Copiare il codice seguente e incollarlo nel file **scripts.js**, negli script di importazione esistenti.

```javascript
import {
  initMartech,
  updateUserConsent,
  martechEager,
  martechLazy,
  martechDelayed,
} from '../plugins/martech/src/index.js';
```

Salva le modifiche.

![AEMCS](./images/mtplugin6.png)

```javascript
const isConsentGiven = true;
  const martechLoadedPromise = initMartech(
    // The WebSDK config
    // Documentation: https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview#configure-js
    {
      datastreamId: "045c5ee9-468f-47d5-ae9b-a29788f5948f",
      orgId: "907075E95BF479EC0A495C73@AdobeOrg",
      onBeforeEventSend: (payload) => {
        // set custom Target params 
        // see doc at https://experienceleague.adobe.com/en/docs/platform-learn/migrate-target-to-websdk/send-parameters#parameter-mapping-summary
        payload.data.__adobe.target ||= {};

        // set custom Analytics params
        // see doc at https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping
        payload.data.__adobe.analytics ||= {};
      },

      // set custom datastream overrides
      // see doc at:
      // - https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/datastream-overrides
      // - https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides
      edgeConfigOverrides: {
        // Override the datastream id
        // datastreamId: '...'

        // Override AEP event datasets
        // com_adobe_experience_platform: {
        //   datasets: {
        //     event: {
        //       datasetId: '...'
        //     }
        //   }
        // },

        // Override the Analytics report suites
        // com_adobe_analytics: {
        //   reportSuites: ['...']
        // },

        // Override the Target property token
        // com_adobe_target: {
        //   propertyToken: '...'
        // }
      },
    },
    // The library config
    {
      launchUrls: ["https://assets.adobedtm.com/b754ed1bed61/b9f7c7c484de/launch-28b548849fb9.min.js"],
      personalization: !!getMetadata('target') && isConsentGiven,
    },
  );
```

![AEMCS](./images/mtplugin8.png)

![AEMCS](./images/mtplugin7.png)

```javascript
if (main) {
    decorateMain(main);
    await Promise.all([
      martechLoadedPromise.then(martechEager),
      waitForLCP(LCP_BLOCKS),
    ]);
  }
```

![AEMCS](./images/mtplugin10.png)

```javascript
await martechLazy();
```

![AEMCS](./images/mtplugin9.png)

```javascript
window.setTimeout(() => {
    martechDelayed();
    return import('./delayed.js');
  }, 3000);
```

![AEMCS](./images/mtplugin11.png)


![AEMCS](./images/mtplugin12.png)


![AEMCS](./images/mtplugin13.png)

Potrai visualizzare le modifiche apportate al tuo sito web andando su `main--citisignal--XXX.aem.page/us/en` e/o `main--citisignal--XXX.aem.live/us/en`, dopo aver sostituito XXX con il tuo account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal--woutervangeluwe.aem.page/us/en` e/o `https://main--citisignal--woutervangeluwe.aem.live/us/en`.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md){target="_blank"}

[Torna al modulo 2.1](./aemcs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

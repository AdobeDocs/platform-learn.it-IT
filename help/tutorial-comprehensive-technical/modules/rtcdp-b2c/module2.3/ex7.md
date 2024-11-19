---
title: Real-time CDP - SDK Destinazioni
description: Real-time CDP - SDK Destinazioni
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 5%

---

# 2.3.7 SDK delle destinazioni

## Configurare il progetto Adobe I/O

In questo esercizio utilizzerai nuovamente Adobe I/O per eseguire query sulle API di Adobe Experience Platform. Se non hai ancora configurato il progetto Adobe I/O, torna all&#39;[Esercizio 3 nel Modulo 2.1](../module2.1/ex3.md) e segui le istruzioni.

## Autenticazione Postman da Adobe I/O

In questo esercizio utilizzerai nuovamente Postman per eseguire query sulle API di Adobe Experience Platform. Se non hai ancora configurato l&#39;applicazione Postman, torna all&#39;[esercizio 3 nel modulo 2.1](../module2.1/ex3.md) e segui le istruzioni.

## Definire endpoint e formato

Per questo esercizio, dovrai configurare un endpoint in modo che, quando un segmento si qualifica, l’evento di qualifica possa essere inviato in streaming a tale endpoint. In questo esercizio utilizzerai un endpoint di esempio utilizzando [https://webhook.site/](https://webhook.site/). Vai a [https://webhook.site/](https://webhook.site/), dove vedrai qualcosa di simile. Fai clic su **Copia negli Appunti** per copiare l&#39;URL. Nel prossimo esercizio dovrai specificare questo URL. L&#39;URL in questo esempio è `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Acquisizione dei dati](./images/webhook1.png)

Per quanto riguarda il formato, utilizzeremo un modello standard che trasmetterà in streaming le qualifiche o le non qualifiche dei segmenti insieme a metadati come gli identificatori dei clienti. I modelli possono essere personalizzati per soddisfare le aspettative di endpoint specifici, ma in questo esercizio riutilizzeremo un modello standard, che si tradurrà in un payload come questo che verrà inviato in streaming all’endpoint.

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## Creare una configurazione di server e modelli

Il primo passaggio per creare una tua destinazione in Adobe Experience Platform consiste nel creare una configurazione di server e modelli.

A tale scopo, passare a **Destination Authoring API**, a **Server e modelli di destinazione** e fare clic per aprire la richiesta **POST - Crea una configurazione del server di destinazione**. Poi vedrai questo. In **Intestazioni**, devi aggiornare manualmente il valore per la chiave **x-sandbox-name** e impostarlo su `--aepSandboxName--`. Selezionare il valore **{{SANDBOX_NAME}}**.

![Acquisizione dei dati](./images/sdkpm1.png)

Sostituiscilo con `--aepSandboxName--`.

![Acquisizione dei dati](./images/sdkpm2.png)

Quindi, vai a **Corpo**. selezionare il segnaposto **{{body}}**.

![Acquisizione dei dati](./images/sdkpm3.png)

Sostituire il segnaposto **{{body}}** con il codice seguente:

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

Dopo aver incollato il codice precedente, è necessario aggiornare manualmente il campo **urlBasedDestination.url.value** e impostarlo sull&#39;URL del webhook creato nel passaggio precedente, che era `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` in questo esempio.

![Acquisizione dei dati](./images/sdkpm4.png)

Dopo aver aggiornato il campo **urlBasedDestination.url.value**, dovrebbe essere simile al seguente. Fai clic su **Invia**.

![Acquisizione dei dati](./images/sdkpm5.png)

Dopo aver fatto clic su **Invia**, verrà creato il modello del server e come parte della risposta verrà visualizzato un campo denominato **instanceId**. Scrivilo, come ti servirà nel passaggio successivo. In questo esempio, **instanceId** è
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Acquisizione dei dati](./images/sdkpm6.png)

## Creare la configurazione di destinazione

In Postman, in **Destination Authoring API**, vai a **Destination configurations** e fai clic per aprire la richiesta **POST - Create a destination configuration**. Poi vedrai questo. In **Intestazioni**, devi aggiornare manualmente il valore per la chiave **x-sandbox-name** e impostarlo su `--aepSandboxName--`. Selezionare il valore **{{SANDBOX_NAME}}**.

![Acquisizione dei dati](./images/sdkpm7.png)

Sostituiscilo con `--aepSandboxName--`.

![Acquisizione dei dati](./images/sdkpm8.png)

Quindi, vai a **Corpo**. selezionare il segnaposto **{{body}}**.

![Acquisizione dei dati](./images/sdkpm9.png)

Sostituire il segnaposto **{{body}}** con il codice seguente:

```json
{
    "name": "--aepUserLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![Acquisizione dei dati](./images/sdkpm11.png)

Dopo aver incollato il codice precedente, devi aggiornare manualmente il campo **destinationDelivery. destinationServerId**, e devi impostarlo su **instanceId** del modello del server di destinazione creato nel passaggio precedente, che era `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` in questo esempio. Fare clic su **Invia**.

![Acquisizione dei dati](./images/sdkpm10.png)

Vedrai questa risposta.

![Acquisizione dei dati](./images/sdkpm12.png)

La destinazione viene ora creata in Adobe Experience Platform. Andiamo lì e controlliamo.

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, fai clic su **Catalogo** e scorri verso il basso fino alla categoria **Streaming**. La destinazione sarà ora disponibile.

![Acquisizione dei dati](./images/destsdk1.png)

## Collegare il segmento alla destinazione

In **Destinazioni** > **Catalogo**, fai clic su **Configura** nella tua destinazione per iniziare ad aggiungere segmenti alla nuova destinazione.

![Acquisizione dei dati](./images/destsdk2.png)

Immettere un token portatore fittizio, ad esempio **1234**. Fai clic su **Connetti alla destinazione**.

![Acquisizione dei dati](./images/destsdk3.png)

Poi vedrai questo. Come nome per la destinazione, utilizzare `--aepUserLdap-- - Webhook`. Seleziona un endpoint di scelta, in questo esempio **EU**. Fai clic su **Avanti**.

![Acquisizione dei dati](./images/destsdk4.png)

È possibile selezionare un criterio di governance dei dati. Fai clic su **Avanti**.

![Acquisizione dei dati](./images/destsdk5.png)

Selezionare il segmento creato in precedenza, denominato `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Fai clic su **Avanti**.

![Acquisizione dei dati](./images/destsdk6.png)

Poi vedrai questo. Assicurarsi di mappare il **CAMPO SOURCE** `--aepTenantId--.identification.core.ecid` al campo `Identity: ecid`. Fai clic su **Avanti**.

![Acquisizione dei dati](./images/destsdk7.png)

Fai clic su **Fine**.

![Acquisizione dei dati](./images/destsdk8.png)

La destinazione è ora live, le nuove qualifiche dei segmenti verranno inviate in streaming al tuo webhook personalizzato ora.

![Acquisizione dei dati](./images/destsdk9.png)

## Test dell’attivazione dei segmenti

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Nella pagina **Integrazioni** è necessario selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Dalla home page di **Luma**, vai a **Men** e fai clic sul prodotto **CAMICIA FITNESS PROTEUS**.

![Acquisizione dei dati](./images/homenadia.png)

Hai visitato la pagina dei prodotti per **PROTEUS FITNESS JACKSHIRT**, il che significa che ora potrai qualificarti per il segmento creato in precedenza in questo esercizio.

![Acquisizione dei dati](./images/homenadiapp.png)

Quando apri il Visualizzatore profili e vai a **Segmenti**, vedrai il segmento idoneo.

![Acquisizione dei dati](./images/homenadiapppb.png)

Torna al webhook aperto su [https://webhook.site/](https://webhook.site/), dove dovresti trovare una nuova richiesta in arrivo, proveniente da Adobe Experience Platform, che contiene l&#39;evento di qualificazione del segmento.

![Acquisizione dei dati](./images/destsdk10.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)

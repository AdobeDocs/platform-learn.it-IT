---
title: AEM CS - Blocco personalizzato di base
description: AEM CS - Blocco personalizzato di base
kt: 5342
doc-type: tutorial
exl-id: 57c08a88-d885-471b-ad78-1dba5992da9d
source-git-commit: 2f53c8da2cbe833120fa6555c65b8b753bfa4f8d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 2.1.4 Sviluppare un blocco personalizzato di base

## 2.1.4.1 Configurare l’ambiente di sviluppo locale

Vai a [https://desktop.github.com/download/](https://desktop.github.com/download/){target="_blank"}, scarica e installa **Github Desktop**.

![Blocca](./images/block1.png)

Una volta installato Github Desktop, vai all’archivio GitHub creato nell’esercizio precedente. Fare clic su **&lt;> Codice** e quindi su **Apri con GitHub Desktop**.

![Blocca](./images/block2.png)

L’archivio GitHub verrà quindi aperto in GitHub Desktop. Puoi cambiare il **percorso locale**. Fare clic su **Clona**.

![Blocca](./images/block3.png)

Verrà ora creata una cartella locale.

![Blocca](./images/block4.png)

Aprire Visual Studio Code. Vai a **File** > **Apri cartella**.

![Blocca](./images/block5.png)

Seleziona la cartella utilizzata dalla configurazione GitHub per **citisignal**.

![Blocca](./images/block6.png)

La cartella verrà aperta in Visual Studio Code e sarà possibile creare un nuovo blocco.

![Blocca](./images/block7.png)

## 2.1.4.2 Creare un blocco personalizzato di base

Adobe consiglia di sviluppare blocchi in un approccio in tre fasi:

- Crea la definizione e il modello per il blocco, rivedilo e portalo in produzione.
- Crea contenuto con il nuovo blocco.
- Implementa la decorazione e gli stili per il nuovo blocco.

### component-definition.json

In Visual Studio Code aprire il file **component-definition.json**.

![Blocca](./images/block8.png)

Scorri verso il basso fino a visualizzare il componente **Preventivo**. Impostare il cursore accanto alla parentesi quadra di chiusura dell&#39;ultimo componente.

![Blocca](./images/block9.png)

Incolla questo codice e immetti una virgola **,** dopo il blocco di codice:

```json
{
  "title": "FiberOffer",
  "id": "fiberoffer",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "FiberOffer",
          "model": "fiberoffer",
          "offerText": "<p>Fiber will soon be available in your region!</p>",
          "offerCallToAction": "Get your offer now!",
          "offerImage": ""
        }
      }
    }
  }
}
```

Salva le modifiche.

![Blocca](./images/block10.png)

### component-models.json

In Visual Studio Code aprire il file **component-models.json**.

![Blocca](./images/block11.png)

Scorri verso il basso fino a visualizzare l’ultimo elemento. Impostare il cursore accanto alla parentesi quadra di chiusura dell&#39;ultimo componente.

![Blocca](./images/block12.png)

Inserisci una virgola **,**, quindi premi Invio e, alla riga successiva, incolla questo codice:

```json
{
  "id": "fiberoffer",
  "fields": [
     {
       "component": "richtext",
       "name": "offerText",
       "value": "",
       "label": "Offer Text",
       "valueType": "string"
     },
     {
       "component": "richtext",
       "valueType": "string",
       "name": "offerCallToAction",
       "label": "Offer CTA",
       "value": ""
     },
     {
       "component": "reference",
       "valueType": "string",
       "name": "offerImage",
       "label": "Offer Image",
        "multi": false
     }
   ]
}
```

Salva le modifiche.

![Blocca](./images/block13.png)

### component-filters.json

In Visual Studio Code aprire il file **component-filters.json**.

![Blocca](./images/block14.png)

In **sezione**, inserisci una virgola **,** e l&#39;ID del componente **fiberoffer** dopo l&#39;ultima riga corrente.

Salva le modifiche.

![Blocca](./images/block15.png)

## 2.1.4.3 Eseguire il commit delle modifiche

Hai ora apportato diverse modifiche al progetto che devono essere salvate nell’archivio GitHub. Per farlo, apri **GitHub Desktop**.

Dovresti quindi visualizzare i 3 file appena modificati in **Modifiche**. Rivedi le modifiche.

![Blocca](./images/block16.png)

Immettere un nome per la PR, `Fiber Offer custom block`. Fare clic su **Commit to main**.

![Blocca](./images/block17.png)

Dovresti vedere questo. Fare clic su **Origine push**.

![Blocca](./images/block18.png)

Dopo un paio di secondi, le modifiche sono state inviate all’archivio GitHub.

![Blocca](./images/block19.png)

Nel browser, vai all’account GitHub e all’archivio creato per CitiSignal. Dovresti quindi vedere qualcosa di simile, che mostra che le modifiche sono state ricevute.

![Blocca](./images/block20.png)

## 2.1.4.4 Aggiungere il blocco a una pagina

Ora che il blocco delle virgolette di base è definito e confermato nel progetto CitiSignal, puoi aggiungere un blocco **fiberoffer** a una pagina esistente.

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png)

Fare clic sui tre punti **...** nella scheda **Ambienti** e quindi su **Visualizza dettagli**.

![AEMCS](./images/aemcs9.png)

Visualizzerai quindi i dettagli dell’ambiente. Fai clic sull&#39;URL dell&#39;ambiente **Author**.

>[!NOTE]
>
>È possibile che l’ambiente sia ibernato. In questo caso, devi prima riattivare l’ambiente.

![AEMCS](./images/aemcs10.png)

Dovresti quindi visualizzare l’ambiente di authoring dell’AEM. Vai a **Sites**.

![AEMCS](./images/block21.png)

Vai a **CitiSignal** > **us** > **en**.

![AEMCS](./images/block22.png)

Fai clic su **Crea** e seleziona **Pagina**.

![AEMCS](./images/block23.png)

Seleziona **Pagina** e fai clic su **Avanti**.

![AEMCS](./images/block24.png)

Immetti i seguenti valori:

- Titolo: **Fibra CitiSignal**
- Nome: **citisignal-fibre**
- Titolo pagina: **Fibra CitiSignal**

Fai clic su **Crea**.

![AEMCS](./images/block25.png)

Dovresti vedere questo.

![AEMCS](./images/block26.png)

Fare clic nell&#39;area vuota per selezionare il componente **sezione**. Quindi, fai clic sull&#39;icona più **+** nel menu a destra.

![AEMCS](./images/block27.png)

Dovresti quindi visualizzare il blocco personalizzato nell’elenco dei blocchi disponibili. Fai clic su per selezionarlo.

![AEMCS](./images/block28.png)

Vedrai quindi campi come **Testo offerta**, **CTA offerta** e **Immagine offerta** aggiunti all&#39;editor. Fai clic su **+ Aggiungi** nel campo **Immagine offerta** per selezionare un&#39;immagine.

![AEMCS](./images/block29.png)

Dovresti vedere questo. Fare clic per aprire la cartella **citisignal**.

![AEMCS](./images/blockpub1.png)

Seleziona l&#39;immagine **product-richment-1.png**. Fai clic su **Seleziona**.

![AEMCS](./images/blockpub2.png)

Dovresti avere questo. Fare clic su **Publish**.

![AEMCS](./images/blockpub3.png)

Fai di nuovo clic su **Publish**.

![AEMCS](./images/blockpub4.png)

La nuova pagina è stata pubblicata.

## 2.1.4.5 Aggiungi la nuova pagina al menu di navigazione

Nella panoramica di AEM Sites, vai a **CitiSignal** > **Frammenti** e seleziona la casella di controllo per **Intestazione**. Fai clic su **Modifica**.

![AEMCS](./images/nav0.png)

Aggiungere un&#39;opzione di menu al menu di navigazione con il testo `Fiber`. Seleziona il testo **Fibre** e fai clic sull&#39;icona **link**.

![AEMCS](./images/nav1.png)

Immetti questo valore per **URL** `/us/en/citisignal-fiber` e fai clic sull&#39;icona **V** per confermare.

![AEMCS](./images/nav3.png)

Dovresti avere questo. Fare clic su **Publish**.

![AEMCS](./images/nav4.png)

Fai di nuovo clic su **Publish**.

![AEMCS](./images/nav5.png)

Potrai visualizzare le modifiche apportate al tuo sito web andando su `main--citisignal--XXX.aem.page/us/en` e/o `main--citisignal--XXX.aem.live/us/en`, dopo aver sostituito XXX con il tuo account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal--woutervangeluwe.aem.page/us/en` e/o `https://main--citisignal--woutervangeluwe.aem.live/us/en`.

Dovresti vedere questo. Fare clic su **Fibra**.

![AEMCS](./images/nav6.png)

Questo è il blocco personalizzato di base, ma ora è incluso nel rendering sul sito web.

![AEMCS](./images/nav7.png)

Passaggio successivo: [2.1.5 Blocco personalizzato avanzato](./ex5.md){target="_blank"}

[Torna al modulo 2.1](./aemcs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

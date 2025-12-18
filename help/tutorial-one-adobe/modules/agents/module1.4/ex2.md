---
title: Implementare Brand Concierge sul sito web
description: Implementare Brand Concierge sul sito web
kt: 5342
doc-type: tutorial
source-git-commit: fb1fc5c72723cc4e1ede87f90410feb0cc314eea
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# 1.4.2 Implementare Brand Concierge sul sito web

>[!IMPORTANT]
>
>Per completare questo esercizio, è necessario avere accesso a un ambiente AEM Assets CS Author funzionante e a un sito Web AEM CS/EDS.
>
>Se non disponi di un ambiente di questo tipo, passa a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.4.2.1 Configura il tuo sito Web per mostrare Brand Concierge - AEM Author

Affinché Brand Concierge venga visualizzato sul sito web, devi creare un nuovo blocco personalizzato che deve essere aggiunto a una nuova pagina e assicurarti che la nuova pagina sia aggiunta alla navigazione del sito web.

Ora devi configurare i seguenti elementi in questo ordine:

- Crea un nuovo blocco personalizzato da utilizzare per caricare Brand Concierge sul sito web.
- Crea una nuova pagina sul tuo sito web per Brand Concierge.
- Collega il blocco personalizzato appena creato nella pagina Brand Concierge appena creata.
- Aggiungi un riferimento per passare alla pagina Brand Concierge appena creata nel file di intestazione del sito web.

### Crea nuovo blocco personalizzato

Per creare il nuovo blocco personalizzato, accedi all’archivio GitHub collegato al tuo sito web.

![Blocca](./images/block1.png)

#### component-definition.json

Scorri verso il basso fino a visualizzare il file **component-definition.json** e aprilo

![Blocca](./images/block8.png)

Fai clic sull&#39;icona **pencl** per iniziare a modificare il file.

![Blocca](./images/block8a.png)

Scorri verso il basso fino a visualizzare i **blocchi**. Imposta il cursore sotto la parentesi quadra di chiusura del componente **Schede**

![Blocca](./images/block9.png)

Incolla questo codice e immetti una virgola **,** dopo il blocco di codice:

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

Fare clic su **Commit changes...**.

![Blocca](./images/block10.png)

Fai clic su **Commit changes**.

![Blocca](./images/block10a.png)

#### component-models.json

Scorri verso il basso fino a visualizzare il file **component-models.json** e fai clic sull&#39;icona **pencil** per iniziare a modificare il file.

![Blocca](./images/block11.png)

Scorri verso il basso fino a visualizzare l’ultimo elemento. Impostare il cursore accanto alla parentesi quadra di chiusura dell&#39;ultimo componente.

![Blocca](./images/block12.png)

Inserisci una virgola **,**, quindi premi Invio e, alla riga successiva, incolla questo codice:

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

Fare clic su **Commit changes...**.

![Blocca](./images/block13.png)

Fai clic su **Commit changes**.

![Blocca](./images/block13a.png)

#### component-filters.json

Scorri verso il basso fino a visualizzare il file **component-filters.json** e fai clic sull&#39;icona **pencil** per iniziare a modificare il file.

![Blocca](./images/block14.png)

Dovresti vedere questo.

![Blocca](./images/block14a.png)

In **sezione**, inserisci una virgola `,` e incolla l&#39;ID del componente `"brandconcierge"` dopo l&#39;ultima riga corrente.

Fare clic su **Commit changes...**.

![Blocca](./images/block15.png)

Fai clic su **Commit changes**.

![Blocca](./images/block15a.png)

#### brandconcierge.css

Durante la creazione di un blocco, è consigliabile creare un file per lo stile del blocco e deve avere lo stesso nome del blocco. ora devi creare il file, che per il momento rimarrà vuoto.

Vai alla cartella **blocca**. Quindi fare clic su **Aggiungi file** e selezionare **Crea nuovo file**.

![Blocca](./images/css1.png)

Nella casella di testo immettere `brandconcierge/brandconcierge.css`. Il file può rimanere vuoto per il momento. Fare clic su **Commit changes...**.

![Blocca](./images/css2.png)

Fai clic su **Commit changes**.

![Blocca](./images/css3.png)

#### brandconcierge.js

Durante la creazione di un blocco, è consigliabile creare un file per il codice JavaScript correlato al blocco e deve avere lo stesso nome del blocco.

Fare clic su **Aggiungi file** e selezionare **Crea nuovo file**.

![Blocca](./images/js1.png)

Nella casella di testo immettere `brandconcierge.js`. Il file può rimanere vuoto per il momento. Fare clic su **Commit changes...**.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![Blocca](./images/js2.png)

Fai clic su **Commit changes**.

![Blocca](./images/js3.png)

### Crea nuova pagina e collega nuovo blocco personalizzato

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png)

Fare clic sui tre punti **...** nella scheda **Ambienti** e quindi su **Visualizza dettagli**.

![AEMCS](./images/aemcs9.png)

Visualizzerai quindi i dettagli dell’ambiente. Fai clic sull&#39;URL dell&#39;ambiente **Author**.

>[!NOTE]
>
>È possibile che l’ambiente sia ibernato. In questo caso, devi prima riattivare l’ambiente. Nel video seguente trovi le istruzioni per riattivare la funzione.

>[!VIDEO](https://video.tv.adobe.com/v/3478141?quality=12&learn=on)

![AEMCS](./images/aemcs10.png)

Dovresti quindi visualizzare l’ambiente AEM Author. Vai a **Sites**.

![AEMCS](./images/block21.png)

Vai a **CitiSignal**. Fai clic su **Crea** e seleziona **Pagina**.

![AEMCS](./images/block23.png)

Seleziona **Pagina** e fai clic su **Avanti**.

![AEMCS](./images/block24.png)

Immetti i seguenti valori:

- Titolo: **Brand Concierge**
- Nome: **brandconcierge**
- Titolo pagina: **Brand Concierge**

Fai clic su **Crea**.

![AEMCS](./images/block25.png)

Seleziona **Apri**.

![AEMCS](./images/block22.png)

Dovresti vedere questo.

![AEMCS](./images/block26.png)

Fare clic nell&#39;area vuota per selezionare il componente **sezione**. Quindi, fai clic sull&#39;icona più **+** nel menu a destra.

![AEMCS](./images/block27.png)

Dovresti quindi visualizzare il blocco personalizzato nell’elenco dei blocchi disponibili. Fai clic su per selezionarlo.

![AEMCS](./images/block28.png)

Dovresti quindi vedere un blocco vuoto aggiunto a questa pagina. Questo blocco verrà caricato dinamicamente utilizzando le librerie JavaScript che aggiungerai nel passaggio successivo.

Fai clic su **Pubblica**.

![AEMCS](./images/block29.png)

Fai di nuovo clic su **Pubblica**.

![AEMCS](./images/block30.png)

La nuova pagina è ora pubblicata e può essere aggiunta all’intestazione di navigazione nel passaggio successivo.

### Aggiorna file di intestazione di navigazione

Nella panoramica di AEM Sites, vai a **CitiSignal** e seleziona la casella di controllo per il file **Header/nav**. Fai clic su **Modifica**.

![AEMCS](./images/nav0.png)

Seleziona il campo **Testo** nella schermata di anteprima, quindi fai clic sul campo **Testo** sul lato destro della schermata per modificarlo.

![AEMCS](./images/nav0a.png)

Creare una nuova opzione di menu nel menu di navigazione con il testo `Brand Concierge`. Quindi, seleziona il testo **Brand Concierge** e fai clic sull&#39;icona **link**.

![AEMCS](./images/nav1.png)

Immetti questo valore per il campo **Percorso o URL** `/content/CitiSignal/brandconcierge.html` e `Brand Concierge` per il campo **Titolo**. Fai clic su **Salva**.

![AEMCS](./images/nav3.png)

Dovresti avere questo. Fai clic su **Fine**.

![AEMCS](./images/nav4.png)

Dovresti avere questo. Fai clic su **Pubblica**.

![AEMCS](./images/nav4a.png)

Fai di nuovo clic su **Pubblica**.

![AEMCS](./images/nav5.png)

La nuova pagina viene aggiunta al menu.

## 1.4.2.2 Configura il tuo sito Web per mostrare Brand Concierge - GitHub

Dopo aver aggiornato il contenuto utilizzando l’ambiente di authoring di AEM, ora è necessario aggiornare parte del codice nell’archivio GitHub utilizzato per il sito web.

### Librerie JavaScript

Per implementare Brand Concierge sul sito web in esecuzione su AEM CS/EDS sono necessarie le seguenti librerie:

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

Scarica tutti e 3 i file sul desktop.

![Brand Concierge](./images/aem0.png)

Vai al progetto GitHub del tuo sito web AEM CS/EDS. Vai a **script**.

![Brand Concierge](./images/aem1.png)

Fare clic su **Aggiungi file**, quindi selezionare **Carica file**.

![Brand Concierge](./images/aem3.png)

Fai clic su **Scegli i file**.

![Brand Concierge](./images/aem3a.png)

Seleziona tutti e 3 i file **styleConfigurations.js, alloy.js e brandconciergemain.js** dal desktop e fai clic su **Apri**.

![Brand Concierge](./images/aem4.png)

Fai clic su **Commit changes**.

![Brand Concierge](./images/aem5.png)

### Aggiorna head.html

Nel passaggio precedente hai caricato 3 nuove librerie. Queste librerie ora devono essere caricate quando il sito Web viene caricato e il modo per farlo è aggiungere riferimenti a questi file nel file **head.html**.

Inoltre, devi fornire le istruzioni nel file **head.html** per garantire che le librerie siano caricate nell&#39;ordine corretto e in modo corretto.

A tale scopo, vai al progetto GitHub del tuo sito Web AEM CS/EDS facendo clic su **Codice**.

![Brand Concierge](./images/aem6.png)

Scorri verso il basso un po&#39;. Apri il file **head.html**.

![Brand Concierge](./images/aem7.png)

Fai clic sull&#39;icona **matita** per modificare questo file.

![Brand Concierge](./images/aem8.png)

Dovresti vedere questo.

![Brand Concierge](./images/aem9.png)

Scorri verso il basso fino alla riga 43 e incolla quanto segue:

Il codice seguente contiene 2 campi che è necessario aggiornare:

>[!IMPORTANT]
>
>- **datastreamId** è attualmente impostato su &quot;XXXXX&quot; e deve essere sostituito dall&#39;ID dello stream di dati creato nel passaggio precedente.
>- **orgId** deve essere sostituito dall&#39;ID organizzazione IMS dell&#39;istanza Adobe Experience Cloud.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

Fare clic su **Commit change...**.

![Brand Concierge](./images/aem10.png)

Fai clic su **Commit change**.

![Brand Concierge](./images/aem11.png)

Ora hai aggiornato il codice richiesto per caricare le librerie sul tuo sito web.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 Verifica la configurazione

Ora potrai verificare le modifiche sul tuo sito web andando su `main--citisignal-aem-accs--XXX.aem.page` o `main--citisignal-aem-accs--XXX.aem.live`, dopo aver sostituito XXX con l&#39;account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/o `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Potrebbero essere necessari alcuni minuti prima che tutte le risorse vengano visualizzate correttamente, in quanto devono essere pubblicate prima.

Dovresti vedere questo. Fare clic su **Brand Concierge**.

![Brand Concierge](./images/aem13.png)

Dovresti quindi visualizzare questo Brand Concierge dove puoi inserire la richiesta.

![Brand Concierge](./images/aem14.png)

Torna a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
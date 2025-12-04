---
title: Implementare Brand Concierge utilizzando i tag di raccolta dati
description: Implementare Brand Concierge utilizzando i tag di raccolta dati
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3 Implementare Brand Concierge utilizzando i tag di raccolta dati

>[!IMPORTANT]
>
>Questo esercizio è in fase di elaborazione e non è ancora terminato.

## Proprietà Tag raccolta dati

Brand Concierge deve inviare dati a Adobe Experience Platform. A tal fine, è necessario distribuire sul sito Web SDK (o alloy.js).

Per renderlo possibile, ora devi creare una proprietà Tag raccolta dati.

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Apri **Raccolta dati**.

![Brand Concierge](./images/aep101.png)

Fare clic su **Nuova proprietà**.

![Brand Concierge](./images/aep102.png)

Immettere il nome `--aepUserLdap-- - CitiSignal Website + Brand Concierge` e il dominio del sito Web.

Fai clic su **Salva**.

![Brand Concierge](./images/aep103.png)

Cerca la tua proprietà e aprila.

![Brand Concierge](./images/aep104.png)

Vai a **Estensioni** e quindi a **Catalogo**.

![Brand Concierge](./images/aep105.png)

Cercare `web sdk`, quindi fare clic sull&#39;estensione **Adobe Experience Platform Web SDK**. Fare clic su **Installa**.

![Brand Concierge](./images/aep106.png)

Dovresti vedere questo. Devi solo fornire i dettagli per il flusso di dati qui. Per farlo, scorri verso il basso un po&#39;.

![Brand Concierge](./images/aep107.png)

Per tutti e 3 gli ambienti **Produzione**, **Gestione temporanea** e **Sviluppo**, seleziona quanto segue:

- **Sandbox**: `--aepUserLdap-- - bc`
- **Stream di dati**: `--aepUserLdap-- - Brand Concierge`

Fare clic su **Salva**.

![Brand Concierge](./images/aep108.png)

Dovresti vedere questo. Vai a **Regole**.

![Brand Concierge](./images/aep108a.png)

Fai clic su **Crea nuova regola**.

![Brand Concierge](./images/aep109.png)

Immettere il nome: `Homepage`. Quindi fare clic su **+ Aggiungi** in **EVENTI**.

![Brand Concierge](./images/aep110.png)

Selezionare le opzioni seguenti:

- **Estensione**: **Core**
- **Tipo evento**: **Libreria caricata (parte superiore della pagina)**

Fai clic su **Mantieni modifiche**.

![Brand Concierge](./images/aep111.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi** in **CONDIZIONI**.

![Brand Concierge](./images/aep112.png)

Selezionare le opzioni seguenti:

- **Tipo di logica**: **Normale**
- **Estensione**: **Core**
- **Tipo Di Condizione**: **Percorso Senza Stringa Di Query**
- **percorso uguale a ...**: immetti il dominio del tuo sito Web, in questo caso `https://vangeluw.adobedemosystem.com/`

Fai clic su **Mantieni modifiche**.

![Brand Concierge](./images/aep113.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi** in **AZIONI**.

![Brand Concierge](./images/aep114.png)

Selezionare le opzioni seguenti:

- **Estensione**: **Core**
- **Tipo Azione**: **Codice Personalizzato**
- **Lingua**: **JavaScript**

Fai clic su **Apri editor**.

![Brand Concierge](./images/aep115.png)

Incolla il seguente codice:

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

Fai clic su **Salva**.

![Brand Concierge](./images/aep116.png)

Dovresti vedere questo. Fai clic su **Mantieni modifiche**.

![Brand Concierge](./images/aep117.png)

Dovresti vedere questo. Fai clic su **Salva**.

![Brand Concierge](./images/aep118.png)

Vai a **Flusso di pubblicazione**. Fare clic su **Aggiungi libreria**.

![Brand Concierge](./images/aep119.png)

Immetti il nome: `Dev`, seleziona **Sviluppo (sviluppo)** per l&#39;ambiente, quindi fai clic su **Aggiungi tutte le risorse modificate**.

Fai clic su **Salva e genera per sviluppo**.

![Brand Concierge](./images/aep120.png)

Dopo un paio di minuti la libreria verrà costruita. Attendi di vedere il **punto verde** accanto a **Dev**. Quindi, vai a **Ambienti**.

![Brand Concierge](./images/aep121.png)

Fare clic sull&#39;icona **Installa** per l&#39;ambiente **Sviluppo**.

![Brand Concierge](./images/aep122.png)

Dovresti vedere questo. Fai clic sul pulsante **copia** per copiare il percorso della libreria. Dovrai implementarlo sul tuo sito web.

Il percorso della libreria deve essere simile al seguente:
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

Torna a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
---
title: Guida introduttiva agli agenti AEM
description: Guida introduttiva agli agenti AEM
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: c7108c2818ee7fad820af33b99f277181bcf6a02
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 1%

---

# 1.6.1 Guida introduttiva agli agenti AEM

>[!IMPORTANT]
>
>Per completare questo esercizio, devi avere accesso a un ambiente AEM Sites e Assets CS funzionante con EDS e i vari agenti AEM devono essere abilitati per l’organizzazione IMS in uso.
>
>Se non si dispone ancora di un ambiente di questo tipo, passare all&#39;esercizio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Sites e Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.6.1.1 agente di individuazione

Adobe Experience Manager (AEM) Discovery Agent è uno strumento basato sull’intelligenza artificiale all’interno di AEM as a Cloud Service che consente agli utenti di trovare, recuperare e utilizzare i contenuti, inclusi Assets, Frammenti di contenuto e Adaptive Forms, utilizzando prompt in linguaggio naturale. Elimina la necessità di filtri manuali, complessi o basati su clic comprendendo le finalità e eseguendo ricerche nell’archivio.

Per utilizzare l&#39;**agente di individuazione**, è necessario creare prima alcuni tag in Adobe Experience Manager e quindi assegnare i tag ad alcune risorse utilizzando tali tag. Al termine, potrai utilizzare l’Assistente AI per individuare le risorse in modo semplice e intuitivo.

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`.

### Creare e utilizzare i tag con Assets

Fare clic per aprire il programma Cloud Manager, che dovrebbe essere denominato `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![Agenti AEM](./images/aemagents1.png)

Fai clic sull’URL dell’ambiente per aprirlo.

![Agenti AEM](./images/aemagents2.png)

Fai clic sull&#39;icona **martello**.

![Agenti AEM](./images/aemagents3.png)

In **Generale**, fare clic su **Assegnazione tag**.

![Agenti AEM](./images/aemagents4.png)

Dovresti vedere questo. Fai clic su **Crea**, quindi seleziona **Crea spazio dei nomi**.

![Agenti AEM](./images/aemagents5.png)

Nel campo **Titolo**, immetti: `CitiSignal`. Fai clic su **Crea**.

![Agenti AEM](./images/aemagents6.png)

Espandere lo spazio dei nomi **CitiSignal** facendo clic su di esso. Fai clic su **Crea**, quindi seleziona **Crea tag**.

![Agenti AEM](./images/aemagents7.png)

Nel campo **Titolo**, immetti: `Campaign`. Fai clic su **Invia**.

![Agenti AEM](./images/aemagents8.png)

Selezionare il tag **Campaign** facendo clic su di esso. Fai clic su **Crea**, quindi seleziona **Crea tag**.

![Agenti AEM](./images/aemagents9.png)

Nel campo **Titolo**, immetti: `Winter 2026`. Fai clic su **Invia**.

![Agenti AEM](./images/aemagents10.png)

Selezionare il tag **Campaign** facendo clic su di esso. Fai clic su **Crea**, quindi seleziona **Crea tag**.

![Agenti AEM](./images/aemagents11.png)

Nel campo **Titolo**, immetti: `Spring 2026`. Fai clic su **Invia**.

![Agenti AEM](./images/aemagents12.png)

Ora dovresti avere questo.

![Agenti AEM](./images/aemagents13.png)

Fare clic su **Adobe Experience Manager** e quindi su **Assets**.

![Agenti AEM](./images/aemagents14.png)

Fare clic su **File**.

![Agenti AEM](./images/aemagents15.png)

Fare doppio clic sulla cartella **CitiSignal** per aprirla.

![Agenti AEM](./images/aemagents16.png)

Fai clic su **Crea**, quindi seleziona **File**.

![Agenti AEM](./images/aemagents17.png)

Scarica il file [citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip) e decomprimi sul desktop.

![Agenti AEM](./images/aemagents17a.png)

Seleziona. i 3 file appena scaricati e fare clic su **apri**.

![Agenti AEM](./images/aemagents18.png)

Fai clic su **Carica**.

![Agenti AEM](./images/aemagents19.png)

Dovresti vedere questo.

![Agenti AEM](./images/aemagents20.png)

Selezionare la prima immagine e quindi fare clic su **Proprietà**.

![Agenti AEM](./images/aemagents21.png)

Fai clic sull&#39;icona **cartella** in Tag.

![Agenti AEM](./images/aemagents22.png)

Seleziona il tag **Spring 2026** e fai clic su **Select**. Ripetere il processo per queste immagini:

- citisignal_lion.png
- citisignal_leopard.png
- citisignal_gorilla.png
- citisignal_rabbit.png

![Agenti AEM](./images/aemagents23.png)

Dopo aver selezionato il tag per tutte le immagini, passa a **Experience Manager Assets**.

![Agenti AEM](./images/aemagents24.png)

Seleziona l’archivio in uso.

![Agenti AEM](./images/aemagents25.png)

Vai a **Assets** e apri la cartella **CitiSignal**.

![Agenti AEM](./images/aemagents26.png)

Aprire la prima immagine.

![Agenti AEM](./images/aemagents27.png)

Seleziona **Approvato**, quindi fai clic su **Salva**.

![Agenti AEM](./images/aemagents28.png)

In **Tag** puoi visualizzare il tag selezionato in precedenza.

![Agenti AEM](./images/aemagents29.png)

Ripetere il processo in modo che le 4 immagini vengano approvate.

![Agenti AEM](./images/aemagents30.png)

Quindi, vai a **La mia area di lavoro** e fai clic per aprire **Assistente IA**.

![Agenti AEM](./images/aemagents31.png)

Immetti il seguente prompt e fai clic su **Invia**.

```javascript
find all assets tagged with 'Spring 2026'
```

![Agenti AEM](./images/aemagents32.png)

Se hai accesso a più ambienti AEM Assets CS, vedrai qualcosa di simile a questo. Fare clic sulla risposta proposta per l&#39;ambiente che si desidera utilizzare e quindi fare clic su **Invia**.

![Agenti AEM](./images/aemagents34.png)

Dovresti vedere una risposta simile. Fai clic sull’icona per espandere l’Assistente AI a schermo intero.

![Agenti AEM](./images/aemagents35.png)

Rivedi le risposte.

![Agenti AEM](./images/aemagents36.png)

Dall’interno della finestra dell’Assistente AI, puoi fare clic su per visualizzare queste risorse.

![Agenti AEM](./images/aemagents37.png)

Verrai quindi portato direttamente in AEM Assets CS, all’immagine specifica.

![Agenti AEM](./images/aemagents38.png)

Puoi quindi esaminare anche gli altri metadati disponibili.

![Agenti AEM](./images/aemagents39.png)

## 1.6.1.2 agente di produzione esperienza

### Aggiornamento contenuti - Assets

L’abilità Aggiornamento contenuto aggiorna facilmente i contenuti esistenti, inclusi frammenti di contenuto, pagine, moduli e risorse. L’agente può eseguire azioni quali l’aggiornamento, la rimozione, la sostituzione o l’aggiunta di elementi di contenuto per mantenere le esperienze accurate e correnti. Gli input possono essere descrizioni in linguaggio naturale e, se utilizzati con Jira PDF e screenshot, possono fornire anche input.

Torna alla schermata dell’Assistente AI.

![Agenti AEM](./images/aemagents40.png)

Immetti il seguente prompt e fai clic su **Invia**.

`Generate multiple social media formats (Instagram 1080x1920, Facebook 1200x630, Twitter 1200x675) for the third image`

![Agenti AEM](./images/aemagents40a.png)

Dopo un paio di minuti, dovrebbe verificarsi una risposta simile.

![Agenti AEM](./images/aemagents41.png)

Rivedi le immagini generate.

![Agenti AEM](./images/aemagents42.png)

### Aggiornamento contenuti - Pagine

Torna all&#39;ambiente Adobe Experience Manager Author e passa a **Sites**.

![Agenti AEM](./images/aemagents43.png)

Vai a **CitiSignal**. Fai clic su **Crea** e seleziona **Pagina**.

![Agenti AEM](./images/aemagents44.png)

Seleziona **Pagina** e fai clic su **Avanti**.

![Agenti AEM](./images/aemagents45.png)

Immetti i seguenti valori:

- Titolo: **Fibra max**
- Nome: **fibre-max**
- Titolo pagina: **Fibra max**

Fai clic su **Crea**.

![Agenti AEM](./images/aemagents46.png)

Seleziona **Apri**.

![Agenti AEM](./images/aemagents47.png)

Dovresti vedere questo.

![Agenti AEM](./images/aemagents48.png)

Fare clic nell&#39;area vuota per selezionare il componente **sezione**. Fai clic sull&#39;icona più **+** nel menu a destra e seleziona **Eroe**.

![Agenti AEM](./images/aemagents49.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi** per aggiungere un&#39;immagine.

![Agenti AEM](./images/aemagents50.png)

Seleziona l’archivio delle risorse. Aprire quindi la cartella **CitiSignal**.

![Agenti AEM](./images/aemagents51.png)

Scegli l&#39;immagine del leone caricata in precedenza. Fai clic su **Seleziona**.

![Agenti AEM](./images/aemagents52.png)

Dovresti vedere questo. Fare clic sull&#39;area **testo** per modificare il testo.

![Agenti AEM](./images/aemagents53.png)

Incolla questo testo nelle:

```
This winter, be as fast as a lion.
```

Selezionare **Intestazione 1**, quindi fare clic su **Fine**.

![Agenti AEM](./images/aemagents54.png)

Dovresti vedere questo. Vai a **Struttura contenuto** e seleziona l&#39;area **Sezione**.

![Agenti AEM](./images/aemagents55.png)

Fai clic sull&#39;icona **+**, quindi seleziona **Schede**.

![Agenti AEM](./images/aemagents56.png)

Dovresti vedere questo. Assicurarsi che nella **Struttura contenuto** sia selezionato **Schede**.

Quindi, fare clic sul pulsante **+** 4 volte.

![Agenti AEM](./images/aemagents57.png)

Ora dovresti vedere questo, dove ci sono 4 **oggetti Card** nell&#39;oggetto **Cards**.

![Agenti AEM](./images/aemagents58.png)

Seleziona la prima **scheda**. Fare clic sull&#39;area **testo** per modificare il testo.

![Agenti AEM](./images/aemagents59.png)

Incolla il testo seguente. Verificare che la prima riga di testo utilizzi **Intestazione 1**. Fai clic su **Fine**.

```
99.9% network reliability

Game, video chat and stream on multiple devices with ultra low lag.
```

![Agenti AEM](./images/aemagents60.png)

Selezionare la seconda **scheda**. Fare clic sull&#39;area **testo** per modificare il testo.

![Agenti AEM](./images/aemagents61.png)

Incolla il testo seguente. Verificare che la prima riga di testo utilizzi **Intestazione 1**. Fai clic su **Fine**.

```
3-year

price lock guarantee

For new and existing Fiber Max customers on all internet plans.

No hidden fees.
```

![Agenti AEM](./images/aemagents62.png)

Seleziona la terza **scheda**. Fare clic sull&#39;area **testo** per modificare il testo.

![Agenti AEM](./images/aemagents63.png)

Incolla il testo seguente. Verificare che la prima riga di testo utilizzi **Intestazione 1**. Fai clic su **Fine**.

```
More ways to save

Save over 45% on the best entertainment with CitiSignal
```

![Agenti AEM](./images/aemagents64.png)

Seleziona la quarta **scheda**. Fare clic sull&#39;area **testo** per modificare il testo.

![Agenti AEM](./images/aemagents65.png)

Incolla il testo seguente. Verificare che la prima riga di testo utilizzi **Intestazione 1**. Fai clic su **Fine**.

```
Get Fiber Max now!

Fill out the form here to get started.
```

![Agenti AEM](./images/aemagents66.png)

Ora dovresti avere questo. Fai clic su **Pubblica**.

![Agenti AEM](./images/aemagents67.png)

Fai di nuovo clic su **Pubblica**.

![Agenti AEM](./images/aemagents68.png)

Fai clic su **Apri pagina**.

![Agenti AEM](./images/aemagents69.png)

Copia l’URL della pagina in base alle tue esigenze.

L&#39;URL deve essere simile al seguente: `https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/content/CitiSignal/fiber-max.html`.

![Agenti AEM](./images/aemagents70.png)

Vai a [https://experience.adobe.com/#/experiencemanager/](https://experience.adobe.com/#/experiencemanager/). Fare clic per aprire **Assistente IA**.

![Agenti AEM](./images/aemagents71.png)

Incolla il seguente prompt e fai clic su **invia**. Sostituisci XXX in questo prompt con l’URL copiato nel passaggio precedente.

```
On the page XXX, please make the following changes:

- change the word 'winter' to 'spring'
- change the word 'lion' to 'leopard'
- change the image in the hero block to use the image 'citisignal_leopard.png'
- change the text '99.9% network reliability' to '99.999% network reliability'
```

![Agenti AEM](./images/aemagents72.png)

Dopo 1-2 minuti, dovresti vedere questo. Immettere il prompt `generate` e fare clic su **Invia**.

![Agenti AEM](./images/aemagents74.png)

Un paio di minuti dopo, dovresti vedere una conferma del genere che le modifiche sono state eseguite. Fare clic su **Anteprima della pagina aggiornata**.

![Agenti AEM](./images/aemagents75.png)

Ora ottieni una conferma visiva delle modifiche apportate. Questa pagina di anteprima ha uno scopo puramente informativo, non puoi intervenire da questa pagina.

![Agenti AEM](./images/aemagents76.png)

Per eseguire un&#39;azione, fare clic su **Modifica in AEM**.

![Agenti AEM](./images/aemagents75a.png)

Nell’Editor universale, ora puoi vedere tutte le modifiche in dettaglio, con la possibilità di modificare qualsiasi cosa. Dopo aver esaminato la pagina, fai clic su **Pubblica**.

![Agenti AEM](./images/aemagents77.png)

Fai di nuovo clic su **Pubblica**. La modifica apportata non è ancora stata pubblicata nell&#39;ambiente di produzione. È stato invece pubblicato in **Lanci** in AEM.

I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura. Viene creato un lancio per consentire di apportare modifiche in preparazione alla pubblicazione futura, mantenendo al contempo le pagine correnti. Ciò significa che stai modificando effettivamente due versioni contemporaneamente: pagine attualmente pubblicate e una versione di tali pagine, da pubblicare in futuro. Una volta arrivato questo momento, puoi sostituire le pagine originali e pubblicare la nuova versione.

![Agenti AEM](./images/aemagents78.png)

Per **Promuovere** le modifiche in sospeso per una versione futura, torna ad AEM. Fai clic su **Adobe Experience Manager** nella parte superiore della pagina, fai clic sull&#39;icona **martello**, quindi seleziona **Lanci**.

![Agenti AEM](./images/aemagents79.png)

Ora dovresti vedere un **Launch** in sospeso. Selezionare la casella di controllo davanti al **lancio** in sospeso.

![Agenti AEM](./images/aemagents80.png)

Fai clic su **Promuovi**.

![Agenti AEM](./images/aemagents81.png)

Seleziona **Promuovi lancio completo** e fai clic su **Avanti**.

![Agenti AEM](./images/aemagents82.png)

Fai clic su **Promuovi**.

![Agenti AEM](./images/aemagents83.png)

Ora dovresti vedere questo. Le modifiche sono ora in produzione.

![Agenti AEM](./images/aemagents84.png)

Aggiorna la pagina: tutte le modifiche dovrebbero essere visualizzate nella pagina pubblicata.

![Agenti AEM](./images/aemagents85.png)

In alternativa, invece di eseguire il processo di promozione manuale, è possibile immettere il prompt `accept` nell&#39;Assistente IA.

![Agenti AEM](./images/aemagents86.png)

Dovresti quindi ottenere una conferma della pubblicazione delle modifiche.

![Agenti AEM](./images/aemagents87.png)

### Aggiornamento contenuto - Creazione modulo

Nel modulo [Adobe Experience Manager Forms con Edge Delivery Services](./../../asset-mgmt/module1.3/aemforms.md){target="_blank"} puoi trovare i passaggi necessari per creare un modulo in modo manuale.

L’abilità di Creazione di moduli ora consente agli utenti di creare moduli adattivi attraverso prompt in linguaggio naturale senza dipendere dai team di sviluppo o IT. Questa funzionalità accelera lo sviluppo dei moduli mantenendo al contempo la coerenza del marchio e consentendo agli utenti aziendali di creare moduli senza una profonda conoscenza tecnica dei prodotti.

Vai a [https://experience.adobe.com/#/ai-assistant/chat](https://experience.adobe.com/#/ai-assistant/chat).

![Agenti AEM](./images/aemagentsforms1.png)

Immetti il seguente prompt e fai clic su **invia**.

```
Create a new adaptive form using Edge Delivery Services with the following details:
- Form name: "citisignal-fiber-max-interest-2"
- Form fields: 4 text input fields are needed, for "first-name", "last-name", "email" and "city"
- When the form is submitted, send the submission to a spreadsheet, with this URL: https://docs.google.com/spreadsheets/d/1WwKrcM8mZ2d_W3sMheUAw3nFhP_OFk05TsqxhHkudfQ/edit?usp=sharing.
```



## Passaggi successivi

Torna a [AEM e agenti](./aemagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

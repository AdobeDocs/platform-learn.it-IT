---
title: Content Production Agent
description: Content Production Agent
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 7ea3bdc9557ea9e88ddd9693f9ffbfbc634857f8
workflow-type: tm+mt
source-wordcount: '859'
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

### Aggiornamento contenuti

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

### Creazione modulo

L’abilità di Creazione di moduli consente agli utenti di creare moduli adattivi attraverso prompt in linguaggio naturale senza dipendere dai team di sviluppo o IT. Questa funzionalità accelera lo sviluppo dei moduli mantenendo al contempo la coerenza del marchio e consentendo agli utenti aziendali di creare moduli senza una profonda conoscenza tecnica dei prodotti.


## Passaggi successivi

Torna a [AEM e agenti](./aemagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

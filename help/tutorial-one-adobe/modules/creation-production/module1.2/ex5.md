---
title: I/O frame e Workfront Fusion
description: I/O frame e Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: 7d4970479ff1a7dcb3ebb1f46660f418ba768da3
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# I/O a 1,2,5 frame e Workfront Fusion

Nell&#39;esercizio precedente è stato configurato lo scenario `--aepUserLdap-- - Firefly + Photoshop` e un webhook in ingresso per attivare lo scenario e una risposta del webhook al completamento dello scenario. Hai quindi utilizzato Postman per attivare tale scenario. Postman è un ottimo strumento per i test, ma in uno scenario di business reale, gli utenti aziendali non utilizzerebbero Postman per attivare uno scenario. Al contrario, utilizzerebbero un’altra applicazione e si aspetterebbero che quest’ultima attivi uno scenario in Workfront Fusion. In questo esercizio, questo è esattamente ciò che si farà con Frame I/O.

## 1.2.5.1 accesso I/O frame

>[!NOTE]
>
>Per completare correttamente questo esercizio, devi essere un utente amministratore nel tuo account di I/O Frame. L&#39;esercizio seguente è stato creato per Frame I/O V3 e verrà aggiornato in una fase successiva per Frame I/O V4.

Vai a [https://app.frame.io/projects](https://app.frame.io/projects).

Fai clic sull&#39;icona **+** per creare un progetto personalizzato in I/O Frame.

![I/O fotogrammi](./images/frame1.png)

Immettere il nome `--aepUserLdap--` e fare clic su **Crea progetto**.

![I/O fotogrammi](./images/frame2.png)

Vedrai quindi il tuo progetto nel menu a sinistra.
In uno degli esercizi precedenti avete scaricato [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} sul desktop. Seleziona il file, quindi trascinalo nella cartella del progetto appena creata.

![I/O fotogrammi](./images/frame3.png)

## 1.2.5.2 Workfront Fusion e I/O Frame

Nell&#39;esercizio precedente è stato creato lo scenario `--aepUserLdap-- - Firefly + Photoshop`, che è iniziato con un webhook personalizzato e si è concluso con una risposta del webhook. L’utilizzo dei webhook è stato quindi testato utilizzando Postman, ma ovviamente, il punto di tale scenario è essere chiamato da un’applicazione esterna. Come indicato in precedenza, Frame I/O sarà quell&#39;esercizio, ma tra Frame I/O e `--aepUserLdap-- - Firefly + Photoshop` è necessario un altro scenario Workfront Fusion. ora configurerai quello scenario.

Nel menu a sinistra, vai a **Scenari** e seleziona la tua cartella `--aepUserLdap--`. Fare clic Crea **un nuovo scenario**.

![I/O fotogrammi](./images/frame4.png)

Utilizzare il nome `--aepUserLdap-- - Frame IO Custom Action`.

![I/O fotogrammi](./images/frame5.png)

Fare clic sull&#39;**oggetto punto interrogativo** nell&#39;area di lavoro. Immettere il testo `webhook` nella casella di ricerca e fare clic su **Webhook**.

![I/O fotogrammi](./images/frame6.png)

Fai clic su **WebHook personalizzato**.

![I/O fotogrammi](./images/frame7.png)

Fai clic su **Aggiungi** per creare un nuovo URL del webhook.

![I/O fotogrammi](./images/frame8.png)

Per il **nome webhook**, utilizzare `--aepUserLdap-- - Frame IO Custom Action Webhook`. Fai clic su **Salva**.

![I/O fotogrammi](./images/frame9.png)

Dovresti vedere questo. Lascia aperta e inalterata questa schermata come ti servirà in un passaggio successivo. Sarà necessario copiare il URL webhook in un passaggio successivo, facendo clic su **Copia indirizzo in Appunti**.

![I/O fotogrammi](./images/frame10.png)

Vai a [https://developer.frame.io/](https://developer.frame.io/). Fai clic su **STRUMENTI PER SVILUPPATORI**, quindi scegli **Azioni personalizzate**.

![I/O fotogrammi](./images/frame11.png)

Fare clic su **Crea azione personalizzata**.

![I/O fotogrammi](./images/frame12.png)

Immettere i seguenti valori:

- **NOME**: utilizzo `vangeluw - Frame IO Custom Action Fusion`
- **DESCRIZIONE**: utilizzo `vangeluw - Frame IO Custom Action Fusion`
- **EVENTO:** utilizzare `fusion.tutorial`.
- **URL**: immettere il URL del webhook appena creato in Workfront Fusion
- **TEAM**: selezionare il team di I/O Frame appropriato, in questo caso **One Adobe Tutorial**.

Fai clic su **Invia**.

![I/O fotogrammi](./images/frame15.png)

Dovresti vedere questo.

![I/O fotogrammi](./images/frame14.png)

Torna a [https://app.frame.io/projects](https://app.frame.io/projects). Aggiorna pagina.

![I/O fotogrammi](./images/frame16.png)

Dopo aver aggiornato la pagina, fai clic sui tre punti **...** della risorsa **citisignal-fiber.psd**. Dovresti quindi visualizzare l’azione personalizzata creata in precedenza nel menu visualizzato. Fare clic sull&#39;azione personalizzata `vangeluw - Frame IO Custom Action Fusion`.

![I/O fotogrammi](./images/frame17.png)

Dovresti quindi vedere un **esito positivo simile.Popup**. Questo popup è il risultato della comunicazione tra Frame I/O e Workfront Fusion.

![I/O fotogrammi](./images/frame18.png)

Ripristinare lo schermo su Workfront Fusion. Ora vedrai **apparire Determinato** correttamente sull&#39;oggetto Webhook personalizzato. Fai clic su **OK**.

![I/O fotogrammi](./images/frame19.png)

Fare clic su **Esegui una volta** per attivare la modalità di test e verificare di nuovo la comunicazione con Frame I/O.

![I/O fotogrammi](./images/frame20.png)

Tornare a I/O frame e fare di nuovo clic sull&#39;azione personalizzata `vangeluw - Frame IO Custom Action Fusion`.

![I/O fotogrammi](./images/frame21.png)

Riportare lo schermo a Workfront Fusion. A questo punto dovrebbe essere visualizzato un segno di spunta verde e una bolla che mostra **1**. Fai clic sulla bolla per visualizzare i dettagli.

![I/O fotogrammi](./images/frame22.png)

La vista dettagliata della bolla mostra i dati ricevuti dal Frame I/O. Dovresti visualizzare diversi ID. Ad esempio, il campo **resource.id** mostra l&#39;ID univoco in I/O frame della risorsa **citisignal-fiber.psd**

![I/O fotogrammi](./images/frame23.png)

Ora che è stata stabilita la comunicazione tra Frame I/O e Workfront Fusion, è possibile continuare la configurazione.

## 1.2.5.3 Fornitura di una risposta del modulo personalizzato all&#39;I/O del frame.



## Passaggi successivi

Vai a [1.2.6 Frame I/O a Fusion a AEM Assets](./ex6.md){target="_blank"}

Torna a [Automazione dei flussi di lavoro Creative con Workfront Fusion](./automation.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}


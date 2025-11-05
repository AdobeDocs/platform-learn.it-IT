---
title: Automazione tramite connettori
description: Automazione tramite connettori
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 0b20ba91-28d4-4f4d-8abe-074f802c389e
source-git-commit: 843140d3befd415a1879410f34c2b60c6adf18d0
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 1%

---

# 1.2.4 Automazione tramite connettori

Ora inizierai a utilizzare i connettori predefiniti di Workfront Fusion per Photoshop e connetterai la richiesta Firefly Text-2-Image e le richieste Photoshop in un unico scenario.

## 1.2.4.1 Aggiorna variabili

Prima di continuare con la configurazione del connettore, è necessario aggiungere le seguenti variabili al modulo **Initialize Constants**.

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Torna al primo nodo, seleziona **Inizializza costanti**, quindi scegli **Aggiungi elemento** per ciascuna di queste variabili.

![WF Fusion](./images/wffusion69.png)

| Chiave | Esempio di valore |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Puoi trovare le variabili tornando a Postman e aprendo **Variabili di ambiente**.

![Archiviazione Azure](./../module1.1/images/az105.png)

Copiate questi valori in Workfront Fusion e aggiungete un nuovo elemento per ciascuna di queste 4 variabili.

Lo schermo dovrebbe essere simile al seguente. Selezionare **OK**.

![WF Fusion](./images/wffusion68.png)

## 1.2.4.2 Attiva lo scenario utilizzando un webhook

Finora lo scenario è stato eseguito manualmente per essere testato. Aggiorniamo ora lo scenario con un webhook, in modo che possa essere attivato da un ambiente esterno.

Seleziona **+**, cerca **webhook**, quindi seleziona **Webhook**.

![WF Fusion](./images/wffusion216.png)

Seleziona **WebHook personalizzato**.

![WF Fusion](./images/wffusion217.png)

Trascina il modulo **Webhook personalizzato** all&#39;inizio dello scenario. Quindi, seleziona l&#39;icona **orologio** e trascinala nel modulo **Webhook personalizzato**.

![WF Fusion](./images/wffusion217a.png)

Dovresti vedere questo. Quindi, trascina il punto rosso del primo modulo verso il punto viola del secondo modulo.

![WF Fusion](./images/wffusion217b.png)

Dovresti vedere questo. Newt, fai clic sul modulo **Webhook personalizzato**.

![WF Fusion](./images/wffusion217c.png)

Fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion218.png)

Imposta **Nome webhook** su `--aepUserLdap-- - Firefly + Photoshop Webhook`. Fai clic su **Salva**.

![WF Fusion](./images/wffusion219.png)

L’URL del webhook è ora disponibile. Fai clic su **Copia indirizzo negli Appunti** per copiare l&#39;URL.

![WF Fusion](./images/wffusion221.png)

Apri Postman e aggiungi una nuova cartella nella raccolta **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Denomina la cartella `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Nella cartella appena creata, seleziona i tre punti **...** e seleziona **Aggiungi richiesta**.

![WF Fusion](./images/wffusion224.png)

Imposta il **tipo di metodo** su **POST** e incolla l&#39;URL del webhook nella barra degli indirizzi.

![WF Fusion](./images/wffusion225.png)

È necessario inviare un corpo personalizzato, in modo che gli elementi della variabile possano essere forniti da un’origine esterna allo scenario Workfront Fusion.

Vai a **Body** e seleziona **raw**.

![WF Fusion](./images/wffusion226.png)

Incolla il testo seguente nel corpo della richiesta. Seleziona **Invia**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

![WF Fusion](./images/wffusion229.png)

In Workfront Fusion, sul webhook personalizzato viene visualizzato un messaggio con il seguente messaggio: **Determinato correttamente**.

![WF Fusion](./images/wffusion227.png)

## Connettore Adobe Firefly 1.2.4.3

Fai clic sull&#39;icona **+** per aggiungere un nuovo modulo.

![WF Fusion](./images/wffcff2.png)

Immettere il termine di ricerca `Adobe Firefly` e selezionare **Adobe Firefly**.

![WF Fusion](./images/wffcff2a.png)

Seleziona **Genera un&#39;immagine**.

![WF Fusion](./images/wffcff3.png)

Fai clic sul modulo **Adobe Firefly** per aprirlo, quindi fai clic su **Aggiungi** per creare una nuova connessione.

![WF Fusion](./images/wffcff5.png)

Compila i campi seguenti:

- **Nome connessione**: utilizzare `--aepUserLdap-- - Firefly connection`.
- **Ambiente**: utilizzare **Produzione**.
- **Tipo**: usa **Account personale**.
- **ID client**: copia **ID client** dal progetto Adobe I/O denominato `--aepUserLdap-- - One Adobe tutorial`.
- **Segreto client**: copia **Segreto client** dal progetto Adobe I/O denominato `--aepUserLdap-- - One Adobe tutorial`.

Puoi trovare **ID client** e **Segreto client** del progetto Adobe I/O [qui](https://developer.adobe.com/console/projects.){target="_blank"}.

![WF Fusion](./images/wffc20.png)

Dopo aver compilato tutti i campi, fai clic su **Continua**. La connessione verrà quindi convalidata automaticamente.

![WF Fusion](./images/wffcff6.png)

Selezionare quindi la variabile **prompt** fornita allo scenario dal **webhook personalizzato** in ingresso.

![WF Fusion](./images/wffcff7.png)

Impostare **Model version** **prompt** su **image4 standard**. Fai clic su **OK**.

![WF Fusion](./images/wffcff7b.png)

Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per verificare la configurazione.

![WF Fusion](./images/wffcff8.png)

Vai a Postman, verifica la richiesta nella richiesta, quindi fai clic su **Invia**.

![WF Fusion](./images/wffcff8a.png)

Dopo aver fatto clic su Invia, torna a Workfront Fusion e fai clic sull&#39;icona a forma di bolla nel modulo **Adobe Firefly** per verificare i dettagli.

![WF Fusion](./images/wffcff9.png)

Vai in **OUTPUT** a **Dettagli** > **url** per trovare l&#39;URL dell&#39;immagine generata da **Adobe Firefly**.

![WF Fusion](./images/wffcff10.png)

Copia l’URL e trasmettilo nel browser. Ora dovresti vedere un&#39;immagine che rappresenta il prompt inviato dalla richiesta di Postman, in questo caso **prati nebbiosi**.

![WF Fusion](./images/wffcff11.png)

## 1.2.4.2 Cambia lo sfondo del file PSD

Ora aggiornerai lo scenario per renderlo più intelligente utilizzando più connettori preconfigurati. Collegherai inoltre l’output da Firefly a Photoshop, in modo che l’immagine di sfondo del file PSD cambi dinamicamente utilizzando l’output dell’azione Genera immagine di Firefly.

Dovresti vedere questo. Passa il puntatore del mouse sul modulo **Adobe Firefly** e fai clic sull&#39;icona **+**.

![WF Fusion](./images/wffc15.png)

Nel menu Cerca, immetti `Photoshop` e quindi fai clic sull&#39;azione **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Selezionare **Applica modifiche PSD**.

![WF Fusion](./images/wffc17.png)

Dovresti vedere questo. Fai clic su **Aggiungi** per aggiungere una nuova connessione ad Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configura la connessione come segue:

- Tipo di connessione: selezionare **Adobe Photoshop (server-to-server)**
- Nome connessione: immetti `--aepUserLdap-- - Adobe I/O`
- ID client: incolla l’ID client
- Segreto client: incolla il segreto client

Fai clic su **Continua**.

![WF Fusion](./images/wffc19.png)

Per trovare il **ID client** e il **Segreto client**, vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"} e apri il progetto Adobe I/O, denominato `--aepUserLdap-- One Adobe tutorial`. Vai a **OAuth Server-to-Server** per trovare l&#39;ID client e il segreto client. Copiare tali valori e incollarli nella configurazione della connessione in Workfront Fusion.

![WF Fusion](./images/wffc20.png)

Dopo aver fatto clic su **Continua**, verrà visualizzata brevemente una finestra popup durante la verifica delle credenziali. Una volta fatto, dovresti vedere questo.

![WF Fusion](./images/wffc21.png)

È ora necessario immettere la posizione del file PSD con cui si desidera utilizzare Fusion. Per **Archiviazione**, selezionare **Azure** e per **Percorso file**, immettere `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`. Posizionare il cursore accanto al secondo `/`. Quindi, controlla le variabili disponibili e scorri verso il basso per trovare la variabile **psdTemplate**. Fai clic sulla variabile **psdTemplate** per selezionarla.

![WF Fusion](./images/wffc22.png)

Dovresti vedere questo.

![WF Fusion](./images/wffc23.png)

Scorri fino in fondo fino a visualizzare **Livelli**. Fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffc24.png)

Dovresti vedere questo. Ora devi immettere il nome del livello nel modello Photoshop PSD utilizzato come sfondo del file.

![WF Fusion](./images/wffc25.png)

Nel file **citisignal-fiber.psd**, troverai il livello utilizzato per lo sfondo. In questo esempio, il livello è denominato **2048x2048-background**.

![WF Fusion](./images/wffc26.png)

Incolla il nome **2048x2048-background** nella finestra di dialogo di Workfront Fusion.

![WF Fusion](./images/wffc27.png)

Scorri verso il basso fino a visualizzare **Input**. Ora è necessario definire cosa deve essere inserito nel livello di sfondo. In questo caso, è necessario selezionare l&#39;output del modulo **Adobe Firefly**, che contiene l&#39;immagine generata dinamicamente.

Per **Archiviazione**, selezionare **Esterna**. Per **Percorso file**, è necessario copiare e incollare la variabile `{{XX.details[].url}}` dall&#39;output del modulo **Adobe Firefly**, ma è necessario sostituire **XX** nella variabile con il numero di sequenza del modulo **Adobe Firefly**, che in questo esempio è **5**.

![WF Fusion](./images/wffc28.png)

Quindi scorri verso il basso fino a visualizzare **Modifica**. Imposta **Modifica** su **Sì** e **Tipo** su **Livello**. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffc29.png)

Dovresti vedere questo. Successivamente, devi definire l’output dell’azione. Fai clic su **Aggiungi elemento** in **output**.

![WF Fusion](./images/wffc30.png)

Seleziona **Azure** per **Archiviazione**, incolla `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}` in **Posizione file** e seleziona **vnd.adobe.photoshop** in **Tipo**. Fare clic per abilitare **Mostra impostazioni avanzate**.

![WF Fusion](./images/wffc31.png)

In **Impostazioni avanzate**, selezionare **Sì** per sovrascrivere i file con lo stesso nome.
Fai clic su **Aggiungi**.

![WF Fusion](./images/wffc32.png)

Dovresti avere questo. Fai clic su **OK**.

![WF Fusion](./images/wffc33.png)

Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per verificare la configurazione.

![WF Fusion](./images/wffc33a.png)

Vai a Postman, verifica la richiesta nella richiesta, quindi fai clic su **Invia**.

![WF Fusion](./images/wffcff8a.png)

Dovresti vedere questo. Fai clic sul fumetto nel modulo **Adobe Photoshop - Applica modifiche PSD**.

![WF Fusion](./images/wffc33b.png)

È ora possibile vedere che un nuovo file PSD è stato generato correttamente e archiviato nell&#39;account di archiviazione di Microsoft Azure.

![WF Fusion](./images/wffc33c.png)

## 1.2.4.3 Modificare i livelli di testo del file PSD

Passa il puntatore del mouse sul modulo **Adobe Photoshop - Applica modifiche PSD** e fai clic sull&#39;icona **+**.

![WF Fusion](./images/wffc34.png)

Seleziona **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Selezionare **Modifica livelli di testo**.

![WF Fusion](./images/wffc36.png)

Dovresti vedere questo. Selezionare innanzitutto la connessione Adobe Photoshop già configurata in precedenza, che deve essere denominata `--aepUserLdap-- Adobe I/O`.

![WF Fusion](./images/wffc37.png)

Per il **file di input**, selezionare **Azure** per **Archiviazione file di input** e assicurarsi di selezionare l&#39;output della richiesta precedente, **Adobe Photoshop - Applica modifiche PSD**, che è possibile definire come segue: ``{{XX.data[].`_links`.renditions[].href}}`` (sostituire XX con il numero di sequenza del modulo precedente Adobe Photoshop - Applica modifiche PSD).

Fare clic su **+Aggiungi elemento** in **Livelli** per iniziare ad aggiungere i livelli di testo da aggiornare.

![WF Fusion](./images/wffc37a.png)

È necessario apportare due modifiche. È necessario aggiornare il testo di CTA e il testo del pulsante nel file **citisignal-fiber.psd**.

Per trovare i nomi dei livelli, apri il file **citisignal-fiber.psd**. Nel file, noterai che il livello contenente il call to action è denominato **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

Nel file **citisignal-fiber.psd**, noterai inoltre che il livello contenente il call to action è denominato **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Devi innanzitutto configurare le modifiche da apportare al livello **2048x2048-cta**. Immetti il nome **2048x2048-cta** in **Nome** nella finestra di dialogo.

![WF Fusion](./images/wffc39.png)

Scorri verso il basso fino a visualizzare **Testo** > **Contenuto**. Selezionare la variabile **cta** dal payload del webhook. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffc40.png)

Dovresti vedere questo. Fai clic su **+Aggiungi elemento** in **Livelli** per iniziare ad aggiungere il livello di testo successivo da aggiornare.

![WF Fusion](./images/wffc40a.png)

Immetti il nome **2048x2048-button-text** in **Name** nella finestra di dialogo.

![WF Fusion](./images/wffc40b.png)

Scorri verso il basso fino a visualizzare **Testo** > **Contenuto**. Seleziona la variabile **button** dal payload del webhook. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffc40c.png)

Dovresti vedere questo.

![WF Fusion](./images/wffc40d.png)

Scorri verso il basso fino a visualizzare **Output**. Per **Archiviazione**, selezionare **Azure**. Per **Percorso file**, immettere il percorso seguente. Si noti l&#39;aggiunta della variabile `{{timestamp}}` al nome file utilizzata per garantire che ogni file generato abbia un nome univoco. Impostare inoltre **Type** su **vnd.adobe.photoshop**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

Imposta **Type** su **vnd.adobe.photoshop**. Fai clic su **OK**.

![WF Fusion](./images/wffc41.png)

Fai clic su **Salva** per salvare le modifiche.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 risposta webhook

Dopo aver applicato queste modifiche al tuo file Photoshop, ora devi configurare una **risposta webhook** che verrà rimandata a qualsiasi applicazione abbia attivato questo scenario.

Passa il puntatore del mouse sul modulo **Adobe Photoshop - Modifica livelli di testo** e fai clic sull&#39;icona **+**.

![WF Fusion](./images/wffc48.png)

Cerca `webhooks` e seleziona **Webhook**.

![WF Fusion](./images/wffc49.png)

Seleziona **Risposta webhook**.

![WF Fusion](./images/wffc50.png)

Dovresti vedere questo. Incolla il payload seguente in **Body**.

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

Copiare e incollare la variabile `{{XX.data[]._links.renditions[].href}}` e sostituire **XX** con il numero di sequenza dell&#39;ultimo modulo **Adobe Photoshop - Modifica livelli di testo**, che in questo caso è **7**.

![WF Fusion](./images/wffc52.png)

Abilitare la casella di controllo per **Mostra impostazioni avanzate**, quindi fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffc52b.png)

Nel campo **Chiave** immettere `Content-Type`. Nel campo **Valore** immettere `application/json`. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffc52a.png)

Dovresti avere questo. Fai clic su **OK**.

![WF Fusion](./images/wffc53.png)

Fare clic su **Allineamento automatico**.

![WF Fusion](./images/wffc54.png)

Dovresti vedere questo. Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per verificare lo scenario.

![WF Fusion](./images/wffc55.png)

Torna a Postman e fai clic su **Invia**. Il prompt utilizzato è **nebbiosi prati**.

![WF Fusion](./images/wffc56.png)

Lo scenario verrà quindi attivato e, dopo un certo periodo di tempo, in Postman verrà visualizzata una risposta contenente l’URL del file PSD appena creato.

![WF Fusion](./images/wffc58.png)

Come promemoria: una volta che lo scenario è stato eseguito in Workfront Fusion, potrai visualizzare le informazioni su ciascun modulo facendo clic sulla bolla sopra ogni modulo.

![WF Fusion](./images/wffc59.png)

Utilizzando Azure Storage Explorer, è quindi possibile trovare e aprire il file PSD appena creato facendo doppio clic su di esso in Azure Storage Explorer.

![WF Fusion](./images/wffc60.png)

Il file dovrebbe quindi essere simile al seguente, con lo sfondo sostituito da uno sfondo con **prati nebbiosi**.

![WF Fusion](./images/wffc61.png)

Se esegui nuovamente lo scenario e invii una nuova richiesta da Postman utilizzando un prompt diverso, vedrai quanto lo scenario è diventato semplice e riutilizzabile. In questo esempio, il nuovo prompt utilizzato è **deserto soleggiato**.

![WF Fusion](./images/wffc62.png)

E un paio di minuti dopo, è stato generato un nuovo file PSD con un nuovo sfondo.

![WF Fusion](./images/wffc63.png)

## Passaggi successivi

Vai a [1.2.5 Frame.io e Workfront Fusion](./ex5.md){target="_blank"}

Torna a [Automazione dei flussi di lavoro Creative con Workfront Fusion](./automation.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}

---
title: Frame I/O su Workfront Fusion su AEM Assets
description: Frame I/O su Workfront Fusion su AEM Assets
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: f02ecbe4-f1d7-4907-9bbc-04e037546091
source-git-commit: 1d1ee3462bd890556037c8e24ba2fe94c3423187
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# I/O da 1.2.6 Frame a Workfront Fusion a AEM Assets

>[!IMPORTANT]
>
>Per completare questo esercizio, è necessario avere accesso a un ambiente AEM Assets CS Author funzionante. Se segui l&#39;esercizio [Adobe Experience Manager Cloud Service e Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"} potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM Assets CS con un ambiente di authoring, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare il processo di disattivazione ora in modo da non rimanere bloccati in un secondo momento.

Nell’esercizio precedente hai configurato uno scenario che genera automaticamente varianti di un file PSD di Adobe Photoshop utilizzando Adobe Firefly, le API di Photoshop e Workfront Fusion. L’output di tale scenario era un nuovo file PSD di Photoshop.

I team aziendali, tuttavia, non hanno bisogno di un file PSD, ma di un file PNG o di un file JPG. In questo esercizio configurerai una nuova automazione che determinerà la generazione di un file PNG dopo l’approvazione della risorsa in Frame I/O e che memorizzerà automaticamente tale file PNG in AEM Assets.

## 1.2.6.1 Crea un nuovo scenario

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Aprire **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Nel menu a sinistra, vai a **Scenari** e seleziona la cartella `--aepUserLdap--`. Fai clic su **Crea un nuovo scenario**.

![I/O fotogrammi](./images/aemf1.png)

Utilizza il nome `--aepUserLdap-- - Asset Approved PNG AEM Assets`. Fare clic su **?Modulo**, immetti il termine di ricerca `webhook` e fai clic su **Webhook**.

![I/O fotogrammi](./images/aemf2.png)

Fai clic su **WebHook personalizzato**.

![I/O fotogrammi](./images/aemf3.png)

Fai clic su **Aggiungi** per creare un nuovo webhook.

![I/O fotogrammi](./images/aemf4.png)

Utilizza il nome `--aepUserLdap-- - Frame.io Webhook`. Fai clic su **Salva**.

![I/O fotogrammi](./images/aemf5.png)

Dovresti vedere questo. Fare clic su **Copia indirizzo negli Appunti**.

![I/O fotogrammi](./images/aemf6.png)

## 1.2.6.2 Configurare il webhook in Frame.io

Vai a Postman e apri la richiesta **POST - Ottieni token di accesso** nella raccolta **Adobe IO - OAuth**. Fai clic su **Invia** per richiedere un nuovo **access_token**.

![I/O fotogrammi](./images/frameV4api2.png)

Nel menu a sinistra, torna a **Raccolte**. Apri la richiesta **POST - Crea webhook** nella raccolta **Frame.io V4 - Tech Insiders**, nella cartella **Webhook**.

Vai al **Corpo** della richiesta. Cambia il campo **name** in `--aepUserLdap--  - Fusion to AEM Assets`, quindi cambia il campo **url** con il valore dell&#39;URL del webhook copiato da Workfront Fusion.

Fai clic su **Invia**.

![I/O fotogrammi](./images/framewh1.png)

L&#39;azione personalizzata Frame.io V4 è stata creata.

![I/O fotogrammi](./images/framewh2.png)

Vai a [https://next.frame.io/project](https://next.frame.io/project){target="_blank"} e vai al progetto creato in precedenza, che deve essere denominato `--aepUserLdap--`, quindi apri la cartella **Campagna Fibre Channel CitiSignal**. Dovresti ora visualizzare le risorse create nell’esercizio precedente.

![I/O fotogrammi](./images/aemf11a.png)

Fare clic sul campo **Stato** e modificare lo stato in **In corso**.

![I/O fotogrammi](./images/aemf12.png)

Tornare a Workfront Fusion. Ora dovresti vedere che la connessione era **stabilita correttamente**.

![I/O fotogrammi](./images/aemf13.png)

Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per eseguire un test rapido.

![I/O fotogrammi](./images/aemf14.png)

Torna a Frame.io, fai clic sul campo **In corso** e cambia lo stato in **Da rivedere**.

![I/O fotogrammi](./images/aemf15.png)

Torna a Workfront Fusion e fai clic sul fumetto nel modulo **Webhook personalizzato**.

La vista dettagliata della bolla mostra i dati ricevuti da Frame.io. Dovresti visualizzare diversi ID. Ad esempio, il campo **resource.id** mostra l&#39;ID univoco in Frame.io della risorsa **citisignal-fiber.psd**.

![I/O fotogrammi](./images/aemf16.png)

## 1.2.6.3 Ottieni dettagli risorsa da Frame.io

Ora che la comunicazione tra Frame.io e Workfront Fusion è stata stabilita tramite un webhook personalizzato, è necessario ottenere ulteriori dettagli sulla risorsa per la quale è stata aggiornata l’etichetta di stato. A questo scopo, utilizzerai nuovamente il connettore Frame.io in Workfront Fusion, in modo simile all’esercizio precedente.

Passa il puntatore sull&#39;oggetto **webhook personalizzato** e fai clic sull&#39;icona **+** per aggiungere un altro modulo.

![I/O fotogrammi](./images/aemf18a.png)

Immettere il termine di ricerca `frame`. Fare clic su **Frame.io**.

![I/O fotogrammi](./images/aemf18.png)

Fare clic su **Frame.io**.

![I/O fotogrammi](./images/aemf19.png)

Fai clic su **Effettua una chiamata API personalizzata**.

![I/O fotogrammi](./images/aemf20.png)

Verificare che la connessione sia impostata sulla stessa connessione creata nell&#39;esercizio precedente, che deve essere denominata `--aepUserLdap-- - Adobe I/O - Frame.io S2S`.

![I/O fotogrammi](./images/aemf21.png)

Per la configurazione del modulo **Frame.io - Effettuare una chiamata API personalizzata**, utilizzare l&#39;URL: `/v4/accounts/{{1.account.id}}/files/{{1.resource.id}}`.

>[!NOTE]
>
>È possibile specificare manualmente le variabili in Workfront Fusion utilizzando la seguente sintassi: `{{1.account.id}}` e `{{1.resource.id}}`. Il numero nella variabile fa riferimento al modulo nello scenario. In questo esempio, puoi vedere che il primo modulo nello scenario è denominato **Webhook** e ha un numero di sequenza di **1**. Ciò significa che le variabili `{{1.account.id}}` e `{{1.resource.id}}` accederanno a quel campo dal modulo con il numero di sequenza 1. I numeri di sequenza a volte possono essere diversi, quindi fai attenzione quando copi/incolla tali variabili e verifica sempre che il numero di sequenza utilizzato sia quello corretto.

Fare clic su **+ Aggiungi elemento** in **Stringa di query**.

![I/O fotogrammi](./images/aemf21a.png)

Immetti questi valori e fai clic su **Aggiungi**.

| Chiave | Valore |
|:-------------:| :---------------:| 
| `include` | `media_links.original` |

![I/O fotogrammi](./images/aemf21b.png)

Ora dovresti avere questo. Fai clic su **OK**.

![I/O fotogrammi](./images/aemf22.png)

Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per verificare la configurazione.

![I/O fotogrammi](./images/aemf23.png)

Torna a Frame.io e cambia lo stato in **In corso**.

![I/O fotogrammi](./images/aemf24.png)

Torna a Workfront Fusion e fai clic sul fumetto nel modulo **Frame.io - Effettua una chiamata API personalizzata**. Dovresti quindi visualizzare una panoramica simile.

![I/O fotogrammi](./images/aemf25.png)

Successivamente, devi impostare un filtro per garantire che venga eseguito il rendering di un file PNG solo per le risorse con stato **Approvato**. A tale scopo, fare clic sull&#39;icona **Chiave chiave** tra i moduli **WebHook personalizzato** e **Frame.io - Effettuare una chiamata API personalizzata** e quindi selezionare **Configura filtro**.

![I/O fotogrammi](./images/aemf25a.png)

Configura i campi seguenti:

- **Etichetta**: utilizzare `Status = Approved`.
- **Condizione**: `{{1.metadata.value[]}}`.
- **Operatori di base**: selezionare **Uguale a**.
- **Valore**: `Approved`.

Fai clic su **OK**.

![I/O fotogrammi](./images/aemf35.png)

Dovresti avere questo. Fai clic su **Salva** per salvare le modifiche.

![I/O fotogrammi](./images/aemf35a.png)

## 1.2.6.4 Converti in PNG

Passa il puntatore del mouse sul modulo **Frame.io - Esegui una chiamata API personalizzata** e fai clic sull&#39;icona **+**.

![I/O fotogrammi](./images/aemf27.png)

Immettere il termine di ricerca `photoshop` e quindi fare clic su **Adobe Photoshop**.

![I/O fotogrammi](./images/aemf28.png)

Fare clic su **Converti formato immagine**.

![I/O fotogrammi](./images/aemf29.png)

Verificare che il campo **Connessione** utilizzi la connessione creata in precedenza, denominata `--aepUserLdap-- - Adobe IO`.

In **Input**, impostare il campo **Archiviazione** su **Esterna** e impostare **Posizione file** per utilizzare la variabile **Originale** restituita dal modulo **Frame.io - Effettuare una chiamata API personalizzata**.

Fare clic su **Aggiungi elemento** in **Output**.

![I/O fotogrammi](./images/aemf30.png)

Per la configurazione di **Output**, impostare il campo **Archiviazione** su **Archiviazione interna di Fusion** e il **Tipo** su **immagine/png**. Fai clic su **Aggiungi**.

![I/O fotogrammi](./images/aemf31.png)

Fai clic su **OK**.

![I/O fotogrammi](./images/aemf33.png)

Fai clic su **Salva** per salvare le modifiche, quindi fai clic su **Esegui una volta** per verificare la configurazione.

![I/O fotogrammi](./images/aemf32.png)

Torna a Frame.io, fai clic sul campo **In corso** e cambia lo stato in **Approvato**.

![I/O fotogrammi](./images/aemf37.png)

Tornare a Workfront Fusion. Ora dovresti notare che tutti i moduli nello scenario sono stati eseguiti correttamente. Fare clic sulla bolla del modulo **Adobe Photoshop - Converti formato immagine**.

![I/O fotogrammi](./images/aemf38.png)

Nei dettagli dell&#39;esecuzione del modulo **Adobe Photoshop - Converti formato immagine** è stato generato un file PNG. Il passaggio successivo consiste nell’archiviare tale file in AEM Assets CS.

![I/O fotogrammi](./images/aemf39.png)

## PNG dell&#39;archivio 1.2.6.5 in AEM Assets CS

Passa il puntatore del mouse sul modulo **Adobe Photoshop - Converti formato immagine** e fai clic sull&#39;icona **+**.

![I/O fotogrammi](./images/aemf40.png)

Immetti il termine di ricerca `aem` e seleziona **AEM Assets**.

![I/O fotogrammi](./images/aemf41.png)

Fai clic su **Carica una risorsa**.

![I/O fotogrammi](./images/aemf42.png)

Ora devi configurare la connessione ad AEM Assets CS. Fai clic su **Aggiungi**.

![I/O fotogrammi](./images/aemf43.png)

Utilizza le seguenti impostazioni:

- **Tipo di connessione**: **AEM Assets as a Cloud Service**.
- **Nome connessione**: `--aepUserLdap-- AEM Assets CS`.
- **URL istanza**: copia l&#39;URL istanza dell&#39;ambiente di authoring AEM Assets CS, che deve essere simile al seguente: `https://author-pXXXXX-eXXXXXXX.adobeaemcloud.com`.
- **Opzioni di riempimento dettagli di accesso**: selezionare **Fornisci JSON**.

È ora necessario fornire le **credenziali dell&#39;account tecnico in formato JSON**. A tal fine, è necessario seguire una serie di passaggi utilizzando AEM Cloud Manager. Mentre lo fai, tieni aperta questa schermata.

![I/O fotogrammi](./images/aemf44.png)

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`. Poi vedrai qualcosa del genere. Fare clic per aprire il programma, che deve essere denominato `--aepUserLdap-- - Citi Signal`.

![I/O fotogrammi](./images/aemf45.png)

Fai clic sui tre punti **...** e seleziona **Developer Console**.

![I/O fotogrammi](./images/aemf46.png)

Fai clic su **Accedi con Adobe**.

![I/O fotogrammi](./images/aemf47.png)

Vai a **Strumenti** > **Integrazioni**.

![I/O fotogrammi](./images/aemf47a.png)

Fai clic su **Crea nuovo account tecnico**.

![I/O fotogrammi](./images/aemf48.png)

Dovresti vedere qualcosa del genere. Apri l’account tecnico appena creato. Fare clic sui tre punti **...**, quindi selezionare **Visualizza**.

![I/O fotogrammi](./images/aemf48a.png)

Dovresti quindi visualizzare un payload del token di account tecnico simile. Copia l’intero payload JSON negli Appunti.

![I/O fotogrammi](./images/aemf50.png)

Torna a Workfront Fusion e incolla il payload JSON completo nel campo **Credenziali account tecnico in formato JSON**. Fai clic su **Continua**.

![I/O fotogrammi](./images/aemf49.png)

La connessione verrà quindi convalidata e, in caso di esito positivo, verrà selezionata automaticamente nel modulo AEM Assets. Passare quindi alla configurazione di una cartella. Come parte dell’esercizio, devi creare una nuova cartella dedicata.

![I/O fotogrammi](./images/aemf51.png)

Per creare una nuova cartella dedicata, vai a [https://experience.adobe.com](https://experience.adobe.com/){target="_blank"}. Verificare che sia selezionata l&#39;istanza Experience Cloud corretta, che deve essere `--aepImsOrgName--`. Quindi fare clic su **Experience Manager Assets**.

![I/O fotogrammi](./images/aemf52.png)

Fai clic su **Seleziona** nell&#39;ambiente AEM Assets CS, che deve essere denominato `--aepUserLdap-- - Citi Signal dev`.

![I/O fotogrammi](./images/aemf53.png)

Vai a **Risorse** e fai clic su **Crea cartella**.

![I/O fotogrammi](./images/aemf54.png)

Immettere il nome `--aepUserLdap-- - CitiSignal Fiber Campaign` e fare clic su **Crea**.

![I/O fotogrammi](./images/aemf55.png)

La cartella viene quindi creata.

![I/O fotogrammi](./images/aemf56.png)

Torna a Workfront Fusion, seleziona **Fai clic qui per scegliere la cartella**, quindi scegli la cartella `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![I/O fotogrammi](./images/aemf57.png)

Verificare che la destinazione sia impostata su `--aepUserLdap-- - CitiSignal Fiber Campaign`. Quindi, in **File Source**, seleziona **Mappa**.

In **Nome file**, scegliere la variabile `{{3.filenames[1]}}`.

In **Dati**, scegliere la variabile `{{3.files[1]}}`.

>[!NOTE]
>
>È possibile specificare manualmente le variabili in Workfront Fusion utilizzando la seguente sintassi: `{{3.filenames[1]}}`. Il numero nella variabile fa riferimento al modulo nello scenario. In questo esempio, puoi vedere che il terzo modulo nello scenario è denominato **Adobe Photoshop - Converti formato immagine** e ha un numero di sequenza di **3**. Ciò significa che la variabile `{{3.filenames[1]}}` accederà al campo **nomefile[]** dal modulo con numero di sequenza 3. I numeri di sequenza a volte possono essere diversi, quindi fai attenzione quando copi/incolla tali variabili e verifica sempre che il numero di sequenza utilizzato sia quello corretto.

Fai clic su **OK**.

![I/O fotogrammi](./images/aemf58.png)

Fai clic su **Salva** per salvare le modifiche.

![I/O fotogrammi](./images/aemf59.png)

Successivamente, devi impostare autorizzazioni specifiche per l’account tecnico appena creato. Quando l&#39;account è stato creato in **Developer Console** in **Cloud Manager**, gli sono stati concessi i diritti di accesso **Read**, ma per questo caso d&#39;uso sono necessari i diritti di accesso **Write**. Per farlo, vai all’ambiente AEM CS Author.

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`. Fare clic per aprire il programma, che deve essere denominato `--aepUserLdap-- - Citi Signal`. Poi vedrai qualcosa del genere. Fai clic sull’URL dell’autore.

![I/O fotogrammi](./images/aemf60.png)

Fai clic su **Accedi con Adobe**.

![I/O fotogrammi](./images/aemf61.png)

Vai a **Impostazioni** > **Sicurezza** > **Utenti**.

![I/O fotogrammi](./images/aemf62.png)

Fai clic su per aprire l’account utente dell’account tecnico.

![I/O fotogrammi](./images/aemf63.png)

Vai a **Gruppi** e aggiungi questo utente account tecnico al gruppo **Utenti DAM**.

![I/O fotogrammi](./images/aemf64.png)

Fai clic su **Salva e chiudi**.

![I/O fotogrammi](./images/aemf65.png)

Tornare a Workfront Fusion. Fai clic su **Esegui una volta** per verificare lo scenario.

![I/O fotogrammi](./images/aemf66.png)

Torna a Frame.io e assicurati che lo stato della risorsa sia nuovamente **Approvato**.

>[!NOTE]
>
>Potrebbe essere necessario modificarlo di nuovo in **In corso** o **È necessario rivederlo**, quindi modificarlo di nuovo in **Approvato**.

![I/O fotogrammi](./images/aemf15.png)

Lo scenario Workfront Fusio verrà quindi attivato e dovrebbe essere completato correttamente. Visualizzando le informazioni nel fumetto del modulo **AEM Assets**, è già possibile vedere che il file PNG è stato archiviato correttamente in AEM Assets CS.

![I/O fotogrammi](./images/aemf67.png)

Tornare a AEM Assets CS e aprire la cartella `--aepUserLdap-- - Frame.io PNG`. Ora dovresti vedere il file PNG generato come parte dello scenario Workfront Fusion. Fare doppio clic sul file per aprirlo.

![I/O fotogrammi](./images/aemf68.png)

Ora puoi visualizzare ulteriori dettagli sui metadati del file PNG generato.

![I/O fotogrammi](./images/aemf69.png)

Hai completato correttamente questo esercizio.

## Passaggi successivi

Vai a [Riepilogo e vantaggi di Creative Workflow Automation con Workfront Fusion](./summary.md){target="_blank"}

Torna a [Automazione dei flussi di lavoro Creative con Workfront Fusion](./automation.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}

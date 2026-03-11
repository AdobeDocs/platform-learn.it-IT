---
title: Eseguire il flusso di lavoro personalizzato a livello di programmazione
description: Eseguire il flusso di lavoro personalizzato a livello di programmazione
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2 Eseguire il flusso di lavoro personalizzato a livello di programmazione

## 1.7.2.1 Esegui il flusso di lavoro personalizzato con Postman

Dopo aver pubblicato il flusso di lavoro nell’esercizio precedente, dovresti vedere qualcosa di simile a questo. Fai clic sul pulsante **Copia** per copiare il payload di esempio.

![Flussi di lavoro personalizzati Firefly](./images/ffcw61.png)

Apri Postman e crea una nuova **raccolta** utilizzando il nome **Flussi di lavoro personalizzati Firefly**. Quindi, fai clic su **aggiungi richiesta**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw62.png)

Dovresti quindi visualizzare una nuova richiesta vuota. Nella barra degli indirizzi, incolla il payload copiato dal flusso di lavoro pubblicato.

Postman riconoscerà il comando cURL incollato, prenderà tutte le informazioni dal payload e le aggiungerà nella richiesta nel modo corretto per te.

![Flussi di lavoro personalizzati Firefly](./images/ffcw63.png)

Dovrebbero essere visualizzate queste **variabili Intestazione**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw64.png)

Vai a **Corpo**, dove dovresti vedere qualcosa di simile a questo.

![Flussi di lavoro personalizzati Firefly](./images/ffcw65.png)

Ora devi fornire le istruzioni richieste nel corpo di questa richiesta. Quando si lavora con i file in modo programmatico, è necessario utilizzare URL prefirmati. Per questo esercizio, puoi trovare gli URL predefiniti qui sotto per le 3 immagini che fanno parte di questo esercizio. Questi URL prefirmati sono stati creati utilizzando le funzionalità di archiviazione di Microsoft Azure. Per ulteriori informazioni sulla creazione di URL prefirmati, consulta questo articolo: [Ottimizza il processo Firefly con Microsoft Azure e URL prefirmati](./../module1.1/ex2.md).

Per questo esercizio, puoi utilizzare i seguenti URL in modo da non dover creare personalmente nuovi URL prefirmati.

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

È inoltre necessario fornire prompt come parte della richiesta Postman. Di seguito sono riportati i prompt che è possibile utilizzare.

- **Prompt 1**:

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **Prompt 2**:

```
background hearts fluttering
```

Di seguito è riportato un payload di esempio, ma non puoi copiarlo e riutilizzarlo poiché i campi **node_id** sono univoci per il flusso di lavoro. Questo serve solo per darti un’idea di come dovrebbe apparire il payload:

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

Dopo aver apportato le modifiche al payload, dovrebbe presentarsi così. Al termine, fai clic su **Invia**. Quindi, usa **CMD + S** o **CTRL + S** per **salvare** la tua richiesta.

![Flussi di lavoro personalizzati Firefly](./images/ffcw66.png)

Nel payload di risposta ora puoi trovare un paio di collegamenti. Questi collegamenti consentono di eseguire una query sullo **stato** del flusso di lavoro e, una volta completato lo stato **&#x200B;**, è possibile utilizzare l&#39;URL **risultati** per recuperare l&#39;immagine e il video generati.

Seleziona l&#39;URL **status** e copialo.

![Flussi di lavoro personalizzati Firefly](./images/ffcw67.png)

Fai clic sui 3 punti della richiesta in uso, quindi seleziona **Duplica**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw69.png)

Nella nuova richiesta, modifica il tipo di richiesta in **GET** e sostituisci l&#39;URL con l&#39;URL dello stato appena copiato.

![Flussi di lavoro personalizzati Firefly](./images/ffcw70.png)

In **Corpo**, assicurati che tutto sia eliminato. Quindi fare clic su **Invia**. Dovresti quindi ricevere un payload di risposta simile, con uno stato visualizzato. Puoi inviare nuovamente la richiesta finché lo stato non cambia in **completato**. Non dimenticare di utilizzare **CMD + S** o **CTRL + S** per **salvare** la richiesta.

![Flussi di lavoro personalizzati Firefly](./images/ffcw71.png)

Torna alla prima richiesta **POST**. Copia ora l&#39;URL **results**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw72.png)

Fai clic sui tre punti **...** della seconda richiesta creata, quindi seleziona **Duplica**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw73.png)

Nella nuova richiesta, incolla l&#39;URL **results** copiato, quindi fai clic su **Invia**. Non dimenticare di utilizzare **CMD + S** o **CTRL + S** per **salvare** la richiesta.

![Flussi di lavoro personalizzati Firefly](./images/ffcw74.png)

Scorri verso il basso nel payload di risposta, dove troverai i riferimenti all’immagine e al video creati. Fai clic sui collegamenti per aprire questi file.

![Flussi di lavoro personalizzati Firefly](./images/ffcw75.png)

Ecco l&#39;immagine generata.

![Flussi di lavoro personalizzati Firefly](./images/ffcw76.png)

## 1.7.2.2 Esegui il flusso di lavoro personalizzato con Workfront Fusion

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Aprire **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Vai a **Scenari**. Se non si dispone ancora di una cartella, crearne una e per il nome utilizzare: `--aepUserLdap--`. Selezionare la cartella, quindi selezionare **Crea nuovo scenario**.

![WF Fusion](./images/wffusion2.png)

Dovresti vedere questo.

![WF Fusion](./images/wffusion3.png)

Dopo aver pubblicato il flusso di lavoro nell’esercizio precedente, dovresti vedere qualcosa di simile a questo. Fai clic sul pulsante **Copia** per copiare il payload di esempio.

![Flussi di lavoro personalizzati Firefly](./images/ffcw61.png)

Torna allo scenario Workfront Fusion. Utilizza **CMD + V** o **CTRL + V** per incollare il payload copiato nello scenario. Workfront Fusion rileverà automaticamente la richiesta cURL e creerà un nuovo modulo **HTTP - Creazione automatica di una richiesta**.

Trascina l&#39;icona **orologio** nel modulo **HTTP - Invia una richiesta**.

![WF Fusion](./images/wffusion5.png)

Dovresti vedere questo. Fai clic sul modulo **HTTP - Crea una richiesta** per aprirlo.

![WF Fusion](./images/wffusion6.png)

Dovresti quindi vedere che le variabili **Header** sono già disponibili.

![WF Fusion](./images/wffusion7.png)

Scorri verso il basso per visualizzare il payload predefinito. Fai clic sull&#39;**icona** come indicato per abbellire il payload JSON.

![WF Fusion](./images/wffusion8.png)

Torna a Postman, alla prima richiesta **POST**. Copia il payload.

![WF Fusion](./images/wffusion9.png)

Torna allo scenario Workfront Fusion. Sostituisci il payload predefinito esistente con quello copiato da Postman. Fai clic sull&#39;**icona** come indicato per abbellire il payload JSON.

Seleziona la casella di controllo per **Analisi risposta**.

Fai clic su **OK**.

![WF Fusion](./images/wffusion10.png)

Salva le modifiche e fai clic su **Esegui una volta**.

![WF Fusion](./images/wffusion11.png)

Una volta eseguito lo scenario, puoi vedere una risposta simile a quella ottenuta in Postman. Con queste informazioni disponibili in Workfront Fusion, ora puoi basarti su di esse per eseguire il polling dell&#39;URL **status** fino a quando lo stato non è completato, e una volta che ciò si è verificato, puoi utilizzare l&#39;URL **results** per raccogliere l&#39;immagine e il video generati.

![WF Fusion](./images/wffusion12.png)

## Passaggi successivi

Torna a [Flussi di lavoro personalizzati Firefly](./workflowbuilder.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}

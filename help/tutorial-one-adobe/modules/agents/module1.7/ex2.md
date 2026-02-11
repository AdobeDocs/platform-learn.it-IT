---
title: Utilizzare Cursor.ai per sviluppare il progetto
description: Utilizzare Cursor.ai per sviluppare il progetto
kt: 5342
doc-type: tutorial
source-git-commit: 2bfa7f4bee54df8411c96b001224d2986e9fcaf9
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 1.7.2 Utilizza Cursor.ai per sviluppare il tuo progetto

## 1.7.2.1 Configura directory e strumenti

Sul desktop, creare una nuova directory denominata `--aepUserLdap---commerce`

![Commerce e agente](./images/cursorai1.png)

Fai clic con il pulsante destro del mouse sulla cartella e seleziona **Nuovo terminale nella cartella**.

![Commerce e agente](./images/cursorai2.png)

Dovresti vedere questo.

![Commerce e agente](./images/cursorai3.png)

Ora devi clonare un archivio Github esistente, che puoi visualizzare [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit).

Questo archivio è il kit di avvio per l’integrazione di Adobe che utilizza Adobe Developer App Builder per migliorare l’affidabilità delle connessioni in tempo reale e ridurre il time-to-market per le integrazioni tra Adobe Commerce e altri sistemi di back-office, come ERP, CRM e PIM.

![Commerce e agente](./images/cursorai4.png)

Esistono diversi modi per clonare questo archivio; in questo esempio viene utilizzato Terminal.

Immetti il seguente comando nella finestra del terminale ed eseguilo.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce e agente](./images/cursorai5.png)

Dopo un paio di secondi, dovresti vedere questo risultato.

![Commerce e agente](./images/cursorai6.png)

Quindi, passa alla cartella appena creata. Immetti il seguente comando, quindi eseguilo.

`cd commerce-integration-starter-kit`

![Commerce e agente](./images/cursorai7.png)

Dovresti vedere questo.

![Commerce e agente](./images/cursorai8.png)

Successivamente, devi impostare gli strumenti di estensibilità di Commerce per Cursor.ai. Immetti il seguente comando, quindi eseguilo.

`aio commerce extensibility tools-setup`

![Commerce e agente](./images/cursorai9.png)

Selezionare **Directory corrente**.

![Commerce e agente](./images/cursorai10.png)

Seleziona **Cursore**.

![Commerce e agente](./images/cursorai11.png)

Seleziona **npm**.

![Commerce e agente](./images/cursorai12.png)

Dopo un paio di minuti, dovresti vederlo.

![Commerce e agente](./images/cursorai13.png)

Installando gli strumenti di estensibilità di Commerce per Cursor.ai, ora è disponibile un server MCP come parte dell’ambiente Cursor.ai. Negli esercizi successivi, utilizzerai il server MCP per sviluppare e distribuire il progetto App Builder.

## 1.7.2.2 Configura il tuo webhook

Per questo esercizio, avrai bisogno di un webhook che deve essere configurato in modo che, quando viene creato un ordine, l’evento dell’ordine possa essere inviato in streaming a tale webhook. In questo esercizio utilizzerai un endpoint di esempio utilizzando [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Vai a [https://pipedream.com/requestbin](https://pipedream.com/requestbin), crea un account e quindi crea un&#39;area di lavoro. Una volta creata l’area di lavoro, verrà visualizzato qualcosa di simile a questo.

Fai clic su **copia** per copiare l&#39;URL. Nel prossimo esercizio dovrai specificare questo URL. L&#39;URL in questo esempio è `https://eodts05snjmjz67.m.pipedream.net`.

![Cursor.ai + Commerce](./images/webhook1.png)

## Cursore.ai 1.7.2.3

Apri Cursor.ai. Fai clic su **Apri progetto**.

![Cursor.ai + Commerce](./images/cursorai14.png)

Passare alla cartella creata, che deve essere denominata `--aepUserLdap---commerce`. In tale cartella selezionare la cartella denominata `commerce-integration-starter-kit`. Fai clic su **Apri**.

![Cursor.ai + Commerce](./images/cursorai15.png)

Dovresti vedere questo. Prima di continuare, verificare che la cartella di primo livello aperta in Cursor.ai sia `commerce-integration-starter-kit`.

![Cursor.ai + Commerce](./images/cursorai16.png)

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

## Passaggi successivi

Torna a [Strumenti per sviluppatori intelligenti per Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
---
title: Server e cursore MCP di AEM
description: Server e cursore MCP di AEM
kt: 5342
doc-type: tutorial
exl-id: c966623f-3b8b-451a-b5fb-5569ef50c88f
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# 1.6.2 Server e cursore MCP AEM

>[!IMPORTANT]
>
>Per completare questo esercizio, devi avere accesso a un ambiente AEM Sites e Assets CS funzionante con EDS e i vari agenti AEM devono essere abilitati per l’organizzazione IMS in uso.
>
>Se non si dispone ancora di un ambiente di questo tipo, passare all&#39;esercizio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Sites e Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.


Di seguito sono elencati tutti i server AEM MCP disponibili:

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly (Operazioni per contenuti di sola lettura)
- https://mcp.adobeaemcloud.com/adobe/mcp/content-updater (espone l’abilità corrispondente dall’agente Experience Production)
- https://mcp.adobeaemcloud.com/adobe/mcp/experience-governance (espone le abilità per ottenere e controllare la politica del brand per una pagina)
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery (espone le abilità per scoprire i contenuti in un ambiente AEM)

In questo esercizio troverai istruzioni su come utilizzare questi server MCP specifici:

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery

È possibile utilizzare le istruzioni seguenti per configurare server MCP simili per gli altri server MCP di AEM disponibili, in quanto il processo è molto simile.

## Configurazione del server MCP del cursore di 1.6.2.1 Experience Agent Production

Crea una nuova cartella vuota sul desktop.

![Cursore + AEM](./images/cursorai1.png)

Apri cursore. Fai clic su **Apri progetto**.

![Cursore + AEM](./images/cursorai2.png)

Seleziona la cartella creata in precedenza e fai clic su **Apri**.

![Cursore + AEM](./images/cursorai3.png)

Fare clic su **Sì, gli autori sono attendibili**.

![Cursore + AEM](./images/cursorai4.png)

Dovresti vedere questo. Utilizzare la scelta rapida da tastiera `Cmd + Shift + J` per aprire le impostazioni del cursore. Dovresti vedere questo. Vai a **Strumenti e MCP**.

![Cursore + AEM](./images/cursorai5.png)

Fare clic su **+ Nuovo server MCP**.

![Cursore + AEM](./images/cursorai6.png)

Aggiungi il seguente server MCP al file **mcp.json**. Potrebbero essere già presenti altri server MCP specificati in questo file. Non rimuoverli e aggiungi semplicemente le nuove righe seguenti. Salva le modifiche.

```json
"aem": {
    "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
    }
```

![Cursore + AEM](./images/cursorai7.png)

Torna alla scheda **Impostazioni cursore**. Nell&#39;elenco dei server MCP è stato aggiunto lo strumento **aem**. Fai clic su **connetti** per eseguire l&#39;autenticazione con il tuo account Adobe.

![Cursore + AEM](./images/cursorai8.png)

Se ricevi questo messaggio, fai clic su **Apri**. A questo punto dovrai effettuare l’autenticazione nel browser.

![Cursore + AEM](./images/cursorai9.png)

Dopo l’autenticazione corretta, dovresti vedere qualcosa di simile a questo.

![Cursore + AEM](./images/cursorai10.png)

Chiudi le schede **Impostazioni cursore** e **mcp.json**. Incolla il seguente prompt nella chat e fai clic su **invia**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Cursore + AEM](./images/cursorai11.png)

Fare clic su **Esegui**.

![Cursore + AEM](./images/cursorai12.png)

Dovresti vedere una risposta simile.

![Cursore + AEM](./images/cursorai13.png)

![Cursore + AEM](./images/cursorai14.png)

Come puoi vedere, funzionalità simili vengono esposte tramite il server MCP in Cursor rispetto a quanto era possibile utilizzando l’Assistente AI nell’esercizio precedente.

Immetti il seguente prompt e fai clic su **Invia**.

```javascript
List AEM Author instances
```

![Cursore + AEM](./images/cursorai15.png)

Dovresti vedere qualcosa del genere. Cercare l&#39;ambiente che si desidera utilizzare, quindi immettere il seguente prompt e fare clic su **Invia**.

```javascript
use environment number X
```

![Cursore + AEM](./images/cursorai16.png)

Dovresti vedere questo.

![Cursore + AEM](./images/cursorai17.png)

Incolla il seguente prompt e fai clic su **invia**. Sostituisci XXX in questo prompt con l’URL copiato nell’esercizio precedente.

```
On the page https://author-p185022-e1936676.adobeaemcloud.com/content/CitiSignal/fiber-max.html, please make the following changes:

- change the word 'winter' to 'summer'
- change the text 'be as fast as a leopard' to 'dominate your internet like a gorilla'
- change the image in the hero block to use the image 'citisignal_gorilla.png'
- change the text '99.9% network reliability' to '99.998% network reliability'
```

![Cursore + AEM](./images/cursorai18.png)

Dopo 1-2 minuti, dovrebbe ottenere una risposta simile. Copia l’URL e apri la pagina nel browser.

![Cursore + AEM](./images/cursorai19.png)

Dovresti vedere questo.

![Cursore + AEM](./images/cursorai20.png)

Immetti il seguente prompt e fai clic su **Invia**.

```javascript
promote the changes by creating a new launch and promoting it
```

![Cursore + AEM](./images/cursorai21.png)

Dopo 1-2 minuti, le modifiche sono state promosse.

![Cursore + AEM](./images/cursorai22.png)

Ora puoi vedere le modifiche in diretta sul tuo sito web.

![Cursore + AEM](./images/cursorai23.png)

Puoi esplorare anche le altre funzionalità del server AEM MCP.

## Installazione del server MCP del cursore dell&#39;agente di individuazione 1.6.2.2

Utilizzare la scelta rapida da tastiera `Cmd + Shift + J` per aprire le impostazioni del cursore. Dovresti vedere questo. Vai a **Strumenti e MCP**. Fare clic su **+ Nuovo server MCP**.

![Cursore + AEM](./images/cursoraiz5.png)

Aggiungi il seguente server MCP al file **mcp.json**. Potrebbero essere già presenti altri server MCP specificati in questo file. Non rimuoverli e aggiungi semplicemente le nuove righe seguenti. Salva le modifiche.

```
,
"aem-discovery": {
    "url": "https://mcp.adobeaemcloud.com/adobe/mcp/discovery"
}
```

![Cursore + AEM](./images/cursoraiz7.png)

Torna alla scheda **Impostazioni cursore**. Nell&#39;elenco dei server MCP è stato aggiunto lo strumento **aem**. Fai clic su **connetti** per eseguire l&#39;autenticazione con il tuo account Adobe.

![Cursore + AEM](./images/cursoraiz8.png)

Dopo l’autenticazione, dovresti visualizzarlo.

![Cursore + AEM](./images/cursoraiz9.png)

Chiudi le schede **Impostazioni cursore** e **mcp.json**. Incolla il seguente prompt nella chat e fai clic su **invia**.

```
I just created a new custom mcp server named 'aem-discovery'. what can I do with that?
```

![Cursore + AEM](./images/cursoraiz10.png)

```
for the environment https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/, list all assets tagged with 'Spring 2026'
```

![Cursore + AEM](./images/cursoraiz11.png)

Dovresti vedere qualcosa del genere.

![Cursore + AEM](./images/cursoraiz12.png)

## Passaggi successivi

Torna a [AEM e agenti](./aemagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

---
title: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora - Definizione di azioni personalizzate
description: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora - Definizione di azioni personalizzate
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 8.3 Definire un’azione personalizzata

In questo esercizio creerai due azioni personalizzate utilizzando Adobe Journey Optimizer in combinazione.

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fai clic su **Gestisci** pulsante sotto **Azioni**.

![Demo](./images/menuactions.png)

Vedrai il **Azioni** elenco.

![Demo](./images/acthome.png)

Definisci un’azione che invia un testo a un canale di Slack.

## 8.3.1 Azione: Invia testo al canale di Slack

Ora potrai utilizzare un canale di Slack esistente e inviare messaggi a tale canale di Slack. Slack dispone di un’API di facile utilizzo e utilizzeremo Adobe Journey Optimizer per attivarne l’API.

![Demo](./images/slack.png)

Fai clic su **Crea azione** per iniziare ad aggiungere una nuova azione.

![Demo](./images/adda.png)

Verrà visualizzata una finestra a comparsa Azione vuota.

![Demo](./images/emptyact.png)

Come nome dell’azione, utilizza `--demoProfileLdap--TextSlack`. In questo esempio, il Nome azione è `vangeluwTextSlack`.

Imposta descrizione su: `Send Text to Slack`.

![Demo](./images/slackname.png)

Per **Configurazione URL**, utilizza:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metodo: **POST**

>[!NOTE]
>
>L&#39;URL di cui sopra fa riferimento a una funzione AWS Lambda che inoltrerà la richiesta al canale di Slack come indicato sopra. Questo viene fatto per proteggere l&#39;accesso a un canale di Slack di proprietà di un Adobe. Se hai un tuo canale di Slack, devi creare un&#39;app di Slack tramite [https://api.slack.com/](https://api.slack.com/), devi quindi creare un Webhook in entrata in quell’app di Slack e sostituire l’URL di cui sopra con l’URL Webhook in entrata.

Non è necessario modificare i campi di intestazione.

![Demo](./images/slackurl.png)

**Autenticazione** deve essere impostato su **Nessuna autenticazione**.

![Demo](./images/slackauth.png)

Per **Parametri azione**, è necessario definire quali campi devono essere inviati verso lo Slack. Logicamente, vogliamo che Adobe Journey Optimizer e Adobe Experience Platform siano il cervello della personalizzazione, quindi il testo da inviare allo Slack dovrebbe essere definito da Adobe Journey Optimizer e quindi inviato allo Slack per l&#39;esecuzione.

Quindi per **Parametri azione**, fai clic su **Modifica payload** icona.

![Demo](./images/slackmsgp.png)

Verrà visualizzata una finestra popup vuota.

![Demo](./images/slackmsgpopup.png)

Copia il testo seguente e incollalo nella finestra popup vuota.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

FYI: specificando i campi seguenti, questi campi diventeranno accessibili dal Percorso del cliente e potrai compilarli dinamicamente dal Percorso:

**&quot;toBeMapped&quot;: vero,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Vedrai questo:

![Demo](./images/slackmsgpopup1.png)

Fai clic su **Salva**.

![Demo](./images/twiliomsgpopup2.png)

Scorri verso l’alto e fai clic su **Salva** un&#39;altra volta per salvare l&#39;azione personalizzata.

![Demo](./images/slackmsgpopup3.png)

L&#39;azione personalizzata ora fa parte del **Azioni** elenco.

![Demo](./images/slackdone.png)

Hai definito eventi, origini dati esterne e azioni. Ora consolidiamo tutto questo in un percorso.

Passaggio successivo: [8.4 Creare percorsi e messaggi](./ex4.md)

[Torna al modulo 8](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../overview.md)

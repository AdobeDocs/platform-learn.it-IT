---
title: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definisci azioni personalizzate
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definisci azioni personalizzate
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 3%

---

# 3.2.3 Definire un&#39;azione personalizzata

In questo esercizio creerai due azioni personalizzate utilizzando Adobe Journey Optimizer in combinazione.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Per passare da una sandbox all&#39;altra, fare clic su **Production Prod (VA7)** e selezionare la sandbox dall&#39;elenco. In questo esempio, la sandbox è denominata **AEP Enablement FY22**. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Azioni**.

![Demo](./images/menuactions.png)

Verrà quindi visualizzato l&#39;elenco **Azioni**.

![Demo](./images/acthome.png)

Definirai un’azione che invia un testo a un canale di Slack.

## 3.2.3.1 Azione: inviare testo al canale di Slack

Ora utilizzerai un canale di Slack esistente e invierai messaggi a tale canale di Slack. Slack ha un’API di facile utilizzo e utilizzeremo Adobe Journey Optimizer per attivarne l’API.

![Demo](./images/slack.png)

Fai clic su **Crea azione** per iniziare ad aggiungere una nuova azione.

![Demo](./images/adda.png)

Viene visualizzata una finestra a comparsa Azione vuota.

![Demo](./images/emptyact.png)

Come nome dell&#39;azione, utilizzare `--aepUserLdap--TextSlack`. In questo esempio, il nome azione è `vangeluwTextSlack`.

Imposta descrizione su: `Send Text to Slack`.

![Demo](./images/slackname.png)

Per la **configurazione URL**, utilizzare:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metodo: **POST**

>[!NOTE]
>
>L’URL riportato sopra fa riferimento a una funzione AWS Lambda che inoltra la richiesta al canale di Slack come indicato sopra. Questa operazione viene eseguita per proteggere l’accesso a un canale di Slack di proprietà dell’Adobe. Se si dispone di un proprio canale di Slack, è necessario creare un&#39;app di Slack tramite [https://api.slack.com/](https://api.slack.com/), quindi è necessario creare un webhook in ingresso in tale app di Slack e sostituire l&#39;URL indicato sopra con l&#39;URL del webhook in ingresso.

Non è necessario modificare i campi intestazione.

![Demo](./images/slackurl.png)

**Autenticazione** deve essere impostato su **Nessuna autenticazione**.

![Demo](./images/slackauth.png)

Per **Parametri azione**, è necessario definire quali campi devono essere inviati allo Slack. Logicamente, vogliamo che Adobe Journey Optimizer e Adobe Experience Platform siano il cervello della personalizzazione, quindi il testo da inviare allo Slack deve essere definito da Adobe Journey Optimizer e quindi inviato allo Slack per l’esecuzione.

Quindi, per **Parametri azione**, fai clic sull&#39;icona **Modifica payload**.

![Demo](./images/slackmsgp.png)

Viene quindi visualizzata una finestra popup vuota.

![Demo](./images/slackmsgpopup.png)

Copiare il testo seguente e incollarlo nella finestra popup vuota.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

Nota: specificando i campi seguenti, questi campi saranno accessibili dal Percorso del cliente e potrai compilarli in modo dinamico dal Percorso:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;stringa&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

A questo punto viene visualizzato quanto segue:

![Demo](./images/slackmsgpopup1.png)

Fai clic su **Salva**.

![Demo](./images/twiliomsgpopup2.png)

Scorri verso l&#39;alto e fai clic su **Salva** un&#39;altra volta per salvare l&#39;azione personalizzata.

![Demo](./images/slackmsgpopup3.png)

L&#39;azione personalizzata fa ora parte dell&#39;elenco **Azioni**.

![Demo](./images/slackdone.png)

Hai definito eventi, un’origine dati esterna e azioni. Ora consolidiamo tutto questo in un percorso.

Passaggio successivo: [3.2.4 Creare il percorso e i messaggi](./ex4.md)

[Torna al modulo 8](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../../overview.md)

---
title: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definisci azioni personalizzate
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definisci azioni personalizzate
kt: 5342
doc-type: tutorial
exl-id: d9bdc4c6-7539-4646-9b75-f397b792479f
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 3%

---

# 3.2.3 Definire un&#39;azione personalizzata

In questo esercizio verrà creata un&#39;azione personalizzata per inviare un messaggio a un canale di Slack.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

Ora utilizzerai un canale di Slack esistente e invierai messaggi a tale canale di Slack. Slack dispone di un’API di facile utilizzo e utilizzerai Adobe Journey Optimizer per attivarne l’API.

![Demo](./images/slack.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Azioni**.

![Demo](./images/menuactions.png)

Verrà quindi visualizzato l&#39;elenco **Azioni**. Fai clic su **Crea azione**.

![Demo](./images/acthome.png)

Viene visualizzata una finestra a comparsa Azione vuota.

![Demo](./images/emptyact.png)

Come nome dell&#39;azione, utilizzare `--aepUserLdap--TextSlack`.

Imposta descrizione su: `Send Message to Slack`.

Per la **configurazione URL**, utilizzare:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metodo: **POST**

>[!NOTE]
>
>L’URL riportato sopra fa riferimento a una funzione AWS Lambda che inoltra la richiesta al canale di Slack come indicato sopra. Questa operazione viene eseguita per proteggere l’accesso a un canale di Slack di proprietà dell’Adobe. Se si dispone di un proprio canale di Slack, è necessario creare un&#39;app di Slack tramite [https://api.slack.com/](https://api.slack.com/), quindi è necessario creare un webhook in ingresso in tale app di Slack e sostituire l&#39;URL indicato sopra con l&#39;URL del webhook in ingresso.

![Demo](./images/slackname.png)

Non è necessario modificare i campi intestazione.

![Demo](./images/slackurl.png)

**Autenticazione** deve essere impostato su **Nessuna autenticazione**.

![Demo](./images/slackauth.png)

In **Payload**, è necessario definire quali campi devono essere inviati allo Slack. Logicamente, vuoi che Adobe Journey Optimizer e Adobe Experience Platform siano il cervello della personalizzazione, quindi il testo da inviare allo Slack deve essere definito da Adobe Journey Optimizer e quindi inviato allo Slack per l’esecuzione.

Per **Richiesta**, fai clic sull&#39;icona **Modifica payload**.

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

A questo punto viene visualizzato quanto segue:

![Demo](./images/slackmsgpopup1.png)

Scorri verso l&#39;alto e fai clic su **Salva** un&#39;altra volta per salvare l&#39;azione.

![Demo](./images/slackmsgpopup3.png)

L&#39;azione personalizzata fa ora parte dell&#39;elenco **Azioni**.

![Demo](./images/slackdone.png)

Hai definito eventi, un’origine dati esterna e azioni. Ora consolidiamo tutto questo in un percorso.

Passaggio successivo: [3.2.4 Creare il percorso e i messaggi](./ex4.md)

[Torna al modulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../../overview.md)

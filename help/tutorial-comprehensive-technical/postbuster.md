---
title: PostBuster - Dipendenti Adobe
description: PostBuster - Dipendenti Adobe
doc-type: multipage-overview
exl-id: a798e9d7-bb99-4390-885f-5fbd2ef4cee9
source-git-commit: 9c1b30dc0fcca6b4324ec7c8158699fa273cdc90
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Le istruzioni seguenti sono destinate esclusivamente ai dipendenti Adobe.

>[!IMPORTANT]
>
>Seguendo le istruzioni di seguito, avrai già a disposizione tutte le raccolte API richieste che verranno utilizzate in questi esercizi:
>
>- [2.1.3 Visualizza il tuo profilo cliente in tempo reale - API](./modules/rtcdp-b2c/module2.1/ex3.md)
>- [2.3.6 Destinazioni SDK](./modules/rtcdp-b2c/module2.3/ex6.md)
>- [3.3.6 Verifica la tua decisione utilizzando l&#39;API](./modules/ajo-b2c/module3.3/ex6.md)
>- [5.1.8 API servizio query](./modules/datadistiller/module5.1/ex8.md)

## Installare PostBuster

Vai a [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Fai clic per scaricare l&#39;ultima versione di **PostBuster**.

![PostBuster](./assets/images/pb1.png)

Scarica la versione corretta per il tuo sistema operativo.

![PostBuster](./assets/images/pb2.png)

Una volta completato e installato il download, aprire PostBuster. Dovresti vedere questo. Fai clic su **Importa**.

![PostBuster](./assets/images/pb3.png)

Scarica [postbuster.json.zip](./assets/postman/postbuster.json.zip) ed estrailo dal desktop.

![PostBuster](./assets/images/pbpb.png)

Fare clic su **Scegli un file**.

![PostBuster](./assets/images/pb4.png)

Seleziona il file **aep_tutorial.json**. Fai clic su **Apri**.

![PostBuster](./assets/images/pb5.png)

Dovresti vedere questo. Fare clic su **Scansione**.

![PostBuster](./assets/images/pb6.png)

Fai clic su **Importa**.

![PostBuster](./assets/images/pb7.png)

Dovresti vedere questo. Fai clic su per aprire la raccolta importata.

![PostBuster](./assets/images/pb8.png)

Ora puoi vedere la tua raccolta. È comunque necessario configurare un ambiente in modo che contenga alcune variabili di ambiente.

![PostBuster](./assets/images/pb9.png)

Fare clic su **Ambiente base** e quindi sull&#39;icona **modifica**.

![PostBuster](./assets/images/pb10.png)

Dovresti vedere questo.

![PostBuster](./assets/images/pb11.png)

Copiare il segnaposto dell&#39;ambiente seguente e incollarlo nell&#39;**ambiente base**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"read_organizations",
		"additional_info.projectedProductContext",
		"session",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"QS_QUERY_ID": "",
	"SANDBOX_NAME": ""
}
```

Dovresti avere questo.

![PostBuster](./assets/images/pb12.png)

Dopo aver creato il progetto di I/O Adobe, l’ambiente dovrebbe presentarsi così. Non è necessario eseguire questa operazione ora, verrà affrontata in una fase successiva.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Informazioni tecniche](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](./overview.md)

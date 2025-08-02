---
title: Guida introduttiva a Workfront
description: Guida introduttiva a Workfront
kt: 5342
doc-type: tutorial
source-git-commit: 34f37a33e874f55eea37290b5626ab613f575764
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---

# 1.2.4 Workfront + AEM Sites

Accedi ad Adobe Workfront da [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Poi vedete questo.

![WF](./images/wfb1.png)

## 1.2.4.1 Configurare l&#39;integrazione AEM Sites

>[!NOTE]
>
>Questo plug-in è attualmente in modalità **Accesso anticipato** e non è ancora disponibile a livello generale.
>
>Questo plug-in potrebbe essere già installato nell’istanza di Workfront utilizzata. Se è già installato, puoi consultare le istruzioni riportate di seguito, ma non è necessario apportare alcuna modifica alla configurazione.

Vai a [https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}.

Verificare che l&#39;opzione **Attiva** per questo plug-in sia impostata su **Attiva**. Quindi, fai clic sull&#39;icona **ingranaggio**.

![WF](./images/wfb8.png)

Verrà visualizzata una finestra a comparsa **Configurazione estensione**. Configura i campi seguenti per utilizzare questo plug-in.

| Chiave | Valore |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;: true, &quot;publishUrl&quot;: true}&#39;** |

Fai clic su **Salva**.

![WF](./images/wfb8.png)

Torna all&#39;interfaccia utente di Workfront e fai clic sull&#39;icona dei 9 puntini **hamburger**. Selezionare **Configurazione**.

![WF](./images/wfb9.png)

Nel menu a sinistra, vai a **Forms personalizzato** e seleziona **Modulo**. Fare clic su **+ Nuovo modulo personalizzato**.

![WF](./images/wfb10.png)

Seleziona **Attività** e fai clic su **Continua**.

![WF](./images/wfb11.png)

Verrà quindi visualizzato un modulo personalizzato vuoto. Immettere il nome del modulo `Content Fragment & Integration ID`.

![WF](./images/wfb12.png)

Trascina un nuovo campo **Testo su riga singola** nell&#39;area di lavoro.

![WF](./images/wfb13.png)

Configura il nuovo campo come segue:

- **Etichetta**: **Frammento di contenuto**
- **Nome**: **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

Aggiungi un nuovo campo **Testo a riga singola** nell&#39;area di lavoro e configura il nuovo campo come segue:

- **Etichetta**: **ID integrazione**
- **Nome**: **`aem_workfront_integration_id`**

Fare clic su **Applica**.

![WF](./images/wfb15.png)

Ora devi configurare un secondo modulo personalizzato. Fare clic su **+ Nuovo modulo personalizzato**.

![WF](./images/wfb10.png)

Seleziona **Attività** e fai clic su **Continua**.

![WF](./images/wfb11.png)

Verrà quindi visualizzato un modulo personalizzato vuoto. Immettere il nome del modulo `Preview & Publish URL`.

![WF](./images/wfb16.png)

Trascina un nuovo campo **Testo su riga singola** nell&#39;area di lavoro.

![WF](./images/wfb17.png)

Configura il nuovo campo come segue:

- **Etichetta**: **URL anteprima**
- **Nome**: **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

Aggiungi un nuovo campo **Testo a riga singola** nell&#39;area di lavoro e configura il nuovo campo come segue:

- **Etichetta**: **URL pubblicazione**
- **Nome**: **`aem_workfront_integration_publish_url`**

Fare clic su **Applica**.

![WF](./images/wfb19.png)

Dovresti quindi avere a disposizione 2 moduli personalizzati.

![WF](./images/wfb20.png)

Passaggio successivo: [1.2.2 Verifica con Workfront](./ex2.md){target="_blank"}

Torna a [Gestione dei flussi di lavoro con Adobe Workfront](./workfront.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

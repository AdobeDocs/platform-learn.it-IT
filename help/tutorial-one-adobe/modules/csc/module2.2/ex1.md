---
title: Guida introduttiva a Workfront
description: Guida introduttiva a Workfront
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# 2.2.1 Guida introduttiva a Workfront

Accedi ad Adobe Workfront da [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Poi vedete questo.

![WF](./images/wfb1.png)

## 2.2.1.1 Configurare l’integrazione di AEM Assets

Fai clic sull&#39;icona dei 9 punti **hamburger**, quindi seleziona **Configurazione**.

![WF](./images/wfb2.png)

Nel menu a sinistra, scorri verso il basso fino a **Documenti** e quindi fai clic su **Experience Manager Assets**.

![WF](./images/wfb3.png)

Fare clic su **+ Aggiungi integrazione Experience Manager**.

![WF](./images/wfb4.png)

Per il nome dell&#39;integrazione, utilizzare `--aepUserLdap-- - Citi Signal AEM`.

Apri il menu a discesa **Archivio Experience Manager** e seleziona l&#39;istanza di AEM CS, che deve essere denominata `--aepUserLdap-- - Citi Signal`.

![WF](./images/wfb5.png)

In **Metadati**, configura la seguente mappatura:

| Campo Workfront | Campo Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Documento** > **Nome** | **wm:nomeDocumento** |
| **Progetto** > **Descrizione** | **wm:projectDescription** |
| **Attività** > **Nome** | **wm:taskName** |
| **Attività** > **Descrizione** | **wm:taskDescription** |

Abilitare il parametro per **sincronizzare i metadati dell&#39;oggetto**.

Fai clic su **Salva**.

![WF](./images/wfb6.png)

L’integrazione tra Workfront e AEM Assets CS è ora configurata.

![WF](./images/wfb7.png)

## 2.2.1.2 Configurare l’integrazione di AEM Sites

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

- **Etichetta**: **URL Publish**
- **Nome**: **`aem_workfront_integration_publish_url`**

Fare clic su **Applica**.

![WF](./images/wfb19.png)

Dovresti quindi avere a disposizione 2 moduli personalizzati.

![WF](./images/wfb20.png)

[Torna al modulo 2.2](./workfront.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

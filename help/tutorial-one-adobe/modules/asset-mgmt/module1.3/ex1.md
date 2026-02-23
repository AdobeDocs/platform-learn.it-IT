---
title: Creare il primo modulo
description: Creare il primo modulo
kt: 5342
doc-type: tutorial
source-git-commit: 8f59b9fdadc9c5aeadb1d4ecccd75090c339b43e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 10%

---

# 1.3.1 Creare il primo modulo

>[!IMPORTANT]
>
>Per completare questo esercizio, devi avere accesso a un ambiente AEM Assets CS Author funzionante in cui sia abilitato AEM Assets Dynamic Media.
>
>Se non disponi di un ambiente di questo tipo, passa a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.3.1.1 -

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`. Apri l’ambiente.

![AEM Forms](./images/aemforms1.png)

Vai a **Forms**.

![AEM Forms](./images/aemforms2.png)

Vai a **Forms e documenti**.

![AEM Forms](./images/aemforms3.png)

Fai clic su **Crea**, quindi seleziona **Modulo adattivo**.

![AEM Forms](./images/aemforms4.png)

Seleziona **Edge Delivery Services** e quindi **Pagina vuota**. Fai clic su **Crea**.

![AEM Forms](./images/aemforms5.png)

Dovresti vedere questo. Compila i campi seguenti:

- **Titolo**: `Fiber Max Interest Form`
- **Nome**: deve essere compilato automaticamente in base al campo **Titolo**.
- **URL Github**: fornisci il percorso dell&#39;archivio Github collegato al tuo sito Web

Fai clic su **Crea**.

![AEM Forms](./images/aemforms6.png)

Dopo aver fatto clic su **Crea**, l&#39;**Editor universale** dovrebbe aprirsi automaticamente e dovrebbe essere visualizzato qualcosa di simile. Fare clic sull&#39;icona per aprire la **Struttura contenuto**.

![AEM Forms](./images/aemforms7.png)

Nella **Struttura contenuto**, selezionare l&#39;oggetto **Modulo adattivo**.

![AEM Forms](./images/aemforms8.png)

Quindi fare clic sull&#39;icona **+** per aggiungere un nuovo elemento e selezionare **immissione testo**.

![AEM Forms](./images/aemforms9.png)

Nella **Struttura contenuto**, selezionare il campo **Input testo**.

![AEM Forms](./images/aemforms10.png)

Passare alla visualizzazione **Base**. Dovresti vedere questo.

Compila i campi seguenti:

- **Nome**: `first-name`
- **Titolo**: `First Name`

Quindi, vai a **Convalida**.

![AEM Forms](./images/aemforms11.png)

Capovolgere l&#39;interruttore per rendere obbligatorio il campo. Compila i campi seguenti:

- **Messaggio di errore**: `Enter your first name`
- **Pattern**: `[A-Za-z][A-Za-z ]+`
- **Messaggio di errore pattern**: `Letters only!`

![AEM Forms](./images/aemforms12.png)

Nella **Struttura contenuto**, seleziona il campo **Modulo adattivo**. Fai clic sull&#39;icona **+**, quindi seleziona **immissione testo**.

![AEM Forms](./images/aemforms13.png)

Nella **Struttura contenuto**, selezionare il campo appena creato **Input testo**. Vai a **Proprietà**.

![AEM Forms](./images/aemforms14.png)

Passare alla visualizzazione **Base**. Dovresti vedere questo.

Compila i campi seguenti:

- **Nome**: `last-name`
- **Titolo**: `Last Name`

Quindi, vai a **Convalida**.

![AEM Forms](./images/aemforms15.png)

Capovolgere l&#39;interruttore per rendere obbligatorio il campo. Compila i campi seguenti:

- **Messaggio di errore**: `Enter your last name`
- **Pattern**: `[A-Za-z][A-Za-z ]+`
- **Messaggio di errore pattern**: `Letters only!`

![AEM Forms](./images/aemforms16.png)

Nella **Struttura contenuto**, seleziona il campo **Modulo adattivo**. Fai clic sull&#39;icona **+**, quindi seleziona **immissione testo**.

![AEM Forms](./images/aemforms17.png)

Nella **Struttura contenuto**, selezionare il campo appena creato **Input testo**. Vai a **Proprietà**.

![AEM Forms](./images/aemforms18.png)

Passare alla visualizzazione **Base**. Dovresti vedere questo.

Compila i campi seguenti:

- **Nome**: `email`
- **Titolo**: `Email`

Quindi, vai a **Convalida**.

![AEM Forms](./images/aemforms19.png)

Capovolgere l&#39;interruttore per rendere obbligatorio il campo. Compila i campi seguenti:

- **Messaggio di errore**: `Enter your email address`
- **Pattern**: `^[^@]+@[^@]+\.[^@]+$`
- **Messaggio di errore pattern**: `Please verify your email address!`

![AEM Forms](./images/aemforms20.png)

Nella **Struttura contenuto**, seleziona il campo **Modulo adattivo**. Fai clic sull&#39;icona **+**, quindi seleziona **immissione testo**.

![AEM Forms](./images/aemforms21.png)

Nella **Struttura contenuto**, selezionare il campo appena creato **Input testo**.

![AEM Forms](./images/aemforms22.png)

Passare alla visualizzazione **Base**. Dovresti vedere questo.

Compila i campi seguenti:

- **Nome**: `city`
- **Titolo**: `city`

Quindi, vai a **Convalida**.

![AEM Forms](./images/aemforms23.png)

Capovolgere l&#39;interruttore per rendere obbligatorio il campo. Compila i campi seguenti:

- **Messaggio di errore**: `Enter your city`
- **Pattern**: `[A-Za-z][A-Za-z ]+`
- **Messaggio di errore pattern**: `Letters only!`

![AEM Forms](./images/aemforms24.png)

Fai clic su **Pubblica**.

![AEM Forms](./images/aemforms25.png)

Fai di nuovo clic su **Pubblica**.

![AEM Forms](./images/aemforms26.png)

Fare clic per aprire il modulo.

![AEM Forms](./images/aemforms27.png)

Sarà quindi possibile compilare il modulo, ma non è ancora possibile inviarlo.

![AEM Forms](./images/aemforms28.png)

## Passaggi successivi

Passaggio successivo: [-](./ex1.md){target="_blank"}

Torna a [Adobe Experience Manager Forms con Edge Delivery Services](./aemforms.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

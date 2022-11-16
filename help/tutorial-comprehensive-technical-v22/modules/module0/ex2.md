---
title: Guida introduttiva - Utilizzare Demo System Next per impostare la proprietà Launch
description: Guida introduttiva - Utilizzare Demo System Next per impostare la proprietà Launch
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 9c0eddf5-bfd7-4e7a-a8e2-ccd55ccd966d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 0.2 Utilizzare Demo System Next per configurare la proprietà client Adobe Experience Platform Data Collection

Dopo aver effettuato la registrazione al tutorial tecnico completo per Adobe Experience Platform, è disponibile un processo automatizzato che ti fornirà l’accesso a Demo System, in modo da poter accedere ed eseguire la configurazione seguente.

Una volta ottenuto l&#39;accesso a Demo System, procedi con i passaggi seguenti.

Vai a [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/). Seleziona la sandbox e fai clic su **Configurazione rapida**.

![DSN](./images/dsnh1.png)

Vedrai questo:

![DSN](./images/dsnhome.png)

Sotto **Generale** - **Ambiente**, seleziona la tua istanza Adobe Experience Platform e la tua sandbox, in questo caso:

- **Experience Platform internazionale**
- **aepenablementfy22**
- Configurazione: selezionare **Global v2.0**

![DSN](./images/dsn1.png)

Quindi, seleziona il predefinito **Utente di abilitazione** e fai clic su **Inizio**.

![DSN](./images/dsn2.png)

Nella finestra a comparsa, immetti un nome per la proprietà Raccolta dati. Utilizza questa convenzione di denominazione: **Sistema di demo (GG/MM/AAAA)**. FYI: il tuo LDAP verrà aggiunto automaticamente, non devi aggiungerlo tu stesso.

Fai clic su **Avvia**.

![DSN](./images/dsn3.png)

Verrà quindi visualizzata questa finestra a comparsa che mostra lo stato di avanzamento durante la creazione di progetti di siti web e app mobili e le proprietà di raccolta dati.

![DSN](./images/dsn4.png)

Una volta completato il processo di configurazione rapida, avrai a disposizione:

- 1 Progetto Web Retail, che consente di utilizzare un sito web dimostrativo con il marchio demo Luma
- 1 Progetto Mobile Retail, che consente di utilizzare un’app mobile demo con il marchio demo Luma
- 1 Progetto CX App Retail, che consente di utilizzare un call center e un’app client con il marchio demo Luma
- 1 Proprietà di raccolta dati per il web, che utilizzerai per raccogliere dati dal sito web
- 1 Proprietà di raccolta dati per dispositivi mobili, che utilizzerai per raccogliere dati dall’app mobile

![DSN](./images/dsn5.png)

Tieni aperta questa schermata quando ne avrai bisogno nei passaggi successivi.

Passaggio successivo: [0.3 Creare il Datastream](./ex3.md)

[Torna al modulo 0](./getting-started.md)

[Torna a tutti i moduli](./../../overview.md)

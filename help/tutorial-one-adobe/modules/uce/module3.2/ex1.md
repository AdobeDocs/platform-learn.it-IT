---
title: Guida introduttiva ad AJO Translation Services
description: Guida introduttiva ad AJO Translation Services
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---

# 3.2.1 Fornitore di traduzioni

## 3.2.1.1 Configurare Microsoft Azure Translator

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home).

![Traduzioni](./images/transl1.png)

Nella barra di ricerca immettere `translators`. Quindi fare clic su **+ Crea**.

![Traduzioni](./images/transl2.png)

Seleziona **Crea traduttore**.

![Traduzioni](./images/transl3.png)

Scegli il tuo **ID abbonamento** e **gruppo di risorse**.
Imposta **Regione** su **Globale**.
Impostare **Livello prezzi** su **F0** gratuito.

Seleziona **Rivedi + crea**.

![Traduzioni](./images/transl4.png)

Seleziona **Crea**.

![Traduzioni](./images/transl5.png)

Selezionare **Vai alla risorsa**.

![Traduzioni](./images/transl6.png)

Nel menu a sinistra, vai a **Gestione risorse** > **Chiavi ed endpoint**. Fai clic su per copiare la chiave.

![Traduzioni](./images/transl7.png)

## 3.2.1.2 Dizionario delle impostazioni internazionali

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Nel menu a sinistra, vai a **Traduzioni** e quindi vai a **Dizionario impostazioni internazionali**. Se viene visualizzato questo messaggio, fare clic su **Aggiungi impostazioni internazionali predefinite**.

![Traduzioni](./images/locale1.png)

Dovresti vedere questo.

![Traduzioni](./images/locale2.png)

## 3.2.1.3 Configurare il provider di traduzioni in AJO

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Nel menu a sinistra, vai a **Traduzioni** e quindi vai a **Provider**. Fare clic su **Aggiungi provider**.

![Traduzioni](./images/transl8.png)

In **Provider**, selezionare **Microsoft Translator**. Seleziona la casella di controllo per abilitare l’utilizzo del provider di traduzione. Incolla la chiave copiata da Microsoft Azure Translators. Quindi fare clic su **Convalida credenziali**.

![Traduzioni](./images/transl9.png)

Le credenziali devono quindi essere convalidate correttamente. Se lo sono, scorri verso il basso per selezionare le lingue per la traduzione.

![Traduzioni](./images/transl10.png)

Selezionare `[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`.

![Traduzioni](./images/transl11.png)

Scorri verso l&#39;alto e fai clic su **Salva**.

![Traduzioni](./images/transl12.png)

Il **provider di traduzioni** è pronto per essere utilizzato.

![Traduzioni](./images/transl13.png)

## 3.2.1.4 Configurare il progetto di traduzione

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Nel menu a sinistra, vai a **Traduzioni** e quindi vai a **Dizionario impostazioni internazionali**. Se viene visualizzato questo messaggio, fare clic su **Crea progetto**.

![Traduzioni](./images/ajoprovider1.png)

Immettere il nome `--aepUserLdap-- - Translations`, impostare **Impostazioni internazionali Source** su `[en-US] English - United States` e selezionare la casella di controllo per abilitare **Pubblica automaticamente traduzioni approvate**. Fare clic su **+ Aggiungi una lingua**.

![Traduzioni](./images/ajoprovider1a.png)

Cerca `fr`, abilita la casella di controllo per `[fr] French`, quindi abilita la casella di controllo per **Microsoft Translator**. Fare clic su **+ per aggiungere una lingua**.

![Traduzioni](./images/ajoprovider2.png)

Cerca `es`, abilita la casella di controllo per `[es] Spanish`, quindi abilita la casella di controllo per **Microsoft Translator**. Fare clic su **+ per aggiungere una lingua**.

![Traduzioni](./images/ajoprovider3.png)

Cerca `nl`, abilita la casella di controllo per `[nl] Spanish`, quindi abilita la casella di controllo per **Microsoft Translator**. Fare clic su **+ per aggiungere una lingua**.

![Traduzioni](./images/ajoprovider6.png)

Fai clic su **Salva**.

![Traduzioni](./images/ajoprovider8.png)

Il progetto **Traduzioni** è pronto per essere utilizzato.

![Traduzioni](./images/ajoprovider9.png)

Hai finito questo esercizio.

## Passaggi successivi

Vai a [3.2.2 Crea la tua campagna](./ex2.md)

Torna a [Modulo 3.2](./ajotranslationsvcs.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
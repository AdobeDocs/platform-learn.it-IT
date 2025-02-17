---
title: Guida introduttiva ad AJO Translation Services
description: Guida introduttiva ad AJO Translation Services
kt: 5342
doc-type: tutorial
exl-id: ec032c58-c5c2-48d2-bdd3-ff860bc4a35a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 3.5.1 Fornitore di traduzioni

## 3.5.1.1 Configurare Microsoft Azure Translator

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

## 3.5.1.2 Dizionario delle impostazioni internazionali

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Nel menu a sinistra, vai a **Traduzioni** e quindi vai a **Dizionario impostazioni internazionali**. Se viene visualizzato questo messaggio, fare clic su **Aggiungi impostazioni internazionali predefinite**.

![Traduzioni](./images/locale1.png)

Dovresti vedere questo.

![Traduzioni](./images/locale2.png)

## 3.5.1.3 Configurare il provider di traduzioni in AJO

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

## 3.5.1.4 Configurare il progetto di traduzione

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Nel menu a sinistra, vai a **Traduzioni** e quindi vai a **Dizionario impostazioni internazionali**. Se viene visualizzato questo messaggio, fare clic su **Crea progetto**.

![Traduzioni](./images/ajoprovider1.png)

Immettere il nome `--aepUserLdap-- - Translations`, impostare **Impostazioni internazionali Source** su `[en-US] English - United States` e selezionare le caselle di controllo per abilitare **Pubblica automaticamente traduzioni approvate** e **Abilita flusso di lavoro di revisione**. Fare clic su **+ Aggiungi una lingua**.

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

## 3.5.1.5 Configurare le impostazioni della lingua

Vai a **Canali** > **Impostazioni generali** > **Impostazioni lingua**. Fare clic su **Crea impostazioni lingua**.

![Journey Optimizer](./images/camploc6.png)

Utilizza il nome `--aepUserLdap--_translations`. Seleziona **Progetto di traduzione**. Quindi fai clic sull&#39;icona **modifica**.

![Journey Optimizer](./images/camploc7.png)

Seleziona il progetto di traduzioni creato nel passaggio precedente. Fai clic su **Seleziona**.

![Journey Optimizer](./images/camploc8.png)

Dovresti vedere questo. Imposta la **preferenza di fallback** su **Inglese - Stati Uniti**. Fai clic per selezionare **Seleziona l&#39;attributo preferito della lingua del profilo**, che deciderà quale campo del profilo cliente utilizzare per caricare le traduzioni. Quindi fai clic sull&#39;icona **modifica** per selezionare il campo da utilizzare.

![Journey Optimizer](./images/camploc9.png)

Immetti **lingua preferita** nella barra di ricerca, quindi seleziona il campo **Lingua preferita**.

![Journey Optimizer](./images/camploc10.png)

Fai clic sull&#39;icona **modifica** per **Inglese - Stati Uniti** e **Olandese** per esaminarne la configurazione.

![Journey Optimizer](./images/camploc11.png)

Ecco la configurazione per **Inglese - Stati Uniti**. Fare clic su **Annulla**.

![Journey Optimizer](./images/camploc12.png)

Fare clic per visualizzare la configurazione per **Olandese**. Fare clic su **Annulla**.

![Journey Optimizer](./images/camploc13.png)

Scorri verso l&#39;alto e fai clic su **Invia**.

![Journey Optimizer](./images/camploc14.png)

Le impostazioni della lingua sono ora configurate.

![Journey Optimizer](./images/camploc15.png)

Hai finito questo esercizio.

## Passaggi successivi

Vai a [3.5.2 Crea la tua campagna](./ex2.md)

Torna a [Adobe Journey Optimizer: Servizi di traduzione](./ajotranslationsvcs.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}

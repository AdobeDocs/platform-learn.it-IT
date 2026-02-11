---
title: Configurare una campagna con messaggi in-app
description: Configurare una campagna con messaggi in-app
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 3.3.3 Configurare una campagna con messaggi in-app

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Configurazione canale messaggi in-app 3.3.3.1

Nel menu a sinistra, vai a **Canali** e quindi seleziona **Configurazioni canale**. Fai clic su **Crea configurazione canale**.

![InApp](./images/inapp1.png)

Immetti il nome: `--aepUserLdap--_In-app_Messages`, seleziona il canale **Messaggistica in-app**, quindi abilita le piattaforme **Web**, **iOS** e **Android**.

![InApp](./images/inapp2.png)

Scorri verso il basso, dovresti vedere questo.

![InApp](./images/inapp3.png)

Verificare che **Pagina singola** sia abilitato.

Per **Web**, immettere l&#39;URL del sito Web creato in precedenza come parte del modulo **Guida introduttiva**, che si presenta così: `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. Non dimenticare di modificare **XXXX** nel codice univoco del sito Web.

Per **iOS** e **Android**, immetti `com.adobe.dsn.dxdemo`.

![InApp](./images/inapp4.png)

Scorri verso l&#39;alto e fai clic su **Invia**.

![InApp](./images/inapp5.png)

La configurazione del canale è ora pronta per essere utilizzata.

![InApp](./images/inapp6.png)

## 3.3.3.2 Configurare una campagna pianificata per i messaggi in-app

Nel menu a sinistra, vai a **Campagne** e quindi fai clic su **Crea campagna**.

![InApp](./images/inapp7.png)

Selezionare **Pianificato - Marketing**, quindi fare clic su **Crea**.

![InApp](./images/inapp8.png)

Immettere il nome `--aepUserLdap-- - CitiSignal Fiber Max` e quindi fare clic su **Azioni**.

![InApp](./images/inapp9.png)

Fai clic su **+ Aggiungi azione**, quindi seleziona **Messaggio in-app**.

![InApp](./images/inapp10.png)

Selezionare la configurazione del canale messaggi in-app creata nel passaggio precedente, denominata: `--aepUserLdap--_In-app_Messages`. Fare clic su **Modifica contenuto**.

![InApp](./images/inapp11.png)

Dovresti vedere questo. Fai clic su **Modale**.

![InApp](./images/inapp12.png)

Fare clic su **Cambia layout**.

![InApp](./images/inapp13.png)

Fai clic sull&#39;icona **URL file multimediali** per scegliere una risorsa da AEM Assets.

![InApp](./images/inapp14.png)

Vai alla cartella **citisignal-images** e seleziona il file di immagine **neon-rabbit.jpg**. Fai clic su **Seleziona**.

![InApp](./images/inapp15.png)

Per il testo **Intestazione**, utilizzare: `CitiSignal Fiber Max`.
Per il testo **Body**, utilizzare: `Conquer lag with Fiber Max`.

![InApp](./images/inapp16.png)

Impostare il **pulsante #1 testo** su: `Go to Plans`.
Imposta **target** su `com.adobe.dsn.dxdemo://plans`.

Fai clic su **Rivedi per attivare**.

![InApp](./images/inapp17.png)

Fare clic su **Attiva**.

![InApp](./images/inapp18.png)

Lo stato della campagna è ora impostato su **Attivazione**. Potrebbero essere necessari un paio di minuti prima che la campagna sia in diretta.

![InApp](./images/inapp19.png)

Dopo aver cambiato lo stato in **Live**, puoi testare la tua campagna.

![InApp](./images/inapp20.png)

## 3.3.3.3 Test della campagna di messaggistica in-app su dispositivi mobili

Sul dispositivo mobile, apri l’app. Dovresti quindi visualizzare il nuovo messaggio in-app dopo l’avvio dell’app. Fai clic sul pulsante **Vai a piani**.

![InApp](./images/inapp21.png)

Verrai quindi portato alla pagina **Piani**.

![InApp](./images/inapp22.png)

## Passaggi successivi

Torna a [Adobe Journey Optimizer: messaggi push e in-app](ajopushinapp.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}

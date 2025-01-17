---
title: Guida introduttiva a Workfront Fusion
description: Guida introduttiva a Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 3%

---

# 1.2.1 Guida introduttiva di Workfront Fusion

In questo esercizio utilizzerai Workfront Fusion e Adobe I/O per eseguire query sulle API di Adobe Firefly Services.

## 1.2.1.1 Creare un nuovo scenario

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic per aprire **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Dovresti vedere questo. Vai a **Scenari**.

![WF Fusion](./images/wffusion2.png)

Fai clic sull&#39;icona **+** per creare una nuova cartella.

![WF Fusion](./images/wffusion2a.png)

Per il nome della cartella, utilizzare: `--aepUserLdap--`. Fai clic su **Salva**.

![WF Fusion](./images/wffusion2b.png)

Seleziona la cartella e fai clic su **Crea nuovo scenario**.

![WF Fusion](./images/wffusion3.png)

Viene quindi visualizzato uno scenario vuoto. Fai clic sull&#39;icona **strumenti** e seleziona **Imposta più variabili**.

![WF Fusion](./images/wffusion4.png)

È ora necessario spostare l&#39;icona **orologio** sulle **variabili multiple** appena aggiunte.

![WF Fusion](./images/wffusion5.png)

Poi vedrai questo.

![WF Fusion](./images/wffusion6.png)

Quindi fare clic con il pulsante destro del mouse sul punto interrogativo e selezionare **Elimina modulo**.

![WF Fusion](./images/wffusion7.png)

Fare quindi clic con il pulsante destro del mouse sull&#39;oggetto **Imposta più variabili** e selezionare **Impostazioni**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurare l’autenticazione Adobe I/O

Ora devi configurare le variabili necessarie per l’autenticazione in base a Adobe I/O. Nell’esercizio precedente hai creato un progetto di Adobe I/O. Le variabili di tale progetto di Adobe I/O ora devono essere definite in Workfront Fusion.

È necessario definire le seguenti variabili:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `CONST_client_id` | ID client del progetto Adobe I/O |
| `CONST_client_secret` | il segreto client del progetto Adobe I/O |
| `CONST_scope` | ambito del progetto di Adobe I/O |

Per trovare queste variabili, vai a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) e apri il tuo progetto di Adobe I/O, denominato `--aepUserLdap-- Firefly`.

![WF Fusion](./images/wffusion9.png)

Nel progetto, fai clic su **OAuth Server-to-Server** per visualizzare i valori per le chiavi di cui sopra.

![WF Fusion](./images/wffusion10.png)

Con le chiavi e i valori indicati sopra, è possibile configurare l&#39;oggetto **Imposta più variabili**. Fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffusion11.png)

Immetti il **Nome variabile**: **CONST_client_id** e il relativo **Valore variabile**, quindi fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion12.png)

Fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffusion13.png)

Immetti il **Nome variabile**: **CONST_client_secret** e il relativo **Valore variabile**, quindi fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion14.png)

Fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffusion15.png)

Immetti il **Nome variabile**: **Const_scope** e il relativo **Valore variabile**, quindi fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion16.png)

Fai clic su **OK**.

![WF Fusion](./images/wffusion17.png)

Passa il puntatore del mouse sull&#39;oggetto **Imposta più variabili** e fai clic sull&#39;icona grande **+** per aggiungere un altro modulo.

![WF Fusion](./images/wffusion18.png)

Dovresti vedere questo.

![WF Fusion](./images/wffusion19.png)

Nella barra di ricerca immettere **http**. Seleziona **HTTP** per aprirlo.

![WF Fusion](./images/wffusion21.png)

e quindi selezionare **Effettua una richiesta**.

![WF Fusion](./images/wffusion20.png)

| Chiave | Valore |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Fare clic su **Aggiungi elemento**.

![WF Fusion](./images/wffusion22.png)

Aggiungi elementi per ciascuno dei seguenti valori:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `client_id` | la variabile predefinita per `CONST_client_id` |
| `client_secret` | la variabile predefinita per `CONST_client_secret` |
| `scope` | la variabile predefinita per `CONST_scope` |
| `grant_type` | `client_credentials` |

Configurazione per `client_id`.

![WF Fusion](./images/wffusion23.png)

Configurazione per `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configurazione per `scope`.

![WF Fusion](./images/wffusion26.png)

Configurazione per `grant_type`.

![WF Fusion](./images/wffusion28.png)

Panoramica sulla configurazione. Scorri verso il basso e seleziona la casella di controllo per **Analizzare la risposta**. Fai clic su **OK**.

![WF Fusion](./images/wffusion27.png)

Dovresti vedere questo. Fare clic su **Esegui una volta**.

![WF Fusion](./images/wffusion29.png)

Una volta eseguito lo scenario, dovresti visualizzarlo.

![WF Fusion](./images/wffusion30.png)

Fai clic sull&#39;icona **punto interrogativo** nell&#39;oggetto **Imposta più variabili** per vedere cosa è successo quando l&#39;oggetto è stato eseguito.

![WF Fusion](./images/wffusion31.png)

Fai clic sull&#39;icona **punto interrogativo** sull&#39;oggetto **HTTP - Richiedi** per vedere cosa è successo quando l&#39;oggetto è stato eseguito. Nel **OUTPUT**, vedrai il **access_token** restituito dall&#39;Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Passa il puntatore del mouse sull&#39;oggetto **HTTP - Esegui una richiesta** e fai clic sull&#39;icona **+** per aggiungere un altro modulo.

![WF Fusion](./images/wffusion33.png)

Nella barra di ricerca, cercare `tools`. Seleziona **Strumenti**.

![WF Fusion](./images/wffusion34.png)

Selezionare **Imposta più variabili**.

![WF Fusion](./images/wffusion35.png)

Seleziona **Aggiungi elemento**.

![WF Fusion](./images/wffusion36.png)

Impostare **Nome variabile** su `bearer_token`. Selezionare `access_token` come **valore di variabile** dinamico. Clic **Aggiungi**.

![WF Fusion](./images/wffusion37.png)

Dovresti avere questo. Fai clic su **OK**.

![WF Fusion](./images/wffusion38.png)

Fai di nuovo clic su **Esegui**.

![WF Fusion](./images/wffusion39.png)

Una volta eseguito lo scenario, fare clic sull&#39;icona **punto interrogativo** sull&#39;ultimo oggetto **Imposta più variabili**. Si noti quindi che il token di accesso viene archiviato nella variabile `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Fare quindi clic con il pulsante destro del mouse sul primo oggetto **Imposta più valori** e selezionare **Rinomina**.

![WF Fusion](./images/wffusion41.png)

Imposta il nome su **Inizializza costanti**. Fai clic su **OK**.

![WF Fusion](./images/wffusion42.png)

Rinominare il secondo oggetto e impostare il nome su **Autentica su Adobe I/O**. Fai clic su **OK**.

![WF Fusion](./images/wffusion43.png)

Rinomina il terzo oggetto e imposta il nome su **Imposta token Bearer**. Fai clic su **OK**.

![WF Fusion](./images/wffusion44.png)

Dovresti avere questo.

![WF Fusion](./images/wffusion45.png)

Quindi, cambia il nome dello scenario in `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Fai clic su **Salva**.

![WF Fusion](./images/wffusion47.png)

Passaggio successivo: [1.2.2 Utilizzare le API Adobe in Workfront Fusion](./ex2.md)

[Torna al modulo 1.2](./automation.md)

[Torna a tutti i moduli](./../../../overview.md)

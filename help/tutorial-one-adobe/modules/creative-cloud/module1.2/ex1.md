---
title: Guida introduttiva a Workfront Fusion
description: Scopri come utilizzare Workfront Fusion e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 53ff5158eec2693703b20e7841fffbec72288210
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---

# Guida introduttiva a Workfront Fusion

Scopri come utilizzare Workfront Fusion e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly.

## Crea nuovo scenario

1. Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Aprire **Workfront Fusion**.

   ![WF Fusion](./images/wffusion1.png)

1. Vai a **Scenari**.

   ![WF Fusion](./images/wffusion2.png)

1. Seleziona **Crea nuovo scenario**.

   ![WF Fusion](./images/wffusion2a.png)

1. Assegna un nome alla cartella `--aepUserLdap--` e seleziona **Salva**.

   ![WF Fusion](./images/wffusion2b.png)

1. Selezionare la cartella, quindi selezionare **Crea nuovo scenario**.

   ![WF Fusion](./images/wffusion3.png)

1. Viene visualizzato uno scenario vuoto. Selezionare **strumenti** e **Imposta più variabili**.

   ![WF Fusion](./images/wffusion4.png)

1. Sposta l&#39;icona **orologio** nelle **variabili multiple** appena aggiunte.

   ![WF Fusion](./images/wffusion5.png)

   Lo schermo dovrebbe essere simile al seguente.

   ![WF Fusion](./images/wffusion6.png)

1. Fare clic con il pulsante destro del mouse sul punto interrogativo e selezionare **Elimina modulo**.

   ![WF Fusion](./images/wffusion7.png)

1. Fare clic con il pulsante destro del mouse su **Imposta più variabili** e selezionare **Impostazioni**.

   ![WF Fusion](./images/wffusion8.png)

## Configurare l’autenticazione Adobe I/O

Ora devi configurare le variabili necessarie per l’autenticazione in base a Adobe I/O. Nell’esercizio precedente hai creato un progetto di Adobe I/O. Le variabili di tale progetto di Adobe I/O ora devono essere definite in Workfront Fusion.

È necessario definire le seguenti variabili:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `CONST_client_id` | ID client del progetto Adobe I/O |
| `CONST_client_secret` | il segreto client del progetto Adobe I/O |
| `CONST_scope` | ambito del progetto di Adobe I/O |

1. Trova queste variabili da [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) e apri il tuo progetto di Adobe I/O, denominato `--aepUserLdap-- Firefly`.

   ![WF Fusion](./images/wffusion9.png)

1. Nel progetto, seleziona **OAuth Server-Server** per visualizzare i valori per le chiavi di cui sopra.

   ![WF Fusion](./images/wffusion10.png)

1. Utilizzando le chiavi e i valori di cui sopra, è possibile configurare l&#39;oggetto **Imposta più variabili**. Seleziona **Aggiungi elemento**.

   ![WF Fusion](./images/wffusion11.png)

1. Immetti il **Nome variabile**: **CONST_client_id** e il relativo **Valore variabile**, seleziona **Aggiungi**.

   ![WF Fusion](./images/wffusion12.png)

1. Seleziona **Aggiungi elemento**.

   ![WF Fusion](./images/wffusion13.png)

1. Immetti **Nome variabile**: **CONST_client_secret** e il relativo **Valore variabile**. Seleziona **Aggiungi**.

   ![WF Fusion](./images/wffusion14.png)

1. Seleziona **Aggiungi elemento**.

   ![WF Fusion](./images/wffusion15.png)

1. Immetti **Nome variabile**: **CONST_scope** e il relativo **Valore variabile**. Seleziona **Aggiungi**.

   ![WF Fusion](./images/wffusion16.png)

1. Selezionare **OK**.

   ![WF Fusion](./images/wffusion17.png)

1. Passa il puntatore del mouse su **Imposta più variabili** e seleziona l&#39;icona grande **+** per aggiungere un altro modulo.

   ![WF Fusion](./images/wffusion18.png)

   Lo schermo dovrebbe essere simile al seguente.

   ![WF Fusion](./images/wffusion19.png)

1. Nella barra di ricerca immettere **http**. Seleziona **HTTP** per aprirlo.

   ![WF Fusion](./images/wffusion21.png)

1. Seleziona **Crea una richiesta**.

   ![WF Fusion](./images/wffusion20.png)

   | Chiave | Valore |
   |:-------------:| :---------------:| 
   | `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
   | `Method` | `POST` |
   | `Body Type` | `x-www-form-urlencoded` |

1. Seleziona **Aggiungi elemento**.

   ![WF Fusion](./images/wffusion22.png)

1. Aggiungi elementi per ciascuno dei seguenti valori:

   | Chiave | Valore |
   |:-------------:| :---------------:| 
   | `client_id` | la variabile predefinita per `CONST_client_id` |
   | `client_secret` | la variabile predefinita per `CONST_client_secret` |
   | `scope` | la variabile predefinita per `CONST_scope` |
   | `grant_type` | `client_credentials` |

1. Configurazione per `client_id`:

   ![WF Fusion](./images/wffusion23.png)

1. Configurazione per `client_secret`.

   ![WF Fusion](./images/wffusion25.png)

1. Configurazione per `scope`.

   ![WF Fusion](./images/wffusion26.png)

1. Configurazione per `grant_type`.

   ![WF Fusion](./images/wffusion28.png)

1. Scorri verso il basso e seleziona la casella per **Analizzare la risposta**. Selezionare **OK**.

   ![WF Fusion](./images/wffusion27.png)

1. Lo schermo dovrebbe essere simile al seguente. Selezionare **Esegui una volta**.

   ![WF Fusion](./images/wffusion29.png)

   Una volta eseguito lo scenario, lo schermo dovrebbe essere simile al seguente:

   ![WF Fusion](./images/wffusion30.png)

1. Selezionare l&#39;icona **punto interrogativo** nell&#39;oggetto **Imposta più variabili** per visualizzare l&#39;evento che si è verificato durante l&#39;esecuzione dell&#39;oggetto.

   ![WF Fusion](./images/wffusion31.png)

1. Seleziona l&#39;icona **punto interrogativo** sull&#39;oggetto **HTTP - Richiedi** per visualizzare l&#39;evento che si è verificato durante l&#39;esecuzione dell&#39;oggetto. Nel **OUTPUT**, vedi il **access_token** restituito dall&#39;Adobe I/O.

   ![WF Fusion](./images/wffusion32.png)

1. Passa il puntatore del mouse su **HTTP - Effettua una richiesta** e seleziona l&#39;icona **+** per aggiungere un altro modulo.

   ![WF Fusion](./images/wffusion33.png)

1. Nella barra di ricerca, cercare `tools`. Seleziona **Strumenti**.

   ![WF Fusion](./images/wffusion34.png)

1. Selezionare **Imposta più variabili**.

   ![WF Fusion](./images/wffusion35.png)

1. Seleziona **Aggiungi elemento**.

   ![WF Fusion](./images/wffusion36.png)

1. Imposta **Nome variabile** su `bearer_token`. Selezionare `access_token` come **valore di variabile** dinamico. Seleziona **Aggiungi**.

   ![WF Fusion](./images/wffusion37.png)

1. Lo schermo dovrebbe essere simile al seguente. Selezionare **OK**.

   ![WF Fusion](./images/wffusion38.png)

1. Seleziona di nuovo **Esegui**.

   ![WF Fusion](./images/wffusion39.png)

1. Una volta eseguito lo scenario, selezionare l&#39;icona **punto interrogativo** sull&#39;ultimo oggetto **Imposta più variabili**. Il token di accesso viene archiviato nella variabile `bearer_token`.

   ![WF Fusion](./images/wffusion40.png)

1. Fare quindi clic con il pulsante destro del mouse sul primo oggetto **Imposta più valori** e selezionare **Rinomina**.

   ![WF Fusion](./images/wffusion41.png)

1. Imposta il nome su **Inizializza costanti**. Selezionare **OK**.

   ![WF Fusion](./images/wffusion42.png)

1. Rinomina il secondo oggetto in **Autentica in Adobe I/O**. Selezionare **OK**.

   ![WF Fusion](./images/wffusion43.png)

1. Rinomina il terzo oggetto in **Imposta token Bearer**. Selezionare **OK**.

   ![WF Fusion](./images/wffusion44.png)

   Lo schermo dovrebbe essere simile al seguente:

   ![WF Fusion](./images/wffusion45.png)

1. Quindi, cambia il nome dello scenario in `--aepUSerLdap-- - Adobe I/O Authentication`.

   ![WF Fusion](./images/wffusion46.png)

1. Seleziona **Salva**.

   ![WF Fusion](./images/wffusion47.png)

## Passaggi successivi

Vai a [Utilizza le API di Adobe in Workfront Fusion](./ex2.md){target="_blank"}

Torna a [Automazione dei servizi Adobe Firefly](./automation.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}

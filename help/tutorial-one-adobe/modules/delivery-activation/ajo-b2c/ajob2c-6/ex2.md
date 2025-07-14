---
title: Pagine di destinazione in Adobe Journey Optimizer
description: Pagine di destinazione in Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: bf499aad-91d0-4fb5-a38c-db8fcd56480b
source-git-commit: 83e8418b1a9e5e0e37f97473d2c7539ccd3fd803
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 9%

---

# 3.6.2 Pagine di destinazione

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.6.2.1 elenchi di iscrizioni

Le pagine di destinazione in Adobe Journey Optimizer funzionano insieme a **Elenchi di iscrizioni**. Per impostare le pagine di destinazione, devi prima configurare **Elenchi di iscrizioni**.

CitiSignal desidera invitare i propri clienti a conoscere il loro interesse per i seguenti domini:

- Pagina principale Smart
- Lavoro da casa
- Giochi online

Una volta che un cliente ha indicato il suo interesse in uno di questi domini, deve essere aggiunto a un elenco specifico in modo che possa successivamente essere utilizzato come destinazione un contenuto specifico nell’ambito delle prossime campagne.

Verranno creati 3 elenchi di iscrizioni.

Nel menu a sinistra, vai a **Elenchi di iscrizioni**. Fai clic su **Crea elenco iscrizioni**.

![Pagine di destinazione](./images/lp1.png)

Per **Titolo**, utilizzare: `--aepUserLdap--_SL_Interest_in_Smart_Home`.
Per **Descrizione**, utilizzare: `Interest in Smart Home`.

Fai clic su **Invia**.

![Pagine di destinazione](./images/lp2.png)

Fai clic su **Crea elenco iscrizioni** per creare un altro elenco.

![Pagine di destinazione](./images/lp3.png)

Per **Titolo**, utilizzare: `--aepUserLdap--_SL_Interest_WFH`.
Per **Descrizione**, utilizzare: `Interest in Work From Home`.

Fai clic su **Invia**.

![Pagine di destinazione](./images/lp4.png)

Fai clic su **Crea elenco iscrizioni** per creare un altro elenco.

![Pagine di destinazione](./images/lp5.png)

Per **Titolo**, utilizzare: `--aepUserLdap--_SL_Interest_Online_Gaming`.
Per **Descrizione**, utilizzare: `Interest in Online Gaming`.

Fai clic su **Invia**.

![Pagine di destinazione](./images/lp6.png)

Sono stati creati i 3 elenchi necessari.

![Pagine di destinazione](./images/lp7.png)

## Predefinito per pagina di destinazione 3.6.2.2

Per utilizzare le pagine di destinazione in Adobe Journey Optimizer, è necessario creare un predefinito.

Nel menu a sinistra, vai a **Amministrazione** > **Canali**, quindi seleziona **Predefiniti pagina di destinazione**.

Fai clic su **Crea predefinito per pagina di destinazione**.

![Pagine di destinazione](./images/lp8.png)

Per il campo **Nome**, utilizza: `--aepUserLdap-- - CitiSignal LP` e seleziona il sottodominio disponibile nella tua istanza.

>[!NOTE]
>
>Se nell’istanza non trovi un sottodominio, contatta il tuo amministratore AJO per aggiungerne uno.

Fai clic su **Invia**.

![Pagine di destinazione](./images/lp9.png)

Il predefinito per pagina di destinazione è stato creato.

![Pagine di destinazione](./images/lp10.png)

## Pagina di destinazione 3.6.2.3

Ora puoi creare la pagina di destinazione. Nel menu a sinistra, vai a **Gestione contenuto** > **Pagine di destinazione**.

Fai clic su **Crea pagina di destinazione**.

![Pagine di destinazione](./images/lp11.png)

Per il campo **Titolo**, utilizzare: `vangeluw - CitiSignal Interests`. Quindi, seleziona il **predefinito per pagina di destinazione** configurato nel passaggio precedente.

Fai clic su **Crea**.

![Pagine di destinazione](./images/lp12.png)

Dovresti vedere questo.

![Pagine di destinazione](./images/lp13.png)

Cambia il campo **Nome pagina** in `--aepUserLdap-- - CitiSignal Interests`.

Immettere il nome personalizzato in **Impostazioni di accesso**: `--aepUserLdap---citisignal-interests`.

Fare clic su **Apri Designer**.

![Pagine di destinazione](./images/lp14.png)

Seleziona **Progettazione da zero**.

![Pagine di destinazione](./images/lp15.png)

Dovresti vedere questo.

![Pagine di destinazione](./images/lp16.png)

Aggiungere un componente struttura **1:1 colonna** all&#39;area di lavoro.

![Pagine di destinazione](./images/lp17.png)

Aggiungi un componente di contenuto **Modulo** all&#39;area di lavoro.

![Pagine di destinazione](./images/lp18.png)

Aggiorna il campo **Etichetta** per **Casella di controllo 1** in `Keep me updated about CitiSignal's offering for Smart Home`.

Assicurati che la casella di controllo **Consenso se selezionata** sia abilitata e che sia selezionato **Elenco iscrizioni**.

Quindi fare clic su **Seleziona elenco iscrizioni**.

![Pagine di destinazione](./images/lp19.png)

Selezionare quindi l&#39;elenco `--aepUserLdap--_SL_Interest_in_Smart_Home` e fare clic su **Seleziona**.

![Pagine di destinazione](./images/lp20.png)

Fare clic su **+ Aggiungi campo** e quindi selezionare **Casella di controllo**.

![Pagine di destinazione](./images/lp21.png)

Dovresti vedere questo.

![Pagine di destinazione](./images/lp22.png)

Aggiorna il campo **Etichetta** per **Casella di controllo 2** in `Keep me updated about CitiSignal's offering for Work From Home`.

Assicurati che la casella di controllo **Consenso se selezionata** sia abilitata e che sia selezionato **Elenco iscrizioni**.

Quindi fare clic su **Seleziona elenco iscrizioni**.

![Pagine di destinazione](./images/lp23.png)

Selezionare quindi l&#39;elenco `--aepUserLdap--_SL_Interest_WFH` e fare clic su **Seleziona**.

![Pagine di destinazione](./images/lp24.png)

Fare clic su **+ Aggiungi campo** e quindi selezionare **Casella di controllo**.

![Pagine di destinazione](./images/lp25.png)

Dovresti vedere questo.

![Pagine di destinazione](./images/lp26.png)

Aggiorna il campo **Etichetta** per **Casella di controllo 3** in `Keep me updated about CitiSignal's offering for Online Gaming`.

Assicurati che la casella di controllo **Consenso se selezionata** sia abilitata e che sia selezionato **Elenco iscrizioni**.

Quindi fare clic su **Seleziona elenco iscrizioni**.

![Pagine di destinazione](./images/lp27.png)

Selezionare quindi l&#39;elenco `--aepUserLdap--_SL_Interest_Online_Gaming` e fare clic su **Seleziona**.

![Pagine di destinazione](./images/lp28.png)

Dovresti vedere questo.

![Pagine di destinazione](./images/lp29.png)

Vai al campo modulo **CALL TO ACTION**.

Aggiorna i campi seguenti:

- **Testo** - Etichetta pulsante: `Save`.
- **Azione di conferma**: selezionare **Testo di conferma**.
- **Testo di conferma**: utilizzare: `Thanks for updating your preferences!`
- **Azione errore**: selezionare **Testo errore**.
- **Testo errore**: utilizzare: `There was an error updating your preferences.`

Fai clic su **Salva**, quindi fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare alla schermata precedente.

![Pagine di destinazione](./images/lp30.png)

Fai clic su **Pubblica**.

![Pagine di destinazione](./images/lp31.png)

Fai di nuovo clic su **Pubblica**.

![Pagine di destinazione](./images/lp32.png)

La pagina di destinazione è ora pubblicata e può essere utilizzata in un’e-mail.

![Pagine di destinazione](./images/lp33.png)

## 3.6.2.4 Includi pagina di destinazione nell&#39;e-mail

Nell&#39;esercizio 3.1 hai creato un percorso denominato `--aepUserLdap-- - Registration Journey`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/published.png)

Ora devi aggiornare il messaggio e-mail in tale percorso per includere il collegamento alla pagina di destinazione.

Nel menu a sinistra, vai a **Percorsi** e fai clic per aprire il percorso `--aepUserLdap-- - Registration Journey`.

![Pagine di destinazione](./images/lp34.png)

Fai clic su **Altro...**, quindi seleziona **Crea una nuova versione**.

![Pagine di destinazione](./images/lp35.png)

Fai clic su **Crea una nuova versione**.

![Pagine di destinazione](./images/lp36.png)

Fare clic per selezionare l&#39;azione **E-mail**, quindi selezionare **Modifica contenuto**.

![Pagine di destinazione](./images/lp37.png)

Fai clic su **Modifica corpo dell&#39;e-mail**.

![Pagine di destinazione](./images/lp38.png)

Dovresti vedere qualcosa del genere. Aggiungere un nuovo componente struttura **1:1 colonna** all&#39;area di lavoro.

![Pagine di destinazione](./images/lp39.png)

Aggiungi un nuovo componente contenuto **Testo** nel componente struttura appena creato.

![Pagine di destinazione](./images/lp40.png)

Incolla il testo seguente nel componente di contenuto **Testo**.

`Would you like to hear from us about Smart Home news? Do you work from home and would you like to hear our tips? Or are you an avid online gamer and do you want to receive our game reviews? Click here to update your preferences and interests!`

Applicare lo stile al testo e selezionare la parola `here`. Fai clic sull&#39;icona **collegamento**.

Imposta **Tipo** del collegamento su **Pagina di destinazione** e imposta il campo **Destinazione** su **Vuota**.

Fai clic sull&#39;icona **modifica** per selezionare la pagina di destinazione da collegare.

![Pagine di destinazione](./images/lp41.png)

Selezionare la pagina di destinazione `--aepUserLdap-- - CitiSignal Interests`. Fai clic su **Seleziona**.

![Pagine di destinazione](./images/lp42.png)

Dovresti vedere questo. Fai clic su **Salva**.

![Pagine di destinazione](./images/lp43.png)

Fai clic sulla freccia nell’angolo in alto a sinistra per tornare alla schermata precedente.

![Pagine di destinazione](./images/lp44.png)

Fai clic sulla freccia nell’angolo in alto a sinistra per tornare nuovamente alla schermata precedente.

![Pagine di destinazione](./images/lp45.png)

Fai clic su **Salva**.

![Pagine di destinazione](./images/lp46.png)

Fai clic su **Pubblica**.

![Pagine di destinazione](./images/lp47.png)

Fai di nuovo clic su **Pubblica**.

![Pagine di destinazione](./images/lp48.png)

Le modifiche sono state pubblicate e puoi testare il percorso.

![Pagine di destinazione](./images/lp49.png)

## 3.6.2.5 Verifica percorso e pagina di destinazione

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo. Vai a **Accedi**

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Fare clic su **CREA UN ACCOUNT**. Compila i tuoi dettagli e fai clic su **Registra**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Ora verrai reindirizzato alla home page. Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

1 minuto dopo aver creato l’account, riceverai l’e-mail di creazione dell’account da Adobe Journey Optimizer.

Fai clic sul collegamento nell’e-mail per aggiornare le preferenze.

![Configurazione lancio](./images/email.png)

Dovresti quindi visualizzare il modulo creato. Abilita alcune caselle di controllo e fai clic su **Salva**.

![Configurazione lancio](./images/email1.png)

Dovresti quindi visualizzare un messaggio di conferma.

![Configurazione lancio](./images/email2.png)

## Reporting elenco iscrizioni 3.6.2.6

Per visualizzare i report disponibili sugli elenchi di abbonamento, vai a **Elenchi di abbonamento** nel menu a sinistra e fai clic su per aprire uno degli elenchi di abbonamento configurati in precedenza.

![Pagine di destinazione](./images/lp50.png)

Fai clic su **Report**.

![Pagine di destinazione](./images/lp51.png)

Dovresti quindi visualizzare la panoramica dell’elenco, con la quantità di persone che si sono iscritte o hanno annullato l’iscrizione.

![Pagine di destinazione](./images/lp52.png)

## Passaggi successivi

Vai a [3.6.3 AJO e GenStudio for Performance Marketing](./ex3.md)

Torna a [Adobe Journey Optimizer: gestione dei contenuti](./ajocontent.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}

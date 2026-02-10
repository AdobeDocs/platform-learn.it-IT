---
title: Utilizzare il modello Dynamic Media con Adobe Journey Optimizer
description: Utilizzare il modello Dynamic Media con Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: 0dd499cc-ec3b-42c3-9c08-6512ea5b9377
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 1.4.2 Utilizzare il modello Dynamic Media con Adobe Journey Optimizer

## 1.4.2.1 Crea la tua campagna in Adobe Journey Optimizer

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Ora creerai una campagna. A differenza del percorso basato sugli eventi dell’esercizio precedente, che si basa su eventi di esperienza o entrate o uscite di pubblico in arrivo per attivare un percorso per 1 cliente specifico, le campagne sono indirizzate a un intero pubblico una volta con contenuti univoci come newsletter, promozioni una tantum o informazioni generiche, oppure periodicamente con contenuti simili inviati regolarmente, come ad esempio campagne e promemoria di compleanno.

Nel menu, vai a **Campagne** e fai clic su **Crea campagna**.

![Journey Optimizer](./images/gsemail21.png)

Seleziona **Pianificato - Marketing** e fai clic su **Crea**.

![Journey Optimizer](./images/gsemail22.png)

Nella schermata di creazione della campagna, configura quanto segue:

- **Nome**: `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Fai clic su **Azioni**.

![Journey Optimizer](./images/gsemail23.png)

Fare clic su **+ Aggiungi azione** e quindi selezionare **E-mail**.

![Journey Optimizer](./images/gsemail24.png)

Quindi, selezionare una **configurazione e-mail** esistente e fare clic su **Modifica contenuto**.

![Journey Optimizer](./images/gsemail25.png)

Poi vedrai questo. Per la **riga oggetto**, utilizza:

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Fare clic su **Modifica contenuto**.

![Journey Optimizer](./images/gsemail26.png)

Seleziona **Progettazione da zero**.

![Journey Optimizer](./images/gsemail27.png)

Dovresti vedere questo.

![Journey Optimizer](./images/gsemail28.png)

Aggiungi 2x **1:1 colonna** all&#39;area di lavoro.

![Journey Optimizer](./images/gsemail29.png)

Vai a **Frammenti**, trascina il frammento **header** nella prima colonna 1:1, quindi trascina il frammento **footer** nella seconda colonna 1:1.

![Journey Optimizer](./images/gsemail30.png)

Aggiungere una nuova colonna 1:1 tra i due frammenti, quindi aggiungere una **Immagine** nella colonna 1:1. Quindi fare clic su **Sfoglia**.

![Journey Optimizer](./images/gsemail31.png)

Passa alla cartella in cui è stato memorizzato il modello Dynamic Media. Seleziona il modello Dynamic Media e fai clic su **Seleziona**.

![Journey Optimizer](./images/gsemail32.png)

Dovresti vedere questo. Anche tu. nota i **PARAMETRI** che ti consentono di modificare i parametri del modello dynamic media.

![Journey Optimizer](./images/gsemail33.png)

## 1.4.2.2 Personalizzare il modello Dynamic Media

Come descritto nell’esercizio precedente, ora AJO deve decidere dinamicamente quali dovrebbero essere i valori che diventano parte del modello Dynamic Media.

Proprio come nel passaggio **Anteprima** dell&#39;esercizio precedente, i campi **city_paris**, **city_dubai** e **city_ny** devono essere impostati su 1, il che significa che queste immagini saranno nascoste.

Per il campo **titolo**, fai clic sull&#39;icona di personalizzazione.

![Journey Optimizer](./images/gsemail34.png)

Sostituire il testo predefinito con questo: `Hi {{profile.person.name.firstName}}`. Fai clic su **Salva**.

![Journey Optimizer](./images/gsemail35.png)

Per il campo **body**, fai clic sull&#39;icona di personalizzazione.

![Journey Optimizer](./images/gsemail36.png)

Sostituire il testo predefinito con questo: `CitiSignal is coming to {{profile.homeAddress.city}}!`. Fai clic su **Salva**.

![Journey Optimizer](./images/gsemail37.png)

Verificare che il campo **`dynamic_city_hide`** sia impostato su 0. Fare clic sull&#39;icona di personalizzazione per il campo **`dynamic_city_image`**.

![Journey Optimizer](./images/gsemail38.png)

Sostituire il testo predefinito con questo: `--aepUserLdap--CitiSignalDM/citisignal-fiber-max-is-coming_citisignal-{{profile._experienceplatform.individualCharacteristics.fiber_rollout.closest_rollout_city}}-1`. Fai clic su **Salva**.

![Journey Optimizer](./images/gsemail39.png)

Dovresti vedere questo. Non viene più eseguito il rendering dell’immagine, il che è previsto perché le variabili dinamiche non sono disponibili nel contesto dell’editor e-mail.

Fai clic su **Salva**.

![Journey Optimizer](./images/gsemail40.png)

Verifica la configurazione, fai clic su **Simula contenuto**, quindi seleziona **Simula contenuto**.

![Journey Optimizer](./images/gsemail41.png)

Dovresti vedere qualcosa del genere. Se non hai profili di test disponibili, puoi aggiungerli da **Gestisci profili di test**.

Una volta disponibili profili di test che contengono i dati necessari per testare questo caso d’uso, puoi passare da un profilo all’altro per vedere le modifiche apportate in modo dinamico.

Ecco un profilo collegato alla città rollout di New York.

![Journey Optimizer](./images/gsemail42.png)

Ecco un profilo collegato alla città di rollout Parigi.

![Journey Optimizer](./images/gsemail43.png)

Ecco un profilo collegato alla città rollout Dubai.

Fai clic su **Chiudi**.

![Journey Optimizer](./images/gsemail44.png)

Hai terminato questo esercizio. Non è necessario pubblicare la campagna e-mail.

## Passaggi successivi

Torna a [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
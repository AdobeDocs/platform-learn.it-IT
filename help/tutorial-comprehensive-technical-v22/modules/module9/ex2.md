---
title: 'offer decisioning: configurare le offerte e l’ID decisione'
description: 'offer decisioning: configurare le offerte e l’ID decisione'
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 4b2c2753-8b7e-496e-9fb5-3ccb9f6a10ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---

# 9.2 Configurare le offerte e le decisioni

## 9.2.1 Creare offerte personalizzate

In questo esercizio, ne creerai quattro **Offerte personalizzate**. Di seguito sono riportati i dettagli da tenere in considerazione durante la creazione di tali offerte:

| Nome | Date Range | Collegamento immagine per e-mail | Collegamento immagine per web | Testo | Priorità | Ammissibilità | Lingua |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--demoProfileLdap-- - Nadia Elements Shell` | oggi - 1 mese dopo | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | all - Clienti femminili | Inglese (Stati Uniti) |
| `--demoProfileLdap-- - Radiant Tee` | oggi - 1 mese dopo | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | all - Clienti femminili | Inglese (Stati Uniti) |
| `--demoProfileLdap-- - Zeppelin Yoga Pant` | oggi - 1 mese dopo | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | all - Clienti maschili | Inglese (Stati Uniti) |
| `--demoProfileLdap-- - Proteus Fitness Jackshirt` | oggi - 1 mese dopo | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | all - Clienti maschili | Inglese (Stati Uniti) |

{style=&quot;table-layout:auto&quot;}

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Nel menu a sinistra, fai clic su **Offerte** e poi vai a **Offerte**. Fai clic su **+ Crea offerta**.

![Regola decisionale](./images/offers1.png)

Vedrete questa finestra a comparsa. Seleziona **Offerta personalizzata** e fai clic su **Successivo**.

![Regola decisionale](./images/offers2.png)

Ora sei sul **Dettagli** visualizza.

![Regola decisionale](./images/offers3.png)

In questo caso, devi configurare l’offerta `--demoProfileLdap-- - Nadia Elements Shell`. Utilizza le informazioni nella tabella precedente per compilare i campi. In questo esempio, il nome dell’offerta personalizzata è **vangeluw - Nadia Elements Shell**. Inoltre, imposta la **Data e ora di inizio** a ieri e imposta il **Data e ora di fine** a una data tra un mese.

Una volta fatto, dovreste avere questo. Fai clic su **Avanti**.

![Regola decisionale](./images/offers4.png)

Ora devi creare **Rappresentazioni**. Le rappresentazioni sono una combinazione di un **Posizionamento** e una risorsa reale.

Per **Rappresentazione 1**, seleziona:

- Canale: Web
- Posizionamento: Web - Immagine
- Contenuto: URL
- Posizione pubblica: copia l’URL dalla colonna **Collegamento immagine per web** nella tabella precedente

![Regola decisionale](./images/addcontent1.png)

In alternativa, è possibile selezionare **Libreria risorse** per il contenuto, quindi fai clic su **Sfoglia**.

![Regola decisionale](./images/addcontent2.png)

Verrà visualizzata una finestra a comparsa della libreria Risorse, vai alla cartella . **enablement-assets** e seleziona il file di immagine **nadia-web.png**. Quindi, fai clic su **Seleziona**.

![Regola decisionale](./images/addcontent3.png)

Vedrai questo:

![Regola decisionale](./images/addcontentrep20.png)

Fai clic su **+ Aggiungi rappresentanza**.

![Regola decisionale](./images/addrep.png)

Per **Rappresentazione 2**, seleziona:

- Canale: E-mail
- Posizionamento: E-mail - Immagine
- Contenuto: URL
- Posizione pubblica: copia l’URL dalla colonna **Collegamento immagine per e-mail** nella tabella precedente

![Regola decisionale](./images/addcontentrep21.png)

In alternativa, è possibile selezionare **Libreria risorse** per il contenuto, quindi fai clic su **Sfoglia**.

![Regola decisionale](./images/addcontent2b.png)

Verrà visualizzata una finestra a comparsa della libreria Risorse, vai alla cartella . **enablement-assets** e seleziona il file di immagine **nadia-email.png**. Quindi, fai clic su **Seleziona**.

![Regola decisionale](./images/addcontent3b.png)

Vedrai questo:

![Regola decisionale](./images/addcontentrep20b.png)

Quindi, fai clic su **+ Aggiungi rappresentazione**.

![Regola decisionale](./images/addrep.png)

Per **Rappresentazione 3**, seleziona:

- Canale: Non digitale
- Posizionamento: Non digitale - Testo

Quindi, devi aggiungere del contenuto. In questo caso, significa aggiungere il testo da utilizzare come invito all’azione.

Fai clic su **Aggiungi contenuto**.

![Regola decisionale](./images/addcontentrep31.png)

Vedrete questa finestra a comparsa.

![Regola decisionale](./images/addcontent3text.png)

Seleziona **Testo personalizzato** e compilare i seguenti campi:

Guarda il **Testo** campo della tabella precedente e inserisci il testo qui, in questo caso: `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`.

Noterai inoltre che puoi selezionare qualsiasi attributo di profilo e includerlo come campo dinamico nel testo dell’offerta. In questo esempio, il campo `{{ profile.person.name.firstName }}` farà in modo che il nome del cliente che riceverà l’offerta venga incluso nel testo dell’offerta.

Vedrete questo. Fai clic su **Salva**.

![Regola decisionale](./images/addcontentrep3text.png)

Ora avete questo. Fai clic su **Avanti**.

![Regola decisionale](./images/addcontentrep3textdone.png)

Vedrai questo:

![Regola decisionale](./images/constraints.png)

Seleziona **Per regola decisionale definita** e fai clic su **+** icona per aggiungere la regola **all - Clienti femminili**.

![Regola decisionale](./images/constraints1.png)

Vedrete questo. Compila il **Priorità** come indicato nella tabella precedente. Fai clic su **Avanti**.

![Regola decisionale](./images/constraints2.png)

Viene visualizzata una panoramica del nuovo **Offerta personalizzata**.

![Regola decisionale](./images/offeroverview.png)

Infine, fai clic su **Salva e approva**.

![Regola decisionale](./images/saveapprove.png)

Potrai quindi vedere l’offerta personalizzata appena creata diventare disponibile nella Panoramica delle offerte:

![Regola decisionale](./images/offeroverview1.png)

È ora necessario ripetere i passaggi precedenti per creare le altre tre offerte personalizzate per i prodotti Tee radiante, Zeppelin Yoga Pant e Proteus Fitness Jackshirt.

Al termine, il tuo **Panoramica dell’offerta** schermo per **Offerte personalizzate** dovrebbe mostrare tutte le tue offerte.

![Offerte finali](./images/finaloffers.png)

## 9.2.2 Creare l&#39;offerta di fallback

Dopo aver creato quattro offerte personalizzate, ora devi configurare un **Offerta di fallback**.

Assicurati di essere nel **Offerte** visualizza:

![Offerte finali](./images/finaloffers.png)

Fai clic su **+ Crea offerta**.

![Regola decisionale](./images/createoffer.png)

Vedrete questa finestra a comparsa. Seleziona **Offerta di fallback** e fai clic su **Successivo**.

![Regola decisionale](./images/foffers2.png)

Vedrai questo:

![Regola decisionale](./images/foffers3.png)

Immetti questo nome per la tua offerta di fallback: `--demoProfileLdap-- - Luma Fallback Offer`. Fai clic su **Avanti**.

![Regola decisionale](./images/foffers4.png)

Ora devi creare **Rappresentazioni**. Le rappresentazioni sono una combinazione di un **Posizionamento** e una risorsa reale.

Per **Rappresentazione 1**, seleziona:

- Canale: Web
- Posizionamento: Web - Immagine
- Contenuto: URL
- Posizione pubblica: `https://bit.ly/3nBOt9h`

![Regola decisionale](./images/addcontent1fb.png)

In alternativa, è possibile selezionare **Libreria risorse** per il contenuto, quindi fai clic su **Sfoglia**.

![Regola decisionale](./images/addcontent2fb.png)

Verrà visualizzata una finestra a comparsa della libreria Risorse, vai alla cartella . **enablement-assets** e seleziona il file di immagine **spriteyogastraps-web.png**. Quindi, fai clic su **Seleziona**.

![Regola decisionale](./images/addcontent3fb.png)

Vedrai questo:

![Regola decisionale](./images/addcontentrep20fb.png)

Per **Rappresentazione 2**, seleziona:

- Canale: E-mail
- Posizionamento: E-mail - Immagine
- Contenuto: URL
- Posizione pubblica: `https://bit.ly/3nF4qvE`

![Regola decisionale](./images/addcontentrep21fb.png)

In alternativa, è possibile selezionare **Libreria risorse** per il contenuto, quindi fai clic su **Sfoglia**.

![Regola decisionale](./images/addcontent2bfb.png)

Verrà visualizzata una finestra a comparsa della libreria Risorse, vai alla cartella . **enablement-assets** e seleziona il file di immagine **spriteyogastraps-email.png**. Quindi, fai clic su **Seleziona**.

![Regola decisionale](./images/addcontent3bfb.png)

Vedrai questo:

![Regola decisionale](./images/addcontentrep20bfb.png)

Quindi, fai clic su **+ Aggiungi rappresentazione**.

![Regola decisionale](./images/addrep.png)

Per **Rappresentazione 3**, seleziona:

- Canale: Non digitale
- Posizionamento: Non digitale - Testo

Quindi, devi aggiungere del contenuto. In questo caso, significa aggiungere il collegamento immagine.

Fai clic su **Aggiungi contenuto**.

![Regola decisionale](./images/addcontentrep21text.png)

Vedrete questa finestra a comparsa.

![Regola decisionale](./images/addcontent2text.png)

Seleziona **Testo personalizzato** e compilare i seguenti campi:

Inserisci il testo `{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!` e fai clic su **Salva**.

![Regola decisionale](./images/faddcontent3text.png)

Vedrete questo. Fai clic su **Avanti**.

![Regola decisionale](./images/faddcontentrep3.png)

Viene visualizzata una panoramica del nuovo **Offerta di fallback**. Fai clic su **Fine**.

![Regola decisionale](./images/fofferoverview.png)

Infine, fai clic su **Salva e approva**.

![Regola decisionale](./images/saveapprovefb.png)

Nel tuo **Panoramica dell’offerta** a questo punto verrà visualizzato questo:

![Offerte finali](./images/ffinaloffers.png)

## 9.2.3 Creare la raccolta

Una raccolta viene utilizzata per **filter** crea un sottoinsieme di offerte dall’elenco delle offerte personalizzate e utilizzalo come parte di una decisione per accelerare il processo decisionale.

Vai a **Raccolte**. Fai clic su **+ Crea raccolta**.

![Regola decisionale](./images/collections.png)

Poi vedrete questa finestra a comparsa. Configura la raccolta in questo modo. Fai clic su **Avanti**.

- Nome raccolta: use `--demoProfileLdap-- - Luma Collection`
- Seleziona **Creare una raccolta statica**.

![Regola decisionale](./images/createcollectionpopup1.png)

Nella schermata successiva, seleziona i quattro **Offerte personalizzate** creato nell&#39;esercizio precedente. Fai clic su **Salva**.

![Regola decisionale](./images/createcollectionpopup2.png)

Ora verrà visualizzato questo:

![Regola decisionale](./images/colldone.png)

## 9.2.4 Crea la tua decisione

Una decisione combina Posizionamenti, una Raccolta di Offerte personalizzate e un’Offerta di fallback da utilizzare in ultima analisi dal motore di Offer decisioning per trovare l’offerta migliore per un profilo specifico, in base a ciascuna delle singole caratteristiche di offerta personalizzata come priorità, vincolo di idoneità e limite totale/utente.

Per configurare le **Decisione**, vai a **Decisioni**. Fai clic su **+ Crea attività**.

![Regola decisionale](./images/activitydd.png)

Vedrai questo:

![Regola decisionale](./images/activity1.png)

Compila i campi come questo. Fai clic su **Avanti**.

- Nome: `--demoProfileLdap-- - Luma Decision`
- Data e ora di inizio: ieri
- Data e ora di fine: oggi + 1 mese

![Regola decisionale](./images/activity2.png)

Nella schermata successiva, è necessario aggiungere posizionamenti negli ambiti decisionali. Sarà necessario creare ambiti decisionali per i posizionamenti **Web - Immagine**, **E-mail - Immagine** e **Non digitale - Testo**.

![Regola decisionale](./images/addplacements.png)

In primo luogo, crea il campo di applicazione della decisione per **Non digitale - Testo** selezionando tale posizione nel menu a discesa . Quindi, fai clic sul pulsante **Aggiungi** per aggiungere criteri di valutazione.

![Regola decisionale](./images/activity3.png)

Seleziona la raccolta `--demoProfileLdap-- - Luma Collection` e fai clic su **Aggiungi**.

![Regola decisionale](./images/activity4text.png)

Vedrete questo. Fai clic sul pulsante **-** per aggiungere un nuovo ambito decisionale.

![Regola decisionale](./images/activity5text.png)

Selezionare il posizionamento **Web - Immagine** e aggiungi la tua raccolta `--demoProfileLdap-- - Luma Collection` in base ai criteri di valutazione. Quindi, fai clic sul pulsante **+** per aggiungere un nuovo ambito decisionale.

![Regola decisionale](./images/activity6text.png)

Selezionare il posizionamento **E-mail - Immagine** e aggiungi la tua raccolta `--demoProfileLdap-- - Luma Collection` in base ai criteri di valutazione. Quindi, fai clic su **Successivo**.

![Regola decisionale](./images/activity4.png)

Ora devi selezionare il tuo **Offerta di fallback**, denominato `--demoProfileLdap-- - Luma Fallback Offer`. Fai clic su **Avanti**.

![Regola decisionale](./images/activity10.png)

Rivedi la tua decisione. Fai clic su **Fine**.

![Regola decisionale](./images/activity11.png)

Nella finestra a comparsa, fai clic su **Salva e attiva**.

![Regola decisionale](./images/activity12.png)

Infine, vedrai la tua decisione nella panoramica:

![Regola decisionale](./images/activity13.png)

La decisione è stata configurata correttamente. La tua decisione è ora live e può essere utilizzata per fornire offerte ottimizzate e personalizzate ai tuoi clienti in tempo reale.

Passaggio successivo: [9.3 Prepara ad Offer decisioning la proprietà del client di raccolta dati e la configurazione dell&#39;SDK per web](./ex3.md)

[Torna al modulo 9](./offer-decisioning.md)

[Torna a tutti i moduli](./../../overview.md)

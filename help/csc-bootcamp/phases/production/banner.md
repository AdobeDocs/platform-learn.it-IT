---
title: CSC Bootcamp - Creare il banner home page del prodotto
description: CSC Bootcamp - Creare il banner home page del prodotto
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Creare il banner della homepage del prodotto

## Produzione del banner

L’automazione dei contenuti porta la potenza di Adobe Creative Cloud a Experience Manager Assets, offrendo agli addetti al marketing la possibilità di automatizzare la produzione delle risorse su larga scala, velocizzando notevolmente la creazione delle varianti. Usiamo queste funzionalità per generare un banner da utilizzare sulla homepage!

- Vai all&#39;autore AEM su [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e accedi con le credenziali fornite.

- Dalla home page, passa a Strumenti \> Risorse \> Profili elaborazione.

![Strumenti > Risorse > Profili di elaborazione](./images/prod-processing-profiles.png)

- Nell’interfaccia di vengono visualizzati tutti i profili di elaborazione esistenti. Questi possono essere utilizzati per abilitare determinate automazioni.

![elenco dei profili di elaborazione](./images/prod-profile-list.png)


- I seguenti sono di tuo interesse:
   - Banner Adobe scuro: crea un banner Adobe con sovrapposizione scura, in base alla risorsa selezionata
      ![banner scuro](./images/prod-banner-dark.jpg)
   - Luce banner Adobe: crea un banner Adobe con una sovrapposizione leggera, in base alla risorsa selezionata
      ![banner luminoso](./images/prod-banner-light.jpg)
   - Verde banner Adobe: crea un banner Adobe con una sovrapposizione verde, in base alla risorsa selezionata
      ![banner verde](./images/prod-banner-green.jpg)

- Dopo aver scelto il tipo di banner che si desidera creare, selezionare il profilo di elaborazione, quindi selezionare &quot;Applica profilo alle cartelle&quot;.

![applica profilo alla cartella](./images/prod-apply-profile.png)

- Nella schermata successiva, individua la cartella del team in AEM Assets. Quindi, dall&#39;alto a sinistra, seleziona il pulsante &quot;Crea&quot; per creare una nuova cartella e assegnargli un nome significativo, ad esempio &quot;Crea banner scuro&quot;.

![crea cartella](./images/prod-create-profile-folder.png)

![creare i dettagli della cartella](./images/prod-profile-folder-details.png)

- Dopo aver creato la cartella, selezionare la casella accanto al suo nome, quindi fare clic sul pulsante &quot;Applica&quot; in alto a destra.

![applica alla cartella creata](./images/prod-select-profile-folder.png)

Ora che abbiamo fatto la configurazione necessaria, generiamo il nostro banner.

- Fai clic sul Logo AEM nell’angolo in alto a sinistra per aprire la navigazione, quindi vai a Navigazione \> Risorse \> File.

![home screen di aem](./images/prod-select-assets.png)
![schermata risorse aem](./images/prod-select-assets-2.png)

- Individua la cartella &quot;Risorse Adobe generate&quot; e aprila facendo clic sulla scheda . Qui vengono visualizzati i banner generati.

![risorse adobike generate](./images/prod-generated-banners.png)

- Apri una nuova scheda e passa di nuovo a AEM Assets. Quindi, accedi alla cartella a cui è stato applicato il profilo di elaborazione.

- Nella cartella , carica l’immagine per la quale vuoi creare un banner trascinandola e rilasciandola sul browser oppure facendo clic su Crea file nell’angolo in alto a destra dell’interfaccia.

![caricare tramite trascinamento n rilascio](./images/prod-drag-drop-banner.png)

![caricare utilizzando crea file](./images/prod-create-file.png)


- Attendi un minuto per l’elaborazione della risorsa, quindi ricarica lo schermo. Se trovi la risorsa nello stato &quot;Nuovo&quot;, sai che è stata elaborata.

![risorsa in nuovo stato](./images/prod-asset-processed.png)

- Torna alla scheda precedente e ricarica la schermata anche qui. Dovresti notare una nuova risorsa nello stato &quot;Nuovo&quot;. Questo è il nostro banner generato, tutto dal DAM! Non la vedi ancora? Attendi un altro minuto, quindi ricarica lo schermo.

![banner generato](./images/prod-new-banner.png)

>[!NOTE]
>
> Non sei soddisfatto del risultato? Puoi applicare un altro profilo di elaborazione alla cartella e ricaricare la risorsa per generare un banner diverso (o ovviamente caricare un’altra risorsa). Durante il ricaricamento, il sistema ti chiederà cosa vuoi fare con la risorsa esistente, seleziona &quot;Sostituisci&quot;.
> ![sostituisci esistente](./images/prod-replace-asset.png)

Ora disponiamo del banner generato che possiamo utilizzare in seguito durante la distribuzione della campagna. Assicurati di pubblicare il banner selezionandolo, quindi cliccando sul pulsante &quot;Pubblicazione rapida&quot; sulla barra multifunzione.

![pubblicare risorsa](./images/prod-publish-banner.png)

## Follow-up in Workfront

Se hai bisogno di un processo formale e verificabile di revisione e approvazione delle tue risorse, Workfront è il posto giusto per essere.

>[!NOTE]
>
> Anche se lo menzioniamo esplicitamente qui, è l&#39;intenzione di aggiornare le attività in Workfront dopo averle completate. Devi sempre cercare un flusso Crea > Rivedi > Approva .

- Torniamo al nostro progetto ed espandiamo il pannello &#39;Go/No Go Banner Review&#39; per aprire l&#39;attività facendo clic su di esso:

![banner go/no-go](./images/banner-gonogo.png)

- Fai clic sulla sezione documenti dell&#39;attività (colonna a sinistra), quindi fai clic sulla cartella collegata AEM Assets &quot;Finale&quot;. Seleziona la risorsa facendo clic sulla relativa zona e fai clic su &quot;Crea bozza&quot;. Una prova è la capacità di controllare il contenuto, ad esempio immagine, testo, video, sito web, ecc., in modo strutturato e collaborativo, dove vengono raccolti commenti, correzioni, modifiche dei soggetti interessati, versioni e risultati possono essere confrontati e approvati definitivamente con un solo clic.

![crea bozza](./images/wf-create-proof.png)

- Poiché vogliamo un processo di approvazione elaborato, seleziona &quot;Proof avanzato&quot;.

![prova avanzata](./images/wf-advanced-proof.png)

>[!NOTE]
>
> Decideremo manualmente chi esaminerà e/o approverà le nostre prove in questo bootcamp. Nella maggior parte dei casi d’uso reali, utilizzeremmo un modello predefinito di flusso di approvazione già definito per ciascun tipo di prova.

- Per impostazione predefinita, siamo in un tipo di flusso di lavoro &quot;base&quot; e sceglieremo il tuo Workfront Bootcamp Specialist come revisore e approvatore. Digita il nome del tuo Specialist Workfront Bootcamp dove c&#39;è scritto &#39;Digita il nome del contatto o l&#39;indirizzo e-mail per aggiungere un destinatario:

![assegnare una bozza](./images/wf-proof-assign.png)

![assegnare una bozza](./images/wf-assign-proof-2.png)

- Imposta come &#39;Revisore e approvatore&#39;:

![revisore e approvatore](./images/wf-review-approve.png)

- Fai clic su &quot;Crea prova&quot;. Workfront impiegherà alcuni minuti per generare la bozza:

![prova generatrice](./images/wf-generating-proof.png)

- I Workfront Specialist avranno ricevuto una nuova notifica per informarli di disporre di una prova per la revisione e/o l&#39;approvazione:

![compito anteriore](./images/wf-proof-task.png)

- Dopo aver fatto clic sulla notifica, verranno mostrate le tue prove e saranno in grado di commentare e/o approvare questa bozza.

   - Possono fare clic su &quot;Aggiungi commento&quot; nella parte superiore dello schermo se hanno osservazioni:

   ![Aggiungi commento](./images/wf-proof-add-comment.png)

   - Potranno quindi non solo aggiungere commenti, ma anche utilizzare la piccola barra degli strumenti puntatori per definire chiaramente quale area deve essere modificata.

   ![Commento punto](./images/wf-proof-comment.png)

   - Aggiungendo il commento, è possibile comunicare che è necessario eseguire un ulteriore lavoro su una nuova versione della bozza. Aggiorna la scheda Workfront e avrai una nuova notifica che ti informa esattamente di questo. Una volta che sai quali modifiche devi apportare, apporta le modifiche in AEM e quindi vieni a caricare la nuova versione qui:

   ![carica nuova versione](./images/wf-upload-version.png)

   - Seleziona la risorsa aggiornata (se non sono necessarie modifiche nello scenario di bootcamp, carica di nuovo la stessa risorsa) e fai clic su &quot;Collega&quot;:

   ![risorsa di collegamento](./images/wf-link-new-asset.png)

   - Quindi, fai clic su &quot;crea bozza&quot; sul lato destro.

   ![crea bozza](./images/create-new-proof.png)

   - Una volta generata la prova (che può richiedere alcuni minuti), il tuo Workfront Specialist riceverà una notifica e sarà in grado di rivedere e, si spera, approvare questa nuova versione.  Ad esempio, utilizzando il pulsante di confronto delle prove, è possibile vedere un confronto affiancato tra V1 e V2 e tutti i commenti effettuati.

   ![confronto delle prove](./images/wf-proof-compare.png)

   ![decidere](./images/make-decision-proof.png)

   ![approvato](./images/approved.png)

Ora abbiamo un&#39;approvazione formale per l&#39;uso del nostro banner. È facile seguire dove siamo nel processo, e gli aggiornamenti che si fanno attivare automaticamente le notifiche, in modo da poter lavorare nel modo più efficiente possibile.

Passaggio successivo: [Fase 2 - Produzione: Crea annuncio social media](./social.md)

[Torna alla fase 1 - Pianificazione: Altri lavori preliminari](../planning/prework.md)

[Torna a tutti i moduli](../../overview.md)

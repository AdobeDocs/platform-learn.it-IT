---
title: CSC Bootcamp - Altri lavori preliminari
description: CSC Bootcamp - Altri lavori preliminari
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Altri lavori preliminari

## Selezionare Brand Assets

Come descritto nella sezione dedicata ai contenuti creativi, sono necessarie alcune risorse per lanciare in modo efficace la nostra campagna. Queste risorse del marchio verranno aggiunte alla campagna in Workfront in modo da potervi accedere centralmente.

- Espandi l’attività 1, &quot;ATTIVITÀ INIZIALI&quot;, quindi apri l’attività &quot;Seleziona 5 risorse del marchio (fronte, retro, ...)&quot; facendo clic su di essa.

![apri attività risorse](./images/wf-open-assets-task.png)

- Fai clic su &quot;Documenti&quot; e poi su &quot;Aggiungi nuovo:

![aggiungi documento](./images/wf-add-new-doc.png)

- Seleziona &quot;Da experience-manager&quot;; questo ci consentirà di scegliere le risorse del brand già disponibili in AEM Assets:

![da experience-manager](./images/wf-from-aem.png)

- Una volta visualizzata la gerarchia delle cartelle AEM, passa al seguente percorso: experience-manager > Risorse Adobe > Spari in bicicletta Seleziona 5 risorse e fai clic su &quot;Link&quot;.

![risorse selezionate](./images/selected-assets.png)

- Ora disponiamo delle risorse del nostro Brand per il nostro compito. Questo significa che possiamo impostare l&#39;attività 2 come completa al 100%:

![operazione completa](./images/wf-task-2-complete.png)


## Demo di Adobe Commerce

Adobe Commerce è uno dei molti prodotti in Adobe Experience Cloud che può aiutarti a fornire ai tuoi clienti le migliori esperienze digitali. Tuttavia, c&#39;era semplicemente troppo poco tempo per fare tutto insieme durante il bootcamp.

Questo video ti permette di conoscere meglio Adobe Commerce e mostra il prodotto che abbiamo creato per l’utilizzo durante il bootcamp. In uno scenario reale, puoi caricare le risorse del marchio selezionate in precedenza in Adobe Commerce nella configurazione del prodotto.

>[!VIDEO](https://video.tv.adobe.com/v/3418945?quality=12&learn=on)

Una volta completata questa attività, puoi contrassegnare l’attività 3 come completa al 100% in Workfront.

## Le campagne flessibili sono un prerequisito

Durante la revisione del nostro piano di lavoro, abbiamo notato un piccolo problema: il nostro Product Manager (il Richiedente) ha messo un aggiornamento che ha dimenticato di richiedere un &#39;Product Homepage Banner&#39;.  Lo aggiungeremo al nostro piano di progetto.

- Vai all&#39;elenco Attività e aggiungi l&#39;attività &quot;Crea banner per la homepage del prodotto&quot; appena sotto l&#39;attività 4 &quot;PRODUZIONE&quot;. A questo scopo, seleziona l’attività &quot;Prepara contenuto app mobile&quot; e fai clic sull’icona &quot;aggiungi attività sopra&quot;:

![aggiungi attività sopra](./images/wf-add-task-above.png)

- Assegna all’attività aggiunta un nome significativo, ad esempio &quot;Crea banner per la home page del prodotto&quot;.

![crea attività](./images/wf-create-banner.png)

- Ora che abbiamo creato l&#39;attività, aggiungiamo un po&#39; di contenuto. Fai clic sui tre punti a destra del titolo del progetto e seleziona &quot;Allega modello&quot;:

![allega modello](./images/wf-attach-template.png)

- Seleziona &#39;Crea banner home del prodotto&#39; e fai clic su &#39;Personalizza e allega&#39;:

![crea banner home page del prodotto](./images/wf-homepage-banner.png)

- Nella schermata di personalizzazione, assicurati di fare riferimento all’attività &quot;Crea banner pagina iniziale del prodotto&quot; come elemento padre:

![aggiungi padre](./images/wf-create-banner-parent.png)

- Infine, accertati di contrassegnare l’attività padre &quot;Crea home page prodotto&quot; con un predecessore dell’attività 3 in quanto non è possibile avviare alcuna produzione finché il prodotto non viene creato in Adobe Commerce:

![aggiungi il predecessore corretto](./images/wf-predecessor.png)

Ora abbiamo una campagna completa e pianificata, il che significa che possiamo iniziare con la produzione e la consegna della nostra campagna!


Passaggio successivo: [Fase 2 - Produzione: Creare il banner della homepage del prodotto](../production/banner.md)

[Torna alla fase 1 - Pianificazione: Pianificazione](./planning.md)

[Torna a tutti i moduli](../../overview.md)
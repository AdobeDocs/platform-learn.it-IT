---
title: CSC Bootcamp - Altre attività preliminari
description: CSC Bootcamp - Altre attività preliminari
doc-type: multipage-overview
exl-id: 76546141-68d5-4f09-b44a-e06cc08bbaa7
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Altri lavori preliminari

## Seleziona Brand Assets

Come descritto nel documento creativo, ci sono alcune risorse che saranno necessarie per lanciare la nostra campagna in modo efficace. Queste risorse dei marchi verranno aggiunte alla campagna in Workfront, in modo che possiamo accedervi da una posizione centrale.

- Espandi l’attività 1, &quot;INITIAL TASKS&quot; (ATTIVITÀ INIZIALI), quindi apri l’attività &quot;Select 5 brand assets (front, back, ...)&quot; facendo clic su di essa.

![apri attività risorse](./images/wf-open-assets-task.png)

- Fai clic su &quot;Documenti&quot; e quindi su &quot;Aggiungi nuovo:

![aggiungi documento](./images/wf-add-new-doc.png)

- Seleziona &quot;Da experience-manager&quot; per scegliere le risorse del brand già disponibili su AEM Assets:

![da experience-manager](./images/wf-from-aem.png)

- Una volta visualizzata la gerarchia delle cartelle di AEM, passa al seguente percorso: experience-manager > Adobike Assets > Riprese bici Seleziona 5 risorse e quindi fai clic su &quot;Collega&quot;.

![risorse selezionate](./images/selected-assets.png)

- Ora il nostro compito è affidato a Brand Assets. Ciò significa che è possibile impostare l&#39;attività 2 come completata al 100%:

![attività completata](./images/wf-task-2-complete.png)


## Demo di Adobe Commerce

Adobe Commerce è uno dei tanti prodotti di Adobe Experience Cloud che possono aiutarti a fornire ai tuoi clienti le migliori esperienze digitali. Tuttavia, c&#39;era semplicemente troppo poco tempo per fare tutto insieme durante il bootcamp.

Questo video ti fa conoscere Adobe Commerce e mostra il prodotto che abbiamo creato per utilizzare durante il bootcamp. In uno scenario reale, puoi caricare le risorse del brand selezionate in precedenza in Adobe Commerce nella configurazione del prodotto.

>[!VIDEO](https://video.tv.adobe.com/v/3418945?quality=12&learn=on&enablevpops)

Una volta completata questa attività, in Workfront puoi contrassegnarla come completata al 100%.

## Le campagne flessibili sono un prerequisito

Durante la revisione del nostro piano di lavoro, abbiamo notato un piccolo problema: il nostro Product Manager (il richiedente) ha inserito un aggiornamento che ha dimenticato di richiedere per un &quot;banner della homepage del prodotto&quot;.  Questo verrà aggiunto al piano del progetto.

- Vai all’elenco Attività e aggiungi l’attività &quot;Crea banner pagina iniziale prodotto&quot; appena sotto l’attività 4 &quot;PRODUZIONE&quot;. A questo scopo, seleziona l’attività &quot;Prepara contenuto app mobile&quot; e fai clic sull’icona &quot;Aggiungi attività in alto&quot;:

![aggiungi attività in alto](./images/wf-add-task-above.png)

- Assegna un nome significativo all’attività aggiunta, ad esempio &quot;Crea banner della home page del prodotto&quot;.

![crea attività](./images/wf-create-banner.png)

- Dopo aver creato l’attività, aggiungiamo del contenuto. Fai clic sui tre punti a destra del titolo del progetto e seleziona Allega modello:

![allega modello](./images/wf-attach-template.png)

- Seleziona &quot;Crea banner home page prodotto&quot; e fai clic su &quot;Personalizza e allega&quot;:

![crea banner home page prodotto](./images/wf-homepage-banner.png)

- Nella schermata di personalizzazione, accertati di indicare l’attività &quot;Crea banner pagina iniziale prodotto&quot; come elemento principale:

![aggiungi elemento padre](./images/wf-create-banner-parent.png)

- Infine, assicurati di contrassegnare l’attività principale &quot;Crea home page del prodotto&quot; con un predecessore dell’attività 3, in quanto non è possibile avviare alcuna produzione fino a quando il prodotto non viene creato in Adobe Commerce:

![aggiungi il predecessore corretto](./images/wf-predecessor.png)

Ora abbiamo una campagna completa e pianificata, il che significa che possiamo iniziare con la produzione e la consegna della nostra campagna!


Passaggio successivo: [Fase 2 - Produzione: crea banner home page prodotto](../production/banner.md)

[Torna alla Fase 1 - Pianificazione: Pianificazione](./planning.md)

[Torna a tutti i moduli](../../overview.md)

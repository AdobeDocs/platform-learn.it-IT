---
title: 'Offer decisioning: verifica la decisione utilizzando il sito web demo'
description: Verifica la tua decisione utilizzando il sito web demo
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 3.3.4 Combinare Adobe Target e Offer Decisioning

## 3.3.4.1 Raccogliere il collegamento condivisibile del progetto demo

Per caricare il progetto demo del sito web in Adobe Target, devi innanzitutto raccogliere un collegamento speciale che consenta ad Adobe Target di caricare il progetto demo del sito web.

Per eseguire questa operazione, vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![RTCDP](./images/builder1.png)

Ora vedrai questo. Fai clic su **Condividi**.

![RTCDP](./images/builder2.png)

Fare clic su **Genera collegamento** e quindi copiare il collegamento negli Appunti.

![RTCDP](./images/builder3.png)

Vai a [https://bitly.com](https://bitly.com), incolla il collegamento copiato e fai clic su **Accorcia**. Verrà visualizzato un collegamento abbreviato, simile al seguente: `https://bit.ly/3JxN7aG`. Sarà necessario il collegamento nell&#39;esercizio successivo.

![RTCDP](./images/builder4.png)

## 3.3.4.2 Raccolta

Passare alla home page di Adobe Experience Cloud da [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Fai clic su **Target**.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/excl.png)

Nella home page di **Adobe Target** verranno visualizzate tutte le attività esistenti.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatov.png)

Fai clic su **+ Crea attività** per creare una nuova attività.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatcr.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Ora seleziona **Visivo** e incolla il collegamento abbreviato nel campo **Inserisci l&#39;URL attività**. Fai clic su **Avanti**.

![RTCDP](./images/exclatcrxt1.png)

Vedrai quindi il tuo progetto demo del sito web caricato nel Compositore esperienza visivo.

![RTCDP](./images/vec1.png)

Passa alla modalità **Sfoglia** per fare clic su **Consenti tutto** nella finestra a comparsa del consenso dei cookie.

![RTCDP](./images/vec2.png)

Fare clic sull&#39;area contenente il testo **Categorie in primo piano**. Fai clic su **Inserisci prima**, quindi seleziona **Decisione offerta**.

![RTCDP](./images/vec3.png)

Poi vedrai questo popup. Seleziona la sandbox `--aepSandboxName--` e quindi il posizionamento **Web - Immagine**.

![RTCDP](./images/vec4.png)

Quindi, selezionare la decisione `--aepUserLdap-- - Luma Decision`. Fai clic su **Salva**.

![RTCDP](./images/vec5.png)

Poi vedrai questo. Assicurati che la regola di aggiunta del modello **URL** **contenga** **nome-progetto**. Selezionare **Salva**.

![RTCDP](./images/vec6.png)

Poi vedrai questo. Fai clic su **Avanti**.

![RTCDP](./images/vec7.png)

Immettere un nome per l&#39;offerta, utilizzare questo nome: `--aepUserLdap-- - XT with Offers (VEC)`. Fai clic su **Avanti**.

![RTCDP](./images/vec8.png)

Poi vedrai questo. Definisci la **metrica obiettivo** come indicato. Fai clic su **Salva e chiudi**.

![RTCDP](./images/vec9.png)

L&#39;offerta è stata creata ed è in fase di pubblicazione.

![RTCDP](./images/vec10.png)

Una volta pubblicata l’offerta, puoi abilitarla.

Passaggio successivo: [3.3.5 Utilizza la tua decisione in un messaggio e-mail e sms](./ex5.md)

[Torna al modulo 3.3](./offer-decisioning.md)

[Torna a tutti i moduli](./../../../overview.md)

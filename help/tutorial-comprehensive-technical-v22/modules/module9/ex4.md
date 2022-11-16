---
title: offer decisioning - Testa la tua decisione utilizzando il sito web demo
description: Verifica la tua decisione utilizzando il sito web demo
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# 9.4 Combinare Adobe Target e Offer Decisioning

## 9.4.1 Raccogli il collegamento condivisibile del progetto demo

Per caricare il progetto del sito web demo in Adobe Target, devi prima raccogliere un collegamento speciale che consentirà ad Adobe Target di caricare il progetto del sito web demo.

Per farlo, vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![RTCDP](./images/builder1.png)

Ora vedrete questo. Fai clic su **Condividi**.

![RTCDP](./images/builder2.png)

Fai clic su **Genera collegamento** quindi copia il collegamento negli Appunti.

![RTCDP](./images/builder3.png)

Vai a [https://bitly.com](https://bitly.com), incolla il collegamento copiato e fai clic su **Abbrevia**. Ora riceverai un collegamento abbreviato, simile al seguente: `https://bit.ly/3JxN7aG`. Sarà necessario quel collegamento nel prossimo esercizio.

![RTCDP](./images/builder4.png)

## 9.4.2 Raccolta

Ora vai alla home page di Adobe Experience Cloud andando a [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Fai clic su **Target**.

![RTCDP](../module6/images/excl.png)

Sulla **Adobe Target** nella home page verranno visualizzate tutte le attività esistenti.

![RTCDP](../module6/images/exclatov.png)

Fai clic su **+ Crea attività** per creare una nuova attività.

![RTCDP](../module6/images/exclatcr.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Ora seleziona **Visivo** e incolla il collegamento abbreviato nel campo . **Inserisci URL attività**. Fai clic su **Avanti**.

![RTCDP](./images/exclatcrxt1.png)

Il progetto del sito web demo verrà caricato nel Compositore esperienza visivo.

![RTCDP](./images/vec1.png)

Vai a **Sfoglia** modalità di clic **Consenti tutto** nella finestra a comparsa di consenso cookie.

![RTCDP](./images/vec2.png)

Fare clic sull&#39;area contenente il testo **Categorie supportate**. Fai clic su **Inserisci prima** quindi seleziona **Decisione di offerta**.

![RTCDP](./images/vec3.png)

Vedrete questa finestra a comparsa. Seleziona la sandbox `--aepSandboxId--` quindi seleziona il posizionamento **Web - Immagine**.

![RTCDP](./images/vec4.png)

Quindi, seleziona la tua decisione `--demoProfileLdap-- - Luma Decision`. Fai clic su **Salva**.

![RTCDP](./images/vec5.png)

Vedrete questo. Assicurati di aggiungere una regola di modello aggiuntiva **URL** **contiene** **nome-progetto**. CLick **Salva**.

![RTCDP](./images/vec6.png)

Vedrete questo. Fai clic su **Avanti**.

![RTCDP](./images/vec7.png)

Immetti un nome per la tua offerta, usa questo nome: `--demoProfileLdap-- - XT with Offers (VEC)`. Fai clic su **Avanti**.

![RTCDP](./images/vec8.png)

Vedrete questo. Definisci i **Metrica per obiettivo** come indicato. Fai clic su **Salva e chiudi**.

![RTCDP](./images/vec9.png)

L’offerta viene ora creata e pubblicata.

![RTCDP](./images/vec10.png)

Una volta pubblicata l’offerta, puoi abilitarla.

Passaggio successivo: [9.5 Utilizza la tua decisione in un messaggio e-mail e sms](./ex5.md)

[Torna al modulo 9](./offer-decisioning.md)

[Torna a tutti i moduli](./../../overview.md)

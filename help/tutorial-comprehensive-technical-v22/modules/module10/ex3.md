---
title: Adobe Journey Optimizer - Applicare la personalizzazione in un messaggio e-mail
description: Questo esercizio spiega come utilizzare la personalizzazione dei segmenti all’interno di un contenuto e-mail
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 10%

---

# 10.3 Applicare la personalizzazione in un messaggio e-mail

Accedi a Adobe Experience Cloud accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Verrai reindirizzato al **Pagina principale** in Journey Optimizer. Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepTenantId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo.

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1 Personalizzazione basata su segmenti

In questo esercizio migliorerai il messaggio e-mail della newsletter con un testo personalizzato basato sull’appartenenza al segmento.

Vai a **Percorsi**. Trova il percorso di newsletter creato nell’esercizio precedente. Cerca `--demoProfileLdap-- - Newsletter`. Fai clic sul percorso per aprirlo.

![Journey Optimizer](./images/sbp1.png)

Vedrete questo. Fai clic su **Duplica**.

![Journey Optimizer](./images/sbp2.png)

Fai clic su ** Duplica**.

![Journey Optimizer](./images/sbp3.png)

Seleziona la tua **E-mail** e fai clic su **Modifica contenuto**.

![Journey Optimizer](./images/sbp3a.png)

Fai clic su **E-mail Designer**.

![Journey Optimizer](./images/sbp4.png)

Vedrete questo.

![Journey Optimizer](./images/sbp5.png)

Apri **Componenti contenuto** e trascina un **Testo** sotto il contenuto della newsletter corrente.

![Journey Optimizer](./images/sbp6.png)

Selezionare l’intero testo predefinito ed eliminarlo. Quindi fai clic sul pulsante **Aggiungi personalizzazione** nella barra degli strumenti.

![Journey Optimizer](./images/sbp7.png)

Vedrai questo:

![Journey Optimizer](./images/seg1.png)

Nel menu a sinistra, fai clic su **Appartenenze ai segmenti**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Se non riesci a trovare il segmento in questo elenco, scorri verso il basso per trovare istruzioni su come recuperare manualmente l’ID segmento.

Selezionare il segmento `Luma - Women's Category Interest` e fai clic su **+** , che dovrebbe avere questo aspetto:

![Journey Optimizer](./images/seg3.png)

È quindi necessario lasciare la prima riga così com&#39;è e sostituire le righe 2 e 3 con questo codice:

``
Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

A quel punto avrai questo:

![Journey Optimizer](./images/seg4.png)

Fai clic su **Convalida** per verificare che il codice sia corretto. Fai clic su **Salva**.

![Journey Optimizer](./images/sbp8.png)

Per salvare il messaggio, fai clic sul pulsante **Salva** nell&#39;angolo in alto a destra. Quindi, fai clic su **Simula contenuto**.

![Journey Optimizer](./images/sbp9.png)

Seleziona uno dei profili creati come parte di questa esercitazione e fai clic su **Anteprima**. Verrà quindi visualizzato il risultato della configurazione.

![Journey Optimizer](./images/sbp10.png)

Vedrete questo. Quindi, fai clic su **Chiudi**.

![Journey Optimizer](./images/sbp10fff.png)

Torna al dashboard dei messaggi facendo clic sul pulsante **freccia** accanto all’oggetto nell’angolo in alto a sinistra.

![Journey Optimizer](./images/sbp11.png)

Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/oc79afff.png)

Fai clic su **Ok** per chiudere l’azione e-mail.

![Journey Optimizer](./images/oc79bfff.png)

Cambia il tuo **Pianificazione** a **Una volta** e definire un **Data/ora**. Fai clic su **Ok**.

>[!NOTE]
>
>La data e l’ora di invio del messaggio devono essere entro più di un’ora.

![Journey Optimizer](./images/sbp18.png)

Fai clic sul pulsante **Pubblica** nel percorso.

![Journey Optimizer](./images/sbp19.png)

Nella finestra a comparsa, fai clic su **Pubblica** di nuovo.

![Journey Optimizer](./images/sbp20.png)

Il percorso base della newsletter è stato pubblicato. Il messaggio e-mail della newsletter verrà inviato in base alla pianificazione e il percorso si interromperà non appena l’ultima e-mail sarà stata inviata.

![Journey Optimizer](./images/sbp20fff.png)

Ha finito questo esercizio.

Passaggio successivo: [10.4 Configurazione e utilizzo delle notifiche push per iOS](./ex4.md)

[Torna al modulo 10](./journeyoptimizer.md)

[Torna a tutti i moduli](../../overview.md)

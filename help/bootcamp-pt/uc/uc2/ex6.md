---
title: Bootcamp - Personalizzazione nel call center - Brasile
description: Bootcamp - Personalizzazione nel call center - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 2.6 Personalizzazione nel call center

Come già discusso più volte durante il bootcamp, personalizzare l’esperienza del cliente è qualcosa che dovrebbe accadere in modo omnicanale. Un call center è spesso completamente disconnesso dal resto del percorso di clienti e questo porta spesso a esperienze frustranti per i clienti, ma non è necessario che lo sia. Mostriamo un esempio di come il call center può essere facilmente collegato a Adobe Experience Platform in tempo reale.

## Flusso del Percorso cliente

Nell’esercizio precedente, utilizzando l’app mobile, hai acquistato un prodotto facendo clic sul pulsante **Acquista** pulsante .

![DSN](./images/app20.png)

Supponiamo che tu abbia una domanda sullo stato del tuo ordine, cosa faresti? In genere, il call center viene chiamato.

Prima di chiamare il call center, devi conoscere il tuo **ID fedeltà**. Puoi trovare il tuo ID fedeltà nel Visualizzatore profili del sito web.

![DSN](./images/cc1.png)

In questo caso, il **ID fedeltà** è **5863105**. Come parte dell’implementazione personalizzata della funzione call center nell’ambiente demo, devi aggiungere un prefisso al tuo **ID fedeltà**. Il prefisso è **11373**, quindi l’ID fedeltà da utilizzare in questo esempio è **11373 5863105**.

Facciamolo ora. Usa il telefono e chiama il numero **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Ti verrà chiesto di inserire il tuo ID fedeltà, seguito da **#**. Immetti il tuo ID fedeltà.

![DSN](./images/cc3.png)

A quel punto sentirete **Ciao, nome**. Questo nome viene preso dal Profilo del cliente in tempo reale in Adobe Experience Platform. Poi hai 3 scelte. Numero della stampa **1**, **Stato dell&#39;ordine**.

![DSN](./images/cc4.png)

Dopo aver sentito il tuo stato d&#39;ordine, ti sarà data la possibilità di scegliere di premere **1** per tornare al menu principale o altro, premere 2. Press **2**.

![DSN](./images/cc5.png)

Verrà quindi chiesto di valutare l&#39;esperienza del call center selezionando un numero compreso tra 1 e 5, con 1 basso e 5 alto. Fate la vostra scelta.

![DSN](./images/cc6.png)

La chiamata al call center terminerà.

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Profili** e **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Seleziona la **Spazio dei nomi identità** **E-mail** e inserisci l&#39;indirizzo e-mail del tuo profilo cliente. Fai clic su **Visualizza**. Fai clic su per aprire il tuo profilo.

![DSN](./images/cc7.png)

Vedrai di nuovo il tuo profilo cliente. Vai a **Eventi**.

![DSN](./images/cc8.png)

In eventi, visualizzerai 2 eventi con un eventType di **callCenter**. Il primo evento è il risultato della tua risposta alla domanda **Valuta la tua soddisfazione di chiamata**.

![DSN](./images/cc9.png)

Scorri un po&#39; verso il basso e vedrai l&#39;evento registrato quando hai selezionato l&#39;opzione per controllare il tuo **Stato dell&#39;ordine**.

![DSN](./images/cc10.png)

Vai a **Iscrizione al segmento**. Ora vedrai che 2 segmenti si qualificano sul tuo profilo, in tempo reale, in base alle interazioni che hai avuto attraverso il call center. Le appartenenze a questi segmenti possono e devono quindi essere utilizzate per influenzare ciò che la comunicazione e la personalizzazione si verificano in qualsiasi altro canale.

![DSN](./images/cc11.png)

Ora avete finito questo esercizio.

[Torna al flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)

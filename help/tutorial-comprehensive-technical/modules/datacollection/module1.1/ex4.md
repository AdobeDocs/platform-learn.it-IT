---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Raccolta dati web lato client
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Raccolta dati web lato client
kt: 5342
doc-type: tutorial
exl-id: dce7f1b5-72ca-41b2-9aa8-41c13ce25c82
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# 1.1.4 Raccolta di dati web lato client

## 1.1.4.1 Convalidare i dati nella richiesta

### Installare l’Adobe Experience Platform Debugger

Experience Platform Debugger è un’estensione disponibile per i browser Chrome e Firefox che consente di visualizzare la tecnologia Adobe implementata nelle pagine web. Installa la versione per il browser preferito:

- [Estensione Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)

- [Estensione Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se non hai mai utilizzato il debugger in precedenza (e questo è diverso dal precedente Adobe Experience Cloud Debugger), guarda questo video introduttivo di cinque minuti:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Dato che stai caricando il sito web demo in modalità in incognito, devi assicurarti che Debugger Experience Platform sia disponibile anche in modalità in incognito. Per farlo, vai a **chrome://extensions** nel browser e apri l&#39;estensione Debugger di Experience Platform.

Verifica che le due impostazioni seguenti siano abilitate:

- Modalità sviluppatore
- Consenti in incognito

![Home page notizie EXP](./images/ext1.png)

### Apri il sito web della demo

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](.//images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

### Utilizza Experience Platform Debugger per visualizzare le chiamate indirizzate all’Edge

Accertati di avere aperto il sito web demo e fai clic sull’icona dell’estensione Experience Platform Debugger.

![Home page notizie EXP](./images/ext2.png)

Verrà aperto Debugger e verranno visualizzati i dettagli dell’implementazione creata nella proprietà Adobe Experience Platform Data Collection. Ricorda che stai eseguendo il debug dell’estensione e delle regole che hai appena modificato.

Fai clic sul pulsante **[!UICONTROL Accedi]** in alto a destra per eseguire l&#39;autenticazione. Se disponi già di una scheda del browser aperta con l’interfaccia di Adobe Experience Platform Data Collection, il passaggio di autenticazione sarà automatico e non dovrai immettere nuovamente il nome utente e la password.

![Debugger AEP](./images/validate2.png)

In seguito, potrai accedere al Debugger.

![Debugger AEP](./images/validate2ab.png)

Premi il pulsante Ricarica sul sito web demo per collegare il debugger a quella scheda specifica.

![Debugger AEP](./images/validate2a.png)

Conferma che il debugger è **[!UICONTROL connesso alla Home]** come illustrato in precedenza, quindi fai clic sull&#39;icona **[!UICONTROL blocca]** per bloccare il debugger sul sito Web demo. Se non esegui questa operazione, il debugger continuerà a passare per esporre i dettagli di implementazione di qualsiasi scheda del browser attiva, il che può creare confusione. Una volta bloccato il debugger, l&#39;icona diventerà **Sblocca**.

![Debugger AEP](./images/validate3.png)

Quindi, vai a qualsiasi pagina del sito web demo, ad esempio la pagina della categoria **Piani**.

![Estensione AEP Web SDK di AEP Debugger](./images/validate4.png)

Ora fai clic su **[!UICONTROL Experience Platform Web SDK]** nell&#39;area di navigazione a sinistra per visualizzare le **[!UICONTROL richieste di rete]**.

Ogni richiesta contiene una riga **[!UICONTROL events]**.

![Estensione AEP Web SDK di AEP Debugger](./images/validate5.png)

Fare clic per aprire una riga di **[!UICONTROL eventi]**. Nota come visualizzare l&#39;evento **web.webpagedetails.pageViews** e altre variabili predefinite conformi al formato **Web SDK ExperienceEvent XDM**.

![Valore eventi](./images/validate8.png)

Questi tipi di dettagli della richiesta sono visibili anche nella scheda Rete. Filtra le richieste con **interagire** per individuare le richieste inviate da Web SDK. Puoi trovare tutti i dettagli del payload XDM nella sezione Payload:

![Scheda Rete](./images/validate9.png)

Passaggio successivo: [1.1.5 Implementare Adobe Analytics e Adobe Audience Manager](./ex5.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)

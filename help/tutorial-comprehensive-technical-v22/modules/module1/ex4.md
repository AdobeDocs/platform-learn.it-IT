---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell'estensione Web SDK - Raccolta dati web lato client
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell'estensione Web SDK - Raccolta dati web lato client
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: c4ebca8d-93e0-4056-8553-c0d7e342beca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# 1.4 Raccolta dati web lato client

## 1.4.1 Convalida i dati nella richiesta

### Installare Adobe Experience Platform Debugger

Experience Platform Debugger è un’estensione disponibile per i browser Chrome e Firefox che consente di visualizzare la tecnologia Adobe implementata nelle pagine web. Scarica la versione per il browser preferito:

- [Estensione Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)

- [Estensione Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se non hai mai utilizzato il debugger prima di - e questo è diverso dal precedente debugger Adobe Experience Cloud - potresti voler guardare questo video di panoramica di cinque minuti:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Dato che stai caricando il sito web demo in modalità in incognito, è necessario assicurarsi che Experience Platform Debugger sia disponibile anche in modalità in incognito. Per farlo, vai a **chrome://extensions** nel browser e apri l’estensione Experience Platform Debugger.

Verifica che le due impostazioni siano abilitate:

- Modalità Sviluppatore
- Consenti in incognito

![Home page di EXP News](./images/ext1.png)

### Apri il sito web demo

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../module0/images/web8.png)

Sulla **Schermi** pagina, fai clic su **Esegui**.

![DSN](./images/web2.png)

Vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../module0/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../module0/images/web4.png)

Incolla l’URL del sito web dimostrativo che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l&#39;accesso utilizzando il tuo Adobe ID.

![DSN](../module0/images/web5.png)

Seleziona il tipo di account e completa il processo di accesso.

![DSN](../module0/images/web6.png)

Il sito web verrà quindi caricato in una finestra del browser in incognito. Per ogni dimostrazione, è necessario utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../module0/images/web7.png)

### Utilizza il debugger di Experience Platform per visualizzare le chiamate che arrivano al server Edge

Assicurati di aver aperto il sito web demo e fai clic sull’icona dell’estensione Experience Platform Debugger .

![Home page di EXP News](./images/ext2.png)

Il debugger verrà aperto e mostrerà i dettagli dell’implementazione creata nella proprietà di raccolta dati di Adobe Experience Platform. Ricorda che stai eseguendo il debug dell’estensione e delle regole che hai appena modificato.

Fai clic sul pulsante **[!UICONTROL Accesso]** in alto a destra per l&#39;autenticazione. Se hai già una scheda del browser aperta con l’interfaccia Adobe Experience Platform Data Collection, il passaggio di autenticazione sarà automatico e non dovrai immettere nuovamente il tuo nome utente e password.

![Debugger AEP](./images/validate2.png)

Premi il pulsante di ricarica sul sito web dimostrativo per collegare il debugger a tale scheda specifica.

![Debugger AEP](./images/validate2a.png)

Conferma che Debugger sia **[!UICONTROL Connessione a Home]** come illustrato in precedenza, quindi fai clic sul pulsante **[!UICONTROL bloccare]** icona per bloccare Debugger sul sito web demo. In caso contrario, Debugger continuerà a passare a per esporre i dettagli di implementazione di qualsiasi scheda del browser in questione, il che può generare confusione.

![Debugger AEP](./images/validate3.png)

Quindi, vai a qualsiasi pagina del sito web demo come per esempio, il **Uomini** pagina categoria.

![Estensione AEP Debugger AEP Web SDK](./images/validate4.png)

Ora fai clic su **[!UICONTROL Experience Platform Web SDK]** nella navigazione a sinistra, per visualizzare il **[!UICONTROL Richieste di rete]**.

Ogni richiesta contiene un **[!UICONTROL events]** fila.

![Estensione AEP Debugger AEP Web SDK](./images/validate5.png)

Fai clic per aprire **[!UICONTROL events]** fila. Si noti come è possibile visualizzare le **web.webpagedetails.pageViews** , nonché altre variabili predefinite conformi al **XDM di ExperienceEvent SDK per web** formato.

![Valore degli eventi](./images/validate8.png)

Questi tipi di dettagli di richiesta sono visibili anche nella scheda Rete. Filtrare le richieste con **interagire** per individuare le richieste inviate dall’SDK web. Puoi trovare tutti i dettagli del payload XDM nelle intestazioni del payload della richiesta:

![Scheda Rete](./images/validate9.png)

Passaggio successivo: [1.5 Implementare Adobe Analytics e Adobe Audience Manager](./ex5.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)

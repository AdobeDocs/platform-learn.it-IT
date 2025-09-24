---
title: Configurare l’ambiente AEM CS
description: Configurare l’ambiente AEM CS
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 15adbf950115f0b6bb6613e69a60b310f25de058
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 1.1.2 Configurare l’ambiente AEM CS

## 1.1.2.1 Configurare l&#39;archivio GitHub

Vai a [https://github.com](https://github.com){target="_blank"}. Fai clic su **Accedi**.

![AEMCS](./images/aemcssetup1.png)

Immettere le credenziali. Fai clic su **Accedi**.

![AEMCS](./images/aemcssetup2.png)

Una volta effettuato l’accesso, verrà visualizzata la dashboard di GitHub.

![AEMCS](./images/aemcssetup3.png)

Vai a [https://github.com/adobe-rnd/aem-boilerplate-xcom](https://github.com/adobe-rnd/aem-boilerplate-xcom){target="_blank"}. Poi vedrai questo. Fare clic su **Usa questo modello** e quindi su **Crea nuovo repository**.

![AEMCS](./images/aemcssetup4.png)

Per il **nome archivio**, utilizzare `citisignal-aem-accs`. Imposta la visibilità su **Privato**. Fare clic su **Crea repository**.

![AEMCS](./images/aemcssetup5.png)

Dopo un paio di secondi, potrai creare l’archivio.

![AEMCS](./images/aemcssetup6.png)

Quindi, vai a [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Fare clic su **Installa** o **Configura**.

![AEMCS](./images/aemcssetup7.png)

Fai clic sul pulsante **Continua** accanto al tuo account utente GitHub.

![AEMCS](./images/aemcssetup8.png)

Fai clic su **Configura** accanto al tuo account utente GitHub.

![AEMCS](./images/aemcssetup8a.png)

Fai clic su **Seleziona solo archivi** e quindi aggiungi l&#39;archivio appena creato.

![AEMCS](./images/aemcssetup9.png)

Scorri verso il basso e fai clic su **Salva**.

![AEMCS](./images/aemcssetup9a.png)

Riceverai questa conferma.

![AEMCS](./images/aemcssetup10.png)

## 1.1.2.2 Aggiorna file fstab.yaml

Nel repository GitHub, fare clic per aprire il file `fstab.yaml`.

![AEMCS](./images/aemcssetup11.png)

Fai clic sull&#39;icona **modifica**.

![AEMCS](./images/aemcssetup12.png)

È ora necessario aggiornare il valore per il campo **url** nella riga 3.

![AEMCS](./images/aemcssetup13.png)

È necessario sostituire il valore corrente con l’URL dell’ambiente AEM Sites CS specifico in combinazione con le impostazioni dell’archivio GitHub.

Valore corrente dell&#39;URL: `https://author-p130360-e1272151.adobeaemcloud.com/bin/franklin.delivery/adobe-rnd/aem-boilerplate-xcom/main`.

È necessario aggiornare 3 parti dell’URL

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX deve essere sostituito dall’URL dell’ambiente AEM CS Author.

YYY deve essere sostituito dall’account utente GitHub.

ZZZ deve essere sostituito dal nome dell’archivio GitHub utilizzato nell’esercizio precedente.

Per trovare l&#39;URL dell&#39;ambiente di authoring AEM CS, vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png)

Fare clic sui tre punti **...** nella scheda **Ambienti** e quindi su **Visualizza dettagli**.

![AEMCS](./images/aemcs9.png)

Visualizzerai quindi i dettagli dell&#39;ambiente, incluso l&#39;URL dell&#39;ambiente **Author**. Copia l’URL.

![AEMCS](./images/aemcs10.png)

XXX = `author-p166717-e1786231.adobeaemcloud.com`

Per il nome dell’account utente GitHub, puoi trovarlo facilmente nell’URL del browser. In questo esempio, il nome dell&#39;account utente è `woutervangeluwe`.

AAAA = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

Per il nome dell’archivio GitHub, puoi trovarlo anche nella finestra del browser che hai aperto in GitHub. In questo caso, il nome dell&#39;archivio è `citisignal`.

ZZZ = `citisignal-aem-accs`

![AEMCS](./images/aemcs12.png)

Questi 3 valori combinati generano questo nuovo URL che deve essere configurato nel file `fstab.yaml`.

`https://author-p166717-e1786231.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal-aem-accs/main`

Fare clic su **Commit changes...**.

![AEMCS](./images/aemcs13.png)

Fai clic su **Commit changes**.

![AEMCS](./images/aemcs14.png)

Il file `fstab.yaml` è stato aggiornato.

## 1.1.2.3 Carica risorse e sito CitiSignal

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png)

Quindi, fai clic sull’URL dell’ambiente di authoring.

![AEMCS](./images/aemcssetup18.png)

Fai clic su **Accedi con Adobe**.

![AEMCS](./images/aemcssetup19.png)

Viene quindi visualizzato l’ambiente di authoring.

![AEMCS](./images/aemcssetup20.png)

L&#39;URL sarà simile al seguente: `https://author-p166717-e1786231.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

È ora necessario accedere all&#39;ambiente **Gestione pacchetti CRX** di AEM. Per eseguire questa operazione, rimuovere `ui#/aem/aem/start.html?appId=aemshell` dall&#39;URL e sostituirlo con `crx/packmgr`, il che significa che l&#39;URL dovrebbe avere un aspetto simile al seguente:
`https://author-p166717-e1786231.adobeaemcloud.com/crx/packmgr`.
Premi **Invio** per caricare l&#39;ambiente di gestione dei pacchetti

![AEMCS](./images/aemcssetup22.png)

Fare clic su **Carica pacchetto**.

![AEMCS](./images/aemcssetup21.png)

Fai clic su **Sfoglia** per individuare il pacchetto da caricare.

Il pacchetto da caricare si chiama **citisignal-assets.zip** e può essere scaricato qui: [https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal_aem_accs.zip](https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal_aem_accs.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png)

Selezionare il pacchetto `citisignal_aem_accs.zip` e fare clic su **Apri**.

![AEMCS](./images/aemcssetup24.png)

Fare clic su **OK**.

![AEMCS](./images/aemcssetup25.png)

Il pacchetto verrà quindi caricato. Fai clic su **Installa** nel pacchetto appena caricato.

![AEMCS](./images/aemcssetup27.png)

Fare clic su **Installa**.

![AEMCS](./images/aemcssetup28.png)

Dopo un paio di minuti, il pacchetto verrà installato.

![AEMCS](./images/aemcssetup29.png)

È ora possibile chiudere questa finestra.

## 1.1.2.4 risorse CitiSignal di pubblicazione

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png)

Quindi, fai clic sull’URL dell’ambiente di authoring.

![AEMCS](./images/aemcssetup18.png)

Fai clic su **Accedi con Adobe**.

![AEMCS](./images/aemcssetup19.png)

Viene quindi visualizzato l’ambiente di authoring. Fare clic su **Assets**.

![AEMCS](./images/aemcsassets1.png)

Fare clic su **File**.

![AEMCS](./images/aemcsassets2.png)

Fare clic per selezionare la cartella **CitiSignal** e quindi fare clic su **Gestisci pubblicazione**.

![AEMCS](./images/aemcsassets3.png)

Fai clic su **Avanti**.

![AEMCS](./images/aemcsassets4.png)

Fai clic su **Pubblica**.

![AEMCS](./images/aemcsassets5.png)

Le risorse sono state pubblicate.

## Sito Web CitiSignal di pubblicazione 1.1.2.5

Fai clic sul nome del prodotto **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo, quindi fai clic sulla **freccia** accanto a **Assets**.

![AEMCS](./images/aemcssetup30a.png)

Fare clic su **Sites**.

![AEMCS](./images/aemcssetup30.png)

Dovresti quindi visualizzare il sito Web **CitiSignal** creato dopo l&#39;installazione del pacchetto precedente.

![AEMCS](./images/aemcssetup31.png)

Per collegare il sito all&#39;archivio GitHub creato in precedenza, è necessario creare una **configurazione Edge Delivery Services**.

Il primo passaggio consiste nel creare una **configurazione cloud**.

A tale scopo, fai clic sul nome del prodotto **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo, quindi fai clic sull&#39;icona **strumenti** e seleziona **Generale**. Fare clic per aprire **Browser configurazioni**.

![AEMCS](./images/aemcssetup31a.png)

Dovresti vedere questo. Fai clic su **Crea**

![AEMCS](./images/aemcssetup31b.png)

Imposta i campi **Titolo** e **Nome** su `CitiSignal`. Abilita la casella di controllo per **Configurazioni cloud**.

Fai clic su **Crea**.

![AEMCS](./images/aemcssetup31c.png)

Dovresti avere questo.

![AEMCS](./images/aemcssetup31d.png)

Successivamente, devi aggiornare alcuni campi della **configurazione cloud** appena creata.

A tale scopo, fai clic sul nome del prodotto **Adobe Experience Manager** nell&#39;angolo in alto a sinistra dello schermo, quindi fai clic sull&#39;icona **strumenti** e seleziona **Servizi cloud**. Fare clic per aprire **Configurazione Edge Delivery Services**.

![AEMCS](./images/aemcssetup32.png)

Seleziona **CitiSignal**, fai clic su **Crea** e seleziona **Configurazione**.

![AEMCS](./images/aemcssetup31e.png)

È ora necessario compilare i campi **Organizzazione** e **Nome sito**. Per farlo, controlla innanzitutto l’URL dell’archivio GitHub.

![AEMCS](./images/aemcssetup31f.png)

- **Organizzazione**: utilizza il nome dell&#39;organizzazione GitHub; in questo esempio è `woutervangeluwe`
- **Nome sito**: utilizzare il nome dell&#39;archivio GitHub, che deve essere `citisignal-aem-accs`.

Fai clic su **Salva e chiudi**.

![AEMCS](./images/aemcssetup33.png)

Dovresti avere questo. Abilita la casella di controllo davanti alla configurazione cloud di Edge appena creata e fai clic su **Pubblica**.

![AEMCS](./images/aemcssetup34.png)

## 1.1.2.6 Aggiorna percorsi file.json

Nel repository GitHub, fare clic per aprire il file `paths.json`.

![AEMCS](./images/aemcssetupjson1.png)

Fai clic sull&#39;icona **modifica**.

![AEMCS](./images/aemcssetupjson2.png)

È ora necessario aggiornare il testo sostitutivo `aem-boilerplate-commerce` con `CitiSignal` nelle righe 3, 4, 5, 6, 7 e 10.

Fai clic su **Commit Changes**.

![AEMCS](./images/aemcssetupjson3.png)

Fai clic su **Commit Changes**.

![AEMCS](./images/aemcssetupjson4.png)

Il file `paths.json` è stato aggiornato.

## Sito Web CitiSignal di pubblicazione 1.1.2.7

Fai clic sul nome del prodotto **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo, quindi seleziona **Sites**.

![AEMCS](./images/aemcssetup38.png)

Fare clic sulla casella di controllo davanti a **CitiSignal**. Quindi fare clic su **Gestisci pubblicazione**.

![AEMCS](./images/aemcssetup39.png)

Fai clic su **Avanti**.

![AEMCS](./images/aemcssetup40.png)

Fare clic su **Includi impostazioni figlio**.

![AEMCS](./images/aemcssetup41.png)

Fare clic per selezionare la casella di controllo **Includi elementi figlio** e quindi fare clic per deselezionare le altre caselle di controllo. Fai clic su **OK**.

![AEMCS](./images/aemcssetup42.png)

Fai clic su **Pubblica**.

![AEMCS](./images/aemcssetup43.png)

Allora verrai rimandato qui. Fai clic su **CitiSignal**, seleziona la casella di controllo davanti a **index**, quindi fai clic su **Modifica**.

![AEMCS](./images/aemcssetup44.png)

Il sito Web verrà quindi aperto in **Universal Editor**.

![AEMCS](./images/aemcssetup45.png)

Ora potrai accedere al tuo sito web da `main--citisignal-aem-accs--XXX.aem.page` e/o `main--citisignal-aem-accs--XXX.aem.live`, dopo aver sostituito XXX con il tuo account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/o `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Potrebbero essere necessari alcuni minuti prima che tutte le risorse vengano visualizzate correttamente, in quanto devono essere pubblicate prima.

A questo punto viene visualizzato quanto segue:

![AEMCS](./images/aemcssetup46.png)

## Prestazioni pagina di prova 1.1.2.8

Vai a [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Immetti l&#39;URL e fai clic su **Analizza**.

![AEMCS](./images/aemcssetup48.png)

Vedrai quindi che il tuo sito web, sia nella visualizzazione per dispositivi mobili che in quella desktop, ottiene un punteggio alto:

**Dispositivi mobili**:

![AEMCS](./images/aemcssetup49.png)

**Desktop**:

![AEMCS](./images/aemcssetup50.png)

Passaggio successivo: [sviluppare un blocco personalizzato](./ex3.md){target="_blank"}

Torna a [Adobe Experience Manager Cloud Service e Edge Delivery Services](./aemcs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

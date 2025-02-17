---
title: Configurare l’ambiente AEM CS
description: Configurare l’ambiente AEM CS
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# 1.1.3 Configurare l’ambiente AEM CS

## 1.1.3.1 Configurare l’archivio GitHub

Vai a [https://github.com](https://github.com){target="_blank"}. Fai clic su **Accedi**.

![AEMCS](./images/aemcssetup1.png){zoomable="yes"}

Immettere le credenziali. Fai clic su **Accedi**.

![AEMCS](./images/aemcssetup2.png){zoomable="yes"}

Una volta effettuato l’accesso, verrà visualizzata la dashboard di GitHub.

![AEMCS](./images/aemcssetup3.png){zoomable="yes"}

Vai a [https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one){target="_blank"}. Poi vedrai questo. Fare clic su **Usa questo modello** e quindi su **Crea nuovo repository**.

![AEMCS](./images/aemcssetup4.png){zoomable="yes"}

Per il **nome archivio**, utilizzare `citisignal`. Imposta la visibilità su **Privato**. Fare clic su **Crea repository**.

![AEMCS](./images/aemcssetup5.png){zoomable="yes"}

Dopo un paio di secondi, potrai creare l’archivio.

![AEMCS](./images/aemcssetup6.png){zoomable="yes"}

Quindi, vai a [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Fare clic su **Configura**.

![AEMCS](./images/aemcssetup7.png){zoomable="yes"}

Fai clic sul tuo account GitHub.

![AEMCS](./images/aemcssetup8.png){zoomable="yes"}

Fai clic su **Seleziona solo archivi** e quindi aggiungi l&#39;archivio appena creato. Fare clic su **Installa**.

![AEMCS](./images/aemcssetup9.png){zoomable="yes"}

Riceverai questa conferma.

![AEMCS](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.3.2 Aggiornamento del file fstab.yaml

Nel repository GitHub, fare clic per aprire il file `fstab.yaml`.

![AEMCS](./images/aemcssetup11.png){zoomable="yes"}

Fai clic sull&#39;icona **modifica**.

![AEMCS](./images/aemcssetup12.png){zoomable="yes"}

È ora necessario aggiornare il valore per il campo **url** nella riga 4.

![AEMCS](./images/aemcssetup13.png){zoomable="yes"}

È necessario sostituire il valore corrente con l’URL dell’ambiente AEM CS specifico in combinazione con le impostazioni dell’archivio GitHub.

Valore corrente dell&#39;URL: `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`.

È necessario aggiornare 3 parti dell’URL

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX deve essere sostituito dall’URL dell’ambiente AEM CS Author.

YYY deve essere sostituito dall’account utente GitHub.

ZZZ deve essere sostituito dal nome dell’archivio GitHub utilizzato nell’esercizio precedente.

Per trovare l&#39;URL dell&#39;ambiente AEM CS Author, vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Fare clic sui tre punti **...** nella scheda **Ambienti** e quindi su **Visualizza dettagli**.

![AEMCS](./images/aemcs9.png){zoomable="yes"}

Visualizzerai quindi i dettagli dell&#39;ambiente, incluso l&#39;URL dell&#39;ambiente **Author**. Copia l’URL.

![AEMCS](./images/aemcs10.png){zoomable="yes"}

XXX = `author-p148073-e1511503.adobeaemcloud.com`

Per il nome dell’account utente GitHub, puoi trovarlo facilmente nell’URL del browser. In questo esempio, il nome dell&#39;account utente è `woutervangeluwe`.

AAAA = `woutervangeluwe`

![AEMCS](./images/aemcs11.png){zoomable="yes"}

Per il nome dell’archivio GitHub, puoi trovarlo anche nella finestra del browser che hai aperto in GitHub. In questo caso, il nome dell&#39;archivio è `citisignal`.

ZZZ = `citisignal`

![AEMCS](./images/aemcs12.png){zoomable="yes"}

Questi 3 valori combinati generano questo nuovo URL che deve essere configurato nel file `fstab.yaml`.

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

Fare clic su **Commit changes...**.

![AEMCS](./images/aemcs13.png){zoomable="yes"}

Fai clic su **Commit changes**.

![AEMCS](./images/aemcs14.png){zoomable="yes"}

Il file `fstab.yaml` è stato aggiornato.

## 1.1.3.3 Caricare risorse CitiSignal

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Quindi, fai clic sull’URL dell’ambiente di authoring.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Fai clic su **Accedi con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Viene quindi visualizzato l’ambiente di authoring.

![AEMCS](./images/aemcssetup20.png){zoomable="yes"}

L&#39;URL sarà simile al seguente: `https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

È ora necessario accedere all&#39;ambiente **Gestione pacchetti CRX** di AEM. Per eseguire questa operazione, rimuovere `ui#/aem/aem/start.html?appId=aemshell` dall&#39;URL e sostituirlo con `crx/packmgr`, il che significa che l&#39;URL dovrebbe avere un aspetto simile al seguente:
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`.
Premi **Invio** per caricare l&#39;ambiente di gestione dei pacchetti

![AEMCS](./images/aemcssetup22.png){zoomable="yes"}

Fare clic su **Carica pacchetto**.

![AEMCS](./images/aemcssetup21.png){zoomable="yes"}

Fai clic su **Sfoglia** per individuare il pacchetto da caricare.

Il pacchetto da caricare si chiama **citisignal-assets.zip** e può essere scaricato qui: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png){zoomable="yes"}

Selezionare il pacchetto e fare clic su **Apri**.

![AEMCS](./images/aemcssetup24.png){zoomable="yes"}

Fare clic su **OK**.

![AEMCS](./images/aemcssetup25.png){zoomable="yes"}

Il pacchetto verrà quindi caricato.

![AEMCS](./images/aemcssetup26.png){zoomable="yes"}

Fai clic su **Installa** nel pacchetto appena caricato.

![AEMCS](./images/aemcssetup27.png){zoomable="yes"}

Fare clic su **Installa**.

![AEMCS](./images/aemcssetup28.png){zoomable="yes"}

Dopo un paio di minuti, il pacchetto verrà installato.

![AEMCS](./images/aemcssetup29.png){zoomable="yes"}

È ora possibile chiudere questa finestra.


## 1.1.3.4 Pubblicare risorse CitiSignal

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Quindi, fai clic sull’URL dell’ambiente di authoring.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Fai clic su **Accedi con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Viene quindi visualizzato l’ambiente di authoring. Fare clic su **Assets**.

![AEMCS](./images/aemcsassets1.png){zoomable="yes"}

Fare clic su **File**.

![AEMCS](./images/aemcsassets2.png){zoomable="yes"}

Fare clic per selezionare la cartella **CitiSignal** e quindi fare clic su **Gestisci pubblicazione**.

![AEMCS](./images/aemcsassets3.png){zoomable="yes"}

Fai clic su **Avanti**.

![AEMCS](./images/aemcsassets4.png){zoomable="yes"}

Fai clic su **Pubblica**.

![AEMCS](./images/aemcsassets5.png){zoomable="yes"}

Le risorse sono state pubblicate.

## 1.1.3.5 Creare il sito web CitiSignal

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Fai clic sul **Programma** per aprirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Quindi, fai clic sull’URL dell’ambiente di authoring.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Fai clic su **Accedi con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Viene quindi visualizzato l’ambiente di authoring. Fare clic su **Sites**.

![AEMCS](./images/aemcssetup30.png){zoomable="yes"}

Fare clic su **Crea** e quindi su **Sito da modello**.

![AEMCS](./images/aemcssetup31.png){zoomable="yes"}

Fai clic su **Importa**.

![AEMCS](./images/aemcssetup32.png){zoomable="yes"}

Ora devi importare un modello preconfigurato per il sito. Puoi scaricare il modello [qui](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip){target="_blank"}. Salva il file sul desktop.

Selezionare il file `citisignal-edge-delivery-services-template-0.0.4.zip` e fare clic su **Apri**.

![AEMCS](./images/aemcssetup33.png){zoomable="yes"}

Poi vedrai questo. Fai clic per selezionare il modello appena caricato, quindi fai clic su **Avanti**.

![AEMCS](./images/aemcssetup34.png){zoomable="yes"}

Ora devi compilare alcuni dettagli.

- Titolo sito: utilizza **CitiSignal**
- Nome sito: utilizzare **citisignal-one**
- URL GitHub: copia l’URL dell’archivio GitHub utilizzato in precedenza

![AEMCS](./images/aemcssetup35.png){zoomable="yes"}

Allora avrai questo. Fai clic su **Crea**.

![AEMCS](./images/aemcssetup36.png){zoomable="yes"}

Creazione del sito in corso. L&#39;operazione potrebbe richiedere alcuni minuti. Fare clic su **OK**.

![AEMCS](./images/aemcssetup37.png){zoomable="yes"}

Dopo alcuni minuti, aggiorna lo schermo e vedrai il tuo nuovo sito Web CitiSignal creato.

![AEMCS](./images/aemcssetup38.png){zoomable="yes"}

## 1.1.3.6 Pubblicare il sito web CitiSignal

Fare clic sulla casella di controllo davanti a **CitiSignal**. Quindi fare clic su **Gestisci pubblicazione**.

![AEMCS](./images/aemcssetup39.png){zoomable="yes"}

Fai clic su **Avanti**.

![AEMCS](./images/aemcssetup40.png){zoomable="yes"}

Fare clic su **Includi impostazioni figlio**.

![AEMCS](./images/aemcssetup41.png){zoomable="yes"}

Fare clic per selezionare la casella di controllo **Includi elementi figlio** e quindi fare clic per deselezionare le altre caselle di controllo. Fai clic su **OK**.

![AEMCS](./images/aemcssetup42.png){zoomable="yes"}

Fai clic su **Pubblica**.

![AEMCS](./images/aemcssetup43.png){zoomable="yes"}

Allora verrai rimandato qui. Passa a **CitiSignal** > **us** > **en**. Fare clic sulla casella di controllo davanti a **index** e quindi su **Modifica**.

![AEMCS](./images/aemcssetup44.png){zoomable="yes"}

Il sito Web verrà quindi aperto in **Universal Editor**.

![AEMCS](./images/aemcssetup45.png){zoomable="yes"}

Ora potrai accedere al tuo sito web da `main--citisignal--XXX.aem.page/us/en` e/o `main--citisignal--XXX.aem.live/us/en`, dopo aver sostituito XXX con il tuo account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal--woutervangeluwe.aem.page/us/en` e/o `https://main--citisignal--woutervangeluwe.aem.live/us/en`.

Potrebbero essere necessari alcuni minuti prima che tutte le risorse vengano visualizzate correttamente, in quanto devono essere pubblicate prima.

A questo punto viene visualizzato quanto segue:

![AEMCS](./images/aemcssetup46.png){zoomable="yes"}

Dopo un paio di minuti, tutte le risorse verranno caricate correttamente.

![AEMCS](./images/aemcssetup47.png){zoomable="yes"}

## 1.1.3.7 Prestazioni della pagina di prova

Vai a [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Immetti l&#39;URL e fai clic su **Analizza**.

![AEMCS](./images/aemcssetup48.png){zoomable="yes"}

Vedrai quindi che il tuo sito web, sia nella visualizzazione per dispositivi mobili che in quella desktop, ottiene un punteggio alto:

**Dispositivi mobili**:

![AEMCS](./images/aemcssetup49.png){zoomable="yes"}

**Desktop**:

![AEMCS](./images/aemcssetup50.png){zoomable="yes"}

Passaggio successivo: [1.1.4 Configurare un blocco personalizzato](./ex4.md){target="_blank"}

Torna a [Adobe Experience Manager Cloud Service e Edge Delivery Services](./aemcs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

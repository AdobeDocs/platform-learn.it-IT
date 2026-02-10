---
title: Creare le risorse e il modello Dynamic Media
description: Creare le risorse e il modello Dynamic Media
kt: 5342
doc-type: tutorial
exl-id: 3867f23b-9b88-4971-a892-5821800e39ac
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 0%

---

# 1.4.1 Creare le risorse e il modello per elementi multimediali dinamici

>[!IMPORTANT]
>
>Per completare questo esercizio, devi avere accesso a un ambiente AEM Assets CS Author funzionante in cui sia abilitato AEM Assets Dynamic Media.
>
>Se non disponi di un ambiente di questo tipo, passa a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.4.1.1 Crea la tua azienda Dynamic Media

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`.

![AEM Assets Dynamic Media](./images/aaemassdmcomp1.png)

Scorri verso il basso fino a **Dynamic Media Companies**. Fai clic sull&#39;icona **+** per creare una nuova società Dynamic Media.

![AEM Assets Dynamic Media](./images/aaemassdmcomp2.png)

Immettere le seguenti informazioni:

- **Nome società**: `--aepUserLdap---CitiSignal`.
- **Regione dell&#39;azienda**: seleziona l&#39;area più vicina all&#39;utente.
- **E-mail amministratore società**: inserisci l&#39;e-mail amministratore.

Fai clic su **Crea**.

![AEM Assets Dynamic Media](./images/aaemassdmcomp3.png)

Dovresti vedere questo.

![AEM Assets Dynamic Media](./images/aaemassdmcomp4.png)

A questo punto dovresti ricevere un&#39;e-mail simile a quella riportata di seguito, contenente la tua password temporanea. Per modificare la password o recuperarla nel caso in cui non sia stato ricevuto un messaggio di posta elettronica, installare l&#39;**app desktop Adobe Dynamic Media Classic**. Le istruzioni di installazione sono disponibili qui: [https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app).

Segui le istruzioni e torna qui una volta che l’app è installata sul tuo sistema.

Apri l&#39;**app desktop Adobe Dynamic Media Classic**. Se conosci la password, inseriscila qui e segui le istruzioni per modificarla al primo accesso.

Se non conosci la password, fai clic sul collegamento **Password dimenticata** e segui le istruzioni per reimpostare la password, quindi torna qui e accedi.

![AEM Assets Dynamic Media](./images/aaemassdmcomp5.png)

Dopo aver effettuato l’accesso, dovresti vedere una schermata simile a questa.

![AEM Assets Dynamic Media](./images/aaemassdmcomp6.png)

## 1.4.1.2 Configurare Dynamic Media in AEM

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`.

Fare clic per aprire il programma Cloud Manager, che dovrebbe essere denominato `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![AEM Assets Dynamic Media](./images/accsaemassets1.png)

Fai clic sull’ambiente.

![AEM Assets Dynamic Media](./images/accsaemassets3.png)

Fai clic sull’URL dell’ambiente.

![AEM Assets Dynamic Media](./images/accsaemassets2.png)

Vai a **Strumenti**, a **Servizi cloud** e quindi a **Configurazione elementi multimediali dinamici**.

![AEM Assets Dynamic Media](./images/accsaemassets4.png)

Seleziona **Global** (non selezionare la casella di controllo), quindi fai clic su **Crea**.

![AEM Assets Dynamic Media](./images/accsaemassets5.png)

Immettere le seguenti informazioni:

- **Titolo**: usa questo titolo: `--aepUserLdap-- - CitiSignal`.
- **E-mail**: immetti il tuo indirizzo e-mail.
- **Password**: immetti la password dell&#39;account Dynamic Media
- **Area geografica**: seleziona l&#39;area geografica scelta durante la creazione della società Dynamic Media, in questo esempio **Europa**.

Fai clic su **Connetti a Dynamic Media**.

![AEM Assets Dynamic Media](./images/accsaemassets6.png)

Dovresti vedere questo. Configura quanto segue:

- Selezionare la **società**: `--aepUserLdap-- - CitiSignal`.
- Imposta **Pubblica Assets** su **Immediata**.
- Selezionare la casella di controllo per **Sincronizzare tutto il contenuto**.

Fai clic su **Salva**.

![AEM Assets Dynamic Media](./images/accsaemassets7.png)

La configurazione di DYnamic Media è terminata. Fai clic su **OK**.

![AEM Assets Dynamic Media](./images/accsaemassets8.png)

## 1.4.1.3 Esporta le risorse

Scarica il file [citisignal-fibre-max-is-coming.psd](./assets/citisignal-fiber-max-is-coming.psd){target="_blank"} e aprilo con Adobe Photoshop.

Dovresti vedere questo. CitiSignal sta pianificando un rollout di Fiber Max in 3 città: New York, Parigi e Dubai.

Mostrando o nascondendo livelli specifici, potete visualizzare l&#39;immagine creata dai designer.

Di seguito sono riportate le istruzioni per esportare i file immagine dal modello Photoshop PSD. Se preferisci, puoi scaricare le immagini finite qui [citisignal-dm-email-assets.zip](./assets/citisignal-dm-email-assets.zip){target="_blank"} e decomprimere il file sul desktop.

Questa è la versione per New York.

![AEM Assets Dynamic Media](./images/aemdm1.png)

Questa è la versione per Dubai.

![AEM Assets Dynamic Media](./images/aemdm2.png)

Questa è la versione per Parigi.

![AEM Assets Dynamic Media](./images/aemdm3.png)

Potenzialmente, ci saranno molte altre città in cui Citisegnale distribuirà Fibre Max in modo che in futuro possano essere creati nuovi livelli in questo file. Per il momento l&#39;attenzione si concentra sulle 3 città già menzionate.

Per utilizzare queste varianti in combinazione con AEM Assets Dynamic Media, i livelli di ciascuna città devono essere esportati come immagini separatamente senza il file di sfondo e deve essere eseguita un’altra esportazione per il livello di sfondo senza includere alcuna città.

Ora dovete nascondere e mostrare solo uno dei livelli. Il primo livello da mostrare è il livello **Parigi** e tutti gli altri livelli devono essere nascosti.

Per esportare il livello, passare a **File** > **Esporta** > **Esporta con nome...**.

![AEM Assets Dynamic Media](./images/aemdm4.png)

Dovresti vedere questo. Selezionare il tipo di file **PNG**, verificare che **Transparency** sia abilitato e quindi fare clic su **Export**.

![AEM Assets Dynamic Media](./images/aemdm5.png)

Cambia il nome del file in `citisignal-fiber-max-is-coming-paris.png` e fai clic su **Esporta**.

![AEM Assets Dynamic Media](./images/aemdm6.png)

Il livello successivo da visualizzare è il livello **Dubai** e tutti gli altri livelli devono essere nascosti.

Per esportare il livello, passare a **File** > **Esporta** > **Esporta con nome...**.

![AEM Assets Dynamic Media](./images/aemdm4a.png)

Dovresti vedere questo. Selezionare il tipo di file **PNG**, verificare che **Transparency** sia abilitato e quindi fare clic su **Export**.

![AEM Assets Dynamic Media](./images/aemdm5a.png)

Cambia il nome del file in `citisignal-fiber-max-is-coming-dubai.png` e fai clic su **Esporta**.

![AEM Assets Dynamic Media](./images/aemdm6a.png)

Il livello successivo da visualizzare è il livello **New York** e tutti gli altri livelli devono essere nascosti.

Per esportare il livello, passare a **File** > **Esporta** > **Esporta con nome...**.

![AEM Assets Dynamic Media](./images/aemdm4b.png)

Dovresti vedere questo. Selezionare il tipo di file **PNG**, verificare che **Transparency** sia abilitato e quindi fare clic su **Export**.

![AEM Assets Dynamic Media](./images/aemdm5b.png)

Cambia il nome del file in `citisignal-fiber-max-is-coming-newyork.png` e fai clic su **Esporta**.

![AEM Assets Dynamic Media](./images/aemdm6b.png)

Il livello successivo da visualizzare è il livello **sfondo** e tutti gli altri livelli devono essere nascosti.

Per esportare il livello, passare a **File** > **Esporta** > **Esporta con nome...**.

![AEM Assets Dynamic Media](./images/aemdm4c.png)

Dovresti vedere questo. Selezionare il tipo di file **PNG**, verificare che **Transparency** sia abilitato e quindi fare clic su **Export**.

![AEM Assets Dynamic Media](./images/aemdm5c.png)

Cambia il nome del file in `citisignal-fiber-max-is-coming-background` e fai clic su **Esporta**.

![AEM Assets Dynamic Media](./images/aemdm6c.png)

Dovresti quindi avere questi file disponibili nel percorso di esportazione selezionato.

![AEM Assets Dynamic Media](./images/aemdm7.png)

## 1.4.1.4 Carica le risorse in AEM Assets CS

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Vai a **Experience Manager Assets**.

![AEM Assets Dynamic Media](./images/aemdm8.png)

Selezionare l&#39;archivio, che deve essere denominato `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![AEM Assets Dynamic Media](./images/aemdm9.png)

Vai a **Assets** e fai clic su **Crea cartella**.

![AEM Assets Dynamic Media](./images/aemdm10.png)

Per la cartella, utilizzare il nome: `--aepUserLdap-- - CitiSignal Dynamic Media`. Fai clic su **Crea**.

![AEM Assets Dynamic Media](./images/aemdm11.png)

Fare doppio clic per aprire la cartella appena creata.

![AEM Assets Dynamic Media](./images/aemdm12.png)

Fare clic su **Aggiungi Assets**.

![AEM Assets Dynamic Media](./images/aemdm13.png)

Fare clic su **Sfoglia**, quindi selezionare **Sfoglia file**.

![AEM Assets Dynamic Media](./images/aemdm15.png)

Selezionare i 4 file PNG esportati nel passaggio precedente.

![AEM Assets Dynamic Media](./images/aemdm16.png)

Fai clic su **Carica**.

![AEM Assets Dynamic Media](./images/aemdm17.png)

Le immagini sono ora disponibili in AEM Assets CS.

![AEM Assets Dynamic Media](./images/aemdm18.png)

Attendi alcuni minuti e apri la **app desktop Adobe Dynamic Media Classic**. Dovresti vedere che le immagini caricate saranno disponibili in Dynamic Media.

![AEM Assets Dynamic Media](./images/aemdm19.png)

## 1.4.1.5 Configura modello Dynamic Media

Nel menu a sinistra, vai a **Dynamic Media Assets**. Fare clic per aprire la cartella `--aepUserLdap-- - CitiSignal Dynamic Media`. Quindi fare clic su **Crea modello**.

![AEM Assets Dynamic Media](./images/aemdm20.png)

Immettere le seguenti informazioni:

- **Nome modello**: `--aepUserLdap-- - CitiSignal Fiber Max Launch Email Assets`
- **Larghezza area di lavoro**: `600px`
- **Altezza area di lavoro**: `600px`

Fai clic su **Crea**.

![AEM Assets Dynamic Media](./images/aemdm21.png)

Dovresti vedere questo. Fai clic sull&#39;icona **Aggiungi immagine**.

![AEM Assets Dynamic Media](./images/aemdm22.png)

Trascina il file **citisignal-fiber-max-is-coming_citisignal-background.png** nell’area di lavoro e adattalo all’area di lavoro.

![AEM Assets Dynamic Media](./images/aemdm23.png)

Trascinare il file **citisignal-fibre-max-is-coming_citisignal-newyork.png** nell&#39;area di lavoro e adattarlo all&#39;area di lavoro.

![AEM Assets Dynamic Media](./images/aemdm24.png)

Trascinare il file **citisignal-fibre-max-is-coming_citisignal-dubai.png** nell&#39;area di lavoro e adattarlo all&#39;area di lavoro.

![AEM Assets Dynamic Media](./images/aemdm25.png)

Trascinare il file **citisignal-fiber-max-is-coming_citisignal-paris.png** nell&#39;area di lavoro e adattarlo all&#39;area di lavoro.

![AEM Assets Dynamic Media](./images/aemdm26.png)

Ora tutte e 3 le varianti del modello sono disponibili come livelli distinti contemporaneamente. Puoi mostrare/nascondere livelli specifici facendo clic sull&#39;icona **livelli**, in cui puoi vedere che tutti i livelli sono attualmente visibili.

![AEM Assets Dynamic Media](./images/aemdm27.png)

Nascondendo un paio di livelli, è possibile controllare l&#39;aspetto dell&#39;immagine. In questo esempio, sono visibili solo il livello per **Parigi** e il livello di sfondo.

![AEM Assets Dynamic Media](./images/aemdm28.png)

Successivamente, è necessario aggiungere un livello di testo. Fai clic sull&#39;icona **livello di testo**.

![AEM Assets Dynamic Media](./images/aemdm29.png)

Dovresti vedere questo.

![AEM Assets Dynamic Media](./images/aemdm30.png)

Puoi adattare il campo di testo nel modo che preferisci, ecco un esempio. Non dimenticare di abilitare l&#39;opzione **Ridimensionamento automatico del testo** in modo che il testo reale inserito in una fase successiva risulti corretto.

![AEM Assets Dynamic Media](./images/aemdm31.png)

Aggiungete un secondo livello di testo e impostatelo in questo modo. Non dimenticare di abilitare l&#39;opzione **Ridimensionamento automatico del testo** in modo che il testo reale inserito in una fase successiva risulti corretto.

![AEM Assets Dynamic Media](./images/aemdm32.png)

Selezionate il primo livello di testo. Fai clic sui tre punti **...**, quindi seleziona **Modifica**.

![AEM Assets Dynamic Media](./images/aemdm33.png)

Dovresti vedere questo. Scorri verso il basso.

![AEM Assets Dynamic Media](./images/aemdm34.png)

Fai clic sull&#39;icona **commutatore** in modo che il campo **Testo** sia abilitato. Cambia il **Nome parametro** in `title`.

![AEM Assets Dynamic Media](./images/aemdm35.png)

Selezionate il secondo livello di testo. Fai clic sui tre punti **...**, quindi seleziona **Modifica**.

![AEM Assets Dynamic Media](./images/aemdm36.png)

Dovresti vedere questo. Scorri verso il basso.

![AEM Assets Dynamic Media](./images/aemdm37.png)

Fai clic sull&#39;icona **commutatore** in modo che il campo **Testo** sia abilitato. Cambia il **Nome parametro** in `body`.

![AEM Assets Dynamic Media](./images/aemdm38.png)

Seleziona il livello per **Parigi**. Fai clic sui tre punti **...** e fai clic su **Modifica**.

![AEM Assets Dynamic Media](./images/aemdm39.png)

Vai a **Parametri**. Abilita il campo **Nascondi** e immetti il **Nome parametro**: `city_paris`. Fai clic su **Salva**.

![AEM Assets Dynamic Media](./images/aemdm40.png)

Seleziona il livello per **Dubai**. Fai clic sui tre punti **...** e fai clic su **Modifica**.

![AEM Assets Dynamic Media](./images/aemdm41.png)

Vai a **Parametri**. Abilita il campo **Nascondi** e immetti il **Nome parametro**: `city_dubai`. Fai clic su **Salva**.

![AEM Assets Dynamic Media](./images/aemdm42.png)

Seleziona il livello per **New York**. Fai clic sui tre punti **...** e fai clic su **Modifica**.

![AEM Assets Dynamic Media](./images/aemdm43.png)

Vai a **Parametri**. Abilita il campo **Nascondi** e immetti il **Nome parametro**: `city_ny`. Fai clic su **Salva**.

![AEM Assets Dynamic Media](./images/aemdm44.png)

Fare clic su **Anteprima**.

![AEM Assets Dynamic Media](./images/aemdm45.png)

Abilita il commutatore per **Includi tutti i parametri** e modifica alcune variabili di input come indicato nella schermata. Dovresti vedere la tua immagine cambiare dinamicamente in base all’input fornito. Per i campi **city_paris**, **city_dubai** e **city_ny**, il valore 0 indica che questa immagine NON sarà nascosta e il valore 1 indica che questa immagine sarà nascosta.

![AEM Assets Dynamic Media](./images/aemdm46.png)

Modificando alcune variabili, ora viene visualizzata un’altra immagine.

![AEM Assets Dynamic Media](./images/aemdm47.png)

Modificando più variabili, ora viene visualizzata un’altra immagine.

Per utilizzare questo modello con Adobe Journey Optimizer e soddisfare i requisiti di questo caso d’uso, è necessario aggiungere un ulteriore livello che verrà utilizzato per modificare dinamicamente il percorso del file da visualizzare, in base a un campo che fa parte di Real-Time Customer Profile in Adobe Experience Platform.

Durante il processo di creazione dati, è stato creato un campo in Schema Adobe Experience Platform per memorizzare la **città di rollout più vicina** per un cliente. Il percorso del campo è `--aepTenantId--.individualCharacteristics.fiber_rollout.closest_rollout_city`.

>[!NOTE]
>
>La schermata seguente dello schema Adobe Experience Platform ha valore puramente informativo. Non è necessario passare ad AEP per visualizzarlo.

![AEM Assets Dynamic Media](./images/aemdm50.png)

Nell’esercizio successivo, utilizzerai quel campo per selezionare dinamicamente quale immagine mostrare a quale cliente.

Per renderlo possibile, devi aggiungere un nuovo livello immagine.

Per prima cosa, nascondiamo gli altri livelli che contengono immagini per le città di rollout.

![AEM Assets Dynamic Media](./images/aemdm51.png)

Quindi, vai a **Immagini** e seleziona un&#39;immagine casuale di una città, aggiungila all&#39;area di lavoro e accertati che sia adatta all&#39;intera area di lavoro. Non importa quale immagine della città scegli, poiché il percorso verrà modificato dinamicamente da AJO nel prossimo esercizio.

![AEM Assets Dynamic Media](./images/aemdm52.png)


![AEM Assets Dynamic Media](./images/aemdm53.png)

Vai a **Parametri**.

Fai clic sull&#39;icona **commutatore** in modo che il campo **Nascondi** sia abilitato. Cambia il **Nome parametro** in `dynamic_city_hide`.

Fai clic sull&#39;icona **commutatore** in modo che il campo **Nascondi** sia abilitato. Cambia il **Nome parametro** in `dynamic_city_image`.

Fai clic su **Salva**.

![AEM Assets Dynamic Media](./images/aemdm54.png)

Fare clic su **Anteprima**.

![AEM Assets Dynamic Media](./images/aemdm55.png)

Dovresti vedere questo. Abilita l&#39;icona del commutatore su **Includi tutti i parametri**. Modifica alcune variabili di input come indicato nella schermata. Dovresti vedere la tua immagine cambiare dinamicamente in base all’input fornito. I campi statici **city_paris**, **city_dubai** e **city_ny** devono essere impostati su 1, il che significa che queste immagini saranno nascoste.

Il campo **dynamic_city_hide** deve essere impostato su 0, ovvero verrà visualizzato.

Il campo **dynamic_city_image** ora contiene l&#39;URL dell&#39;immagine di Parigi, che si presenta così: `vangeluwCitiSignalDM/citisignal-fiber-max-is-coming_citisignal-paris-1`.

![AEM Assets Dynamic Media](./images/aemdm56.png)

Selezionare la parola **paris** nell&#39;URL.

![AEM Assets Dynamic Media](./images/aemdm57.png)

Cambia **paris** in `newyork` e quindi fai clic in un altro punto dell&#39;interfaccia utente per visualizzare la modifica dell&#39;immagine nella città di New York.

![AEM Assets Dynamic Media](./images/aemdm58.png)

Seleziona la parola **newyork** e modificala in `dubai`, quindi fai clic in un altro punto dell&#39;interfaccia utente per visualizzare la modifica dell&#39;immagine nella città di Dubai.

Infine, fare clic su **Pubblica**.

![AEM Assets Dynamic Media](./images/aemdm60.png)

Dovresti vedere questo. Fare clic su **Sì**.

![AEM Assets Dynamic Media](./images/aemdm61.png)

Il modello Dynamic Media è ora configurato e pubblicato correttamente. Nell’esercizio successivo, utilizzerai tale modello in combinazione con una campagna e-mail in Adobe Journey Optimizer.

## Passaggi successivi

Passaggio successivo: [Utilizzare il modello Dynamic Media con Adobe Journey Optimizer](./ex2.md){target="_blank"}

Torna a [Adobe Experience Manager Assets e Dynamic Media](./aemassetsdm.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

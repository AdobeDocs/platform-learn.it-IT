---
title: Collegare ACS ad AEM Assets CS
description: Collegare ACS ad AEM Assets CS
kt: 5342
doc-type: tutorial
source-git-commit: ca895385f5c1f318a7c4d0b338dcfa4e91763005
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---

# 1.5.3 Collegare ACS ad AEM Assets CS

>[!IMPORTANT]
>
>Per completare questo esercizio, è necessario avere accesso a un ambiente AEM Sites e Assets CS funzionante con EDS.
>
>Se non si dispone ancora di un ambiente di questo tipo, passare all&#39;esercizio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Sites e Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.5.3.1 Aggiorna configurazione pipeline

Vai a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L&#39;organizzazione da selezionare è `--aepImsOrgName--`.

Fare clic per aprire il programma Cloud Manager, che dovrebbe essere denominato `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![ACCS+AEM Assets](./images/accsaemassets1.png)

Scorrere verso il basso e quindi fare clic su **Accedi a dati archivio** nella scheda **Pipeline**.

![ACCS+AEM Assets](./images/accsaemassets2.png)

Dovresti vedere questo. Fare clic su **Genera password**.

![ACCS+AEM Assets](./images/accsaemassets3.png)

Fai di nuovo clic su **Genera password**.

![ACCS+AEM Assets](./images/accsaemassets4.png)

Dovresti quindi disporre di una password. Fare clic sull&#39;icona **copia** accanto al campo **Riga di comando Git**.

![ACCS+AEM Assets](./images/accsaemassets5.png)

Crea una nuova directory nel percorso desiderato sul computer e denominala **AEM Pipeline GitHub**.

![ACCS+AEM Assets](./images/accsaemassets6.png)

Fare clic con il pulsante destro del mouse sulla cartella e selezionare **Nuovo terminale nella cartella**.

![ACCS+AEM Assets](./images/accsaemassets7.png)

Dovresti vedere questo.

![ACCS+AEM Assets](./images/accsaemassets8.png)

Incolla il comando **Git** copiato in precedenza nella finestra di Terminal.

![ACCS+AEM Assets](./images/accsaemassets9.png)

Immettere un nome utente. Copia il nome utente dalla pipeline del programma Cloud Manager **Accedi a dati archivio** e premi **Invio**.

![ACCS+AEM Assets](./images/accsaemassets10.png)

Quindi, devi immettere la password. Copia la password dalla pipeline del programma Cloud Manager **Accedi a dati archivio** e premi **Invio**.

![ACCS+AEM Assets](./images/accsaemassets11.png)

Questo potrebbe richiedere un minuto. Una volta completato, avrai una copia locale dell’archivio Git collegata alla pipeline del programma.

![ACCS+AEM Assets](./images/accsaemassets12.png)

Verrà visualizzata una nuova directory nella directory **GitHub della pipeline AEM**. Apri quella directory.

![ACCS+AEM Assets](./images/accsaemassets13.png)

Selezionare tutti i file nella directory ed eliminarli tutti.

![ACCS+AEM Assets](./images/accsaemassets14.png)

Assicurati che la directory sia vuota.

![ACCS+AEM Assets](./images/accsaemassets15.png)

Vai a [https://github.com/ankumalh/assets-commerce](https://github.com/ankumalh/assets-commerce).

Quindi, copia il file **assets-commerce-main.zip** sul desktop e decomprimi. Apri la cartella **assets-commerce-main**.

![ACCS+AEM Assets](./images/accsaemassets16.png)

Copia tutti i file dalla directory **assets-commerce-main** nella directory vuota della directory dell&#39;archivio delle pipeline del programma.

![ACCS+AEM Assets](./images/accsaemassets17.png)

Aprire quindi **Microsoft Visual Studio Code** e aprire la cartella contenente l&#39;archivio delle pipeline del programma in **Microsoft Visual Studio Code**.

![ACCS+AEM Assets](./images/accsaemassets18.png)

Vai a **Cerca** nel menu a sinistra e cerca `<my-app>`. È necessario sostituire tutte le occorrenze di `<my-app>` con `--aepUserLdap--citisignalaemaccs`.

Fai clic sull&#39;icona **sostituisci tutto**.

![ACCS+AEM Assets](./images/accsaemassets19.png)

Fare clic su **Sostituisci**.

![ACCS+AEM Assets](./images/accsaemassets20.png)

I nuovi file sono ora pronti per essere caricati nuovamente nell’archivio Git collegato all’archivio delle pipeline del programma. Per farlo, apri la cartella **GitHub della pipeline AEM** e fai clic con il pulsante destro del mouse sulla cartella che contiene i nuovi file. Selezionare **Nuovo terminale nella cartella**.

![ACCS+AEM Assets](./images/accsaemassets21.png)

Dovresti vedere questo. Incolla il comando `git add .` e premi **Invio**.

![ACCS+AEM Assets](./images/accsaemassets22.png)

Dovresti vedere questo. Incolla il comando `git commit -m "add assets integration"` e premi **Invio**.

![ACCS+AEM Assets](./images/accsaemassets23.png)

Dovresti vedere questo. Incolla il comando `git push origin main` e premi **Invio**.

![ACCS+AEM Assets](./images/accsaemassets24.png)

Dovresti vedere questo. Le modifiche sono state distribuite nell’archivio Git della pipeline del programma.

![ACCS+AEM Assets](./images/accsaemassets25.png)

Torna a Cloud Manager e fai clic su **Chiudi**.

![ACCS+AEM Assets](./images/accsaemassets26.png)

Dopo aver apportato modifiche all&#39;archivio Git della pipeline, devi eseguire nuovamente la pipeline **Distribuisci su Dev**. Fare clic sui tre punti **...** e selezionare **Esegui**.

![ACCS+AEM Assets](./images/accsaemassets27.png)

Fare clic su **Esegui**. L’esecuzione di una distribuzione della pipeline può richiedere 10-15 minuti. Prima di continuare, devi attendere il completamento della distribuzione della pipeline.

![ACCS+AEM Assets](./images/accsaemassets28.png)

## 1.5.3.2 Abilitare l&#39;integrazione di AEM Assets in ACCS

Torna all’istanza ACS. Nel menu a sinistra, vai a **Archivi** e quindi seleziona **Configurazione**.

![ACCS+AEM Assets](./images/accsaemassets49.png)

Scorri verso il basso nel menu fino a **ADOBE SERVICES**, quindi apri **AEM Assets Integration**. Dovresti vedere questo.

![ACCS+AEM Assets](./images/accsaemassets50.png)

Compila le seguenti variabili:

- **ID programma AEM Assets**: puoi prendere l&#39;ID programma dall&#39;URL dell&#39;autore di AEM CS. In questo esempio, l&#39;ID del programma è `166717`.

![ACCS+AEM Assets](./images/accsaemassets50a.png)

- **ID ambiente AEM Assets**: puoi prendere l&#39;ID ambiente dall&#39;URL di authoring di AEM CS. In questo esempio, l&#39;ID ambiente è `1786231`.

![ACCS+AEM Assets](./images/accsaemassets50b.png)

- **ID client IMS selettore risorse**: impostato su `1`
- **Sincronizzazione abilitata**: impostata su `Yes`
- **Proprietario visualizzazione**: `AEM Assets`
- **Regola di corrispondenza risorse**: `Match by product SKU`
- **Corrispondenza per nome attributo SKU prodotto**: `commerce:skus`

Fai clic su **Salva configurazione**.

![ACCS+AEM Assets](./images/accsaemassets51.png)

## 1.5.3.3 Aggiornamento config.json

Vai all’archivio GitHub creato durante la configurazione dell’ambiente AEM Sites CS/EDS. L&#39;archivio è stato creato nell&#39;esercizio [1.1.2 Configurare l&#39;ambiente AEM CS](./../../../modules/asset-mgmt/module2.1/ex3.md){target="_blank"} e deve essere denominato **citisignal-aem-accs**.

Nella directory principale, scorrere verso il basso e fare clic per aprire il file **config.json**. Fai clic sull&#39;icona **modifica** per apportare modifiche al file.

![ACCS+AEM Assets](./images/accsaemassets101.png)

Aggiungere il frammento di codice seguente alla riga 5 `"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/XXX/graphql",`:

```json
 "commerce-assets-enabled": "true",
```

Fare clic su **Commit Changes...**.

![ACCS+AEM Assets](./images/accsaemassets102.png)

Fai clic su **Commit Changes**.

![ACCS+AEM Assets](./images/accsaemassets103.png)

La modifica è stata salvata e verrà pubblicata a breve. Potrebbero essere necessari un paio di minuti prima che la modifica sia visibile sulla vetrina.

![ACCS+AEM Assets](./images/accsaemassets104.png)

## 1.5.3.4 Verifica campi Commerce in AEM Assets CS

Accedi all&#39;ambiente di authoring di AEM CS e passa a **Assets**.

![ACCS+AEM Assets](./images/accsaemassets30.png)

Vai a **File**.

![ACCS+AEM Assets](./images/accsaemassets31.png)

Apri la cartella **CitiSignal**.

![ACCS+AEM Assets](./images/accsaemassets32.png)

Passa il puntatore del mouse su una risorsa e fai clic sull&#39;icona **info**.

![ACCS+AEM Assets](./images/accsaemassets33.png)

Dovresti ora visualizzare una scheda **Commerce** contenente 2 nuovi attributi di metadati.

![ACCS+AEM Assets](./images/accsaemassets34.png)

Il tuo ambiente AEM Assets CS ora supporta l’integrazione con Commerce. Ora puoi iniziare a caricare le immagini del prodotto.

## 1.5.3.4 Carica Assets prodotto e collega ai prodotti

[Scarica qui le immagini del prodotto](./images/Product_Images.zip). Una volta scaricati, esportare i file sul desktop.

![ACCS+AEM Assets](./images/accsaemassets35.png)

Fai clic su **Crea**, quindi seleziona **Cartella**.

![ACCS+AEM Assets](./images/accsaemassets36.png)

Immetti il valore **Product_Images** per i campi **Title** e **Name**. Fai clic su **Crea**.

![ACCS+AEM Assets](./images/accsaemassets37.png)

Fai clic su per aprire la cartella appena creata.

![ACCS+AEM Assets](./images/accsaemassets38.png)

Fai clic su **Crea**, quindi seleziona **File**.

![ACCS+AEM Assets](./images/accsaemassets39.png)

Passa alla cartella **Product_Images** sul desktop, seleziona tutti i file e fai clic su **Apri**.

![ACCS+AEM Assets](./images/accsaemassets40.png)

Fai clic su **Carica**.

![ACCS+AEM Assets](./images/accsaemassets41.png)

Le immagini saranno quindi disponibili nella cartella.

![ACCS+AEM Assets](./images/accsaemassets42.png)

Fai clic sulla prima immagine del prodotto per aprirla.

![ACCS+AEM Assets](./images/accsaemassets43.png)

Imposta lo stato dell&#39;immagine del prodotto su **Approvato**. L’integrazione AEM Assets CS - ACCS funziona solo per le immagini approvate.

![ACCS+AEM Assets](./images/accsaemassets44.png)

Passa alla scheda **Commerce** e fai clic su **Aggiungi** in **SKU prodotto**.

![ACCS+AEM Assets](./images/accsaemassets45.png)

Prendi lo SKU del prodotto dal nome del file di immagine, aumenta il valore a 1 e seleziona tutte le opzioni nell&#39;elenco a discesa **utilizzo**.

![ACCS+AEM Assets](./images/accsaemassets46.png)

Dovresti avere questo. Fai clic su **Salva e chiudi**.

![ACCS+AEM Assets](./images/accsaemassets47.png)

Ripeti questa azione di approvazione di una risorsa e impostazione della scheda Commerce per ogni immagine importata in questa cartella. Al termine, ogni immagine deve avere un pollice verde **alto**, che indica che la risorsa è stata approvata.

![ACCS+AEM Assets](./images/accsaemassets48.png)

## 1.5.3.5 Verifica immagini prodotto in AEM Sites CS/EDS Storefront



Passaggio successivo: [Riepilogo e vantaggi](./summary.md){target="_blank"}

Torna a [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

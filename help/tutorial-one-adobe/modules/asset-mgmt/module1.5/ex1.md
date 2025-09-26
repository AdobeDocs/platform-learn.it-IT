---
title: Guida introduttiva ad Adobe Commerce as a Cloud Service
description: Guida introduttiva ad Adobe Commerce as a Cloud Service
kt: 5342
doc-type: tutorial
exl-id: 8603c8e2-c3ba-4976-9703-cef9e63924b8
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.1 Guida introduttiva ad Adobe Commerce as a Cloud Service

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Assicurarsi di trovarsi nell&#39;ambiente corretto, che deve essere denominato `--aepImsOrgName--`. Fare clic su **Commerce**.

![AEM Assets](./images/accs1.png)

## 1.5.1.1 Crea la tua istanza ACS

Dovresti vedere questo. Fare clic su **+ Aggiungi istanza**.

![AEM Assets](./images/accs2.png)

Compila i campi in questo modo:

- **Nome istanza**: `--aepUserLdap-- - ACCS`
- **Ambiente**: `Sandbox`
- **Area**: `North America`

Fai clic su **Aggiungi istanza**.

![AEM Assets](./images/accs3.png)

Creazione dell’istanza in corso. Questa operazione può richiedere 5-10 minuti.

![AEM Assets](./images/accs4.png)

Quando l’istanza è pronta, fai clic sull’istanza per aprirla.

![AEM Assets](./images/accs5.png)

## 1.5.1.2 Imposta l&#39;archivio CitiSignal

Dovresti vedere questo. Fai clic su **Accedi con Adobe ID**, quindi accedi.

![AEM Assets](./images/accs6.png)

Dopo aver effettuato l’accesso, dovresti visualizzare questa pagina home. Il primo passo è configurare l&#39;archivio CitiSignal in Commerce. Fare clic su **Archivi**.

![AEM Assets](./images/accs7.png)

Fare clic su **Tutti gli archivi**.

![AEM Assets](./images/accs8.png)

Fai clic su **Crea sito Web**.

![AEM Assets](./images/accs9.png)

Compila i campi in questo modo:

- **Nome**: `CitiSignal`
- **Codice**: `citisignal`

Fare clic su **Salva sito Web**.

![AEM Assets](./images/accs10.png)

Allora dovresti tornare qui. Fai clic su **Crea archivio**.

![AEM Assets](./images/accs11.png)

Compila i campi in questo modo:

- **Sito Web**: `CitiSignal`
- **Nome**: `CitiSignal`
- **Codice**: `citisignal`
- **Categoria principale**: `Default Category`

Fai clic su **Salva archivio**.

![AEM Assets](./images/accs12.png)

Allora dovresti tornare qui. Fare clic su **Crea visualizzazione archivio**.

![AEM Assets](./images/accs13.png)

Compila i campi in questo modo:

- **Archivio**: `CitiSignal`
- **Nome**: `CitiSignal`
- **Codice**: `citisignal`
- **Stato**: `Enabled`

Fai clic su **Salva visualizzazione archivio**.

![AEM Assets](./images/accs14.png)

Dovresti visualizzare questo messaggio. Fai clic su **OK**.

![AEM Assets](./images/accs15.png)

Allora dovresti tornare qui. Fare clic sul sito Web **CitiSignal** per aprirlo.

![AEM Assets](./images/accs16.png)

Selezionare la casella di controllo per impostare il sito Web come sito Web predefinito.

Fare clic su **Salva sito Web**.

![AEM Assets](./images/accs16a.png)

Allora dovresti tornare qui.

![AEM Assets](./images/accs16.png)

## 1.5.1.3 Configurare categorie e prodotti

Vai a **Catalogo** e seleziona **Categorie**.

![AEM Assets](./images/accs17.png)

Selezionare **Categoria predefinita**, quindi fare clic su **Aggiungi sottocategoria**.

![AEM Assets](./images/accs18.png)

Immettere il nome `Phones` e fare clic su **Salva**.

![AEM Assets](./images/accs19.png)

Selezionare **Categoria predefinita**, quindi fare di nuovo clic su **Aggiungi sottocategoria**.

![AEM Assets](./images/accs20.png)

Immettere il nome `Watches` e fare clic su **Salva**.

![AEM Assets](./images/accs21.png)

Dovresti quindi creare 2 categorie.

![AEM Assets](./images/accs22.png)

Quindi, passa a **Catalogo** e seleziona **Prodotti**.

![AEM Assets](./images/accs23.png)

Dovresti vedere questo. Fare clic su **Aggiungi prodotto**.

![AEM Assets](./images/accs24.png)

Configura il tuo prodotto in questo modo:

- **Nome prodotto**: `iPhone Air`
- **SKU**: `iPhone-Air`
- **Prezzo**: `999`
- **Quantità**: `10000`
- **Categorie**: selezionare `Phones`

Fai clic su **Salva**.

![AEM Assets](./images/accs25.png)

Scorri verso il basso fino a **Configurazioni** e fai clic su **Crea configurazioni**.

![AEM Assets](./images/accs26.png)

Dovresti vedere questo. Fare clic su **Crea nuovo attributo**.

![AEM Assets](./images/accs27.png)

Imposta **Etichetta predefinita** su `Storage`, quindi fai clic su **Aggiungi opzione** in **Gestisci opzioni**.

![AEM Assets](./images/accs28.png)

Configurare la prima opzione utilizzando il nome `256GB` in tutte e tre le colonne, quindi fare di nuovo clic su **Aggiungi opzione**.

![AEM Assets](./images/accs29.png)

Configurare la seconda opzione utilizzando il nome `512GB` in tutte e tre le colonne, quindi fare di nuovo clic su **Aggiungi opzione**.

![AEM Assets](./images/accs30.png)

Configurare la terza opzione utilizzando il nome `1TB` in tutte e 3 le colonne.

![AEM Assets](./images/accs31.png)

Scorri verso il basso fino a **Proprietà vetrina**. Imposta le seguenti opzioni su **Sì**:

- **Utilizzo nella ricerca**
- **Consenti tag HTML in Storefront**
- **Visibile nelle pagine del catalogo in Storefront**
- **Utilizzo nell&#39;elenco prodotti**

![AEM Assets](./images/accs32.png)

Scorri verso l&#39;alto e fai clic su **Salva attributo**.

![AEM Assets](./images/accs33.png)

Dovresti vedere questo. Selezionare entrambi gli attributi per **color** e **storage** e fare clic su **Next**.

![AEM Assets](./images/accs34.png)

Dovresti vedere questo. Ora devi aggiungere le opzioni di colore disponibili. A tale scopo, fare clic su **Crea nuovo valore**.

![AEM Assets](./images/accs35.png)

Immettere il valore `Sky-Blue` e fare clic su **Crea nuovo valore**.

![AEM Assets](./images/accs36.png)

Immettere il valore `Light-Gold` e fare clic su **Crea nuovo valore**.

![AEM Assets](./images/accs37.png)

Immettere il valore `Cloud-White` e fare clic su **Crea nuovo valore**.

![AEM Assets](./images/accs38.png)

Immettere il valore `Space-Black`. Fai clic su **Seleziona tutto**

![AEM Assets](./images/accs39.png)

Seleziona tutte e 3 le opzioni in **Archiviazione** e fai clic su **Avanti**.

![AEM Assets](./images/accs40.png)

Lascia le impostazioni predefinite e fai clic su **Avanti**.

![AEM Assets](./images/accs41.png)

Dovresti vedere questo. Fare clic su **Genera prodotti**.

![AEM Assets](./images/accs42.png)

Imposta la **quantità** di ciascun prodotto su `10000`. Fai clic su **Salva**.

![AEM Assets](./images/accs43.png)

Scorri verso il basso fino a **Prodotto nei siti Web** e seleziona la casella di controllo per **CitiSignal**.

Fai clic su **Salva**.

![AEM Assets](./images/accs44.png)

Fai clic su **Conferma**.

![AEM Assets](./images/accs45.png)

Dovresti vedere questo. Fai clic su **Indietro**.

![AEM Assets](./images/accs46.png)

Il prodotto **iPhone Air** e le relative varianti sono ora visualizzati nel catalogo prodotti.

![AEM Assets](./images/accs47.png)

Passaggio successivo: [Connetti ACS a AEM Sites CS/EDS Storefront](./ex2.md){target="_blank"}

Torna a [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

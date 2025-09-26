---
title: Collegare ACS ad AEM Sites CS/EDS Storefront
description: Collegare ACS ad AEM Sites CS/EDS Storefront
kt: 5342
doc-type: tutorial
exl-id: 81d826a8-c9f0-4e2a-9107-d6e06a4b8427
source-git-commit: 7280f6b7d3579226f2d8c7f94e75ca8d3f2941cc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 1.5.2 Collegamento di ACS ad AEM Sites CS/EDS Storefront

>[!IMPORTANT]
>
>Per completare questo esercizio, è necessario avere accesso a un ambiente AEM Sites e Assets CS funzionante con EDS.
>
>Se non si dispone ancora di un ambiente di questo tipo, passare all&#39;esercizio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Segui le istruzioni e potrai accedere a tale ambiente.

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Sites e Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

In questo esercizio collegherai la vetrina AEM Sites CS/EDS al backend ACS. Al momento, quando apri la tua vetrina AEM Sites CS/EDS e vai alla pagina dell&#39;elenco dei prodotti **Phone**, non trovi ancora alcun prodotto.

Al termine di questo esercizio, i prodotti configurati nell&#39;esercizio precedente verranno visualizzati nella pagina dell&#39;elenco dei prodotti **Phone** dello store AEM Sites CS/EDS.

![ACCS+AEM Sites](./images/accsaemsites0.png)

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Assicurarsi di trovarsi nell&#39;ambiente corretto, che deve essere denominato `--aepImsOrgName--`. Fare clic su **Commerce**.

![ACCS+AEM Sites](./images/accsaemsites1.png)

Fai clic sull&#39;icona **info** accanto all&#39;istanza ACS, che dovrebbe essere denominata `--aepUserLdap-- - ACCS`.

![ACCS+AEM Sites](./images/accsaemsites2.png)

Dovresti vedere questo. Copia l&#39;**endpoint GraphQL**.

![ACCS+AEM Sites](./images/accsaemsites3.png)

Vai a [https://da.live/app/adobe-commerce/storefront-tools/tools/config-generator/config-generator](https://da.live/app/adobe-commerce/storefront-tools/tools/config-generator/config-generator). Ora devi generare un file config.json che verrà utilizzato per collegare la vetrina AEM Sites CS al backend ACCS.

Nella pagina **Generatore di configurazioni**, incolla l&#39;**URL endpoint GraphQL** copiato.

Fai clic su **Genera**.

![ACCS+AEM Sites](./images/accsaemsites4.png)

Copia l’intero payload JSON generato.

![ACCS+AEM Sites](./images/accsaemsites5.png)

Vai all’archivio GitHub creato durante la configurazione dell’ambiente AEM Sites CS/EDS. L&#39;archivio è stato creato nell&#39;esercizio [1.1.2 Configurare l&#39;ambiente AEM CS](./../../../modules/asset-mgmt/module2.1/ex3.md){target="_blank"} e deve essere denominato **citisignal-aem-accs**.

![ACCS+AEM Sites](./images/accsaemsites6.png)

Nella directory principale, scorrere verso il basso e fare clic per aprire il file **config.json**.

![ACCS+AEM Sites](./images/accsaemsites7.png)

Fai clic sull&#39;icona **Modifica**.

![ACCS+AEM Sites](./images/accsaemsites8.png)

Rimuovi tutto il testo corrente e sostituiscilo incollando il payload JSON copiato nella pagina **Generatore di configurazioni**.

Fare clic su **Commit modifiche...**.

![ACCS+AEM Sites](./images/accsaemsites9.png)

Fai clic su **Commit modifiche**.

![ACCS+AEM Sites](./images/accsaemsites10.png)

Il file **config.json** è stato aggiornato. Dovresti vedere le modifiche sul sito web entro un paio di minuti. Per verificare se le modifiche sono state selezionate correttamente, vai alla pagina del prodotto **Telefoni**. Dovresti vedere **iPhone Air** visualizzato nella pagina.

Per accedere al tuo sito web, devi passare a `main--citisignal-aem-accs--XXX.aem.page` e/o `main--citisignal-aem-accs--XXX.aem.live`, dopo aver sostituito XXX con il tuo account utente GitHub, che in questo esempio è `woutervangeluwe`.

In questo esempio, l’URL completo diventa:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` e/o `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

![ACCS+AEM Sites](./images/accsaemsites11.png)

Ora che il prodotto è visualizzato correttamente, non è ancora disponibile un’immagine per il prodotto. Nel prossimo esercizio configurerai il collegamento con AEM Assets CS per le immagini del prodotto.

Passaggio successivo: [Connetti ACS ad AEM Assets CS](./ex3.md){target="_blank"}

Torna a [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

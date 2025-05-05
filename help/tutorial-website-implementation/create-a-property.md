---
title: Creare una proprietà tag
description: Scopri come accedere all’interfaccia di Data Collection e creare una proprietà tag. Questa lezione fa parte dell’esercitazione Implementare l’Experience Cloud su siti web.
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 54%

---

# Creare una proprietà tag

In questa lezione verrà creata la prima proprietà tag.

Una proprietà è fondamentalmente un contenitore che riempi con estensioni, regole, elementi dati e librerie durante la distribuzione di tag sul sito.

## Prerequisiti

Per completare le lezioni successive, devi disporre dell’autorizzazione per Develop, Approve, Publish, Manage Extensions e Manage Environments in tags. Se non riesci a completare nessuna di queste operazioni perché le opzioni dell’interfaccia utente non sono disponibili, rivolgiti al tuo amministratore Experience Cloud per richiedere l’accesso. Per ulteriori informazioni sulle autorizzazioni per gli utenti tag, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=it).

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto quando si utilizza questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Platform Launch Server Side è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=it)**
> * Le configurazioni di Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Accedi all’interfaccia utente di Data Collection
* Creare una nuova proprietà tag
* Configurare una proprietà tag

## Passa all’interfaccia di Data Collection

**Per accedere alla raccolta dati**

1. Accedi ad [Adobe Experience Cloud](https://experiencecloud.adobe.com).

1. Fai clic sull&#39;icona ![icona del commutatore della soluzione](images/launch-solutionSwitcher.png) per aprire il commutatore dell&#39;app

1. Seleziona **[!UICONTROL Launch/Data Collection]** dal menu ![Apri il commutatore della soluzione utilizzando l&#39;icona e fai clic su Launch/Data Collection](images/launch-solutionSwitcherActivation.png)

Ora dovresti visualizzare la `Tags Properties` schermata (se non sono state create proprietà nell’account, questa schermata potrebbe essere vuota):

![Schermata Proprietà](images/launch-propertiesScreen.png)

## Creare una proprietà

Una proprietà è fondamentalmente un contenitore che riempi con estensioni, regole, elementi dati e librerie durante la distribuzione di tag sul sito. Una proprietà può essere un raggruppamento di uno o più domini e sottodomini. Puoi gestire e tenere traccia di queste risorse in modo simile. Ad esempio, supponi di disporre di più siti Web basati su un modello e di voler tenere traccia delle stesse risorse su tutti. Puoi applicare una proprietà a più domini. Per ulteriori informazioni sulla creazione di proprietà, consulta [&quot;Aziende e proprietà&quot;](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=it) nella documentazione del prodotto.

**Creare una proprietà**

1. Fare clic sul pulsante **[!UICONTROL Nuova proprietà]**:

   ![Fare clic su Nuova proprietà](images/launch-addNewProperty.png)

1. Denomina la proprietà (ad esempio `Luma Tutorial` o `Luma Tutorial - Daniel`)
1. Come dominio, immetti `enablementadobe.com` poiché è il dominio in cui è ospitato il sito dimostrativo Luma. Anche se il campo &quot;Dominio&quot; è obbligatorio, la proprietà tag funzionerà su qualsiasi dominio in cui è implementata. Lo scopo principale di questo campo è precompilare le opzioni di menu nel Generatore di regole.
1. Espandi la sezione **[!UICONTROL Opzioni avanzate]** e seleziona la casella a **[!UICONTROL Esegui componenti regola in sequenza]**
1. Fai clic sul pulsante **[!UICONTROL Salva]**

   ![Creare una nuova proprietà](images/launch-newProperty.png)

La nuova proprietà deve essere visualizzata sulla pagina Proprietà. Tieni presente che se selezioni la casella accanto al nome della proprietà, le opzioni per **[!UICONTROL Configurare]** o **[!UICONTROL Eliminare]** la proprietà vengono visualizzate sopra l&#39;elenco delle proprietà. Fai clic sul nome della proprietà (ad es. `Luma Tutorial`) per aprire la schermata `Overview`.
![Fare clic sul nome della proprietà per aprirla](images/launch-openProperty.png)

[Avanti &quot;Aggiungere il codice di incorporamento&quot; >](add-embed-code.md)

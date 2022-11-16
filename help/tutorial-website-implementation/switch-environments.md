---
title: Cambiare ambienti di tag con Adobe Experience Cloud Debugger
description: Scopri come utilizzare il Experience Cloud Debugger per caricare diversi codici di incorporamento dei tag. Questa lezione fa parte dell’esercitazione Implementa l’Experience Cloud in siti web .
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 40%

---

# Cambiare ambienti di tag con il Experience Cloud Debugger

In questa lezione verrà utilizzato il [Estensione Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) per sostituire la proprietà tag hardcoded nel [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con la tua proprietà.

Questa tecnica si chiama cambio di ambiente e sarà utile in un secondo momento, quando lavori con i tag sul tuo sito web. Potrai caricare il tuo sito web di produzione nel tuo browser, ma con il tuo *sviluppo* ambiente tag. Questo ti consente di creare e convalidare le modifiche ai tag in modo indipendente dalle regolari versioni del codice.  Dopo tutto, questa separazione delle versioni dei tag di marketing dalle versioni regolari del codice è uno dei motivi principali per cui i clienti usano i tag in primo luogo!

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto durante l’utilizzo di questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Lato server di platform launch è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**


## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Utilizzare il debugger per caricare un ambiente tag alternativo
* Utilizza il debugger per verificare di aver caricato un ambiente tag alternativo

## Ottenere l’URL dell’ambiente di sviluppo

1. Nella proprietà tag , apri la `Environments` page

1. Nella riga **[!UICONTROL Sviluppo]**, fai clic sull’icona Installa ![icona Installa](images/launch-installIcon.png) per aprire il modale

1. Fai clic sull’icona Copia ![icona Copia](images/launch-copyIcon.png) per copiare il codice da incorporare negli Appunti

1. Fai clic su **[!UICONTROL Chiudi]** per chiudere il modale

   ![Icona di installazione](images/launch-copyInstallCode.png)

## Sostituire l’URL del tag nel sito di dimostrazione Luma

1. Apri il [sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) nel browser Chrome

1. Apri l’estensione [Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) facendo clic sull’icona dell’icona ![icona debugger](images/icon-debugger.png)

   ![Fai clic sull’icona Debugger](images/switchEnvironments-openDebugger.png)

1. La proprietà tag attualmente implementata viene visualizzata nella scheda Riepilogo

   ![ambiente tag mostrato in Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Passa alla scheda Strumenti
1. Scorri fino alla sezione **[!UICONTROL Sostituisci codice di incorporamento Launch]**
1. Assicurati che la scheda Chrome con il sito Luma sia attiva dietro al debugger (non la scheda con questa esercitazione o la scheda con l’interfaccia di raccolta dati).  Incolla nel campo di input il codice di incorporamento presente negli Appunti
1. Attiva la funzione &quot;Applica in luma.enablementadobe.com&quot; in modo che tutte le pagine del sito Luma vengano mappate sulla tua proprietà tag
1. Fai clic sul pulsante **[!UICONTROL Salva]**.

   ![ambiente tag mostrato in Debugger](images/switchEnvironments-debugger-save.png)

1. Ricarica il sito Luma e seleziona la scheda Riepilogo del debugger. Nella sezione Launch, dovresti notare che è in uso la tua Proprietà di sviluppo. Assicurati che il Nome della proprietà corrisponda a quello della tua e che l’Ambiente indichi &quot;sviluppo&quot;.

   ![ambiente tag mostrato in Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>Debugger salverà questa configurazione e sostituirà i codici di incorporamento dei tag ogni volta che vieni reindirizzato al sito Luma. Questo non coinvolge altri siti visitati in altre schede aperte. Per impedire che il debugger sostituisca il codice di incorporamento, fai clic sul pulsante **[!UICONTROL Rimuovi]** accanto al codice di incorporamento nella scheda Strumenti del debugger.

Continuando l’esercitazione, utilizzerai questa tecnica per mappare il sito Luma sulla tua proprietà tag per convalidare l’implementazione dei tag. Quando inizi a utilizzare i tag sul sito web di produzione, puoi usare la stessa tecnica per convalidare le modifiche.

[Avanti “Aggiungere il servizio Adobe Experience Platform Identity” >](id-service.md)

---
title: Cambiare ambienti di tag con Adobe Experience Cloud Debugger
description: Scopri come utilizzare il Experience Cloud Debugger per caricare diversi codici di incorporamento di tag. Questa lezione fa parte dell’esercitazione Implementare l’Experience Cloud su siti web.
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 36%

---

# Cambiare ambienti di tag con il Experience Cloud Debugger

In questa lezione verrà utilizzato il [Estensione Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) per sostituire la proprietà di tag in codifica fissa [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con la tua proprietà.

Questa tecnica è denominata cambio di ambiente e sarà utile in un secondo momento, quando lavorerai con i tag sul tuo sito web. Potrai caricare il tuo sito web di produzione nel browser, ma con il tuo *sviluppo* ambiente di tag. Questo ti consente di creare e convalidare le modifiche ai tag in modo indipendente dalle regolari versioni del codice.  Dopo tutto, questa separazione tra versioni di tag di marketing e versioni di codice è uno dei motivi principali per cui i clienti utilizzano i tag.

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto quando si utilizza questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Platform launch Server Side è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni Edge ora sono **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Utilizzare il debugger per caricare un ambiente di tag alternativo
* Utilizza Debugger per verificare di aver caricato un ambiente di tag alternativo

## Ottenere l’URL dell’ambiente di sviluppo

1. Nella proprietà tag, apri la `Environments` pagina

1. Nella riga **[!UICONTROL Sviluppo]**, fai clic sull’icona Installa ![icona Installa](images/launch-installIcon.png) per aprire il modale

1. Fai clic sull’icona Copia ![icona Copia](images/launch-copyIcon.png) per copiare il codice da incorporare negli Appunti

1. Fai clic su **[!UICONTROL Chiudi]** per chiudere il modale

   ![Icona di installazione](images/launch-copyInstallCode.png)

## Sostituire l’URL del tag nel sito di dimostrazione Luma

1. Apri il [sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) nel browser Chrome

1. Apri [Estensione Experienci Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) facendo clic su ![Icona debugger](images/icon-debugger.png) icona

   ![Fai clic sull’icona Debugger](images/switchEnvironments-openDebugger.png)

1. La proprietà del tag attualmente implementata viene visualizzata nella scheda Riepilogo

   ![ambiente di tag visualizzato in Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Passa alla scheda Strumenti
1. Scorri fino alla sezione **[!UICONTROL Sostituisci codice di incorporamento Launch]**
1. Assicurati che la scheda Chrome con il sito Luma sia attiva dietro al debugger (non la scheda con questa esercitazione o la scheda con l’interfaccia di Data Collection).  Incolla nel campo di input il codice di incorporamento presente negli Appunti
1. Attiva la funzione &quot;Applica in luma.enablementadobe.com&quot; in modo che tutte le pagine del sito Luma vengano mappate sulla proprietà tag
1. Fai clic sul pulsante **[!UICONTROL Salva]**.

   ![ambiente di tag visualizzato in Debugger](images/switchEnvironments-debugger-save.png)

1. Ricarica il sito Luma e seleziona la scheda Riepilogo del debugger. Nella sezione Launch, dovresti notare che è in uso la tua Proprietà di sviluppo. Assicurati che il Nome della proprietà corrisponda a quello della tua e che l’Ambiente indichi &quot;sviluppo&quot;.

   ![ambiente di tag visualizzato in Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>Il debugger salverà questa configurazione e sostituirà i codici di incorporamento dei tag ogni volta che vieni reindirizzato al sito Luma. Questo non coinvolge altri siti visitati in altre schede aperte. Per impedire che il debugger sostituisca il codice di incorporamento, fai clic sul pulsante **[!UICONTROL Rimuovi]** accanto al codice di incorporamento nella scheda Strumenti del debugger.

Continuando l’esercitazione, utilizzerai questa tecnica per mappare il sito Luma sulla tua proprietà tag per convalidare l’implementazione dei tag. Quando inizi a utilizzare i tag sul sito web di produzione, puoi usare questa stessa tecnica per convalidare le modifiche.

[Avanti “Aggiungere il servizio Adobe Experience Platform Identity” >](id-service.md)

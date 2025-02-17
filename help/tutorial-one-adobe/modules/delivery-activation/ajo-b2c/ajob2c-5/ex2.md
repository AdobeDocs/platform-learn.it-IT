---
title: Creare una campagna con i servizi di traduzione AJO
description: Creare una campagna con i servizi di traduzione AJO
kt: 5342
doc-type: tutorial
exl-id: 536caf45-c614-48e8-adbb-6dc67d1a9606
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 3.5.2 Creare la campagna

Vai a [https://experience.adobe.com/](https://experience.adobe.com/). Fare clic su **Journey Optimizer**.

![Traduzioni](./images/ajolp1.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`.

![ACOP](./images/ajolp2.png)

>[!NOTE]
>
>Se hai già creato i frammenti di intestazione e piè di pagina come parte dell&#39;esercizio [esercizio 3.1.2.1](./../ajob2c-1/ex2.md) e dell&#39;esercizio [esercizio 3.1.2.2](./../ajob2c-1/ex2.md), passa all&#39;esercizio 3.5.2.3 Crea campagna in fibra. Non creare più frammenti di intestazione e piè di pagina.

## 3.5.2.1 Creare il frammento di intestazione

Nel menu a sinistra, fai clic su **Frammenti**. Un frammento è un componente riutilizzabile all’interno di Journey Optimizer che evita la duplicazione e facilita le modifiche future che dovrebbero interessare tutti i messaggi, come le modifiche a un’intestazione o a un piè di pagina in un messaggio e-mail.

Fare clic su **Crea frammento**.

![ACOP](./images/fragm1.png)

Immettere il nome `--aepUserLdap-- - CitiSignal - Header` e selezionare **Tipo: frammento visivo**. Fai clic su **Crea**.

![ACOP](./images/fragm2.png)

Poi vedrai questo. Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

Trascina e rilascia una **colonna 1:1** dal menu nell&#39;area di lavoro. Questo sarà il segnaposto per l&#39;immagine del logo.

![Journey Optimizer](./images/fragm3.png)

Successivamente, puoi utilizzare i Componenti contenuto per aggiungere contenuto all’interno di questi blocchi. Trascina e rilascia un componente **Immagine** nella prima cella della prima riga. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/fragm4.png)

Viene visualizzata un’apertura a comparsa con la libreria multimediale di AEM Assets. Vai alla cartella **citi-signal-images**, fai clic per selezionare l&#39;immagine **CitiSignal-Logo-White.png** e fai clic su **Select**.

>[!NOTE]
>
>Se non trovi le immagini Citi Signal nella tua libreria AEM Assets, puoi trovarle [qui](./../../../../assets/ajo/CitiSignal-images.zip). Scaricali sul desktop, crea la cartella **citi-signal-images** e carica tutte le immagini in quella cartella.

![Journey Optimizer](./images/fragm5.png)

Poi vedrai questo. L&#39;immagine è bianca e non è ancora visualizzata. A questo punto è necessario definire un colore di sfondo per la corretta visualizzazione dell&#39;immagine. Fai clic su **Stili**, quindi fai clic sulla casella **Colore di sfondo**.

![Journey Optimizer](./images/fragm6.png)

Nel popup, cambiare il codice colore **Hex** in **#8821F4** e quindi cambiare lo stato attivo facendo clic nel campo **100%**. Viene quindi visualizzato il nuovo colore applicato all&#39;immagine.

![Journey Optimizer](./images/fragm7.png)

L&#39;immagine è anche un po&#39; troppo grande in questo momento. Modifichiamo la larghezza facendo scorrere il commutatore **Larghezza** in **40%**.

![Journey Optimizer](./images/fragm8.png)

Il frammento di intestazione è ora pronto. Fai clic su **Salva**, quindi fai clic sulla freccia per tornare alla schermata precedente.

![Journey Optimizer](./images/fragm9.png)

Il frammento deve essere pubblicato prima di poter essere utilizzato. Fai clic su **Pubblica**.

![Journey Optimizer](./images/fragm10.png)

Dopo alcuni minuti, lo stato del frammento sarà **Live**.
Successivamente, devi creare un nuovo frammento per il piè di pagina dei messaggi e-mail. Fare clic su **Crea frammento**.

![Journey Optimizer](./images/fragm11.png)

## 3.5.2.2 Creare il frammento di piè di pagina

Fare clic su **Crea frammento**.

![Journey Optimizer](./images/fragm11.png)

Immettere il nome `--aepUserLdap-- - CitiSignal - Footer` e selezionare **Tipo: frammento visivo**. Fai clic su **Crea**.

![Journey Optimizer](./images/fragm12.png)

Poi vedrai questo. Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

Trascina e rilascia una **colonna 1:1** dal menu nell&#39;area di lavoro. Questo sarà il segnaposto per il contenuto del piè di pagina.

![Journey Optimizer](./images/fragm13.png)

Successivamente, puoi utilizzare i Componenti contenuto per aggiungere contenuto all’interno di questi blocchi. Trascina e rilascia un componente **HTML** nella prima cella della prima riga. Fare clic sul componente per selezionarlo, quindi fare clic sull&#39;icona **&lt;/>** per modificare il codice sorgente di HTML.

![Journey Optimizer](./images/fragm14.png)

Poi vedrai questo.

![Journey Optimizer](./images/fragm15.png)

Copia il frammento di codice HTML seguente e incollalo nella finestra **Modifica HTML** in Journey Optimizer.

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

Allora avrai questo. Alle righe 7, 12 e 17 ora devi inserire un file di immagine, utilizzando le risorse nella libreria di AEM Assets.

![Journey Optimizer](./images/fragm16.png)

Verificare che il cursore si trovi nella riga 7, quindi scegliere **Assets** dal menu a sinistra. Fai clic su **Apri selettore risorse** per selezionare l&#39;immagine.

![Journey Optimizer](./images/fragm17.png)

Apri la cartella **citi-signal-images** e fai clic per selezionare l&#39;immagine **Icon_Facebook.png**. Fai clic su **Seleziona**.

![Journey Optimizer](./images/fragm18.png)

Assicurati che il cursore si trovi sulla riga 12, quindi fai clic su **Apri selettore risorse** per selezionare l&#39;immagine.

![Journey Optimizer](./images/fragm19.png)

Apri la cartella **citi-signal-images** e fai clic per selezionare l&#39;immagine **Icon_X.png**. Fai clic su **Seleziona**.

![Journey Optimizer](./images/fragm20.png)

Assicurati che il cursore si trovi alla riga 17, quindi fai clic su **Apri selettore risorse** per selezionare l&#39;immagine.

![Journey Optimizer](./images/fragm21.png)

Apri la cartella **citi-signal-images** e fai clic per selezionare l&#39;immagine **Icon_Instagram.png**. Fai clic su **Seleziona**.

![Journey Optimizer](./images/fragm22.png)

Poi vedrai questo. Fai clic su **Salva**.

![Journey Optimizer](./images/fragm23.png)

Tornerai nell&#39;editor. Le icone non sono ancora visibili perché lo sfondo e i file di immagine sono tutti in bianco. Per cambiare il colore di sfondo, passa a **Stili** e fai clic sulla casella di controllo **Colore di sfondo**.

![Journey Optimizer](./images/fragm24.png)

Cambia il codice colore **Hex** in **#000000**.

![Journey Optimizer](./images/fragm25.png)

Modifica l’allineamento in modo che sia centrato.

![Journey Optimizer](./images/fragm26.png)

Aggiungiamo altre parti al piè di pagina. Trascina e rilascia un componente **Immagine** sopra il componente HTML appena creato. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/fragm27.png)

Fare clic per selezionare il file di immagine **`CitiSignal_Footer_Logo.png`** e fare clic su **Seleziona**.

![Journey Optimizer](./images/fragm28.png)

Passa a **Stili** e fai clic sulla casella di controllo **Colore di sfondo**. Torniamo a usare il nero. Cambia il codice colore **Hex** in **#000000**.

![Journey Optimizer](./images/fragm29.png)

Modifica la larghezza in **20%** e verifica che l&#39;allineamento sia impostato per essere centrato.

![Journey Optimizer](./images/fragm30.png)

Trascina e rilascia un componente **Testo** sotto il componente HTML creato. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/fragm31.png)

Copiare e incollare il testo seguente sostituendo il testo segnaposto.

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

Imposta l&#39;allineamento **Testo** da centrare.

![Journey Optimizer](./images/fragm32.png)

Cambia **Colore carattere** in bianco, **#FFFFFF**.

![Journey Optimizer](./images/fragm33.png)

Cambia il **colore di sfondo** in nero, **#000000**.

![Journey Optimizer](./images/fragm34.png)

Selezionare il testo **Annulla sottoscrizione** nel piè di pagina e fare clic sull&#39;icona **Collegamento** nella barra dei menu. Imposta **Type** su **External Opt-out/Unsubscription** e imposta l&#39;URL su **https://aepdemo.net/unsubscribe.html** (non è consentito avere un URL vuoto per il collegamento di annullamento dell&#39;abbonamento).

![Journey Optimizer](./images/fragm35.png)

Allora avrai questo. Il piè di pagina è pronto. Fare clic su **Salva** e quindi sulla freccia per tornare alla pagina precedente.

![Journey Optimizer](./images/fragm36.png)

Fai clic su **Pubblica** per pubblicare il piè di pagina in modo che possa essere utilizzato in un&#39;e-mail.

![Journey Optimizer](./images/fragm37.png)

Dopo alcuni minuti lo stato del piè di pagina verrà modificato in **Live**.

![Journey Optimizer](./images/fragm38.png)

## 3.5.2.3 Creare una campagna in fibra ottica

Ora creerai una campagna. A differenza del percorso basato sugli eventi dell’esercizio precedente, che si basa su eventi di esperienza o entrate o uscite di pubblico in arrivo per attivare un percorso per 1 cliente specifico, le campagne sono indirizzate a un intero pubblico una volta con contenuti univoci come newsletter, promozioni una tantum o informazioni generiche, oppure periodicamente con contenuti simili inviati regolarmente, come ad esempio campagne e promemoria di compleanno.

Nel menu, vai a **Campagne** e fai clic su **Crea campagna**.

![Journey Optimizer](./images/oc43.png)

Seleziona **Pianificato - Marketing** e fai clic su **Crea**.

![Journey Optimizer](./images/campaign1.png)

Nella schermata di creazione della campagna, configura quanto segue:

- **Nome**: `--aepUserLdap-- - CitiSignal Fiber`.
- **Descrizione**: Campagna in fibra
- **Tipo di identità**: modifica in E-mail

![Journey Optimizer](./images/campaign2.png)

Scorri verso il basso fino a **Azione**. Per **Azione**, seleziona **E-mail**.

![Journey Optimizer](./images/campaign3.png)

Quindi, seleziona una **configurazione e-mail** esistente. Il contenuto verrà modificato in un paio di minuti.

![Journey Optimizer](./images/campaign3a.png)

Scorri fino a **Pubblico**. Fai clic su **Seleziona pubblico**.

![Journey Optimizer](./images/campaign2b.png)

Per il **pubblico**, selezionare il pubblico creato in [1.3.3 Creare una composizione federata](./../../datacollection/dc1.3/ex3.md), denominata `--aepUserLdap-- - CitiSignal Eligible for Fiber`. Fai clic su **Salva**.

![Journey Optimizer](./images/campaign2a.png)

Scorri verso il basso fino a **Pianificazione**. Per la **Pianificazione**, scegli **In una data e un&#39;ora specifiche** e imposta un&#39;ora a scelta.

![Journey Optimizer](./images/campaign4.png)

Ora puoi iniziare a creare il messaggio e-mail stesso. Scorri verso l&#39;alto e fai clic su **Modifica contenuto**.

![Journey Optimizer](./images/campaign5.png)

Poi vedrai questo. Per la **riga oggetto**, utilizza:

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

Quindi, fare clic su **Modifica corpo e-mail**.

![Journey Optimizer](./images/campaign6.png)

Scegli **Progettazione da zero**.

![Journey Optimizer](./images/campaign7.png)

Poi vedrai questo. Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

Trascina e rilascia 4 volte una **colonna 1:1** nell&#39;area di lavoro, per ottenere la seguente struttura:

![Journey Optimizer](./images/campaign8.png)

Nel menu a sinistra, vai a **Frammenti**. Trascina l’intestazione creata in precedenza sul primo componente nell’area di lavoro. Trascinare il piè di pagina creato in precedenza sull&#39;ultimo componente dell&#39;area di lavoro.

![Journey Optimizer](./images/campaign9.png)

Fai clic sull&#39;icona **+** nel menu a sinistra. Vai a **Sommario** per iniziare ad aggiungere contenuti all&#39;area di lavoro.

![Journey Optimizer](./images/campaign10.png)

Trascina e rilascia un componente **Testo** sulla seconda riga.

![Journey Optimizer](./images/campaign11.png)

Selezionare il testo predefinito nel componente **Digitare qui il testo.** e sostituirlo con il testo seguente. Cambia l&#39;allineamento in **Allineamento al centro**.

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal customer, you're in pole position to discover our new Fiber offering. Have a look at the below offer and update your contract!

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

Trascina e rilascia un componente **Immagine** sulla terza riga. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/campaign13.png)

Seleziona l’archivio AEM Assets creato come parte dei moduli precedenti. L&#39;archivio deve essere denominato `--aepUserLdap-- - Citi Signal dev`. Fare clic per aprire la cartella `--aepUserLdap-- - Workfront Assets`.

![Journey Optimizer](./images/campaign15a.png)

Fai clic per selezionare l&#39;immagine **2048x2048_buynow.png** e fai clic su **Seleziona**.

![Journey Optimizer](./images/campaign14.png)

L’e-mail della newsletter di base è ora pronta. Fai clic su **Salva**.

![Journey Optimizer](./images/ready.png)

Torna al dashboard della campagna facendo clic sulla **freccia** accanto al testo dell&#39;oggetto nell&#39;angolo in alto a sinistra.

![Journey Optimizer](./images/campaign19.png)

Fai clic su **Rivedi per attivare**.

![Journey Optimizer](./images/campaign20.png)

L&#39;errore potrebbe quindi essere visualizzato. In questo caso, potresti dover aspettare fino a 24 ore prima che il pubblico sia stato valutato, quindi provare di nuovo ad attivare la campagna. Potrebbe essere inoltre necessario aggiornare la pianificazione della campagna per eseguirla in un secondo momento.

![Journey Optimizer](./images/campaign21a.png)

Fare clic su **Attiva**.

![Journey Optimizer](./images/campaign21.png)

Una volta attivata, la campagna verrà pianificata per l’esecuzione.

![Journey Optimizer](./images/campaign22.png)

Hai finito questo esercizio.

## Passaggi successivi

Vai a [3.5.3 Aggiungi lingue al tuo indirizzo e-mail](./ex3.md)

Torna a [Adobe Journey Optimizer: Servizi di traduzione](./ajotranslationsvcs.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}

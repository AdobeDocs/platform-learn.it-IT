---
title: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo percorso e push - Brasile notifica
description: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo percorso e push - Brasile notifica
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 2%

---

# 3.3 Crie sua jornada e notificação push

Neste exercício, você irá configurar a jornada e a mensagem que precisa ser acionada quando alguém inserir uma sinalização (beacon) o aplicativo móvel.

Accesso Faça su Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clipart **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da a **Pagina principale** niente Journey Optimizer. Primeiro se você está germente sandbox corrispondente. O nome do sandbox que dev ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selione o sandbox na lista. Neste esempio, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Pagina principale**  sandbox da fare `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

Nessun menu à esquerda, clique em **Percorsi**. Em seguida, clique em **Crea Percorso** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Nessun exercício anteriore, você criou um novo **Evento**. Você nomeou o evento `yourLastNameBeaconEntryEvent` e sostituito `yourLastName` pelo seu sobrenome. Este foi o risultanti da criação do evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. Sua Jornada agora deve ser semelhante ao seguinte. Clipart **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Azioni**, selione a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você Deve criar sua notificação push.

Definisci a **Categoria** como **Marketing** e selecione um push Surface que permite enviar notificações push. Nesse caso, una superfície spingere un utente selionada é **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

Clipart **Modifica contenuto**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo será exibida:

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação push.

Clique no campo de texto **Titolo**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalização para o campo **Nome** que está armazenado em `profile.person.name.firstName`. Nessun menu à esquerda, selione **Attributi del profilo**, ruolo para baixo/navegue para encontrar o **Persona** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. Clipart **Salva**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personalização ao lado campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em  **Attributi contestuali** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clipart **Eventi**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que dev ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clipart **Posizionare il contesto**.

![ACOP](./images/jomsg6.png)

Clipart **Interazione POI**.

![ACOP](./images/jomsg7.png)

Clipart **Dettagli POI**.

![ACOP](./images/jomsg8.png)

Cliff no **+** icona no **Nome POI**.
Em seguida, o seguinte será exibido. Clipart **Salva**.

![ACOP](./images/jomsg9.png)

Sua Mensagem agora está pronta. Clique na seta no canto superiore esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clipart **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você adicionar uma ação  **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Azioni**, selione a ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publar uma mensagem no **Endpoint** usado pela exibição na loja. A ação **sendMessageToScreen** espera que múltiplas variáveis sejam definidas. Você pode visalizaliziana essas variáveis rolando para baixo até ver **Parametri azione**.

![ACOP](./images/jomsg16.png)

Agora você precisa definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são necessários e onde.

| Parametro | Valore  |
|:-------------:| :---------------:|
| CONSEGNA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERIA | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Para definir esses valores, clique no ícone **Modifica**.

![ACOP](./images/jomsg17.png)

Em seguida, selione **Modalità avanzata**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clipart **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse sette sella adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de sostituir  `yourLastName` pelo seu sobrenome.

O risultante sviluppo sostenibile semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Ruolo per la cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Devi ancora dare un Nome al tuo percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra sullo schermo.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jornada aqui. Seleziona `yourLastName - Beacon Entry Journey`. Clipart **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode pubblicitario sua jornada clicando em **Pubblica**.

![ACOP](./images/publishjourney.png)

Clipart **Pubblica** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício.

Próxima etapa: [3.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)

---
title: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail - Brasile
description: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensagem de mail

Neste exercício, você irá configurar a jornada que precisa ser acionada quando alguém parar uma conta no site de dimostração.

Accesso Faça su Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clipart **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da a **Pagina principale**  niente Journey Optimizer. Primeiro se você está germente sandbox corrispondente. O nome do sandbox que dev ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selione o sandbox na lista. Neste esempio, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Pagina principale** sandbox da fare `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Crie a sua jornada

Nessun menu à esquerda, clique em **Percorsi**. Em seguida, clique em **Crea Percorso** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Nessun exercício anteriore, você criou um novo **Evento**. Você nomeou o evento `yourLastNameAccountCreationEvent` e sostituito `yourLastName` pelo seu sobrenome. Este foi o risultanti da criação do evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada. Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você adicionar uma etapa curta de **Wait**. Vá para o lado esquerdo da tela a seção **Orchestrazione** para encontrar isso. Você usará atributos de perfil e precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo reale.

![ACOP](./images/journeywait.png)

Sua Jornada agora deve ser semelhante ao seguinte. No lado direito da tela você precisa configurar o tempo de espera. Defina como 1 . Isso dará bastante tempo para que os atributos do perfil estejam disponíveis após o disparo do evento.

![ACOP](./images/journeywait1.png)

Clipart **Ok** para salvar suas alterações.

Como terceira etapa da jornada, você adicionar uma ação **E-mail**. Vá para o lado esquerdo da tela para **Azioni**, selione a ação **E-mail** e arraste e solte a ação no segundo nó da sua jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Imposta la **Categoria** a **Marketing** e seleziona una superficie e-mail che ti consente di inviare e-mail. In questo caso, la superficie dell’e-mail da selezionare è **E-mail**. Assicurati che le caselle di controllo per **Clic su e-mail** e **aperture e-mail** sono entrambi abilitati.

Definisci a **Categoria** como **Marketing** e selecione uma superfície de e-mail que permita o envio de mail. Nesse caso, una superfície e-mail un utente selionada é E-mail. Certifique se de que as caixas de seleção **Clic su e-mail** e **aperture e-mail** estejam marcadas.

![ACOP](./images/journeyactions1.png)

Un próximo etapa é criar sua mensagem. Para isso, clique em **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, clique em **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Linea oggetto**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de ainda não está. Em seguida, você precisa trazer o token de personalização para o **Nome** que está armazenado em `profile.person.name.firstName`. Nessun menu à esquerda, ruolo para baixo para encontrar o **Persona** e clique na seta para ir um nível mais profundo.

![Journey Optimizer](./images/msg7.png)

Agora incontra o costa **Nome completo** e clique na seta para ir um nível mais profundo.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **Nome** e clique no símbolo **+**  ao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **agradecemos a sua inscrição!** Clique em Salvar. . Clipart **Salva**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Clipart **E-mail Designer**  para criar o conteúdo e-mail.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solicitado que você forneça o conteúdo e-mail através de 3 métodos diferentes:

- **Progettazione da zero**: Comece com uma tela em branco e usa l&#39;editor WYSIWYG para arrastar e soltar a estrutura e os components de conteúdo para criar visualmente o conteúdo do e-mail.
- **Codice personalizzato**: Crie seu prómodelo de e-mail codificando HTML
- **Importa HTML**: Importe um modelo HTML esistente, que você poderá editar.

Clipart **Importa HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [qui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail padrão:

![Journey Optimizer](./images/msg14.png)

Vamos personalizar o e-mail. Clique ao lado fare testo **Olá** e, em seguida, clique no ícone **Aggiungi personalizzazione**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o token de personalização **Nome** que está armazenado em `profile.person.name.firstName`. Nessun menu, localize o **Persona**, faça uma detalhada no **Nome completo** e clique no ícone **+** para adicionar o campo **Nome** redattore del ao de espressão.

Clipart **Salva**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clipart **Salva** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o antidel de mensagens clicando na seta ao lado texto da linha de no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você conclude un criação do seu e-mail de cadastro. Clique na seta no canto superiore esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

Clipart **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Pubblicazione di una sua jornada

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone **Proprietà** nessun canto superiore direito da tela.

![ACOP](./images/journeyname.png)

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone `yourLastName - Account Creation Journey`. Clipart **OK** para salvar come mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode pubblicitario sua jornada clicando em **Pubblica**.

![ACOP](./images/publishjourney.png)

Clipart **Pubblica**  novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este exercício.

Próxima etapa: [2.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
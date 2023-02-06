---
title: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento ad Adobe Target - Brasile
description: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento ad Adobe Target - Brasile
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 1.4 Ação: Inviate seu segmento para o Adobe Target

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você precisa selionar um **sandbox**. O nome fare sandbox un ser selionado é Bootcamp. É possível fazer isso clicando nessun texto **[!UICONTROL Produzione Prod]** na linha azul na parte superior da tela. depois de selionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedica.

![Acquisizione dei dati](./images/sb1.png)

## 1.4.1 Ative seu segmento para destino do Adobe Target

O Adobe Target está disponível como destino do CDP em tempo reale. Para configurar sua integração com o Adobe Target, acesse **Destinazioni** e **Catalogo**.

Clipart **Personalizzazione** nessun menu **Categorie**. Você verá o cartão de destino **Adobe Target**. Clipart **Attiva segmenti**.

![AT](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` cricca **Successivo**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selione o segmento que você criou em [1.3 Crite um segmento](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Successivo**.

![AT](./images/atdest8.png)

Na próxima página, clique em **Successivo**.

![AT](./images/atdest9.png)

Clipart **Fine**.

![AT](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediapós criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que to destino seja ativado. Este é um tempo de espera único devido à definição da configuração de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end forem conclusioni, os segmentos de borda recém-adicionados que são enviados ao destino do Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configurare sua atividade baseada em formulário do Adobe Target

Agora que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível configurar sua atividade de Segmentação por experiência su Adobe Target. Neste exercício, você irá configurar uma atividade baseada no Visual Experience Composer (Compositore esperienza visivo).

Acesse a página inicial da Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clipart **Target** para abrir.

![RTCDP](./images/excl.png)

Sulla **Adobe Target** nella home page verranno visualizzate tutte le attività esistenti.
Fai clic su **+ Crea attività** per creare una nuova attività.
Na página inicial do **Adobe Target**você verá todas as atividades esiste.
Clipart **+ Crea attività** parcriar uma nova atividade.

![RTCDP](./images/exclatov.png)

Selecione **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visivo** e defina **URL attività** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, sostituito XX por um número entre 01 e 30.

>[!IMPORTANT]
>
>Cada partecipante da condensitação deve usar uma página da Web separada para evar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e encontrar un URL acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas páginas compartilham a mesma URL base e terminam com o número do partecipante.
>
>Por esempio, o partecipante 1 deve usar un URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o partecipante 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selezione dell&#39;area di lavoro **AT Bootcamp**.

Clipart **Successivo**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer (Compositore esperienza visivo). Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

Atualmente o público padrão são **Tutti i visitatori**. N. di cricca **3 punti** ao lado **Tutti i visitatori** e clique em **Cambia pubblico**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o o segmento da Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. Selecione o segmento que você criou anteriormente na Adobe Experience Platform. Clipart **Assegna pubblico**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar un caporedattore di immagini, você deve clicar em **Consenti tutto** nessun banner de cookies.

Para isso, vá para **Sfoglia**

![RTCDP](./images/cook1.png)

Em seguida, clique em **Consenti tutto**.

![RTCDP](./images/cook2.png)

Em seguida, retorne para **Componi**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **Sostituisci contenuto** e selione **Immagine**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Selecione e clique em **Salva**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público selionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, utilizzare:

- `yourLastName - RTCDP - XT (VEC)`

Clipart **Successivo**.

![RTCDP](./images/atform8.png)

Clipart **Successivo**.

![RTCDP](./images/atform8a.png)

Página **Obiettivi e impostazioni**, acesse **Metriche dell&#39;obiettivo**.

![RTCDP](./images/atform9.png)

Definizione di un como Meta principal **Coinvolgimento** - **Time On Site**. Clipart **Salva e chiudi**.

![RTCDP](./images/vec3.png)

Agora você está na página **Panoramica dell’attività**. Você ainda precisa ativar sua Atividade.

![RTCDP](./images/atform10.png)

Clik senza campo **Inattivo** e selione **Attiva**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de dimostração e visitar a página do produto para **Real-Time CDP**, você se Qualará instantaneamente para o segmento que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada partecipante da condensitação deve usar uma página da Web separada para evar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e encontra un URL acessando ao link: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas páginas compartilham a mesma URL base e terminam com o número do partecipante.
>
>Por esempio, o partecipante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o partecipante 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Intervenire: inviare il segmento a Facebook](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)

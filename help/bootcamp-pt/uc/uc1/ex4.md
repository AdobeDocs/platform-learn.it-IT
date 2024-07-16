---
title: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento ad Adobe Target - Brasile
description: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento ad Adobe Target - Brasile
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 Ação: envie seu para o Adobe Target

[Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

## 1.4.1 Seu attiva para o destino do Adobe Target

O Adobe Target está disponível como um destino do CDP em tempo real. Para configurar sua integração com o Adobe Target, acesse **Destinazioni** e **Catalogo**.

Clique em **Personalization** senza menu **Categorie**. Você verá o cartão de destino do **Adobe Target**. **Attiva segmenti**.

![ALLE](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` e cricca **Successivo**.

![ALLE](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o você criou em [1.3 Crie um](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, cricca em **Avanti**.

![ALLE](./images/atdest8.png)

Na próxima página, cricca em **Successiva**.

![ALLE](./images/atdest9.png)

**Fine**.

![ALLE](./images/atdest10.png)

Seu agora está ativado para o Adobe Target.

![ALLE](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este é um tempo de espera único devido à definição da configuração de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end forem concluídos, os segmentos de borda recém-adicionados que são enviados ao destino do Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configurare sua atividade su Adobe Target

Agora que seu Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você irá configurar uma atividade baseada no Visual Experience Composer (Compositore esperienza visivo)

Acesse a página inicial da Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas as atividades exists.
Clique em **+ Crea attività** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visivo** e definisce un **URL attività** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 e 60.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e encontrar a URL acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Páginas compartilham è una base URL mesma e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selezionare l&#39;area di lavoro **AT Bootcamp**.

**Avanti**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está no Visual Experience Composer (Compositore esperienza visivo). Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **Tutti i visitatori**. N. cricca **3 punti** ao lado de **Tutti i visitatori** e N. cricca **Cambia pubblico**.

![RTCDP](./images/atform3.png)

Agora você está vendendo una lista de públicos disponíveis, e o da Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. Selecione o você criou anteriormente a una Adobe Experience Platform. **Assegna pubblico**.

![RTCDP](./images/exclatvecchaud.png)

Seu da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, você deve clicar em **Consenti a tutti** nessun banner de cookies.

Para isso, vá para **Sfoglia**

![RTCDP](./images/cook1.png)

Em seguida, cricca em **Consenti tutti**.

![RTCDP](./images/cook2.png)

Em seguida, nuovo para **Componi**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **Sostituisci contenuto** e selecione **Immagine**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Selecione e cricca em **Salva**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Cricca no título da sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, usare:

- `seuSobrenome - RTCDP - XT (VEC)`

**Avanti**.

![RTCDP](./images/atform8.png)

**Avanti**.

![RTCDP](./images/atform8a.png)

Na página **Obiettivi e impostazioni**, **Metriche obiettivo**.

![RTCDP](./images/atform9.png)

Definisci un Meta principal como **Coinvolgimento** - **Tempo sul sito**. **Salva e chiudi**.

![RTCDP](./images/vec3.png)

Agora você está na página **Panoramica delle attività**. Você ainda ativar sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inattivo** e selecione **Attiva**.

![RTCDP](./images/atform11.png)

Você receberá uma confirm mação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de dimostração e visitar a página do produto para **Real-Time CDP**, você se qualificará instantanea para o que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e contrasta con un URL acessando ao link: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Páginas compartilham è una base URL mesma e terminam com o número do participante.
>
>Por exemplo, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar un URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: envie seu para o Facebook](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)

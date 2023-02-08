---
title: Bootcamp - Customer Journey Analytics - Visualizzazione con Customer Journey Analytics - Brasile
description: Bootcamp - Customer Journey Analytics - Visualizzazione con Customer Journey Analytics - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 1%

---

# 4.5 Customer Journey Analytics Visualização o

## Obiettivi

- Entenda un’interfaccia utente esegui Analysis Workspace
- Alghe di Conheça ricorsos que tornam o Analysis Workspace tão diferente.
- Aprenda un analisar su CJA o Analysis Workspace

## Contexto

Neste exercício, você usará o Analysis Workspace no CJA para analisar visualizações de producos, funis de produtos, rotatividade, ecc.

Vamos usar o projeto que você criou em  [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selionado, você está rapidamente para começar a costrutuir suas primeiras visualizações.

![demo](./images/prodataView1.png)

## Quantas visualizações de produtos temos diariamente?

Em primeiro chargar, precisamos selionar come datas certas para analisar os dados. Acesse o menu suspenso do calendário no lado direito da tela. Clique nele e selecione o Interval de datas aplicável.

>[!IMPORTANT]
>
>Selecione um Interval de datas como **Questa settimana** Tu **Questo mese**. Os dados disponíveis mais recentes foram assorbvidos em 19 de setembro de 2022.

![demo](./images/pro1.png)
Nessun menu do lado esquerdo (área de componentes), encontre as métricas calcoladas **Visualizzazioni prodotto**. Selecione-as e arraste e solte na tela, no canto superiore direito da tabela de forma livre.

![demo](./images/pro2.png)

Automaticamente a dimensione **Giorno** será adicionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediata.

![demo](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no resumo da métrica.

![demo](./images/pro4.png)

Clipart **Visualizza** e selione **Linea** Como visualização.

![demo](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![demo](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **Impostazioni** una visualizzazione.

![demo](./images/pro7.png)

Clique no ponto ao lado de **Linea** e **Gestione dell&#39;origine dati**.

![demo](./images/pro7a.png)

Em seguida, clique em **Blocca selezione** e selione **Elementi selezionati** para bloquear esta visualização para que sempre exiba uma linha do tempo de Visualizações de producos.

![demo](./images/pro7b.png)

## 5 prodotti mais vistos

Quais são os 5 produtos mais vistos?

Lembre-se de salvar o projeto de tempos em tempos.

| Sistema operativo | Taglio corto |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Vamos começar a encontrar os 5 produtos mais vistos. Nessun menu do lado esquerdo, encontre o Nome do produto - Dimensão.

![demo](./images/pro8.png)

Agora arraste e solite **Nome del prodotto** para sostituituir a dimensão **Giorno**:

Este será o risultante.

![demo](./images/pro10a.png)

Em seguida, distdir um dos produtos por Nome da marca. Pesquise **brandName** e arraste para baixo do primeiro nome do produto.

![demo](./images/pro13.png)

Em seguida, faça um detalhamento o appio de usuário. Pesquise **Agente utente** e arraste-o para baixo do nome da marca.

![demo](./images/pro15.png)

Em seguida, será exibida a tela abaixo:

![demo](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. No lado esquerdo, em visualizações, pesquise `Donut`. Pegame `Donut`, arraste e solte na tela sob a visualização **Linea** 

![demo](./images/pro18.png)

Quindi, nella tabella, selezionare il primo 5 **Agente utente**  righe dal raggruppamento che abbiamo fatto in **Smartphone nero Google Pixel XL da 32 GB** > **Segnale Citi**. Quando selezioni le 5 righe, tieni premuto il pulsante **CTRL** su Windows o **Comando** (su Mac).

Em seguida, na Tabela, selione come primeiras 5 linhas de **Agente utente** do detalhamento que fizemos em **Smartphone nero Google Pixel XL da 32 GB** > **Segnale Citi**. Ao selionare come 5 linhas, segure o botão **CTRL** (senza Windows) o botão **Comando** (nessun Mac).

![demo](./images/pro20.png)

Você verá o gráfico de donut alterado:

![demo](./images/pro21.png)

Você pode até adaptar o design para ser mais legível, tornando o gráfico de **Linea** e o gráfico de de **Anello** um pouco menor para que sejam exibidos lado a lado:

![demo](./images/pro22.png)

Clique no ponto ao lado de *Anello** para **Gestione dell&#39;origine dati**. Em seguida, clique em **Blocca selezione** para bloquear essa visualização para que sempre exiba uma linha do tempo de Visualizações de produto.

![demo](./images/pro22b.png)

Saiba mais visualizações sogna o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=it](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=it)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Esistem muitas formas de resolver esta questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **Visualizzazione Abbandono**. Vamos usar o último, pois queremos visualizar e analisar ao mesmo tempo.

Feche o dolorel atual clicando aqui:

![demo](./images/pro23.png)

Agora adicione um novo antidel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro24.png)

Clique na visualização de **Abbandono**.

![demo](./images/pro25.png)

Selecione o mesmo a intervalli de datas do exercício anteriore.

![demo](./images/prodatef.png)

Em seguida, você verá:

![demo](./images/prodatefa.png)

Incontrare una dimensione **Tipo evento** nos components no lado esquerdo:

![demo](./images/pro26.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro27.png)

Você verá todos os Tipos de eventos disponíveis.

![demo](./images/pro28.png)

Selecione o articolo **commerce.productViews** e arraste e solte-o no campo **Aggiungi punto di contatto** dentro **Visualizzazione Abbandono**.

![demo](./images/pro29.png)

Faça o mesmo com **commerce.productListAdd** e **commerce.purchase** e solte-os no campo **Aggiungi punto di contatto** dentro  **Visualizzazione Abbandono**. Sua visualizzazione ação agora deve ser semelhante ao seguinte:

![demo](./images/props1.png)

Você pode fazer muitas coisas aqui. Gli algoritmi sfruttano: comparar ao longo do tempo, comparar cada passo porto ou comparar por fidelidade. No entanto, se quisermos analisar coisas interessantes como porque os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta do CJA: clicar com o botão direito.

Clique com o botão direito do mouse no touchpoint **commerce.productListAdd**. Em seguida, clique em **Abbandono suddiviso in questo punto di contatto**.

![demo](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se não comaram.

![demo](./images/pro33.png)

Altere o **Tipo evento** da **Nome pagina**, na nova tabela de formato livre, para ver em quais páginas eles estão indo, em vez da Página de confirmação de compra.

![demo](./images/pro34.png)

## O que as pessoas fazem no site antes de acessar a página Cancelar serviço?

Novamente, há muitas formas de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

Feche o dolorel atual clicando aqui:

![demo](./images/pro0.png)

Agora adicione um novo antidel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro0a.png)

Clique na visualização **Flusso**.

![demo](./images/pro35.png)

Em seguida, será exibido:

![demo](./images/pro351.png)

Selecione o mesmo a intervalli de datas do exercício anteriore.

![demo](./images/pro0b.png)

Incontrare una dimensione **Nome pagina** nos components no lado esquerdo:

![demo](./images/pro36.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro37.png)

Você encontrará todas as páginas vistas. Encontre o nome da página: **Annulla servizio**.
Arraste e solite **Annulla servizio** na Visualização de fluxo no campo do meio:

![demo](./images/pro38.png)

Em seguida, será exibido:

![demo](./images/pro40.png)

Vamos agora analisar se os clientaram que visitaram a página C **Annulla servizio** nessun sito também ligaram para o call center e qual foi o risultante.

Nas dimensões, Retorne e encontre Tipo de interação de chamada. Arraste e solite **Tipo di interazione chiamata** para sostanziali a primeira interação à direita em **Visualizzazione Flusso**.

![demo](./images/pro43.png)

Agora você visualizzazione su ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **Annulla servizio**.

![demo](./images/pro44.png)

Em seguida, nas dimensões, procure **Sensazione di chiamata**. Arraste e solte para sostituituir a primeira interação à direita na visualização de fluxo.

![demo](./images/pro46.png)

Em seguida, será exibido:

![demo](./images/flow.png)

Como pode ver, eseguutamos uma análise omnichannel a visualização de fluxo. Graças a isso, descobrimos que alguns clientes que estavam pensando em cancelar o servço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## Qual é o desempenho dos clientes com um contato de Call center Positivo em relação aos principi KPI?

Primeiramente, vamos segmentar os dados para obter apenas usuários com chamadas **positivo**. No CJA, os Segmentos são chamados de Filtros. Acesse para filtros na área de componentes (no lado esquerdo) e clique em **+**.

![demo](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| Nome | Descrizione |
| ----------------- |-------------| 
| Sensazione di chiamata - Positivo | Sensazione di chiamata - Positivo |

![demo](./images/pro47.png)

No componenti (dentro do Construtor de filtro), encontres **Sensazione di chiamata** e arraste e solte na Definição do Construtor de filtro.

![demo](./images/pro48.png)

Agora selione **positivo** como valor para o filtro.

![demo](./images/pro49.png)

Altere o escopo para o nível **Persona**.

![demo](./images/pro50.png)

Para finalizar, basta clicar em **Salva**.

![demo](./images/pro51.png)

Então, você irá retornar para esta tela. Se ainda não retornou, feche o dolorel anteriore.

![demo](./images/pro0c.png)

Agora adicione um novo antidel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro24c.png)

Selecione o mesmo a intervalli de datas do exercício anteriore.

![demo](./images/pro24d.png)

Clipart **Tabella a forma libera**.

![demo](./images/pro52.png)

Agora arraste e solte o filtro que você acabou de criar.

![demo](./images/pro53.png)

Hora de adicionar algumas métricas. Comece com **Visualizzazioni prodotto**. Arraste e solte na tabela de forma livre. Você também pode excluir a métrica **Eventi**.

![demo](./images/pro54.png)

Faça o mesmo com **Persone**, **Aggiungi al carrello** e **Acquisti**. Você via acabar com uma tabela como a seguinte.

![demo](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos criar esta tabela e verificato alghe KPI em um segmento para responder a essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido do que usar SQL ou usar outras soluções de BI.

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace rimuovere todas as limitações típicas de um relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensioni, métricas, segmentos e granularidades de tempo) para um projeto. Você pode criar de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De insights a ação](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)

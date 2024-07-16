---
title: Bootcamp - Customer Journey Analytics - Visualizzazione tramite Customer Journey Analytics - Brasile
description: Bootcamp - Customer Journey Analytics - Visualizzazione tramite Customer Journey Analytics - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5 Customer Journey Analytics Visualização o

## Objetivos

- Entenda un’interfaccia utente per Analysis Workspace
- Conheça alguns recursos que tornam o Analysis Workspace tão diferente.
- Aprenda un analisar no CJA o Analysis Workspace

## Contexto

Neste exercício, você usará o Analysis Workspace no CJA para analisar visualizações de produtos, funis de produtos, rotatividade, ecc.

Vamos usar o projeto que você criou em [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar a costrutt suas primeiras visualizações.

![demo](./images/prodataView1.png)

## Quantas visualizações de produtos temos diLETTANTIUM

Em primeiro lugar, precisamos selecionar come datas certas para analisar os dados. Acesse o menu suspenso do calendário no lado direito da tela. Clique nele e selecione o intervalli de datas aplicável.

>[!IMPORTANT]
>
>Selecione um intervalli de datas como **Questa settimana** ou **Questo mese**. Os dados disponíveis mais recentes foram assorbvidos em 19 de setembro de 2022.

![demo](./images/pro1.png)
Nessun menu do lado esquerdo (área de componentes), encontre come métricas calculadas **Visualizzazioni prodotto**. Selecione-as e arraste e solte na tela, no canto superior direito da tabela de forma livre.

![demo](./images/pro2.png)

Automaticamente una dimensione **Giorno** será adicionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediatamente.

![demo](./images/pro3.png)

Em seguida, cricca com o botão direito do mouse no resumo da métrica.

![demo](./images/pro4.png)

Clique em **Visualizza** e seleziona **Riga** como visualização.

![demo](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![demo](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **Impostazioni** na visualização.

![demo](./images/pro7.png)

Clique no ponto ao lado de **Line** e **Gestione del Data Source**.

![demo](./images/pro7a.png)

Em seguida, cricca em **Blocca selezione** e selecione **Elementi selezionati** para bloquear esta visualização para que ela sempre exiba uma linha do tempo de Visualizações de produtos.

![demo](./images/pro7b.png)

## 5 prodotti mais vistos

Quais são os 5 produtos mais vistos?

Lembre-se de salvar o projeto de tempos em tempos.

| Sistema operativo | Scelta rapida |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Vamos começar a encontrar os 5 prodotti mais vistos. Nessun menu do lado esquerdo, encontre o Nome do produto - Dimensão.

![demo](./images/pro8.png)

Agora arraste e solte **Nome prodotto** para subituir a dimensão **Giorno**:

Este será o resultado.

![demo](./images/pro10a.png)

Em seguida, tente dividir um dos produtos por Nome da marca. Pesquise **brandName** e arraste para baixo do primeiro nome do produto.

![demo](./images/pro13.png)

Em seguida, faça um detalhamento o Agente di usuario. Pesquise **Agente utente** e arraste-o para baixo do nome da marca.

![demo](./images/pro15.png)

Em seguida, será exibida a tela abaixo:

![demo](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. Nessun lado esquerdo, em visualizações, pesquise `Donut`. Pegue `Donut`, arraste e solte na tela sob a visualização **Riga** 

![demo](./images/pro18.png)

Quindi, nella tabella, seleziona le prime 5 **righe Agente utente** dal raggruppamento eseguito in **Smartphone nero Google Pixel XL da 32 GB** > **Segnale Citi**. Durante la selezione delle 5 righe, tenere premuto il pulsante **CTRL** (in Windows) o il pulsante **Comando** (in Mac).

Em seguida, na Tabela, selecione come primeiras 5 linhas de **Agente utente** do detalhamento que fizemos em **Google Pixel XL 32 GB Smartphone nero** > **Segnale Citi**. Ao selecionar come 5 linha, segure o botão **CTRL** (nessuna finestra) ou o botão **Comando** (nessuna Mac).

![demo](./images/pro20.png)

Você verá o gráfico de donut alterado :

![demo](./images/pro21.png)

Você pode até adaptar o design para ser mais legível, tornando o gráfico de **Line** e o gráfico de **Ciambella** um pouco menor para que sejam exibidos lado a lado:

![demo](./images/pro22.png)

Clique no ponto ao lado de *Anello** para **Gestire il Data Source**. Em seguida, cricca em **Blocca selezione** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizações de produto.

![demo](./images/pro22b.png)

Saiba mais sobre visualizações o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Voce principale: Muitas formas de resolver esta questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **Visualizzazione fallout**. Vamos usar o último, pois queremos visualizar e analisar ao mesmo tempo.

Feche o painel clicando atual aqui:

![demo](./images/pro23.png)

Agora adicione um novo painel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro24.png)

Clique na visualização de **Abbandono**.

![demo](./images/pro25.png)

Selecione o mesmo intervallo di dati do exercício anteriore.

![demo](./images/prodatef.png)

Em seguida, você verá

![demo](./images/prodatefa.png)

Confermare una dimensione **Tipo evento** componenti nos no lado esquerdo:

![demo](./images/pro26.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro27.png)

Você verá todos os Tipos de eventos disponíveis.

![demo](./images/pro28.png)

Seleziona l&#39;elemento **commerce.productViews** e arraste e solte-o no campo **Aggiungi punto di contatto** dentro da **Visualizzazione abbandono**.

![demo](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** e **commerce.purchases** e solte-os no campo **Aggiungi punto di contatto** dentro da **Visualizzazione fallout**. Sua visualização agora deve ser semelhante ao seguinte:

![demo](./images/props1.png)

Você pode fazer muitas coisas aqui. Esempi di algoritmi: comparar ao longo do tempo, comparar cada passo por dispositivo comparar por fidelidade. Nessun entanto, se quisermos analisar coisas interessantes como porque os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta do CJA: clicar com o botão direito.

Clique com o botão direito do mouse no punto di contatto **commerce.productListAdds**. Em seguida, cricca em **Abbandono in questo punto di contatto**.

![demo](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se não comaram.

![demo](./images/pro33.png)

Altere o **Tipo evento** di **Nome pagina**, na nova tabela de formato livre, para ver em quais páginas eles estão indo, em vez da Página de confirm mação de compra.

![demo](./images/pro34.png)

## O que as pessoas fazem no site antes de acessar a página Cancelar serviço?

Novamente, há muitas formas de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

Feche o painel clicando atual aqui:

![demo](./images/pro0.png)

Agora adicione um novo painel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro0a.png)

Clique na visualização **Flusso**.

![demo](./images/pro35.png)

Em seguida, será exibido:

![demo](./images/pro351.png)

Selecione o mesmo intervallo di dati do exercício anteriore.

![demo](./images/pro0b.png)

Encontre a dimensão **Page Name** nos componentes no lado esquerdo:

![demo](./images/pro36.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro37.png)

Você encontrará todas come páginas vistas. Encontre o nome da página: **Annulla servizio**.
Arraste e solte **Annulla servizio** na Visualização de fluxo no campo do meio:

![demo](./images/pro38.png)

Em seguida, será exibido:

![demo](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **Annulla servizio** no site também ligaram para o call center e qual foi o resultado.

Nas dimensões, retorne e encontre Tipo de interação de chamada. Arraste e solte **Tipo di interazione chiamata** para subituir a primeira interação à direita em **Visualizzazione flusso**.

![demo](./images/pro43.png)

Agora você visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **Annulla servizio**.

![demo](./images/pro44.png)

Em seguida, nas dimensões, procura **Sentimenti di chiamata**. Arraste e solte para substituir a primeira interação à direita na visualização de fluxo.

![demo](./images/pro46.png)

Em seguida, será exibido:

![demo](./images/flow.png)

Como pode ver, EXECUTAMOS uma análise omnichannel una visualização de fluxo. Graças a isso, descobrimos que alguns clientes que estavam pensando em cancelar o serviço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## Qual è o desempenho dos clientes com um contato de Call center Positivo em relação aos principais KPI?

Primeiramente, vamos segmentar os dados para obter apenas usuários com chamadas **positivi**. No CJA, os Segmentos são chamados de Filtros. Acesse para filtros na área de componentes (no lado esquerdo) e cricca em **+**.

![demo](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| Nome | Descrizione |
| ----------------- |-------------| 
| Sentimento di chiamata - Positivo | Sentimento di chiamata - Positivo |

![demo](./images/pro47.png)

Nessun componente (dentro do Construtor de filtro), encontre **Chiamare Feeling** e arraste e solte na Definição do construtor de filtro de filtro.

![demo](./images/pro48.png)

Agora selecione **positiva** como valor para o filtro.

![demo](./images/pro49.png)

Altere o escopo para o nível **Persona**.

![demo](./images/pro50.png)

Para finalizar, basta clicar em **Salva**.

![demo](./images/pro51.png)

Voce irá retornar para esta tela. Se ainda não retornou, feche o painel anteriore.

![demo](./images/pro0c.png)

Agora adicione um novo painel em branco clicando em **+ Aggiungi pannello vuoto**.

![demo](./images/pro24c.png)

Selecione o mesmo intervallo di dati do exercício anteriore.

![demo](./images/pro24d.png)

**Tabella a forma libera**.

![demo](./images/pro52.png)

Agora arraste e solte o filtro que você acabou de criar.

![demo](./images/pro53.png)

Hora de algumas métricas adicionari. Comece com **Visualizzazioni prodotto**. Arraste e solte na tabela de forma livre. Você também pode excluir a métrica **Eventi**.

![demo](./images/pro54.png)

Faça o mesmo com **Persone**, **Aggiungi al carrello** e **Acquisti**. Voce via acabar com uma tabela como a seguinte.

![demo](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos criar esta tabela e verificar alguns KPIs em um para responder a essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido que usar SQL ou usar outras soluções de BI.

## Ricapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace rimuovere todas come limitações típicas de um relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Você pode criar de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 Approfondimenti a ação](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)

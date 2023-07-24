---
title: Bootcamp - Customer Journey Analytics - Creare una visualizzazione dati - Brasile
description: 'Customer Journey Analytics: creazione di una visualizzazione dati - Brasile'
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 Crie uma Visualização de Dados

## Objetivos

- Entenda a UI de Visualização de Dados
- Compreenda as configurações básicas de definição de visita
- Compreenda a distribuição e a Persistência em uma Visualização de

## 4.3.1 Visualização de Dados

Agora, com sua conexão concluída, é possível progredir para influenciar a visualização. Uma diferença entre o Adobe Analytics e o CJA é que o CJA de uma visualização de dados para limpar e preparar os dados antes da visualização.

Uma Visualização de Dados é semelhante ao concepito de Virtual Report Suites no Adobe Analytics, onde você estabelece as definições de visita com reconhecimento de contexto, filtragem e também como os componentes são chamados.

Será necessário, no mínimo, uma Visualização de Dados por conexão. No entanto, para alguns casos de uso, é ótimo ter múltiplas Visualizações de Dados para a mesma conexão, com o objetivo de fornecer insights diferentes para equipes distinas. Se você deseja que sua empresa seja orientada por dados, deve adaptar a forma como os dados são vistos em cada equipe. Esempi di algoritmi:

- Métricas de UX apenas para a equipe de UX Design
- Usare os mesmos nomes para KPIs e métricas para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma.
- Visualização de Dados filtrada para mostrar, por exemplo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

Na tela **Connessioni** marque a caixa de seleção da conexão que você acabou de criar. Clique em  **Crea visualizzazione dati**.

![demo](./images/exta.png)

Você será redirecionado para o fluxo de trabalho **Crea visualizzazione dati** flusso di lavoro.

![demo](./images/0-v2.png)

## 4.3.2 Definição de Visualização de Dados

Agora você pode configurar as definições básicas para sua Visualização de dados.

![demo](./images/0-v2.png)

A **Connessione** que você criou no exercício anteriore já está selecionada. Sua conexão se chama `yourLastName – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Em seguida, dê um nome à sua Visualização de Dados seguindo este modelo de nomenclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a descrição: `yourLastName – Omnichannel Data View`.

| Nome | Descrizione |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demo](./images/1-v2.png)

Paragrafo **Fuso orario**, selecione o fuso horário **Berlim, Estocolmo, Roma, Berna, Bruxelas, Viena, Amsterdã GMT+01:00**. Este é um cenário, pois algumas empresas operam em diferentes países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados, como, por exemplo, acreditar que a maioria das pessoas compra camisetas às 4h no Peru.

![demo](./images/ext7.png)

Você também pode modificar a nomenclatura das métricas princippais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas alguns clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessão e Eventos (convenção de nomenclatura padrão do Customer Journey Analytics).

Agora você deve ter come seguintes configurações definidas:

![demo](./images/1-v2.png)

Clique em **Salva e continua**.

![demo](./images/12-v2.png)

## 4.3.3 Componenti da Visualização de Dados

Neste exercício, você irá configurar os componentes necessários para analisar os dados e visualizá-los o Analysis Workspace. Nesta IU, há três áreas principais:

- Lado esquerdo: Componenti disponíveis dos set di dati selecionados
- Meio: Componenti adicionados à Visualização de Dados
- Lado direito: Configurações do componente

![demo](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrar uma métrica ou dimensão específica, verifique se o campo `Contains data` foi removido de sua visualização de dados. Il caso contrário, l&#39;esclusa esse campo.
>
>![demo](./images/2-v2a.png)

Agora você arrastar e soltar os componentes necessários para a análise nos **Componenti aggiunti**. Para isso, você deve selecionar os componentes no menu à esquerda e arrastá-los e soltá-los na tela no meio.

Vamos começar com o primeiro componente: **Nome (web.webPageDetails.name)**. Pesquise esse componente e arraste-o e solte-o na tela.

![demo](./images/3-v2.png)

Esse componenti é o nome da página, como você pode derivar da leitura do campo do schema `(web.webPageDetails.name)`.

Nessun entanto, usar **Nome** como o nome não é a melhor convocção de nomenclatura para um usuário corporativo comprender essa dimensão.

Vamos mudar o nome para **Nome pagina**. Cricca no componente e o renomeie na área **Impostazioni dei componenti**.

![demo](./images/3-0-v2.png)

Come Configurações de persistência são **Impostazioni persistenza**. Os concepitos de eVars e prop não exist no CJA, mas as configurações de Persistência possibilitam um semelhante.

![demo](./images/3-0-v21.png)

Se você não alterar essas configurações, o CJA irá interpretar a dimensão como um **Prop** (nível de ocorrência). Além disso, podemos alterar a Persistência para tornar a dimensão uma **eVar** (persistir o valor ao longo da jornada).

Se você não estiver familiarizado com eVars e Props [leia mais sobre isso na documentação](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página como Prop. Dessa forma, você não nenhuma **Impostazioni persistenza**.

| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| Nome (web.webPageDetails.name) | Nome pagina |          |

Em seguida, escolha a dimensão **phoneNumber** e solte-a na tela. O novo nome deve ser **Numero di telefono**.

![demo](./images/3-1-v2.png)

Por fim, vamos alterar come Configurações de persistência, pois o Número do Celular deve persistir no nível do usuário.

Para alterar a Persistência, ruolo para baixo no menu à direita e abra a aba **Persistenza**:

![demo](./images/5-v2.png)

Marque a caixa de seleção para modificar come configurações de persistência. Selecione **Più recente** e o escopo **Persona (intervallo di reporting)**, pois nos preocupamos apenas com o último número de celular da pessoa. Se o cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido.

![demo](./images/6-v2.png)

| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numero di telefono | Più recente, persona (intervallo di reporting) |

O próximo componente `web.webPageDetails.pageViews.value`.

Nessun menu à esquerda, pesquise `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela.

Altere o nome para **Visualizzazioni pagina** sotto **Impostazioni dei componenti**.

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![demo](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Osservação: Come configurações de persistência nas métricas também podem ser alteradas no Analysis Workspace. Em alguns casos, você pode optar por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual é o melhor modelo de persistência.

Em seguida, você terá que configurar várias Dimensões e Métricas, conforme indicado na tabela abaixo.

### DIMENSIONI

| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| brandName | Marchio | Più recente, sessione |
| sentimento di chiamata | Sentimento di chiamata |          |
| ID chiamata | Tipo di interazione chiamata |          |
| callTopic | Richiama argomento | Più recente, sessione |
| ecid | ECID | Più recente, persona (intervallo di reporting) |
| e-mail | ID e-mail | Più recente, persona (intervallo di reporting) |
| Tipo di pagamento | Tipo di pagamento |          |
| Metodo di aggiunta prodotto | Metodo di aggiunta prodotto | Più recente, sessione |
| Tipo evento | Tipo evento |         |
| Nome (productListItems.name) | Nome prodotto |         |
| SKU | SKU (sessione) | Più recente, sessione |
| ID transazione | ID transazione |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agente utente | Agente utente | Più recente, sessione |

### MÉTRICA

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| Quantità | Quantità |          |
| commerce.order.priceTotal | Ricavi |         |

Sua configuração deve ser semelhante ao seguinte:

![demo](./images/11-v2.png)

Não se esqueça de Salvar sua Visualização de Dados. Então cricca em **Salva**.

![demo](./images/12-v2s.png)

## 4.3.4 Calcoli metrici

Embora tenhamos organizado todos os componentes na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises.

Se você se lembra, não trouxemos especificamente Métricas como Adicionar ao Carrinho, Visualização do produto ou Compras para a Visualização de dados. Nessun entanto, temos uma dimensão chamada: **Tipo di evento**. Então, vamos derivar esses tipos de interação criando 3 métricas calculadas.

Vamos começar com a primeira Métrica **Visualizzazioni prodotto**.

Nessun lado esquerdo, pesquise **Tipo di evento** Abbiamo selezionato una dimensione. Em seguida, arraste-o e solte-o na tela **Componenti inclusi**.

![demo](./images/calcmetr1.png)

Clique para selecionar a nova métrica **Tipo di evento**.

![demo](./images/calcmetr2.png)

Agora altere o nome e a descrição do componente para os seguintes valores:

| Nome componente | Descrizione componente |
| ----------------- |-------------| 
| Visualizzazioni prodotto | Visualizzazioni prodotto |

![demo](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **Visualizzazioni prodotto**. Para fazer isso, ruolo para baixo em **Impostazioni dei componenti** até ver Valores de **Includi valori di esclusione**. Certifique-se de habilitar a opção **Impostare i valori di inclusione/esclusione**.

![demo](./images/calcmetr4.png)

Como queremos apena contar **Visualizzazioni prodotto**, speciifique **commerce.productViews** nos critérios

![demo](./images/calcmetr5.png)

Agora a sua métrica calcolada está pronta!

Em seguida, repita o mesmo processore para os eventos **Aggiungi al carrello** e **Acquisto**.

### Aggiungi al carrello

Primeiro, arraste e solte a mesma dimensão **Tipo di evento**.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos a mesma variável. Clique em **Aggiungi comunque**:

![demo](./images/calcmetr6.png)

Agora, siga o mesmo processo que fizemos para a métrica Visualizações de produto:
- Primeiro altere o nome e a descrição.
- Por fim, adicione **commerce.productListAdds** como critério para contar apenas Aggiungi al carrello

| Nome | Descrizione | Criteri |
| ----------------- |-------------| -------------|
| Aggiungi al carrello | Aggiungi al carrello | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Acquisti

Primeiro, arraste e solte a mesma dimensão **Tipo di evento** como fizemos para as duas métricas anteriores.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos a mesma variável. Clique em **Aggiungi comunque**:

![demo](./images/calcmetr7.png)

Agora, siga o mesmo processore que fizemos para as métricas Visualizzazioni del prodotto e Aggiungi al carrello:
- Primeiro altere o nome e a descrição.
- Por fim, adicione **commerce.purchases** como critérios para apenas come Compras

| Nome | Descrizione | Criteri |
| ----------------- |-------------| -------------|
| Acquisti | Acquisti | commerce.purchases |

![demo](./images/calcmetr7a.png)

Sua configuração final deve ser semelhante ao seguinte. Clique em **Salva e continua**.

![demo](./images/calcmetr8.png)

## 4.3.5 Componenti da Configuração de Dados

Você deve ser redirecionado para esta tela:

![demo](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações importantes para alterar a forma como os dados são processados. Vamos começar definizione o **Timeout sessione** como 30 min Graças ao registro de data e hora de cada evento de experiência, você pode estender o concepito de uma sessão em todos os canais. Por exemplo, o que acontece se um cliente ligar para o call center depois de visitar o site? Usando Tempos Limite de Sessão personalizados, você tem muita flexibilidade para decidir o que é uma sessão e como essa sessão irá mesclar os dados.

![demo](./images/ext8.png)

Nesta aba você pode modificar outras coisas como os dados filtrar um/. Você não precisará fazer isso neste exercício

![demo](./images/10-v2.png)

Quando terminale, cricca em **Salva e termina**.

![demo](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados posteriormente e alterare come configurações e os componentes a qualquer momento. Come alterações afetarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise!

Próxima etapa [4.4 Preparação de dados em Customer Journey Analytics](./ex4.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)

---
title: Bootcamp - Customer Journey Analytics - Connetti i set di dati Adobe Experience Platform in Customer Journey Analytics - Brasile
description: Bootcamp - Customer Journey Analytics - Connetti i set di dati Adobe Experience Platform in Customer Journey Analytics - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 2%

---

# 4.2 Set di dati collegati da Adobe Experience Platform nessun Customer Journey Analytics

## Obiettivi

- Compreenda un&#39;interfaccia utente da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda ID da pessoa e a compilação de dados
- Aprenda o concito de streaming de dados no Percorso del cliente

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar al Customer Journey Analytics.

Na página inicale do Customer Journey Analytics, acesse **Connessioni**.

![demo](./images/cja2.png)

Aqui você pode ver todas as diferentes conexões feitas entre o CJA e a Plataforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics. No entanto, un coleta dos dados é completamente diferente. Todos os dados vêm de datasets da Adobe Experience Platform.

Vamos criar sua primeira conexão. Clipart **Crea nuova connessione**.

![demo](./images/cja4.png)

Você contro interfaccia utente **Crea connessione** Interfaccia utente.

![demo](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Utilizzare il modello este di classificazione: `yourLastName – Omnichannel Data Connection`.

Esempio: `vangeluw - Omnichannel Data Connection`

Você também dev selionar o sandbox correto para usar. Nessun menu sandbox, selezionione seu sandbox, que deve ser `Bootcamp`. Neste esempio, o sandbox un ser usado é o **Bootcamp**. E você também deve definir o **Numero medio di eventi giornalieri** a **meno di 1 milione**.

![demo](./images/cjasb.png)

Sandbox selionare di Após seu, você pode começar a adicionar datasets a esta conexão. Clipart **Aggiungi set di dati**.

![demo](./images/cjasb1.png)

## 4.2.2 Set di dati selezionati da Adobe Experience Platform

Previsione del set di dati `Demo System - Event Dataset for Website (Global v1.1)`. Clipart **+** para adicionar o set di dati a esta conexão.

![demo](./images/cja7.png)

Agora pesquise e marque come caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. Clipart **Successivo**.

![demo](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora é juntar esses datasets. Para cada set di dati selionado, você verá um campo chamado **ID persona**. Set di dati di Canada seu próbuffercampo de ID de pessoa.

![demo](./images/cja11.png)

Como você pode ver, a maioria li deles o ID da pessoa selionado automaticamente. Isso ocorre porque um identificador principal é selecionado em cada esquema na Adobe Experience Platform. Como exemplo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pover que o Identificador Primário está definido como `phoneNumber`.

![demo](./images/cja13.png)

No entanto, você ainda pode influenciar identador será usado para compilar datasets para sua conexão. Você pode usar qualquer identifier configurado no esquema vinculado ao seu dataset. Clique no menu suspenso para explorar os IDs disponíveis em cada set di dati.

![demo](./images/cja14.png)

Conforme mencionado, você pode definir diversi IDs de pessoa para cada set di dati. Isso permite reunir differentes datasets de múltiplas origens su CJA. Immaginate il trazer NPS ou dados de pesquisa que seriam muito interessantes e úteis para compressender o contexto e o decidere de um acontecimento.

O nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa corrispondenti. Digamos que temos `email` em um set di dati e `emailAddress` em outro set di dati definido como ID da pessoa. Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os datasets, o CJA poderá compilar os dados.

Atualmente, algume esistite outras limitações, como compilar o comportamento anônimo para conhecido. Consulte come perguntas frequenta aqui: [Domande frequenti](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=it).


### Compilando os dados o ID da pessoa

Agora que você Comende o concito de compilar datasets o ID da pessoa, vamos escolher `email` como ID da pessoa para cada set di dati.

![demo](./images/cja15.png)

Set di dati cada di Acesse para atualizar o ID da pessoa.

![demo](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa.

![demo](./images/cja17.png)

Depois de compilar os três datasets, estamos prontos para continuar.

| Set di dati | ID persona |
| ----------------- |-------------| 
| Sistema di demo - Set di dati evento per il sito web (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per assistenti vocali (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | e-mail |

Você também precisa garantir que, para cada dataset, essas opções estejam habilitadas:

- Strumenti importanti os novos dados
- Preencher todos os dados esiste

Clipart **Aggiungi set di dati**.

![demo](./images/cja16.png)

Clipart **Salva** e vá para o próximo exercício. Depois de criar sua **Connessione**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demo](./images/cja20.png)

Próxima etapa: [4.3 Criterio uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)

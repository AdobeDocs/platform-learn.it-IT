---
title: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente - Brasile
description: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Crie um - Interfaccia utente

Neste exercício, você irá criar um o Construtor de Segmentos da Adobe Experience Platform.

## História

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso clicando no texto **[!UICONTROL Prod produzione]** è una linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, acesse **Segmenti**. Nesta página, você tem uma visão geral de todos os segmentos exists. Clique no botão + Criar para começar a criar um novo.

![Segmentazione](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você irá perceber imediatamente a opção de menu **Attributi** e a referência do **Profilo individuale XDM**.

![Segmentazione](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, in modo indipendente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a partir dessa interface do usuário do construtor de, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora você um de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para costrutir este, você adicionar um Evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no ícone **Eventi** barra di menu **Campi**.

![Segmentazione](./images/findee.png)

Em seguida, você verá o no **XDM ExperienceEvents** nível superiore. Clique em **XDM ExperienceEvent**.

![Segmentazione](./images/see.png)

Acesse **Elementi elenco prodotti**.

![Segmentazione](./images/plitems.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu à esquerda na tela do construtor de segmentos na seção **Eventi**. Em seguida, o seguinte será exibido:

![Segmentazione](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **è uguale a** e, no campo de entrada, insira **Real-time CDP**.

![Segmentazione](./images/pv.png)

Sempre que adicionar um elemento ao costruttore de segmentos, você pode clicar no botão **Aggiorna stima** para obter uma nova estimativa da população em seu.

![Segmentazione](./images/refreshest.png)

Paragrafo **Metodo di valutazione**, selecione **Bordo**.

![Segmentazione](./images/evedge.png)

Por fim, vamos dar um nome ao seu e salvá-lo.

Como modello della nomenclatura, uso:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, cricca no botão **Salva e chiudi** para salvar seu.

![Segmentazione](./images/segmentname.png)

Agora você irá retornar à página de visão geral do, onde verá uma visualização de amostra dos perfis de clientes que se qualificam para o seu.

![Segmentazione](./images/savedsegment.png)

Agora você pode continuar no próximo exercício e usar seu com o Adobe Target.

Próxima etapa [1.4 Ação: envie seu para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)

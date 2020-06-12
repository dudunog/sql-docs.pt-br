---
title: Documentando modelos de mineração (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 92ed5c43fa2b7484485b915d42946121487386d9
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528482"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>Documentando modelos de mineração (Suplementos de Mineração de Dados para Excel)
  ![Botão Modelo de Documento, faixa de opções Mineração de Dados](media/dmc-docmodel.gif "Botão Modelo de Documento, faixa de opções Mineração de Dados")  
  
 O assistente de **modelo de documento** cria um relatório que fornece informações úteis sobre os modelos de mineração que você criou. Ao documentar os modelos criados, você pode rastrear a origem dos dados usados para gerar um modelo, obter informações adicionais sobre a data de processamento do modelo e rastrear alterações de parâmetro que afetam os resultados do modelo.  
  
## <a name="using-the-document-model-wizard"></a>Usando o assistente de Modelo de Documento  
  
1.  Clique na guia **mineração de dados** .  
  
2.  No grupo **uso do modelo** , clique em **modelo do documento**.  
  
3.  Na caixa de diálogo **selecionar modelo** , selecione o modelo a ser relatado e clique em **Avançar**. Você deve executar o assistente de **modelo de documento** separadamente para cada modelo que você deseja documentar.  
  
4.  Na caixa de diálogo **selecionar detalhes da documentação** , escolha uma das duas opções: informações **completas** ou **informações de resumo**.  
  
5.  Clique em **Concluir**.  
  
6.  O assistente cria automaticamente uma nova planilha que contém o relatório especificado, título **documentação do modelo**,  
  
## <a name="understanding-the-report"></a>Entendendo o relatório  
 Quando você cria um relatório que documenta um modelo de mineração de dados, pode criar um resumo, que contém informações básicas, como o nome e a descrição do modelo, ou um relatório completo, que contém detalhes sobre a estrutura subjacente e informações avançadas sobre o modelo de mineração.  
  
 Dependendo do algoritmo usado para criação do modelo, tipos diferentes de informações são fornecidos. Por exemplo, em um modelo associado, você está mais interessado em saber o número de conjuntos de itens e regras gerados. Para um modelo de clustering, o número de clusters é mais interessante.  
  
 A tabela a seguir lista as opções e as informações fornecidas no relatório para cada opção.  
  
> [!NOTE]  
>  As colunas no relatório são definidas com um determinado tamanho por padrão. Assim, se os nomes ou os valores de uma coluna forem muito longos, talvez não fiquem visíveis ou apareçam como ### no Excel. Para tornar os valores visíveis, redimensione a linha. Se a célula estiver selecionada, clique nas setas duplas na extremidade direita da barra de fórmulas e arraste-as para mostrar a cadeia de caracteres ou o valor completo.  
  
### <a name="summary-report"></a>Relatório Resumido  
  
||||  
|-|-|-|  
|**Metadados**|Nome do modelo<br /><br /> Descrição do modelo<br /><br /> Nome do algoritmo<br /><br /> Data do último processamento||  
|**Resultados do modelo**|Associação|Contagem de conjuntos de itens<br /><br /> Contagem de regras|  
||Clustering|Contagem de clusters<br /><br /> Suporte para cada cluster|  
||Árvore de decisão|Número de árvores<br /><br /> Número de nós em cada árvore|  
||Regressão linear|Número de árvores (sempre 1)<br /><br /> Número de nós (sempre 1)|  
||Naïve Bayes|Atributos importantes|  
||Rede neural|Número de nós de entrada<br /><br /> Número de nós de saída<br /><br /> Número de nós ocultos|  
||Clustering de sequências|Número de clusters|  
  
### <a name="complete-report"></a>Relatório completo  
 O relatório completo contém todos os itens do relatório resumido, além de informações detalhadas sobre as colunas de dados usadas no modelo e os resultados da análise:  
  
||||  
|-|-|-|  
|**Metadados**|Metadados do modelo|Parâmetros e valores do algoritmo|  
||Metadados da coluna|Nome da coluna<br /><br /> Uso<br /><br /> Tipo de dados<br /><br /> Tipo de conteúdo<br /><br /> Valores (lista de valores discretos ou intervalos de valores)|  
|**Estatísticas do modelo**|Colunas contínuas|Valor médio<br /><br /> Valor mínimo<br /><br /> Valor máximo<br /><br /> Erro de raiz quadrada média<br /><br /> Erro de média absoluta<br /><br /> Pontuação de log<br /><br /> Fórmula de regressão (para modelos de regressão linear apenas)|  
||Colunas discretas|Contagem de passagens<br /><br /> Contagem de falhas<br /><br /> Pontuação de log<br /><br /> Comparação de Precisão|  
  
> [!NOTE]  
>  Você pode documentar qualquer tipo de modelo que tenha suporte do SQL Server Analysis Services. Portanto, a tabela lista alguns tipos de modelo que não podem ser criados com o uso das Ferramentas de Análise de Tabela ou com os assistentes no Cliente de Mineração de Dados. No entanto, você pode criar todos os tipos de modelo usando o **Editor de consulta de mineração de dados avançado**. Para obter mais informações, consulte [consultas &#40;SQL Server suplementos de mineração de dados&#41;](query-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Implantando e dimensionando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  

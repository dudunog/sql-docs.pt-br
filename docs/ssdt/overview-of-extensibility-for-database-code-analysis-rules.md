---
title: Extensibilidade para regras de análise de código de banco de dados
description: Familiarize-se com os vários componentes das regras de análise de código de banco de dados e como elas interagem no SQL Server Data Tools. Saiba mais sobre como criar regras personalizadas.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: e67b6dabc0d8db2b3644a6183b4a6855738e54ba
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897622"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>Visão geral de extensibilidade para regras de análise de código do banco de dados

As edições do Visual Studio contendo SQL Server Data Tools incluem regras de análise de código para relatórios em avisos de design, nomeação e desempenho Transact\-SQL em seu código de banco de dados. Para saber mais, confira [Analisar o código do banco de dados para melhorar a qualidade do código](https://msdn.microsoft.com/library/dd172133(v=vs.100).aspx).  
  
Se as regras de análise de código integradas não tiverem cobertura para um determinado problema Transact\-SQL a ser incluído, você pode criar regras de análise de código do banco de dados personalizadas. Por exemplo, você pode querer criar uma regra personalizada que evite usar a instrução WAITFOR DELAY, como demonstrado em [Passo a passo: criar um assembly de regra de análise de código estático personalizado para o SQL Server](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md). Para criar regras de análise de código personalizado do banco de dados, você pode usar as classes no namespace [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx).  
  
Antes de criar regras de análise de código personalizado, você deve compreender a arquitetura básica entre os vários componentes de regras de análise de código do banco de dados.  
  
## <a name="database-code-analysis-rules-components"></a>Componentes de regras de análise de código do banco de dados  
O diagrama a seguir ilustra como os componentes de regras de análise de código de banco de dados interagem:  
  
![Componentes de regras de análise de código do banco de dados](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "Componentes de regras de análise de código do banco de dados")  
  
Quando você usa o recurso de regras de análise de código do banco de dados, seja executando a análise de código estático diretamente (para obter mais informações, confira [Como analisar o código Transact-SQL para encontrar defeitos](https://msdn.microsoft.com/library/dd172119(v=vs.100).aspx)) ou executando uma compilação, todas as regras são carregadas e usadas de acordo com a forma como você as configurou em seu projeto. Para obter mais informações, confira [Como habilitar e desabilitar regras específicas para análise estática de código do banco de dados](https://msdn.microsoft.com/library/dd172131(v=vs.100).aspx). O Gerenciador de Extensões também carregará todos os assemblies de regra personalizada que você tenha criado e registrado. Para obter mais informações, confira [Como instalar e gerenciar extensões de recurso](../ssdt/how-to-install-and-manage-feature-extensions.md).  
  
Uma classe de regra de análise de código personalizada herda de [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx). A classe de regra personalizada pode acessar um número de objetos úteis por meio de seu contexto de execução de regra. Eles incluem:  
  
-   Metadados sobre a regra em si.  
  
-   O Dac.Model.TSqlModel que representa o esquema do banco de dados, incluindo todos os elementos do modelo, relações entre eles e as propriedades dos elementos.  
  
-   Para regras que examinam os elementos específicos de Dac.Model.TSqlModel que representa o elemento de esquema no modelo que está incluído no contexto.  
  
-   Muitos objetos de esquema também têm uma representação [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) que pode ser acessada por meio desse contexto. Essa é uma representação baseada em AST de um elemento que pode ser útil ao tentar prever problemas de sintaxe em potencial, como a presença de [SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx).  
  
Um Dac.CodeAnalysis.SqlRuleProblem é criado pela regra para representar quaisquer problemas encontrados por ele. Ao criá-lo, o Dac.Model.TSqlObject relevante e possivelmente um elemento de representação [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) são passados para o construtor e usados para determinar o local do problema em seus arquivos de código-fonte. Ao final da análise, todos esses problemas são passados para o Gerenciador de Erro e exibidos na Lista de Erros.  
  
## <a name="see-also"></a>Consulte Também  
[Estender os recursos de banco de dados](../ssdt/extending-the-database-features.md)  
  

---
description: Trabalhando com o script de console de exemplo FilesExecuting The SSMA console (AccessToSQL)
title: Trabalhar com o script de console de exemplo FilesExecuting o console do SSMA | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 91ccdde50fc0e4f031f376132213881db0a85449
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418522"
---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>Trabalhando com o script de console de exemplo FilesExecuting The SSMA console (AccessToSQL)
Alguns arquivos de exemplo foram fornecidos junto com o produto para a referência e o uso do usuário. Esta seção descreve a maneira de personalizar facilmente esses scripts para atender às necessidades do usuário final.  
  
## <a name="sample-console-script-files"></a>Arquivos de script de console de exemplo  
Os seguintes arquivos de script de console de exemplo que abrangem diferentes cenários foram fornecidos para referência de usuário:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   Este exemplo fornece os diferentes modos de conexão disponíveis para o banco de dados de origem e destino, e o usuário pode selecionar qualquer modo de acordo com o requisito. Este exemplo contém as definições de servidor.  
  
    -   O usuário pode se conectar ao banco de dados necessário simplesmente alterando os valores para as definições de servidor de origem e de destino necessárias. No exemplo fornecido, todos os valores foram fornecidos como valores de variáveis que estão disponíveis no **VariableValueFileSample.xml**. Todos os outros parâmetros de conexão podem ser removidos do arquivo de conexão do servidor de trabalho do usuário.  
  
    -   Para obter mais informações sobre como se conectar ao servidor de origem e de destino, consulte [criando os arquivos de conexão do servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md) .  
  
-   **VariableValueFileSample.xml:** Todas as variáveis que foram usadas nos arquivos de script de console de exemplo e foram `ServersConnectionFileSample.xml` agrupadas neste arquivo. Para executar os scripts de console de exemplo, o usuário precisa simplesmente substituir os valores de variáveis de exemplo por aqueles definidos pelo usuário e passar esse arquivo como um argumento de linha de comando adicional junto com o arquivo de script.  
  
    Para obter mais informações sobre o arquivo de valor de variável, consulte [criando arquivos de valor de variável &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** Este exemplo permite que o usuário gere um relatório de avaliação XML que pode ser usado pelo usuário para análise antes de começar a converter e migrar dados.  
  
    No `generate-assessment-report` comando, o usuário precisa mandatorily alterar o valor da variável (consulte **VariableValueFileSample.xml**) no `object-name` atributo para o nome do banco de dados que está sendo usado pelo usuário. Dependendo do tipo de objeto especificado, o `object-type` valor também precisará ser alterado.  
  
    Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar vários `metabase-object` nós, conforme ilustrado no `generate-assessment-report` exemplo 4 do comando do arquivo de script do console de exemplo.  
  
    Para obter mais informações sobre como gerar relatórios, consulte [gerando relatórios &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
    > [!NOTE]  
    > -   Certifique-se de que o argumento de linha de comando do arquivo de valor da variável seja passado para o aplicativo de console e VariableValueFileSample.xml seja atualizado com os valores especificados pelo usuário.  
    > -   Verifique se o argumento de linha de comando do arquivo de conexão do servidor foi passado para o aplicativo de console e se o ServersConnectionFileSample.xml está atualizado com valores de parâmetro de servidor corretos.  
  
-   **ConversionAndDataMigrationSample.xml:** Este exemplo permite que o usuário execute uma migração de ponta a ponta da conversão para a migração de dados. A lista de valores de atributo obrigatórios que eles terão que ser alterados está listada abaixo:  
  
    |Nome do comando|Descrição|Atributo|  
    |----------------|---------------|-------------|  
    |`map-schema`|Mapeamento de esquema do banco de dados de origem para o esquema de destino.|`source-schema:` Especifica o banco de dados de origem que exige a conversão.<br /><br />`sql-server-schema`: Especifica o banco de dados de destino que deve ser migrado para|  
    |`convert-schema`|Executa a conversão de esquema da origem para o esquema de destino.<br /><br />Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar vários `metabase-object` nós, conforme ilustrado no `convert-schema` exemplo 4 do comando do arquivo de script do console de exemplo.|`object-name`: Especifique o nome do banco de dados/objeto de origem que exige a conversão. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no `object-name`|  
    |`synchronize-target`|Sincroniza os objetos de destino com o banco de dados de destino.<br /><br />Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar vários `metabase-object` nós, conforme ilustrado no `synchronize-target` exemplo 3 do comando do arquivo de script do console de exemplo.|`object-name:` Especifique o nome do banco de dados/objeto do SQL Server que requer a criação. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no `object-name`|  
    |`migrate-data`|Migra os dados de origem para o destino.<br /><br />Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar vários `metabase-object` nós, conforme ilustrado no `migrate-data` exemplo 2 do comando do arquivo de script do console de exemplo.|`object-name:` Especifica o nome do banco de dados/tabelas de origem que exige a migração. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no `object-name`|  
  
## <a name="see-also"></a>Consulte Também  
[Criando arquivos de valor de variável &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[Criando os arquivos de conexão do servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[Gerando relatórios &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)  
  

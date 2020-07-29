---
title: Exemplo de arquivo de entrada XML com configuração especificada pelo usuário
description: Este artigo contém um arquivo de entrada XML de exemplo com configurações especificadas pelo usuário a ser usado para ajustar as cargas de trabalho a empregar com o Orientador de Otimização do Mecanismo de Banco de Dados.
titleSuffix: DTA
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 0096fbcfe97806865224f20f6a3e8ffacb1cd76e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731940"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Copie e cole este exemplo de um arquivo de entrada XML que especifica uma configuração especificada pelo usuário com o elemento **Configuration** em seu editor XML ou editor de texto favorito. Isso permite realizar uma análise hipotética. A análise hipotética envolve o uso do elemento **Configuration** para especificar um conjunto de estruturas de design físico hipotéticas para o banco de dados que você deseja ajustar. Então você usa o Orientador de Otimização do Mecanismo de Banco de Dados para analisar os efeitos de executar uma carga de trabalho em relação a essa configuração hipotética para descobrir se ela melhorará o desempenho de processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se sua configuração hipotética não oferecer a melhora de desempenho desejada, é fácil alterá-la e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
 Depois de copiar esse exemplo em sua ferramenta de edição, substitua os valores especificados para os elementos **Servidor**, **Banco de Dados**, **Esquema**, **Tabela**, **Carga de trabalho**, **Opções de Ajuste**e **Configuração** com aqueles para sua sessão de ajuste específica. Para obter mais informações sobre todos os atributos e elementos filho que podem ser usados com esses elementos, veja a [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md). O exemplo a segui usa um subconjunto de atributo único disponível e opções de elemento filho.  
  
## <a name="code"></a>Código  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
<!-- To tune multiple databases, list them and their associated tables in the following section. -->  
      <Database>  
        <Name>MyDatabaseName</Name>  
        <Schema>  
          <Name>MyDatabaseSchemaName</Name>  
<!-- You can list as many tables as necessary in the following section. -->  
          <Table>  
            <Name>MyTableName1</Name>  
          </Table>  
          <Table>  
            <Name>MyTableName2</Name>  
          </Table>  
        </Schema>  
      </Database>  
    </Server>  
    <Workload>  
<!-- The following element specifies a workload file, which can be a trace file or a Transact-SQL script file. -->  
      <File>c:\PathToYourWorkloadFile</File>  
    </Workload>  
    <TuningOptions>  
      <TuningTimeInMin>180</TuningTimeInMin>  
      <StorageBoundInMB>10000</StorageBoundInMB>  
      <FeatureSet>IDX_IV</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
      <OnlineIndexOperation>OFF</OnlineIndexOperation>  
    </TuningOptions>  
    <Configuration SpecificationMode="Absolute">  
      <Server>  
        <Name>MyServerName</Name>  
          <Database>  
            <Name>MyDatabaseName</Name>  
            <Schema>  
              <Name>MyDatabaseSchemaName</Name>  
                <Table>  
                  <Name>MyTableName1</Name>  
                  <Recommendation>  
                    <Create>  
                      <Index Clustered="true" Unique="false" Online="false" IndexSizeInMB="873.75">  
                        <Name>MyIndexName</Name>  
                        <Column Type="KeyColumn" SortOrder="Ascending">  
                          <Name>MyColumnName1</Name>  
                        </Column>  
                        <Filegroup>MyFileGroupName1</FileGroup>  
                      </Index>  
                    </Create>  
                  </Recommendation>  
                </Table>  
            </Schema>  
          </Database>  
      </Server>  
    </Configuration>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="comments"></a>Comentários  
  
-   A remoção das estruturas de design físico não terá suporte caso você especifique o modo **Absoluto** para o elemento **Configuration** (`Configuration SpecificationMode="Absolute"`).  
  
-   Não é possível criar e remover a mesma estrutura de design físico em qualquer um dos modos (**Relative** ou **Absolute**) do elemento **Configuration** .  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

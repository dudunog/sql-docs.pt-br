---
title: Propriedades personalizadas OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 039b36c2092d9e08e81802e441f42587be66445c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298156"
---
# <a name="ole-db-custom-properties"></a>Propriedades personalizadas OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Propriedades personalizadas de fontes**  
  
 A origem OLE DB tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem de OLE DB. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar o banco de dados. Os valores possíveis são **Abrir Conjunto de Linhas**, **Abrir Conjunto de Linhas da Variável**, **Comando do SQL**e **Comando SQL da Variável**. O valor padrão é **Abrir Conjunto de Linhas**.|  
|AlwaysUseDefaultCodePage|Boolean|Um valor que indica se o valor da propriedade **DefaultCodePage** deve ser usado para todas as colunas ou para tentar derivar a página de código da localidade de cada coluna. O valor padrão dessa propriedade é **False**.|  
|CommandTimeOut|Integer|O número de segundos antes de um comando expirar. Um valor de 0 indica que nunca expirará.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Origem de OLE DB**, mas pode ser definida usando o **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código a ser usada quando informações de página de código não estão disponíveis na fonte de dados.|  
|OpenRowset|String|O nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|OpenRowsetVariable|String|A variável que contém o nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|ParameterMapping|String|O mapeamento de parâmetros no comando SQL para variáveis.|  
|SqlCommand|String|O comando SQL a ser executado.|  
|SqlCommandVariable|String|A variável que contém o comando do SQL a ser executado.|  
  
 A saída e as colunas de saída da origem OLE DB não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino OLE DB tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino OLE DB. Todas as propriedades são de leitura/gravação.  
  
> [!NOTE]  
>  As opções de FastLoad listadas aqui (FastLoadKeepIdentity, FastLoadKeepNulls e FastLoadOptions) correspondem às propriedades de nomes parecidas expostas pela interface **IRowsetFastLoad** implementada pelo Provedor Microsoft OLE DB para SQL Server (SQLOLEDB). Para obter mais informações, procure por IRowsetFastLoad na Biblioteca MSDN.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica como o destino acessa o seu banco de dados de destino.<br /><br /> Essa propriedade pode ter um dos seguintes valores:<br /><br /> <br /><br /> **OpenRowset** (0) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset from Variable** (1) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload** (3) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload from Variable** (4) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **Comando SQL** (2) – Forneça uma instrução SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Um valor que indica se o valor da propriedade **DefaultCodePage** deve ser usado para todas as colunas ou para tentar derivar a página de código da localidade de cada coluna. O valor padrão dessa propriedade é **False**.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor 0 indica que não há limite de tempo. O valor padrão dessa propriedade é 0.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Destinos OLE DB**, mas pode ser definida no **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código padrão associada ao destino OLE DB.|  
|FastLoadKeepIdentity|Boolean|Um valor que especifica se os valores de identidade devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**. Essa propriedade corresponde à propriedade [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) do OLE DB **SSPROP_FASTLOADKEEPIDENTITY**.|  
|FastLoadKeepNulls|Boolean|Um valor que especifica se os valores Nulos devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**. Essa propriedade corresponde à propriedade [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) do OLE DB **SSPROP_FASTLOADKEEPNULLS**.|  
|FastLoadMaxInsertCommitSize|Integer|Um valor que especifica o tamanho do lote que o destino OLE DB tenta confirmar durante as operações de carregamento rápido. O valor padrão, **0**, indica uma única operação de confirmação após o processamento de todas as linhas.|  
|FastLoadOptions|String|Uma coleção de opções de carregamento rápido. As opções de carregamento rápido incluem o bloqueio de tabelas e a verificação de restrições. É possível especificar uma, ambas ou nenhuma. Essa propriedade corresponde à propriedade IRowsetFastLoad do OLE DB **SSPROP_FASTLOADOPTIONS** e aceita opções de cadeia de caracteres como **CHECK_CONSTRAINTS** e **TABLOCK**.<br /><br /> Observação: Algumas opções dessa propriedade não estão disponíveis no **Editor de Destinos Excel**, mas podem ser definidas no **Editor Avançado**.|  
|OpenRowset|String|Quando AccessMode é **OpenRowset**, o nome da tabela ou exibição acessada pelo destino OLE DB.|  
|OpenRowsetVariable|String|Quando AccessMode é **OpenRowset from Variable**, o nome da variável que contém o nome da tabela ou exibição acessada pelo destino OLE DB.|  
|SqlCommand|String|Quando AccessMode é **Comando SQL**, a instrução Transact-SQL usada pelo destino OLE DB para especificar as colunas de destino dos dados.|  
  
 A entrada e as colunas de entrada do destino OLE DB não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

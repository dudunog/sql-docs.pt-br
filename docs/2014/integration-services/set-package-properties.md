---
title: Definir as propriedades do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 917c5af173fa1e7087d47789b17b0845ab426dad
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963356"
---
# <a name="set-package-properties"></a>Definir as propriedades do pacote
  Ao criar um pacote no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] usando a interface gráfica fornecida pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você define as propriedades do objeto do pacote na janela Propriedades.  
  
 A janela **Propriedades** fornece uma lista de propriedades categorizada e alfabética. Para classificar a janela **Propriedades** por categoria, clique no ícone Categorizado.  
  
 Quando organizada por categoria, a janela **Propriedades** agrupa propriedades nas seguintes categorias:  
  
-   [Pontos de Verificação](#Checkpoints)  
  
-   [Execução](#Execution)  
  
-   [Valor de Execução Forçada](#ForcedExecutionValue)  
  
-   [Identificação](#Identification)  
  
-   [Diversos](#Misc)  
  
-   [Segurança](#Security)  
  
-   [Transações](#Transactions)  
  
-   [Versão](#Version)  
  
 Para obter informações sobre as propriedades de pacote adicionais que você não pode definir na janela **Propriedades** , consulte <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>Para definir as propriedades de pacote na janela Propriedades  
  
-   [Definir as propriedades de um pacote](../../2014/integration-services/set-the-properties-of-a-package.md)  
  
## <a name="properties-by-category"></a>Propriedades por Categoria  
 As tabelas a seguir listam as propriedades de pacote por categoria.  
  
###  <a name="checkpoints"></a><a name="Checkpoints"></a> Pontos de Verificação  
 Você pode usar as propriedades nessa categoria para reiniciar o pacote a partir de um ponto de falha no fluxo de controle do pacote, em vez de executar novamente o pacote desde o começo de seu fluxo de controle. Para saber mais, confira [Restart Packages by Using Checkpoints](packages/restart-packages-by-using-checkpoints.md).  
  
|Propriedade|DESCRIÇÃO|  
|--------------|-----------------|  
|`CheckpointFileName`|O nome do arquivo que captura as informações do ponto de verificação que permite a reinicialização de um pacote. Quando o pacote é concluído com sucesso, este arquivo é excluído.|  
|`CheckpointUsage`|Especifica quando um pacote pode ser reinicializado. Os valores são `Never`, `IfExists` e `Always`. O valor padrão dessa propriedade é `Never`, que indica que o pacote não pode ser reinicializado. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|`SaveCheckpoints`|Especifica se os pontos de verificação são gravados no arquivo de ponto de verificação quando o pacote é executado. O valor padrão dessa propriedade é `False`.|  
  
> [!NOTE]  
>  A opção `/CheckPointing on` do dtexec equivale à configuração da propriedade `SaveCheckpoints` do pacote como True e da propriedade `CheckpointUsage` como Sempre. Para saber mais, veja [dtexec Utility](packages/dtexec-utility.md).  
  
###  <a name="execution"></a>Execução do <a name="Execution"></a>  
 As propriedades nesta categoria configuram o comportamento de tempo de execução do objeto de pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`DelayValidation`|Indica se a validação do pacote está adiada até que o pacote seja executado. O valor padrão para essa propriedade é `False`.|  
|**Desabilitar**|Indica se o pacote está desabilitado ou não. O valor padrão dessa propriedade é `False`.|  
|`DisableEventHandlers`|Especifica se os manipuladores de eventos de pacote são executados. O valor padrão dessa propriedade é `False`.|  
|`FailPackageOnFailure`|Especifica se o pacote falha caso ocorra um erro em um componente de pacote. O único valor válido dessa propriedade é `False`.|  
|`FailParentOnError`|Especifica se o contêiner pai falha caso ocorra um erro em um contêiner filho. O valor padrão dessa propriedade é `False`.|  
|`MaxConcurrentExecutables`|O número de arquivos executáveis que o pacote pode executar simultaneamente. O valor padrão dessa propriedade é **-1**, que indica que não há nenhum limite.|  
|`MaximumErrorCount`|O número máximo de erros que podem acontecer antes de um pacote parar de ser executado. O valor padrão dessa propriedade é **1**.|  
|`PackagePriorityClass`|A classe de prioridade de thread Win32 do thread de pacote. Os valores são `Default`, `AboveNormal`, `Normal`, `BelowNormal`, `Idle`. O valor padrão dessa propriedade é `Default`. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="forced-execution-value"></a><a name="ForcedExecutionValue"></a>Valor de execução forçada  
 As propriedades dessa categoria configuram um valor de execução opcional para o pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`ForcedExecutionValue`|Se ForceExecutionValue for definido como `True` , um valor que especifica o valor de execução opcional que o pacote retorna. O valor padrão dessa propriedade é **0**.|  
|`ForcedExecutionValueType`|O tipo de dados de ForcedExecutionValue. O valor padrão dessa propriedade é `Int32`.|  
|`ForceExecutionValue`|Um valor Booliano que especifica se o valor de execução opcional do contêiner deve ser forçado a conter um valor específico. O valor padrão dessa propriedade é `False`.|  
  
###  <a name="identification"></a><a name="Identification"></a>ID  
 As propriedades dessa categoria fornecem informações como o identificador exclusivo e o nome do pacote.  
  
|Propriedade|DESCRIÇÃO|  
|--------------|-----------------|  
|`CreationDate`|A data em que o pacote foi criado.|  
|`CreatorComputerName`|O nome do computador no qual o pacote foi criado.|  
|`CreatorName`|O nome da pessoa que criou o pacote.|  
|`Description`|Uma descrição da funcionalidade do pacote.|  
|`ID`|O GUID do pacote, que é atribuído quando o pacote é criado. Essa propriedade é somente leitura. Para gerar um novo valor aleatório para a `ID` propriedade, selecione **\<Generate New ID>** na lista suspensa.|  
|`Name`|O nome do pacote.|  
|`PackageType`|O tipo do pacote. Os valores são `Default`, `DTSDesigner`, `DTSDesigner100`, `DTSWizard`, `SQLDBMaint` e `SQLReplication`. O valor padrão dessa propriedade é `Default`. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="misc"></a><a name="Misc"></a>Diversos  
 As propriedades desta categoria são usadas para acessar as configurações e expressões que um pacote usa e para fornecer informações sobre a localidade e o modo de log do pacote. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`Configurations`|A coleção de configurações que o pacote usa. Clique no botão Procurar **(…)** para exibir e configurar as configurações do pacote.|  
|`Expressions`|Clique no botão Procurar **(…)** para criar expressões para as propriedades do pacote.<br /><br /> Observação: você pode criar expressões de propriedade para todas as propriedades de pacote que o modelo de objeto inclui, não apenas as propriedades listadas no janela Propriedades.<br /><br /> Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md).<br /><br /> Para exibir expressões de propriedade existentes, expanda `Expressions`. Clique no botão Procurar **(…)** em uma caixa de texto de expressão para modificar e avaliar uma expressão.|  
|`ForceExecutionResult`|O resultado de execução do pacote. Os valores são `None`, `Success`, `Failure` e `Completion`. O valor padrão dessa propriedade é `None`. Para obter mais informações, consulte T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|`LocaleId`|É uma localidade do Microsoft Win32. O valor padrão dessa propriedade é a localidade do sistema operacional no computador local.|  
|`LoggingMode`|Um valor que especifica o comportamento de log do pacote. Os valores são `Disabled`, `Enabled` e `UseParentSetting`. O valor padrão dessa propriedade é `UseParentSetting`. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|`OfflineMode`|Indica se o pacote está no modo offline. Essa propriedade é somente leitura. A propriedade é definida no nível de projeto. Geralmente, o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] tenta se conectar a cada fonte de dados usada por seu próprio pacote para validar os metadados associados às fontes e aos destinos. Você pode habilitar **Trabalhar Offline** no menu **SSIS** , até mesmo antes de abrir um pacote, para evitar essas tentativas de conexão, e os erros de validação resultantes quando as fontes de dados não estão disponíveis. Você também pode habilitar a opção **Trabalhar Offline** para acelerar as operações no designer e a desabilitar apenas quando você desejar validar seu pacote.|  
|`SuppressConfigurationWarnings`|Indica se os avisos gerados por configurações são suprimidos. O valor padrão dessa propriedade é `False`.|  
|`UpdateObjects`|Indica se o pacote está atualizado para usar versões mais novas dos objetos que contém, se essas versões estiverem disponíveis. Por exemplo, se essa propriedade estiver definida como `True`, um pacote que inclua uma tarefa Inserção em Massa será atualizado para usar a versão mais nova da tarefa Inserção em Massa que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece. O valor padrão dessa propriedade é `False`.|  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 As propriedades nesta categoria são usadas para definir o nível de proteção do pacote. Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`PackagePassword`|A senha para os níveis de proteção do pacote ( `EncryptSensitiveWithPassword` e `EncryptAllWithPassword` ) que exigem senhas.|  
|`ProtectionLevel`|O nível de proteção do pacote. Os valores são `DontSaveSensitive` , `EncryptSensitiveWithUserKey` , `EncryptSensitiveWithPassword` , `EncryptAllWithPassword` e **ServerStorage**. O valor padrão dessa propriedade é `EncryptSensitiveWithUserKey`. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="transactions"></a><a name="Transactions"></a>Transações  
 As propriedades nesta categoria configuram o nível de isolamento e a opção de transação do pacote. Para obter mais informações, consulte [Transações do Integration Services](integration-services-transactions.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`IsolationLevel`|O nível de isolamento da transação do pacote.  O valor padrão dessa propriedade é `Serializable`. Os valores válidos são <br />`Unspecified`<br />`Chaos`<br />`ReadUncommitted`<br />`ReadCommitted`<br />`RepeatableRead`<br />`Serializable`<br />`Snapshot`.<br /><br /> O sistema aplica a propriedade `IsolationLevel` às transações de pacote somente quando o valor da propriedade `TransactionOption` está definido como `Required`.<br /><br /> O valor da propriedade `IsolationLevel` solicitado por um contêiner filho é ignorado quando as seguintes condições forem verdadeiras:<br /><br /> O valor da propriedade `TransactionOption` do contêiner filho é `Supported`.<br />O contêiner filho une-se à transação de um contêiner pai.<br /><br /> O valor da propriedade `IsolationLevel` solicitada pelo contêiner é respeitado apenas quando o contêiner inicia uma nova transação. Um contêiner iniciará uma nova transação quando as seguintes condições forem verdadeiras:<br /><br /> O valor da propriedade `TransactionOption` do contêiner for `Required`.<br />O pai ainda não iniciou uma transação.<br /><br /> <br /><br /> Observação: o valor `Snapshot` da propriedade `IsolationLevel` é incompatível com transações de pacote. Portanto, você não pode usar a propriedade `IsolationLevel` para definir o nível de isolamento das transações de pacote como `Shapshot`. Em vez disso, use uma consulta SQL para definir as transações de pacote como `Snapshot`. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).<br /><br /> Para obter mais informações sobre a propriedade `IsolationLevel`, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|`TransactionOption`|A participação transacional do pacote. Os valores são `NotSupported` , `Supported` , `Required` . O valor padrão dessa propriedade é `Supported`. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="version"></a><a name="Version"></a>Versão  
 As propriedades nesta categoria fornecem informações sobre a versão do objeto de pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`VersionBuild`|O número de versão da criação do pacote.|  
|`VersionComments`|Comentários sobre a versão do pacote.|  
|`VersionGUID`|O GUID da versão do pacote. Essa propriedade é somente leitura.|  
|`VersionMajor`|A versão principal mais recente do pacote.|  
|`VersionMinor`|A versão secundária mais recente do pacote.|  
  
  

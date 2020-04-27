---
title: Editor da tarefa sistema de arquivos (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 594b87b3e2d58ffe60bd3c31324811a66038c82b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058809"
---
# <a name="file-system-task-editor-general-page"></a>Editor da Tarefa Sistema de Arquivos (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Sistema de Arquivos** para configurar a operação de sistema de arquivos que a tarefa executa.  
  
 Para obter informações sobre essa tarefa, consulte [File System Task](control-flow/file-system-task.md).  
  
 Você deve especificar um gerenciador de conexões de origem e destino, definindo as propriedades SourceConnection e DestinationConnection. Você pode fornecer os nomes dos gerenciadores de conexões de Arquivo que apontam para os arquivos que a tarefa usa como origem ou destino ou, se os caminhos dos arquivos estiverem armazenados em variáveis, fornecer os nomes das variáveis. Antes de usar variáveis para armazenar os caminhos de arquivo, defina as opções IsSourcePathVariable, para a conexão de origem, e IsDestinationPatheVariable, para a conexão de destino, como **True**. Em seguida, opte por utilizar as variáveis do sistema ou definidas pelo usuário existentes, ou então, crie novas variáveis. Na caixa de diálogo **Adicionar Variável** , é possível configurar e especificar o escopo das variáveis. O escopo deve ser a tarefa Sistema de Arquivos ou um contêiner pai. Para obter mais informações, consulte [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md) e [usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md).  
  
> [!NOTE]  
>  Para substituir `SourceConnection` as variáveis selecionadas para as propriedades e `DestinationConnection` , insira uma expressão para as propriedades de **origem** e de **destino** . Insira expressões na página **Expressões** do **Editor da Tarefa Sistema de Arquivos**. Por exemplo, para definir o caminho dos arquivos que a tarefa usa como um destino, você pode querer usar a variável A sob determinadas condições e usar a variável B sob outras condições.  
  
> [!NOTE]  
>  A tarefa Sistema de Arquivos funciona em um único arquivo ou diretório. Por isso, essa tarefa não dá suporte a uso de caracteres curingas para executar a mesma operação em vários arquivos ou diretórios. Para fazer com que uma tarefa Sistema de Arquivos repita uma operação em vários arquivos ou diretórios, coloque-a em um contêiner Loop Foreach. Para obter mais informações, consulte [File System Task](control-flow/file-system-task.md).  
  
 Você pode usar expressões para usar variáveis diferentes para o  
  
## <a name="options"></a>Opções  
 **IsDestinationPathVariable**  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**True**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
|**For**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. A seleção desse valor exibe a opção dinâmica `DestinationConnection`,.|  
  
 **OverwriteDestination**  
 Especifique se a operação pode substituir arquivos no diretório de destino.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Sistema de Arquivos. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Sistema de Arquivos.  
  
 **Operação**  
 Selecione a operação de sistema de arquivos a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Copiar diretório**|Copiar um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Copiar arquivo**|Copia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Criar diretório**|Criar um diretório. A seleção deste valor exibe as opções dinâmicas para um diretório de origem e destino.|  
|**Excluir diretório**|Exclui um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir conteúdo do diretório**|Exclui o conteúdo de um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir arquivo**|Exclui um arquivo. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Mover diretório**|Move um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Mover arquivo**|Move um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino.<br /><br /> Observação: ao mover um arquivo, não inclua um nome de arquivo no caminho do diretório que você fornece como o destino.|  
|**Renomear arquivo**|Renomeia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino.<br /><br /> Observação: ao renomear um arquivo, inclua o novo nome de arquivo no caminho do diretório que você forneceu para o destino.|  
|**Definir atributos**|Define os atributos de um arquivo ou diretório. A seleção desse valor exibe as opções dinâmicas para origem e operação.|  
  
 `IsSourcePathVariable`  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor||  
|-----------|-|  
|**True**|O caminho de destino é armazenado em uma variável. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|  
|**For**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>Opções dinâmicas de IsDestinationPathVariable  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Selecione o nome da variável na lista ou clique em \< **nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<em **nova conexão...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>Opções dinâmicas de IsSourcePathVariable  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Selecione o nome da variável na lista ou clique em \< **nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<em **nova conexão...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Opções dinâmicas de operação  
  
### <a name="operation--set-attributes"></a>Operação = Definir atributos  
 **Oculto**  
 Indique se o arquivo ou diretório deve ficar visível.  
  
 **ReadOnly**  
 Indique se o arquivo é somente leitura.  
  
 **Archive**  
 Indique se o arquivo ou diretório está pronto para ser arquivado.  
  
 **Sistema**  
 Indique se o arquivo é um arquivo do sistema operacional.  
  
### <a name="operation--create-directory"></a>Operação = Criar diretório  
 `UseDirectoryIfExists`  
 Indica se a operação **Criar diretório** usa um diretório existente com o nome especificado, em vez de criar um novo diretório.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  

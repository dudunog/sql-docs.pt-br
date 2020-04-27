---
title: Editor da tarefa Enviar email (página email) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- Send Mail Task Editor
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d80ca8e475bf9c2b56c11118a44e5282573f280d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055827"
---
# <a name="send-mail-task-editor-mail-page"></a>Editor da tarefa Enviar Email (página Email)
  Use a página **Email** da caixa de diálogo do **Editor da Tarefa Enviar Email** para especificar destinatários, o tipo de mensagem e a prioridade de uma mensagem. Você também pode anexar arquivos à mensagem. O texto da mensagem pode ser uma cadeia de caracteres fornecida por você, uma conexão com um arquivo que contém o texto ou o nome de uma variável que contém o texto.  
  
 Para obter informações sobre essa tarefa, consulte [Send Mail Task](control-flow/send-mail-task.md).  
  
## <a name="options"></a>Opções  
 **SMTPConnection**  
 Selecione um Gerenciador de conexões SMTP na lista ou clique em ** \<nova conexão... >** para criar um novo Gerenciador de conexões.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
 **Tópicos relacionados:** [Gerenciador de conexões SMTP](connection-manager/smtp-connection-manager.md)  
  
 **De**  
 Especifique o endereço de email do remetente.  
  
 **Para**  
 Forneça os endereços de email dos destinatários, separados por ponto-e-vírgula.  
  
 **CC**  
 Especifique os endereços de email de outras pessoas que também receberão cópias da mensagem, separando todos os emails por ponto-e-vírgula.  
  
 **Cco**  
 Especifique os endereços de email de outras pessoas que também receberão cópias da mensagem com cópia oculta (Cco), separando todos os emails por ponto-e-vírgula.  
  
 **Assunto**  
 Indique o assunto da mensagem de email.  
  
 **MessageSourceType**  
 Selecione o tipo de origem da mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem do texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
|**Conexão do Arquivo**|Defina a origem do arquivo que contém o texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
|**Variável**|Defina a origem de uma variável que contém o texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
  
 **Priority**  
 Defina a prioridade da mensagem.  
  
 **Anexos**  
 Forneça os nomes de arquivo dos anexos à mensagem de email, separados por uma barra vertical (|).  
  
> [!NOTE]  
>  As linhas Para, Cc e Cco são limitadas a 256 caracteres, de acordo com os padrões da Internet.  
  
## <a name="messagesourcetype-dynamic-options"></a>Opções dinâmicas de MessageSourceType  
  
### <a name="messagesourcetype--direct-input"></a>MessageSourceType = Entrada direta  
 **MessageSource**  
 Digite o texto da mensagem ou clique no botão Procurar (...) e digite a mensagem na caixa de diálogo **Origem da mensagem**.  
  
### <a name="messagesourcetype--file-connection"></a>MessageSourceType = Conexão do arquivo  
 **MessageSource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="messagesourcetype--variable"></a>MessageSourceType = Variável  
 **MessageSource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Enviar email &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  

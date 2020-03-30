---
title: Criar e gerenciar atribuições de função | Microsoft Docs
ms.date: 05/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 863904e2d82fc97045305dd2430241a91e333f11
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65619597"
---
# <a name="create-and-manage-role-assignments"></a>Criar e gerenciar atribuições de função

Um *atribuição de função* é uma política de segurança que determina as permissões do usuário ou do grupo. As permissões decidem se o usuário ou grupo pode acessar ou modificar um item de servidor de relatório específico ou executar uma tarefa. Uma atribuição de função consiste em um único nome de conta de usuário ou grupo e em uma ou mais definições de função.

As atribuições de função podem afetar o *nível do item* ou o *nível do sistema*.

- Uma atribuição de função em nível de item é criada para um item ou ramificação específica na hierarquia de pastas no servidor de relatório. Navegue até uma pasta específica ou item para criar uma atribuição de função.

- As atribuições de função no nível do sistema fornecem aos usuários selecionados a possibilidade de realizar tarefas que afetam o site de servidor de relatório como um todo. Essas tarefas incluem:
  - Criar agendas compartilhadas
  - Gerenciar trabalhos
  - Processar relatórios
  - Definir propriedades

A segurança no nível do sistema não permite o acesso a itens na hierarquia de pastas do servidor de relatório.

## <a name="creating-an-item-level-role-assignment"></a>Criando uma atribuição de função em nível de item

A partir desse ponto, você poderá criar uma atribuição de função separada para cada conta de usuário ou grupo que requer acesso ao servidor de relatório. Se a conta estiver em um domínio diferente do domínio que contém o servidor de relatório, inclua o nome de domínio. Depois de especificar uma conta, você escolhe uma ou mais definições de função. As definições de função são aditivas. O conjunto combinado de todas as tarefas de todas as definições é suportado na atribuição para um grupo ou usuário específico.

Para permitir o acesso completo, escolha um item que esteja no nível superior da hierarquia de pastas (por exemplo, o pasta raiz Início). Depois você pode criar atribuições de função para bloquear áreas específicas de nível inferior da hierarquia de pastas.

Você deve ser membro do grupo de Administradores local no computador do servidor de relatório para criar uma atribuição de função. Você pode delegar essa responsabilidade atribuindo outros usuários à função **Gerenciador de Conteúdo** .

Para criar ou gerenciar atribuições de função ou para saber mais, confira [Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md)
  
## <a name="creating-a-system-level-role-assignment"></a>Criando uma atribuição de função no nível do sistema

As atribuições de função em nível de sistema e de item são criadas juntas. Crie uma atribuição de função em nível de sistema para cada usuário ou grupo que tem uma atribuição de função em nível de item.

As atribuições de função em nível de sistema incluem uma ampla variedade de permissões, mas não incluem permissões que fazem parte de uma atribuição de função em nível de item.

Em contraste com as permissões de sistema em um computador, as funções de sistema no servidor de relatório não concedem permissões de longo alcance que incluem todas as tarefas possíveis. Em vez disso, as atribuições de função no nível do sistema simplesmente são um conjunto de tarefas que afetam o site do servidor de relatório. Atribuições de função de sistema determinam se os usuários podem exibir propriedades de aplicativo (como a imagem ou o título da página inicial), exibir ou gerenciar agendas compartilhadas ou usar o Construtor de Relatórios.

Para criar ou gerenciar uma atribuição de função em nível de sistema ou para saber mais, confira [Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md) e [Funções Predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md).  

## <a name="modifying-a-role-assignment"></a>Modificando atribuições de função

Você pode modificar uma atribuição de função a qualquer momento. Suas alterações entram em vigor quando você salva a atribuição de função. As sessões de usuário não são afetadas pelas alterações da atribuição de função. Se um usuário tiver um relatório aberto e você modificar uma atribuição de função para negar o acesso, o usuário pode continuar usando o relatório para aquela sessão ativa.

Se você adicionar uma conta de usuário a um grupo que já faz parte de uma atribuição de função, haverá um retardo antes que a conta de usuário consiga acessar itens da alteração. Esse retardo é causado pelo armazenamento em cache do IIS de tokens de autenticação. Você pode aguardar a atualização dos tokens (normalmente 15 minutos) ou redefinir o IIS para atualizar o cache imediatamente.

Você pode modificar só uma atribuição de função de cada vez. Não é possível executar uma operação de localização e substituição global para alterar nomes de definição de função, configurações de atribuição de função, nem para localizar todas as atribuições de função que incluem um usuário ou grupo específico.

## <a name="deleting-a-role-assignment"></a>Excluindo atribuições de função

Você pode excluir atribuições de função marcando a caixa de seleção de cada atribuição que deseja excluir e clicando em **Excluir**. Você também pode excluir atribuições de função clicando em **Reverter em Segurança Pai**. Quando você seleciona esse botão, as atribuições de função existentes para o item são excluídas e substituídas com as atribuições herdadas do item pai.

## <a name="see-also"></a>Consulte Também

[Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md)  
[Atribuições de função](../../reporting-services/security/role-assignments.md)  
[Definições de função](../../reporting-services/security/role-definitions.md)  
[Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)  
[Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)

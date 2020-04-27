---
title: Página Segurança (Configurações de Site - Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: acc9a905-90f8-4544-aec6-b2ab3a1b0015
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6c0b0cc68c73c66dabb237d859aba641fb234647
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102179"
---
# <a name="security-page-site-settings-report-manager"></a>Página Segurança (Configurações de Site - Gerenciador de Relatórios)
  Use a página Segurança para exibir as atribuições de função do sistema que controlam acesso ao site do servidor de relatório. As atribuições de função do sistema existem fora do escopo do namespace de servidor de relatórios ou da hierarquia de pastas. As atribuições de função do sistema são globais e não variam para itens específicos. Operações que têm suporte nas atribuições de função do sistema incluem a criação e o uso de agendas compartilhadas, o uso do Construtor de Relatórios e configuração de valores padrão para alguns recursos de servidor.  
  
 Uma atribuição de função do sistema padrão é criada quando o servidor de relatório é instalado. Essa atribuição de função do sistema concede permissões a administradores de sistema locais para gerenciar o ambiente do servidor de relatório. Um administrador de sistema local sempre pode definir segurança para um servidor de relatório local, mesmo que as atribuições de função do sistema sejam excluídas.  
  
 Todos os outros usuários que necessitam de acesso ao Construtor de Relatórios ou a agendas compartilhadas devem ser designados para uma atribuição de função do sistema.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-security-page-for-site-settings"></a>Para abrir a página Segurança de Configurações de Site  
  
1.  Abra o Gerenciador de Relatórios.  
  
2.  Na parte superior da página, clique em **Configurações de Site**. Esse procedimento abre a página Propriedades Gerais do site.  
  
3.  Selecione a guia **Segurança**.  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Clique para excluir uma atribuição de função existente. Antes de clicar em **Excluir**, marque a caixa de seleção ao lado do nome do grupo ou usuário a ser removido. Você não poderá excluir uma atribuição de função se ela for a única. A exclusão de uma atribuição de função não exclui uma conta de grupo ou usuário, nem as definições da função.  
  
 **Atribuição de Nova Função**  
 Clique para abrir a página Atribuição de Nova Função do Sistema, a qual é usada para criar atribuições de função do sistema adicionais para o site do servidor de relatório. Para obter mais informações, consulte [novas atribuições de função do sistema: página Editar atribuições de função do sistema &#40;Report Manager&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md).  
  
 **Editar**  
 Clique para abrir a página Editar Atribuições de Função do Sistema, a qual é usada para editar atribuições de função do sistema individuais para o site do servidor de relatório. Para obter mais informações, consulte [novas atribuições de função do sistema: página Editar atribuições de função do sistema &#40;Report Manager&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md).  
  
 **Grupo ou Usuário**  
 Lista os grupos e usuários que fazem parte de uma atribuição de função existente. Atribuições de função existentes para a pasta atual são definidas para os grupos e usuários que aparecem nesta coluna. Clique em **Editar** ao lado de um grupo ou nome de usuário para exibir ou editar detalhes da atribuição da função.  
  
 **Funções**  
 Lista uma ou mais definições de função que fazem parte de uma atribuição de função existente. Se várias funções forem atribuídas a um grupo ou conta de usuário, esse grupo de usuários pode desempenhar todas as tarefas que pertencem a todas as funções. Para exibir o conjunto de tarefas que cada função dá suporte, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]use. Você não pode exibir, criar, modificar ou excluir funções no Gerenciador de Relatórios. Para obter instruções, consulte [criar, excluir ou modificar uma função &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 Report Manager](../../2014/reporting-services/report-manager-f1-help.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

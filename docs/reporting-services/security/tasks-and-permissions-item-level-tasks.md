---
title: Tarefas em nível de item | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7224b99b721a48f14467da7479137fb4c61d4da9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570275"
---
# <a name="tasks-and-permissions---item-level-tasks"></a>Tarefas e permissões – tarefas em nível de item
  Uma tarefa em nível de item é uma coleção de permissões relacionadas a um relatório, pasta, modelo de relatório, recurso ou fonte de dados compartilhada. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também inclui tarefas em nível do sistema que se aplicam ao site do servidor de relatório como um todo. Para obter mais informações, consulte [Tarefas de nível de sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md). Para obter mais informações sobre tarefas e permissões em geral, consulte [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Se você estiver trabalhando programaticamente com essas tarefas, deve usar métodos ofereçam suporte a tarefas de nível de item. Para obter mais informações, consulte <xref:ReportService2010.ReportingService2010.ListTasks%2A> e <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-item-level-tasks"></a>Permissões em tarefas de nível de item  
 A tabela a seguir relaciona tarefas de nível de item, as permissões incluídas em cada tarefa e os itens para os quais as permissões se aplicam. Permissões são listadas somente para fins informativos para fornecer uma descrição mais precisa da funcionalidade disponível em cada tarefa.  
  
 Conjuntos de dados compartilhados usam o mesmo conjunto de permissões dos relatórios. Partes de relatório usam o mesmo conjunto de permissões de Recursos.  
  
|Tarefa|Aplica-se ao item|Permissões|  
|----------|---------------------|-----------------|  
|Relatórios de consumo|Relatórios|Ler Conteúdo<br /><br /> Ler Definições de Relatório<br /><br /> Ler Propriedades|  
|Relatórios de consumo|Conjuntos de dados compartilhados|Ler Conteúdo<br /><br /> Ler Definições de Relatório<br /><br /> Ler Propriedades|  
|Criar relatórios vinculados|Relatórios|Criar Link<br /><br /> Ler Propriedades|  
|Gerenciar todas as assinaturas|Relatórios|Ler Propriedades<br /><br /> Ler Qualquer Assinatura<br /><br /> Criar Qualquer Assinatura<br /><br /> Excluir Qualquer Assinatura<br /><br /> Atualizar Qualquer Assinatura|  
|Gerenciar as fontes de dados|Pastas|Criar Fonte de Dados|  
|Gerenciar as fontes de dados|Fontes de dados|Atualizar Propriedades<br /><br /> Excluir Atualizar Conteúdo<br /><br /> Ler Propriedades|  
|Gerenciar pastas|Pastas|Criar pasta<br /><br /> Excluir Atualizar Propriedades<br /><br /> Ler Propriedades|  
|Administrar assinaturas individuais|Relatórios|Ler Propriedades<br /><br /> Criar Assinatura<br /><br /> Excluir Assinatura<br /><br /> Ler Assinatura<br /><br /> Atualizar Assinatura|  
|Gerenciar modelos|Pastas|Criar Modelo|  
|Gerenciar modelos|Modelos|Ler Propriedades<br /><br /> Ler Conteúdo<br /><br /> Excluir Atualizar Conteúdo<br /><br /> Ler Fontes de Dados<br /><br /> Atualizar Fontes de Dados<br /><br /> Ler Políticas de Autorização de Item de Modelo<br /><br /> Atualizar Políticas de Autorização de Item de Modelo<br /><br /> Excluir Atualizar Propriedades|  
|Gerenciar histórico de relatório|Relatórios|Ler Propriedades<br /><br /> Criar histórico de relatórios<br /><br /> Excluir Histórico de Relatório<br /><br /> Executar Política de Leitura<br /><br /> Atualizar Política<br /><br /> Listar Histórico de Relatório|  
|Gerenciar relatórios|Pastas|Criar Relatório<br /><br /> também se aplica à criação de conjuntos de dados compartilhados|  
|Gerenciar relatórios|Relatórios|Ler Propriedades<br /><br /> Excluir Atualizar Propriedades<br /><br /> Atualizar Parâmetros<br /><br /> Ler Fontes de Dados<br /><br /> Atualizar Fontes de Dados<br /><br /> Ler Definição de Relatório<br /><br /> Atualizar Definição de Relatório<br /><br /> Executar Política de Leitura<br /><br /> Atualizar Política|  
|Gerenciar relatórios|Conjuntos de dados compartilhados|Ler Propriedades<br /><br /> Excluir Atualizar Propriedades<br /><br /> Atualizar Parâmetros<br /><br /> Ler Fontes de Dados<br /><br /> Atualizar Fontes de Dados<br /><br /> Ler Definição de Relatório<br /><br /> Atualizar Definição de Relatório<br /><br /> Executar Política de Leitura<br /><br /> Atualizar Política|  
|Gerenciar recursos|Pastas|Criar recurso|  
|Gerenciar recursos|Recursos|Atualizar Propriedades<br /><br /> Excluir Atualizar Conteúdo<br /><br /> Ler Propriedades|  
|Gerenciar recursos|Partes de relatório|Atualizar Propriedades<br /><br /> Excluir Atualizar Conteúdo<br /><br /> Ler Propriedades|  
|Definir segurança para itens individuais|Relatórios, Recursos, Fontes de dados, Conjuntos de Dados Compartilhados, Pastas|Ler Políticas de Segurança Atualizar Políticas de Segurança|  
|Exibir fontes de dados|Fontes de dados|Ler Conteúdo<br /><br /> Ler Propriedades|  
|Exibir pastas|Pastas|Ler Propriedades<br /><br /> Executar e Exibir<br /><br /> Listar Histórico de Relatório|  
|Exibir modelos|Modelos de relatório|Ler Propriedades<br /><br /> Ler Conteúdo<br /><br /> Ler Fontes de Dados|  
|Exibir relatórios|Relatórios|Ler Conteúdo<br /><br /> Ler Propriedades|  
|Exibir relatórios|Conjuntos de dados compartilhados|Ler Conteúdo<br /><br /> Ler Propriedades|  
|Exibir recursos|Recursos|Ler Conteúdo<br /><br /> Ler Propriedades|  
|Exibir recursos|Partes de relatório|Ler Conteúdo<br /><br /> Ler Propriedades|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

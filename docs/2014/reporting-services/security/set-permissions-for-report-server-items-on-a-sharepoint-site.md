---
title: Definir permissões para itens do servidor de relatório em um site do SharePoint (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c8c0e8f0714efb337d78d4440938dcb5a332fcf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101559"
---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site-reporting-services-in-sharepoint-integrated-mode"></a>Definir permissões para itens de servidor de relatório em um site do SharePoint (Reporting Services no modo integrado do SharePoint)
  Se as configurações de segurança padrão não fornecerem o nível de acesso desejado, você poderá criar novos níveis de permissão para fornecer acesso a itens ou operações específicos do servidor de relatório. As configurações de segurança personalizadas podem ser úteis se você quiser restringir o acesso a um determinado relatório.  
  
 Você deve ser um proprietário de site para criar níveis de permissão e grupos. Níveis de permissão são usados em todo o site. Se um novo nível de permissão for criado, estará disponível para outros proprietários de site.  
  
 A maioria das permissões é herdada de um site pai. Se você atribuir permissões em uma biblioteca ou item específico, a herança de permissões será quebrada, acarretando uma sobrecarga adicional no gerenciamento de permissões para essa ramificação da hierarquia do seu site.  
  
 É possível definir permissões em arquivos de definição de relatório (.rdl), modelo (.smdl) e fonte de dados compartilhados (.rsds). Não é possível combinar permissões herdadas e gerenciadas no mesmo item. Se você optar por gerenciar permissões diretamente, as permissões herdadas não afetarão o item atual. Se desejar retomar a herança de permissões posteriormente, selecione **Herdar Permissões** no menu **Ações** .  
  
 Para definir permissões em entidades e perspectivas em um modelo, você deve ter o nível de permissão Controle Total no modelo. O nível Controle Total inclui a tarefa “Gerenciar Permissões”, uma permissão no nível do site concedida aos proprietários do site e outros grupos do SharePoint que possuem o nível de permissão Controle Total. Se desejar que usuários específicos possam definir a segurança do item de modelo, interrompa a herança de permissões e conceda permissões elevadas (como Controle Total) ao usuário ou grupo no arquivo do modelo. Ao conceder Controle Total em um item, como um arquivo da biblioteca, as permissões são delimitadas para esse item e não se estendem ao pai ou a outros itens da mesma biblioteca. Depois que o usuário tiver a permissão Gerenciar Permissões no modelo, poderá usar a segurança do item de modelo por meio do site do SharePoint ou do Designer de Modelo.  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>Para definir permissões em um relatório, modelo ou fonte de dados individual  
  
1.  Se a biblioteca ainda não estiver aberta, clique no seu nome no Início Rápido. Se o nome da biblioteca não for exibido, clique em **Exibir Todo o Conteúdo do Site**e, em seguida, clique no nome da biblioteca.  
  
2.  Aponte para o arquivo de relatório, modelo do relatório ou fonte de dados compartilhados.  
  
3.  Clique na seta para baixo e, no menu, clique em **Gerenciar Permissões**.  
  
4.  No menu **Ações** , clique em **Editar Permissões**e em **OK** para confirmar a ação.  
  
5.  Para atribuir permissões a um usuário ou grupo que ainda não possua permissões para usar o arquivo, clique em **Novo**e em **Adicionar Usuários**.  
  
6.  Para remover ou modificar permissões para um usuário ou grupo existente, clique na caixa de seleção ao lado do usuário ou grupo, clique em **Ações**e, em seguida, clique em **Remover Permissões do Usuário** ou **Editar Permissões do Usuário**.  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>Para definir permissões que habilitam a segurança do item de modelo  
  
1.  Faça logon no site do SharePoint usando uma conta que tenha a permissão Gerenciar Permissões no site.  
  
2.  Abra a biblioteca que contém o modelo.  
  
3.  Aponte para o modelo.  
  
4.  Clique na seta para baixo ao lado do modelo e clique em **Gerenciar Permissões**.  
  
5.  Clique em **Ações**.  
  
6.  Clique em **Editar Permissões**. Clique em **OK**.  
  
7.  Clique em **Nova**.  
  
8.  Clique em **Adicionar Usuários**.  
  
9. Em Usuários/Grupos, insira a conta de usuário.  
  
10. Selecione **Dar permissões a usuários diretamente**.  
  
11. Clique em **Controle Total**.  
  
12. Clique em **OK**. Após o usuário conseguir gerenciar permissões para um modelo específico, poderá abrir o modelo para editar permissões.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório](sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [Conceder permissões para itens do servidor de relatório em um site do SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  

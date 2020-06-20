---
title: Dependências de objeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 02fadc1b87393e02d1ff27f9596d6d7677e23cb3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058616"
---
# <a name="object-dependencies"></a>Dependências de objeto
  Alguns objetos de banco de dados têm dependências de outros objetos de banco de dados. Por exemplo, exibições e procedimentos armazenados dependem da existência de tabelas que contenham dados retornados pela exibição ou pelo procedimento. As **Dependências entre objetos (página Geral)** para o objeto atual lista ambos os objetos de banco de dados que devem estar presentes para o objeto funcionar corretamente e os objetos que dependem do objeto selecionado. Um objeto que faz referência a outro objeto em sua definição, e essa definição é armazenada no catálogo do sistema, é denominado *entidade de referência*. Um objeto que é referenciado por outro objeto é denominado *entidade referenciada*.  
  
 As **Dependências entre objetos (página Avançado)** do objeto atual lista os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que dependem do objeto. Os objetos podem ser armazenados em servidores diferentes.  
  
 Use esta caixa de diálogo para entender as dependências antes de alterar ou excluir o objeto selecionado.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Objetos que dependem de**  _\<selected object>_  
 Clicando neste botão, você exibe uma lista dos objetos que são rastreados por dependência e que dependem do objeto selecionado.  
  
 **Objetos nos quais** _\<selected object>_ **depende**      
 Clicando neste botão, você exibe uma lista dos objetos que são rastreados por dependência e dos quais depende o objeto selecionado.  
  
 **Dependências**  
 Se você clicar em **Objetos que dependem de** _\<selected object>_ , será exibida uma exibição hierárquica dos objetos que dependem do objeto selecionado. Se **Objetos dos quais** _\<selected object>_ **depende** for clicado, será exibida uma exibição hierárquica dos objetos dos quais o objeto selecionado depende.  
  
 **Nome**  
 Exibe o nome do objeto selecionado no modo de exibição de árvore **Dependências** acima.  
  
 **Tipo**  
 Exibe o tipo do objeto selecionado no modo de exibição de árvore **Dependências** acima.  
  
 **Hora da Última Sincronização**  
 > [!NOTE]  
>  Esta opção só está disponível na página **Avançado** .  
  
 Especifica a data e a hora em que as informações de dependência foram atualizadas pela última vez.  
  
 **Tipo de dependência**  
 > [!NOTE]  
>  Esta opção só está disponível na página **Geral** .  
  
 Exibe o tipo de dependência entre dois objetos. Um dos seguintes pode ser feito:  
  
-   Dependência associada a esquema  
  
     É uma relação entre dois objetos que impedem o objeto mencionado de ser descartado ou modificado desde que exista o objeto referenciado. Uma dependência associada a esquema é criada quando uma exibição ou função definida pelo usuário é criada usando a cláusula WITH SCHEMABINDING, ou quando uma tabela faz referência a outro objeto por uma restrição CHECK ou DEFAULT ou na definição de uma coluna computada.  
  
-   Dependência não associada a esquema  
  
     É uma relação entre dois objetos que não impedem o descarte ou a modificação do objeto referenciado.  
  
-   Entidade não disponível ou não resolvida  
  
     Indica que o tipo de dependência não pode ser determinado. Isso só acontece quando o objeto selecionado estiver em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
  

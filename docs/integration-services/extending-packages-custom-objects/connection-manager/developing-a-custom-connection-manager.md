---
description: Desenvolvendo um gerenciador de conexões personalizado
title: Desenvolver um gerenciador de conexões personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], connections
- custom connection managers [Integration Services], about custom connection managers
- connection managers [Integration Services], custom
- Integration Services packages, connection managers
- SSIS packages, connection managers
- SQL Server Integration Services packages, connection managers
- custom connection managers [Integration Services]
ms.assetid: bda0b29e-57f5-4879-b04d-1396dc56daa8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ad61fc88b68d2df7fb04839ef0f8fc3978a05e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484234"
---
# <a name="developing-a-custom-connection-manager"></a>Desenvolvendo um gerenciador de conexões personalizado

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa gerenciadores de conexões para encapsular as informações necessárias para conexão a uma fonte de dados externa. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui vários gerenciadores de conexões que dão suporte a conexões às fontes de dados usadas mais comumente, de bancos de dados corporativos a arquivos de texto e planilhas do Excel. Se os gerenciadores de conexões e as fontes de dados externas suportadas pelo [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] não satisfizerem totalmente os seus requisitos, você pode criar um gerenciador de conexões personalizado.  
  
 Para criar um gerenciador de conexões personalizado, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> a sua nova classe e substituir os métodos e as propriedades importantes da classe base, incluindo a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> e o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>.  
  
> [!IMPORTANT]  
>  A maioria das tarefas, fontes e destinos incluídos no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] funcionam somente com tipos específicos de gerenciadores de conexões internos. Antes de desenvolver um gerenciador de conexões personalizado para ser usado com tarefas e componentes internos, verifique se esses componentes restringem a lista de gerenciadores de conexões disponíveis para os de tipo específico. Se sua solução precisar de um gerenciador de conexões personalizado, é possível que você também tenha que desenvolver uma tarefa personalizada ou uma origem ou destino personalizado, para uso com o gerenciador de conexões.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção descreve como criar, configurar e codificar um gerenciador de conexões personalizado e sua interface de usuário personalizada opcional. Os snippets de códigos mostrados nesta seção foram retirados do exemplo de Gerenciador de Conexões Personalizado do SQL Server.  
  
 [Criando um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/creating-a-custom-connection-manager.md)  
 Descreve como criar as classes para um projeto de gerenciador de conexões personalizado.  
  
 [Codificando um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)  
 Descreve como implementar um gerenciador de conexões personalizado anulando os métodos e propriedades da classe base.  
  
 [Desenvolvendo uma interface do usuário para um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
 Descreve como implementar a classe de interface de usuário e o formulário usado para configurar o gerenciador de conexões personalizado.  
  
## <a name="related-sections"></a>Seções relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Aborda como programar tarefas personalizadas.  
  
 [Desenvolver um provedor de log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolver um enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Aborda como programar enumeradores personalizados.  
  
 [Desenvolver um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  

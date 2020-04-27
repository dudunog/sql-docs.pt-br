---
title: Caixa de diálogo Propriedades da Conexão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 350e48c225814052655e4fced89d2f934efa188f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62808394"
---
# <a name="connection-properties-dialog-box"></a>caixa de diálogo Propriedades da conexão
  Use essa caixa de diálogo para exibir as propriedades da conexão atual. Essa caixa de diálogo está disponível quando você clica em **Exibir propriedades da conexão** em várias caixas de diálogo do Pesquisador de Objetos. As propriedades exibidas nessa página são somente leitura.  
  
 Para alterar propriedades como **Banco de Dados**, conecte ao banco de dados desejado com o Pesquisador de Objetos antes de abrir a caixa de diálogo **Propriedades da Conexão** .  
  
 Observe que o período limite de consulta para o SQL Azure é de 30 minutos.  
  
## <a name="authentication"></a>Autenticação  
 Exiba propriedades de autenticação para a conexão atual. As propriedades de autenticação são o logon e método de autenticação quando a conexão foi estabelecida. Para alterar as propriedades de autenticação, desconectar de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e, em seguida, conectar o pesquisador de objetos ao servidor novamente, usando as opções de conexão desejadas.  
  
 **Método de autenticação**  
 O método de autenticação usado para a conexão atual.  
  
 **Nome de usuário**  
 O nome do usuário de logon usado para a autenticação da conexão.  
  
## <a name="connection-category"></a>Categoria de conexão  
 Exiba as propriedades de conexão para a conexão atual. A maioria das propriedades da conexão foi selecionada na guia **Propriedades da Conexão** da caixa de diálogo **Conectar ao servidor** durante o processo de conexão.  
  
 **Backup de banco de dados**  
 O nome do banco de dados ao qual se está conectado atualmente. Para alterar isso, use a barra de ferramentas do SQL Editor.  
  
 **SPID**  
 A ID do processo do sistema atribuída pelo servidor à conexão. Isso não pode ser alterado para essa conexão.  
  
 **Protocolo de rede**  
 O protocolo de rede da conexão do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Para alterar isso, conecte novamente com as propriedades de conexão desejadas.  
  
 **Tamanho do pacote de rede**  
 O tamanho de pacote usado ao comunicar com o servidor. Para alterar isso, conecte novamente com as propriedades de conexão desejadas.  
  
 **Tempo limite da conexão**  
 O intervalo de tempo em segundos a esperar quando conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] antes de atingir o tempo-limite e retornar ao usuário uma falha em conectar. Para alterar isso, conecte novamente com as propriedades de conexão desejadas.  
  
 **Tempo limite de execução**  
 O intervalo de tempo em segundos a aguardar antes que a execução de uma tarefa seja concluída no servidor. Para alterar isso, conecte novamente com as propriedades de conexão desejadas.  
  
 **Criptografado**  
 Se a conexão atual é criptografada. Para alterar isso, conecte novamente com as propriedades de conexão desejadas.  
  
## <a name="product-category"></a>Categoria do Produto  
 Exiba as propriedades do produto para a conexão atual. Essas propriedades descrevem o produto de servidor, versão, nome de instância e ordenação. As propriedades são definidas durante a instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Nome do produto**  
 O nome do produto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Versão do produto**  
 A versão do produto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Nome do servidor**  
 O nome do computador que executa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nome da instância**  
 Nome da instância do servidor. A instância padrão é em branco.  
  
 **Idioma**  
 A versão do idioma do produto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Ordenação**  
 A ordenação do servidor.  
  
## <a name="server-environment-category"></a>Categoria do ambiente do servidor  
 Exiba propriedades do ambiente do servidor para a conexão atual relacionadas ao hardware do servidor e sistema operacional. As propriedades não podem ser configuradas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nome do computador**  
 O nome do computador do servidor que está executando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Plataforma**  
 O nome do sistema operacional, nome do fabricante e família de CPU do servidor.  
  
 **Sistema operacional**  
 A versão do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows instalada no servidor.  
  
 **Processadores**  
 O número de processadores no servidor.  
  
 **Memória do Sistema Operacional**  
 O total de memória física no servidor, em megabytes.  
  
## <a name="see-also"></a>Consulte Também  
 [Páginas de propriedades no SQL Server Management Studio](../ssms/property-pages-in-sql-server-management-studio.md)   
 [Conectar ao servidor &#40;página Logon&#41; Mecanismo de Banco de Dados](../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  
  

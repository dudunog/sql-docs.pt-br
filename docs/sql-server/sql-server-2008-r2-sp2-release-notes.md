---
title: Notas de Versão do SQL Server 2008 R2 SP2 | Microsoft Docs
description: Este documento de Notas de Versão descreve problemas conhecidos sobre os quais você deve ler antes de instalar ou solucionar problemas do Microsoft SQL Server 2008 R2 Service Pack 2.
ms.prod: sql
ms.technology: release-landing
ms.custom: ''
ms.date: 07/22/2020
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: rothja
ms.author: jroth
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a8ed0a9892110f4469a9adeb4d586c8eec7f081c
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111017"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
Este documento de Notas de Versão descreve problemas conhecidos sobre os quais você deve ler antes de instalar ou solucionar problemas do Microsoft SQL Server 2008 R2 Service Pack 2. O documento de Notas de Versão aplica-se a todas as edições do SQL Server 2008 R2 SP2 e está disponível somente online. Ele é atualizado periodicamente.  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 O que há de novo no Service Pack 2  
Modo de exibição de gerenciamento dinâmico (DMV) adicionado **sys.dm_db_stats_properties**. Você pode usar essa DMV para retornar propriedades de estatísticas para uma tabela especificada ou exibição indexada no banco de dados atual. Por exemplo, essa DMV retorna o número de linhas da amostra e o número de etapas no histograma.  
  
## <a name="20-before-you-install"></a>2.0 Antes da instalação  
Para saber mais sobre como instalar atualizações do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] , veja a [Documentação de serviços do SQL Server 2008 R2](https://msdn.microsoft.com/library/dd638062(SQL.105).aspx).  
  
Para obter informações gerais sobre como iniciar e instalar o SQL Server 2008 R2, consulte o Leiame do SQL Server 2008 R2. O documento Leiame está disponível na mídia de instalação. Você também pode encontrar mais informações nos [Fóruns do SQL Server](https://social.msdn.microsoft.com/Forums/category/sqlserver/).
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 Escolha o arquivo correto para baixar e instalar  
Use a tabela a seguir para determinar qual arquivo baixar e instalar. Verifique se você tem os requisitos de sistema corretos antes de instalar o service pack. Os requisitos de sistemas são fornecidos nas páginas de download vinculadas na tabela.  
  
|Se a versão instalada atual for...|E você quiser...|Baixar e instalar...|  
|-------------------------------------------|----------------------|---------------------------|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2008 R2 ou SQL Server 2008 R2 SP1|Atualizar para a versão de 32 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 32 bits do SQL Server 2008 R2 RTM Express ou SQL Server 2008 R2 SP1 Express|Atualizar para a versão de 32 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 32 bits de somente ferramentas do cliente e de gerenciamento para o SQL Server 2008 R2 ou SQL Server 2008 R2 SP1 (incluindo SQL Server 2008 R2 Management Studio)|Atualizar as ferramentas do cliente e de gerenciamento para a versão de 32 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 32 bits do SQL Server 2008 R2 Management Studio Express ou SQL Server 2008 R2 SP1 Management Studio Express|Atualizar a versão de 32 bits do SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x86_ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2008 R2 ou SQL Server 2008 R2 SP1 **e** uma versão de 32 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2008 R2 RTM Management Studio)|Atualizar todos os produtos para a versão de 32 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 32 bits de uma ou mais ferramentas do [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272)|Atualizar as ferramentas para a versão de 32 bits do Microsoft SQL Server 2008 R2 SP2 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|Nenhuma instalação de 32 bits do SQL Server 2008 R2|Instalar o Server 2008 R2 incluindo SP2|Vá para [SQL Server 2008 R2 SP2 – Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) e siga as instruções.|  
|Nenhuma instalação de 32 bits do SQL Server 2008 R2 Management Studio|Instalar o SQL Server 2008 R2 Management Studio incluindo SP2|SQLManagementStudio_x86_ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251791) para instalar gratuitamente o SQL Server 2008 R2 SP2 Management Studio Express Edition.|  
|Uma versão de 64 bits de qualquer edição do SQL Server 2008 R2 ou SQL Server 2008 R2 SP1|Atualizar para a versão de 64 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU ou SQLServer2008R2SP2-KB2630455-IA64-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 64 bits do SQL Server 2008 R2 RTM Express ou SQL Server 2008 R2 SP1 Express|Atualizar para a versão de 64 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe ou SQLServer2008R2SP2-KB2630455-IA64-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 64 bits de somente o cliente e as ferramentas de gerenciamento para SQL Server 2008 R2 ou SQL Server 2008 R2 SP1 (incluindo SQL Server 2008 R2 Management Studio)|Atualizar o cliente e as ferramentas de gerenciamento para a versão de 64 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe ou SQLServer2008R2SP2-KB2630455-IA64-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 64 bits do SQL Server 2008 R2 Management Studio Express ou SQL Server 2008 R2 SP1 Management Studio Express|Atualizar a versão de 64 bits do SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x64_ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Uma versão de 64 bits de qualquer edição do SQL Server 2008 R2 ou SQL Server 2008 R2 SP1 **e** uma versão de 64 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2008 R2 RTM Management Studio)|Atualizar todos os produtos para a versão de 64 bits do SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Uma versão de 64 bits de uma ou mais ferramentas do [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272)|Atualizar as ferramentas para a versão de 64 bits do Microsoft SQL Server 2008 R2 SP2 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|Nenhuma instalação de 64 bits do SQL Server 2008 R2|Instalar o Server 2008 R2 incluindo SP2|Vá para [SQL Server 2008 R2 SP2 – Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) e siga as instruções.|  
|Nenhuma instalação de 64 bits do SQL Server 2008 R2 Management Studio|Instalar o SQL Server 2008 R2 Management Studio incluindo SP2|SQLManagementStudio_x64_ENU.exe [aqui](https://go.microsoft.com/fwlink/p/?LinkId=251791) para instalar gratuitamente o SQL Server 2008 R2 SP2 Management Studio Express Edition.|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 A instalação pode falhar se SQAGTRES.dll estiver bloqueado por outro processo  
**Problema**: uma operação de configuração do SQL Server pode falhar com este erro: `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` A causa raiz é que C:\Windows\system32\SQAGTRES.DLL está bloqueado por outro processo e a Instalação não foi capaz de atualizá-lo.  
  
**Solução alternativa**: renomeie C:\Windows\system32\SQAGTRES.DLL para um nome temporário, por exemplo, C:\Windows\system32\SQAGTRES_old.DLL e, em seguida, selecione a opção Tentar novamente na mensagem de erro de instalação. Isso fará a Instalação continuar. Depois de reinicializar, você poderá excluir o arquivo temporário C:\Windows\system32\SQAGTRES_old.DLL.  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 Problemas conhecidos corrigidos neste Service Pack  
Para obter uma lista completa de bugs e problemas conhecidos corrigidos neste service pack, consulte este [artigo mestre da Base de Dados de Conhecimento](https://support.microsoft.com/kb/2630455).  
  
## <a name="see-also"></a>Consulte Também  
[Como determinar a versão e a edição do SQL Server](https://support.microsoft.com/kb/321185)  
  

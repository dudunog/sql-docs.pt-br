---
title: MSSQLSERVER_2533 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2533 (Database Engine error)
ms.assetid: 0418352c-0ab2-4dc7-b8b9-5c3bad94560c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e87c0983ac7e74b45251bb72c44265f2134aa3b9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68103736"
---
# <a name="mssqlserver_2533"></a>MSSQLSERVER_2533
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2533|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_PAGE_WAS_NOT_SEEN|  
|Texto da mensagem|Erro de tabela: a página P_ID alocada à ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE) não foi vista. A página pode ser inválida ou ter uma ID de unidade de alocação incorreta em seu cabeçalho.|  
  
## <a name="explanation"></a>Explicação  
Uma página é alocada para a ID de unidade de alocação, *A_ID*, mas essa ID não está no cabeçalho da página. O cabeçalho tem outra ID de unidade de alocação. Se a ID de unidade de alocação contida no cabeçalho da página for de um objeto válido, talvez a página tenha um erro de incompatibilidade MSSQLEngine_2534.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Se não houver um backup limpo, execute DBCC CHECKDB sem uma cláusula REPAIR para determinar a extensão do dano. DBCC CHECKDB recomendará uma cláusula REPAIR para ser usada. Execute DBCC CHECKDB com a cláusula REPAIR apropriada para reparar o dano.  
  
> [!CAUTION]  
> Se você não tiver certeza do efeito de DBCC CHECKDB com uma cláusula REPAIR sobre seus dados, contate o provedor de suporte antes de executar essa instrução.  
  
Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.  
  
### <a name="results-of-running-repair-options"></a>Resultados da execução de opções REPAIR  
REPAIR desalocará a página. Se a página for de uma unidade de alocação de dados na linha, o índice, se houver, será recriado.  
  
> [!CAUTION]  
> Essa correção pode causar perda de dados.  
  
## <a name="see-also"></a>Consulte Também  
[MSSQLSERVER_2534](~/relational-databases/errors-events/mssqlserver-2534-database-engine-error.md)  
  

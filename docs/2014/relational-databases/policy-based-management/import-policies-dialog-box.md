---
title: Caixa de diálogo Importar Políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a0830e5db32fcc651b59114e1a2dad870e48d07
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62705236"
---
# <a name="import-policies-dialog-box"></a>Caixa de diálogo Importar Políticas
  Use esta caixa de diálogo para importar uma ou mais políticas (e suas condições referenciadas) salvas como arquivo XML na instância atual do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Arquivos a importar**  
 Para importar uma política de um arquivo XML, digite o caminho e o nome do arquivo ou use o botão Procurar ( **...** ).  
  
 **Substituir duplicatas por itens importados**  
 Selecione para substituir as políticas ou condições existentes com o mesmo nome, caso elas já existam nessa instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Uma condição com uma política dependente não pode ser substituída, a menos que a política dependente também esteja sendo substituída. Se esta opção não estiver selecionada uma condição existente que esteja usando a mesma expressão de condição não causará um erro.  
  
 **Estado da política**  
 Selecione o estado que você deseja para a política importada:  
  
-   **Preservar estado de política na importação**  
  
-   **Habilitar todas as políticas na importação**  
  
-   **Desabilitar todas as políticas na importação**  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md)   
 [Importar política de Gerenciamento Baseado em Políticas](import-a-policy-based-management-policy.md)   
 [Exportar uma política do gerenciamento baseado em políticas](export-a-policy-based-management-policy.md)  
  
  

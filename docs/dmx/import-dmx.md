---
title: IMPORTAR (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e17363aa255591977dc1a9e9ecb4ece04604814
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670076"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carrega um modelo de mineração ou estrutura de mineração de um arquivo .abf (Analysis Services Backup) no servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome do arquivo*  
 Uma cadeia de caracteres que contém o nome e o local do arquivo a ser importado.  
  
## <a name="remarks"></a>Comentários  
 Se nenhum objeto for especificado, serão carregados os conteúdos inteiros do arquivo .dmb. Se o arquivo .dmb incluir um banco de dados não existente no servidor, o banco de dados será criado.  
  
 É preciso ser um banco de dados ou administrador de servidor para exportar ou importar objetos.  
  
## <a name="import-from-file-example"></a>Exemplo de importar do arquivo  
 O exemplo a seguir importa todo o conteúdo do arquivo com o modelo e a estrutura de associação para o servidor atual.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &#40;DMX&#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  

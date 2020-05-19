---
title: Resultados do processo (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 060709db7842173f6f30e78a6384a4b9489dfb3d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712835"
---
# <a name="process-results-odbc"></a>Processar resultados (ODBC)
    
### <a name="to-process-results"></a>Para processar resultados  
  
1.  Recupere informações do conjunto de resultados.  
  
2.  Se forem usadas colunas associadas, para cada coluna à qual deseja associar, chame [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para associar um buffer de programa à coluna.  
  
3.  Para cada linha no conjunto de resultados:  
  
    -   Chame [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) para acessar a próxima linha.  
  
    -   Se forem usadas colunas associadas, use os dados disponíveis agora nos buffers de coluna associados.  
  
    -   Se forem usadas colunas desassociadas, chame [SQLGetData](../native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados dessas colunas depois da última coluna associada. As chamadas a `SQLGetData` deveriam estar em ordem crescente de número de coluna.  
  
    -   Chame `SQLGetData` várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Quando [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) sinalizar o término do conjunto de resultados retornando SQL_NO_DATA, chame [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) para determinar se há outro conjunto de resultados disponível.  
  
    -   Se SQL_SUCCESS for retornado, outro conjunto de resultados estará disponível.  
  
    -   Se SQL_NO_DATA for retornado, nenhum outro conjunto de resultados estará disponível.  
  
    -   Se SQL_SUCCESS_WITH_INFO ou SQL_ERROR for retornado, chame [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) para determinar se a saída de uma instrução PRINT ou RAISERROR estará disponível.  
  
         Se parâmetros de instrução associados forem usados para parâmetros de saída ou o valor retornado de um procedimento armazenado, use os dados disponíveis agora nos buffers de parâmetro associados. Além disso, quando são usados parâmetros associados, cada chamada para [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) ou [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) terá executado a instrução SQL por *S* vezes, em que *S* é o número de elementos na matriz de parâmetros associados. Isso significa que haverá *S* conjuntos de resultados a serem processados, em que cada conjunto de resultados inclui todos os conjuntos de resultados, parâmetros de saída e códigos de retorno geralmente retornados por uma única execução da instrução SQL.  
  
    > [!NOTE]  
    >  Quando um conjunto de resultados contém linhas computadas, cada linha computada é disponibilizada como um conjunto de resultados separado. Esses conjuntos de resultados computados são intercalados nas linhas normais e dividem as linhas normais em vários conjuntos de resultados.  
  
5.  Outra opção é chamar [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) com SQL_UNBIND para liberar qualquer buffer de coluna associado.  
  
6.  Se outro conjunto de resultados estiver disponível, vá para a Etapa 1.  
  
> [!NOTE]  
>  Para cancelar o processamento de um conjunto de resultados antes que [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) retorne SQL_NO_DATA, chame [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre o processamento de resultados &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  

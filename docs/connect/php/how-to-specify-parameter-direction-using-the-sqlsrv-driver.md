---
title: Como especificar a direção do parâmetro usando o driver SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf8169b2efa1c3016e98b61b34e9710635ac0d76
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993373"
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Como especificar a direção do parâmetro com o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve como usar o driver SQLSRV para especificar a direção do parâmetro ao chamar um procedimento armazenado. A direção do parâmetro é especificada ao criar um parâmetro de matriz (etapa 3) que é passado para [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Para especificar a direção do parâmetro  
  
1.  Defina uma consulta Transact-SQL que chame um procedimento armazenado. Use pontos de interrogação (?) em vez dos parâmetros a serem passados ao procedimento armazenado. Por exemplo, essa cadeia de caracteres chama um procedimento armazenado (UpdateVacationHours) que aceita dois parâmetros:  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Chamar os procedimentos armazenados usando a sintaxe canônica é a prática recomendada. Para obter mais informações sobre a sintaxe canônica, veja [Como chamar um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
2.  Inicialize ou atualize as variáveis do PHP correspondentes aos espaços reservados na consulta Transact-SQL. Por exemplo, o código a seguir inicializa os dois parâmetros para o procedimento armazenado UpdateVacationHours:  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Variáveis que são inicializadas ou atualizadas para **null**, **DateTime**ou tipos de fluxo não podem ser usadas como parâmetros de saída.  
  
3.  Use suas variáveis PHP da etapa 2 para criar ou atualizar uma matriz de valores de parâmetros que correspondam, em sequência, aos espaços reservados do parâmetro na cadeia de caracteres Transact-SQL. Especifique a direção de cada parâmetro na matriz. A direção de cada parâmetro é determinada por uma destas duas formas: por padrão (para parâmetros de entrada) ou usando constantes **SQLSRV_PARAM_\*** (para parâmetros de saída e bidirecionais). Por exemplo, o código a seguir especifica o parâmetro *$employeeId* como um parâmetro de entrada e o parâmetro *$usedVacationHours* como um parâmetro bidirecional:  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    Para entender a sintaxe para especificar a direção do parâmetro em geral, suponha que *$var1*, *$var2*e *$var3* correspondam aos parâmetros de entrada, saída e bidirecional, respectivamente. Você pode especificar a direção do parâmetro das seguintes maneiras:  
  
    -   Especificar implicitamente o parâmetro de entrada, especificar explicitamente o parâmetro de saída e especificar explicitamente um parâmetro bidirecional:  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   Especificar explicitamente o parâmetro de entrada, especificar explicitamente o parâmetro de saída e especificar explicitamente um parâmetro bidirecional:  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  Execute a consulta com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou com [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) e [sqlsrv_execute](../../connect/php/sqlsrv-execute.md). Por exemplo, o código a seguir usa a conexão *$conn* para executar a consulta *$tsql* com valores de parâmetros especificados em *$params*:  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Como recuperar parâmetros de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[Como recuperar parâmetros de entrada e de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  

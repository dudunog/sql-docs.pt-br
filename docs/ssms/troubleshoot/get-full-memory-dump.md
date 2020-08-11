---
title: Obter despejo de memória completo para solucionar problemas do SSMS
Description: Solucionar problemas do SSMS com falha ou sem resposta coletando um despejo de memória completo
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.reviewer: dineth, sstein
ms.custom: seo-lt-2019
ms.date: 05/17/2019
ms.openlocfilehash: 7b55e8e68076ad14f874306ffdb578f619af1cf0
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091222"
---
# <a name="get-full-memory-dump"></a>Obtenha Despejo de Memória Completo

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Neste artigo, você aprenderá a capturar informações de diagnóstico para solucionar problemas em um sistema com falha ou sem resposta ao usar o SSMS (SQL Server Management Studio).

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra um prompt de comando (como `cmd.exe`) e execute o seguinte comando.

    ```
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    Ele solicitará que você aceite um contrato de licença, selecione **Concordo**.

4. Inicie o SSMS, se ainda não tiver iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta.

## <a name="outofmemoryexception"></a>OutOfMemoryException

Você também pode obter o despejo de memória completo do SSMS quando ele gera uma OutOfMemoryException (pode ser qualquer exceção gerenciada).

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas de uma OutOfMemoryException do SSMS.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Ele solicitará que você aceite um contrato de licença, selecione **Concordo**.

4. Inicie o SQL Server Management Studio, se ainda não tiver iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta.

## <a name="share-the-information"></a>Compartilhar as informações

1. Para compartilhar informações com a equipe do SSMS, registre em log o problema em https://aka.ms/sqlfeedback.

2. Em seguida, compartilhe o arquivo de despejo de memória coletado para o OneDrive (ou equivalente) no qual o arquivo pode ser coletado.

    > [!Important]
    > Os arquivos de despejo de memória podem conter informações confidenciais.

## <a name="next-steps"></a>Próximas etapas

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)
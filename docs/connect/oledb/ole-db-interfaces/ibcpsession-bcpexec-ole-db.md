---
title: IBCPSession::BCPExec (driver do OLE DB) | Microsoft Docs
description: O método IBCPSession::BCPExec copia dados de um arquivo de usuário para uma tabela de banco de dados ou vice-versa no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPExec method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c3970eba0c3e9839d2eaa1ba42ad384fdbd5909
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081815"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Executa a operação de cópia em massa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>Comentários  
 O método **BCPExec** copia os dados de um arquivo de usuário para uma tabela de banco de dados ou vice-versa, dependendo do valor do parâmetro *eDirection* usado com o método [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
 Antes de chamar **BCPExec**, chame o método **BCPInit** com um nome de arquivo de usuário válido. Caso isso não seja feito, será gerado um erro. A única exceção será se uma consulta for usada para uma operação de cópia em massa. Nesse caso, especifique NULL para o nome da tabela no método **BCPInit** e, depois, especifique a consulta usando a opção BCP_OPTION_HINTS.  
  
 O método **BCPExec** é o único método de cópia em massa que provavelmente permanecerá pendente durante qualquer intervalo de tempo. Ele é, portanto, o único método de cópia em massa que oferece suporte ao modo assíncrono. Para usar o modo assíncrono, defina a propriedade de sessão SSPROP_ASYNCH_BULKCOPY específica do provedor como VARIANT_TRUE antes de chamar o método **BCPExec** . Essa propriedade está disponível no conjunto de propriedades DBPROPSET_SQLSERVERSESSION. Para testar a conclusão, chame o método **BCPExec** com os mesmos parâmetros. Se a cópia em massa ainda não estiver concluída, o método **BCPExec** retornará DB_S_ASYNCHRONOUS. Ele também retornará, no argumento *pRowsCopied* , uma contagem de status do número de linhas que foram enviadas para o servidor ou recebidas dele. As linhas enviadas para o servidor não serão confirmadas até que o fim de um lote seja atingido.  
  
## <a name="arguments"></a>Argumentos  
 *pRowsCopied*[out]  
 Um ponteiro para uma DWORD. O método **BCPExec** preenche a método com o número de linhas copiadas com êxito. Se o argumento *pRowsCopied* for definido como NULL, ele será ignorado pelo método **BCPExec** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Um erro específico do provedor ocorreu. Para obter informações detalhadas, use a interface [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md).  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método **BCPInit** não foi chamado antes da chamada desse método. Também ocorrerá se a operação for anulada com a opção BCP_OPTION_ABORT e o método **BCPExec** for chamado depois.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 DB_S_ENDOFROWSET  
 A operação de cópia em massa terminou e toda a transferência de dados foi concluída.  
  
 DB_S_ASYNCHRONOUS  
 O lote atual de linhas foi copiado. Chame o método **BCPExec** novamente para transferir o próximo lote.  
  
 DB_S_ERRORSOCCURRED  
 Ocorreram erros durante a operação de cópia em massa e algumas linhas podem não ter sido copiadas. O número de erros ainda é menor do que o máximo de erros permitido.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
  

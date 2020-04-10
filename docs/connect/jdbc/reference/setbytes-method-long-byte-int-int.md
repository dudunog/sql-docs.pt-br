---
title: Método setBytes (long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eaa3f23fdf9b38553b3492ca96895645dc8de371
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929144"
---
# <a name="setbytes-method-long-byte-int-int"></a>Método setBytes (long, byte[], int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava toda ou parte da matriz de bytes fornecida no BLOB iniciando na posição, no deslocamento e no comprimento determinados e, em seguida, retorna o número de bytes gravados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 A posição (baseada em 1) no BLOB em que a gravação de dados é iniciada.  
  
 *bytes*  
  
 A matriz de bytes a ser gravada no BLOB.  
  
 *offset*  
  
 O deslocamento na matriz de bytes onde iniciar a leitura de dados da matriz de **byte**.  
  
 *len*  
  
 O número de bytes que tentará ser lido da matriz de bytes no BLOB.  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que contém o número de bytes gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setBytes é especificado pelo método setBytes na interface java.sql.Blob.  
  
 Os dados são substituídos iniciando na posição especificada e podem ultrapassar o comprimento inicial do BLOB. A especificação de valores posição+1 acrescentará bytes. A transmissão de um valor posição+2 ou maior (ou zero ou menos) lançará um erro de posição. A transmissão de uma matriz de **byte** de comprimento zero retornará zero, pois nenhum byte foi gravado.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

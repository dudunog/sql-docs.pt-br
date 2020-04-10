---
title: Método setPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52f5093d4f9ba61bda2b3fb44cf6a64e76b6fe4e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920784"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Método setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o tamanho do pacote de rede atual usado para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especificado em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *packetSize*  
  
 Um valor **int** que contém o tamanho do pacote de rede.  
  
## <a name="remarks"></a>Comentários  
 O intervalo de valores aceitáveis dessa propriedade é [-1 | 0 | 512..32767]. Se essa propriedade for definida como um valor fora do intervalo aceitável, ocorrerá uma exceção.  
  
 O aplicativo poderá definir a propriedade packetSize enquanto estiver conectado com criptografia SSL (Protocolo SSL). O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] negocia o tamanho do pacote com o servidor. Se a propriedade de criptografia for definida como "**true**" e o tamanho de pacote negociado for maior que o tamanho do registro SSL do provedor de segurança padrão da JVM (Máquina Virtual Java), o driver retornará um erro e finalizará a conexão.  
  
 Além disso, o aplicativo poderá definir a propriedade packetSize sem solicitar a criptografia SSL. Nesse caso, se o servidor exigir que o cliente dê suporte à criptografia SSL, o driver verificará o tamanho do registro SSL do provedor de segurança padrão da Máquina Virtual Java. Se a propriedade packetSize for maior que o tamanho do registro SSL do provedor de segurança padrão da Máquina Virtual Java, o driver retornará um erro e finalizará a conexão.  
  
 Para obter mais informações sobre como usar SSL, confira [Como usar a criptografia SSL](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

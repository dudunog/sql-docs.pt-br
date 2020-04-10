---
title: Como trabalhar usando dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a94761b9c85e4d3aa1d88a21efdce51a0f46e6f7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922543"
---
# <a name="working-with-large-data"></a>Trabalhando com dados grandes

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

O driver JDBC oferece suporte para buffer adaptável, que permite recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor. Com o buffer adaptável, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] recupera os resultados da execução da instrução por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à medida que o aplicativo precisa deles, em vez de todos de uma vez. O driver também descarta os resultados assim que o aplicativo já não os pode acessar.  
  
No [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] JDBC Driver versão 1.2, o modo de buffer era "**cheio**" por padrão. Se o aplicativo não definiu a propriedade de conexão "responseBuffering" como "**adaptável**" nas propriedades de conexão ou usando o método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), isso significa que o driver deu suporte à leitura do resultado inteiro imediatamente do servidor. Para obter o comportamento de buffer adaptável, o aplicativo teve que definir a propriedade de conexão "responseBuffering" explicitamente como "**adaptável**".  
  
O valor **adaptável** é o modo de buffer padrão, e o driver JDBC armazena em buffer o mínimo de dados possível quando necessário. Para obter mais informações sobre como usar o buffer adaptável, confira [Como usar o buffer adaptável](../../../connect/jdbc/using-adaptive-buffering.md).  
  
Os tópicos nesta seção descrevem maneiras diferentes de recuperar dados de valor grande de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                                                                         | DESCRIÇÃO                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [Lendo exemplo de dados grandes](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | Descreve como usar uma instrução SQL para recuperar dados de valor grande.       |
| [Lendo exemplo de dados grandes com procedimentos armazenados](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | Descreve como recuperar um valor grande do parâmetro OUT do CallableStatement. |
| [Atualizando o exemplo de dados grandes](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | Descreve como atualizar dados de valor grande em um banco de dados.                |
  
## <a name="see-also"></a>Confira também

[Aplicativos de exemplo do JDBC Driver](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  

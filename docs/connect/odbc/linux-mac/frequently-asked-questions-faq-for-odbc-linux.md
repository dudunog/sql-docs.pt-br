---
title: Perguntas frequentes para Linux e macOS ODBC
description: Encontre respostas para perguntas comuns sobre o Microsoft ODBC Driver for SQL Server em Linux e em macOS.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 700c89b520cdaa33a60f1adabe69c669388bcccb
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886449"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Perguntas frequentes para Linux e macOS ODBC
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Veja a seguir respostas para perguntas sobre o driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS.
  
## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Como os aplicativos ODBC existentes no Linux ou no macOS funcionam com o driver?**  
Você deve ser capaz de compilar e executar os aplicativos ODBC que você vem compilando e executando no Linux ou no macOS usando outros drivers. 
  
**Com quais recursos do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] essa versão do driver é compatível?**

O driver ODBC no Linux e no macOS dá suporte a todos os recursos de servidor no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], exceto LocalDB. Para obter mais informações sobre os recursos com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**O driver é compatível com a autenticação Kerberos?**  
Sim. Se você tiver uma configuração de ambiente Kerberos existente, deverá ser capaz de se conectar a servidores usando a opção de cadeia de conexão ou DSN `Trusted_Connection=Yes`. Para obter mais informações, consulte [Como usar autenticação integrada](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Qual codificação Unicode um aplicativo deve usar?**  
UTF-8 para dados SQL_CHAR e UTF-16 para dados SQL_WCHAR. Dependendo da localidade do sistema e da versão do driver, os dados não UTF-8 em uma das diversas codificações também poderão ser compatíveis. Para obter mais informações, confira [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).

**Há exemplos de ODBC que eu possa baixar e executar com o driver para experimentar ou avaliar?**

Consulte [Use exemplos ODBC do MSDN C ++ para o driver ODBC no Linux](/archive/blogs/sqlblog/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver) para obter um exemplo. Isso também e aplicável ao driver ODBC do macOS.

**O driver ODBC no Linux ou no macOS é software livre?**

Não, os drivers ODBC no Linux e no macOS não são um produto de software livre.  

## <a name="see-also"></a>Consulte Também

- [Como instalar o Microsoft ODBC Driver for SQL Server em Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Como instalar o Microsoft ODBC Driver for SQL Server no macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)

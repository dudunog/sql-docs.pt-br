---
title: Wrappers e interfaces | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc8a8277147dd2dc136379471f6a4f7df789c3ee
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923933"
---
# <a name="wrappers-and-interfaces"></a>Wrappers e interfaces

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível com interfaces que permitem criar um proxy de uma classe, além de wrappers que permitem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.

## <a name="wrappers"></a>Wrappers

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte à interface java.sql.Wrapper. Essa interface fornece um mecanismo para acessar extensões para a API do JDBC que são específicas do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.

A interface java.sql.Wrapper define dois métodos: **isWrapperFor** e **unwrap**. O método **isWrapperFor** verifica se o objeto de entrada especificado implementa essa interface. O método **unwrap** retorna um objeto que implementa essa interface para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

os métodos **isWrapperFor** e **Unwrap** são expostos da seguinte maneira:

- [Método isWrapperFor &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [Método unwrap &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [Método isWrapperFor &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [Método unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [Método unwrap &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [Método isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [Método unwrap &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [Método isWrapperFor &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [Método unwrap &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [Método isWrapperFor &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [Método unwrap &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>Interfaces

Começando com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0, as interfaces são disponibilizadas para um servidor de aplicativos para acessar um método específico de driver usando a classe associada. O servidor de aplicativos pode encapsular a classe criando um proxy, expondo a funcionalidade específica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] de uma interface. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível com interfaces que têm os métodos específicos e constantes do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para que um servidor de aplicativos possa criar um proxy da classe.

Como as interfaces derivam das interfaces Java padrão, você pode usar o mesmo objeto após o desencapsulamento para acessar a funcionalidade específica do driver ou a funcionalidade genérica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

As seguintes interfaces são adicionadas:

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>Exemplo

### <a name="description"></a>DESCRIÇÃO

Esse exemplo demonstra como acessar uma função específica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usando um objeto DataSource. Essa classe DataSource pode ter sido encapsulada por um servidor de aplicativos. Para acessar a função específica ou a constante do JDBC Driver, é possível desencapsular a fonte de dados em uma interface ISQLServerDataSource e usar as funções declaradas na interface.

### <a name="code"></a>Código

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)

---
title: Método getCrossReference (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f23da4d83217fbed39e6dddacfe92541eae0db23
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67984222"
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>Método getCrossReference (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das colunas de chave estrangeira da tabela de chaves estrangeiras fornecida que referencia as colunas de chave primária da tabela de chaves primárias fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *cat1*  
  
 Uma **String** que contém o nome de catálogo da tabela que contém a chave primária.  
  
 *schem1*  
  
 Uma **String** que contém o nome de esquema da tabela que contém a chave primária.  
  
 *tab1*  
  
 Uma **String** que contém o nome de tabela da tabela que contém a chave primária.  
  
 *cat2*  
  
 Uma **String** que contém o nome de catálogo da tabela que contém a chave estrangeira.  
  
 *schem2*  
  
 Uma **String** que contém o nome de esquema da tabela que contém a chave estrangeira.  
  
 *tab2*  
  
 Uma **String** que contém o nome de tabela da tabela que contém a chave estrangeira.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCrossReference é especificado pelo método getCrossReference na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getCrossReference conterá as seguintes informações:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**Cadeia de caracteres**|O nome do catálogo que contém a tabela de chaves primárias.|  
|PKTABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema da tabela de chaves primárias.|  
|PKTABLE_NAME|**Cadeia de caracteres**|O nome da tabela de chaves primárias.|  
|PKCOLUMN_NAME|**Cadeia de caracteres**|O nome da coluna da chave primária.|  
|FKTABLE_CAT|**Cadeia de caracteres**|O nome do catálogo que contém a tabela de chaves estrangeiras.|  
|FKTABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema da tabela de chaves estrangeiras.|  
|FKTABLE_NAME|**Cadeia de caracteres**|O nome da tabela de chaves estrangeiras.|  
|FKCOLUMN_NAME|**Cadeia de caracteres**|O nome da coluna da chave estrangeira.|  
|KEY_SEQ|**short**|O número de sequência da coluna em uma chave primária de várias colunas.|  
|UPDATE_RULE|**short**|A ação aplicada à chave estrangeira quando a operação SQL for uma atualização. Pode ser um dos seguintes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|A ação aplicada à chave estrangeira quando a operação SQL for uma exclusão. Pode ser um dos seguintes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**Cadeia de caracteres**|O nome da chave estrangeira.|  
|PK_NAME|**Cadeia de caracteres**|O nome da chave primária.|  
|DEFERRABILITY|**short**|Indica se a avaliação da restrição de chave estrangeira poderá ser adiada até uma confirmação. Pode ser um dos seguintes valores:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getCrossReference, consulte "sp_fkeys (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getCrossReference para retornar informações sobre a relação de chave primária e estrangeira entre as tabelas Person.Contact e HumanResources.Employee no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

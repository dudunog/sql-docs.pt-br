---
title: Suporte para UDTs grandes | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 621b6d13-10f1-47d0-b63c-7adb6ab904e0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5aa293ec241534c026d433b3a48f96c86f371615
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000319"
---
# <a name="support-for-large-udts"></a>Suporte a UDTs grandes
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Esta solução de exemplo contém dois projetos. Um projeto cria um assembly (DLL) de código-fonte C#. Este assembly contém o tipo CLR. Uma tabela será adicionada ao banco de dados. Uma coluna na tabela será de um tipo definido no assembly, por padrão, este exemplo usará o banco de dados mestre. O segundo projeto é um aplicativo nativo C que lê dados da tabela.  
  
 Este exemplo não funcionará com nenhuma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Para obter mais informações sobre o suporte a UDTs grandes, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="example"></a>Exemplo  
 A primeira listagem de código é o código de origem C#. Cole-a em um arquivo chamado LargeStringUDT.cs e compile-a para uma DLL. Copie LargeStringUDT.dll no diretório raiz da unidade C.  
  
 A segunda [!INCLUDE[tsql](../../includes/tsql-md.md)] listagem de código () cria o assembly no banco de dados mestre.  
  
 Compile a segunda listagem de código (C++) com odbc32.lib e user32.lib. Verifique se a variável de ambiente INCLUDE inclui o diretório que contém sqlncli.h.  
  
 Se você compilar e executar esse exemplo como um aplicativo de 32 bits em um sistema operacional de 64 bits, deverá criar a fonte de dados ODBC com o Administrador ODBC em %windir%\SysWOW64\odbcad32.exe.  
  
 Esse aplicativo se conecta à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do computador. Para conectar-se a uma instância nomeada, altere a definição da fonte de dados ODBC para especificar a instância usando o seguinte formato: servidor\instância_nomeada. Por padrão, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado em uma instância nomeada.  
  
 A quarta [!INCLUDE[tsql](../../includes/tsql-md.md)] listagem de código () exclui o assembly do banco de dados mestre.  
  
```  
// LargeStringUDT.cs  
// compile with: /target:library  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Text;  
  
[assembly: System.CLSCompliantAttribute(true)]  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.UserDefined, IsFixedLength = false, MaxByteSize = -1, IsByteOrdered = true)]  
public class LargeStringUDT : INullable, IBinarySerialize {  
    private bool _isNull;  
    private string _largeString;  
  
    public bool IsNull {  
        get {  
            return (_isNull);  
        }  
    }  
  
    public static LargeStringUDT Null {  
        get {  
            LargeStringUDT lsUDT = new LargeStringUDT();  
            lsUDT._isNull = true;  
            return lsUDT;  
        }  
    }  
  
    public override string ToString() {  
        if (IsNull)  
            return "NULL";  
        else  
            return _largeString;  
    }  
  
    [SqlMethod(OnNullCall = false)]  
    public static LargeStringUDT Parse(SqlString s) {  
        if (s.IsNull)  
            return Null;  
  
        LargeStringUDT lsUDT = new LargeStringUDT();  
        lsUDT._largeString = s.Value;  
        return lsUDT;  
    }  
  
    public String LargeString {  
        get {  
            return _largeString;  
        }  
  
        set {  
            _largeString = value;  
        }  
    }  
  
    public void Read(System.IO.BinaryReader r) {  
        _isNull = r.ReadBoolean();  
        if (!_isNull)  
            _largeString = new String(r.ReadChars(r.ReadInt32()));  
    }  
  
    public void Write(System.IO.BinaryWriter w) {  
        w.Write(_isNull);  
        if (!_isNull) {  
            w.Write(_largeString.Length);  
            for (int i = 0; i < _largeString.Length; ++i)  
                w.Write(_largeString[i]);  
        }  
    }  
}  
```  
  
```  
USE [MASTER]  
IF EXISTS (SELECT * FROM sys.objects WHERE name = 'LargeStringUDTs')  
   DROP TABLE LargeStringUDTs  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE name = 'LargeStringUDT')  
   DROP TYPE dbo.LargeStringUDT  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = 'LargeStringUDT')  
   DROP ASSEMBLY LargeStringUDT  
GO  
  
CREATE ASSEMBLY LargeStringUDT  
FROM 'C:\LargeStringUDT.dll'  
WITh PERMISSION_SET=SAFE;  
GO  
  
CREATE TYPE dbo.LargeStringUDT   
EXTERNAL NAME LargeStringUDT.[LargeStringUDT];  
GO  
  
CREATE TABLE dbo.LargeStringUDTs  
(ID int IDENTITY(1,1) PRIMARY KEY, LargeString LargeStringUDT)  
GO  
  
INSERT INTO dbo.LargeStringUDTs (LargeString) VALUES (CONVERT(LargeStringUDT, 'This is the first string'));  
INSERT INTO dbo.LargeStringUDTs (LargeString) VALUES (CONVERT(LargeStringUDT, 'This is the second string'));  
INSERT INTO dbo.LargeStringUDTs (LargeString) VALUES (Convert(LargeStringUDT, 'This is the third string'));  
GO  
```  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#define ODBCVER 0x0350  
#include <sql.h>  
#include <sqlext.h>  
#include <sqltypes.h>  
#define _SQLNCLI_ODBC  
#include "sqlncli.h"  
  
int main() {  
   // The command to execute.  
   SQLTCHAR* szCmdString = (SQLTCHAR *)_T("SELECT ID, LargeString FROM dbo.LargeStringUDTs");  
  
   int ret = 0;  
   SQLRETURN rc;  
   SQLHENV hEnv = NULL;  
   SQLHDBC hDbc = NULL;  
   SQLHSTMT hStmt = NULL;  
   SQLTCHAR szConn[256];   
   BYTE DataBuf[15];  
   SQLSMALLINT iLen = 0;  
   SQLLEN iDataLen = 0;  
  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &hEnv);  
   if (rc != SQL_SUCCESS) {  
      printf("Failed to get HENV\n");  
      return -1;  
   }  
  
   rc = SQLSetEnvAttr (hEnv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);  
   if (rc != SQL_SUCCESS) {  
      printf("Failed to SetEnvAttr\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
      return -1;  
   }  
  
   rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &hDbc);  
   if (rc != SQL_SUCCESS) {  
      printf("Failed to get HDBC\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
      return -1;  
   }  
  
   rc = SQLDriverConnect(hDbc, NULL,   
      (SQLTCHAR *)_T("DRIVER={SQL Server Native Client 10.0};SERVER=(local);Trusted_Connection=Yes;database=master"),   
      SQL_NTS, szConn, 255, &iLen, SQL_DRIVER_NOPROMPT);  
   if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO) {  
      printf("Failed to connect\n");  
      ret = -1;  
      goto End;  
   }  
  
   rc = SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
   if (rc != SQL_SUCCESS) {  
      printf("Failed to get hstmt\n");  
      ret = -1;  
      goto End;  
   }  
  
   // Execute the command.  
   rc = SQLExecDirect(hStmt, szCmdString, SQL_NTS);  
   if (rc != SQL_SUCCESS) {  
      printf("Failed to get hstmt\n");  
      ret = -1;  
      goto End;  
   }  
  
   // Process the result set.  
   SQLSMALLINT paramType;  
   SQLTCHAR szData[100], szData2[100];  
   SQLSMALLINT NameLengthPtr = 0, DataTypePtr, DecimalDigitsPtr, NullablePtr;  
   SQLULEN ColumnSizePtr[2];  
   rc = SQLDescribeCol(hStmt, 1, szData, sizeof(szData), &NameLengthPtr, &DataTypePtr, &ColumnSizePtr[0], &DecimalDigitsPtr, &NullablePtr);  
   _tprintf(_T("%s"), szData);  
   rc = SQLDescribeCol(hStmt, 2, szData2, sizeof(szData2), &NameLengthPtr, &DataTypePtr, &ColumnSizePtr[1], &DecimalDigitsPtr, &NullablePtr);  
   _tprintf(_T("          %s\n"), szData2);  
  
   while ( ( rc = SQLFetch(hStmt ) ) == SQL_SUCCESS ) {  
      rc = SQLGetData(hStmt, 1, SQL_C_SHORT, &paramType, sizeof(SQL_C_SHORT), NULL);  
      printf("%d           ", paramType);  
  
      bool ifFirst = true;  
      while ( ( rc = SQLGetData(hStmt, 2 , SQL_C_BINARY, DataBuf, sizeof(DataBuf) ,&iDataLen ) ) != SQL_NO_DATA) {  
         // process number of bytes in the DataBuf;  
         int NumBytes = (iDataLen > sizeof(DataBuf)) || (iDataLen == SQL_NO_TOTAL) ? sizeof(DataBuf): iDataLen;  
         for ( int i = ifFirst?5:0 ; i <NumBytes ; i++ )  
            putchar((char)DataBuf[i]);  
         ifFirst = false;  
      };  
      printf("\n");  
   }  
  
   if ( rc != SQL_NO_DATA ) {  
      printf("Failed to fetch data\n");  
      ret= -1;  
   }  
  
End:  
   if (hStmt) {  
      SQLFreeStmt(hStmt,SQL_CLOSE);  
      SQLFreeStmt(hStmt,SQL_DROP);  
   }  
  
   if (hDbc) {  
      SQLDisconnect(hDbc);  
      SQLFreeConnect(hDbc);  
   }  
  
   if (hEnv)  
      SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
};  
```  
  
```  
USE [MASTER]  
IF EXISTS (SELECT * FROM sys.objects WHERE name = 'LargeStringUDTs')  
   DROP TABLE LargeStringUDTs  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE name = 'LargeStringUDT')  
   DROP TYPE dbo.LargeStringUDT  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = 'LargeStringUDT')  
   DROP ASSEMBLY LargeStringUDT  
GO  
```  
  
  

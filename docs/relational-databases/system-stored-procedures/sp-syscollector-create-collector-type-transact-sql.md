---
title: sp_syscollector_create_collector_type (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collector_type
- sp_syscollector_create_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 568e9119-b9b0-4284-9cef-3878c691de5f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ba0086ac19daa4118bb411a4d2cb091ec9f1ce86
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892953"
---
# <a name="sp_syscollector_create_collector_type-transact-sql"></a>sp_syscollector_create_collector_type (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria um tipo de coletor para o coletor de dados. Um tipo de coletor é um wrapper lógico em volta dos [!INCLUDE[ssIS](../../includes/ssis-md.md)] pacotes que fornecem o mecanismo real para coletar dados e carregá-los no data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_create_collector_type   
    [ [@collector_type_uid = ] 'collector_type_uid' OUTPUT ]  
    , [ @name = ] 'name'  
    , [ [ @parameter_schema = ] 'parameter_schema' ]  
    , [ [ @parameter_formatter = ] 'parameter_formatter' ]  
    , [ @collection_package_id = ] 'collection_package_id'  
    , [ @upload_package_id = ] 'upload_package_id'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collector_type_uid =] '*collector_type_uid*'  
 É o GUID do tipo de coletor. *collector_type_uid* é **uniqueidentifier** e, se for NULL, ele será criado automaticamente e retornado como saída.  
  
 [ @name =] '*nome*'  
 É o nome do tipo de coletor. o *nome* é **sysname** e deve ser especificado.  
  
 [ @parameter_schema =] '*parameter_schema*'  
 É o esquema XML deste tipo de coletor. *parameter_schema* é **XML** com um padrão de NULL.  
  
 [ @parameter_formatter =] '*parameter_formatter*'  
 É o modelo a ser usado para transformar o XML para uso na página de propriedades do conjunto de coleta. *parameter_formatter* é **XML** com um padrão de NULL.  
  
 [ @collection_package_id =] *collection_package_id*  
 É um identificador exclusivo local que aponta para o pacote de coleta do [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado pelo conjunto de coleta. *collection_package_id* é **uniqueidentifier** e é necessário.  
  
 [ @upload_package_id =] *upload_package_id*  
 É um identificador exclusivo local que aponta para o pacote de carregamento do [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado pelo conjunto de coleta. *upload_package_id* é **uniqueidentifier** e é obrigatório.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_admin (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="example"></a>Exemplo  
 Isto cria o tipo de coletor de Consultas T-SQL Genérico.  
  
```  
EXEC sp_syscollector_create_collector_type  
@collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
    <xs:element name="TSQLQueryCollector">  
      <xs:complexType>  
        <xs:sequence>  
          <xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
            <xs:complexType>  
              <xs:sequence>  
                <xs:element name="Value" type="xs:string" />  
                <xs:element name="OutputTable" type="xs:string" />  
              </xs:sequence>  
            </xs:complexType>  
          </xs:element>  
          <xs:element name="Databases" minOccurs="0" maxOccurs="1">  
            <xs:complexType>  
              <xs:sequence>  
                <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
              </xs:sequence>  
              <xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
              <xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
            </xs:complexType>  
          </xs:element>  
        </xs:sequence>  
      </xs:complexType>  
    </xs:element>  
  </xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  

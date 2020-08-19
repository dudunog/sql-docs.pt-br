---
description: catalog.set_environment_reference_type (banco de dados SSISDB)
title: catalog.set_environment_reference_type (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6af8fdff22031cd5f806cb3d6f640223414f3ac1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425068"
---
# <a name="catalogset_environment_reference_type-ssisdb-database"></a>catalog.set_environment_reference_type (banco de dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define o tipo de referência e o nome de ambiente associados a uma referência de ambiente existente para um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @reference_id = ] *reference_id*  
 O identificador exclusivo da referência de ambiente que deve ser atualizada. O *reference_id* é **bigint**.  
  
 [ @reference_type = ] *reference_type*  
 Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Use o valor `R` para indicar uma referência relativa. Use o valor `A` para indicar uma referência absoluta. O *reference_type* é **char(1)** .  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 A pasta na qual o ambiente está localizado. Esse valor é necessário para referências absolutas. O *environment_folder_name* é **nvarchar(128)** .  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto e permissão READ no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome de pasta, o nome de ambiente ou o ID de referência não é válido  
  
-   O usuário não tem as permissões adequadas  
  
-   Uma referência absoluta está especificada usando o caractere `A` no parâmetro *reference_location*, mas o nome da pasta não foi especificado com o parâmetro *environment_folder_name*.  
  
## <a name="remarks"></a>Comentários  
 Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome e requerem que ele resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Elas podem fazer referência a ambientes que residam em uma pasta diferente da pasta do projeto. Um projeto pode fazer referência a vários ambientes.  
  
> [!IMPORTANT]  
>  Se uma referência relativa for especificada, o valor do parâmetro *environment_folder_name* não será usado e o nome da pasta do ambiente será definido automaticamente como **NULL**. Se uma referência absoluta for especificada, o nome da pasta de ambiente deverá ser fornecido no parâmetro *environment_folder_name*.  
  
  

---
title: PDO::beginTransaction | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec1b4149b882e520eb58a8789516461c83c01de
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919401"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Desativa o modo de confirmação automática e inicia uma transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>Valor retornado  
true se a chamada do método for bem-sucedida; caso contrário, false.  
  
## <a name="remarks"></a>Comentários  
A transação começava com PDO::beginTransaction terminará quando [PDO::commit](../../connect/php/pdo-commit.md) ou [PDO::rollback](../../connect/php/pdo-rollback.md) era chamado.  
  
PDO::beginTransaction não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT (e não o afeta).  
  
Você não tem permissão para chamar PDO::beginTransaction antes de o PDO::beginTransaction anterior ser finalizado com PDO::rollback ou PDO::commit.  
  
A conexão retornará para o modo de confirmação automática se esse método falhar.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa um banco de dados chamado Test e uma tabela chamada Table1. Ele inicia uma transação e, em seguida, emite comandos para adicionar duas linhas e depois excluir uma linha. Os comandos são enviados para o banco de dados e a transação é finalizada explicitamente com `PDO::commit`.  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  

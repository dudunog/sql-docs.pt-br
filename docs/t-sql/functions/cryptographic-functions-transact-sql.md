---
title: Funções criptográficas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cryptographic
- crypto functions
- cryptography [SQL Server], functions
- decryption [SQL Server], functions
- security functions
- encryption [SQL Server], functions
ms.assetid: 0be5626b-5a25-4d8c-9f44-7abbfccf816c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3bc543e40f4f5189a1d813d21b66af6b26b51d52
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68026438"
---
# <a name="cryptographic-functions-transact-sql"></a>Funções criptográficas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essas funções oferecem suporte à assinatura digital, validação de assinatura digital, criptografia e descriptografia.
  
## <a name="symmetric-encryption-and-decryption"></a>Criptografia e descriptografia simétricas
  
|||  
|-|-|  
|[ENCRYPTBYKEY](../../t-sql/functions/encryptbykey-transact-sql.md)|[DECRYPTBYKEY](../../t-sql/functions/decryptbykey-transact-sql.md)|  
|[ENCRYPTBYPASSPHRASE](../../t-sql/functions/encryptbypassphrase-transact-sql.md)|[DECRYPTBYPASSPHRASE](../../t-sql/functions/decryptbypassphrase-transact-sql.md)|  
|[KEY_ID](../../t-sql/functions/key-id-transact-sql.md)|[KEY_GUID](../../t-sql/functions/key-guid-transact-sql.md)|  
|[DECRYPTBYKEYAUTOASYMKEY](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)|[KEY_NAME](../../t-sql/functions/key-name-transact-sql.md)|  
|[SYMKEYPROPERTY](../../t-sql/functions/symkeyproperty-transact-sql.md)||  
  
## <a name="asymmetric-encryption-and-decryption"></a>Criptografia e descriptografia assimétricas
  
|||  
|-|-|  
|[ENCRYPTBYASYMKEY](../../t-sql/functions/encryptbyasymkey-transact-sql.md)|[DECRYPTBYASYMKEY](../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
|[ENCRYPTBYCERT](../../t-sql/functions/encryptbycert-transact-sql.md)|[DECRYPTBYCERT](../../t-sql/functions/decryptbycert-transact-sql.md)|  
|[ASYMKEYPROPERTY](../../t-sql/functions/asymkeyproperty-transact-sql.md)|[ASYMKEY_ID](../../t-sql/functions/asymkey-id-transact-sql.md)|  
  
## <a name="signing-and-signature-verification"></a>Assinatura e verificação de assinatura
  
|||  
|-|-|  
|[SIGNBYASYMKEY](../../t-sql/functions/signbyasymkey-transact-sql.md)|[VERIFYSIGNEDBYASMKEY](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)|  
|[SIGNBYCERT](../../t-sql/functions/signbycert-transact-sql.md)|[VERIGYSIGNEDBYCERT](../../t-sql/functions/verifysignedbycert-transact-sql.md)|  
|[IS_OBJECTSIGNED](../../t-sql/functions/is-objectsigned-transact-sql.md)||  
  
## <a name="symmetric-decryption-with-automatic-key-handling"></a>Descriptografia simétrica com manipulação automática de chave
  
|||  
|-|-|  
|[DecryptByKeyAutoCert](../../t-sql/functions/decryptbykeyautocert-transact-sql.md)||  
  
## <a name="encryption-hashing"></a>Hash de criptografia
  
|||  
|-|-|  
|[HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)||  
  
## <a name="certificate-copying"></a>Cópia de certificado
  
|||  
|-|-|  
|[CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)||  
|[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)||  
  
## <a name="see-also"></a>Confira também
[Funções](../../t-sql/functions/functions.md)  
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

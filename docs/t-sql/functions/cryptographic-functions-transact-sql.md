---
description: Funções criptográficas (Transact-SQL)
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
ms.openlocfilehash: f54a52f2fdb4e17d3e32ab47ca7e3dccfcb9aeb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468158"
---
# <a name="cryptographic-functions-transact-sql"></a>Funções criptográficas (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essas funções oferecem suporte à assinatura digital, validação de assinatura digital, criptografia e descriptografia.
  
## <a name="symmetric-encryption-and-decryption"></a>Criptografia e descriptografia simétricas

:::row:::
    :::column:::
        [ENCRYPTBYKEY](../../t-sql/functions/encryptbykey-transact-sql.md)
    :::column-end:::
    :::column:::
        [DECRYPTBYKEY](../../t-sql/functions/decryptbykey-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [ENCRYPTBYPASSPHRASE](../../t-sql/functions/encryptbypassphrase-transact-sql.md)
    :::column-end:::
    :::column:::
        [DECRYPTBYPASSPHRASE](../../t-sql/functions/decryptbypassphrase-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [KEY_ID](../../t-sql/functions/key-id-transact-sql.md)
    :::column-end:::
    :::column:::
        [KEY_GUID](../../t-sql/functions/key-guid-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [DECRYPTBYKEYAUTOASYMKEY](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)
    :::column-end:::
    :::column:::
        [KEY_NAME](../../t-sql/functions/key-name-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [SYMKEYPROPERTY](../../t-sql/functions/symkeyproperty-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="asymmetric-encryption-and-decryption"></a>Criptografia e descriptografia assimétricas
  
:::row:::
    :::column:::
        [ENCRYPTBYASYMKEY](../../t-sql/functions/encryptbyasymkey-transact-sql.md)
    :::column-end:::
    :::column:::
        [DECRYPTBYASYMKEY](../../t-sql/functions/decryptbyasymkey-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [ENCRYPTBYCERT](../../t-sql/functions/encryptbycert-transact-sql.md)
    :::column-end:::
    :::column:::
        [DECRYPTBYCERT](../../t-sql/functions/decryptbycert-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [ASYMKEYPROPERTY](../../t-sql/functions/asymkeyproperty-transact-sql.md)
    :::column-end:::
    :::column:::
        [ASYMKEY_ID](../../t-sql/functions/asymkey-id-transact-sql.md)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="signing-and-signature-verification"></a>Assinatura e verificação de assinatura

:::row:::
    :::column:::
        [SIGNBYASYMKEY](../../t-sql/functions/signbyasymkey-transact-sql.md)
    :::column-end:::
    :::column:::
        [VERIFYSIGNEDBYASMKEY](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [SIGNBYCERT](../../t-sql/functions/signbycert-transact-sql.md)
    :::column-end:::
    :::column:::
        [VERIGYSIGNEDBYCERT](../../t-sql/functions/verifysignedbycert-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [IS_OBJECTSIGNED](../../t-sql/functions/is-objectsigned-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

&nbsp;
  
## <a name="symmetric-decryption-with-automatic-key-handling"></a>Descriptografia simétrica com manipulação automática de chave

:::row:::
    :::column:::
        [DecryptByKeyAutoCert](../../t-sql/functions/decryptbykeyautocert-transact-sql.md)
    :::column-end:::
:::row-end:::
 
&nbsp;

## <a name="encryption-hashing"></a>Hash de criptografia

:::row:::
    :::column:::
        [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="certificate-copying"></a>Cópia de certificado 

:::row:::
    :::column:::
        [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)
    :::column-end:::
    :::column:::
        [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="see-also"></a>Confira também
[Funções](../../t-sql/functions/functions.md)  
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

---
description: MSSQLSERVER_6602
title: MSSQLSERVER_6602
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 6602 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: dc40432af6994b184678414efba4dcd098dc400b
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797742"
---
# <a name="mssqlserver_6602"></a>MSSQLSERVER_6602
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|6602|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|XMLERR_PARSEERR2|
|Texto da mensagem|A descrição do erro é '%.*ls'.|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando você tenta executar um procedimento armazenado `sp_xml_preparedocument` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em que o conteúdo do parâmetro `xmltext` é um documento XML complexo. Uma mensagem de erro semelhante à mostrada a seguir é relatada ao usuário

> O erro de análise de XML 0x80004005 ocorreu no número de linha 1, próximo ao texto XML "\<XML document sample>"  
Mensagem 6602, Nível 16, Estado 2, Procedimento sp_xml_preparedocument, Linha 1  
A descrição do erro é 'Erro não especificado'.

## <a name="cause"></a>Causa

Esse problema ocorre devido a uma limitação de design do analisador MSXML (Msxmlsql.dll) usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

O problema não está estritamente relacionado ao tamanho do documento XML, mas à estrutura complexa. Uma combinação da profundidade da estrutura do elemento XML, do número e do tamanho dos atributos e do número de entidades dentro dos atributos pode causar esse problema. No entanto, o nível de complexidade necessário para alcançar esse limite é encontrado em documentos XML que têm vários megabytes.

## <a name="user-action"></a>Ação do usuário

Para resolver esse problema, tente reduzir a complexidade do documento XML.

> [!NOTE]
> Cuidado com atributos de cadeia de caracteres única muito grandes que contêm muitas entidades XML.

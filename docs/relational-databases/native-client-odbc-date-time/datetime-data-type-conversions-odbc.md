---
title: conversões de tipo de dados DateTime (ODBC) | Microsoft Docs
description: Saiba mais sobre conversões de tipo de dados no ODBC, que já estão definidas pelo ODBC ou são extensões consistentes do ODBC.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09a018250887ecf88e6a48c49222046699a14763
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967648"
---
# <a name="datetime-data-type-conversions-odbc"></a>Conversões do tipo de dados datetime (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  As conversões a seguir já estão definidas pelo ODBC ou são uma extensão consistente do ODBC. As conversões fornecidas por cada provedor são determinadas pela comunidade atendida pelo provedor e, com frequência, existem inconsistências entre os resultados. Os valores entre colchetes são opcionais.  
  
-   O formato de cadeias de caracteres datetime é 'aaaa-mm-dd[ hh:mm:ss[.9999999][ mais/menos hh:mm]]'  
  
-   O formato de cadeias de caracteres de hora é 'hh:mm:ss[.9999999]'  
  
-   O formato de cadeias de caracteres de data é 'aaaa-mm-dd'  
  
 As conversões de cadeias de caracteres permitem uma flexibilidade nos espaços em branco e na largura dos campos. Para obter mais informações, consulte a seção "formatos de dados: cadeias de caracteres e literais" do [suporte de tipo de dados para aprimoramentos de data e hora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  
  
 Seguem as regras de conversão gerais:  
  
-   Se não houver uma hora mas o receptor puder armazenar horas, a hora será definida como zero.  
  
-   Se não houver uma data presente, mas o receptor puder armazenar datas, a data atual será usada.  
  
-   Se não houver um fuso horário presente no tipo de dados que o cliente está utilizando, mas o servidor puder armazenar fusos horários, a data será armazenada no fuso horário do cliente. Observe que isso é diferente do comportamento do servidor.  
  
-   Se não houver um fuso horário presente no tipo do servidor, mas o tipo do cliente tiver um fuso horário, a hora será convertida para UTC antes de ser armazenada no servidor.  
  
-   Se houver uma hora presente, mas o receptor não puder armazenar horas, o componente de hora será ignorado.  
  
-   Se houver uma data presente, mas o receptor não puder armazenar datas, o componente de data será ignorado.  
  
-   Se ocorrer o truncamento de segundos ou frações de segundos ao converter do C para o SQL, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime".  
  
-   Se ocorrer o truncamento de segundos ou frações de segundos ao converter do SQL para o C, um registro de diagnóstico será gerado com SQLSTATE 01S07 e a mensagem "Truncamento de frações".  
  
## <a name="in-this-section"></a>Nesta seção  
 [Conversões do C para o SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)  
 Lista os problemas a serem considerados ao converter tipos do C em tipos de data/hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Conversões de SQL em C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)  
 Lista os problemas a serem considerados ao converter tipos de data/hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipos do C.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  

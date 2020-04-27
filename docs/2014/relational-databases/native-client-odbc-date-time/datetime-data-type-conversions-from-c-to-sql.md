---
title: Conversões de C para SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8179b9452852777bb6d2a06018d0bf86598a5bf8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63207018"
---
# <a name="conversions-from-c-to-sql"></a>Conversões do C para o SQL
  Este tópico lista os problemas a serem considerados quando você converte de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] C em tipos de data/hora.  
  
 As conversões descritas na tabela a seguir se aplicam a conversões feitas no cliente. Nos casos em que o cliente especifica uma precisão de frações de segundo para um parâmetro diferente daquela definida no servidor, a conversão do cliente pode ser bem-sucedida, mas o servidor irá retornar um erro quando `SQLExecute` ou `SQLExecuteDirect` for chamado. Em particular, o cliente trata qualquer truncamento de frações de segundo como um erro, enquanto o comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é arredondar; por exemplo, o arredondamento ocorre quando você vai do `datetime2(6)` para o `datetime2(2)`. Os valores da coluna datetime são arredondados para 1/300º de um segundo e as colunas smalldatetime têm os segundos definidos como zero pelo servidor.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1, 5, 7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1, 5, 7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|N/D|N/D|1,10,11|N/D|N/D|N/D|N/D|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/D|N/D|N/D|N/D|1,10,11|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9, 3|9,10|9,7,10|9,5,7,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9, 3, 4|9,4,10|9,10|9,5,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9, 3, 4, 8|9,4,8,10|9,8,10|9,10|N/D|N/D|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão. Será gerado um registro de diagnóstico com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".|  
|1|Se os dados fornecidos não forem válidos, um registro de diagnóstico será gerado com SQLSTATE 22007 e a mensagem "Formato de datetime inválido".|  
|2|Os campos de hora devem ser zero ou um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Truncamento fracionário".|  
|3|Os segundos fracionais devem ser zero ou um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Truncamento fracionário".|  
|4|O componente de data é ignorado.|  
|5|O fuso horário é definido com a configuração de fuso horário do cliente.|  
|6|A hora é definida como zero.|  
|7|A data é definida com a data atual.|  
|8|A hora é convertida do fuso horário do cliente para UTC. Se ocorrer um erro durante esta conversão, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime".|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é então convertida no tipo de destino, seguindo as regras na tabela anterior para o tipo de origem descoberto por este processo. Se for detectado um erro ao analisar os dados, um registro de diagnóstico será gerado com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão". Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo ao qual esses tipos dão suporte, um registro de diagnóstico será gerado com SQLSATE 22007 e a mensagem "Formato de datetime inválido".<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não estiver no intervalo de UTC com suporte, um registro de diagnóstico será gerado com SQLSTATE 22007 e a mensagem "Formato de datetime inválido".|  
|10|Se ocorrer truncamento com perda de dados, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Formato de hora inválido". Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor.|  
|11|Se o comprimento de bytes dos dados não for igual ao tamanho da estrutura exigida pelo tipo SQL, um registro de diagnóstico será gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".|  
|12|Se o comprimento de bytes dos dados for 4 ou 8, os dados serão enviados para o servidor no formato TDS bruto smalldatetime ou datetime. Se o comprimento de bytes dos dados corresponder exatamente ao tamanho de SQL_TIMESTAMP_STRUCT, os dados serão convertidos no formato TDS para datetime2.|  
|13|Se ocorrer truncamento com perda de dados, um registro de diagnóstico será gerado com SQLSTATE 22001 e a mensagem "Dados de cadeia de caracteres truncados à direita".<br /><br /> O número de dígitos de segundos fracionários (a escala) é determinado do tamanho da coluna de destino de acordo com o seguinte:<br /><br /> **Tipo:** SQL_C_TYPE_TIMESTAMP<br /><br /> Escala implícita<br /><br /> 0<br /><br /> 19<br /><br /> Escala implícita<br /><br /> 1.. 9<br /><br /> 21..29<br /><br /> Entretanto, para SQL_C_TYPE_TIMESTAMP, se as frações de segundo puderem ser representadas com três dígitos sem perda de dados e o tamanho da coluna for 23 ou maior, serão gerados exatamente três dígitos de frações de segundo. Esse comportamento assegura a compatibilidade com versões anteriores de aplicativos desenvolvidos usando drivers ODBC mais antigos.<br /><br /> Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo ODBC.<br /><br /> Um tamanho de coluna zero implica em tamanho ilimitado para tipos de caracteres de comprimento variável no ODBC (9 dígitos, a menos que a regra de 3 dígitos para SQL_C_TYPE_TIMESTAMP se aplique). A especificação de um tamanho de coluna zero com um tipo de caractere de comprimento fixo é um erro.|  
|N/D|O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;&#41;ODBC](date-and-time-improvements-odbc.md)  
  
  

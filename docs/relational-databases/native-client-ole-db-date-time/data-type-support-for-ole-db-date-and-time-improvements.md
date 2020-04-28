---
title: Suporte a tipos de dados para melhorias de data e hora do OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], data type support
- OLE DB, date/time improvements
ms.assetid: d40e3fd6-9057-4371-8236-95cef300603e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f00744ce2f0363e7fcf38820b20e2b631df7adc6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301038"
---
# <a name="data-type-support-for-ole-db-date-and-time-improvements"></a>Suporte a tipos de dados para melhorias de data e hora do OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico fornece informações sobre tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB (cliente nativo) que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte a tipos de dados de data/hora.  
  
## <a name="data-type-mapping-in-rowsets-and-parameters"></a>Mapeamento de tipos de dados em conjuntos de linhas e parâmetros  
 O OLE DB fornece dois novos tipos de dados para dar suporte aos novos tipos de servidor: DBTYPE_DBTIME2 e DBTYPE_DBTIMESTAMPOFFSET. A seguinte tabela mostra o mapeamento de tipo do servidor completo:  
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Tipo de dados OLE DB|Valor|  
|-----------------------------------------|----------------------|-----------|  
|DATETIME|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|smalldatetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|date|DBTYPE_DBDATE|133 (oledb.h)|  
|time|DBTYPE_DBTIME2|145 (sqlncli. h)|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|146 (sqlncli. h)|  
|datetime2|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
  
## <a name="data-formats-strings-and-literals"></a>Formatos de dados: cadeias e literais  
  
|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Tipo de dados OLE DB|Formato de cadeia de caracteres para conversões do cliente|  
|-----------------------------------------|----------------------|------------------------------------------|  
|DATETIME|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss[.999]'<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a até três dígitos de fração de segundo para Datetime.|  
|smalldatetime|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss'<br /><br /> Este tipo de dados tem precisão de um minuto. O componente de segundos será zero na saída, sendo arredondado pelo servidor na entrada.|  
|date|DBTYPE_DBDATE|'aaaa-mm-dd'|  
|time|DBTYPE_DBTIME2|'hh:mm:ss[.9999999]'<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
|datetime2|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss[.fffffff]'<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|'aaaa-mm-dd hh:mm:ss[.fffffff] +/-hh:mm'<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
  
 Não há nenhuma alteração às sequências de escape para literais de data/hora.  
  
 As frações de segundo nos resultados usam um ponto (.) em vez de um dois-pontos (:).  
  
 Valores da cadeia de caracteres passados como retorno aos aplicativos sempre terão o mesmo comprimento para uma determinada coluna. Componentes de ano, mês, dia, hora, minuto e segundo serão preenchidos com zeros à esquerda até seu comprimento máximo. Haverá exatamente um espaço entre a data e a hora e exatamente um espaço entre a hora e o deslocamento de fuso horário. Um deslocamento de fuso horário sempre será precedido de um sinal. Este sinal será positivo (+) quando o deslocamento for zero. Não haverá nenhum espaço em branco entre o sinal e o valor do deslocamento. Frações de segundo serão preenchidas com zero à direita, se necessário, até a precisão definida para a coluna, mas não mais que isso. Para colunas do tipo datetime, haverá três dígitos para frações de segundo. Para colunas do tipo smalldatetime, não haverá nenhum dígito de fração de segundo e os segundos sempre serão zero.  
  
 Conversões de valores da cadeia de caracteres fornecidos pelo aplicativo serão mais flexíveis e permitirão valores componentes com comprimento menor que o máximo. Anos podem ter de 1 a 4 dígitos. Meses, dias, horas, minutos e segundos podem ter 1 ou 2 dígitos. Pode haver um espaço em branco arbitrário entre data/hora e hora/deslocamentos de fuso horário. O sinal de um deslocamento com zero horas e zero minutos pode ser mais ou menos. São permitidos zeros à direita para frações de segundo até um máximo de 9 dígitos. Um componente de hora pode terminar com um ponto decimal e não ter dígitos de fração de segundo.  
  
 Uma cadeia de caracteres vazia não é um literal de data/hora válido e não representa um valor NULL. Uma tentativa de conversão de uma cadeia de caracteres vazia para um valor de data/hora resultará em erros com SQLState 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão".  
  
## <a name="data-formats-data-structures"></a>Formatos de dados: estruturas de dados  
 Nas estruturas específicas do OLE DB descritas a seguir, o OLE DB obedece às mesmas restrições que o ODBC. Elas são extraídas do calendário gregoriano:  
  
-   O intervalo de meses é de 1 a 12.  
  
-   O intervalo do campo de dias é de 1 ao número de dias do mês e deve ser coerente com os campos de ano e mês, levando em conta os anos bissextos.  
  
-   O intervalo de horas é de 0 a 23.  
  
-   O intervalo de minutos é de 0 a 59.  
  
-   O intervalo de segundos é de 0 a 59. Isso permite até dois segundos bissextos para manter a sincronização com a hora sideral.  
  
 Foram modificadas as implementações dos seguintes structs do OLE DB existentes para dar suporte aos novos tipos de data e hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, as definições não foram alteradas.  
  
-   DBTYPE_DATE (É um tipo de automação DATE. Ele é representado internamente como um **double**. A parte inteira é o número de dias desde 30 de dezembro de 1899 e a parte fracionária é a fração de um dia. Este tipo tem uma exatidão de 1 segundo, portanto tem uma escala efetiva de 0.)  
  
-   DBTYPE_DBDATE  
  
-   DBTYPE_DBTIME  
  
-   DBTYPE_DBTIMESTAMP (o campo de fração é definido pelo OLE DB como o número de bilionésimos de segundo (nanossegundos) e varia de 0 a 999.999.999)  
  
-   DBTYPE_FILETIME  
  
### <a name="dbtype_dbtime2"></a>DBTYPE_DBTIME2  
 Esse struct é preenchido com até 12 bytes nos sistemas operacionais de 32 e 64 bits.  
  
```  
typedef struct tagDBTIME2 {  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    } DBTIME2;  
```  
  
### <a name="dbtype_-dbtimestampoffset"></a>DBTYPE_ DBTIMESTAMPOFFSET  
  
```  
typedef struct tagDBTIMESTAMPOFFSET {  
    SHORT year;  
    USHORT month;  
    USHORT day;  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    SHORT timezone_hour;  
    SHORT timezone_minute;  
    } DBTIMESTAMPOFFSET;  
```  
  
 Se `timezone_hour` for negativo, `timezone_minute` deve ser negativo ou zero. Se `timezone_hour` for positivo, `timezone minute` deve ser positivo ou zero. Se `timezone_hour` for zero, `timezone minute` poderá ter valor entre -59 e +59.  
  
### <a name="ssvariant"></a>SSVARIANT  
 Agora esse struct inclui as novas estruturas, DBTYPE_DBTIME2 e DBTYPE_DBTIMESTAMPOFFSET, e adiciona a escala de frações de segundo para os tipos apropriados.  
  
```  
struct SSVARIANT {  
   SSVARTYPE vt;  
   DWORD dwReserved1;  
   DWORD dwReserved2;  
   union {  
// ...  
      DBTIMESTAMP tsDateTimeVal;  
      DBDATE dDateVal;  
      struct _Time2Val {  
         DBTIME2 tTime2Val;  
         BYTE bScale;  
      } Time2Val;  
      struct _DateTimeVal {  
         DBTIMESTAMP tsDateTimeVal;  
         BYTE bScale;  
      } DateTimeVal;  
      struct _DateTimeOffsetVal {   
         DBTIMESTAMPOFFSET tsoDateTimeOffsetVal;  
         BYTE bScale;  
      } DateTimeOffsetVal;  
// ...  
   };  
};  
```  
  
 Além disso, o enum associado à codificação do tipo SSVARIANT, que determina o tipo do enum, será estendido conforme indicado a seguir:  
  
```  
enum SQLVARENUM {  
// ...  
   // Datetime  
   VT_SS_DATETIME      = DBTYPE_DBTIMESTAMP,  
   VT_SS_SMALLDATETIME = 206,  
  
   VT_SS_DATE = DBTYPE_DBDATE,  
   VT_SS_TIME2 = DBTYPE_DBTIME2,  
   VT_SS_DATETIME2 = 212  
   VT_SS_DATETIMEOFFSET = DBTYPE_DBTIMESTAMPOFFSET  
};  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os aplicativos que usam o **sql_variant** e contam com a precisão limitada de **DateTime** precisarão ser atualizados se o esquema subjacente for atualizado para usar **datetime2** em vez de **DateTime**.  
  
 Também foram estendidas as macros de acesso para SSVARIANT com a adição do seguinte:  
  
```  
#define V_SS_DATETIME2(X)       V_SS_UNION(X, DateTimeVal)  
#define V_SS_TIME2(X)           V_SS_UNION(X, Time2Val)  
#define V_SS_DATE(X)            V_SS_UNION(X, dDateVal)  
#define V_SS_DATETIMEOFFSET(X)  V_SS_UNION(X, DateTimeOffsetVal)  
```  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Mapeamento de tipo de dados em ITableDefinition::CreateTable  
 O seguinte mapeamento de tipo é usado com estruturas DBCOLUMNDESC usadas por ITableDefinition::CreateTable:  
  
|Tipo de dados OLE DB (*wType*)|Tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Observações|  
|----------------------------------|-----------------------------------------|-----------|  
|DBTYPE_DBDATE|date||  
|DBTYPE_DBTIMESTAMP|**datetime2**(p)|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro DBCOLUMDESC *bScale* para determinar a precisão de segundos fracionários.|  
|DBTYPE_DBTIME2|**time**(p)|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro DBCOLUMDESC *bScale* para determinar a precisão de segundos fracionários.|  
|DBTYPE_DBTIMESTAMPOFFSET|**datetimeoffset**(p)|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro DBCOLUMDESC *bScale* para determinar a precisão de segundos fracionários.|  
  
 Quando um aplicativo especificar DBTYPE_DBTIMESTAMP em *wType*, ele poderá substituir o mapeamento para **datetime2** fornecendo um nome de tipo em *pwszTypeName*. Se **datetime** for especificado, *bScale* precisará ser 3. Se **smalldatetime** for especificado, *bScale* precisará ser 0. Se *bScale* não for consistente com *wType* e *pwszTypeName*, DB_E_BADSCALE será retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  

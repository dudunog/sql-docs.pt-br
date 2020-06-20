---
title: srv_describe (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_describe
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
ms.openlocfilehash: 264781f21e328c4740ee31b53fe3812bbe392305
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050778"
---
# <a name="srv_describe-extended-stored-procedure-api"></a>srv_describe (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Define o nome da coluna e os tipos de dados da origem e do destino de uma coluna específica em sequência.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Trata-se de um ponteiro para a estrutura SRV_PROC, que é o identificador de uma conexão de cliente específica (nesse caso, o cliente que envia a linha). A estrutura contém todas as informações que a biblioteca de APIs de Procedimento Armazenado Estendido usa para gerenciar as comunicações e os dados entre o aplicativo e o cliente.  
  
 *colnumber*  
 Atualmente ele não tem suporte. As colunas devem ser descritas em ordem. Todas as colunas devem ser descritas antes de **srv_sendrow** ser chamado.  
  
 *column_name*  
 Especifica o nome da coluna à qual pertencem os dados. Esse parâmetro pode ser NULL, porque não é obrigatório que uma coluna tenha um nome.  
  
 *namelen*  
 Especifica o tamanho, em bytes, de *column_name*. Se *namelen* for SRV_NULLTERM, *column_name* deverá terminar em nulo.  
  
 *desttype*  
 Especifica o tipo de dados da coluna da linha de destino. Trata-se do tipo de dados enviado ao cliente. O tipo de dados deverá ser especificado mesmo se os dados forem NULL; para obter mais informações, consulte [Tipos de dados &#40;API de Procedimento Armazenado Estendido&#41;](data-types-extended-stored-procedure-api.md).  
  
 *destlen*  
 Especifica o comprimento, em bytes, dos dados a serem enviados ao cliente. Para tipos de dados de comprimento fixo que não permitem valores nulos, *destlen* é ignorado. Para tipos de dados de comprimento variável e tipos de dados de comprimento fixo que permitem valores nulos, *destlen* especifica o tamanho máximo que os dados de destino podem ter.  
  
 *srctype*  
 Especifica o tipo dos dados de origem.  
  
 *srclen*  
 Especifica o comprimento, em bytes, dos dados de origem. Esse valor é ignorado em tipos de dados de comprimento fixo.  
  
 *srcdata*  
 Fornece o endereço dos dados de origem de uma determinada coluna. Quando **srv_sendrow** é chamado, ele procura os dados de *colnumber* em *srcdata*. Por isso, ele não deve ser liberado antes de uma chamada para **srv_sendrow**. O endereço dos dados de origem pode ser alterado entre chamadas para **srv_sendrow**, usando **srv_setcoldata**. A memória alocada para *srcdata* não deve ser liberada até que os dados da coluna sejam substituídos por outra chamada para **srv_setcoldata** ou até que **srv_senddone** seja chamado.  
  
 Caso *desttype* seja SRVDECIMAL ou SRVNUMERIC, o parâmetro *srcdata* deverá ser um ponteiro para uma estrutura DBNUMERIC ou DBDECIMAL com os campos de precisão e escala da estrutura já definidos com os valores desejados. É possível usar DEFAULTPRECISION para especificar uma precisão padrão, e DEFAULTSCALE para especificar uma escala padrão.  
  
## <a name="returns"></a>Retornos  
 O número da coluna descrita. A primeira coluna é a coluna 1. Caso ocorra um erro, retorna 0.  
  
## <a name="remarks"></a>Comentários  
 A função **srv_describe** deve ser chamada uma vez a cada coluna na linha antes da primeira chamada a **srv_sendrow**. As colunas de uma linha podem ser descritas em qualquer ordem.  
  
 Para alterar o local e o tamanho dos dados de origem nas linhas da coluna antes de o conjunto de resultados completo ser enviado, use **srv_setcoldata** e **srv_setcollen**, respectivamente.  
  
 Para obter uma descrição dos tipos de dados e conversões de tipo de dados da API de Procedimento Armazenado Estendido, consulte [Tipos de dados &#40;API de Procedimento Armazenado Estendido&#41;](data-types-extended-stored-procedure-api.md).  
  
 Caso o nome da coluna do aplicativo esteja em Unicode, você precisará convertê-lo na página de código multibyte do servidor antes de chamar **srv_describe**. Para obter mais informações, consulte [dados Unicode e páginas de código do servidor](../extended-stored-procedures-programming/unicode-data-and-server-code-pages.md).  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_sendrow &#40;API de procedimento armazenado estendido&#41;](srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype &#40;API de procedimento armazenado estendido&#41;](srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata &#40;API de Procedimento Armazenado Estendido&#41;](srv-setcoldata-extended-stored-procedure-api.md)  
  
  

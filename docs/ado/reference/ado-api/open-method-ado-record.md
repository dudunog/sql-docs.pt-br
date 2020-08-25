---
description: Método Open (Registro do ADO)
title: Método Open (registro ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: rothja
ms.author: jroth
ms.openlocfilehash: 980e7c840cfb19077c6f4f1d1041d1f1eb8acf64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773795"
---
# <a name="open-method-ado-record"></a>Método Open (Registro do ADO)
Abre um objeto de [registro](./record-object-ado.md) existente ou cria um novo item representado pelo **registro**, como um arquivo ou diretório.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Uma **variante** que pode representar a URL da entidade a ser representada por este objeto de **registro** , um **comando**, um [conjunto de registros](./recordset-object-ado.md) aberto ou outro objeto de **registro** , uma cadeia de caracteres que contém uma instrução SQL SELECT ou um nome de tabela.  
  
 *ActiveConnection*  
 Opcional. Uma **variante** que representa a cadeia de conexão ou o objeto Open [Connection](./connection-object-ado.md) .  
  
 *Modo*  
 Opcional. Um valor de [ConnectModeEnum](./connectmodeenum.md) que especifica o modo de acesso para o objeto de **registro** resultante. O valor padrão é **adModeUnknown**.  
  
 *Criaroptions*  
 Opcional. Um valor de [RecordCreateOptionsEnum](./recordcreateoptionsenum.md) que especifica se um arquivo ou diretório existente deve ser aberto ou se um novo arquivo ou diretório deve ser criado. O valor padrão é **adFailIfNotExists**. Se definido como o valor padrão, o modo de acesso é obtido da propriedade [Mode](./mode-property-ado.md) . Esse parâmetro é ignorado quando o parâmetro de *origem* não contém uma URL.  
  
 *Opções*  
 Opcional. Um valor [RecordOpenOptionsEnum](./recordopenoptionsenum.md) que especifica as opções para abrir o **registro**. O valor padrão é **adOpenRecordUnspecified**. Esses valores podem ser combinados.  
  
 *UserName*  
 Opcional. Um valor de **cadeia de caracteres** que contém a ID de usuário que, se necessário, autoriza o acesso à *origem*.  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém a senha que, se necessário, verifica o *nome de usuário*.  
  
## <a name="remarks"></a>Comentários  
 A *origem* pode ser:  
  
-   Uma URL. Se o protocolo para a URL for http, o provedor da Internet será invocado por padrão. Se a URL aponta para um nó que contém um script executável (como um. Página ASP), um **registro** que contém a origem em vez do conteúdo executado é aberto por padrão. Use o argumento *Options* para modificar esse comportamento.  
  
-   Um objeto de **registro** . Um objeto de **registro** aberto de outro **registro** clonará o objeto de **registro** original.  
  
-   Um objeto de **comando** . O objeto de **registro** aberto representa a única linha retornada pela execução do **comando**. Se os resultados contiverem mais de uma única linha, o conteúdo da primeira linha será colocado no registro e um erro poderá ser adicionado à coleção de **erros** .  
  
-   Uma instrução SQL SELECT. O objeto de **registro** aberto representa a única linha retornada pela execução do conteúdo da cadeia de caracteres. Se os resultados contiverem mais de uma única linha, o conteúdo da primeira linha será colocado no registro e um erro poderá ser adicionado à coleção de **erros** .  
  
-   Um nome de tabela.  
  
 Se o objeto **Record** representa uma entidade que não pode ser acessada com uma URL (por exemplo, uma linha de um **conjunto de registros** derivado de um banco de dados), os valores da propriedade [ParentURL](./parenturl-property-ado.md) e do campo acessados com a constante **adRecordURL** são NULL.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Open (conexão ADO)](./open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](./open-method-ado-recordset.md)   
 [Método Open (fluxo ADO)](./open-method-ado-stream.md)   
 [Método OpenSchema](./openschema-method.md)
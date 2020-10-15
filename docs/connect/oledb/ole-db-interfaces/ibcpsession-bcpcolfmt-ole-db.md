---
title: IBCPSession::BCPColFmt (driver do OLE DB) | Microsoft Docs
description: Saiba como o método IBCPSession::BCPColFmt cria uma associação entre variáveis de programa e colunas do SQL Server no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPColFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColFmt method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bfff1da26e499043206fc3f777e1bd9ba5902e44
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081855"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPColFmt(   
      DBORDINAL idxUserDataCol,  
      int eUserDataType,  
      int cbIndicator,  
      int cbUserData,  
      BYTE *pbUserDataTerm,  
      int cbUserDataTerm,  
      DBORDINAL idxServerCol);  
```  
  
## <a name="remarks"></a>Comentários  
 O método **BCPColFmt** é usado para criar uma associação entre campos de arquivo de dados BCP e colunas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ele usa o comprimento, o tipo, o terminador e o comprimento do prefixo de uma coluna como parâmetros e define cada uma dessas propriedades para arquivos individuais.  
  
 Caso o usuário opte pelo modo interativo, esse método é chamado duas vezes: uma para definir o formato da coluna de acordo com os valores padrão (que dependem do tipo de coluna do servidor) e outra para definir o formato de acordo com o tipo de coluna da opção feita pelo cliente durante o modo interativo em cada coluna.  
  
 Em modos não interativos, ele é chamado somente uma vez por coluna para definir o tipo de cada coluna como caractere ou tipo nativo, além de definir os terminadores de coluna e linha.  
  
 O método **BCPColFmt** permite especificar o formato de arquivo do usuário para cópias em massa. Para cópia em massa, um formato contém as seguintes partes:  
  
-   Um mapeamento dos campos de arquivo do usuário para as colunas do banco de dados.  
  
-   O tipo de dados de cada campo de arquivo do usuário.  
  
-   O comprimento do indicador opcional de cada campo.  
  
-   O comprimento máximo dos dados por campo de arquivo do usuário.  
  
-   A sequência de bytes de encerramento opcional de cada campo <a href="#terminator_note"><sup>**1**</sup></a>.  
  
-   O comprimento da sequência de bytes de encerramento opcional <a href="#terminator_note"><sup>**1**</sup></a>.  
  

> [!IMPORTANT]
> <b id="terminator_note">[1]:</b> O uso da sequência de encerramento em cenários em que a página de código do arquivo de dados está definida como UTF-8 não é compatível. Nesses cenários, **pbUserDataTerm** deve ser definido como `nullptr` e **cbUserDataTerm** deve ser definido como `0`.

 Cada chamada para **BCPColFmt** especifica o formato de um campo de arquivo do usuário. Por exemplo, para alterar as configurações padrão de três campos em um arquivo de dados do usuário com cinco campos, primeiro chame `BCPColumns(5)`e, em seguida, **BCPColFmt** cinco vezes, com três dessas chamadas definindo o formato personalizado. Para as duas chamadas restantes, defina *eUserDataType* como BCP_TYPE_DEFAULT, além de *cbIndicator*, *cbUserData*e *cbUserDataTerm* como 0, BCP_VARIABLE_LENGTH e 0, respectivamente. Esse procedimento copia todas as cinco colunas, três com seu formato personalizado e duas com o formato padrão.  
  
> [!NOTE]  
>  O método [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) precisa ser chamado antes de qualquer chamada a **BCPColFmt**. Você deve chamar **BCPColFmt** uma vez para cada coluna no arquivo do usuário. Chamar **BCPColFmt** mais de uma vez para qualquer coluna de arquivo do usuário causa um erro.  
  
 Você não precisa copiar todos os dados de um arquivo de usuário para uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para ignorar uma coluna, especifique o formato dos dados da coluna definindo o parâmetro idxServerCol como 0. Para ignorar um campo, você continua precisando de todas as informações para que o método funcione corretamente.  
  
 **Observação** a função [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) pode ser usada para persistir a especificação do formato fornecida por meio de **BCPColFmt**.  
  
## <a name="arguments"></a>Argumentos  
 *idxUserDataCol*[in]  
 Índice do campo no arquivo de dados do usuário.  
  
 *eUserDataType*[in]  
 O tipo de dados do campo no arquivo de dados do usuário. Os tipos de dados disponíveis são listados no arquivo de cabeçalho do Driver do OLE DB para SQL Server (msoledbsql.h) com o formato BCP_TYPE_XXX; por exemplo, BCP_TYPE_SQLINT4. Caso o valor BCP_TYPE_DEFAULT seja especificado, o provedor tenta usar o mesmo tipo como a tabela ou o tipo de coluna de exibição. Para operações de cópia em massa fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e em um arquivo quando o argumento **eUserDataType** é BCP_TYPE_SQLDECIMAL ou BCP_TYPE_SQLNUMERIC:  
  
-   Se a coluna de origem não for decimal ou numeric, serão usadas a precisão e escala padrão.  
  
-   Se a coluna de origem não for decimal ou numéric, serão usadas a precisão e escala da coluna de origem.  
  
 *cbIndicator*[in]  
 Comprimento do prefixo do campo. O padrão é BCP_PREFIX_DEFAULT. Os comprimentos válidos do prefixo são 0, 1, 2, 4 e 8. Um tamanho de prefixo igual a 8 é mais usado para indicar que o campo está em bloco. Isso é usado para copiar grandes colunas de tipo de valor em massa com eficiência.  
  
 *cbUserData*[in]  
 O comprimento máximo, em bytes, dos dados desse campo no arquivo do usuário, sem incluir o comprimento de qualquer indicador de comprimento ou terminador.  
  
 Definir **cbUserData** como BCP_LENGTH_NULL indica que todos os valores nos campos de arquivo de dados são, ou deveriam ser, definidos como NULL. Definir **cbUserData** como BCP_LENGTH_VARIABLE indica que o sistema deve determinar o comprimento dos de cada campo. Para alguns campos, isso poderia significar que um indicador de comprimento/nulidade é gerado para preceder dados de uma cópia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou que o indicador é esperado nos dados copiados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para tipos de dados binários e de caractere do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], **cbUserData** pode ser BCP_LENGTH_VARIABLE, BCP_LENGTH_NULL, 0 ou um valor positivo. Caso **cbUserData** seja BCP_LENGTH_VARIABLE, o sistema usa o indicador de comprimento, se presente, ou uma sequência de terminador para determinar o comprimento dos dados. Se forem fornecidos um indicador de comprimento e uma sequência de terminador, a cópia em massa usará aquele que resultar na menor quantidade de dados sendo copiados. Se **cbUserData** for BCP_LENGTH_VARIABLE, o tipo de dados for um caractere ou um tipo binário do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um indicador de tamanho nem uma sequência de terminador forem especificados, o sistema retornará uma mensagem de erro.  
  
 Se **cbUserData** for 0 ou um valor positivo, o sistema usará **cbUserData** como o comprimento de dados máximo. Entretanto, se, além de um **cbUserData**positivo, for fornecido um indicador de comprimento ou uma sequência de terminador, o sistema determinará o comprimento dos dados usando o método que resulta na menor quantidade de dados sendo copiados.  
  
 O valor **cbUserData** representa a contagem de bytes dos dados. Se dados de caracteres forem representados por caracteres que abrangem Unicode, um valor de parâmetro **cbUserData** positivo representará o número de caracteres multiplicado pelo tamanho, em bytes, de cada caractere.  
  
 *pbUserDataTerm*[size_is][in]  
 A sequência de terminador a ser usada para o campo. Este parâmetro é útil principalmente para tipos de dados character porque todos os outros tipos têm comprimento fixo ou, no caso de dados binary, exigem um indicador de comprimento que permite registrar com precisão o número de bytes presentes.  
  
 Para evitar encerrar os dados extraídos ou indicar que os dados em um arquivo de usuário não foram encerrados, defina este parâmetro como NULL.  
  
 Se for usada mais de uma maneira de especificar um comprimento de coluna de arquivo de usuário (como um terminador e um indicador de comprimento ou um terminador e um comprimento de coluna máximo), a cópia em massa escolherá aquela que resultar na menor quantidade de dados sendo copiados.  
  
 A API de cópia em massa executa a conversão de caracteres Unicode em MBCS conforme necessário. É necessário tomar cuidado para garantir que tanto a cadeia de caracteres de bytes do terminador quanto o comprimento da cadeia de caracteres de bytes estejam definidos corretamente. Confira a seção [Comentários](#remarks) acima para ver as limitações da codificação UTF-8.

 *cbUserDataTerm*[in]  
 O comprimento, em bytes, da sequência de terminador a ser usada para a coluna. Se nenhum terminador estiver presente ou for desejado nos dados, defina esse valor como 0. Confira a seção [Comentários](#remarks) acima para ver as limitações da codificação UTF-8.

 *idxServerCol*[in]  
 A posição ordinal da coluna na tabela do banco de dados. O número da primeira coluna é 1. A posição ordinal de uma coluna é informada por **IColumnsInfo::GetColumnInfo** ou métodos semelhantes. Caso esse valor seja 0, a cópia em massa ignora o campo no arquivo de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Erro específico do provedor. Para obter informações detalhadas, use a interface [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md).  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) não foi chamado antes desse método.  
  
 E_INVALIDARG  
 O argumento era inválido.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
  

---
title: Lendo exemplo de dados grandes com procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7132ddcd254358cd2199145d260f09ed0465adb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027811"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Lendo exemplo de dados grandes com procedimentos armazenados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como recuperar um parâmetro OUT grande de um procedimento armazenado.

O arquivo de código desta amostra chama-se ExecuteStoredProcedure.java e pode ser encontrado neste local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Você também precisará definir o classpath para incluir o arquivo mssql-jdbc.jar. Para obter mais informações sobre como definir o caminho de classe, confira [Como usar o JDBC Driver](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

O exemplo criaria o procedimento armazenado exigido no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria dados de exemplo e atualiza a tabela Production.Document usando uma consulta parametrizada. Em seguida, o código de exemplo obtém o modo de buffer adaptável usando o método [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) e executa o procedimento armazenado GetLargeDataValue. A partir da versão 2.0 do driver JDBC, a propriedade de conexão responseBuffering é definida como "adaptável" por padrão.

Por fim, o código de exemplo exibe os dados retornados com os parâmetros OUT e também demonstra como usar os métodos `mark` e `reset` no fluxo para reler qualquer parte dos dados.

[!code[JDBC#UsingAdaptiveBuffering2](../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Confira também

[Trabalhando com dados grandes](../../connect/jdbc/working-with-large-data.md)

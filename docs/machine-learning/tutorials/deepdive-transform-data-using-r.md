---
title: Transformar dados usando o RevoScaleR
description: 'Tutorial 9 do RevoScaleR: Como transformar dados usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 03f8b3f9cacd4faa77116cd560abfdb81596d074
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116729"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>Transformar dados usando o R (tutorial do SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o tutorial 9 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você aprenderá sobre as funções do **RevoScaleR** para transformar os dados em vários estágios da análise.

> [!div class="checklist"]
> * Use **rxDataStep** para criar e transformar um subconjunto de dados
> * Use **rxImport** para transformar dados em trânsito de ou para um arquivo XDF ou um quadro de dados na memória durante a importação

Embora não sejam destinadas especificamente à movimentação de dados, as funções **rxSummary**, **rxCube**, **rxLinMod**e **rxLogit** dão suporte a transformações de dados.

## <a name="use-rxdatastep-to-transform-variables"></a>Usar o rxDataStep para transformar variáveis

A função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) processa uma parte dos dados por vez, lendo de uma fonte de dados e gravando em outra. Você pode especificar as colunas a serem transformadas, bem como as transformações a serem carregadas, e assim por diante.

Para tornar este exemplo interessante, vamos usar uma função de outro pacote do R para transformar os dados. O pacote **inicialização** é um dos pacotes “recomendados”, o que significa que **inicialização** é incluído com cada distribuição do R, mas não é carregado automaticamente na inicialização. Portanto, o pacote já deve estar disponível na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada para a integração do R.

No pacote **inicialização**, use a função **inv.logit**, que calcula o inverso de um logit. Ou seja, a função **inv.logit** converte um logit novamente para uma probabilidade na escala [0,1].

> [!TIP] 
> Outra maneira de fazer previsões nessa escala é definir o parâmetro *type* como **response** na chamada original à **rxPredict**.

1. Comece criando uma fonte de dados para manter os dados destinados à tabela, `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Adicione outra fonte de dados para manter os dados da tabela `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    Na nova tabela, armazene todas as variáveis da tabela `ccScoreOutput` anterior, além da variável recém-criada.
  
3. Defina o contexto de computação como a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use a função **rxSqlServerTableExists** para verificar se a tabela de saída `ccScoreOutput2` já existe e, nesse caso, use a função **rxSqlServerDropTable** para excluir a tabela.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Chame a função **rxDataStep** e especifique as transformações desejadas em uma lista.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Quando define as transformações aplicadas a cada coluna, você também pode especificar todos os pacotes do R adicionais necessários para executar as transformações.  Para obter mais informações sobre os tipos de transformações que podem ser executadas, confira [Como transformar e fazer subconjuntos de dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Chame **rxGetVarInfo** para exibir um resumo das variáveis no novo conjunto de dados.
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**Resultados**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

As pontuações de logit originais são preservadas, mas uma nova coluna, *ccFraudProb*, foi adicionada, na qual as pontuações de logit são representadas como valores entre 0 e 1.

Observe que as variáveis de fator foram gravadas na tabela `ccScoreOutput2` como dados de caractere. Para usá-las como fatores nas próximas análises, use o parâmetro *colInfo* para especificar os níveis.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Carregar dados na memória usando rxImport](../../machine-learning/tutorials/deepdive-load-data-into-memory-using-rximport.md)
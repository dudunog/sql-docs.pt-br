---
title: 'Tutorial do R: Criar recursos de dados'
titleSuffix: SQL machine learning
description: Na terceira parte desta série de tutoriais em cinco partes, você usará as funções do T-SQL para criar e armazenar recursos de dados de exemplo com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: 67c8c2c34ff49df4c9be7bea9dc1015d4bcebedd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470167"
---
# <a name="r-tutorial-create-data-features"></a>Tutorial do R: Criar recursos de dados
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

Na terceira parte desta série de tutoriais em cinco partes, você aprenderá a criar recursos a partir de dados brutos usando uma função do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você chamará essa função por meio de um procedimento armazenado do SQL para criar uma tabela que contém os valores de recurso.

Neste artigo, você vai:

> [!div class="checklist"]
> + Modificar uma função personalizada para calcular a distância de viagem
> + Salvar os recursos usando outra função personalizada

Na [parte um](r-taxi-classification-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](r-taxi-classification-explore-data.md), você examinou os dados do exemplo e gerou alguns gráficos.

Na [parte quatro](r-taxi-classification-train-model.md), você carregará os módulos e chamará as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server.

Na [parte cinco](r-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

Na [parte cinco](./python-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

## <a name="about-feature-engineering"></a>Sobre a engenharia de recursos

Após várias rodadas de exploração de dados, você reuniu algumas ideias sobre os dados e está pronto para passar para a *engenharia de recursos*. Esse processo de criação de recursos significativos com base nos dados brutos é uma etapa crítica para a criação de modelos analíticos.

Neste conjunto de dados, os valores de distância baseiam-se na distância do medidor relatado e não representam necessariamente a distância geográfica nem a distância real percorrida. Portanto, você precisará calcular a distância direta entre os pontos de embarque e desembarque de passageiros, usando as coordenadas disponíveis no conjunto de dados NYC Taxi de origem. Você pode fazer isso usando a [fórmula de Haversine](https://en.wikipedia.org/wiki/Haversine_formula) em uma função personalizada [!INCLUDE[tsql](../../includes/tsql-md.md)] .

Você usará uma função personalizada do T-SQL, _fnCalculateDistance_, para calcular a distância usando a fórmula de Haversine e usará uma segunda função personalizada do T-SQL, _fnEngineerFeatures_, para criar uma tabela que contém todos os recursos.

Em linhas gerais, o processo é o seguinte:

+ Criar a função T-SQL que executa os cálculos

+ Chamar a função para gerar os dados de recurso

+ Salvar os dados de recurso em uma tabela

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcular a distância da corrida usando fnCalculateDistance

A função _fnCalculateDistance_ deve ter sido baixada e registrada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte da preparação para este tutorial. Reserve um minuto para examinar o código.
  
1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programação**, **Funções** e **Funções de valor escalar**.   

2. Clique com o botão direito do mouse em _fnCalculateDistance_ e selecione **Modificar** para abrir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma nova janela de consulta.
  
   ```sql
   CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
   -- User-defined function that calculates the direct distance between two geographical coordinates.  
   RETURNS float  
   AS  
   BEGIN  
     DECLARE @distance decimal(28, 10)  
     -- Convert to radians  
     SET @Lat1 = @Lat1 / 57.2958  
     SET @Long1 = @Long1 / 57.2958  
     SET @Lat2 = @Lat2 / 57.2958  
     SET @Long2 = @Long2 / 57.2958  
     -- Calculate distance  
     SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
     --Convert to miles  
     IF @distance <> 0  
     BEGIN  
       SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
     END  
     RETURN @distance  
   END
   GO
   ```
  
   + A função é uma função de valor escalar, retornando um único valor de dados de um tipo predefinido.
  
   + Ela usa os valores de latitude e longitude como entradas, obtidos dos locais de embarque e desembarque de passageiros. A fórmula de Haversine converte locais em radianos e usa esses valores para calcular a distância direta em milhas entre os dois locais.

## <a name="generate-the-features-using-_fnengineerfeatures_"></a>Gere os recursos usando _fnEngineerFeatures_

Para adicionar os valores calculados a uma tabela que pode ser usada para treinar o modelo, você usará outra função, _fnEngineerFeatures_. A nova função chama a função do T-SQL criada anteriormente, _fnCalculateDistance_, para obter a distância direta entre os locais de embarque e desembarque de passageiros. 

1. Reserve um minuto para examinar a função personalizada do T-SQL no o código, _fnEngineerFeatures_, que deve ter sido criada como parte da preparação para esse passo a passo.
  
   ```sql
   CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
   @passenger_count int = 0,  
   @trip_distance float = 0,  
   @trip_time_in_secs int = 0,  
   @pickup_latitude float = 0,  
   @pickup_longitude float = 0,  
   @dropoff_latitude float = 0,  
   @dropoff_longitude float = 0)  
   RETURNS TABLE  
   AS
     RETURN
     (
     -- Add the SELECT statement with parameter references here
     SELECT
       @passenger_count AS passenger_count,
       @trip_distance AS trip_distance,
       @trip_time_in_secs AS trip_time_in_secs,
       [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
     )
   GO
   ```

   + Essa é uma função com valor de tabela que usa várias colunas como entradas e gerar uma tabela com várias colunas de recurso.

   + A finalidade dessa função é criar recursos para uso na criação de um modelo.

2. Para verificar se essa função funciona, é possível usá-la para calcular a distância geográfica dessas corridas em que a distância limitada era 0, mas os locais de embarque e desembarque de passageiros eram diferentes.
  
   ```sql
       SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
       trip_distance, pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
       FROM nyctaxi_sample
       WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
       ORDER BY trip_time_in_secs DESC
   ```
  
   Como você pode ver, a distância relatada pelo medidor nem sempre corresponde à distância geográfica. Por isso a engenharia de recursos é tão importante. É possível usar esses recursos de dados aprimorados para treinar um modelo de machine learning usando o R.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Modificou uma função personalizada para calcular a distância de viagem
> + Salvou os recursos usando outra função personalizada

> [!div class="nextstepaction"]
> [Tutorial do R: treinar e salvar o modelo](r-taxi-classification-train-model.md)
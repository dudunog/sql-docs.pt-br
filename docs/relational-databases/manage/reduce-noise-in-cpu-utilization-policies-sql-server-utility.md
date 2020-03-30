---
title: Reduzir o ruído em políticas de utilização da CPU (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9fc6db57277044267a89cc89e6c196c782ea920
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115348"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>Reduzir o ruído em políticas de utilização da CPU (Utilitário do SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use as estratégias a seguir para reduzir o relato de ruídos e violações indesejáveis em políticas de utilização de recursos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>Qual deve ser a frequência de violação na utilização do processador para relatá-lo como superutilizado?  
 O período de tempo de avaliação e a tolerância em violações de percentual são ambos configuráveis usando as definições da guia **Política** no nó **Administração do Utilitário** do Gerenciador do Utilitário. Para alterar políticas, use os controles deslizantes à direita das descrições de política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O intervalo de coleta de dados é de 15 minutos. Este valor não é configurável.  
  
-   O limite superior padrão da política de utilização de processador é de 70%. As opções variam de 0% a 100%.  
  
-   O período de avaliação padrão para superutilização do processador é de 1 hora. As opções variam de 1 hora a 1 semana.  
  
-   O percentual padrão de pontos de dados em violação antes de a CPU ser relatada como superutilizada é de 20%. As opções variam de 0% a 100%.  
  
 Por exemplo, com base em valores padrão, serão coletados 4 pontos de dados a cada hora e o limite de política é de 20%. Então, por padrão, qualquer violação em um período de coleta de 1 hora será 25% de 4 pontos de dados. Os valores padrão relatam qualquer violação do limite da política de superutilização da CPU.  
  
 Para reduzir o ruído gerado por uma única violação, considere as seguintes opções:  
  
-   Aumentar o período de avaliação em 1 incremento para 6 horas. Uma única violação em 6 horas seria 1 ponto de dados em um tamanho de exemplo de 24. Nesse caso, a política toleraria 4 violações do limite da política (16,7% de pontos de dados) em 6 horas, mas relataria a superutilização para 5 ou mais violações (>20% de pontos de dados) em um período de coleta de 6 horas.  
  
-   Aumentar a tolerância para o percentual de violações em 1 incremento para 30%. Uma única violação em 1 hora equivaleria a 1 ponto de dados em um tamanho de exemplo de 4. Nesse caso, a política toleraria 1 violação por hora, mas relataria a superutilização para 2 ou mais violações (>30% de pontos de dados) em um período de coleta de 1 hora.  
  
-   Aumentar os limites da política para a instância gerenciada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e utilização de processador de aplicativo da camada de dados. Para obter mais informações sobre como alterar as políticas de utilização global da CPU de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de aplicativos da camada de dados, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Para obter mais informações sobre como alterar as políticas de utilização da CPU para instâncias individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] veja [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2). Para obter mais informações sobre como alterar as políticas de utilização de CPU de aplicativos da camada de dados individuais, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>Qual deve ser a frequência de violação na utilização do processador para relatá-lo como subutilizado?  
 O período de tempo de avaliação e a tolerância em violações de percentual são ambos configuráveis usando as definições da guia **Política** no nó **Administração do Utilitário** do Gerenciador do Utilitário. Para alterar políticas, use os controles deslizantes à direita das descrições de política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O intervalo de coleta de dados é de 15 minutos. Este valor não é configurável.  
  
-   O limite inferior padrão da política de utilização de processador é de 0%. As opções variam de 0% a 100%.  
  
-   O período de avaliação padrão para subutilização do processador é de 1 semana. As opções variam de 1 dia a 1 mês.  
  
-   O percentual padrão de pontos de dados em violação antes de a CPU ser relatada como subutilizada é de 90%. As opções variam de 0% a 100%.  
  
 Com base em valores padrão, são coletados 672 pontos de dados a cada semana, mas o limite de política é de 0%. Então, por padrão, esta política não gera violações de subutilização de processador. Para obter mais informações sobre como alterar as políticas de utilização global da CPU de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de aplicativos da camada de dados, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Para obter mais informações sobre como alterar as políticas de utilização da CPU para instâncias individuais do SQL Server, veja [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2). Para obter mais informações sobre como alterar as políticas de utilização de CPU de aplicativos da camada de dados individuais, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)   
 [Monitorar instâncias do SQL Server no Utilitário do SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Modificar uma definição de política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  

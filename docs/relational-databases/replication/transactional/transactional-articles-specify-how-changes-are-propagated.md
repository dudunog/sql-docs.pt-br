---
title: Especificar como as alterações são propagadas (Transacional)
description: Saiba como especificar como a alteração é propagada para uma Publicação Transacional em SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e7b267c0bfcfc7e12e2dc17c08bb6b18f2f36bf6
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919894"
---
# <a name="transactional-articles---specify-how-changes-are-propagated"></a>Artigos transacionais – Especificar como as alterações são propagadas
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  A replicação transacional permite que você especifique como as alterações de dados são propagadas do Publicador aos Assinantes. Para cada tabela publicada, você pode especificar uma das quatro maneiras em que cada operação (INSERT, UPDATE ou DELETE) deverá ser propagada ao Assinante:  
  
-   Especifique que a replicação transacional deverá gerar script e subsequentemente chamar um procedimento armazenado para propagar alterações aos Assinantes (o padrão).  
  
-   Especifique que a alteração deverá ser propagada usando uma instrução INSERT, UPDATE ou DELETE (o padrão para Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
-   Especifique que um procedimento armazenado personalizado deverá ser usado.  
  
-   Especifique que esta ação não deverá ser executada em qualquer Assinante. As transações desse tipo não são replicadas.  
  
 Por padrão, a replicação transacional propaga alterações aos Assinantes por um conjunto de procedimentos armazenados instalados em cada Assinante. Quando ocorre uma inserção, atualização ou exclusão em uma tabela no Publicador, a operação é convertida em uma chamada para um procedimento armazenado no Assinante. O procedimento armazenado aceita parâmetros que mapeiam para as colunas da tabela, permitindo que essas colunas sejam alteradas no Assinante.  
  
 Para definir o método de propagação de alterações de dados para artigos transacionais, consulte [Definir o método de propagação de alterações de dados para artigos transacionais](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md).  
  
## <a name="default-and-custom-stored-procedures"></a>Procedimentos armazenados padrão e personalizados  
 Os três procedimentos que a replicação cria por padrão para cada artigo de tabela são:  
  
-   **sp_MSins_\<** *tablename* **>** , que trata de inserções.  
  
-   **sp_MSupd_\<** *tablename* **>** , que trata de atualizações.  
  
-   **sp_MSdel_\<** *tablename* **>** , que trata de exclusões.  
  
 O **\<**_tablename_**>** usado no procedimento depende de como o artigo foi adicionado à publicação e se o banco de dados de assinatura contém uma tabela do mesmo nome com um proprietário diferente.  
  
 Qualquer um desses procedimentos pode ser substituído com um procedimento personalizado que você especifica ao adicionar um artigo a uma publicação. Os procedimentos personalizados são usados se um aplicativo requerer lógica personalizada, como inserir dados em uma tabela de auditoria quando uma linha é atualizada em um Assinante. Para obter mais informações sobre como especificar procedimentos armazenados personalizados, consulte os tópicos de instruções relacionados acima.  
  
 Se você especificar os procedimentos de replicação ou procedimentos personalizados, você especificará também a sintaxe de chamada para cada procedimento (a replicação seleciona padrões se você utilizar os procedimentos padrão). A sintaxe de chamada determina a estrutura dos parâmetros fornecidos para o procedimento e quanta informação é enviada ao Assinante com cada alteração de dados. Para obter mais informações, consulte a seção "Sintaxe de chamada de procedimentos armazenados" neste tópico.  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>Considerações ao usar procedimentos armazenados personalizados  
 Lembre-se das seguintes considerações ao usar procedimentos armazenados personalizados:  
  
-   Você deve oferecer suporte à lógica do procedimento armazenado; [!INCLUDE[msCoName](../../../includes/msconame-md.md)] não oferece suporte à lógica personalizada.  
  
-   Para evitar conflitos com as transações usadas pela replicação, transações explícitas não devem ser usadas em procedimentos personalizados.  
  
-   O esquema no Assinante é geralmente idêntico ao esquema do Publicador, mas pode também ser um subconjunto do esquema do Publicador se for usado filtragem de coluna. Porém, se você precisar transformar o esquema assim que os dados forem removidos de modo que o esquema do Assinante não seja um subconjunto do esquema do Publicador, o [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] é a solução recomendada. Para obter mais informações, consulte [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md).  
  
-   Se você fizer alterações de esquema a uma tabela publicada, os procedimentos personalizados devem ser regenerados. Para obter mais informações, consulte [Regenerar os procedimentos transacionais personalizados para refletir alterações de esquema](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
-   Se você usar um valor maior do que 1 para o parâmetro **-SubscriptionStreams** do Agente de Distribuição, você deverá se assegurar de que as atualizações nas colunas de chave primária tiveram êxito. Por exemplo:  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     Se o Agente de Distribuição usar mais de uma conexão, estas duas atualizações poderão ser replicadas em conexões diferentes. Se a atualização 1 for aplicada primeiro, não haverá problema; se a atualização 2 for aplicada primeiro ela retornará '0 linhas afetadas' porque a atualização 1 ainda não ocorreu. Essa situação é tratada nos procedimentos padrão ao gerar um erro se nenhuma linha for afetada na atualização:  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     Elevar o erro forçará o Agente de Distribuição a tentar novamente as atualizações em uma única conexão, que terá sucesso. Procedimentos armazenados personalizados devem incluir lógica semelhante.  
  
### <a name="call-syntax-for-stored-procedures"></a>Sintaxe de chamada para procedimentos armazenados  
 Há cinco opções para a sintaxe usada para chamar os procedimentos usados por replicação transacional:  
  
-   Sintaxe CALL. Pode ser usada para inserções, atualizações e exclusões. Por padrão, a replicação usa esta sintaxe para inserções e exclusões.  
  
-   Sintaxe SCALL. Só pode ser usada para atualizações. Por padrão, a replicação usa esta sintaxe para atualizações.  
  
-   Sintaxe MCALL. Só pode ser usada para atualizações.  
  
-   Sintaxe XCALL. Pode ser usada para atualizações e exclusões.  
  
-   VCALL. Usado para assinaturas atualizáveis. Somente para uso interno.  
  
 Cada método difere na quantia de dados que é propagada ao Assinante. Por exemplo, SCALL só passa valores para as colunas que são atualmente afetadas por uma atualização. Ao contrário, XCALL requer todas as colunas (sejam ou não afetadas por uma atualização) e todos os valores de dados antigos para cada coluna. Em muitos casos, SCALL é apropriado para atualizações, mas se o seu aplicativo requer todos os valores de dados durante uma atualização, XCALL permite isso.  
  
#### <a name="call-syntax"></a>Sintaxe CALL  
 Procedimentos armazenados de INSERT  
 Procedimentos armazenados que controlam instruções INSERT receberão os valores inseridos para todas as colunas:  
  
```  
c1, c2, c3,... cn  
```  
  
 Procedimentos armazenados de UPDATE  
 Procedimentos armazenados que controlam instruções UPDATE receberão valores atualizados para todas as colunas definidas no artigo, seguidos pelos valores originais para as colunas de chave primárias (não é feita nenhuma tentativa para determinar quais as colunas que foram alteradas.):  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 Procedimentos armazenados de DELETE  
 Procedimentos armazenados que controlam instruções DELETE receberão valores das colunas de chave primária:  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>Sintaxe SCALL  
 Procedimentos armazenados de UPDATE  
 Procedimentos armazenados que controlam instruções UPDATE receberão valores atualizados apenas para as colunas que foram alteradas, seguidos pelos valores originais para as colunas de chave primária, seguidos por um parâmetro (**binary(n)** ) bitmask que indica as colunas alteradas. No exemplo seguinte, a coluna 2 (c2) não foi alterada:  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>Sintaxe MCALL  
 Procedimentos armazenados de UPDATE  
 Procedimentos armazenados que controlam instruções UPDATE receberão valores atualizados para todas as colunas definidas no artigo, seguidos pelos valores originais para as colunas de chave primária, seguidos por um parâmetro (**binary(n)** ) bitmask que indica as colunas alteradas.  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>Sintaxe XCALL  
 Procedimentos armazenados de UPDATE  
 Procedimentos armazenados que controlam instruções UPDATE receberão os valores originais (a imagem anterior) para todas as colunas definidas no artigo, seguidos pelos valores atualizados (a imagem posterior) para todas as colunas definidas no artigo:  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 Procedimentos armazenados de DELETE  
 Procedimentos armazenados que controlam instruções DELETE receberão os valores originais (a imagem anterior) para todas as colunas definidas no artigo:  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  Ao usar XCALL, os valores da imagem anterior para **texto** e colunas de **imagem** são esperados para ser NULL.  
  
## <a name="examples"></a>Exemplos  
 Os procedimentos a seguir são os procedimentos padrão criados para a `Vendor Table` no banco de dados de exemplo [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] .  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  

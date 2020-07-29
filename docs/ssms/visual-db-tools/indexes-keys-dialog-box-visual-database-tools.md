---
title: Índices – caixa de diálogo Chaves
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65539
- vdt.ppg.indexeskeys
ms.assetid: 9e4060ba-80c3-468f-bccb-e12e99f672c2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: f251517d488324028af33e2749955cbb91c1193e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85980561"
---
# <a name="indexes---keys-dialog-box-visual-database-tools"></a>Caixa de diálogo Índices – Chaves (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Use essa caixa de diálogo para criar ou modificar índices, chaves primárias e chaves exclusivas. Para acessar essa caixa de diálogo, abra a definição da tabela com o índice ou chave; clique com o botão direito do mouse na grade de definição da tabela e depois clique em **Índices/Chaves**.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
**Índice ou Chave Exclusiva/Primária Selecionada**  
Lista os índices e as chaves primárias/exclusivas existentes. Selecione um para mostrar suas propriedades à direita da grade. Se a lista estiver vazia, nenhum terá sido definido para a tabela.  
  
**Adicionar**  
Crie um novo índice ou chave primária ou exclusiva.  
  
**Delete (excluir)**  
Exclua a chave ou o índice selecionado na lista **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
**Categoria Geral**  
Quando expandida, mostra as propriedades de **Colunas**, **É Exclusivo**e **Tipo**.  
  
**Colunas**  
Lista as ordens de classificação escolhidas para as colunas na chave ou índice e fornece acesso a uma caixa de diálogo em que as ordens de classificação podem ser definidas. Para exibir a caixa de diálogo, clique em **Colunas** e depois clique no botão de reticências (...) que aparece à direita do campo de propriedade.  
  
**É Exclusivo**  
Indica se os dados digitados no índice ou na chave precisam ser exclusivos. Não está disponível em índices XML.  
  
**Tipo**  
Especifique se o item selecionado na lista **Índice ou Chave Exclusiva/Primária Selecionada** é uma chave exclusiva, chave primária ou um índice. Nas chaves primárias, esse campo é somente leitura.  
  
**Categoria de identidade**  
Quando expandida, mostra os campos de propriedade de **Nome** e **Descrição**.  
  
**Nome**  
Mostra o nome da chave ou índice. Quando um novo índice é criado ele recebe um nome padrão com base na tabela da janela ativa no Designer de tabelas. É possível alterar o nome a qualquer momento.  
  
**Descrição**  
Fornece um local para a descrição da chave ou do índice. Para escrever uma descrição mais detalhada, clique em **Descrição** e, em seguida, clique no botão de reticências ( **…** ) que aparece à direita do campo de propriedade. Isso criará uma área maior para a redação do texto.  
  
**Categoria do Designer de Tabelas**  
Quando expandida, mostra as informações para **Criar como Clusterizado**.  
  
**Criar como Clusterizado**  
Faça com que a chave ou índice fiquem clusterizados. Somente um índice clusterizado é permitido em uma tabela. Os dados de uma tabela são armazenados na ordem do índice clusterizado. Para obter mais informações, consulte [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md) e [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md).  
  
**Especificação de Espaço de Dados**  
Quando expandida, mostra informações de **(Tipo de Espaço de Dados)** , **Grupo de arquivos ou Nome de esquema de partição**e **Lista de Colunas da Partição**.  
  
**(Tipo de Espaço de Dados)**  
Indica se o índice ou a chave pertence a um grupo de arquivo ou esquema de partição.  
  
**Grupo de arquivos ou Nome de esquema de partição**  
Mostra o nome do grupo de arquivos ou esquema de partição em que é armazenado.  
  
**Lista de Colunas da Partição**  
Exibe uma lista de colunas separada por vírgulas que integram a função da coluna de partição. Indisponível se o grupo de arquivos for selecionado no campo **(Tipo de Espaço de Dados)** .  
  
**Especificação de preenchimento**  
Quando expandido, mostra informações de **Fator de Preenchimento** e **Preenchimento de índice**.  
  
**Fator de Preenchimento**  
Especifica qual percentual de páginas do nível folha do índice o sistema poderá preencher. Após o preenchimento da página, o sistema precisará dividir as páginas para adicionar novos dados, comprometendo o desempenho.  
  
-   Um valor de 100 significa que as páginas serão preenchidas. Isso demandará o menor espaço de armazenamento. Essa configuração só deverá usada quando não houver alterações de dados; por exemplo, em uma tabela somente leitura.  
  
-   Um valor inferior deixa mais espaço vazio nas páginas de dados. Isso reduz a necessidade de dividir páginas de dados à medida que os índices crescem, mas requer mais espaço de armazenamento.  
  
**Preenchimento de índice**  
Indica se o mesmo percentual de espaço vazio (preenchimento) especificado em **Fator de Preenchimento** é fornecido às páginas intermediárias do índice quando elas aumentarem.  
  
**Ignorar Chaves Duplicadas**  
Especifica o que acontece quando uma linha é inserida durante uma operação de inserção em massa, cujo valor de chave é igual a um valor de chave existente. Se você escolher:  
  
-   **Sim** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitirá um aviso, ignorará a norma de linha de entrada e tentará inserir as linhas restantes.  
  
-   **Não** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitirá uma mensagem de erro e reverterá toda a operação BULK INSERT.  
  
**Colunas Incluídas**  
Exibe uma lista com os nomes de todas as colunas, separada por vírgulas, que compõem a chave de índice. As colunas de subchaves só podem ser especificadas para índices não clusterizados. Essa propriedade é oculta aos índices XML.  
  
**Está Desabilitado**  
Indica se o índice está desabilitado. Trata-se de uma propriedade somente leitura. Essa propriedade só será definida como **Sim** quando o índice tiver sido desabilitado no Visual Database Tools.  
  
**É Chave de Texto Completo**  
Especifique se esse índice é de chave de texto completo. Para obter mais informações sobre chaves de texto completo, consulte os Manuais Online do SQL Server. Essa propriedade é oculta aos índices XML.  
  
**Bloqueios de página permitidos**  
Especifica se o bloqueio de página é permitido no índice. A permissão ou não dos bloqueios de página afeta o desempenho do banco de dados. A configuração recomendada é **Sim**.  
  
**Recalcular estatísticas**  
Especifique se o [!INCLUDE[ssDE](../../includes/ssde_md.md)] subjacente deve calcular novas estatísticas quando o índice é criado. O recálculo das estatísticas retarda a criação de índices, mas certamente aprimora o desempenho da consulta.  
  
**Bloqueios de Linha Permitidos**  
Especifica se o bloqueio de linha é permitido no índice. A permissão ou não dos bloqueios de linha afeta o desempenho do banco de dados. A configuração recomendada é **Sim**.  
  
## <a name="see-also"></a>Consulte Também  
[Trabalhando com restrições (https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Trabalhando com chaves (https://msdn.microsoft.com/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd)  
  

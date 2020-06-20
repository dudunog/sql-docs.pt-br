---
title: Escolher um idioma ao criar um índice de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b514820ad64cbf17df209cbda552e4c5182b75fc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997775"
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>Escolher um idioma ao criar um índice de texto completo
  Ao criar um índice de texto completo, você precisa especificar um idioma no nível de coluna para a coluna indexada. O [separador de palavras e os lematizadores](configure-and-manage-word-breakers-and-stemmers-for-search.md) do idioma especificado serão usados por consultas de texto completo na coluna. Há algumas coisas a considerar ao escolher o idioma da coluna ao criar um índice de texto completo. Essas considerações estão relacionadas a como seu texto é transformado em token e, depois, indexado pelo Mecanismo de Texto Completo.  
  
> [!NOTE]  
>  Para especificar um idioma no nível de coluna para uma coluna de índice de texto completo, use a cláusula LANGUAGE *language_term* ao especificar a coluna. Para obter mais informações, veja [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql) e [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql).  
  
##  <a name="language-support-in-full-text-search"></a><a name="langsupp"></a> Suporte de idioma na pesquisa de texto completo  
 Esta seção apresenta uma introdução aos separadores de palavras e lematizadores e discute como a pesquisa de texto completo usa o LCID do idioma no nível de coluna.  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>Introdução aos separadores de palavras e lematizadores  
 O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores incluem uma família nova completa de separadores de palavras e lematizadores, que são significativamente melhores do que os disponíveis antes no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  O MS NLG (Microsoft Natural Language Group) implementou e dá suporte a esses novos componentes linguísticos.  
  
 Os novos separadores de palavras proporcionam os seguintes benefícios:  
  
-   Robustez  
  
     Testes mostraram que os novos separadores de palavras são robustos em ambientes de consulta de alta pressão.  
  
-   Segurança  
  
     Os novos separadores de palavras são habilitados por padrão em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] graças aos aprimoramentos de segurança nos componentes lingüísticos. É altamente recomendável que componentes externos, como separadores de palavras e filtros, sejam assinados para melhorar a segurança geral e a robustez do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. É possível configurar a pesquisa de texto completo para verificar se esses componentes estão assinados, da seguinte forma:  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   Qualidade  
  
     Os separadores de palavras foram reformulados, e testes mostraram que os novos separadores de palavras proporcionam melhor qualidade semântica do que os anteriores. Isso aumenta a precisão da recuperação.  
  
-   Cobertura de uma lista extensa de idiomas e separadores de palavras que estão são incluídos no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prontos para uso e habilitados por padrão.  
  
 Para obter uma lista dos idiomas para os quais o inclui um separador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] palavras e lematizadores, consulte [sys. Fulltext_languages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  

  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>Como a pesquisa de texto completo usa o nome do idioma no nível de coluna  
 Ao criar um índice de texto completo, você precisa especificar um nome de idioma válido para cada coluna. Se um nome de idioma for válido, mas não for retornado pela exibição de catálogo [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) , a pesquisa de texto completo reverterá para o nome de idioma mais próximo disponível da mesma família de idiomas, se houver. Caso contrário, a pesquisa de texto completo reverterá para o separador de palavras Neutro. Esse comportamento de reversão poderá afetar a precisão da recuperação. Portanto, é altamente recomendável especificar um nome de idioma válido e disponível para cada coluna quando você criar um índice de texto completo.  
  
> [!NOTE]  
>  O LCID é usado em todos os tipos de dados qualificados para indexação de texto completo (como `char` ou `nchar`). Se você tiver a ordem de classificação de um tipo de coluna e a ordem de um tipo de coluna `char`, `varchar` ou `text` definido com uma configuração de idioma diferente do idioma identificado pelo LCID, o LCID será usado de qualquer forma durante a indexação de texto completo e a consulta dessas colunas.  
  

  
##  <a name="word-breaking"></a><a name="breaking"></a> Quebra de palavras  
 Um separador de palavras cria tokens do texto que está sendo indexado em limites de palavra, que são específicos de idioma. Por isso, o comportamento da separação de palavras é diferente entre diferentes idiomas. Se você usar o idioma x para indexar vários idiomas {x, y e ,z}, o comportamento de alguns deles poderá gerar resultados inesperados. Por exemplo, um traço (-) ou uma vírgula (,) pode ser um elemento de separação de palavras que será acionado em um idioma, mas não em outro. Além disso, pode ocorrer um comportamento de lematização raramente inesperado porque uma dada palavra pode ter um comportamento de lematização diferente em outro idioma. Por exemplo, no idioma inglês, os limites de palavras normalmente são espaços em branco ou alguma forma de pontuação. Em outros idiomas, como no alemão, palavras ou caracteres podem ser combinados. Portanto, o idioma no nível de coluna escolhido deve representar o idioma que você espera que será armazenado em linhas dessa coluna.  
  
### <a name="western-languages"></a>Idiomas ocidentais  
 No caso da família de idiomas ocidentais, se você não tiver certeza de quais idiomas serão armazenados em uma coluna ou se espera que mais de um seja armazenado, uma alternativa é usar um separador de palavras para o idioma mais complexo que poderá ser armazenado na coluna. Por exemplo, talvez você espere armazenar conteúdo em inglês, espanhol e alemão em uma única coluna. Esses três idiomas ocidentais têm padrões do separação de palavras muito parecidos, sendo que os padrões do alemão são os mais complexos. Por isso, uma boa opção nesse caso seria usar o separador de palavras do idioma alemão, que deverá poder processar os textos em inglês e espanhol corretamente. Por outro lado, o separador de palavras do inglês pode não processar textos em alemão perfeitamente por causa das palavras compostas do idioma.  
  
 Observe que o uso do separador de palavras do idioma mais complexo de uma família de idiomas não garante a indexação perfeita de todos os idiomas da família. Pode haver situações específicas nas quais o separador de palavras mais complexo não pode lidar corretamente com textos escritos em outro idioma.  
  

  
### <a name="non-western-languages"></a>Idiomas não ocidentais  
 Em idiomas não ocidentais (como chinês, japonês, hindu, entre outros), a solução alternativa acima não funcionará necessariamente, por motivos linguísticos. Para idiomas não ocidentais, considere uma das seguintes alternativas:  
  
-   Para idiomas de famílias diferentes  
  
     Se uma coluna tiver de conter idiomas drasticamente diferentes, como espanhol e japonês, considere armazenar o conteúdo de idiomas diferentes em colunas separadas. Isso lhe permitiria usar o separador de palavras específico de idioma para cada coluna. Se você escolher essa solução e não souber qual é o idioma de consulta quando fizer a consulta, talvez precise emitir a consulta nas colunas para garantir que ela encontre a linha ou o documento certo.  
  
-   Para conteúdo binário (como documentos do Microsoft Word)  
  
     Quando o conteúdo indexado for do tipo `binary`, o filtro da pesquisa de texto completo que processa o conteúdo textual antes de enviá-lo para o separador de palavras poderá respeitar as marcas do idioma específico dentro do arquivo binário. Nesse caso, no momento da indexação, o filtro emitirá o LCID correto para um documento ou uma seção de um documento. O Mecanismo de Texto Completo chamará o separador de palavras para o idioma com esse LCID. Porém, após a indexação de conteúdo em vários idiomas, é recomendável verificar se o conteúdo foi indexado corretamente.  
  
-   Para conteúdo em texto sem-formatação  
  
     Quando o conteúdo é um texto sem-formatação, você pode convertê-lo para o tipo de dados `xml` e adicionar marcas de idioma que indiquem o idioma correspondente para cada documento ou seção de documento. No entanto, para que isso funcione, você deve saber qual é o idioma antes de executar a indexação de texto completo.  
  

  
##  <a name="stemming"></a><a name="stemming"></a> Lematização  
 Outro aspecto que você deve levar em consideração quando escolher o idioma no nível de coluna é a lematização. Em consultas de texto completo,*lematização* é o processo de procurar todas as formas lematizadas (flexivas) de uma palavra em determinado idioma. Quando você usa um separador de palavras genérico para processar vários idiomas, o processo de lematização só funcionará para o idioma especificado para a coluna, e não para os outros idiomas da coluna. Por exemplo, os lematizados de alemão não funcionam para inglês ou espanhol (e assim por diante). Isso poderia afetar a recuperação, dependendo do idioma escolhido no momento da consulta.  
  

  
##  <a name="effect-of-column-type-on-full-text-search"></a><a name="type"></a> Efeito do tipo de coluna na pesquisa de texto completo  
 Outro aspecto a ser considerado na escolha do idioma está relacionada a como os dados são representados. Para dados que não são armazenados na coluna `varbinary(max)`, nenhuma filtragem especial é executada. Em vez disso, o texto geralmente é passado pelo separador de palavras assim como é.  
  
 Além disso, os separadores de palavra foram criados principalmente para processar texto escrito. Então, se você tiver algum tipo de formatação em seu texto (como HTML), não será possível obter grande precisão linguística durante a indexação e procura. Nesse caso, você tem duas opções: o método preferencial é simplesmente armazenar os dados de texto na `varbinary(max)` coluna e indicar seu tipo de documento para que ele possa ser filtrado. Se não houver essa opção, você poderá considerar a possibilidade de usar o separador de palavras neutro e, se possível, adicionar dados de marcação (como ‘br’ em HTML) à lista de palavras de ruído.  
  
> [!NOTE]  
>  A lematização com base no idioma não entra em jogo quando você especifica o idioma neutro.  
  

  
##  <a name="specifying-a-non-default-column-level-language-in-a-full-text-query"></a><a name="nondef"></a> Especificando um idioma em nível de coluna não padrão em uma consulta de texto completo  
 Por padrão, no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a pesquisa de texto completo analisará os termos da consulta usando o idioma especificado para cada coluna incluída na cláusula de texto completo. Para ignorar esse comportamento, especifique um idioma não padrão no momento da consulta. Para os idiomas com suporte cujos recursos estão instalados, a cláusula *language_term* de LANGUAGE de uma consulta [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)ou [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) pode ser usada para especificar o idioma utilizado para separação de palavras, lematização, dicionário de sinônimos e processamento de palavra irrelevante (stop word) dos termos da consulta.  
  

  
## <a name="see-also"></a>Consulte Também  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Configurar e gerenciar filtros para pesquisa](configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  

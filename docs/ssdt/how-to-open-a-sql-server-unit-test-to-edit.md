---
title: Abrir um teste de unidade do SQL Server para edição
description: Saiba como editar um teste de unidade de SQL Server para que você possa adicionar funcionalidades ou personalizar condições. Confira diferentes maneiras de abrir o arquivo de código-fonte do teste.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: c6af1b12-54cd-42f9-b2ef-7164f8078323
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 8ed1f08f02b22aabc85a18068b5bbbe02b5a7ee9
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987945"
---
# <a name="how-to-open-a-sql-server-unit-test-to-edit"></a>Como fazer: Abrir um teste de unidade do SQL Server para edição

Após criar um teste de unidade do SQL Server, use o **Designer de Teste de Unidade do SQL Server** para adicionar instruções Transact\-SQL e condições de teste. Os testes criados por meio do designer geram código do Visual C# ou do Visual Basic. Esse é código executado quando o teste é executado.  
  
Se você estiver satisfeito com seu teste, execute-o dessa forma. Se você quiser adicionar mais funcionalidade a esse teste de unidade, edite o código. Esse código reside em um arquivo .cs ou .vb no projeto de teste. Para saber mais, confira [Arquivos de teste de unidade SQL Server](../ssdt/sql-server-unit-test-files.md). Você também pode personalizar os testes criando novas condições de teste. Para obter mais informações, confira [Como Criar condições de teste para o Designer de teste de unidade de banco de dados (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/aa833409(v=vs.100)).  
  
> [!NOTE]  
> Se você excluir um método de teste editando o arquivo .cs ou .vb, o método de teste ainda aparecerá no **Designer de Teste de Unidade do SQL Server**. Isso acontece porque o método InitializeComponent da classe de teste ainda contém variáveis de membro para esse teste. Embora o teste seja exibido no designer, você não poderá executá-lo porque seu código não está mais presente. Para regenerar o método de teste em questão, edite o Transact\-SQL no editor e salve o arquivo de teste .cs ou .vb ou recompile o projeto de teste.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-solution-explorer"></a>Para abrir o arquivo do código-fonte de um teste de unidade do SQL Server no Gerenciador de Soluções  
  
-   No **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo do código-fonte que contém o teste de unidade do SQL Server e clique em **Exibir Código**.  
  
    O método do teste de unidade aparece na janela de edição principal do Visual Studio quando o arquivo é aberto.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2010"></a>Para abrir o arquivo do código-fonte de um teste de unidade do SQL Server na janela Modo de Teste (Visual Studio 2010)  
  
1.  Execute um teste de unidade. Para obter mais informações, veja a seção "Executar testes de unidade do SQL Server" no [Passo a passo: Criar e Executar um Teste de Unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md).  
  
2.  Na janela Modo de Teste, clique com o botão direito do mouse no teste e clique em **Abrir Teste**.  
  
    O método do teste de unidade aparece na janela de edição principal do Visual Studio quando o arquivo é aberto.  
  
### <a name="to-open-the-source-code-file-of-a-sql-server-unit-test-from-the-test-view-window-visual-studio-2012"></a>Para abrir o arquivo do código-fonte de um teste de unidade do SQL Server na janela Modo de Teste (Visual Studio 2012)  
  
1.  Execute um teste de unidade. Para obter mais informações, veja a seção "Executar testes de unidade do SQL Server" no [Passo a passo: Criar e Executar um Teste de Unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md).  
  
2.  Na janela Gerenciador de Testes, clique no nome do arquivo do código-fonte do teste de unidade.  
  
    O método do teste de unidade aparece na janela de edição principal do Visual Studio quando o arquivo é aberto.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  

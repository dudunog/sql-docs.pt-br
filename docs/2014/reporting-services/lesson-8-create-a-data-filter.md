---
title: 'Lição 8: Criar um filtro de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5204cab43e3c801acf80113ec92c51e00c0f9d13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108386"
---
# <a name="lesson-8-create-a-data-filter"></a>Lição 8: Criar um filtro de dados
  Após adicionar uma ação de detalhamento no relatório pai, a próxima etapa é criar um filtro de dados para a tabela de dados definida para o relatório filho.  
  
 Você pode criar um filtro baseado em tabela **ou** um filtro de consulta para o relatório de detalhamento. Esta lição fornece instruções para ambas as opções.  
  
## <a name="table-based-filter"></a>Filtro baseado em tabela  
 É necessário concluir as seguintes tarefas para implementar um filtro baseado em tabela.  
  
-   Adicione uma expressão de filtro ao tablix no relatório filho.  
  
-   Crie uma função que seleciona dados não filtrados na tabela `PurchaseOrderDetail`.  
  
-   Adicione um manipulador de eventos que associe a DataTable `PurchaseOrderDetail` ao relatório filho.  
  
#### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>Para adicionar uma expressão de filtro ao tablix no relatório filho  
  
1.  Abra o relatório filho.  
  
2.  Selecione um título de coluna no Tablix, clique com o botão direito do mouse na célula cinza que aparece acima do título da coluna e clique em **Propriedades do Tablix**.  
  
3.  Clique na página **filtros** e, em seguida, clique em **Adicionar**.  
  
4.  Na **expressão** registrada, clique `ProductID` na lista suspensa. Esta é a coluna à qual você aplicará o filtro.  
  
5.  Clique no operador EQUAL**=**() na lista suspensa **operador** .  
  
6.  Clique no botão de expressão ao lado do campo **valor** , clique em **parâmetros** na área **categoria** e clique `productid` duas vezes na área **valores** . O campo **Definir expressão para: Valor** agora deve conter uma expressão semelhante a **=Parameters!productid.Value**.  
  
7.  Clique em **OK** e em **OK** novamente na caixa de diálogo **Propriedades do Tablix** .  
  
8.  Salve o arquivo .rdlc.  
  
#### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>Para criar uma função que seleciona dados não filtrados na tabela PurchaseOrdeDetail.  
  
1.  No Gerenciador de Soluções, expanda Default.aspx e clique duas vezes em Default.aspx.cs.  
  
2.  Crie uma nova função que aceite um parâmetro, `productid`, do tipo inteiro, retorne `datatable` um objeto e faça o seguinte.  
  
    1.  Cria uma instância do conjunto de dados `DataSet2`,, que foi criada na etapa 2 da [lição 4: definir uma conexão de dados e uma data Table para o relatório filho](lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Crie uma conexão com o banco de dados SQL Server para executar a consulta definida na **Lição 4: Definir uma conexão de dados e uma DataTable para o relatório filho**.  
  
    3.  A consulta deve retornará dados não filtrados.  
  
    4.  Preencha a instância do DataSet com os dados não filtrados executando a consulta.  
  
    5.  Retorne a DataTable `PurchaseOrderDetail`.  
  
         A função terá aparência similar à mostrada abaixo (Isso é apenas para fins de referência. Você pode seguir o padrão desejado para buscar os dados necessários ao relatório filho).  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>Para adicionar um manipulador de eventos que associe a DataTable PurchaseOrderDetail ao relatório filho.  
  
1.  Abra o Default.aspx  
  
2.  Clique com o botão direito do mouse no controle ReportViewer e clique em **Propriedades.**  
  
3.  Na página **Propriedades** , clique no ícone **eventos** .  
  
4.  Clique duas vezes no evento de **detalhamento** .  
  
     Isso adicionará uma seção do manipulador de eventos ao código, que será semelhante ao bloco abaixo.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Conclua o manipulador de eventos. Ela deve incluir a funcionalidade a seguir.  
  
    1.  Busque a referência de objeto do relatório filho no parâmetro *DrillthroughEventArgs* .  
  
    2.  Chame a função,`GetPurchaseOrderDetail`  
  
    3.  Associe a DataTable `PurchaseOrderDetail` à fonte de dados correspondente do relatório.  
  
         O código completo do manipulador de eventos será semelhante ao conteúdo seguinte.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salve o arquivo.  
  
## <a name="query-filter"></a>Filtro de consulta  
 É necessário concluir as seguintes tarefas para implementar um filtro de consulta.  
  
-   Crie uma função que tenha selecionado dados filtrados na tabela `PurchaseOrderDetail`.  
  
-   Adicione um manipulador de eventos que recupere valores de parâmetro e associe a DataTable `PurchaseOrdeDetail` ao relatório filho.  
  
#### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>Para criar uma função que selecione dados filtrados na tabela PurchaseOrderDetail  
  
1.  No Gerenciador de Soluções, expanda Default.aspx e clique duas vezes em Default.aspx.cs.  
  
2.  Crie uma nova função que aceite um parâmetro, `productid`, do tipo inteiro e retorne um objeto `datatable`, e faça o seguinte.  
  
    1.  Cria uma instância do conjunto de dados `DataSet2`,, que foi criada na etapa 2 da [lição 4: definir uma conexão de dados e uma data Table para o relatório filho](lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Crie uma conexão com o banco de dados SQL Server para executar a consulta definida na **Lição 4: Definir uma conexão de dados e uma DataTable para o relatório filho**.  
  
    3.  A consulta incluirá um parâmetro, `productid`, assegurar que os dados retornados serão filtrados com base na `ProductID` selecionada no relatório pai.  
  
    4.  Preencha a instância do DataSet com os dados filtrados executando a consulta.  
  
    5.  Retorne a DataTable `PurchaseOrderDetail`.  
  
         A função terá aparência similar à mostrada abaixo (Isso é apenas para fins de referência. Você pode seguir o padrão desejado para buscar os dados necessários ao relatório filho).  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = " + productid, sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>Para adicionar um manipulador de eventos que recupere valores de parâmetro e associe a DataTable PurchaseOrdeDetail ao relatório filho  
  
1.  Abra o Default.aspx  
  
2.  Clique com o botão direito do mouse no controle ReportViewer e clique em **Propriedades**.  
  
3.  No painel **Propriedades** , clique no ícone **eventos** .  
  
4.  Clique duas vezes no evento de **detalhamento** .  
  
     Isso adicionará uma seção do manipulador de eventos ao código, que será semelhante ao conteúdo abaixo.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Conclua o manipulador de eventos. Ele deve incluir a seguinte funcionalidade.  
  
    1.  Busque a referência de objeto do relatório filho no parâmetro *DrillthroughEventArgs* .  
  
    2.  Obtenha a lista de parâmetros do relatório filho no objeto do relatório filho buscado.  
  
    3.  Itere pela coleção do parâmetro e recupere o valor do parâmetro `ProductID` passado pelo relatório pai.  
  
    4.  Chame a função `GetPurchaseOrderDetail` e passe o valor para o parâmetro `ProductID`.  
  
    5.  Associar a `PurchaseOrderDetail` DataTable à fonte de dados correspondente do relatório.  
  
         O código completo do manipulador de eventos será semelhante ao conteúdo seguinte.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salve o arquivo.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou, com êxito, um filtro de dados para a tabela de dados definida para o relatório filho. Em seguida, você compilará e executará o aplicativo de site.  
  
  

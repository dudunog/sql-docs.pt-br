---
title: Representação do indicador chave de desempenho (tabular) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 8d3d949e-5d43-4d2e-9dc8-48d182a7a935
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7cc9ec7e6ccae664a6f608c350483ae9744fb49d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940017"
---
# <a name="key-performance-indicator-representation-tabular"></a>Representação de indicador chave de desempenho (de tabela)
  Um KPI é usado para medir o desempenho de um valor, definido por uma medida base, em relação a um valor de destino  
  
## <a name="key-performance-indicator-representation"></a>Representação de indicador chave de desempenho  
 Em modelos de objeto de tabela, um indicador chave de desempenho-KPI-é uma medida com informações adicionais para o aplicativo cliente exibi-lo graficamente. Um kpi normalmente tem informações sobre uma meta a ser obtida, o status da medida comparada à meta e informações para a ferramenta de cliente sobre como exibir o status graficamente.  
  
### <a name="key-performance-indicator-in-amo"></a>Indicador chave de desempenho no AMO  
 Ao usar o AMO para gerenciar um kpi de modelo de tabela, não há nenhuma correspondência de objeto um para um para um kpi no AMO, o objeto de AMO <xref:Microsoft.AnalysisServices.Kpi>não é usado para este propósito; no AMO, para modelos de tabela, um kpi é representado por uma série de objetos criada em um dos elementos na coleção <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e no <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>.  
  
 O snippet de código a seguir mostra como criar uma de muitas possíveis definições de kpi.  
  
```  
  
private void addStaticKPI(object sender, EventArgs e)  
{  
    double KPIGoal = 0, status1ThresholdValue = 0, status2ThresholdValue = 0  
        , redAreaValue = 0, yellowAreaValue = 0, greenAreaValue = 0;  
    string clientStatusGraphicImageName = "Three Circles Colored";  
  
    //Verify input requirements  
    //Goal values  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        if (string.IsNullOrEmpty(staticTargetKPIGoal.Text)  
            || string.IsNullOrWhiteSpace(staticTargetKPIGoal.Text)  
            || !double.TryParse(staticTargetKPIGoal.Text, out KPIGoal))  
        {  
            MessageBox.Show(String.Format("Static Goal is not defined or is not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
            return;  
        }  
    }  
    else  
    {//Measure KPI Goal selected  
        if (!TargetMeasureForKPISelected)  
        {  
            MessageBox.Show(String.Format("Measure Goal is not selected."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
            return;  
        }  
    }  
  
    //Status  
    if (string.IsNullOrEmpty(firstStatusThresholdValue.Text)  
        || string.IsNullOrWhiteSpace(firstStatusThresholdValue.Text)  
        || !double.TryParse(firstStatusThresholdValue.Text, out status1ThresholdValue)  
        || string.IsNullOrEmpty(secondStatusThresholdValue.Text)  
        || string.IsNullOrWhiteSpace(secondStatusThresholdValue.Text)  
        || !double.TryParse(secondStatusThresholdValue.Text, out status2ThresholdValue))  
    {  
        MessageBox.Show(String.Format("Status Threshold are not defined or they are not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (string.IsNullOrEmpty(statusValueRedArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueRedArea.Text)  
        || !double.TryParse(statusValueRedArea.Text, out redAreaValue)  
        || string.IsNullOrEmpty(statusValueYellowArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueYellowArea.Text)  
        || !double.TryParse(statusValueYellowArea.Text, out yellowAreaValue)  
        || string.IsNullOrEmpty(statusValueGreenArea.Text)  
        || string.IsNullOrWhiteSpace(statusValueGreenArea.Text)  
        || !double.TryParse(statusValueGreenArea.Text, out greenAreaValue))  
    {  
        MessageBox.Show(String.Format("Status Area values are not defined or they are not a valid number."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    //Set working variables  
    string kpiTableName = ((DataRowView)MeasuresInModelList.CheckedItems[0])[0].ToString();  
    string kpiMeasureName = ((DataRowView)MeasuresInModelList.CheckedItems[0])[1].ToString();  
  
    //Verify if KPI is already defined  
    if (modelCube.MdxScripts["MdxScript"].CalculationProperties.Contains(string.Format("KPIs.[{0}]", kpiMeasureName)))  
    {  
        //ToDo: Verify with the user if wants to update KPI or exit  
        //If user wants to update then remove KPI from mdxScripts and continue with the creating the KPI  
        //  
        // Until the code to remove KPI is finished we'll have to exit with a message of no duplicated KPIs are allowed  
        MessageBox.Show(String.Format("Another KPI exists for the same measeure."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    StringBuilder kpiCommand = new StringBuilder();  
  
    AMO.MdxScript mdxScript = modelCube.MdxScripts["MdxScript"];  
    kpiCommand.Append(mdxScript.Commands[1].Text);  
  
    string goalExpression;  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        goalExpression = KPIGoal.ToString();  
    }  
    else  
    {//Measure KPI Goal selected  
        string measureGoalMeasureName = ((DataRowView)KpiTargetMeasures.CheckedItems[0])[1].ToString();  
        goalExpression = string.Format("[Measures].[{0}]", measureGoalMeasureName);  
    }  
  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Goal] AS '{2}', ASSOCIATED_MEASURE_GROUP = '{0}';"  
            , kpiTableName, kpiMeasureName, goalExpression));  
  
    string statusExpression;  
    if (staticTargetKPI.Checked)  
    {//Static KPI Goal selected  
        statusExpression = string.Format("KpiValue(\"{0}\")", kpiMeasureName).Trim();  
    }  
    else  
    {//Measure KPI Goal selected  
        string measureGoalMeasureName = ((DataRowView)KpiTargetMeasures.CheckedItems[0])[1].ToString().Trim();  
  
        string M = string.Format("[Measures].[{0}]", kpiMeasureName);  
        string T = string.Format("[Measures].[{0}]", measureGoalMeasureName);  
  
        if (KpiRelationDifference.Checked)  
        {  
            statusExpression = string.Format("{1} - {0}", M, T);  
        }  
        else  
        {  
            if (KpiRelationRatioMT.Checked)  
            {  
                statusExpression = string.Format("{0} / {1}", M, T);  
            }  
            else  
            {  
                statusExpression = string.Format("{1} / {0}", M, T);  
            }  
        }  
    }  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Status] "  
                                              + " AS 'Case When IsEmpty({9}) Then Null "  
                                                       + " When ({9}) {2} {3} Then {4} "  
                                                       + " When ({9}) {5} {6} Then {7} "  
                                                       + " Else {8} End'"  
                                              + ", ASSOCIATED_MEASURE_GROUP = '{0}';"  
        , kpiTableName, kpiMeasureName // 0, 1  
        , statusThreshold1ComparisonOperator.Text, status1ThresholdValue, redAreaValue // 2, 3, 4  
        , statusThreshold2ComparisonOperator.Text, status2ThresholdValue, yellowAreaValue, greenAreaValue // 5, 6, 7, 8  
        , statusExpression // 9  
        ));  
  
    kpiCommand.AppendLine(string.Format("CREATE MEMBER CURRENTCUBE.Measures.[_{1} Trend] AS '0', ASSOCIATED_MEASURE_GROUP = '{0}';"  
        , kpiTableName, kpiMeasureName));  
  
    kpiCommand.AppendLine(string.Format("CREATE KPI CURRENTCUBE.[{1}] AS Measures.[{1}]"  
                                               + ", ASSOCIATED_MEASURE_GROUP = '{0}'"  
                                               + ", GOAL = Measures.[_{1} Goal]"  
                                               + ", STATUS = Measures.[_{1} Status]"  
                                               + ", TREND = Measures.[_{1} Trend]"  
                                               + ", STATUS_GRAPHIC = '{2}'"  
                                               + ", TREND_GRAPHIC = '{2}';"  
        , kpiTableName, kpiMeasureName, clientStatusGraphicImageName));  
  
    {//Adding Calculation Reference for the Measure itself  
        if (!mdxScript.CalculationProperties.Contains(kpiMeasureName))  
        {  
            AMO.CalculationProperty cp = new AMO.CalculationProperty(kpiMeasureName, AMO.CalculationType.Member);  
            cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
            cp.Visible = true;  
            mdxScript.CalculationProperties.Add(cp);  
        }  
    }  
    {//Adding Calculation Reference for the Goal measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Goal]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the Status measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Status]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the Status measure  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("Measures.[_{0} Trend]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = false;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
  
    {//Adding Calculation Reference for the KPI  
        AMO.CalculationProperty cp = new AMO.CalculationProperty(string.Format("KPIs.[{0}]", kpiMeasureName), AMO.CalculationType.Member);  
        cp.FormatString = ""; // ToDo: Get formatting attributes for the member  
        cp.Visible = true;  
        mdxScript.CalculationProperties.Add(cp);  
    }  
    try  
    {                  
        newDatabase.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        MessageBox.Show(String.Format("KPI successfully defined."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
    }  
    catch (AMO.OperationException amoOperationException)  
    {  
        //ToDo: remove anything left in mdxScript up to the point where the exception was thrown  
        MessageBox.Show(String.Format("Error creating KPI for Measure '{0}'[{1}]\nError message: {2}", kpiTableName, kpiMeasureName, amoOperationException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
    }  
  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>Exemplo de AMO2Tabular  
 Para compreender como usar o AMO para criar e manipular representações de indicador chave de desempenho, consulte o código-fonte do exemplo AMO para Tabela; verifique especificamente o seguinte arquivo de origem: AddKPIs.cs. O exemplo está disponível no Codeplex. Uma nota importante sobre o código: o código é fornecido apenas como um suporte aos conceitos lógicos explicados aqui; ele não deve ser usado em um ambiente de produção, nem para fins que não sejam pedagógicos.  
  
  

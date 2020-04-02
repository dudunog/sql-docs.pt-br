---
title: Criando um componente de item de relatório personalizado em tempo de execução | Microsoft Docs
description: Saiba como criar um componente de runtime do item de relatório personalizado e como definir as propriedades desse componente no ambiente de design.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: b3e15a4a-98f8-4dbb-b847-bbcb20327051
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0946739b0b0aaefd1e0d6a682f0228dfa98529c9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216979"
---
# <a name="creating-a-custom-report-item-run-time-component"></a>Criando um componente de item de relatório personalizado em tempo de execução
  O componente de item de relatório personalizado em tempo de execução é implementado como um componente do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usando qualquer linguagem em conformidade com CLS e é chamado pelo processador de relatório em tempo de execução. Para definir as propriedades do componente em tempo de execução no ambiente de design, modifique o componente em tempo de design correspondente do item de relatório personalizado.  
  
 Para obter uma amostra de um item de relatório personalizado totalmente implementado, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="definition-and-instance-objects"></a>Objetos de definição e objetos de instância  
 Antes de implementar um item de relatório personalizado, é importante compreender a diferença entre *objetos de definição* e *objetos de instância*. Objetos de definição fornecem a representação de RDL do item de relatório personalizado, enquanto objetos de instância são as versões avaliadas dos objetos de definição. Há apenas um objeto de definição para cada item do relatório. Ao acessar propriedades em um objeto de definição contendo expressões, você obterá a cadeia de caracteres de expressão não avaliada. Os objetos de instância contêm as versões avaliadas dos objetos de definição e têm uma relação um-para-muitos com o objeto de definição de um item. Por exemplo, se um relatório tiver uma região de dados <xref:Microsoft.ReportingServices.OnDemandReportRendering.Tablix> que contém um <xref:Microsoft.ReportingServices.OnDemandReportRendering.CustomReportItem> na linha de detalhes, haverá apenas um objeto de definição, mas haverá um objeto de instância para cada linha da região de dados.  
  
## <a name="implementing-the-icustomreportitem-interface"></a>Implementando a interface ICustomReportItem  
 Para criar um componente em tempo de execução **CustomReportItem**, você precisará implementar a interface <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem> que é definida no Microsoft.ReportingServices.ProcessingCore.dll:  
  
```csharp  
namespace Microsoft.ReportingServices.OnDemandReportRendering  
{  
    public interface ICustomReportItem  
    {  
        void GenerateReportItemDefinition(CustomReportItem customReportItem);  
void EvaluateReportItemInstance(CustomReportItem customReportItem);  
    }  
}  
```  
  
 Depois que você implementar a interface <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem>, dois stubs de método serão gerados: <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> e <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A>. O método <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.GenerateReportItemDefinition%2A> é chamado primeiro e é usado para configurar propriedades de definição e criar o objeto <xref:Microsoft.ReportingServices.OnDemandReportRendering.Image> que conterá as propriedades de definição e de instância que são usadas para renderizar o item. O método <xref:Microsoft.ReportingServices.OnDemandReportRendering.ICustomReportItem.EvaluateReportItemInstance%2A> é chamado depois da avaliação dos objetos de definição, e ele fornece os objetos de instância que serão usados para renderizar o item.  
  
 Veja a seguir uma implementação de exemplo de um item de relatório personalizado que renderiza o nome do controle como uma imagem.  
  
```csharp  
namespace Microsoft.Samples.ReportingServices  
{  
    using System;  
    using System.Collections.Generic;  
    using System.Collections.Specialized;  
    using System.Drawing.Imaging;  
    using System.IO;  
    using System.Text;  
    using Microsoft.ReportingServices.OnDemandReportRendering;  
  
    public class PolygonsCustomReportItem : ICustomReportItem  
    {  
        #region ICustomReportItem Members  
  
        public void GenerateReportItemDefinition(CustomReportItem cri)  
        {  
            // Create the Image object that will be   
            // used to render the custom report item  
            cri.CreateCriImageDefinition();  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
        }  
  
        public void EvaluateReportItemInstance(CustomReportItem cri)  
        {  
            // Get the Image definition  
            Image polygonImage = (Image)cri.GeneratedReportItem;  
  
            // Create the image for the custom report item  
            polygonImage.ImageInstance.ImageData = DrawImage(cri);  
        }  
  
        #endregion  
  
        /// <summary>  
        /// Creates an image of the CustomReportItem's name  
        /// </summary>  
        private byte[] DrawImage(CustomReportItem customReportItem)  
        {  
            int width = 1;          // pixels  
            int height = 1;         // pixels  
            int resolution = 75;    // dpi  
  
            System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            System.Drawing.Graphics graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Get the Font for the Text  
            System.Drawing.Font font = new System.Drawing.Font(System.Drawing.FontFamily.GenericMonospace,  
                12, System.Drawing.FontStyle.Regular);  
  
            // Get the Brush for drawing the Text  
            System.Drawing.Brush brush = new System.Drawing.SolidBrush(System.Drawing.Color.LightGreen);  
  
            // Get the measurements for the image  
            System.Drawing.SizeF maxStringSize = graphics.MeasureString(customReportItem.Name, font);  
            width = (int)(maxStringSize.Width + 2 * font.GetHeight(resolution));  
            height = (int)(maxStringSize.Height + 2 * font.GetHeight(resolution));  
  
            bitmap.Dispose();  
            bitmap = new System.Drawing.Bitmap(width, height);  
            bitmap.SetResolution(resolution, resolution);  
  
            graphics.Dispose();  
            graphics = System.Drawing.Graphics.FromImage(bitmap);  
            graphics.PageUnit = System.Drawing.GraphicsUnit.Pixel;  
  
            // Draw the text  
            graphics.DrawString(customReportItem.Name, font, brush, font.GetHeight(resolution),   
                font.GetHeight(resolution));  
  
            // Create the byte array of the image data  
            MemoryStream memoryStream = new MemoryStream();  
            bitmap.Save(memoryStream, ImageFormat.Bmp);  
            memoryStream.Position = 0;  
            byte[] imageData = new byte[memoryStream.Length];  
            memoryStream.Read(imageData, 0, imageData.Length);  
  
            return imageData;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura de item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [Criando um componente de item de relatório personalizado em tempo de design](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Bibliotecas de classes de itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [Como: implantar um Item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  

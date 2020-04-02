---
title: Declarando permissões em assemblies personalizados | Microsoft Docs
description: Saiba como declarar permissões para que você possa implementar um assembly personalizado que faça chamadas seguras para recursos protegidos em seu sistema de segurança.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2b3f4600c4c03fe356f5694f0d9a6cd5bc7afb98
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80217050"
---
# <a name="asserting-permissions-in-custom-assemblies"></a>Declarando permissões em assemblies personalizados
  Por padrão, o código de assembly personalizado é executado com o conjunto de permissões limitado **Execução**. Em alguns casos, talvez você queira implementar um assembly personalizado que crie chamadas seguras para proteger recursos em seu sistema de segurança (como um arquivo ou o Registro). Para realizar isso, faça o seguinte:  
  
1.  Identifique as permissões exatas das quais o seu código precisa para fazer a chamada segura. Se esse método fizer parte de uma biblioteca do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], essas informações deverão ser incluídas na documentação do método.  
  
2.  Modifique os arquivos de configuração de política de servidor de relatório para conceder as permissões exigidas ao assembly personalizado. Para obter mais informações sobre os arquivos de configuração da política de segurança, consulte [Usando arquivos da política de segurança do Reporting Services](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
3.  Declare as permissões exigidas como parte do método no qual a ligação segura será feita. Isso é obrigatório porque o código de assembly personalizado chamado pelo servidor de relatório faz parte do assembly host de expressão de relatório, executado com a permissão **Execução** por padrão. O conjunto de permissões **Execução** permite que o código seja executado, mas não permite o uso de recursos protegidos.  
  
4.  Marque o assembly personalizado com **AllowPartiallyTrustedCallersAttribute** se ele for assinado com um nome forte. Isso é obrigatório porque os assemblies personalizados são chamados por uma expressão de relatório que faz parte do assembly host de expressão de relatório que, por padrão, não recebe a permissão **FullTrust**; dessa forma, ele é um chamador “parcialmente confiável”. Para obter mais informações, consulte [Usando assemblies de nome forte personalizados](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md).  
  
## <a name="implementing-a-secure-call"></a>Implementando uma chamada segura  
 Você pode modificar os arquivos de configuração de política para conceder as permissões específicas ao seu assembly. Por exemplo, se você estiver escrevendo um assembly personalizado para manipular conversão de moedas, talvez seja necessário ler as taxas de câmbio da moeda atual em um arquivo. Para recuperar as informações de taxa, você precisará adicionar outra permissão de segurança, **FileIOPermission**, ao conjunto de permissões do assembly. Crie a entrada adicional a seguir no arquivo de configuração de política:  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 Em seguida, adicione um grupo de códigos que faça referência ao conjunto de permissões:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 Para que seu código adquira a permissão apropriada, você deve declarar a permissão em seu código de assembly personalizado. Por exemplo, se quiser adicionar acesso somente leitura a um arquivo XML, C:\CurrencyRates.xml, adicione o código a seguir a seu método:  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 Você também pode adicionar a declaraçào como um atributo de método:  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 Para obter mais informações, consulte "Segurança do .NET Framework" no Guia do desenvolvedor do .NET Framework.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  

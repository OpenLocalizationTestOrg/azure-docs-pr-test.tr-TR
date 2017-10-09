---
title: aaaAutomate PowerShell ile Azure Application Insights | Microsoft Docs
description: "Bir Azure Resource Manager şablonu kullanarak PowerShell'de oluşturma kaynak, uyarı ve kullanılabilirlik testlerini otomatikleştirme."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a>PowerShell ile Application Insights kaynakları oluşturma
Bu makalede tooautomate nasıl hello oluşturma ve güncelleştirme gösterilmektedir [Application Insights](app-insights-overview.md) Azure kaynak yönetimi kullanarak otomatik olarak kaynakları. Örneğin, bir derleme işleminin parçası olarak bunu olabilir. Merhaba temel Application Insights kaynağı yanı sıra, oluşturduğunuz [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md), ayarlayın [uyarıları](app-insights-alerts.md)ayarlayın hello [düzeni fiyatlandırma](app-insights-pricing.md)ve diğer Azure oluşturun kaynaklar.

Bu kaynaklar JSON şablonları için olan anahtar toocreating hello [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). Buna koysalar hello yordamdır: var olan kaynakların; hello JSON tanımları indirmek adları gibi belirli değerleri Parametreleştirme; ve toocreate yeni bir kaynak istediğinizde hello şablonu çalıştırın. Bazı kaynaklar birlikte, bunların tümü bir - örneğin Git toocreate, bir uygulama İzleyicisi kullanılabilirlik testleri, uyarılar ve sürekli dışa aktarma için depolama paketleyebilirsiniz. Burada açıklayacağız hello parameterizations, bazı subtleties toosome vardır.

## <a name="one-time-setup"></a>Tek seferlik Kurulumu
Önce Azure aboneliğinizle PowerShell kullanmadıysanız:

Hello Azure Powershell modülü toorun hello betikleri istediğiniz hello makineye yükleyin:

1. Yükleme [Microsoft Web Platformu Yükleyicisi (v5 veya üzeri)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Microsoft Azure Powershell tooinstall kullanın.

## <a name="create-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu oluşturma
Yeni bir .json dosyası oluşturma - şimdi çağrı `template1.json` Bu örnekte. Bu içerik bu dosyaya kopyalayın:

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a>Application Insights kaynakları oluşturun
1. PowerShell'de tooAzure oturum:
   
    `Login-AzureRmAccount`
2. Bu gibi bir komutu çalıştırın:
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`Merhaba toocreate hello yeni kaynaklar istediğiniz grubudur.
   * `-TemplateFile`Hello özel parametreler önce gerçekleşmesi gerekir.
   * `-appName`Merhaba kaynak toocreate Hello adı.

Diğer parametreler ekleyebilirsiniz - hello Parametreler bölümünde hello şablonunun açıklamalarını bulabilirsiniz.

## <a name="tooget-hello-instrumentation-key"></a>tooget hello izleme anahtarı
Uygulama kaynağı oluşturduktan sonra hello izleme anahtarını isteyebilirsiniz: 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Set hello fiyat planı

Merhaba ayarlayabilirsiniz [fiyat planı](app-insights-pricing.md).

toocreate hello Kurumsal fiyat planı, yukarıdaki hello şablonunu kullanarak uygulama kaynakla:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|Planlama|
|---|---|
|1|Temel|
|2|Enterprise|

* Toouse hello varsayılan temel fiyat planı yalnızca istiyorsanız hello CurrentBillingFeatures kaynak hello şablondan atlayabilirsiniz.
* Merhaba bileşen kaynak oluşturulduktan sonra toochange hello fiyat planı istiyorsanız, hello "microsoft.insights/components" kaynak atlar bir şablon kullanabilirsiniz. Ayrıca, hello atlayın `dependsOn` kaynak faturalama hello düğümden. 

tooverify güncelleştirilmiş fiyat planı Merhaba, "Özellikleri + fiyatlandırma" Merhaba dikey penceresinde hello tarayıcı bakın. **Merhaba tarayıcı görünümünü yenileyin** toomake hello en son durumunu gördüğünüzden emin.



## <a name="add-a-metric-alert"></a>Ölçüm uyarısı ekleme

Merhaba ölçüm bir uyarı oluşturan tooset aynı birleştirme koda şöyle hello şablon dosyası, Uygulama kaynağı olarak süresi:

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

Merhaba şablon çağırdığınızda, bu parametre isteğe bağlı olarak ekleyebilirsiniz:

    `-responseTime 2`

Elbette, diğer alanlar Parametreleştirme. 

toofind hello tür adları ve diğer uyarı kurallarını yapılandırma ayrıntılarını el ile bir kural oluşturmak ve bunu inceleyin [Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Bir kullanılabilirlik testi ekleyin

Bu, ping sınaması (tootest tek bir sayfayla) örneğidir.  

**İki bölümden oluşur** bir kullanılabilirlik testinde: hello test kendisi ve hataları size bildirir hello uyarı.

Kod hello uygulamasını oluşturur hello şablon dosyasına aşağıdaki hello birleştirin.

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

diğer test konumları ya da daha karmaşık web testleri tooautomate hello oluşturulması için toodiscover hello kodları örnek el ile oluşturup hello koddan Parametreleştirme [Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Daha fazla kaynak ekleyin

herhangi bir türdeki herhangi bir kaynağın tooautomate hello oluşturma örneği el ile oluşturun ve sonra kopyalayın ve kendi koddan Parametreleştirme [Azure Resource Manager](https://resources.azure.com/). 

1. Açık [Azure Resource Manager](https://resources.azure.com/). Aşağı gezinmek `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour Uygulama kaynağı. 
   
    ![Gezinti bölmesinde Azure kaynak Gezgini](./media/app-insights-powershell/01.png)
   
    *Bileşenleri* hello uygulamaları görüntülemek için temel Application Insights kaynaklardır. Merhaba ilişkili uyarı kuralları ve kullanılabilirlik web testleri için ayrı kaynak yok.
2. Kopya hello hello uygun yere içine hello bileşeninin JSON içinde `template1.json`.
3. Bu özellikleri silin:
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Merhaba webtests ve alertrules bölümleri açın ve tek tek öğelerin hello JSON şablonunuza kopyalayın. (Merhaba webtests veya alertrules düğümünden kopyalama: hello öğeleri bunları altında gidin.)
   
    Her web testi ilişkili bir uyarı kuralı sahiptir, bu nedenle toocopy hem de bunların sahip.
   
    Ölçümleri uyarılar de içerir. [Ölçüm adları](app-insights-powershell-alerts.md#metric-names).
5. Her bir kaynağın bu satırı ekleyin:
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Merhaba şablon Parametreleştirme
Artık tooreplace hello belirli adları parametreleri var. çok[şablon Parametreleştirme](../azure-resource-manager/resource-group-authoring-templates.md), kullanarak ifadeler yazma bir [yardımcı işlevleri kümesi](../azure-resource-manager/resource-group-template-functions.md). 

Yalnızca bir dize parçası Parametreleştirme, kullanın `concat()` toobuild dizeleri.

Örnekler hello değişimler toomake isteyeceksiniz. Her değiştirme birkaç kez vardır. Başkalarının şablonunuzda gerekebilir. Bu örnekler hello parametreler ve değişkenler tanımladığımız hello şablon hello üstünde kullanın.

| Bul | değiştirin |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"`(küçük harf) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Delete GUID ve kimliği. |

### <a name="set-dependencies-between-hello-resources"></a>Merhaba kaynakları arasındaki bağımlılıkların ayarlama
Azure hello kaynakları katı sırayla ayarlamanız gerekir. Merhaba sonraki başlamadan önce bir kurulum tamamlandıktan emin toomake bağımlılık satırları ekleyin:

* Merhaba kullanılabilirlik kaynak test edin:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* Uyarı kaynak Hello kullanılabilirliği testi için:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Sonraki adımlar
Diğer Otomasyon makaleler:

* [Application Insights kaynağı oluşturma](app-insights-powershell-script-create-resource.md) -Şablon kullanmadan hızlı yöntem.
* [Uyarıları ayarlayın](app-insights-powershell-alerts.md)
* [Web testleri oluşturma](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Azure tanılama tooApplication Öngörüler Gönder](app-insights-powershell-azure-diagnostics.md)
* [Github'dan tooAzure dağıtma](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Yayın ek açıklamaları oluşturma](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)


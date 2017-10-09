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
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="180b4-103">PowerShell ile Application Insights kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="180b4-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="180b4-104">Bu makalede tooautomate nasıl hello oluşturma ve güncelleştirme gösterilmektedir [Application Insights](app-insights-overview.md) Azure kaynak yönetimi kullanarak otomatik olarak kaynakları.</span><span class="sxs-lookup"><span data-stu-id="180b4-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="180b4-105">Örneğin, bir derleme işleminin parçası olarak bunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="180b4-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="180b4-106">Merhaba temel Application Insights kaynağı yanı sıra, oluşturduğunuz [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md), ayarlayın [uyarıları](app-insights-alerts.md)ayarlayın hello [düzeni fiyatlandırma](app-insights-pricing.md)ve diğer Azure oluşturun kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="180b4-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="180b4-107">Bu kaynaklar JSON şablonları için olan anahtar toocreating hello [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="180b4-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="180b4-108">Buna koysalar hello yordamdır: var olan kaynakların; hello JSON tanımları indirmek adları gibi belirli değerleri Parametreleştirme; ve toocreate yeni bir kaynak istediğinizde hello şablonu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="180b4-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="180b4-109">Bazı kaynaklar birlikte, bunların tümü bir - örneğin Git toocreate, bir uygulama İzleyicisi kullanılabilirlik testleri, uyarılar ve sürekli dışa aktarma için depolama paketleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180b4-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="180b4-110">Burada açıklayacağız hello parameterizations, bazı subtleties toosome vardır.</span><span class="sxs-lookup"><span data-stu-id="180b4-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="180b4-111">Tek seferlik Kurulumu</span><span class="sxs-lookup"><span data-stu-id="180b4-111">One-time setup</span></span>
<span data-ttu-id="180b4-112">Önce Azure aboneliğinizle PowerShell kullanmadıysanız:</span><span class="sxs-lookup"><span data-stu-id="180b4-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="180b4-113">Hello Azure Powershell modülü toorun hello betikleri istediğiniz hello makineye yükleyin:</span><span class="sxs-lookup"><span data-stu-id="180b4-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="180b4-114">Yükleme [Microsoft Web Platformu Yükleyicisi (v5 veya üzeri)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="180b4-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="180b4-115">Microsoft Azure Powershell tooinstall kullanın.</span><span class="sxs-lookup"><span data-stu-id="180b4-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="180b4-116">Bir Azure Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="180b4-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="180b4-117">Yeni bir .json dosyası oluşturma - şimdi çağrı `template1.json` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="180b4-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="180b4-118">Bu içerik bu dosyaya kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="180b4-118">Copy this content into it:</span></span>

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



## <a name="create-application-insights-resources"></a><span data-ttu-id="180b4-119">Application Insights kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="180b4-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="180b4-120">PowerShell'de tooAzure oturum:</span><span class="sxs-lookup"><span data-stu-id="180b4-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="180b4-121">Bu gibi bir komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="180b4-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="180b4-122">`-ResourceGroupName`Merhaba toocreate hello yeni kaynaklar istediğiniz grubudur.</span><span class="sxs-lookup"><span data-stu-id="180b4-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="180b4-123">`-TemplateFile`Hello özel parametreler önce gerçekleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="180b4-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="180b4-124">`-appName`Merhaba kaynak toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="180b4-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="180b4-125">Diğer parametreler ekleyebilirsiniz - hello Parametreler bölümünde hello şablonunun açıklamalarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180b4-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="180b4-126">tooget hello izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="180b4-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="180b4-127">Uygulama kaynağı oluşturduktan sonra hello izleme anahtarını isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180b4-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="180b4-128">Set hello fiyat planı</span><span class="sxs-lookup"><span data-stu-id="180b4-128">Set hello price plan</span></span>

<span data-ttu-id="180b4-129">Merhaba ayarlayabilirsiniz [fiyat planı](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="180b4-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="180b4-130">toocreate hello Kurumsal fiyat planı, yukarıdaki hello şablonunu kullanarak uygulama kaynakla:</span><span class="sxs-lookup"><span data-stu-id="180b4-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="180b4-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="180b4-131">priceCode</span></span>|<span data-ttu-id="180b4-132">Planlama</span><span class="sxs-lookup"><span data-stu-id="180b4-132">plan</span></span>|
|---|---|
|<span data-ttu-id="180b4-133">1</span><span class="sxs-lookup"><span data-stu-id="180b4-133">1</span></span>|<span data-ttu-id="180b4-134">Temel</span><span class="sxs-lookup"><span data-stu-id="180b4-134">Basic</span></span>|
|<span data-ttu-id="180b4-135">2</span><span class="sxs-lookup"><span data-stu-id="180b4-135">2</span></span>|<span data-ttu-id="180b4-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="180b4-136">Enterprise</span></span>|

* <span data-ttu-id="180b4-137">Toouse hello varsayılan temel fiyat planı yalnızca istiyorsanız hello CurrentBillingFeatures kaynak hello şablondan atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180b4-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="180b4-138">Merhaba bileşen kaynak oluşturulduktan sonra toochange hello fiyat planı istiyorsanız, hello "microsoft.insights/components" kaynak atlar bir şablon kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180b4-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="180b4-139">Ayrıca, hello atlayın `dependsOn` kaynak faturalama hello düğümden.</span><span class="sxs-lookup"><span data-stu-id="180b4-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="180b4-140">tooverify güncelleştirilmiş fiyat planı Merhaba, "Özellikleri + fiyatlandırma" Merhaba dikey penceresinde hello tarayıcı bakın.</span><span class="sxs-lookup"><span data-stu-id="180b4-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="180b4-141">**Merhaba tarayıcı görünümünü yenileyin** toomake hello en son durumunu gördüğünüzden emin.</span><span class="sxs-lookup"><span data-stu-id="180b4-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="180b4-142">Ölçüm uyarısı ekleme</span><span class="sxs-lookup"><span data-stu-id="180b4-142">Add a metric alert</span></span>

<span data-ttu-id="180b4-143">Merhaba ölçüm bir uyarı oluşturan tooset aynı birleştirme koda şöyle hello şablon dosyası, Uygulama kaynağı olarak süresi:</span><span class="sxs-lookup"><span data-stu-id="180b4-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

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

<span data-ttu-id="180b4-144">Merhaba şablon çağırdığınızda, bu parametre isteğe bağlı olarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180b4-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="180b4-145">Elbette, diğer alanlar Parametreleştirme.</span><span class="sxs-lookup"><span data-stu-id="180b4-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="180b4-146">toofind hello tür adları ve diğer uyarı kurallarını yapılandırma ayrıntılarını el ile bir kural oluşturmak ve bunu inceleyin [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="180b4-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="180b4-147">Bir kullanılabilirlik testi ekleyin</span><span class="sxs-lookup"><span data-stu-id="180b4-147">Add an availability test</span></span>

<span data-ttu-id="180b4-148">Bu, ping sınaması (tootest tek bir sayfayla) örneğidir.</span><span class="sxs-lookup"><span data-stu-id="180b4-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="180b4-149">**İki bölümden oluşur** bir kullanılabilirlik testinde: hello test kendisi ve hataları size bildirir hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="180b4-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="180b4-150">Kod hello uygulamasını oluşturur hello şablon dosyasına aşağıdaki hello birleştirin.</span><span class="sxs-lookup"><span data-stu-id="180b4-150">Merge hello following code into hello template file that creates hello app.</span></span>

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

<span data-ttu-id="180b4-151">diğer test konumları ya da daha karmaşık web testleri tooautomate hello oluşturulması için toodiscover hello kodları örnek el ile oluşturup hello koddan Parametreleştirme [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="180b4-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="180b4-152">Daha fazla kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="180b4-152">Add more resources</span></span>

<span data-ttu-id="180b4-153">herhangi bir türdeki herhangi bir kaynağın tooautomate hello oluşturma örneği el ile oluşturun ve sonra kopyalayın ve kendi koddan Parametreleştirme [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="180b4-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="180b4-154">Açık [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="180b4-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="180b4-155">Aşağı gezinmek `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour Uygulama kaynağı.</span><span class="sxs-lookup"><span data-stu-id="180b4-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Gezinti bölmesinde Azure kaynak Gezgini](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="180b4-157">*Bileşenleri* hello uygulamaları görüntülemek için temel Application Insights kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="180b4-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="180b4-158">Merhaba ilişkili uyarı kuralları ve kullanılabilirlik web testleri için ayrı kaynak yok.</span><span class="sxs-lookup"><span data-stu-id="180b4-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="180b4-159">Kopya hello hello uygun yere içine hello bileşeninin JSON içinde `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="180b4-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="180b4-160">Bu özellikleri silin:</span><span class="sxs-lookup"><span data-stu-id="180b4-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="180b4-161">Merhaba webtests ve alertrules bölümleri açın ve tek tek öğelerin hello JSON şablonunuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="180b4-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="180b4-162">(Merhaba webtests veya alertrules düğümünden kopyalama: hello öğeleri bunları altında gidin.)</span><span class="sxs-lookup"><span data-stu-id="180b4-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="180b4-163">Her web testi ilişkili bir uyarı kuralı sahiptir, bu nedenle toocopy hem de bunların sahip.</span><span class="sxs-lookup"><span data-stu-id="180b4-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="180b4-164">Ölçümleri uyarılar de içerir.</span><span class="sxs-lookup"><span data-stu-id="180b4-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="180b4-165">[Ölçüm adları](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="180b4-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="180b4-166">Her bir kaynağın bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="180b4-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="180b4-167">Merhaba şablon Parametreleştirme</span><span class="sxs-lookup"><span data-stu-id="180b4-167">Parameterize hello template</span></span>
<span data-ttu-id="180b4-168">Artık tooreplace hello belirli adları parametreleri var.</span><span class="sxs-lookup"><span data-stu-id="180b4-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="180b4-169">çok[şablon Parametreleştirme](../azure-resource-manager/resource-group-authoring-templates.md), kullanarak ifadeler yazma bir [yardımcı işlevleri kümesi](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="180b4-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="180b4-170">Yalnızca bir dize parçası Parametreleştirme, kullanın `concat()` toobuild dizeleri.</span><span class="sxs-lookup"><span data-stu-id="180b4-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="180b4-171">Örnekler hello değişimler toomake isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="180b4-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="180b4-172">Her değiştirme birkaç kez vardır.</span><span class="sxs-lookup"><span data-stu-id="180b4-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="180b4-173">Başkalarının şablonunuzda gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="180b4-173">You might need others in your template.</span></span> <span data-ttu-id="180b4-174">Bu örnekler hello parametreler ve değişkenler tanımladığımız hello şablon hello üstünde kullanın.</span><span class="sxs-lookup"><span data-stu-id="180b4-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="180b4-175">Bul</span><span class="sxs-lookup"><span data-stu-id="180b4-175">find</span></span> | <span data-ttu-id="180b4-176">değiştirin</span><span class="sxs-lookup"><span data-stu-id="180b4-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="180b4-177">`"myappname"`(küçük harf)</span><span class="sxs-lookup"><span data-stu-id="180b4-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="180b4-178">Delete GUID ve kimliği.</span><span class="sxs-lookup"><span data-stu-id="180b4-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="180b4-179">Merhaba kaynakları arasındaki bağımlılıkların ayarlama</span><span class="sxs-lookup"><span data-stu-id="180b4-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="180b4-180">Azure hello kaynakları katı sırayla ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="180b4-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="180b4-181">Merhaba sonraki başlamadan önce bir kurulum tamamlandıktan emin toomake bağımlılık satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="180b4-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="180b4-182">Merhaba kullanılabilirlik kaynak test edin:</span><span class="sxs-lookup"><span data-stu-id="180b4-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="180b4-183">Uyarı kaynak Hello kullanılabilirliği testi için:</span><span class="sxs-lookup"><span data-stu-id="180b4-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="180b4-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="180b4-184">Next steps</span></span>
<span data-ttu-id="180b4-185">Diğer Otomasyon makaleler:</span><span class="sxs-lookup"><span data-stu-id="180b4-185">Other automation articles:</span></span>

* <span data-ttu-id="180b4-186">[Application Insights kaynağı oluşturma](app-insights-powershell-script-create-resource.md) -Şablon kullanmadan hızlı yöntem.</span><span class="sxs-lookup"><span data-stu-id="180b4-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="180b4-187">Uyarıları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="180b4-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="180b4-188">Web testleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="180b4-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="180b4-189">Azure tanılama tooApplication Öngörüler Gönder</span><span class="sxs-lookup"><span data-stu-id="180b4-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="180b4-190">Github'dan tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="180b4-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="180b4-191">Yayın ek açıklamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="180b4-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)


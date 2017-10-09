---
title: "aaaAutomatic ölçekleme ve sanal makine ölçekleme kümeleri | Microsoft Docs"
description: "Tanılama ve otomatik ölçeklendirme kaynakları tooautomatically ölçek sanal makine ölçek kümesindeki kullanma hakkında bilgi edinin."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="83d1a-103">Nasıl toouse otomatik ölçeklendirme ve sanal makine ölçekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="83d1a-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="83d1a-104">Ölçek kümesindeki sanal makinelerin otomatik ölçeklendirmeyi hello oluşturma ya da toomatch performans gereksinimlerini yap hello makinelerinizde silinmesini gerekli.</span><span class="sxs-lookup"><span data-stu-id="83d1a-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="83d1a-105">Merhaba toplu iş büyüdükçe, bir uygulama ek kaynaklar tooenable gerektirebilir onu tooeffectively görevleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="83d1a-106">Otomatik ölçeklendirme yardımcı yönetim yükünü kolaylaştırır otomatik bir işlem var.</span><span class="sxs-lookup"><span data-stu-id="83d1a-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="83d1a-107">Ek yükünü azaltarak, yok toocontinually sistem performansını izleme gerekir veya karar nasıl toomanage kaynakları.</span><span class="sxs-lookup"><span data-stu-id="83d1a-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="83d1a-108">Ölçeklendirme esnek bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-108">Scaling is an elastic process.</span></span> <span data-ttu-id="83d1a-109">Daha fazla kaynak hello yük arttıkça eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="83d1a-110">Ve isteğe bağlı azalıyor, kaynakları kaldırılan toominimize maliyetleri kullanılabilir ve performans düzeylerini sağlamaya.</span><span class="sxs-lookup"><span data-stu-id="83d1a-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="83d1a-111">Otomatik bir Azure Resource Manager şablonu, Azure PowerShell, Azure CLI veya hello Azure portal kullanarak bir ölçekte ölçeklendirmeyi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="83d1a-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="83d1a-112">Resource Manager şablonları kullanarak ölçeklendirmeyi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83d1a-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="83d1a-113">Dağıtma ve her bir kaynağın, uygulamanızın ayrı ayrı yönetmek yerine, tüm kaynakları tek ve eşgüdümlü bir işlemle dağıtan bir şablon kullanın.</span><span class="sxs-lookup"><span data-stu-id="83d1a-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="83d1a-114">Merhaba şablonunda uygulama kaynakları tanımlanır ve farklı ortamlar için dağıtım parametresi belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="83d1a-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="83d1a-115">JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur.</span><span class="sxs-lookup"><span data-stu-id="83d1a-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="83d1a-116">daha fazlasını toolearn bakabilir [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="83d1a-117">Merhaba şablonunda hello kapasite öğesi belirtin:</span><span class="sxs-lookup"><span data-stu-id="83d1a-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="83d1a-118">Kapasite hello kümesindeki sanal makineleri hello sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="83d1a-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="83d1a-119">Farklı bir değere sahip bir şablon dağıtarak hello kapasite el ile değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d1a-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="83d1a-120">Bir şablon tooonly değişiklik hello kapasite dağıtıyorsanız, güncelleştirilmiş hello kapasiteyle yalnızca hello SKU öğe içerebilir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="83d1a-121">Merhaba, Ölçek kümesi kapasitesi otomatik olarak hello birleşimini kullanarak ayarlanabilir **autoscaleSettings** kaynak ve hello tanılama uzantısını.</span><span class="sxs-lookup"><span data-stu-id="83d1a-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="83d1a-122">Hello Azure tanılama uzantısını Yapılandır</span><span class="sxs-lookup"><span data-stu-id="83d1a-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="83d1a-123">Ölçümleri toplama hello ölçek kümesindeki sanal makinelerin her başarılı olursa otomatik ölçeklendirmeyi yalnızca yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="83d1a-124">Hello Azure tanılama uzantısını hello ölçümleri toplama hello otomatik ölçeklendirme kaynak ihtiyaçlarını karşılayan hello izleme ve tanılama olanakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="83d1a-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="83d1a-125">Merhaba uzantısı hello Resource Manager şablonu bir parçası olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d1a-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="83d1a-126">Bu örnekte kullanılan hello değişkenleri hello şablonu tooconfigure hello tanılama uzantısı'nda gösterir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="83d1a-127">Merhaba şablon dağıtıldığında parametreler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="83d1a-128">Bu örnek, hello (verilerinin depolandığı) hello depolama hesabı adını ve hello (burada verileri toplanır) hello ölçek kümesinin adını sağlanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="83d1a-129">Ayrıca bu Windows Server örnekte yalnızca hello iş parçacığı sayısı performans sayacı toplanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="83d1a-130">Tüm kullanılabilir performans sayaçları Windows hello veya Linux kullanılan toocollect tanılama bilgilerini olabilir ve hello uzantısı yapılandırmasında eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="83d1a-131">Bu örnek hello şablonunda hello hello uzantısı tanımını gösterir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-131">This example shows hello definition of hello extension in hello template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="83d1a-132">Merhaba tanılama uzantısını çalıştığında hello veriler depolanır ve belirttiğiniz hello depolama hesabındaki bir tabloda, toplanan.</span><span class="sxs-lookup"><span data-stu-id="83d1a-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="83d1a-133">Merhaba, **WADPerformanceCounters** tablo, toplanan hello veri bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="83d1a-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="83d1a-134">Merhaba autoScaleSettings kaynak yapılandırın</span><span class="sxs-lookup"><span data-stu-id="83d1a-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="83d1a-135">sanal makineler hello ölçeğinde azaltın veya tooincrease hello sayısını ayarlayın yapıp hello autoscaleSettings kaynak hello tanılama uzantısını toodecide hello bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="83d1a-136">Bu örnek hello şablonunda hello kaynak hello yapılandırması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-136">This example shows hello configuration of hello resource in hello template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="83d1a-137">Merhaba yukarıdaki örnekte, iki kural hello otomatik ölçeklendirme eylemleri tanımlamak için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="83d1a-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="83d1a-138">Merhaba ilk kural hello ölçeklendirme eylemi tanımlar ve ölçek eylemi hello hello ikinci kuralı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="83d1a-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="83d1a-139">Bu değerleri hello kurallarında sağlanır:</span><span class="sxs-lookup"><span data-stu-id="83d1a-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="83d1a-140">Kural</span><span class="sxs-lookup"><span data-stu-id="83d1a-140">Rule</span></span> | <span data-ttu-id="83d1a-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="83d1a-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="83d1a-142">metricName</span><span class="sxs-lookup"><span data-stu-id="83d1a-142">metricName</span></span>        | <span data-ttu-id="83d1a-143">Bu değer olan hello hello wadperfcounter değişken hello tanılama uzantısını için tanımlanan hello performans sayacı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="83d1a-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="83d1a-144">Merhaba yukarıdaki örnekte, hello iş parçacığı sayısı sayacını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="83d1a-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="83d1a-145">metricResourceUri</span></span> | <span data-ttu-id="83d1a-146">Bu değer hello sanal makine ölçek kümesinin hello kaynak tanımlayıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="83d1a-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="83d1a-147">Bu tanımlayıcı hello hello kaynak grubunun adını, hello hello kaynak sağlayıcısının adını ve hello ölçek kümesi tooscale hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="83d1a-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="83d1a-148">timeGrain</span></span>         | <span data-ttu-id="83d1a-149">Bu değer toplanan hello ölçümleri hello kesinliği olur.</span><span class="sxs-lookup"><span data-stu-id="83d1a-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="83d1a-150">Hello örnek önceki bir dakikalık bir aralıkta verileri toplanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="83d1a-151">Bu değer timeWindow ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="83d1a-152">İstatistiği</span><span class="sxs-lookup"><span data-stu-id="83d1a-152">statistic</span></span>         | <span data-ttu-id="83d1a-153">Bu değer hello ölçümleri birleşik tooaccommodate hello ölçeklendirme eylemi otomatik şeklini belirler.</span><span class="sxs-lookup"><span data-stu-id="83d1a-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="83d1a-154">Merhaba olası değerler şunlardır: ortalama, Min, maks.</span><span class="sxs-lookup"><span data-stu-id="83d1a-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="83d1a-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="83d1a-155">timeWindow</span></span>        | <span data-ttu-id="83d1a-156">Bu değer hello örnek veriler toplanır zaman aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="83d1a-157">5 dakika ile 12 saat arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="83d1a-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="83d1a-158">timeAggregation</span></span>   | <span data-ttu-id="83d1a-159">Bu değer, toplanan hello veri zaman içinde nasıl birleştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="83d1a-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="83d1a-160">Ortalama Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-160">hello default value is Average.</span></span> <span data-ttu-id="83d1a-161">Merhaba olası değerler şunlardır: ortalama, Minimum, maksimum, son, toplam, sayısı.</span><span class="sxs-lookup"><span data-stu-id="83d1a-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="83d1a-162">işleci</span><span class="sxs-lookup"><span data-stu-id="83d1a-162">operator</span></span>          | <span data-ttu-id="83d1a-163">Bu değer kullanılan toocompare hello ölçüm verileri ve hello eşiğin hello işlecidir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="83d1a-164">Merhaba olası değerler şunlardır: NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual eşittir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="83d1a-165">Eşik</span><span class="sxs-lookup"><span data-stu-id="83d1a-165">threshold</span></span>         | <span data-ttu-id="83d1a-166">Bu değer hello ölçek eylemi tetikler hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="83d1a-167">Merhaba eşik değerleri hello için yeterli birbirinden emin tooprovide olması **genişleme** ve **ölçek bileşenini** eylemler.</span><span class="sxs-lookup"><span data-stu-id="83d1a-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="83d1a-168">Her iki eylemler için aynı değerlere hello ayarlarsanız, bir ölçeklendirme eylemi uygulama engeller sabit değişiklik hello sistem düşünmektedir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="83d1a-169">Örneğin, her iki too600 iş parçacıkları örnek önceki hello ayarı çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="83d1a-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="83d1a-170">Yönü</span><span class="sxs-lookup"><span data-stu-id="83d1a-170">direction</span></span>         | <span data-ttu-id="83d1a-171">Bu değer hello eşik değeri elde edilir, alınır hello eylemi belirler.</span><span class="sxs-lookup"><span data-stu-id="83d1a-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="83d1a-172">Merhaba olası artış veya Azalış değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="83d1a-173">type</span><span class="sxs-lookup"><span data-stu-id="83d1a-173">type</span></span>              | <span data-ttu-id="83d1a-174">Bu değer, gerçekleşeceğini ve tooChangeCount ayarlanmalıdır eylemin hello türüdür.</span><span class="sxs-lookup"><span data-stu-id="83d1a-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="83d1a-175">değer</span><span class="sxs-lookup"><span data-stu-id="83d1a-175">value</span></span>             | <span data-ttu-id="83d1a-176">Bu değer, sanal makinelerin hello ölçek kümesinden kaldırıldı tooor eklenen hello sayıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="83d1a-177">Bu değer, 1 veya daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="83d1a-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="83d1a-178">cooldown</span></span>          | <span data-ttu-id="83d1a-179">Merhaba bir sonraki eylem oluşmadan önce bu değer hello zaman toowait hello son ölçeklendirme eylemi itibaren miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="83d1a-180">Bu değer, bir hafta ve bir dakika arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="83d1a-181">Merhaba performans sayacı, bağlı olarak, kullanmakta olduğunuz, bazı hello şablon Yapılandırması'ndaki hello öğelerin farklı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="83d1a-182">Merhaba, örnek önceki hello performans sayacı iş parçacığı sayısıdır ve hello eşik değeridir 650 bir ölçeklendirme eylemi için hello ölçek eylemi için 550 hello eşik değeri şudur.</span><span class="sxs-lookup"><span data-stu-id="83d1a-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="83d1a-183">% İşlemci zamanı gibi bir sayaç kullanırsanız, hello eşik değeri bir ölçeklendirme eylemi belirler CPU kullanım yüzdesini toohello ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="83d1a-184">Yüksek yük gibi bir ölçeklendirme eylemi tetiklendiğinde hello kapasite hello kümesinin hello şablon hello değerinde göre artar.</span><span class="sxs-lookup"><span data-stu-id="83d1a-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="83d1a-185">Örneğin, burada hello kapasite too3 ayarlanır ve hello ölçeklendirme eylemi değeri too1 bir ölçek kümesindeki:</span><span class="sxs-lookup"><span data-stu-id="83d1a-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="83d1a-186">Ne zaman geçerli yük nedenler hello ortalama iş parçacığı sayısı toogo 650 hello eşiğinin üstünde hello:</span><span class="sxs-lookup"><span data-stu-id="83d1a-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="83d1a-187">A **genişleme** eylem nedenler birden artan hello kümesi toobe kapasitesini hello tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="83d1a-188">Merhaba sonuç bir sanal makine ölçek kümesini toohello eklenir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="83d1a-189">Merhaba ortalama hello makinelerde iş parçacığı sayısı üzerinde 600 kalırsa beş dakika sonra bir cooldown süre, başka bir makine toohello eklenir.</span><span class="sxs-lookup"><span data-stu-id="83d1a-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="83d1a-190">Merhaba ortalama iş parçacığı sayısı 550 altında kalırsa, hello kapasitesi hello ölçek kümesi tarafından azaltılır ve bir makine hello kümesinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="83d1a-191">Azure PowerShell kullanarak ölçeklendirme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83d1a-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="83d1a-192">PowerShell tooset otomatik ölçeklendirmeyi yukarı kullanma toosee örnekleri bakabilir [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="83d1a-193">Azure CLI kullanarak ölçeklendirme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83d1a-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="83d1a-194">Azure CLI tooset otomatik ölçeklendirmeyi yukarı kullanma toosee örnekleri bakabilir [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="83d1a-195">Hello Azure portal kullanarak ölçeklendirmeyi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83d1a-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="83d1a-196">toosee kullanma örneği hello Azure portal tooset otomatik ölçeklendirmeyi yukarı arama sırasında [hello Azure portal kullanarak bir sanal makine ölçek kümesi oluşturma](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="83d1a-197">Ölçeklendirme eylemleri araştırın</span><span class="sxs-lookup"><span data-stu-id="83d1a-197">Investigate scaling actions</span></span>

* <span data-ttu-id="83d1a-198">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="83d1a-198">**Azure portal**</span></span>  
<span data-ttu-id="83d1a-199">Şu anda sınırlı miktarda bilgiyi hello portal kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d1a-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="83d1a-200">**Azure Kaynak Gezgini**</span><span class="sxs-lookup"><span data-stu-id="83d1a-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="83d1a-201">Merhaba, Ölçek kümesini geçerli durumunu incelemek için en iyi hello aracıdır.</span><span class="sxs-lookup"><span data-stu-id="83d1a-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="83d1a-202">Bu yolu izleyin ve oluşturduğunuz kümesi hello örnek görünümü hello ölçeğin görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="83d1a-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="83d1a-203">**Abonelikler > {aboneliğinizi} > resourceGroups > {kaynak grubunuz} > sağlayıcıları > Microsoft.Compute > virtualMachineScaleSets > {Ölçek kümesi} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="83d1a-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="83d1a-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="83d1a-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="83d1a-205">Bu komut tooget bazı bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="83d1a-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="83d1a-206">Toohello jumpbox sanal makine, yalnızca diğer herhangi bir makine olur ve ardından uzaktan hello ölçek kümesi toomonitor tek tek işlemleri hello sanal makinelere erişmek gibi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="83d1a-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83d1a-207">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="83d1a-207">Next Steps</span></span>
* <span data-ttu-id="83d1a-208">Bakmak [otomatik olarak bir sanal makine ölçek kümesindeki makineleri ölçekleme](virtual-machine-scale-sets-windows-autoscale.md) toosee toocreate yapılandırılmış otomatik ölçeklendirmeyi ile nasıl bir ölçek kümesi örnek.</span><span class="sxs-lookup"><span data-stu-id="83d1a-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="83d1a-209">Azure özellikleri izleme monitör örnekleri Bul [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="83d1a-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="83d1a-210">Bildirim özellikler hakkında bilgi edinin [otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri Azure İzleyicisi'nde kullanmayı](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="83d1a-211">Çok hakkında bilgi edinin[Azure İzleyicisi'nde kullanım denetim günlüklerini toosend e-posta ve Web kancası uyarı bildirimleri](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="83d1a-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="83d1a-212">Hakkında bilgi edinin [Gelişmiş otomatik ölçeklendirme senaryoları](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="83d1a-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>

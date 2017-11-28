---
title: "Sanal makineleri bir Azure Resource Manager şablonunda | Microsoft Azure"
description: "Sanal makine kaynak bir Azure Resource Manager şablonu nasıl tanımlanır hakkında daha fazla bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="56434-103">Bir Azure Resource Manager şablonu içindeki sanal makineler</span><span class="sxs-lookup"><span data-stu-id="56434-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="56434-104">Bu makalede, sanal makineleri için geçerli bir Azure Resource Manager şablonu yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="56434-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="56434-105">Bu makalede, bir sanal makine oluşturmak için tam bir şablonu açıklamaz; için depolama hesapları, ağ arabirimleri, ortak IP adresleri ve sanal ağlar için kaynak tanımı gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="56434-106">Bu kaynakların nasıl birlikte tanımlanabilir hakkında daha fazla bilgi için bkz: [Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="56434-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="56434-107">Vardır birçok [galerideki şablonları](https://azure.microsoft.com/documentation/templates/?term=VM) VM kaynak içerir.</span><span class="sxs-lookup"><span data-stu-id="56434-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="56434-108">Bir şablona dahil tüm öğeleri burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="56434-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="56434-109">Bu örnek belirtilen sayıda sanal makineleri oluşturmak için bir şablonu tipik kaynak bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="56434-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="56434-110">Bu örnek daha önce oluşturulmuş bir depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="56434-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="56434-111">Şablondan dağıtarak depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="56434-112">Bu örnek ayrıca bir ağ arabirimi ve şablonda tanımlanan kaynaklarına bağımlı kullanır.</span><span class="sxs-lookup"><span data-stu-id="56434-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="56434-113">Bu kaynaklar örnekte gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="56434-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="56434-114">API sürümü</span><span class="sxs-lookup"><span data-stu-id="56434-114">API Version</span></span>

<span data-ttu-id="56434-115">Bir şablonu kullanarak kaynak dağıtırken kullanmak üzere API sürümü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="56434-116">Örnek bu apiVersion öğesini kullanarak sanal makine kaynağı gösterir:</span><span class="sxs-lookup"><span data-stu-id="56434-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="56434-117">Şablonunuzda belirttiğiniz API sürümü şablonda tanımlayabilirsiniz hangi özelliklerin etkiler.</span><span class="sxs-lookup"><span data-stu-id="56434-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="56434-118">Genel olarak, en son API sürümü şablonları oluştururken seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="56434-119">Var olan şablonları için önceki bir API sürümü kullanmaya devam etmek istiyor veya şablonunuz yeni özelliklerden yararlanmak için en son sürümü için güncelleştirme olup olmadığını karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="56434-120">En son API sürümü almak için bu fırsatları kullanın:</span><span class="sxs-lookup"><span data-stu-id="56434-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="56434-121">REST API - [tüm kaynak sağlayıcıları Listele](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="56434-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="56434-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="56434-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="56434-123">Azure CLI 2.0 - [az sağlayıcısı Göster](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="56434-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="56434-124">Parametreler ve değişkenler</span><span class="sxs-lookup"><span data-stu-id="56434-124">Parameters and variables</span></span>

<span data-ttu-id="56434-125">[Parametreleri](../../resource-group-authoring-templates.md) çalıştırdığınızda şablonu için değerler belirten kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="56434-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="56434-126">Bu Parametreler bölümünden örnekte kullanılır:</span><span class="sxs-lookup"><span data-stu-id="56434-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="56434-127">Örnek şablon dağıttığınızda, değerleri adı ve parola yönetici hesabının oluşturmak için her bir VM ve VM sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="56434-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="56434-128">Şablonla yönetilen ayrı bir dosyada parametre değerleri belirtme veya istendiğinde değerleri sağlayarak seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="56434-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="56434-129">[Değişkenleri](../../resource-group-authoring-templates.md) şablonda kullanılan art arda onu veya zamanla değiştirebilirsiniz değerlerini ayarlamak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="56434-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="56434-130">Bu değişkenler bölümü örnekte kullanılır:</span><span class="sxs-lookup"><span data-stu-id="56434-130">This variables section is used in the example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="56434-131">Örnek şablon dağıttığınızda, değişken değerleri adı ve önceden oluşturulmuş depolama hesabının tanımlayıcısı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56434-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="56434-132">Değişkenleri tanılama uzantısını ayarları sağlamak için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56434-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="56434-133">Kullanım [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../../resource-manager-template-best-practices.md) nasıl parametreler ve değişkenler şablonunuzda yapısı istediğinize karar vermenize yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="56434-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="56434-134">Kaynak döngüler</span><span class="sxs-lookup"><span data-stu-id="56434-134">Resource loops</span></span>

<span data-ttu-id="56434-135">Uygulamanız için birden fazla sanal makine gerektiğinde bir şablonda bir kopya öğesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="56434-136">Bu isteğe bağlı öğe, bir parametre olarak belirtilen VM'ler oluşturmada size döngü:</span><span class="sxs-lookup"><span data-stu-id="56434-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="56434-137">Örnekte'de, fark döngü dizini bazı kaynak için değerleri belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56434-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="56434-138">Örneğin, üç örnek sayısı girdiyseniz, işletim sistemi disklerinde adlarını myOSDisk1, myOSDisk2 ve myOSDisk3 şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56434-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="56434-139">Bu örnek yönetilen diskleri sanal makineler için kullanır.</span><span class="sxs-lookup"><span data-stu-id="56434-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="56434-140">Şablonda bir kaynak için bir döngü oluşturma oluştururken veya diğer kaynaklara erişme döngü kullanmanızı gerektirebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="56434-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="56434-141">Örneğin, üç sanal makineleri oluşturmada size şablonunuzu döngü, aynı zamanda üç ağ arabirimleri oluşturmada size döngü gerekir böylece birden çok VM aynı ağ arabirimi, kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="56434-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="56434-142">Bir ağ arabirimi için bir VM atarken, döngü dizini tanımlamak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="56434-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="56434-143">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="56434-143">Dependencies</span></span>

<span data-ttu-id="56434-144">En fazla kaynak düzgün çalışması için diğer kaynaklara bağımlı.</span><span class="sxs-lookup"><span data-stu-id="56434-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="56434-145">Sanal makineler, bir ağ arabirimi gerektiği yapmak için bir sanal ağ ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="56434-146">[DependsOn](../../resource-group-define-dependencies.md) öğe ağ arabirimi sanal makineleri oluşturmadan önce kullanılmaya hazır olduğundan emin olmak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="56434-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="56434-147">Resource Manager dağıtılan başka bir kaynağa bağımlı olmayan tüm kaynakları paralel olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="56434-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="56434-148">Gereksiz bağımlılıkları belirterek dağıtımınızı yanlışlıkla yavaşlatabileceği için bağımlılıkları ayarlarken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="56434-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="56434-149">Bağımlılıklar birden fazla kaynak zincir.</span><span class="sxs-lookup"><span data-stu-id="56434-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="56434-150">Örneğin, ağ arabirimi genel IP adresi ve sanal ağ kaynaklarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="56434-151">Bir bağımlılık gerekli olup olmadığını nasıl bilebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="56434-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="56434-152">Şablonda ayarlanan değerlerle bakın.</span><span class="sxs-lookup"><span data-stu-id="56434-152">Look at the values you set in the template.</span></span> <span data-ttu-id="56434-153">Bir öğe varsa sanal makine kaynak tanımı noktaları aynı şablonunda dağıtılan başka bir kaynak için bir bağımlılık gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="56434-154">Örneğin, örnek sanal makine bir ağ profili tanımlar:</span><span class="sxs-lookup"><span data-stu-id="56434-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="56434-155">Bu özelliği ayarlamak için ağ arabiriminin mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="56434-156">Bu nedenle, bir bağımlılık gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="56434-157">Ayrıca, bir kaynak (alt) içindeki başka bir kaynak (üst) tanımlandığında bir bağımlılık ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="56434-158">Örneğin, tanılama ayarlarını ve özel komut dosyası uzantılarını hem de sanal makine alt kaynaklar olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="56434-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="56434-159">Sanal makinenin var, oluşturulamaz.</span><span class="sxs-lookup"><span data-stu-id="56434-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="56434-160">Bu nedenle, her iki kaynağın sanal makineye bağlı olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="56434-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="56434-161">Profiller</span><span class="sxs-lookup"><span data-stu-id="56434-161">Profiles</span></span>

<span data-ttu-id="56434-162">Birkaç profil öğeler, bir sanal makine kaynağı tanımlarken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56434-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="56434-163">Bazı gereklidir ve bazı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-163">Some are required and some are optional.</span></span> <span data-ttu-id="56434-164">Örneğin, hardwareProfile, osProfile, storageProfile ve networkProfile öğeleri gerekiyor, ancak diagnosticsProfile isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="56434-165">Bu profiller ayarları gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="56434-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="56434-166">boyutu</span><span class="sxs-lookup"><span data-stu-id="56434-166">size</span></span>](sizes.md)
- <span data-ttu-id="56434-167">[ad](/architecture/best-practices/naming-conventions) ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="56434-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="56434-168">disk ve [işletim sistemi ayarları](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="56434-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="56434-169">Ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="56434-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="56434-170">Önyükleme tanılaması</span><span class="sxs-lookup"><span data-stu-id="56434-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="56434-171">Diskleri ve görüntüleri</span><span class="sxs-lookup"><span data-stu-id="56434-171">Disks and images</span></span>
   
<span data-ttu-id="56434-172">Azure'da, vhd dosyaları gösterebilir [disk veya görüntü](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56434-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="56434-173">Belirli bir VM'yi olması için bir vhd dosyasının işletim sisteminde özelleştirilmiş olduğunda, bir disk olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="56434-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="56434-174">Birçok VM oluşturmak için kullanılacak genelleştirilmiş bir vhd dosyasının işletim sisteminde, bunu bir görüntü olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="56434-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="56434-175">Yeni sanal makineler ve yeni diskler bir platform görüntüsünden oluşturma</span><span class="sxs-lookup"><span data-stu-id="56434-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="56434-176">Bir VM oluşturduğunuzda, hangi işletim sistemi kullanmaya karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="56434-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="56434-177">Imagereference öğesi, yeni bir VM işletim sistemini tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56434-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="56434-178">Örnek bir Windows Server işletim sistemi için bir tanım gösterir:</span><span class="sxs-lookup"><span data-stu-id="56434-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="56434-179">Linux işletim sistemi oluşturmak istiyorsanız, bu tanımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="56434-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="56434-180">İşletim sistemi diski için yapılandırma ayarlarını osDisk öğeyle atanır.</span><span class="sxs-lookup"><span data-stu-id="56434-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="56434-181">Örnek, önbelleğe alma modu ayarlandığında yeni bir yönetilen disk tanımlar **ReadWrite** ve disk alanından oluşturulmakta olan bir [platform görüntüsü](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="56434-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="56434-182">Mevcut yönetilen diskleri yeni sanal makineler oluşturun</span><span class="sxs-lookup"><span data-stu-id="56434-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="56434-183">Sanal makineler var olan disklerden oluşturmak istiyorsanız, Imagereference ve osProfile öğeleri kaldırın ve bu disk ayarlarını tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="56434-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="56434-184">Yönetilen bir görüntüden yeni sanal makineler oluşturun</span><span class="sxs-lookup"><span data-stu-id="56434-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="56434-185">Yönetilen bir görüntüden sanal makine oluşturmak istiyorsanız, Imagereference öğesi değiştirin ve bu disk ayarlarını tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="56434-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="56434-186">Veri diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="56434-186">Attach data disks</span></span>

<span data-ttu-id="56434-187">Veri diskleri sanal makineleri için isteğe bağlı olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="56434-188">[Diskleri sayısı](sizes.md) kullandığınız işletim sistemi disk boyutuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="56434-189">Standard_DS1_v2 için ayarlanmış VM'ler ile bunlara eklenemedi veri disklerinin sayısının iki boyutudur.</span><span class="sxs-lookup"><span data-stu-id="56434-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="56434-190">Örnekte, bir yönetilen veri diski her VM'ye ekleniyor:</span><span class="sxs-lookup"><span data-stu-id="56434-190">In the example, one managed data disk is being added to each VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="56434-191">Uzantılar</span><span class="sxs-lookup"><span data-stu-id="56434-191">Extensions</span></span>

<span data-ttu-id="56434-192">Ancak [uzantıları](extensions-features.md) ayrı bir kaynak, VM yakından bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="56434-193">Uzantılar, bir alt kaynak VM veya farklı bir kaynak olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="56434-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="56434-194">Örnekte gösterildiği [tanılama uzantısını](extensions-diagnostics-template.md) Vm'lere eklenmekte olan:</span><span class="sxs-lookup"><span data-stu-id="56434-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="56434-195">Bu uzantı kaynak storageName değişkeni ve tanılama değişkenleri değerlerini sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="56434-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="56434-196">Bu uzantı tarafından toplanan verileri değiştirmek istiyorsanız, daha fazla performans sayaçları wadperfcounters değişkenine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="56434-197">Tanılama verilerini VM diskleri depolandığı daha farklı bir depolama hesabı içine yerleştirilecek seçebilir.</span><span class="sxs-lookup"><span data-stu-id="56434-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="56434-198">Bir VM'ye yükleyebilirsiniz birçok uzantıları vardır, ancak en büyük olasılıkla yararlıdır [özel betik uzantısının](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="56434-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="56434-199">İlk başladığında örnekte, her VM start.ps1 adlı bir PowerShell komut dosyasını çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="56434-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="56434-200">Start.ps1 komut dosyası, birçok yapılandırma görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="56434-201">Örneğin, örnek vm'lerinin eklenen veri diskleri başlatılamadı; bunları başlatmak için özel bir komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="56434-202">Birden çok başlangıç görevleri yapmak için varsa, Azure depolama alanında başka PowerShell betikleri çağırmak için start.ps1 dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="56434-203">Örnek PowerShell kullanır, ancak işletim sistemi üzerinde kullanılabilir herhangi bir komut dosyası yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="56434-204">Yüklü uzantılarla portalında uzantıları ayarlarından durumunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="56434-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Uzantı durumunu Al](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="56434-206">Kullanarak uzantısı bilgi edinebilirsiniz **Get-AzureRmVMExtension** PowerShell komutunu **vm uzantısı get** Azure CLI 2.0 komut veya **uzantısı bilgialma** REST API.</span><span class="sxs-lookup"><span data-stu-id="56434-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="56434-207">Dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="56434-207">Deployments</span></span>

<span data-ttu-id="56434-208">Bir şablonu dağıttığınızda, Azure kaynakları grup olarak dağıtılmış ve otomatik olarak dağıtılan bu gruba bir isim atar izler.</span><span class="sxs-lookup"><span data-stu-id="56434-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="56434-209">Dağıtım şablonu adı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="56434-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="56434-210">Dağıtımdaki kaynakların durumunu hakkında merak ediyorsanız, Azure portalında kaynak grubu dikey kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="56434-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Dağıtım bilgileri alma](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="56434-212">Kaynakları oluşturun veya var olan kaynakların güncelleştirmek için aynı şablonu kullanmak için bir sorun teşkil etmez.</span><span class="sxs-lookup"><span data-stu-id="56434-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="56434-213">Şablonları dağıtmak için komutları kullandığınızda, hangi söyleyin fırsatına sahip [modu](../../resource-group-template-deploy.md) kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="56434-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="56434-214">Mod için ya da ayarlanabilir **tam** veya **artımlı**.</span><span class="sxs-lookup"><span data-stu-id="56434-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="56434-215">Artımlı güncelleştirmeler yapmak için varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="56434-215">The default is to do incremental updates.</span></span> <span data-ttu-id="56434-216">Kullanırken dikkatli olun **tam** modu kaynakları yanlışlıkla silebilir olduğundan.</span><span class="sxs-lookup"><span data-stu-id="56434-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="56434-217">Modu ayarlandığında **tam**, Resource Manager şablonunda olmayan tüm kaynaklar kaynak grubunda siler.</span><span class="sxs-lookup"><span data-stu-id="56434-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56434-218">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="56434-218">Next Steps</span></span>

- <span data-ttu-id="56434-219">Kendi şablonunu kullanarak oluşturduğunuz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="56434-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="56434-220">Kullanılarak oluşturulan şablonu dağıtmak [Resource Manager şablonu ile Windows sanal makine oluşturma](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="56434-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="56434-221">Gözden geçirerek oluşturulan VM'ler yönetmeyi öğrenin [oluşturma ve Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56434-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

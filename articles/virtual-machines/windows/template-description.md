---
title: "bir Azure Resource Manager şablonu aaaVirtual makinelerinizde | Microsoft Azure"
description: "Merhaba sanal makine kaynak bir Azure Resource Manager şablonu nasıl tanımlanır hakkında daha fazla bilgi edinin."
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
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="62e18-103">Bir Azure Resource Manager şablonu içindeki sanal makineler</span><span class="sxs-lookup"><span data-stu-id="62e18-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="62e18-104">Bu makalede toovirtual makineler geçerli bir Azure Resource Manager şablonu yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="62e18-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="62e18-105">Bu makalede, bir sanal makine oluşturmak için tam bir şablonu açıklamaz; için depolama hesapları, ağ arabirimleri, ortak IP adresleri ve sanal ağlar için kaynak tanımı gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="62e18-106">Bu kaynakların nasıl birlikte tanımlanabilir hakkında daha fazla bilgi için bkz: Merhaba [Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="62e18-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="62e18-107">Vardır birçok [hello galeri şablonlarında](https://azure.microsoft.com/documentation/templates/?term=VM) hello VM kaynak içerir.</span><span class="sxs-lookup"><span data-stu-id="62e18-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="62e18-108">Bir şablona dahil tüm öğeleri burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="62e18-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="62e18-109">Bu örnek belirtilen sayıda sanal makineleri oluşturmak için bir şablonu tipik kaynak bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="62e18-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="62e18-110">Bu örnek daha önce oluşturulmuş bir depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="62e18-111">Merhaba şablondan dağıtarak hello depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="62e18-112">Merhaba örneği aynı zamanda bir ağ arabirimi ve hello şablonda tanımlanan kaynaklarına bağımlı kullanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="62e18-113">Bu kaynaklar hello örnekte gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="62e18-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="62e18-114">API sürümü</span><span class="sxs-lookup"><span data-stu-id="62e18-114">API Version</span></span>

<span data-ttu-id="62e18-115">Bir şablonu kullanarak kaynak dağıttığınızda, toospecify hello API toouse bir sürümüne sahip.</span><span class="sxs-lookup"><span data-stu-id="62e18-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="62e18-116">Merhaba, bu apiVersion öğesi kullanılarak hello sanal makine kaynağı örnektir:</span><span class="sxs-lookup"><span data-stu-id="62e18-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="62e18-117">Merhaba hello şablonunuzda belirttiğiniz API sürümü hello şablonda tanımlayabilirsiniz hangi özelliklerin etkiler.</span><span class="sxs-lookup"><span data-stu-id="62e18-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="62e18-118">Genel olarak, şablonları oluştururken hello en son API sürümü seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="62e18-119">Var olan şablonları için önceki bir API sürümü kullanarak toocontinue istediğiniz veya şablonunuz hello en son sürüm tootake yeni özelliklerden için güncelleştirme olup olmadığını karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="62e18-120">Merhaba son API sürümü almak için bu fırsatları kullanın:</span><span class="sxs-lookup"><span data-stu-id="62e18-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="62e18-121">REST API - [tüm kaynak sağlayıcıları Listele](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="62e18-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="62e18-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="62e18-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="62e18-123">Azure CLI 2.0 - [az sağlayıcısı Göster](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="62e18-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="62e18-124">Parametreler ve değişkenler</span><span class="sxs-lookup"><span data-stu-id="62e18-124">Parameters and variables</span></span>

<span data-ttu-id="62e18-125">[Parametreleri](../../resource-group-authoring-templates.md) çalıştırdığınızda, toospecify değerleri hello şablonu için kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="62e18-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="62e18-126">Bu Parametreler bölümünden hello örnekte kullanılır:</span><span class="sxs-lookup"><span data-stu-id="62e18-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="62e18-127">Merhaba örnek şablonu dağıttığınızda, değerleri hello adı ve parola hello yönetici hesabının her VM'ler toocreate VM ve hello sayısına girin.</span><span class="sxs-lookup"><span data-stu-id="62e18-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="62e18-128">Merhaba şablonuyla yönetilebilir ayrı bir dosyada parametre değerleri belirtme veya istendiğinde değerleri sağlayarak hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="62e18-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="62e18-129">[Değişkenleri](../../resource-group-authoring-templates.md) sizin için değerleri tooset kullanılan art arda onu veya zamanla değiştirebilirsiniz hello şablonunda kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="62e18-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="62e18-130">Bu değişkenler bölümü hello örnekte kullanılır:</span><span class="sxs-lookup"><span data-stu-id="62e18-130">This variables section is used in hello example:</span></span>

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

<span data-ttu-id="62e18-131">Merhaba örnek şablonu dağıttığınızda, değişken değerleri hello adı ve daha önce oluşturduğunuz hello depolama hesabının tanımlayıcısı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62e18-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="62e18-132">Ayrıca hello tanılama uzantı için kullanılan tooprovide hello ayarları değişkenlerdir.</span><span class="sxs-lookup"><span data-stu-id="62e18-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="62e18-133">Kullanım hello [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../../resource-manager-template-best-practices.md) toohelp karar toostructure hello parametreler ve değişkenler şablonunuzda nasıl istiyor.</span><span class="sxs-lookup"><span data-stu-id="62e18-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="62e18-134">Kaynak döngüler</span><span class="sxs-lookup"><span data-stu-id="62e18-134">Resource loops</span></span>

<span data-ttu-id="62e18-135">Uygulamanız için birden fazla sanal makine gerektiğinde bir şablonda bir kopya öğesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="62e18-136">Bu isteğe bağlı öğe, bir parametre olarak belirtilen VM hello sayısı oluşturmada size döngü:</span><span class="sxs-lookup"><span data-stu-id="62e18-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="62e18-137">Ayrıca, bazı hello belirtme hello kaynak için değerleri döngü dizini hello Merhaba örneği bildiriminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62e18-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="62e18-138">Örneğin, üç, hello adlarını hello işletim sistemi disklerinde örnek sayısı girdiyseniz myOSDisk1, myOSDisk2 ve myOSDisk3 şunlardır:</span><span class="sxs-lookup"><span data-stu-id="62e18-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="62e18-139">Bu örnek yönetilen diskleri hello sanal makineler için kullanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="62e18-140">Bir kaynak için bir döngü hello şablonunda oluşturma oluştururken veya diğer kaynaklara erişme, toouse hello döngü gerektirebilecek göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="62e18-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="62e18-141">Örneğin, birden çok VM de oluşturmada size döngü gereken üç VM'ler oluşturmada size şablonunuzu döngüler, üç ağ arabirimleri için aynı ağ arabirimi, hello kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="62e18-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="62e18-142">Bir ağ arabirimi tooa VM atarken hello döngü kullanılan tooidentify dizinidir onu:</span><span class="sxs-lookup"><span data-stu-id="62e18-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="62e18-143">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="62e18-143">Dependencies</span></span>

<span data-ttu-id="62e18-144">En fazla kaynak diğer kaynakları toowork doğru bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="62e18-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="62e18-145">Sanal makineler bir sanal ağ ve ağ arabirimi ihtiyaç duyduğu toodo ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="62e18-146">Merhaba [dependsOn](../../resource-group-define-dependencies.md) öğesidir kullanılan toomake hello ağ arabirimini hello VM'ler oluşturulmadan önce kullanılan hazır toobe olmasını:</span><span class="sxs-lookup"><span data-stu-id="62e18-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="62e18-147">Resource Manager dağıtılan başka bir kaynağa bağımlı olmayan tüm kaynakları paralel olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="62e18-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="62e18-148">Gereksiz bağımlılıkları belirterek dağıtımınızı yanlışlıkla yavaşlatabileceği için bağımlılıkları ayarlarken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="62e18-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="62e18-149">Bağımlılıklar birden fazla kaynak zincir.</span><span class="sxs-lookup"><span data-stu-id="62e18-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="62e18-150">Örneğin, hello ağ arabirimi hello genel IP adresi ve sanal ağ kaynaklarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="62e18-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="62e18-151">Bir bağımlılık gerekli olup olmadığını nasıl bilebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="62e18-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="62e18-152">Merhaba şablonda ayarlanan hello değerleri bakın.</span><span class="sxs-lookup"><span data-stu-id="62e18-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="62e18-153">Öğenin hello sanal makine kaynak tanımı'nda hello dağıtılan tooanother kaynak gösteriyorsa aynı şablonu, bir bağımlılık gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="62e18-154">Örneğin, örnek sanal makine bir ağ profili tanımlar:</span><span class="sxs-lookup"><span data-stu-id="62e18-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="62e18-155">tooset bu özelliğin hello ağ arabirimi var olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="62e18-156">Bu nedenle, bir bağımlılık gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="62e18-157">Bir kaynak (alt) içindeki başka bir kaynak (üst) tanımlandığında tooset bir bağımlılık da gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="62e18-158">Örneğin, hello tanılama ayarlarını ve özel betik uzantılarının her ikisi de hello sanal makine alt kaynaklar olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="62e18-159">Merhaba sanal makine var. Bunlar oluşturulamaz.</span><span class="sxs-lookup"><span data-stu-id="62e18-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="62e18-160">Bu nedenle, her iki kaynağın hello sanal makineye bağlı olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="62e18-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="62e18-161">Profiller</span><span class="sxs-lookup"><span data-stu-id="62e18-161">Profiles</span></span>

<span data-ttu-id="62e18-162">Birkaç profil öğeler, bir sanal makine kaynağı tanımlarken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62e18-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="62e18-163">Bazı gereklidir ve bazı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="62e18-163">Some are required and some are optional.</span></span> <span data-ttu-id="62e18-164">Örneğin, hello hardwareProfile, osProfile, storageProfile ve networkProfile öğeleri gerekiyor, ancak hello diagnosticsProfile isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="62e18-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="62e18-165">Bu profiller ayarları gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="62e18-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="62e18-166">boyutu</span><span class="sxs-lookup"><span data-stu-id="62e18-166">size</span></span>](sizes.md)
- <span data-ttu-id="62e18-167">[ad](/architecture/best-practices/naming-conventions) ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="62e18-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="62e18-168">disk ve [işletim sistemi ayarları](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="62e18-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="62e18-169">Ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="62e18-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="62e18-170">Önyükleme tanılaması</span><span class="sxs-lookup"><span data-stu-id="62e18-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="62e18-171">Diskleri ve görüntüleri</span><span class="sxs-lookup"><span data-stu-id="62e18-171">Disks and images</span></span>
   
<span data-ttu-id="62e18-172">Azure'da, vhd dosyaları gösterebilir [disk veya görüntü](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62e18-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="62e18-173">Bir vhd dosyasının Hello işletim sisteminde özel toobe belirli bir VM'yi olduğunda, başvurulan tooas bir disk olur.</span><span class="sxs-lookup"><span data-stu-id="62e18-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="62e18-174">Bir vhd dosyasının Hello işletim sisteminde genelleştirilmiş toobe toocreate birçok VM kullanılan, başvurulan tooas bir görüntü değil.</span><span class="sxs-lookup"><span data-stu-id="62e18-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="62e18-175">Yeni sanal makineler ve yeni diskler bir platform görüntüsünden oluşturma</span><span class="sxs-lookup"><span data-stu-id="62e18-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="62e18-176">Bir VM oluşturduğunuzda, hangi işletim sistemi toouse karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e18-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="62e18-177">Merhaba Imagereference kullanılan toodefine hello işletim sisteminin yeni bir VM öğedir.</span><span class="sxs-lookup"><span data-stu-id="62e18-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="62e18-178">Merhaba, bir Windows Server işletim sistemi için bir tanım örnektir:</span><span class="sxs-lookup"><span data-stu-id="62e18-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="62e18-179">Linux işletim sistemi toocreate istiyorsanız, bu tanımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62e18-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="62e18-180">Merhaba işletim sistemi diski için yapılandırma ayarlarını hello osDisk öğeyle atanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="62e18-181">Merhaba örnek yeni bir yönetilen disk mod kümesi çok önbelleğe alma hello tanımlar**ReadWrite** ve o hello disk alanından oluşturuluyor bir [platform görüntüsü](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="62e18-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="62e18-182">Mevcut yönetilen diskleri yeni sanal makineler oluşturun</span><span class="sxs-lookup"><span data-stu-id="62e18-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="62e18-183">Var olan disklerin toocreate sanal makinelerden istiyorsanız, hello Imagereference ve hello osProfile öğeleri kaldırın ve bu disk ayarları tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="62e18-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="62e18-184">Yönetilen bir görüntüden yeni sanal makineler oluşturun</span><span class="sxs-lookup"><span data-stu-id="62e18-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="62e18-185">Toocreate istiyorsanız, yönetilen bir görüntüden sanal makine hello Imagereference öğesi değiştirin ve bu disk ayarlarını tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="62e18-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="62e18-186">Veri diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="62e18-186">Attach data disks</span></span>

<span data-ttu-id="62e18-187">Veri diskleri toohello VM'ler isteğe bağlı olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="62e18-188">Merhaba [diskleri sayısı](sizes.md) hello kullandığınız işletim sistemi disk boyutuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="62e18-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="62e18-189">Merhaba ile tooStandard_DS1_v2, bunları iki toohello eklenemedi veri diski maksimum sayısı hello hello VM'ler boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="62e18-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="62e18-190">Merhaba örnekte, bir yönetilen veri diski tooeach VM ekleniyor:</span><span class="sxs-lookup"><span data-stu-id="62e18-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="62e18-191">Uzantılar</span><span class="sxs-lookup"><span data-stu-id="62e18-191">Extensions</span></span>

<span data-ttu-id="62e18-192">Ancak [uzantıları](extensions-features.md) ayrı bir kaynak, yakından bağlı tooVMs oldukları.</span><span class="sxs-lookup"><span data-stu-id="62e18-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="62e18-193">Uzantıları hello VM alt kaynak veya farklı bir kaynak olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="62e18-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="62e18-194">Merhaba örnek gösterir hello [tanılama uzantısını](extensions-diagnostics-template.md) toohello VM'ler eklenmekte olan:</span><span class="sxs-lookup"><span data-stu-id="62e18-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

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

<span data-ttu-id="62e18-195">Bu uzantı kaynak hello storageName değişkeni ve hello tanılama değişkenleri tooprovide değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="62e18-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="62e18-196">Bu uzantı tarafından toplanan toochange hello verilerin istiyorsanız, daha fazla performans sayaçları toohello wadperfcounters değişken ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="62e18-197">Merhaba VM diskleri depolandığı daha farklı bir depolama hesabı içine tooput hello tanılama verilerini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="62e18-198">Bir VM'ye yükleyebilirsiniz birçok uzantıları vardır, ancak en yararlı hello büyük olasılıkla hello [özel betik uzantısının](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="62e18-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="62e18-199">İlk başladığında hello örnekte, her VM start.ps1 adlı bir PowerShell komut dosyasını çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="62e18-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="62e18-200">Merhaba start.ps1 betik birçok yapılandırma görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="62e18-201">Örneğin, toohello VM'ler hello örnekte eklenen hello veri diskleri başlatılamadı; özel bir komut dosyası tooinitialize kullanabileceğiniz bunları.</span><span class="sxs-lookup"><span data-stu-id="62e18-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="62e18-202">Birden çok başlangıç görevleri toodo varsa, Azure depolama alanında hello start.ps1 dosya toocall diğer PowerShell komut dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="62e18-203">Merhaba örnek PowerShell kullanır, ancak hello işletim sisteminde, kullanmakta olduğunuz kullanılabilir herhangi bir komut dosyası yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62e18-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="62e18-204">Merhaba portalındaki hello uzantıları ayarları yüklü hello uzantılardan hello durumunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62e18-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Uzantı durumunu Al](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="62e18-206">Hello kullanarak uzantısı bilgi edinebilirsiniz **Get-AzureRmVMExtension** PowerShell komutunu hello **vm uzantısı get** Azure CLI 2.0 komut veya hello **uzantısı bilgi alma**  REST API.</span><span class="sxs-lookup"><span data-stu-id="62e18-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="62e18-207">Dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="62e18-207">Deployments</span></span>

<span data-ttu-id="62e18-208">Bir şablonu, bir grup olarak ve otomatik olarak dağıtılan Azure parçaları hello kaynakları dağıttığınızda bir adı dağıtılan toothis Grup atar.</span><span class="sxs-lookup"><span data-stu-id="62e18-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="62e18-209">Merhaba dağıtım Hello adı olduğu hello hello şablonu hello adı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="62e18-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="62e18-210">Hello dağıtımda kaynakların hello durumuyla ilgili merak ediyorsanız hello kaynak grubu dikey hello Azure portalını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62e18-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Dağıtım bilgileri alma](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="62e18-212">Bir sorun toouse değil hello aynı şablon toocreate kaynakları veya tooupdate mevcut kaynakları.</span><span class="sxs-lookup"><span data-stu-id="62e18-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="62e18-213">Komutları toodeploy şablonlarını kullandığınızda, hello fırsat toosay sahip olduğu [modu](../../resource-group-template-deploy.md) toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="62e18-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="62e18-214">başlangıç modu tooeither ayarlanabilir **tam** veya **artımlı**.</span><span class="sxs-lookup"><span data-stu-id="62e18-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="62e18-215">Merhaba, toodo artımlı güncelleştirmeler varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="62e18-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="62e18-216">Merhaba kullanırken dikkatli olun **tam** modu kaynakları yanlışlıkla silebilir olduğundan.</span><span class="sxs-lookup"><span data-stu-id="62e18-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="62e18-217">Ayarladığınızda hello modu çok**tam**, Resource Manager hello şablonunda olmayan tüm kaynaklar hello kaynak grubunda siler.</span><span class="sxs-lookup"><span data-stu-id="62e18-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62e18-218">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="62e18-218">Next Steps</span></span>

- <span data-ttu-id="62e18-219">Kendi şablonunu kullanarak oluşturduğunuz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="62e18-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="62e18-220">Kullanılarak oluşturulan hello şablonu dağıtmak [Resource Manager şablonu ile Windows sanal makine oluşturma](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="62e18-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="62e18-221">Nasıl toomanage hello gözden geçirerek oluşturulan VM'ler öğrenin [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62e18-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

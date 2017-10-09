---
title: "Windows sanal makine ölçek kümeleri aaaAutoscale | Microsoft Docs"
description: "Bir Windows sanal makine ölçek Azure PowerShell kullanarak ayarlamak için otomatik ölçeklendirmeyi ayarlayalım ayarlayın"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="ece3e-103">Bir sanal makine ölçek kümesindeki makineleri otomatik olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="ece3e-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="ece3e-104">Sanal makine ölçek kümeleri sizin için toodeploy kolaylaştırır ve aynı sanal makineleri bir küme olarak yönetin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="ece3e-105">Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="ece3e-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="ece3e-106">Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek ayarlar](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="ece3e-107">Bu öğretici toocreate Windows sanal makineler ve otomatik olarak ölçek hello hello makinelerinizde ölçek kümesi nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="ece3e-108">Ve Azure Resource Manager şablonu oluşturma ve Azure PowerShell kullanarak dağıtmayı ölçeklendirmeyi ayarlayın hello ölçeği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ece3e-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="ece3e-109">Şablonlar hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="ece3e-110">Otomatik ölçek kümesi ölçeklendirme hakkında daha fazla toolearn bkz [otomatik ölçeklendirme ve sanal makine ölçek ayarlar](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="ece3e-111">Bu makalede, dağıttığınız hello aşağıdaki kaynaklar ve uzantıları:</span><span class="sxs-lookup"><span data-stu-id="ece3e-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="ece3e-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="ece3e-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="ece3e-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="ece3e-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="ece3e-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="ece3e-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="ece3e-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="ece3e-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="ece3e-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="ece3e-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="ece3e-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="ece3e-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="ece3e-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="ece3e-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="ece3e-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="ece3e-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="ece3e-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="ece3e-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="ece3e-121">Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="ece3e-122">1. adım: Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="ece3e-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="ece3e-123">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooAzure içinde imzalama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="ece3e-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="ece3e-124">2. adım: bir kaynak grubu ve bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ece3e-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="ece3e-125">**Bir kaynak grubu oluşturmak** – tüm kaynakları dağıtılan tooa kaynak grubu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="ece3e-126">Kullanım [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) bir kaynak grubu adında toocreate **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="ece3e-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="ece3e-127">**Depolama hesabı oluşturma** – bu depolama hesabını hello şablon depolandığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="ece3e-128">Kullanım [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) bir depolama hesabı adlı toocreate **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="ece3e-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="ece3e-129">3. adım: hello şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ece3e-129">Step 3: Create hello template</span></span>
<span data-ttu-id="ece3e-130">Bir Azure Resource Manager şablonu, toodeploy mümkün kılar ve hello kaynakları ve ilişkili dağıtım parametreleri JSON açıklamasını kullanarak Azure kaynaklarını birlikte yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="ece3e-131">Sık kullanılan düzenleyicinizde hello dosya C:\VMSSTemplate.json oluşturun ve hello ilk JSON yapısı toosupport hello şablonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="ece3e-132">Parametreler her zaman gerekli değildir, ancak hello şablon dağıtıldığında değerleri yolu tooinput sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="ece3e-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="ece3e-133">Bu parametreleri toohello şablonu eklediğiniz hello parametreleri üst öğenin altında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="ece3e-134">Merhaba ayrı sanal makineyi hello ölçek kümesinde kullanılan tooaccess hello makineler için bir ad.</span><span class="sxs-lookup"><span data-stu-id="ece3e-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="ece3e-135">Merhaba şablon depolandığı hello depolama hesabını Hello adı.</span><span class="sxs-lookup"><span data-stu-id="ece3e-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="ece3e-136">sanal makineler tooinitially Hello sayıda hello ölçek kümesindeki oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ece3e-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="ece3e-137">Merhaba adı ve hello sanal makinelerde hello yönetici hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="ece3e-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="ece3e-138">Toosupport hello ölçek oluşturulan hello kaynaklar için bir ad önekini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ece3e-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="ece3e-139">Değişkenleri, sık sık değişebilir bir şablonu toospecify değerlerini kullanılabilir veya parametre değerlerini birleşiminden toobe gereken değerleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ece3e-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="ece3e-140">Bu değişkenler toohello şablonu eklediğiniz hello değişkenleri üst öğenin altında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="ece3e-141">Merhaba ağ arabirimleri tarafından kullanılan DNS adları.</span><span class="sxs-lookup"><span data-stu-id="ece3e-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="ece3e-142">Başlangıç IP adresi adları ve önekleri hello sanal ağ ve alt ağları için.</span><span class="sxs-lookup"><span data-stu-id="ece3e-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="ece3e-143">Merhaba adları ve tanımlayıcıları hello sanal ağ, yük dengeleyici ve ağ arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="ece3e-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="ece3e-144">Merhaba ölçek kümesindeki hello makinelerle ilişkili hello hesapları için depolama hesabı adları.</span><span class="sxs-lookup"><span data-stu-id="ece3e-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="ece3e-145">Merhaba hello sanal makinelerde yüklü tanılama uzantısını yönelik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ece3e-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="ece3e-146">Merhaba tanılama uzantısını hakkında daha fazla bilgi için bkz: [izleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ece3e-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="ece3e-147">Toohello şablonu eklediğiniz hello kaynakları üst öğenin altında Hello depolama hesabı kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="ece3e-148">Bu şablon, hello işletim sistemi disklerinde ve tanılama verilerinin depolandığı beş depolama hesapları önerilen bir döngü toocreate hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="ece3e-149">Bu hesapları kümesi too100 hello geçerli en büyük bir ölçek kümesindeki sanal makineleri yedeklemek destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="ece3e-150">Her Depolama hesabı hello şablonu için başlangıç parametreleri sağlayın hello öneki ile birleştirilmiş hello değişkenlerine tanımlandı harf göstergesi ile adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="ece3e-151">Merhaba sanal ağ kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-151">Add hello virtual network resource.</span></span> <span data-ttu-id="ece3e-152">Daha fazla bilgi için bkz: [ağ kaynak sağlayıcısı](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="ece3e-153">Hello tarafından kullanılan hello ortak IP adresi kaynakları yük dengeleyici ve ağ arabirimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="ece3e-154">Merhaba ölçek kümesi tarafından kullanılan hello yük dengeleyici kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="ece3e-155">Daha fazla bilgi için bkz: [yük dengeleyici için Azure Resource Manager desteği](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="ece3e-156">Merhaba ayrı sanal makine tarafından kullanılan hello ağ arabirimi kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="ece3e-157">Makineler ölçek kümesindeki bir ortak IP adresi üzerinden erişilebilir değil çünkü ayrı bir sanal makine hello aynı sanal oluşturulan tooremotely erişim hello makinelerin ağ.</span><span class="sxs-lookup"><span data-stu-id="ece3e-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="ece3e-158">Merhaba ayrı sanal makine aynı hello ölçek kümesi olarak ağ hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="ece3e-159">Kaynak Hello sanal makine ölçek kümesi ekleyin ve hello ölçek grubundaki tüm sanal makinelerde yüklü hello tanılama uzantısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="ece3e-160">Bu kaynak için hello ayarlarının pek çoğu hello sanal makine kaynağı ile benzerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="ece3e-161">Merhaba temel farklar hello ölçek kümesindeki sanal makinelerin hello sayısını belirtir hello kapasite öğesi ve güncelleştirmeleri toovirtual makineler nasıl yapılacağını belirten upgradePolicy ' dir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="ece3e-162">Tüm hello depolama hesapları oluşturulana kadar hello ölçek kümesini oluşturulmaz belirtildiği gibi hello dependsOn öğeye sahip.</span><span class="sxs-lookup"><span data-stu-id="ece3e-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
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
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="ece3e-163">Merhaba ölçek kümesini nasıl hello ölçek kümesindeki hello makinelerde hello işlemci kullanımına göre ayarlar tanımlar hello autoscaleSettings kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="ece3e-164">Bu öğretici için bu değerleri önemlidir:</span><span class="sxs-lookup"><span data-stu-id="ece3e-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="ece3e-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="ece3e-165">**metricName**</span></span>  
    <span data-ttu-id="ece3e-166">Bu değer olan hello biz hello wadperfcounter değişkeninde tanımlanan hello performans sayacı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="ece3e-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="ece3e-167">Bu değişkeni kullanarak, hello tanılama uzantısını hello toplar **işlemci(_Toplam)\% işlemci zamanı** sayacı.</span><span class="sxs-lookup"><span data-stu-id="ece3e-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="ece3e-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="ece3e-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="ece3e-169">Bu değer hello sanal makine ölçek kümesinin hello kaynak tanımlayıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="ece3e-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="ece3e-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="ece3e-170">**timeGrain**</span></span>  
    <span data-ttu-id="ece3e-171">Bu değer toplanan hello ölçümleri hello kesinliği olur.</span><span class="sxs-lookup"><span data-stu-id="ece3e-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="ece3e-172">Bu şablonda ayarlamak tooone minute.</span><span class="sxs-lookup"><span data-stu-id="ece3e-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="ece3e-173">**İstatistiği**</span><span class="sxs-lookup"><span data-stu-id="ece3e-173">**statistic**</span></span>  
    <span data-ttu-id="ece3e-174">Bu değer hello ölçümleri birleşik tooaccommodate hello ölçeklendirme eylemi otomatik şeklini belirler.</span><span class="sxs-lookup"><span data-stu-id="ece3e-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="ece3e-175">Merhaba olası değerler şunlardır: ortalama, Min, maks.</span><span class="sxs-lookup"><span data-stu-id="ece3e-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="ece3e-176">Bu şablonda hello ortalama toplam CPU kullanımını hello sanal makinelerin toplanır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="ece3e-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="ece3e-177">**timeWindow**</span></span>  
    <span data-ttu-id="ece3e-178">Bu değer hello örnek veriler toplanır zaman aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="ece3e-179">5 dakika ile 12 saat arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="ece3e-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="ece3e-180">**timeAggregation**</span></span>  
    <span data-ttu-id="ece3e-181">kendi değeri, toplanan hello veri zaman içinde nasıl birleştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="ece3e-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="ece3e-182">Ortalama Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-182">hello default value is Average.</span></span> <span data-ttu-id="ece3e-183">Merhaba olası değerler şunlardır: ortalama, Minimum, maksimum, son, toplam, sayısı.</span><span class="sxs-lookup"><span data-stu-id="ece3e-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="ece3e-184">**işleci**</span><span class="sxs-lookup"><span data-stu-id="ece3e-184">**operator**</span></span>  
    <span data-ttu-id="ece3e-185">Bu değer kullanılan toocompare hello ölçüm verileri ve hello eşiğin hello işlecidir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="ece3e-186">Merhaba olası değerler şunlardır: NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual eşittir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="ece3e-187">**Eşik**</span><span class="sxs-lookup"><span data-stu-id="ece3e-187">**threshold**</span></span>  
    <span data-ttu-id="ece3e-188">Bu değer hello ölçek eylemi tetikler hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="ece3e-189">Bu şablonda makineler toohello ölçeği hello kümesindeki makineler arasında hello ortalama CPU kullanımı % 50 üzerinde olduğunda Ayarla eklenir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="ece3e-190">**yönü**</span><span class="sxs-lookup"><span data-stu-id="ece3e-190">**direction**</span></span>  
    <span data-ttu-id="ece3e-191">Bu değer hello eşik değeri elde edilir, alınır hello eylemi belirler.</span><span class="sxs-lookup"><span data-stu-id="ece3e-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="ece3e-192">Merhaba olası artış veya Azalış değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="ece3e-193">Merhaba eşiği % 50'hello tanımlı zaman penceresinde tekrar ise bu şablonda hello hello ölçek kümesindeki sanal makine sayısı artar.</span><span class="sxs-lookup"><span data-stu-id="ece3e-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="ece3e-194">**türü**</span><span class="sxs-lookup"><span data-stu-id="ece3e-194">**type**</span></span>  
    <span data-ttu-id="ece3e-195">Bu değer, gerçekleşeceğini ve tooChangeCount ayarlanmalıdır eylemin hello türüdür.</span><span class="sxs-lookup"><span data-stu-id="ece3e-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="ece3e-196">**değer**</span><span class="sxs-lookup"><span data-stu-id="ece3e-196">**value**</span></span>  
    <span data-ttu-id="ece3e-197">Bu değer hello eklendiğinde veya kaldırıldığında hello ölçek kümesinden sanal makinelerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="ece3e-198">Bu değer, 1 veya daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-198">This value must be 1 or greater.</span></span> <span data-ttu-id="ece3e-199">Merhaba varsayılan değer 1'dir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-199">hello default value is 1.</span></span> <span data-ttu-id="ece3e-200">Hello eşiğine ulaşıldığında bu şablonda artar hello ölçek makinelerinizde hello sayısı 1 ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ece3e-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="ece3e-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="ece3e-201">**cooldown**</span></span>  
    <span data-ttu-id="ece3e-202">Merhaba bir sonraki eylem oluşmadan önce bu değer hello zaman toowait hello son ölçeklendirme eylemi itibaren miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="ece3e-203">Bu değer, bir hafta ve bir dakika arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="ece3e-204">Merhaba şablon dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="ece3e-205">4. adım: Karşıya yükleme hello şablonu toostorage</span><span class="sxs-lookup"><span data-stu-id="ece3e-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="ece3e-206">Merhaba adını ve 1. adımda oluşturduğunuz hello depolama hesabının birincil anahtarını bilmesi sürece hello şablonu karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="ece3e-207">Merhaba Microsoft Azure PowerShell penceresinde hello 1. adımda oluşturduğunuz hello depolama hesabının adını belirten bir değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ece3e-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="ece3e-208">Merhaba depolama hesabının birincil anahtar hello belirten bir değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ece3e-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="ece3e-209">Bu anahtar hello depolama hesabı kaynağı hello Azure portal görüntülerken hello anahtar simgesine tıklayarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="ece3e-210">Merhaba depolama hesabı kullanılan toovalidate işlemleriyle hello depolama hesabı bağlam nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ece3e-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="ece3e-211">Merhaba şablonu depolamak için hello kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ece3e-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="ece3e-212">Merhaba şablon dosyası toohello yeni kapsayıcı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ece3e-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="ece3e-213">5. adım: hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="ece3e-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="ece3e-214">Merhaba şablon oluşturduğunuza göre hello kaynakları dağıtmaya başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="ece3e-215">Bu komut toostart hello işlemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="ece3e-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="ece3e-216">Bastığınızda girin, size atanan hello değişkenleri için istendiğinde tooprovide değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="ece3e-217">Bu değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="ece3e-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="ece3e-218">Tüm hello kaynakları toosuccessfully dağıtılması için yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ece3e-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="ece3e-219">Merhaba portal'ın özelliği toodeploy hello kaynakları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="ece3e-220">Bu bağlantıyı kullanın: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="ece3e-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="ece3e-221">6. adım: İzleme kaynakları</span><span class="sxs-lookup"><span data-stu-id="ece3e-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="ece3e-222">Bu yöntemleri kullanarak sanal makine ölçek kümeleri hakkında bazı bilgiler elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ece3e-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="ece3e-223">Azure portal hello - şu anda sınırlı miktarda bilgiyi hello portal kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="ece3e-224">Merhaba [Azure kaynak Gezgini](https://resources.azure.com/) -hello hello ölçek kümesinde geçerli durumunu incelemek için en iyi bu aracıdır.</span><span class="sxs-lookup"><span data-stu-id="ece3e-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="ece3e-225">Bu yolu izleyin ve oluşturduğunuz kümesi hello örnek görünümü hello ölçeğin görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ece3e-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="ece3e-226">Abonelikler > {aboneliğinizi} > resourceGroups > vmsstestrg1 > sağlayıcıları > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="ece3e-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="ece3e-227">Azure PowerShell - Bu komut tooget bazı bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="ece3e-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="ece3e-228">Veya</span><span class="sxs-lookup"><span data-stu-id="ece3e-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="ece3e-229">Toohello ayrı sanal makine, yalnızca diğer herhangi bir makine olur ve ardından uzaktan hello ölçek kümesi toomonitor tek tek işlemleri hello sanal makinelere erişmek gibi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ece3e-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="ece3e-230">Ölçek kümeleri hakkında bilgi almak için tam bir REST API bulunabilir [sanal makine ölçek ayarlar](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="ece3e-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="ece3e-231">7. adım: hello kaynakları Kaldır</span><span class="sxs-lookup"><span data-stu-id="ece3e-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="ece3e-232">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan bir iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="ece3e-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="ece3e-233">Bir kaynak grubundan ayrı ayrı her bir kaynağın toodelete gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="ece3e-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="ece3e-234">Merhaba kaynak grubunu silmek ve tüm kaynakları otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="ece3e-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="ece3e-235">Kaynak grubunuzun tookeep istiyorsanız, yalnızca kümesi hello ölçek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece3e-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="ece3e-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ece3e-236">Next steps</span></span>
* <span data-ttu-id="ece3e-237">Merhaba bilgileri kullanarak oluşturulan yeni hello ölçek kümesini yönetmek [sanal makine ölçek kümesindeki sanal makineleri yönetme](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="ece3e-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="ece3e-238">[Sanal Makine Ölçek kümeleri ile dikey otomatik ölçeklendirme](virtual-machine-scale-sets-vertical-scale-reprovision.md) bölümünü gözden geçirerek dikey ölçeklendirme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="ece3e-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="ece3e-239">Azure özellikleri izleme monitör örnekleri Bul [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="ece3e-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="ece3e-240">Bildirim özellikler hakkında bilgi edinin [Azure İzleyicisi'nde otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri kullanın](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="ece3e-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="ece3e-241">Nasıl çok öğrenin[Azure İzleyicisi'nde kullanım denetim günlüklerini toosend e-posta ve Web kancası uyarı bildirimleri](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="ece3e-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>


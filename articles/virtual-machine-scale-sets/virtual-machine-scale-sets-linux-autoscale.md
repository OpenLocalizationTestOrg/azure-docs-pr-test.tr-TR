---
title: "Linux sanal makine ölçek kümeleri aaaAutoscale | Microsoft Docs"
description: "Bir Linux sanal makine ölçek Azure CLI kullanarak ayarlamak için otomatik ölçeklendirmeyi ayarlayalım ayarlayın"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="78746-103">Linux makineler bir sanal makine ölçek kümesindeki otomatik olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="78746-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="78746-104">Sanal makine ölçek kümeleri sizin için toodeploy kolaylaştırır ve aynı sanal makineleri bir küme olarak yönetin.</span><span class="sxs-lookup"><span data-stu-id="78746-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="78746-105">Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="78746-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="78746-106">toolearn daha, fazla [sanal makine ölçek kümesi'ne genel bakış](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78746-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="78746-107">Bu öğretici toocreate ölçek Ubuntu Linux hello en son sürümünü kullanarak Linux sanal makineleri nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="78746-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="78746-108">Merhaba öğretici de tooautomatically ölçek hello hello makinelerinizde nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="78746-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="78746-109">Ve Azure Resource Manager şablonu oluşturma ve Azure CLI kullanarak dağıtmayı ölçeklendirmeyi ayarlayın hello ölçeği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78746-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="78746-110">Şablonlar hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78746-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="78746-111">Otomatik ölçek kümesi ölçeklendirme hakkında daha fazla toolearn bkz [otomatik ölçeklendirme ve sanal makine ölçek ayarlar](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78746-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="78746-112">Bu öğreticide dağıttığınız hello aşağıdaki kaynaklar ve uzantıları:</span><span class="sxs-lookup"><span data-stu-id="78746-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="78746-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="78746-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="78746-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="78746-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="78746-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="78746-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="78746-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="78746-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="78746-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="78746-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="78746-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="78746-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="78746-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="78746-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="78746-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="78746-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="78746-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="78746-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="78746-122">Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="78746-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="78746-123">Bu öğreticide, hello adımları ile çalışmaya başlamadan önce [hello Azure CLI yükleme](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="78746-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="78746-124">1. adım: bir kaynak grubu ve bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="78746-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="78746-125">**TooMicrosoft Azure oturum**</span><span class="sxs-lookup"><span data-stu-id="78746-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="78746-126">Komut satırı arabirimi (Bash, Terminal, komut isteminde) tooResource Yöneticisi modu, geçiş yapın ve ardından [iş veya Okul kimlik bilgilerinizle oturum](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Etkileşimli oturum açma deneyimi tooyour Azure hesabı için Hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="78746-127">Bir iş veya Okul kimlik ve olmayan iki faktörlü kimlik doğrulaması etkinleştirilmiş, kullanın `azure login -u` etkileşimli oturum olmadan içinde hello kimliği toolog ile.</span><span class="sxs-lookup"><span data-stu-id="78746-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="78746-128">Bir iş veya Okul kimliği yok, yapabilecekleriniz [bir iş veya Okul kimlik kişisel Microsoft hesabınızı oluşturma](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78746-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="78746-129">**Bir kaynak grubu oluşturun**</span><span class="sxs-lookup"><span data-stu-id="78746-129">**Create a resource group**</span></span>  
<span data-ttu-id="78746-130">Tüm kaynaklar dağıtılan tooa kaynak grubu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78746-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="78746-131">Bu öğretici için hello kaynak grubu adı **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="78746-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="78746-132">**Bir depolama hesabı hello yeni kaynak grubuna Dağıt**</span><span class="sxs-lookup"><span data-stu-id="78746-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="78746-133">Bu depolama hesabını hello şablon depolandığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="78746-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="78746-134">Adlı depolama hesabı oluşturma **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="78746-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="78746-135">2. adım: hello şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="78746-135">Step 2: Create hello template</span></span>
<span data-ttu-id="78746-136">Bir Azure Resource Manager şablonu, toodeploy mümkün kılar ve hello kaynakları ve ilişkili dağıtım parametreleri JSON açıklamasını kullanarak Azure kaynaklarını birlikte yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78746-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="78746-137">Sık kullanılan düzenleyicinizde hello dosya VMSSTemplate.json oluşturun ve hello ilk JSON yapısı toosupport hello şablonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="78746-138">Parametreler her zaman gerekli değildir, ancak hello şablon dağıtıldığında değerleri yolu tooinput sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="78746-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="78746-139">Bu parametreleri toohello şablonu eklediğiniz hello parametreleri üst öğenin altında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="78746-140">Merhaba ayrı sanal makineyi hello ölçek kümesinde kullanılan tooaccess hello makineler için bir ad.</span><span class="sxs-lookup"><span data-stu-id="78746-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="78746-141">Merhaba şablon depolandığı hello depolama hesabı için bir ad.</span><span class="sxs-lookup"><span data-stu-id="78746-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="78746-142">sanal makineler tooinitially örneklerinin sayısını Hello hello ölçek kümesindeki oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78746-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="78746-143">Bir ad ve hello sanal makinelerde hello yönetici hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="78746-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="78746-144">Toosupport hello ölçek oluşturulan hello kaynaklar için bir ad önekini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78746-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="78746-145">Değişkenleri, sık sık değişebilir bir şablonu toospecify değerlerini kullanılabilir veya parametre değerlerini birleşiminden toobe gereken değerleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="78746-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="78746-146">Bu değişkenler toohello şablonu eklediğiniz hello değişkenleri üst öğenin altında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="78746-147">Merhaba ağ arabirimleri tarafından kullanılan DNS adları.</span><span class="sxs-lookup"><span data-stu-id="78746-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="78746-148">Başlangıç IP adresi adları ve önekleri hello sanal ağ ve alt ağları için.</span><span class="sxs-lookup"><span data-stu-id="78746-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="78746-149">Merhaba adları ve tanımlayıcıları hello sanal ağ, yük dengeleyici ve ağ arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="78746-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="78746-150">Merhaba ölçek kümesindeki hello makinelerle ilişkili hello hesapları için depolama hesabı adları.</span><span class="sxs-lookup"><span data-stu-id="78746-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="78746-151">Merhaba hello sanal makinelerde yüklü tanılama uzantısını yönelik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="78746-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="78746-152">Merhaba tanılama uzantısını hakkında daha fazla bilgi için bkz: [izleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78746-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="78746-153">Toohello şablonu eklediğiniz hello kaynakları üst öğenin altında Hello depolama hesabı kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="78746-154">Bu şablon, hello işletim sistemi disklerinde ve tanılama verilerinin depolandığı beş depolama hesapları önerilen bir döngü toocreate hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="78746-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="78746-155">Bu hesapları kümesi too100 hello geçerli en büyük bir ölçek kümesindeki sanal makineleri yedeklemek destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="78746-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="78746-156">Her Depolama hesabı hello şablonu için başlangıç parametreleri sağlayın hello sonekiyle birlikte hello değişkenlerine tanımlandı harf göstergesi ile adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="78746-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="78746-157">Merhaba sanal ağ kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-157">Add hello virtual network resource.</span></span> <span data-ttu-id="78746-158">Daha fazla bilgi için bkz: [ağ kaynak sağlayıcısı](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="78746-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="78746-159">Hello tarafından kullanılan hello ortak IP adresi kaynakları yük dengeleyici ve ağ arabirimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="78746-160">Merhaba ölçek kümesi tarafından kullanılan hello yük dengeleyici kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="78746-161">Daha fazla bilgi için bkz: [yük dengeleyici için Azure Resource Manager desteği](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="78746-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="78746-162">Merhaba ayrı sanal makine tarafından kullanılan hello ağ arabirimi kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="78746-163">Makineler ölçek kümesindeki bir ortak IP adresi üzerinden erişilebilir değil çünkü ayrı bir sanal makine hello aynı sanal oluşturulan tooremotely erişim hello makinelerin ağ.</span><span class="sxs-lookup"><span data-stu-id="78746-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="78746-164">Merhaba ayrı sanal makine aynı hello ölçek kümesi olarak ağ hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="78746-165">Kaynak Hello sanal makine ölçek kümesi ekleyin ve hello ölçek grubundaki tüm sanal makinelerde yüklü hello tanılama uzantısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="78746-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="78746-166">Bu kaynak için hello ayarlarının pek çoğu hello sanal makine kaynağı ile benzerdir.</span><span class="sxs-lookup"><span data-stu-id="78746-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="78746-167">Merhaba temel farklar hello ölçek kümesindeki sanal makinelerin hello sayısını belirtir hello kapasite öğesi ve güncelleştirmeleri toovirtual makineler nasıl yapılacağını belirten upgradePolicy'dır.</span><span class="sxs-lookup"><span data-stu-id="78746-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="78746-168">Tüm hello depolama hesapları oluşturulana kadar hello ölçek kümesini oluşturulmaz belirtildiği gibi hello dependsOn öğeye sahip.</span><span class="sxs-lookup"><span data-stu-id="78746-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="78746-169">Merhaba ölçek kümesini nasıl hello kümesindeki hello makinelerde işlemci kullanımına göre ayarlar tanımlar hello autoscaleSettings kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="78746-170">Bu öğretici için bu değerleri önemlidir:</span><span class="sxs-lookup"><span data-stu-id="78746-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="78746-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="78746-171">**metricName**</span></span>  
    <span data-ttu-id="78746-172">Bu değer olan hello biz hello wadperfcounter değişkeninde tanımlanan hello performans sayacı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="78746-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="78746-173">Bu değişkeni kullanarak, hello tanılama uzantısını hello toplar **Processor\PercentProcessorTime** sayacı.</span><span class="sxs-lookup"><span data-stu-id="78746-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="78746-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="78746-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="78746-175">Bu değer hello sanal makine ölçek kümesinin hello kaynak tanımlayıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="78746-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="78746-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="78746-176">**timeGrain**</span></span>  
    <span data-ttu-id="78746-177">Bu değer toplanan hello ölçümleri hello kesinliği olur.</span><span class="sxs-lookup"><span data-stu-id="78746-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="78746-178">Bu şablonda ayarlamak tooone minute.</span><span class="sxs-lookup"><span data-stu-id="78746-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="78746-179">**İstatistiği**</span><span class="sxs-lookup"><span data-stu-id="78746-179">**statistic**</span></span>  
    <span data-ttu-id="78746-180">Bu değer hello ölçümleri birleşik tooaccommodate hello ölçeklendirme eylemi otomatik şeklini belirler.</span><span class="sxs-lookup"><span data-stu-id="78746-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="78746-181">Merhaba olası değerler şunlardır: ortalama, Min, maks.</span><span class="sxs-lookup"><span data-stu-id="78746-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="78746-182">Bu şablonda hello ortalama toplam CPU kullanımını hello sanal makinelerin toplanır.</span><span class="sxs-lookup"><span data-stu-id="78746-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="78746-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="78746-183">**timeWindow**</span></span>  
    <span data-ttu-id="78746-184">Bu değer hello örnek veriler toplanır zaman aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="78746-185">5 dakika ile 12 saat arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="78746-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="78746-186">**timeAggregation**</span></span>  
    <span data-ttu-id="78746-187">kendi değeri, toplanan hello veri zaman içinde nasıl birleştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="78746-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="78746-188">Ortalama Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="78746-188">hello default value is Average.</span></span> <span data-ttu-id="78746-189">Merhaba olası değerler şunlardır: ortalama, Minimum, maksimum, son, toplam, sayısı.</span><span class="sxs-lookup"><span data-stu-id="78746-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="78746-190">**işleci**</span><span class="sxs-lookup"><span data-stu-id="78746-190">**operator**</span></span>  
    <span data-ttu-id="78746-191">Bu değer kullanılan toocompare hello ölçüm verileri ve hello eşiğin hello işlecidir.</span><span class="sxs-lookup"><span data-stu-id="78746-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="78746-192">Merhaba olası değerler şunlardır: NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual eşittir.</span><span class="sxs-lookup"><span data-stu-id="78746-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="78746-193">**Eşik**</span><span class="sxs-lookup"><span data-stu-id="78746-193">**threshold**</span></span>  
    <span data-ttu-id="78746-194">Bu değer hello ölçek eylemi tetikler.</span><span class="sxs-lookup"><span data-stu-id="78746-194">This value triggers hello scale action.</span></span> <span data-ttu-id="78746-195">Bu şablonda makineler toohello ölçeği hello kümesindeki makineler arasında hello ortalama CPU kullanımı % 50 üzerinde olduğunda Ayarla eklenir.</span><span class="sxs-lookup"><span data-stu-id="78746-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="78746-196">**yönü**</span><span class="sxs-lookup"><span data-stu-id="78746-196">**direction**</span></span>  
    <span data-ttu-id="78746-197">Bu değer hello eşik değeri elde edilir, alınır hello eylemi belirler.</span><span class="sxs-lookup"><span data-stu-id="78746-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="78746-198">Merhaba olası artış veya Azalış değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="78746-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="78746-199">Merhaba eşiği % 50'hello tanımlı zaman penceresinde tekrar ise bu şablonda hello hello ölçek kümesindeki sanal makine sayısı artar.</span><span class="sxs-lookup"><span data-stu-id="78746-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="78746-200">**türü**</span><span class="sxs-lookup"><span data-stu-id="78746-200">**type**</span></span>  
    <span data-ttu-id="78746-201">Bu değer, gerçekleşeceğini ve tooChangeCount ayarlanmalıdır eylemin hello türüdür.</span><span class="sxs-lookup"><span data-stu-id="78746-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="78746-202">**değer**</span><span class="sxs-lookup"><span data-stu-id="78746-202">**value**</span></span>  
    <span data-ttu-id="78746-203">Bu değer hello eklendiğinde veya kaldırıldığında hello ölçek kümesinden sanal makinelerin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="78746-204">Bu değer, 1 veya daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-204">This value must be 1 or greater.</span></span> <span data-ttu-id="78746-205">Merhaba varsayılan değer 1'dir.</span><span class="sxs-lookup"><span data-stu-id="78746-205">hello default value is 1.</span></span> <span data-ttu-id="78746-206">Hello eşiğine ulaşıldığında bu şablonda artar hello ölçek makinelerinizde hello sayısı 1 ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78746-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="78746-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="78746-207">**cooldown**</span></span>  
    <span data-ttu-id="78746-208">Merhaba bir sonraki eylem oluşmadan önce bu değer hello zaman toowait hello son ölçeklendirme eylemi itibaren miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="78746-209">Bu değer, bir hafta ve bir dakika arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="78746-210">Merhaba şablon dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="78746-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="78746-211">3. adım: Karşıya yükleme hello şablonu toostorage</span><span class="sxs-lookup"><span data-stu-id="78746-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="78746-212">Merhaba adını ve 1. adımda oluşturduğunuz hello depolama hesabının birincil anahtarını bilmesi sürece hello şablonu karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="78746-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="78746-213">Komut satırı arabirimi (Bash, Terminal, komut isteminde) tooaccess depolama hesabı hello tooset hello ortam değişkenleri şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78746-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="78746-214">Hello depolama hesabı kaynağı hello Azure portal görüntülerken hello anahtar simgesine tıklayarak hello anahtar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78746-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="78746-215">Bir Windows Komut İstemi'ni kullanırken yazın **ayarlamak** verme yerine.</span><span class="sxs-lookup"><span data-stu-id="78746-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="78746-216">Merhaba şablonu depolamak için hello kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78746-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="78746-217">Merhaba şablon dosyası toohello yeni kapsayıcı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78746-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="78746-218">Adım 4: hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="78746-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="78746-219">Merhaba şablon oluşturduğunuza göre hello kaynakları dağıtmaya başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78746-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="78746-220">Bu komut toostart hello işlemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="78746-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="78746-221">Bastığınızda girin, size atanan hello değişkenleri için istendiğinde tooprovide değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="78746-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="78746-222">Bu değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="78746-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="78746-223">Tüm hello kaynakları toosuccessfully dağıtılması için yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="78746-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="78746-224">Merhaba portal'ın özelliği toodeploy hello kaynakları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78746-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="78746-225">Bu bağlantıyı kullanın: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="78746-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="78746-226">5. adım: İzleme kaynakları</span><span class="sxs-lookup"><span data-stu-id="78746-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="78746-227">Bu yöntemleri kullanarak sanal makine ölçek kümeleri hakkında bazı bilgiler elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78746-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="78746-228">Azure portal hello - şu anda sınırlı miktarda bilgiyi hello portal kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78746-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="78746-229">Merhaba [Azure kaynak Gezgini](https://resources.azure.com/) -hello hello ölçek kümesinde geçerli durumunu incelemek için en iyi bu aracıdır.</span><span class="sxs-lookup"><span data-stu-id="78746-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="78746-230">Bu yolu izleyin ve oluşturduğunuz kümesi hello örnek görünümü hello ölçeğin görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="78746-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="78746-231">Azure CLI - bu komut tooget bazı bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="78746-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="78746-232">Toohello jumpbox sanal makine, yalnızca diğer herhangi bir makine olur ve ardından uzaktan hello ölçek kümesi toomonitor tek tek işlemleri hello sanal makinelere erişmek gibi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="78746-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="78746-233">Ölçek kümeleri hakkında bilgi almak için tam bir REST API bulunabilir [sanal makine ölçek ayarlar](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="78746-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="78746-234">6. adım: hello kaynakları Kaldır</span><span class="sxs-lookup"><span data-stu-id="78746-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="78746-235">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan bir iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="78746-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="78746-236">Bir kaynak grubundan ayrı ayrı her bir kaynağın toodelete gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="78746-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="78746-237">Merhaba kaynak grubunu silmek ve tüm kaynakları otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="78746-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="78746-238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78746-238">Next steps</span></span>
* <span data-ttu-id="78746-239">Azure özellikleri izleme monitör örnekleri Bul [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="78746-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="78746-240">Bildirim özellikler hakkında bilgi edinin [Azure İzleyicisi'nde otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri kullanın](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="78746-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="78746-241">Nasıl çok öğrenin[Azure İzleyicisi'nde kullanım denetim günlüklerini toosend e-posta ve Web kancası uyarı bildirimleri](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="78746-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="78746-242">Merhaba denetleyin [otomatik ölçeklendirme tanıtım uygulamasını Ubuntu 16.04 üzerinde](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) Python/bottle uygulama tooexercise hello sanal makine ölçek ayarlar işlevselliğini ölçeklendirme otomatik ayarlar şablonu.</span><span class="sxs-lookup"><span data-stu-id="78746-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>


---
title: "Azure Resource Manager şablonu aaaCreate ağ güvenlik grupları - | Microsoft Docs"
description: "Bilgi nasıl toocreate ve ağ güvenlik grupları bir Azure Resource Manager şablonunu kullanarak dağıtın."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="f742c-103">Ağ güvenlik grupları bir Azure Resource Manager şablonu kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="f742c-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f742c-104">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f742c-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f742c-105">Ayrıca [hello Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f742c-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="f742c-106">Bir şablon dosyası NSG kaynakları</span><span class="sxs-lookup"><span data-stu-id="f742c-106">NSG resources in a template file</span></span>
<span data-ttu-id="f742c-107">Görüntüleme ve hello karşıdan yükleme [örnek şablonu](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="f742c-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="f742c-108">Merhaba aşağıdaki bölümde gösterilmektedir hello hello tanımını hello senaryoyu temel ön uç NSG.</span><span class="sxs-lookup"><span data-stu-id="f742c-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="f742c-109">tooassociate hello NSG toohello ön uç alt toochange hello alt ağı tanımını hello şablonda ve kullanım hello başvuru kimliği hello NSG için sahip.</span><span class="sxs-lookup"><span data-stu-id="f742c-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="f742c-110">Aynı hello arka uç NSG ve hello arka uç alt ağ için hello şablonunda gerçekleştirilen hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f742c-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="f742c-111">Kullanarak Hello ARM şablonu dağıtma toodeploy tıklatın</span><span class="sxs-lookup"><span data-stu-id="f742c-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="f742c-112">Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="f742c-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f742c-113">toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f742c-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="f742c-114">PowerShell kullanarak Hello ARM şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="f742c-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="f742c-115">PowerShell kullanarak yüklediğiniz toodeploy hello ARM şablonunu hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f742c-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="f742c-116">Azure PowerShell'i hiç kullanmadıysanız, hello hello yönergeleri izleyin [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) tooinstall ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f742c-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="f742c-117">Merhaba çalıştırmak  **`New-AzureRmResourceGroup`**  kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="f742c-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="f742c-118">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="f742c-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="f742c-119">Hello Azure CLI kullanarak Hello ARM şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="f742c-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="f742c-120">toodeploy hello ARM Şablonu'hello Azure CLI kullanarak hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f742c-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="f742c-121">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="f742c-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f742c-122">Merhaba çalıştırmak  **`azure config mode`**  aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="f742c-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f742c-123">Merhaba, hello komut için beklenen hello çıktı aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="f742c-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f742c-124">Merhaba çalıştırmak  **`azure group deployment create`**  cmdlet toodeploy hello hello şablonu ve parametre kullanarak yeni Vnet'i, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f742c-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f742c-125">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f742c-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="f742c-126">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="f742c-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="f742c-127">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="f742c-127">**-n (or --name)**.</span></span> <span data-ttu-id="f742c-128">Merhaba kaynak grubu toobe oluşturulan adı.</span><span class="sxs-lookup"><span data-stu-id="f742c-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="f742c-129">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="f742c-129">**-l (or --location)**.</span></span> <span data-ttu-id="f742c-130">Merhaba kaynak grubunun oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="f742c-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="f742c-131">**-f (veya --şablon-dosyası)**.</span><span class="sxs-lookup"><span data-stu-id="f742c-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="f742c-132">Yol tooyour ARM şablon dosyası.</span><span class="sxs-lookup"><span data-stu-id="f742c-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="f742c-133">**-e (veya--parametreler-dosyası)**.</span><span class="sxs-lookup"><span data-stu-id="f742c-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="f742c-134">Yol tooyour ARM parametreleri dosya.</span><span class="sxs-lookup"><span data-stu-id="f742c-134">Path tooyour ARM parameters file.</span></span>


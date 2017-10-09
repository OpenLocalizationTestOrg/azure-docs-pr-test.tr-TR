---
title: "bir statik genel IP adresi - Azure Resource Manager şablonu ile bir VM aaaCreate | Microsoft Docs"
description: "Nasıl toocreate VM bir statik genel IP adresi bir Azure Resource Manager şablonu kullanarak öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="c0706-103">Bir Azure Resource Manager şablonu kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0706-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0706-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c0706-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="c0706-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0706-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="c0706-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c0706-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="c0706-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="c0706-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="c0706-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="c0706-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c0706-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c0706-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c0706-110">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="c0706-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="c0706-111">Bir şablon dosyasındaki ortak IP adresi kaynakları</span><span class="sxs-lookup"><span data-stu-id="c0706-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="c0706-112">Görüntüleme ve hello karşıdan yükleme [örnek şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c0706-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="c0706-113">Merhaba aşağıdaki bölümde yukarıdaki hello senaryoyu temel hello genel IP kaynağı, hello tanımını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c0706-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="c0706-114">Bildirim hello **Publicıpallocationmethod** çok ayarlama özelliği*statik*.</span><span class="sxs-lookup"><span data-stu-id="c0706-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="c0706-115">Bu özellik ya da olabilir *dinamik* (varsayılan değer) veya *statik*.</span><span class="sxs-lookup"><span data-stu-id="c0706-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="c0706-116">Merhaba atanan genel IP adresi hiçbir zaman değiştirecek toostatic garanti ayarlama.</span><span class="sxs-lookup"><span data-stu-id="c0706-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="c0706-117">Merhaba aşağıdaki bölümde hello ilişkilendirmesini hello ortak IP adresinin ağ arabirimi gösterir:</span><span class="sxs-lookup"><span data-stu-id="c0706-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="c0706-118">Bildirim hello **Publicıpaddress** toohello işaret eden özellik **kimliği** adlı bir kaynağın **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="c0706-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="c0706-119">Yukarıda gösterilen hello genel IP kaynağı hello adını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c0706-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="c0706-120">Merhaba ağ arabirimi yukarıdaki hello son olarak, listelenen **networkProfile** hello oluşturulan VM özelliği.</span><span class="sxs-lookup"><span data-stu-id="c0706-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="c0706-121">Kullanarak Hello şablonu dağıtma toodeploy tıklatın</span><span class="sxs-lookup"><span data-stu-id="c0706-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="c0706-122">Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0706-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="c0706-123">toodeploy tıklatın toodeploy, bu şablonu kullanarak tıklatın **tooAzure dağıtmak** hello Readme.md dosyasında hello [statik PIP VM](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) şablonu.</span><span class="sxs-lookup"><span data-stu-id="c0706-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="c0706-124">İsterseniz Hello varsayılan parametre değerlerini değiştirin ve hello boş parametreler için değerler girin.</span><span class="sxs-lookup"><span data-stu-id="c0706-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="c0706-125">Merhaba portal toocreate statik genel IP adresine sahip bir sanal makine Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c0706-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="c0706-126">PowerShell kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0706-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="c0706-127">PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c0706-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="c0706-128">Azure PowerShell'i hiç kullanmadıysanız, tam hello hello adımları [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c0706-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="c0706-129">Bir PowerShell konsolunda hello çalıştırın `New-AzureRmResourceGroup` cmdlet toocreate yeni bir kaynak grubu, gerekirse.</span><span class="sxs-lookup"><span data-stu-id="c0706-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="c0706-130">Oluşturulan bir kaynak grubu zaten varsa, toostep 3 gidin.</span><span class="sxs-lookup"><span data-stu-id="c0706-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="c0706-131">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c0706-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="c0706-132">Bir PowerShell konsolunda hello çalıştırın `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="c0706-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="c0706-133">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c0706-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="c0706-134">Hello Azure CLI kullanarak Hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0706-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="c0706-135">hello Azure CLI, tam hello aşağıdaki adımları kullanarak toodeploy hello şablonu:</span><span class="sxs-lookup"><span data-stu-id="c0706-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="c0706-136">Hiç Azure CLI kullanmadıysanız, hello hello adımları [hello Azure CLI yükleyip](../cli-install-nodejs.md) makale tooinstall ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0706-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="c0706-137">Merhaba çalıştırmak `azure config mode` aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="c0706-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c0706-138">Merhaba hello komutunun çıktısını yukarıdaki beklenen:</span><span class="sxs-lookup"><span data-stu-id="c0706-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c0706-139">Açık hello [parametre dosyası](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json)içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0706-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="c0706-140">Bu örnekte, hello parametreleri adlı tooa dosyasına kaydedilir *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="c0706-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="c0706-141">İsterseniz hello dosyası içinde Hello parametre değerlerini değiştirmek ancak en azından hello Admınpassword parametresi tooa benzersiz ve karmaşık bir parola hello değerini değiştirmek önerilir.</span><span class="sxs-lookup"><span data-stu-id="c0706-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="c0706-142">Merhaba çalıştırmak `azure group deployment create` cmd toodeploy hello hello şablonu ve parametre kullanarak yeni Vnet'i, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları.</span><span class="sxs-lookup"><span data-stu-id="c0706-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c0706-143">Merhaba aşağıdaki komutta, <path> hello yoluna sahip hello dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c0706-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="c0706-144">Beklenen çıktı: (kullanılan parametre değerlerini listeler)</span><span class="sxs-lookup"><span data-stu-id="c0706-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK


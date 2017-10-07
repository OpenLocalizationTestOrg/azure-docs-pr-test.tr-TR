---
title: "bir sanal ağ aaaCreate | Azure Resource Manager şablonu | Microsoft Docs"
description: "Nasıl toocreate sanal bir ağ bir Azure Resource Manager şablonu kullanarak öğrenin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="fb5ef-103">Bir Azure Resource Manager şablonu kullanarak bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb5ef-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="fb5ef-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fb5ef-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="fb5ef-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="fb5ef-107">Bu makalede nasıl toocreate bir sanal ağ üzerinden hello Resource Manager dağıtım modeli bir Azure Resource Manager şablonu kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="fb5ef-108">Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="fb5ef-109">Portal</span><span class="sxs-lookup"><span data-stu-id="fb5ef-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="fb5ef-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb5ef-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="fb5ef-111">CLI</span><span class="sxs-lookup"><span data-stu-id="fb5ef-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="fb5ef-112">Şablon</span><span class="sxs-lookup"><span data-stu-id="fb5ef-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="fb5ef-113">Portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="fb5ef-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="fb5ef-114">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="fb5ef-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="fb5ef-115">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="fb5ef-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="fb5ef-116">Şunları öğreneceksiniz nasıl toodownload değiştirmek ve var olan ARM şablonunu github'dan ve hello şablonu GitHub, PowerShell ve Azure CLI hello dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="fb5ef-117">Merhaba ARM şablonunu doğrudan github'dan, herhangi bir değişiklik yapılmadan dağıtıyorsanız çok atla[github'dan şablon dağıtma](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="fb5ef-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="fb5ef-118">İndirme ve hello Azure Resource Manager şablonu anlama</span><span class="sxs-lookup"><span data-stu-id="fb5ef-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="fb5ef-119">Merhaba Github'dan VNet ve iki alt ağ oluşturmak için varolan şablonunu indirebilir, istediğiniz ve yeniden tüm değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="fb5ef-120">toodo, bu nedenle, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="fb5ef-121">Çok gidin[hello örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="fb5ef-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="fb5ef-122">**azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="fb5ef-123">Merhaba dosya tooa bilgisayarınızda yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="fb5ef-124">Şablonları hakkında bilginiz varsa 7 toostep atlayın.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="fb5ef-125">Kaydettiğiniz hello dosyasını açın ve altındaki hello içeriğe bakın **parametreleri** satırında 5.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="fb5ef-126">ARM şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için bir yer tutucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="fb5ef-127">Parametre</span><span class="sxs-lookup"><span data-stu-id="fb5ef-127">Parameter</span></span> | <span data-ttu-id="fb5ef-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fb5ef-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="fb5ef-129">**konum**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-129">**location**</span></span> |<span data-ttu-id="fb5ef-130">Merhaba Vnet'in oluşturulacağı azure bölgesi</span><span class="sxs-lookup"><span data-stu-id="fb5ef-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="fb5ef-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-131">**vnetName**</span></span> |<span data-ttu-id="fb5ef-132">Hello için ad yeni VNet</span><span class="sxs-lookup"><span data-stu-id="fb5ef-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="fb5ef-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-133">**addressPrefix**</span></span> |<span data-ttu-id="fb5ef-134">Adres alanı CIDR biçiminde VNet, hello için</span><span class="sxs-lookup"><span data-stu-id="fb5ef-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="fb5ef-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-135">**subnet1Name**</span></span> |<span data-ttu-id="fb5ef-136">Hello için ad ilk sanal ağ</span><span class="sxs-lookup"><span data-stu-id="fb5ef-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="fb5ef-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-137">**subnet1Prefix**</span></span> |<span data-ttu-id="fb5ef-138">Merhaba ilk alt ağ için CIDR bloğu</span><span class="sxs-lookup"><span data-stu-id="fb5ef-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="fb5ef-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-139">**subnet2Name**</span></span> |<span data-ttu-id="fb5ef-140">Hello için ad ikinci VNet</span><span class="sxs-lookup"><span data-stu-id="fb5ef-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="fb5ef-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="fb5ef-141">**subnet2Prefix**</span></span> |<span data-ttu-id="fb5ef-142">Merhaba ikinci alt ağ için CIDR bloğu</span><span class="sxs-lookup"><span data-stu-id="fb5ef-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="fb5ef-143">GitHub’da tutulan Azure Resource Manager şablonları zaman içinde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="fb5ef-144">Kullanmadan önce hello şablonu denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="fb5ef-145">Merhaba içeriği altında denetleyin **kaynakları** ve hello aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="fb5ef-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-146">**type**.</span></span> <span data-ttu-id="fb5ef-147">Merhaba şablon tarafından oluşturulan kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="fb5ef-148">Bu durumda, bir VNet’i temsil eden **Microsoft.Network/virtualNetworks**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="fb5ef-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-149">**name**.</span></span> <span data-ttu-id="fb5ef-150">Merhaba kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-150">Name for hello resource.</span></span> <span data-ttu-id="fb5ef-151">Bildirim hello kullanımını **[parameters('vnetName')]**, hangi anlamına gelir hello giriş olarak dağıtımı sırasında hello kullanıcı ya da bir parametre dosyası tarafından sağlanan ad olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="fb5ef-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-152">**properties**.</span></span> <span data-ttu-id="fb5ef-153">Merhaba kaynak özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-153">List of properties for hello resource.</span></span> <span data-ttu-id="fb5ef-154">Bu şablon, VNet oluşturulduğu sırada hello adres alanı ve alt ağ özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="fb5ef-155">Geri çok gidin[hello örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="fb5ef-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="fb5ef-156">**azuredeploy-parameters.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="fb5ef-157">Merhaba dosya tooa bilgisayarınızda yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="fb5ef-158">Yeni kaydettiğiniz hello dosyasını açın ve hello parametreleri hello değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="fb5ef-159">Toodeploy hello hello senaryoda açıklanan VNet altındaki değerler aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="fb5ef-160">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="fb5ef-161">PowerShell kullanarak hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="fb5ef-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="fb5ef-162">PowerShell kullanarak yüklediğiniz adımları toodeploy hello şablonunu aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="fb5ef-163">Yükleme ve Azure PowerShell hello hello adımları izleyerek yapılandırma [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="fb5ef-164">Komut toocreate aşağıdaki hello yeni bir kaynak grubu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="fb5ef-165">Merhaba komut oluşturur adlı bir kaynak grubu *TestRG* hello içinde *Orta ABD* azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="fb5ef-166">Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md)’ı ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="fb5ef-167">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="fb5ef-168">Toodeploy Merhaba, yukarıda indirdiğiniz ve değiştirdiğiniz hello şablonu ve parametre dosyalarını kullanarak yeni Vnet'i komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="fb5ef-169">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="fb5ef-170">Çalışma hello şu komutu tooview hello hello özelliklerini yeni VNet:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="fb5ef-171">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="fb5ef-172">Dağıtmak için kullanarak hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="fb5ef-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="fb5ef-173">Microsoft ve açık toohello topluluk tarafından tutulan önceden tanımlanmış Azure Resource Manager şablonları karşıya yüklenen tooa GitHub deposunu yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="fb5ef-174">Bu şablonlar Github'dan sınırsız dağıtılabilir veya indirilir ve gereksinimlerinizi toofit değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="fb5ef-175">toodeploy iki alt ağa sahip VNet oluşturan bir şablonu aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="fb5ef-176">Tarayıcıdan çok gidin[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="fb5ef-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="fb5ef-177">Şablonları hello listesini kaydırın ve tıklayın **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="fb5ef-178">Merhaba denetleyin **README.md** aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-178">Check hello **README.md** file, as shown below.</span></span>

    ![Github’da READEME.md dosyası](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="fb5ef-180">Tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="fb5ef-181">Gerekiyorsa, Azure oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="fb5ef-182">Merhaba, **parametreleri** dikey penceresinde, yeni VNet toouse toocreate istediğiniz ve ardından hello değerleri girin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="fb5ef-183">Merhaba aşağıdaki şekilde hello senaryo için hello değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![ARM şablonu parametreleri](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="fb5ef-185">Tıklatın **kaynak grubu** seçip bir kaynak grubu tooadd Vnet'e hello veya tıklatın **Yeni Oluştur** tooadd hello VNet tooa yeni kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="fb5ef-186">Merhaba aşağıdaki şekilde hello kaynak olarak adlandırılan yeni bir kaynak grubu için Grup ayarları gösterilmektedir **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Kaynak grubu](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="fb5ef-188">Gerekirse, hello değiştirmek **abonelik** ve **konumu** ayarlarını.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="fb5ef-189">Toosee hello VNet hello parçasında olarak istemiyorsanız **Sabitle**, devre dışı **PIN tooStartboard**.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="fb5ef-190">Tıklatın **yasal koşulları**hello koşullarını okuyun ve tıklatın **satın** tooagree.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="fb5ef-191">Tıklatın **oluşturma** toocreate hello VNet.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Önizleme portalında dağıtım kutucuğu gönderiliyor](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="fb5ef-193">Merhaba dağıtım tamamlandıktan sonra hello Azure portal'ı tıklatın **daha fazla hizmet**, türü *sanal ağlar* görünen hello filtre kutusuna sanal ağlar toosee hello sanal ağlar dikey penceresinde'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="fb5ef-194">Merhaba dikey penceresinde tıklayın *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="fb5ef-195">Merhaba, *TestVNet* dikey penceresinde tıklatın **alt ağlar** hello resim aşağıdaki gösterildiği gibi toosee oluşturulan hello alt ağlar:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Önizleme portalında VNet oluşturma](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="fb5ef-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb5ef-197">Next steps</span></span>

<span data-ttu-id="fb5ef-198">Bilgi nasıl tooconnect:</span><span class="sxs-lookup"><span data-stu-id="fb5ef-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="fb5ef-199">Bir sanal makine (VM) tooa sanal ağla okuma hello [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md) veya [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-portal.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="fb5ef-200">Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="fb5ef-201">sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="fb5ef-202">bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="fb5ef-203">Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-arm.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="fb5ef-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>

---
title: "Bir sanal ağ oluşturma | Azure Resource Manager şablonu | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu kullanarak bir sanal ağ oluşturmayı öğrenin."
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
ms.openlocfilehash: 81602766848a91331c8d811ea1c8ec3ffae44b96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="eb431-103">Bir Azure Resource Manager şablonu kullanarak bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb431-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="eb431-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="eb431-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="eb431-105">Microsoft, kaynakların Resource Manager dağıtım modeliyle oluşturulmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="eb431-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="eb431-106">İki model arasındaki farkları öğrenmek için [Azure dağıtım modellerini anlama](../azure-resource-manager/resource-manager-deployment-model.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="eb431-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="eb431-107">Bu makalede Azure Resource Manager şablonu kullanarak Resource Manager dağıtım modeli üzerinden bir VNet oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eb431-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="eb431-108">Resource Manager’da farklı araçlar kullanarak da sanal ağ kurabilir veya aşağıdaki listeden farklı bir seçenek belirleyerek klasik dağıtım modeliyle sanal ağ oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb431-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="eb431-109">Portal</span><span class="sxs-lookup"><span data-stu-id="eb431-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="eb431-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb431-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="eb431-111">CLI</span><span class="sxs-lookup"><span data-stu-id="eb431-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="eb431-112">Şablon</span><span class="sxs-lookup"><span data-stu-id="eb431-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="eb431-113">Portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="eb431-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="eb431-114">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="eb431-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="eb431-115">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="eb431-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="eb431-116">Var olan bir ARM şablonunu GitHub'dan indirip değiştirmeyi ve şablonu GitHub, PowerShell ve Azure CLI'dan dağıtmayı öğreneceksiniz</span><span class="sxs-lookup"><span data-stu-id="eb431-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="eb431-117">ARM şablonunu hiçbir değişiklik yapmadan doğrudan GitHub'dan dağıtıyorsanız [GitHub'dan şablon dağıtma](#deploy-the-arm-template-by-using-click-to-deploy) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="eb431-118">Azure Resource Manager şablonu indirme ve anlama</span><span class="sxs-lookup"><span data-stu-id="eb431-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="eb431-119">Github'dan VNet ve iki alt ağ oluşturmak için varolan şablonunu indirebilir, istediğiniz ve yeniden tüm değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="eb431-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="eb431-120">Bunu yapmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="eb431-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="eb431-121">[Örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets) gidin.</span><span class="sxs-lookup"><span data-stu-id="eb431-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="eb431-122">**azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="eb431-123">Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eb431-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="eb431-124">Şablonları hakkında bilginiz varsa 7. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="eb431-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="eb431-125">Henüz kaydetmiş olduğunuz dosyayı açın ve 5. satırdaki **parametreler** altındaki içeriğe bakın.</span><span class="sxs-lookup"><span data-stu-id="eb431-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="eb431-126">ARM şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için bir yer tutucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb431-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="eb431-127">Parametre</span><span class="sxs-lookup"><span data-stu-id="eb431-127">Parameter</span></span> | <span data-ttu-id="eb431-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eb431-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="eb431-129">**konum**</span><span class="sxs-lookup"><span data-stu-id="eb431-129">**location**</span></span> |<span data-ttu-id="eb431-130">VNet’in oluşturulacağı Azure bölgesi</span><span class="sxs-lookup"><span data-stu-id="eb431-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="eb431-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="eb431-131">**vnetName**</span></span> |<span data-ttu-id="eb431-132">Yeni VNet'in adı</span><span class="sxs-lookup"><span data-stu-id="eb431-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="eb431-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="eb431-133">**addressPrefix**</span></span> |<span data-ttu-id="eb431-134">CIDR biçiminde VNet adres alanı</span><span class="sxs-lookup"><span data-stu-id="eb431-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="eb431-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="eb431-135">**subnet1Name**</span></span> |<span data-ttu-id="eb431-136">İlk VNet adı</span><span class="sxs-lookup"><span data-stu-id="eb431-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="eb431-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="eb431-137">**subnet1Prefix**</span></span> |<span data-ttu-id="eb431-138">İlk alt ağ için CIDR bloğu</span><span class="sxs-lookup"><span data-stu-id="eb431-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="eb431-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="eb431-139">**subnet2Name**</span></span> |<span data-ttu-id="eb431-140">İkinci VNet adı</span><span class="sxs-lookup"><span data-stu-id="eb431-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="eb431-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="eb431-141">**subnet2Prefix**</span></span> |<span data-ttu-id="eb431-142">İkinci alt ağ için CIDR bloğu</span><span class="sxs-lookup"><span data-stu-id="eb431-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="eb431-143">GitHub’da tutulan Azure Resource Manager şablonları zaman içinde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="eb431-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="eb431-144">Kullanmadan önce şablonu denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="eb431-144">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="eb431-145">**Kaynaklar** altındaki içeriği denetleyin ve aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="eb431-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="eb431-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="eb431-146">**type**.</span></span> <span data-ttu-id="eb431-147">Şablon tarafından oluşturulan kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="eb431-147">Type of resource being created by the template.</span></span> <span data-ttu-id="eb431-148">Bu durumda, bir VNet’i temsil eden **Microsoft.Network/virtualNetworks**.</span><span class="sxs-lookup"><span data-stu-id="eb431-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="eb431-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="eb431-149">**name**.</span></span> <span data-ttu-id="eb431-150">Kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="eb431-150">Name for the resource.</span></span> <span data-ttu-id="eb431-151">Kullanıcının adı girdi veya dağıtım sırasında bir parametre dosyası olarak vereceği anlamına gelen **[parameters('vnetName')]** öğesinin kullanımına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="eb431-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="eb431-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="eb431-152">**properties**.</span></span> <span data-ttu-id="eb431-153">Kaynak özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="eb431-153">List of properties for the resource.</span></span> <span data-ttu-id="eb431-154">Bu şablon, VNet oluşturulduğu sırada adres alanını ve alt ağ özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb431-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="eb431-155">[Örnek şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets) geri gidin.</span><span class="sxs-lookup"><span data-stu-id="eb431-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="eb431-156">**azuredeploy-parameters.json** ve **RAW** öğelerine sırayla tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="eb431-157">Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eb431-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="eb431-158">Yeni kaydettiğiniz dosyayı açın ve parametre değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="eb431-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="eb431-159">Senaryoda açıklanan Vnet'i dağıtmak için aşağıdaki aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="eb431-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

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

11. <span data-ttu-id="eb431-160">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eb431-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="eb431-161">PowerShell kullanarak şablonu dağıtmak</span><span class="sxs-lookup"><span data-stu-id="eb431-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="eb431-162">PowerShell kullanarak yüklediğiniz şablonunu dağıtmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="eb431-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="eb431-163">PowerShell'i yükleme ve Azure içindeki adımları tamamlayarak yapılandırma [yükleme ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="eb431-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="eb431-164">Yeni bir kaynak grubu oluşturmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eb431-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="eb431-165">Komut bir kaynak grubu oluşturur *TestRG* içinde *Orta ABD* azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="eb431-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="eb431-166">Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md)’ı ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="eb431-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="eb431-167">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="eb431-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="eb431-168">Yukarıda indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını kullanarak yeni Vnet'i dağıtmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eb431-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="eb431-169">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="eb431-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="eb431-170">Yeni Vnet'in özelliklerini görüntülemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eb431-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="eb431-171">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="eb431-171">Expected output:</span></span>

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

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="eb431-172">Dağıtmak için kullanarak şablonu dağıtmak</span><span class="sxs-lookup"><span data-stu-id="eb431-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="eb431-173">Microsoft tarafından yönetilen bir GitHub deposuna karşıya önceden tanımlanmış Azure Resource Manager şablonları yeniden kullanmak ve topluluğa açık.</span><span class="sxs-lookup"><span data-stu-id="eb431-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="eb431-174">Bu şablonlar Github'dan sınırsız dağıtılabilir veya indirdiğiniz ve gereksinimlerinizi karşılayacak biçimde değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="eb431-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="eb431-175">İki alt ağa sahip VNet oluşturan bir şablonu dağıtmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="eb431-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="eb431-176">Bir tarayıcıdan [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="eb431-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="eb431-177">Şablonları listesini kaydırın ve **101-vnet-two-subnets** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="eb431-178">Aşağıda gösterilen gibi **README.md** dosyası gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="eb431-178">Check the **README.md** file, as shown below.</span></span>

    ![Github’da READEME.md dosyası](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="eb431-180">**Azure’a dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="eb431-181">Gerekiyorsa, Azure oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="eb431-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="eb431-182">**Parametreler** dikey penceresinde, yeni VNet oluşturmak için kullanmak istediğiniz değerleri girip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="eb431-183">Aşağıdaki şekil senaryo için değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="eb431-183">The following figure shows the values for the scenario:</span></span>
   
    ![ARM şablonu parametreleri](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="eb431-185">**Kaynak grubu**’na tıklayıp VNet'e eklenecek kaynak grubunu seçin veya VNet’i yeni bir kaynak grubuna eklemek için **Yeni oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="eb431-186">Kaynak adı verilen yeni bir kaynak grubu için Grup ayarları aşağıdaki şekilde gösterilmiştir **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="eb431-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Kaynak grubu](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="eb431-188">Gerekiyorsa, VNet’inizle ilgili **Abonelik** ve **Konum** ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="eb431-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="eb431-189">VNet’i bir kutucuk olarak görmek istemiyorsanız **Başlangıç panosu**’nda **Başlangıç panosuna sabitlemek** öğesini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="eb431-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="eb431-190">Tıklatın **yasal koşulları**koşullarını okuyun ve tıklatın **satın** kabul edin.</span><span class="sxs-lookup"><span data-stu-id="eb431-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="eb431-191">VNet oluşturmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb431-191">Click **Create** to create the VNet.</span></span>
   
    ![Önizleme portalında dağıtım kutucuğu gönderiliyor](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="eb431-193">Azure portal tıklatın, dağıtım tamamlandıktan sonra **daha fazla hizmet**, türü *sanal ağlar* görüntülenen filtre kutusunda sanal ağlar dikey penceresinde görmek için Sanal Ağları'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eb431-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="eb431-194">Dikey penceresinde tıklayın *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="eb431-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="eb431-195">İçinde *TestVNet* dikey penceresinde tıklatın **alt ağlar** oluşturulan alt ağlar, aşağıdaki resimde gösterildiği gibi görmek için:</span><span class="sxs-lookup"><span data-stu-id="eb431-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![Önizleme portalında VNet oluşturma](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="eb431-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb431-197">Next steps</span></span>

<span data-ttu-id="eb431-198">Nasıl bağlayacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="eb431-198">Learn how to connect:</span></span>

- <span data-ttu-id="eb431-199">Sanal ağ ile sanal makine (VM) bağlantısı için [Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md) veya [Linux VM oluşturma](../virtual-machines/linux/quick-create-portal.md) makalelerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="eb431-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="eb431-200">Makalelerde yer alan adımlarda sanal ağ ve alt ağ oluşturmak yerine var olan sanal ağı ve alt ağı seçerek VM bağlantısı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb431-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="eb431-201">Bir sanal ağı diğer sanal ağlara bağlamak için [Sanal ağları bağlama](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="eb431-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="eb431-202">Bir sanal ağı şirket içi ağa bağlamak için siteden siteye sanal özel ağ (VPN) veya ExpressRoute devresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="eb431-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="eb431-203">Nasıl yapacağınızı öğrenmek için [Siteden siteye VPN kullanarak sanal ağ ile şirket içi ağ arasında bağlantı kurma](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [Bir sanal ağı ExpressRoute devresine bağlama](../expressroute/expressroute-howto-linkvnet-arm.md) makalelerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="eb431-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>

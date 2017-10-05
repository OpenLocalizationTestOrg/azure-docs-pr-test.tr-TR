---
title: "Azure sanal makineleri - PowerShell için birden çok IP adresi | Microsoft Docs"
description: "PowerShell kullanarak bir sanal makine için birden çok IP adresi atama hakkında bilgi edinin | Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="af11f-103">PowerShell kullanarak sanal makineleri için birden çok IP adresi atayın</span><span class="sxs-lookup"><span data-stu-id="af11f-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="af11f-104">Bu makalede PowerShell kullanarak Azure Resource Manager dağıtım modeli sanal makine (VM) oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af11f-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="af11f-105">Birden çok IP adresi Klasik dağıtım modeli aracılığıyla oluşturulan kaynakları atanamaz.</span><span class="sxs-lookup"><span data-stu-id="af11f-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="af11f-106">Azure dağıtım modelleri hakkında daha fazla bilgi için okuma [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="af11f-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="af11f-107"><a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="af11f-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="af11f-108">Adımları birden çok IP adresleriyle VM örneği oluşturmak senaryosunda açıklandığı şekilde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af11f-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="af11f-109">Değişken değerleri, uygulamanız için gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="af11f-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="af11f-110">Bir PowerShell komut istemi açın ve tek bir PowerShell oturumunda bu bölümdeki kalan adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="af11f-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="af11f-111">Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, bölümündeki adımları tamamlamanız [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) makale.</span><span class="sxs-lookup"><span data-stu-id="af11f-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="af11f-112">Oturum açma ile hesabınızı `login-azurermaccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="af11f-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="af11f-113">Değiştir *myResourceGroup* ve *westus* bir adı ve seçtiğiniz konum.</span><span class="sxs-lookup"><span data-stu-id="af11f-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="af11f-114">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af11f-114">Create a resource group.</span></span> <span data-ttu-id="af11f-115">Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="af11f-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="af11f-116">Kaynak grubu ile aynı konumda bir sanal ağ (VNet) ve alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="af11f-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="af11f-117">Bir ağ güvenlik grubu (NSG) ve bir kural oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af11f-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="af11f-118">NSG gelen ve giden kuralları kullanarak VM güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="af11f-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="af11f-119">Bu durumda, bağlantı noktası 3389 için gelen masaüstü bağlantılarına izin veren bir gelen kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="af11f-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="af11f-120">Birincil NIC IP yapılandırmasını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="af11f-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="af11f-121">Önceden tanımlanmış değer kullanmadıysanız, oluşturduğunuz alt ağdaki geçerli bir adrese 10.0.0.4 değiştirin.</span><span class="sxs-lookup"><span data-stu-id="af11f-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="af11f-122">Statik bir IP adresi atamadan önce zaten kullanımda olmadığı ilk onaylamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="af11f-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="af11f-123">Aşağıdaki komutu girin `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="af11f-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="af11f-124">Adres bulunup bulunmadığını çıktıyı döndürür *doğru*.</span><span class="sxs-lookup"><span data-stu-id="af11f-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="af11f-125">Çıktıyı döndürür, kullanılabilir değilse, *False* ve kullanılabilir adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="af11f-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="af11f-126">Aşağıdaki komutlarda **< Değiştir-ile-bilgisayarınızı-benzersiz-adı > kullanmak için benzersiz DNS adı ile değiştirin.**</span><span class="sxs-lookup"><span data-stu-id="af11f-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="af11f-127">Bir Azure bölgesi içindeki tüm ortak IP adresleri arasında adının benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="af11f-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="af11f-128">Bu isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="af11f-128">This is an optional parameter.</span></span> <span data-ttu-id="af11f-129">Yalnızca genel IP adresini kullanarak VM bağlanmak isterseniz kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="af11f-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="af11f-130">Birden fazla IP yapılandırması için bir NIC atadığınızda, bir yapılandırma olarak atanması gerekir *-birincil*.</span><span class="sxs-lookup"><span data-stu-id="af11f-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af11f-131">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="af11f-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="af11f-132">IP adresi fiyatlandırma hakkında daha fazla bilgi için okuma [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="af11f-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="af11f-133">Bir abonelikte kullanılabilir genel IP adresleri sayısına bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="af11f-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="af11f-134">Sınırlar hakkında daha fazla bilgi için [Azure limitleri](../azure-subscription-service-limits.md#networking-limits) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="af11f-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="af11f-135">NIC ikincil IP yapılandırmalarını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="af11f-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="af11f-136">Ekleyebilir veya gerektiği gibi yapılandırmaları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af11f-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="af11f-137">Her IP yapılandırması atanan özel bir IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af11f-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="af11f-138">Her yapılandırma isteğe bağlı olarak atanmış bir genel IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="af11f-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="af11f-139">NIC oluşturun ve ona üç IP yapılandırmaları ilişkilendirin:</span><span class="sxs-lookup"><span data-stu-id="af11f-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="af11f-140">Bu makalede bir NIC'e atanmış tüm yapılandırmalar olsa, VM'ye bağlı her NIC birden çok IP yapılandırmaları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af11f-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="af11f-141">Bir VM ile birden çok NIC oluşturmayı öğrenmek için okuma [bir VM ile birden çok NIC oluşturma](virtual-network-deploy-multinic-arm-ps.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="af11f-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="af11f-142">VM, aşağıdaki komutları girerek oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="af11f-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="af11f-143">İşletim sisteminiz için adımları tamamlayarak VM işletim sistemine özel IP adresleri ekleme [eklemek IP adresleri bir VM işletim sistemine](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="af11f-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="af11f-144">Genel IP adreslerine işletim sistemine eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="af11f-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="af11f-145"><a name="add"></a>Bir VM için IP adreslerini ekleyin</span><span class="sxs-lookup"><span data-stu-id="af11f-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="af11f-146">Adımları tamamlayarak bir NIC'ye özel ve genel IP adresleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af11f-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="af11f-147">Aşağıdaki bölümlerde yer alan örnekler, zaten bir VM açıklanan üç IP yapılandırmaya sahip olduğunu varsayın [senaryo](#Scenario) Bu makale, ancak gerekli değildir, yapın.</span><span class="sxs-lookup"><span data-stu-id="af11f-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="af11f-148">Bir PowerShell komut istemi açın ve tek bir PowerShell oturumunda bu bölümdeki kalan adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="af11f-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="af11f-149">Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, bölümündeki adımları tamamlamanız [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) makale.</span><span class="sxs-lookup"><span data-stu-id="af11f-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="af11f-150">Aşağıdaki $Variables "değerler" adı IP adresine eklemek istediğiniz NIC ve kaynak grubu ve NIC bulunmaktadır konumu ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="af11f-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="af11f-151">İstediğiniz değiştirmek için aşağıdaki komutları girin NIC adını bilmiyorsanız, önceki değişkenlerin değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="af11f-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="af11f-152">Bir değişken oluşturun ve aşağıdaki komutu yazarak mevcut NIC'in ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="af11f-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="af11f-153">Aşağıdaki komutlarda değiştirme *MyVNet* ve *MySubnet* VNet ve NIC bağlı alt ağ adları için.</span><span class="sxs-lookup"><span data-stu-id="af11f-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="af11f-154">NIC bağlı VNet ve alt ağ nesneleri almak için komutları girin:</span><span class="sxs-lookup"><span data-stu-id="af11f-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="af11f-155">NIC bağlı sanal ağ veya alt ağ adını bilmiyorsanız, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="af11f-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="af11f-156">Aşağıdaki örnek çıkış benzer bir metin çıktıda arayın:</span><span class="sxs-lookup"><span data-stu-id="af11f-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="af11f-157">Bu çıkışı *MyVnet* VNet olduğu ve *MySubnet* NIC bağlı alt ağ.</span><span class="sxs-lookup"><span data-stu-id="af11f-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="af11f-158">Gereksinimlerinize göre aşağıdaki bölümlerden birindeki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="af11f-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="af11f-159">**Özel bir IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="af11f-159">**Add a private IP address**</span></span>

    <span data-ttu-id="af11f-160">Özel bir IP adresi için bir NIC eklemeniz için bir IP yapılandırması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="af11f-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="af11f-161">Aşağıdaki komut bir yapılandırma 10.0.0.7 ile bir statik IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af11f-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="af11f-162">Statik bir IP adresi belirtirken, alt ağ için kullanılmayan bir adres olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af11f-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="af11f-163">Kullanılabilir girerek olduğundan emin olmak için adresi önce test önerilir `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` komutu.</span><span class="sxs-lookup"><span data-stu-id="af11f-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="af11f-164">IP adresi bulunup bulunmadığını çıktıyı döndürür *doğru*.</span><span class="sxs-lookup"><span data-stu-id="af11f-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="af11f-165">Çıktıyı döndürür, kullanılabilir değilse, *yanlış*ve kullanılabilir adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="af11f-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="af11f-166">Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af11f-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="af11f-167">İşletim sisteminiz için adımları tamamlayarak VM işletim sistemine özel IP adresi Ekle [eklemek IP adresleri bir VM işletim sistemine](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="af11f-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="af11f-168">**Bir ortak IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="af11f-168">**Add a public IP address**</span></span>

    <span data-ttu-id="af11f-169">Bir ortak IP adresi, yeni bir IP yapılandırması ya da var olan bir IP yapılandırması için genel bir IP adresi kaynağı ilişkilendirerek eklenir.</span><span class="sxs-lookup"><span data-stu-id="af11f-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="af11f-170">Gereksinim duyduğunuz kadar aşağıdaki bölümlerde birindeki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="af11f-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af11f-171">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="af11f-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="af11f-172">IP adresi fiyatlandırma hakkında daha fazla bilgi için okuma [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="af11f-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="af11f-173">Bir abonelikte kullanılabilir genel IP adresleri sayısına bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="af11f-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="af11f-174">Sınırlar hakkında daha fazla bilgi için [Azure limitleri](../azure-subscription-service-limits.md#networking-limits) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="af11f-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="af11f-175">**Yeni bir IP yapılandırması için genel IP adresi kaynağı ilişkilendirme**</span><span class="sxs-lookup"><span data-stu-id="af11f-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="af11f-176">Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="af11f-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="af11f-177">Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af11f-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="af11f-178">Yeni bir tane oluşturmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="af11f-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="af11f-179">Özel bir statik IP adresi ile ilişkili yeni bir IP yapılandırması oluşturmak için *myPublicIp3* genel IP adresi kaynak, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="af11f-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="af11f-180">**Var olan bir IP yapılandırması için genel IP adresi kaynağı ilişkilendirme**</span><span class="sxs-lookup"><span data-stu-id="af11f-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="af11f-181">Yalnızca genel IP adresi kaynağı zaten ilişkili olmayan bir IP yapılandırmasıyla ilişkilendirilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="af11f-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="af11f-182">Aşağıdaki komutu girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="af11f-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="af11f-183">Aşağıdakine benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="af11f-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="af11f-184">Bu yana **Publicıpaddress** sütunu için *IpConfig 3* olduğundan, hiçbir ortak IP adresi kaynağı ilişkili şu anda boştur.</span><span class="sxs-lookup"><span data-stu-id="af11f-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="af11f-185">Mevcut bir ortak IP adresi kaynağı IpConfig-3'e ekleyin veya oluşturmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="af11f-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="af11f-186">Adlı varolan IP yapılandırması için genel IP adresi kaynağı ilişkilendirmek için aşağıdaki komutu girin *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="af11f-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="af11f-187">NIC yeni IP yapılandırması ile aşağıdaki komutu girerek ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="af11f-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="af11f-188">Özel IP adresleri ve aşağıdaki komutu girerek NIC'ye atanan ortak IP adresi kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="af11f-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="af11f-189">İşletim sisteminiz için adımları tamamlayarak VM işletim sistemine özel IP adresi Ekle [eklemek IP adresleri bir VM işletim sistemine](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="af11f-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="af11f-190">Genel IP adresi işletim sistemine eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="af11f-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]

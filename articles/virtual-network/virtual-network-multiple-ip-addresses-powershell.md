---
title: Azure sanal makineleri - PowerShell aaaMultiple IP adreslerinin | Microsoft Docs
description: "Nasıl tooassign birden çok IP adresleri öğrenin PowerShell kullanarak tooa sanal makine | Resource Manager."
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
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="0e863-103">PowerShell kullanarak toovirtual makineler birden çok IP adresi atayın</span><span class="sxs-lookup"><span data-stu-id="0e863-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="0e863-104">Bu makalede nasıl toocreate sanal makineye (VM) üzerinden hello Azure Resource Manager dağıtım modeli PowerShell kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e863-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="0e863-105">Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz.</span><span class="sxs-lookup"><span data-stu-id="0e863-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="0e863-106">Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="0e863-107"><a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e863-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="0e863-108">izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e863-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="0e863-109">Değişken değerleri, uygulamanız için gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0e863-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="0e863-110">Bir PowerShell komut istemi açın ve tam hello kalan tek bir PowerShell oturumunda bu bölümdeki adımları.</span><span class="sxs-lookup"><span data-stu-id="0e863-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="0e863-111">Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, tam hello hello adımları [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="0e863-112">Oturum açma tooyour hello hesabıyla `login-azurermaccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="0e863-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="0e863-113">Değiştir *myResourceGroup* ve *westus* bir adı ve seçtiğiniz konum.</span><span class="sxs-lookup"><span data-stu-id="0e863-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="0e863-114">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e863-114">Create a resource group.</span></span> <span data-ttu-id="0e863-115">Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="0e863-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="0e863-116">Bir sanal ağ (VNet) ve alt ağ hello oluşturmak hello kaynak grubu ile aynı konumda:</span><span class="sxs-lookup"><span data-stu-id="0e863-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

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

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="0e863-117">Bir ağ güvenlik grubu (NSG) ve bir kural oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e863-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="0e863-118">Merhaba NSG korur hello VM gelen ve giden kurallarını kullanma.</span><span class="sxs-lookup"><span data-stu-id="0e863-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="0e863-119">Bu durumda, bağlantı noktası 3389 için gelen masaüstü bağlantılarına izin veren bir gelen kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0e863-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="0e863-120">Merhaba NIC Hello birincil IP yapılandırmasını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="0e863-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="0e863-121">Değişiklik 10.0.0.4 tooa oluşturduğunuz, önceden tanımlanmış hello değer kullanmadıysanız hello alt ağdaki geçerli bir adresi.</span><span class="sxs-lookup"><span data-stu-id="0e863-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="0e863-122">Statik bir IP adresi atamadan önce zaten kullanımda olmadığı ilk onaylamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="0e863-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="0e863-123">Merhaba komutu girin `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="0e863-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="0e863-124">Başlangıç adresi varsa, hello döndürür çıktı *doğru*.</span><span class="sxs-lookup"><span data-stu-id="0e863-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="0e863-125">Kullanılabilir durumda değilse, hello döndürür çıktı *False* ve kullanılabilir adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="0e863-126">Komutları, aşağıdaki hello içinde **< Değiştir-ile-bilgisayarınızı-benzersiz-adı > merhaba benzersiz DNS adı toouse ile değiştirin.**</span><span class="sxs-lookup"><span data-stu-id="0e863-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="0e863-127">bir Azure bölgesi içindeki tüm ortak IP adresleri arasında Hello adının benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e863-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="0e863-128">Bu isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="0e863-128">This is an optional parameter.</span></span> <span data-ttu-id="0e863-129">Tooconnect toohello VM yalnızca istiyorsanız kaldırılması hello ortak IP adresi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0e863-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="0e863-130">Birden çok IP yapılandırmaları tooa NIC atadığınızda, bir yapılandırma hello atanmalıdır *-birincil*.</span><span class="sxs-lookup"><span data-stu-id="0e863-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e863-131">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="0e863-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="0e863-132">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="0e863-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="0e863-133">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e863-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="0e863-134">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="0e863-135">Merhaba NIC için ikincil IP yapılandırmaları Hello tanımlayın</span><span class="sxs-lookup"><span data-stu-id="0e863-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="0e863-136">Ekleyebilir veya gerektiği gibi yapılandırmaları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e863-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="0e863-137">Her IP yapılandırması atanan özel bir IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0e863-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="0e863-138">Her yapılandırma isteğe bağlı olarak atanmış bir genel IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e863-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
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

8. <span data-ttu-id="0e863-139">Merhaba NIC oluşturun ve hello üç IP yapılandırmaları tooit ilişkilendirin:</span><span class="sxs-lookup"><span data-stu-id="0e863-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="0e863-140">Bu makalede tooone NIC atanmış tüm yapılandırmalar olsa, birden çok IP yapılandırmaları tooevery bağlı NIC toohello VM atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e863-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="0e863-141">nasıl toocreate birden çok NIC ile VM okuma toolearn hello [bir VM ile birden çok NIC oluşturma](virtual-network-deploy-multinic-arm-ps.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="0e863-142">Merhaba VM hello aşağıdaki komutları girerek oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e863-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
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
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="0e863-143">Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="0e863-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="0e863-144">Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="0e863-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="0e863-145"><a name="add"></a>IP adreslerini tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="0e863-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="0e863-146">Özel ve genel IP adresleri tooa NIC izleyin hello adımları tamamlayarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e863-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="0e863-147">Merhaba hello bölümleri aşağıdaki örneklerde, zaten bir VM hello açıklanan hello üç IP yapılandırmasına sahip olduğunu varsayın [senaryo](#Scenario) Bu makale, ancak gerekli değildir, yapın.</span><span class="sxs-lookup"><span data-stu-id="0e863-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="0e863-148">Bir PowerShell komut istemi açın ve tam hello kalan tek bir PowerShell oturumunda bu bölümdeki adımları.</span><span class="sxs-lookup"><span data-stu-id="0e863-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="0e863-149">Zaten yüklü ve yapılandırılmış PowerShell sahip değilseniz, tam hello hello adımları [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="0e863-150">Merhaba "değerini" hello NIC bulunmaktadır tooadd IP adresi tooand hello kaynak grubunu ve konumu hello istediğiniz NIC $Variables toohello adı aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e863-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="0e863-151">Merhaba toochange istediğiniz NIC hello adını bilmiyorsanız, komutları aşağıdaki hello girin ve ardından hello önceki değişkenlerin hello değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e863-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="0e863-152">Bir değişken oluşturun ve NIC hello aşağıdaki komutu yazarak varolan toohello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0e863-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="0e863-153">Aşağıdaki komutları hello değiştirme *MyVNet* ve *MySubnet* NIC bağlı hello VNet ve alt ağ hello toohello adları.</span><span class="sxs-lookup"><span data-stu-id="0e863-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="0e863-154">NIC bağlı hello komutları tooretrieve hello VNet ve alt ağ nesneleri hello girin:</span><span class="sxs-lookup"><span data-stu-id="0e863-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="0e863-155">NIC bağlı hello VNet veya alt ağ adı hello bilmiyorsanız, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="0e863-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="0e863-156">Merhaba çıktısında metin benzer toohello örnek çıktı aşağıdaki için bakın:</span><span class="sxs-lookup"><span data-stu-id="0e863-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="0e863-157">Bu çıkışı *MyVnet* hello VNet olduğu ve *MySubnet* hello alt hello NIC bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="0e863-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="0e863-158">Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="0e863-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="0e863-159">**Özel bir IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="0e863-159">**Add a private IP address**</span></span>

    <span data-ttu-id="0e863-160">özel bir IP adresi tooa NIC tooadd, bir IP yapılandırması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e863-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="0e863-161">Merhaba aşağıdaki komutu bir yapılandırma 10.0.0.7 ile bir statik IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e863-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="0e863-162">Statik bir IP adresi belirtirken, hello alt ağ için kullanılmayan bir adres olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0e863-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="0e863-163">Başlangıç adresi tooensure bulunur hello girerek önce test önerilir `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` komutu.</span><span class="sxs-lookup"><span data-stu-id="0e863-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="0e863-164">Başlangıç IP adresi varsa, hello döndürür çıktı *doğru*.</span><span class="sxs-lookup"><span data-stu-id="0e863-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="0e863-165">Kullanılabilir durumda değilse, hello döndürür çıktı *yanlış*ve kullanılabilir adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="0e863-166">Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e863-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="0e863-167">İşletim sisteminizin hello hello adımları tamamlayarak Hello özel IP adresi toohello VM işletim sistemi Ekle [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="0e863-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="0e863-168">**Bir ortak IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="0e863-168">**Add a public IP address**</span></span>

    <span data-ttu-id="0e863-169">Bir ortak IP adresi, bir ortak IP adresi kaynak tooeither yeni bir IP yapılandırması veya var olan IP yapılandırmasını ilişkilendirerek eklenir.</span><span class="sxs-lookup"><span data-stu-id="0e863-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="0e863-170">Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="0e863-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e863-171">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="0e863-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="0e863-172">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="0e863-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="0e863-173">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e863-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="0e863-174">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e863-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="0e863-175">**Merhaba ortak IP adresi kaynak tooa yeni IP yapılandırmasını ilişkilendirin**</span><span class="sxs-lookup"><span data-stu-id="0e863-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="0e863-176">Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0e863-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="0e863-177">Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e863-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="0e863-178">toocreate yeni bir hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="0e863-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="0e863-179">Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIp3* genel IP adresi kaynak, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="0e863-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="0e863-180">**Merhaba ortak IP adresi kaynak tooan mevcut IP yapılandırmasını ilişkilendirin**</span><span class="sxs-lookup"><span data-stu-id="0e863-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="0e863-181">Genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e863-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="0e863-182">Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e863-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="0e863-183">Çıktı benzer toohello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="0e863-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="0e863-184">Merhaba itibaren **Publicıpaddress** sütunu için *IpConfig 3* olduğundan, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit boştur.</span><span class="sxs-lookup"><span data-stu-id="0e863-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="0e863-185">Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="0e863-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="0e863-186">Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="0e863-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="0e863-187">Merhaba NIC hello yeni IP yapılandırması ile komutu aşağıdaki hello girerek ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0e863-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="0e863-188">Görünüm hello özel IP adresleri ve ortak IP adresi atanmış kaynaklar toohello girerek NIC hello komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0e863-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="0e863-189">İşletim sisteminizin hello hello adımları tamamlayarak Hello özel IP adresi toohello VM işletim sistemi Ekle [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="0e863-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="0e863-190">Merhaba ortak IP adresi toohello işletim sistemi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="0e863-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]

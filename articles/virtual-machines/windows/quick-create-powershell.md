---
title: "aaaAzure hızlı başlangıç - Windows VM PowerShell oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde bir Windows sanal makineleri PowerShell ile toocreate öğrenin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="a776d-103">PowerShell ile Windows sanal makinesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a776d-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="a776d-104">Hello Azure PowerShell modülü kullanılan toocreate olan ve hello PowerShell komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="a776d-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="a776d-105">PowerShell toocreate ve Windows Server 2016 çalıştıran Azure sanal makine kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="a776d-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="a776d-106">Dağıtım tamamlandıktan sonra biz toohello sunucusuna bağlanmak ve IIS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a776d-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="a776d-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="a776d-108">Bu hızlı başlangıç hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="a776d-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a776d-109">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="a776d-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="a776d-110">Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a776d-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="a776d-111">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="a776d-111">Log in tooAzure</span></span>

<span data-ttu-id="a776d-112">Tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a776d-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="a776d-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a776d-113">Create resource group</span></span>

<span data-ttu-id="a776d-114">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) ile yeni bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="a776d-115">Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a776d-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="a776d-116">Ağ kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a776d-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="a776d-117">Bir sanal ağ, alt ağ ve genel IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="a776d-118">Bu kaynaklar kullanılan tooprovide ağ bağlantısı toohello sanal makine olan ve toohello bağlamak Internet.</span><span class="sxs-lookup"><span data-stu-id="a776d-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="a776d-119">Bir ağ güvenliği grubu ve bir ağ güvenliği grup kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="a776d-120">Merhaba ağ güvenlik grubu gelen ve giden kuralları kullanarak hello sanal makine güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a776d-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="a776d-121">Bu durumda, bağlantı noktası 3389 için gelen masaüstü bağlantılarına izin veren bir gelen kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a776d-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="a776d-122">Ayrıca toocreate bir gelen kuralı gelen web trafiği sağlayan için bağlantı noktası 80, istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a776d-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="a776d-123">Merhaba sanal makine için bir ağ kartı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="a776d-124">Bir ağ kartı ile oluşturmak [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="a776d-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="a776d-125">Merhaba ağ kartı hello sanal makine tooa alt ağ, ağ güvenlik grubu ve genel IP adresine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a776d-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="a776d-126">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="a776d-126">Create virtual machine</span></span>

<span data-ttu-id="a776d-127">Sanal makine yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="a776d-128">Bu yapılandırma, bir sanal makine görüntüsü, boyutu ve kimlik doğrulama yapılandırması gibi hello sanal makine dağıtımı sırasında kullanılan hello ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a776d-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="a776d-129">Bu adımı çalıştırırken kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="a776d-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="a776d-130">Girdiğiniz hello değerleri hello kullanıcı adı ve parola hello sanal makine için olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a776d-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="a776d-131">Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a776d-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="a776d-132">Toovirtual makineyi bağlayın</span><span class="sxs-lookup"><span data-stu-id="a776d-132">Connect toovirtual machine</span></span>

<span data-ttu-id="a776d-133">Merhaba dağıtım tamamlandıktan sonra bir Uzak Masaüstü Bağlantısı ile Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a776d-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="a776d-134">Kullanım hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn hello genel IP adresi hello sanal makinenin komutu.</span><span class="sxs-lookup"><span data-stu-id="a776d-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="a776d-135">Tarayıcı tootest web bağlantınızı bir sonraki adımda ile tooit bağlanabilmesi için bu IP adresini not alın.</span><span class="sxs-lookup"><span data-stu-id="a776d-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="a776d-136">Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu.</span><span class="sxs-lookup"><span data-stu-id="a776d-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="a776d-137">Başlangıç IP adresi ile hello yerine *Publicıpaddress* sanal makinenizin.</span><span class="sxs-lookup"><span data-stu-id="a776d-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="a776d-138">İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="a776d-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="a776d-139">PowerShell kullanarak IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="a776d-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="a776d-140">Toohello Azure VM'de oturum, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a776d-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="a776d-141">PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a776d-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="a776d-142">Görünüm hello IIS Karşılama sayfası</span><span class="sxs-lookup"><span data-stu-id="a776d-142">View hello IIS welcome page</span></span>

<span data-ttu-id="a776d-143">IIS yüklü ve bağlantı noktası 80, VM'den hello Internet üzerinde şimdi açık ile seçim tooview hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a776d-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="a776d-144">Emin toouse hello olması *Publicıpaddress* toovisit hello varsayılan sayfa belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a776d-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="a776d-146">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="a776d-146">Clean up resources</span></span>

<span data-ttu-id="a776d-147">Artık gerektiğinde Merhaba kullanabilirsiniz [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="a776d-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a776d-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a776d-148">Next steps</span></span>

<span data-ttu-id="a776d-149">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="a776d-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="a776d-150">Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Windows VM'ler için devam edin.</span><span class="sxs-lookup"><span data-stu-id="a776d-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a776d-151">Azure Windows sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="a776d-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

---
title: "aaaAzure hızlı başlangıç - VM PowerShell oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde Linux sanal makineleri PowerShell ile toocreate öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="4aba4-103">PowerShell ile Linux sanal makinesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aba4-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="4aba4-104">Hello Azure PowerShell modülü kullanılan toocreate olan ve hello PowerShell komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="4aba4-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="4aba4-105">Ubuntu server çalıştıran bir sanal makine Hello Azure PowerShell modülü toodeploy kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="4aba4-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="4aba4-106">Merhaba sunucu dağıtıldığında, bir SSH bağlantısı oluşturulur ve bir NGINX Web sunucusu yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4aba4-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="4aba4-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="4aba4-108">Bu hızlı başlangıç hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="4aba4-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="4aba4-109">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="4aba4-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="4aba4-110">Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="4aba4-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="4aba4-111">Son olarak, bir genel SSH anahtarı hello adla *id_rsa.pub* hello depolanan toobe gereken *.ssh* Windows kullanıcı profilinizin dizin.</span><span class="sxs-lookup"><span data-stu-id="4aba4-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="4aba4-112">Azure için SSH anahtarları oluşturma hakkında ayrıntılı bilgi için bkz. [Azure için SSH anahtarları oluşturma](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4aba4-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="4aba4-113">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="4aba4-113">Log in tooAzure</span></span>

<span data-ttu-id="4aba4-114">Tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="4aba4-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="4aba4-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aba4-115">Create resource group</span></span>

<span data-ttu-id="4aba4-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) ile yeni bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="4aba4-117">Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="4aba4-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="4aba4-118">Ağ kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aba4-118">Create networking resources</span></span>

<span data-ttu-id="4aba4-119">Bir sanal ağ, alt ağ ve genel IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="4aba4-120">Bu kaynaklar kullanılan tooprovide ağ bağlantısı toohello sanal makine olan ve toohello bağlamak Internet.</span><span class="sxs-lookup"><span data-stu-id="4aba4-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="4aba4-121">Bir ağ güvenliği grubu ve bir ağ güvenliği grup kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="4aba4-122">Merhaba ağ güvenlik grubu gelen ve giden kuralları kullanarak hello sanal makine güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="4aba4-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="4aba4-123">Bu durumda, bağlantı noktası 22 için gelen SSH bağlantılarına izin veren bir gelen kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4aba4-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="4aba4-124">Ayrıca toocreate bir gelen kuralı gelen web trafiği sağlayan için bağlantı noktası 80, istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4aba4-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="4aba4-125">Bir ağ kartı ile oluşturmak [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="4aba4-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="4aba4-126">Merhaba ağ kartı hello sanal makine tooa alt ağ, ağ güvenlik grubu ve genel IP adresine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4aba4-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="4aba4-127">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="4aba4-127">Create virtual machine</span></span>

<span data-ttu-id="4aba4-128">Sanal makine yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="4aba4-129">Bu yapılandırma, bir sanal makine görüntüsü, boyutu ve kimlik doğrulama yapılandırması gibi hello sanal makine dağıtımı sırasında kullanılan hello ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4aba4-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="4aba4-130">Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="4aba4-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="4aba4-131">Toovirtual makineyi bağlayın</span><span class="sxs-lookup"><span data-stu-id="4aba4-131">Connect toovirtual machine</span></span>

<span data-ttu-id="4aba4-132">Merhaba dağıtım tamamlandıktan sonra bir SSH bağlantısı ile Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aba4-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="4aba4-133">Kullanım hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn hello genel IP adresi hello sanal makinenin komutu.</span><span class="sxs-lookup"><span data-stu-id="4aba4-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="4aba4-134">SSH yüklü bir sistemden tooconnect toohello sanal makine kullanılan hello şu komutu.</span><span class="sxs-lookup"><span data-stu-id="4aba4-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="4aba4-135">Windows üzerinde çalışıyorsanız [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) kullanılan toocreate hello bağlantı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4aba4-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="4aba4-136">İstendiğinde, hello oturum açma kullanıcı adı. *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="4aba4-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="4aba4-137">Bir parola SSH anahtarları oluşturma sırasında girilen, bu da tooenter gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aba4-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="4aba4-138">NGINX yükleme</span><span class="sxs-lookup"><span data-stu-id="4aba4-138">Install NGINX</span></span>

<span data-ttu-id="4aba4-139">Kullanım hello aşağıdaki komut dosyası tooupdate paket kaynaklarını bash ve hello son NGINX paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4aba4-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="4aba4-140">Merhaba NGIX Karşılama sayfasını görüntüle</span><span class="sxs-lookup"><span data-stu-id="4aba4-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="4aba4-141">Yüklü NGINX ve bağlantı noktası 80, VM'den hello Internet - üzerinde şimdi açık seçim tooview hello varsayılan NGINX Hoş Geldiniz sayfasını bir web tarayıcısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aba4-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="4aba4-142">Toovisit hello varsayılan sayfa belgelenen emin toouse hello genel IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="4aba4-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="4aba4-144">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="4aba4-144">Clean up resources</span></span>

<span data-ttu-id="4aba4-145">Artık gerektiğinde Merhaba kullanabilirsiniz [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="4aba4-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4aba4-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4aba4-146">Next steps</span></span>

<span data-ttu-id="4aba4-147">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="4aba4-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="4aba4-148">Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Linux VM'ler için devam edin.</span><span class="sxs-lookup"><span data-stu-id="4aba4-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4aba4-149">Azure Linux sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="4aba4-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

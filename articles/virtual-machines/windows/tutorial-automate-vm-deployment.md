---
title: aaaCustomize Azure Windows VM | Microsoft Docs
description: "Toouse nasıl hello özel betik uzantısı ve anahtar kasası toocustomize azure'da Windows VM öğrenin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="9e874-103">Nasıl toocustomize azure'da Windows sanal makine</span><span class="sxs-lookup"><span data-stu-id="9e874-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="9e874-104">hızlı ve tutarlı bir şekilde, tür Otomasyon tooconfigure sanal makineleri (VM'ler) genellikle istenen.</span><span class="sxs-lookup"><span data-stu-id="9e874-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="9e874-105">Ortak bir yaklaşım toocustomize Windows VM toouse olan [için özel betik uzantısı Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="9e874-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="9e874-106">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e874-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e874-107">Merhaba özel betik uzantısının tooinstall IIS kullanın</span><span class="sxs-lookup"><span data-stu-id="9e874-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="9e874-108">Merhaba özel betik uzantısı kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e874-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="9e874-109">Merhaba uzantısı uygulandıktan sonra çalışan bir IIS sitesi görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="9e874-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="9e874-110">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="9e874-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="9e874-111">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="9e874-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="9e874-112">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9e874-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="9e874-113">Özel betik uzantısı genel bakış</span><span class="sxs-lookup"><span data-stu-id="9e874-113">Custom script extension overview</span></span>
<span data-ttu-id="9e874-114">Merhaba özel betik uzantısının indirir ve Azure Vm'lerinde komut dosyaları çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9e874-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="9e874-115">Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi.</span><span class="sxs-lookup"><span data-stu-id="9e874-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="9e874-116">Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan.</span><span class="sxs-lookup"><span data-stu-id="9e874-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="9e874-117">Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9e874-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="9e874-118">Merhaba özel betik uzantısı, Windows ve Linux VM'ler ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e874-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="9e874-119">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e874-119">Create virtual machine</span></span>
<span data-ttu-id="9e874-120">Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="9e874-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="9e874-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="9e874-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="9e874-122">Yönetici olan hello VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="9e874-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="9e874-123">Oluşturabileceğiniz artık VM ile Merhaba [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="9e874-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="9e874-124">Merhaba aşağıdaki örnek gerekli hello sanal ağ bileşenleri hello işletim sistemi yapılandırması ve ardından adlı bir VM oluşturur *myVM*:</span><span class="sxs-lookup"><span data-stu-id="9e874-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="9e874-125">Merhaba kaynaklar ve oluşturulan VM toobe için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="9e874-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="9e874-126">IIS yükleme otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="9e874-126">Automate IIS install</span></span>
<span data-ttu-id="9e874-127">Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı.</span><span class="sxs-lookup"><span data-stu-id="9e874-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="9e874-128">Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu ve ardından güncelleştirmeleri hello *Default.htm* sayfa tooshow hello hello VM konak adı:</span><span class="sxs-lookup"><span data-stu-id="9e874-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="9e874-129">Sınama web sitesi</span><span class="sxs-lookup"><span data-stu-id="9e874-129">Test web site</span></span>
<span data-ttu-id="9e874-130">Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="9e874-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="9e874-131">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="9e874-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="9e874-132">Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e874-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="9e874-133">Merhaba Web sitesi gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:</span><span class="sxs-lookup"><span data-stu-id="9e874-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Çalışan IIS Web sitesi](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="9e874-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e874-135">Next steps</span></span>

<span data-ttu-id="9e874-136">Bu öğreticide, bir VM'ye IIS yüklemeniz hello otomatik.</span><span class="sxs-lookup"><span data-stu-id="9e874-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="9e874-137">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="9e874-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e874-138">Merhaba özel betik uzantısının tooinstall IIS kullanın</span><span class="sxs-lookup"><span data-stu-id="9e874-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="9e874-139">Merhaba özel betik uzantısı kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e874-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="9e874-140">Merhaba uzantısı uygulandıktan sonra çalışan bir IIS sitesi görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="9e874-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="9e874-141">Toohello sonraki öğretici toolearn nasıl ilerlemek toocreate özel VM görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9e874-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e874-142">Özel VM görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e874-142">Create custom VM images</span></span>](./tutorial-custom-images.md)

---
title: "Azure PowerShell Betiği örnek - IIS | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - IIS"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1f2f6301267c43919efc298573b6239cacf39239
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="61220-103">PowerShell ile bir IIS VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="61220-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="61220-104">Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur ve ardından IIS yüklemek için Azure sanal makine özel betik uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="61220-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="61220-105">Betiği çalıştırdıktan sonra sanal makine genel IP adresi varsayılan IIS Web sitesinin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="61220-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="61220-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="61220-106">Sample script</span></span>

<span data-ttu-id="61220-107">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "VM IIS oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="61220-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="61220-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="61220-108">Clean up deployment</span></span> 

<span data-ttu-id="61220-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="61220-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="61220-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="61220-110">Script explanation</span></span>

<span data-ttu-id="61220-111">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="61220-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="61220-112">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="61220-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="61220-113">Komut</span><span class="sxs-lookup"><span data-stu-id="61220-113">Command</span></span> | <span data-ttu-id="61220-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="61220-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61220-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61220-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61220-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61220-117">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="61220-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61220-118">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-118">Creates a subnet configuration.</span></span> <span data-ttu-id="61220-119">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61220-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="61220-120">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="61220-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="61220-121">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="61220-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="61220-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="61220-123">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="61220-124">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="61220-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="61220-125">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="61220-126">Bu yapılandırma, NSG oluşturulduğunda bir NSG kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61220-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="61220-127">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="61220-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="61220-128">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="61220-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61220-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61220-130">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="61220-130">Gets subnet information.</span></span> <span data-ttu-id="61220-131">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61220-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="61220-132">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="61220-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="61220-133">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="61220-134">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="61220-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="61220-135">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61220-135">Creates a VM configuration.</span></span> <span data-ttu-id="61220-136">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="61220-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="61220-137">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61220-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="61220-138">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="61220-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="61220-139">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61220-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="61220-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="61220-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="61220-141">VM uzantısı sanal makineye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61220-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="61220-142">Bu örnekte, özel betik uzantısının IIS yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61220-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="61220-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61220-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="61220-144">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="61220-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61220-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61220-145">Next steps</span></span>

<span data-ttu-id="61220-146">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61220-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="61220-147">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61220-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

---
title: "Azure PowerShell Betiği örnek - bir Linux VM oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2bf1031e5481bbb662873f57904e889a2908e692
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="755c8-103">PowerShell ile tam olarak yapılandırılmış bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="755c8-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="755c8-104">Bu komut dosyasını bir Ubuntu işletim sistemine sahip bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="755c8-105">Betiği çalıştırdıktan sonra sanal makinenin SSH üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="755c8-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="755c8-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="755c8-106">Sample script</span></span>

<span data-ttu-id="755c8-107">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "ayrıntılı VM oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="755c8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="755c8-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="755c8-108">Clean up deployment</span></span> 

<span data-ttu-id="755c8-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="755c8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="755c8-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="755c8-110">Script explanation</span></span>

<span data-ttu-id="755c8-111">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="755c8-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="755c8-112">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="755c8-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="755c8-113">Komut</span><span class="sxs-lookup"><span data-stu-id="755c8-113">Command</span></span> | <span data-ttu-id="755c8-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="755c8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="755c8-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="755c8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="755c8-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="755c8-117">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="755c8-118">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-118">Creates a subnet configuration.</span></span> <span data-ttu-id="755c8-119">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="755c8-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="755c8-120">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="755c8-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="755c8-121">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="755c8-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="755c8-123">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="755c8-124">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="755c8-125">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="755c8-126">Bu yapılandırma, NSG oluşturulduğunda bir NSG kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="755c8-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="755c8-127">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="755c8-128">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="755c8-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="755c8-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="755c8-130">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="755c8-130">Gets subnet information.</span></span> <span data-ttu-id="755c8-131">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="755c8-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="755c8-132">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="755c8-133">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="755c8-134">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="755c8-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="755c8-135">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="755c8-135">Creates a VM configuration.</span></span> <span data-ttu-id="755c8-136">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="755c8-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="755c8-137">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="755c8-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="755c8-138">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="755c8-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="755c8-139">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="755c8-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="755c8-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="755c8-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="755c8-141">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="755c8-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="755c8-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="755c8-142">Next steps</span></span>

<span data-ttu-id="755c8-143">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="755c8-143">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="755c8-144">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="755c8-144">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

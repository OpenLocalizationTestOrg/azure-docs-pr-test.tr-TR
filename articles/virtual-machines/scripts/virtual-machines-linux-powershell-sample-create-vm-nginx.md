---
title: "aaaAzure PowerShell komut dosyası örneği - NGINX | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - NGINX"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 017a4853e400f8f544a3f92771adaf468b5dee76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-nginx-vm-with-powershell"></a><span data-ttu-id="f87b2-103">PowerShell ile bir NGINX VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f87b2-103">Create an NGINX VM with PowerShell</span></span>

<span data-ttu-id="f87b2-104">Bu komut dosyasını bir Azure sanal makine oluşturur ve ardından hello Azure sanal makine özel betik uzantısının tooinstall NGINX kullanır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-104">This script creates an Azure Virtual Machine and then uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="f87b2-105">Merhaba komut dosyasını çalıştırdıktan sonra hello genel IP adresi hello sanal makinenin demo Web sitesine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f87b2-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f87b2-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f87b2-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Create VM NGINX")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f87b2-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f87b2-107">Clean up deployment</span></span> 

<span data-ttu-id="f87b2-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="f87b2-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f87b2-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f87b2-109">Script explanation</span></span>

<span data-ttu-id="f87b2-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="f87b2-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f87b2-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f87b2-112">Komut</span><span class="sxs-lookup"><span data-stu-id="f87b2-112">Command</span></span> | <span data-ttu-id="f87b2-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="f87b2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f87b2-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f87b2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f87b2-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f87b2-116">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f87b2-117">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-117">Creates a subnet configuration.</span></span> <span data-ttu-id="f87b2-118">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="f87b2-119">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f87b2-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="f87b2-120">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="f87b2-121">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f87b2-122">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="f87b2-123">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="f87b2-124">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="f87b2-125">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="f87b2-126">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="f87b2-127">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="f87b2-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f87b2-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f87b2-129">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-129">Gets subnet information.</span></span> <span data-ttu-id="f87b2-130">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="f87b2-131">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f87b2-132">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="f87b2-133">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="f87b2-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="f87b2-134">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f87b2-134">Creates a VM configuration.</span></span> <span data-ttu-id="f87b2-135">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f87b2-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f87b2-136">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f87b2-137">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f87b2-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f87b2-138">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f87b2-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="f87b2-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="f87b2-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="f87b2-140">VM uzantısı toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f87b2-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="f87b2-141">Bu örnekte kullanılan tooinstall NGINX hello özel komut dosyası uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-141">In this sample, hello custom script extension is used tooinstall NGINX.</span></span> |
|[<span data-ttu-id="f87b2-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f87b2-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f87b2-143">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f87b2-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f87b2-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f87b2-144">Next steps</span></span>

<span data-ttu-id="f87b2-145">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f87b2-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f87b2-146">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f87b2-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

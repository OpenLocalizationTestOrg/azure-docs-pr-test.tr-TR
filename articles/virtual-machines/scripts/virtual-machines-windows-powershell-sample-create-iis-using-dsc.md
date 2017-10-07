---
title: "aaaAzure PowerShell komut dosyası örneği - IIS DSC ile | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - IIS DSC ile"
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
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="9f098-103">PowerShell ile bir IIS VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f098-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="9f098-104">Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur ve ardından hello Azure sanal makine DSC uzantısı tooinstall IIS kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f098-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine DSC Extension tooinstall IIS.</span></span> <span data-ttu-id="9f098-105">Merhaba komut dosyasını çalıştırdıktan sonra hello varsayılan IIS Web sitesinde hello genel IP adresi hello sanal makinenin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="9f098-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9f098-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9f098-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9f098-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="9f098-107">Clean up deployment</span></span> 

<span data-ttu-id="9f098-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="9f098-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9f098-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="9f098-109">Script explanation</span></span>

<span data-ttu-id="9f098-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f098-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9f098-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="9f098-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9f098-112">Komut</span><span class="sxs-lookup"><span data-stu-id="9f098-112">Command</span></span> | <span data-ttu-id="9f098-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="9f098-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f098-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f098-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9f098-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9f098-116">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f098-117">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9f098-118">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f098-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9f098-119">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9f098-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9f098-120">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9f098-121">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9f098-122">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9f098-123">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9f098-124">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9f098-125">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="9f098-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9f098-126">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9f098-127">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="9f098-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9f098-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f098-129">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9f098-129">Gets subnet information.</span></span> <span data-ttu-id="9f098-130">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f098-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9f098-131">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9f098-132">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="9f098-133">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9f098-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9f098-134">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f098-134">Creates a VM configuration.</span></span> <span data-ttu-id="9f098-135">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="9f098-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9f098-136">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f098-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9f098-137">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9f098-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9f098-138">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f098-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="9f098-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="9f098-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="9f098-140">VM uzantısı toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9f098-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="9f098-141">Bu örnekte kullanılan tooinstall IIS hello özel komut dosyası uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="9f098-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="9f098-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f098-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9f098-143">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9f098-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f098-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f098-144">Next steps</span></span>

<span data-ttu-id="9f098-145">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f098-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9f098-146">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f098-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

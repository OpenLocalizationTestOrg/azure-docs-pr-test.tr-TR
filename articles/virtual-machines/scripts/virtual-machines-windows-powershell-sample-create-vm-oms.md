---
title: "aaaAzure PowerShell komut dosyası örneği - OMS | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - OMS"
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="4860e-103">Oluşturma VM PowerShell ile bir Operations Management Suite izlenen</span><span class="sxs-lookup"><span data-stu-id="4860e-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="4860e-104">Bu komut dosyasını bir Azure sanal makinesi oluşturur, hello Operations Management Suite (OMS) Aracısı'nı yükler ve bir OMS çalışma hello sistemiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4860e-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="4860e-105">Merhaba betik çalıştıktan sonra hello sanal makine hello OMS konsolunda görünür.</span><span class="sxs-lookup"><span data-stu-id="4860e-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="4860e-106">Ayrıca, kimliği ve çalışma alanı tooupdate hello OMS çalışma alanı anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="4860e-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4860e-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4860e-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4860e-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="4860e-108">Clean up deployment</span></span> 

<span data-ttu-id="4860e-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="4860e-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4860e-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="4860e-110">Script explanation</span></span>

<span data-ttu-id="4860e-111">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="4860e-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4860e-112">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="4860e-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4860e-113">Komut</span><span class="sxs-lookup"><span data-stu-id="4860e-113">Command</span></span> | <span data-ttu-id="4860e-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="4860e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4860e-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4860e-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4860e-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4860e-117">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4860e-118">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-118">Creates a subnet configuration.</span></span> <span data-ttu-id="4860e-119">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4860e-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="4860e-120">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4860e-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4860e-121">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="4860e-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4860e-123">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4860e-124">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4860e-125">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4860e-126">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="4860e-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="4860e-127">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="4860e-128">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="4860e-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4860e-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4860e-130">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="4860e-130">Gets subnet information.</span></span> <span data-ttu-id="4860e-131">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4860e-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="4860e-132">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4860e-133">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="4860e-134">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="4860e-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4860e-135">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4860e-135">Creates a VM configuration.</span></span> <span data-ttu-id="4860e-136">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="4860e-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4860e-137">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4860e-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4860e-138">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4860e-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4860e-139">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4860e-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="4860e-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="4860e-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="4860e-141">VM uzantısı toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4860e-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="4860e-142">Bu durumda, hello Operations Management Suite Aracı Uzantısı kullanılan tooinstall hello OMS aracısı ve hello bir OMS çalışma alanında VM kaydolun.</span><span class="sxs-lookup"><span data-stu-id="4860e-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="4860e-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4860e-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4860e-144">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4860e-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4860e-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4860e-145">Next steps</span></span>

<span data-ttu-id="4860e-146">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4860e-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4860e-147">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4860e-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

---
title: "Azure PowerShell Betiği örnek - OMS | Microsoft Docs"
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
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="89e07-103">Oluşturma VM PowerShell ile bir Operations Management Suite izlenen</span><span class="sxs-lookup"><span data-stu-id="89e07-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="89e07-104">Bu komut dosyasını bir Azure sanal makinesi oluşturur, Operations Management Suite (OMS) Aracısı'nı yükler ve bir OMS çalışma sistemiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="89e07-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="89e07-105">Betik çalıştıktan sonra sanal makine OMS konsolunda görünür.</span><span class="sxs-lookup"><span data-stu-id="89e07-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="89e07-106">Ayrıca, OMS çalışma alanı kimliği ve çalışma alanı anahtarı güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89e07-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="89e07-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="89e07-107">Sample script</span></span>

<span data-ttu-id="89e07-108">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "VM OMS oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="89e07-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="89e07-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="89e07-109">Clean up deployment</span></span> 

<span data-ttu-id="89e07-110">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89e07-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="89e07-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="89e07-111">Script explanation</span></span>

<span data-ttu-id="89e07-112">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="89e07-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="89e07-113">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="89e07-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="89e07-114">Komut</span><span class="sxs-lookup"><span data-stu-id="89e07-114">Command</span></span> | <span data-ttu-id="89e07-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="89e07-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="89e07-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89e07-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="89e07-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="89e07-118">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="89e07-119">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-119">Creates a subnet configuration.</span></span> <span data-ttu-id="89e07-120">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89e07-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="89e07-121">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="89e07-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="89e07-122">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="89e07-123">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="89e07-124">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="89e07-125">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="89e07-126">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="89e07-127">Bu yapılandırma, NSG oluşturulduğunda bir NSG kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89e07-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="89e07-128">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="89e07-129">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="89e07-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="89e07-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="89e07-131">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="89e07-131">Gets subnet information.</span></span> <span data-ttu-id="89e07-132">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89e07-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="89e07-133">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="89e07-134">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="89e07-135">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="89e07-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="89e07-136">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89e07-136">Creates a VM configuration.</span></span> <span data-ttu-id="89e07-137">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="89e07-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="89e07-138">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89e07-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="89e07-139">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="89e07-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="89e07-140">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89e07-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="89e07-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="89e07-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="89e07-142">VM uzantısı sanal makineye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="89e07-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="89e07-143">Bu durumda, Operations Management Suite Aracı Uzantısı OMS Aracısı'nı yüklemek ve bir OMS çalışma alanında VM kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89e07-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="89e07-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89e07-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="89e07-145">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="89e07-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89e07-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89e07-146">Next steps</span></span>

<span data-ttu-id="89e07-147">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89e07-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="89e07-148">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89e07-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

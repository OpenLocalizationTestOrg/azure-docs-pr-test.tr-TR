---
title: "PowerShell komut dosyası örneği - aaaAzure bir anlık görüntüden bir VM oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir anlık görüntüden bir VM oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="744a5-103">Anlık görüntü PowerShell ile bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="744a5-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="744a5-104">Bu komut dosyasını bir sanal makine işletim sistemi diski bir anlık görüntüden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="744a5-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="744a5-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="744a5-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="744a5-106">Clean up deployment</span></span> 

<span data-ttu-id="744a5-107">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="744a5-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="744a5-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="744a5-108">Script explanation</span></span>

<span data-ttu-id="744a5-109">Bu komut dosyası tooget anlık görüntü özellikler, yönetilen bir disk anlık görüntüden oluşturun ve bir VM oluşturma komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="744a5-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="744a5-110">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="744a5-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="744a5-111">Komut</span><span class="sxs-lookup"><span data-stu-id="744a5-111">Command</span></span> | <span data-ttu-id="744a5-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="744a5-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="744a5-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="744a5-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="744a5-114">Anlık görüntü adı kullanarak bir anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="744a5-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="744a5-115">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="744a5-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="744a5-116">Bir disk yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-116">Creates a disk configuration.</span></span> <span data-ttu-id="744a5-117">Bu yapılandırma hello diski oluşturma işlemi ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="744a5-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="744a5-118">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="744a5-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="744a5-119">Yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="744a5-120">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="744a5-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="744a5-121">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-121">Creates a VM configuration.</span></span> <span data-ttu-id="744a5-122">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="744a5-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="744a5-123">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="744a5-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="744a5-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="744a5-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="744a5-125">İşletim sistemi disk toohello sanal makine olarak Hello yönetilen disk ekler</span><span class="sxs-lookup"><span data-stu-id="744a5-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="744a5-126">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="744a5-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="744a5-127">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="744a5-128">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="744a5-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="744a5-129">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="744a5-130">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="744a5-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="744a5-131">Bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="744a5-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="744a5-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="744a5-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="744a5-133">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="744a5-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="744a5-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="744a5-134">Next steps</span></span>

<span data-ttu-id="744a5-135">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="744a5-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="744a5-136">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="744a5-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

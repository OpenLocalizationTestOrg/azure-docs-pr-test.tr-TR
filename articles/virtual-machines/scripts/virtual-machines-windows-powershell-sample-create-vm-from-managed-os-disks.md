---
title: "aaaAzure PowerShell komut dosyası örneği - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma"
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="6f36d-103">PowerShell ile varolan yönetilen bir işletim sistemi diski kullanarak bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="6f36d-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="6f36d-104">Bu komut dosyasını varolan yönetilen disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f36d-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="6f36d-105">Senaryolar önceki içinde bu komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="6f36d-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="6f36d-106">Yönetilen bir diskten farklı Abonelikteki kopyalanan var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f36d-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="6f36d-107">Özel bir VHD dosyasından oluşturulmuş var olan bir diskten yönetilen bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f36d-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="6f36d-108">Bir anlık görüntüden oluşturulmuş var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f36d-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6f36d-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6f36d-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6f36d-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="6f36d-110">Clean up deployment</span></span> 

<span data-ttu-id="6f36d-111">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="6f36d-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6f36d-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6f36d-112">Script explanation</span></span>

<span data-ttu-id="6f36d-113">Bu komut dosyasını aşağıdaki komutları yönetilen tooget disk özelliklere hello kullanıyorsa, yönetilen disk tooa ekleme yeni VM ve VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f36d-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="6f36d-114">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="6f36d-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6f36d-115">Komut</span><span class="sxs-lookup"><span data-stu-id="6f36d-115">Command</span></span> | <span data-ttu-id="6f36d-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="6f36d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6f36d-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="6f36d-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="6f36d-118">Merhaba adı ve hello kaynak grubu bir disk temel alınarak disk nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="6f36d-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="6f36d-119">Merhaba kimliği özelliği döndürülür disk nesnesi kullanılan tooattach hello disk tooa yeni VM</span><span class="sxs-lookup"><span data-stu-id="6f36d-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="6f36d-120">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="6f36d-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="6f36d-121">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f36d-121">Creates a VM configuration.</span></span> <span data-ttu-id="6f36d-122">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6f36d-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="6f36d-123">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6f36d-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="6f36d-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="6f36d-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="6f36d-125">İşletim sistemi disk tooa yeni sanal makine hello disk Hello kimliği özelliğini kullanarak yönetilen bir disk ekler</span><span class="sxs-lookup"><span data-stu-id="6f36d-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="6f36d-126">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="6f36d-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="6f36d-127">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f36d-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="6f36d-128">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="6f36d-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="6f36d-129">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f36d-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="6f36d-130">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="6f36d-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="6f36d-131">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f36d-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="6f36d-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6f36d-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6f36d-133">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6f36d-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6f36d-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f36d-134">Next steps</span></span>

<span data-ttu-id="6f36d-135">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f36d-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6f36d-136">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f36d-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

---
title: "Azure CLI örnekleri Windows | Microsoft Docs"
description: "Windows Azure CLI örnekleri"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="99df9-103">Azure CLI örnekleri Windows için sanal makineler</span><span class="sxs-lookup"><span data-stu-id="99df9-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="99df9-104">Aşağıdaki tabloda, Windows sanal makineleri dağıtmak, Azure CLI kullanarak oluşturulan komut dosyalarını bash bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="99df9-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="99df9-105">**Sanal makineler oluşturma**</span><span class="sxs-lookup"><span data-stu-id="99df9-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="99df9-106">Bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="99df9-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-107">Windows sanal makinesi en az yapılandırma ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99df9-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="99df9-108">Tam olarak yapılandırılmış bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="99df9-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-109">Bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99df9-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="99df9-110">Yüksek oranda kullanılabilir sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="99df9-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-111">Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99df9-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="99df9-112">Bir VM oluşturma ve yapılandırma komut dosyası çalıştırma</span><span class="sxs-lookup"><span data-stu-id="99df9-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-113">Bir sanal makine oluşturur ve IIS yüklemek için Azure özel betik uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="99df9-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="99df9-114">Bir VM oluşturun ve DSC yapılandırması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="99df9-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-115">Bir sanal makine oluşturur ve IIS yüklemek için Azure istenen durum yapılandırması (DSC) uzantısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="99df9-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="99df9-116">**Ağ sanal makineler**</span><span class="sxs-lookup"><span data-stu-id="99df9-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="99df9-117">Sanal makineler arasındaki ağ trafiğini güvenli</span><span class="sxs-lookup"><span data-stu-id="99df9-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-118">İki sanal makine, tüm ilgili kaynaklar ve bir iç ve dış ağ güvenlik grupları (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99df9-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="99df9-119">**Sanal makineler güvenli**</span><span class="sxs-lookup"><span data-stu-id="99df9-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="99df9-120">VM ve veri diskleri şifrele</span><span class="sxs-lookup"><span data-stu-id="99df9-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-121">Azure anahtar kasası, şifreleme anahtarı ve hizmet sorumlusu oluşturur ve ardından VM şifreler.</span><span class="sxs-lookup"><span data-stu-id="99df9-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="99df9-122">**Sanal makineleri izleme**</span><span class="sxs-lookup"><span data-stu-id="99df9-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="99df9-123">Bir VM Operations Management Suite ile izleme</span><span class="sxs-lookup"><span data-stu-id="99df9-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="99df9-124">Bir sanal makine oluşturur, Operations Management Suite aracısını yükler ve bir OMS çalışma alanında VM kaydeder.</span><span class="sxs-lookup"><span data-stu-id="99df9-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |

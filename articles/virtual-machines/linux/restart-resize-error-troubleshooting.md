---
title: "Yeniden başlatma veya yeniden boyutlandırma VM sorunları Azure'da | Microsoft Docs"
description: "Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Resource Manager dağıtım sorunlarını giderme"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="e8303-103">Yeniden başlatmadan veya varolan bir Linux VM azure'da yeniden boyutlandırma ile dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e8303-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="e8303-104">Durdurulmuş bir Azure sanal makine (VM) Başlat veya mevcut bir Azure VM'yi yeniden boyutlandırmak çalıştığınızda karşılaştığınız ortak bir ayırma hatası hatadır.</span><span class="sxs-lookup"><span data-stu-id="e8303-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="e8303-105">Küme veya bölgede kullanılabilir kaynak yok veya istenen VM boyutu destekleyemez olduğunda bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="e8303-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="e8303-106">Toplama etkinliklerini günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="e8303-106">Collect activity logs</span></span>
<span data-ttu-id="e8303-107">Sorun giderme başlatmak için sorunu ile ilişkili hata tanımlamak için etkinlik günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="e8303-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="e8303-108">Aşağıdaki bağlantılar süreci hakkında ayrıntılı bilgiler içerir:</span><span class="sxs-lookup"><span data-stu-id="e8303-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="e8303-109">Dağıtım işlemlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e8303-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="e8303-110">Azure kaynaklarınızı yönetmek için etkinlik günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="e8303-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="e8303-111">Sorun: durmuş bir VM'yi başlatma sırasında hata</span><span class="sxs-lookup"><span data-stu-id="e8303-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="e8303-112">Durmuş bir VM'yi Başlat ancak alma ayırma hatası deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8303-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e8303-113">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e8303-113">Cause</span></span>
<span data-ttu-id="e8303-114">Bulut hizmeti barındıran özgün kümesine denenmesi durdurulmuş VM başlatmak için bir istek aldı.</span><span class="sxs-lookup"><span data-stu-id="e8303-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="e8303-115">Ancak, Küme isteği gerçekleştirmek kullanılabilir boş disk alanı yok.</span><span class="sxs-lookup"><span data-stu-id="e8303-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="e8303-116">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8303-116">Resolution</span></span>
* <span data-ttu-id="e8303-117">Kullanılabilirlik kümesindeki tüm sanal makineleri durdurmak ve ardından her VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e8303-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="e8303-118">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="e8303-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e8303-119">Tüm sanal makineleri durdurduktan sonra durdurulmuş VM'lerin her birinde seçin ve Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e8303-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="e8303-120">Yeniden başlatma isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8303-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="e8303-121">Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata</span><span class="sxs-lookup"><span data-stu-id="e8303-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="e8303-122">Mevcut bir VM'yi yeniden boyutlandırın, ancak bir ayırma hatası almak deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8303-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e8303-123">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e8303-123">Cause</span></span>
<span data-ttu-id="e8303-124">Bulut hizmeti barındıran özgün kümesine denenmesi VM yeniden boyutlandırmak için bir istek aldı.</span><span class="sxs-lookup"><span data-stu-id="e8303-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="e8303-125">Ancak, küme istenen VM boyutu desteklemez.</span><span class="sxs-lookup"><span data-stu-id="e8303-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="e8303-126">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8303-126">Resolution</span></span>
* <span data-ttu-id="e8303-127">Daha küçük bir VM boyutu kullanarak isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8303-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="e8303-128">İstenen VM boyutu değiştirilemiyorsa:</span><span class="sxs-lookup"><span data-stu-id="e8303-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="e8303-129">Kullanılabilirlik kümesindeki tüm sanal makineleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="e8303-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="e8303-130">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="e8303-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e8303-131">Tüm sanal makineleri durdurduktan sonra daha büyük bir boyutu için istenen VM'yi yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="e8303-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="e8303-132">Yeniden boyutlandırılan VM seçin ve tıklatın **Başlat**, ve durdurulmuş VM'lerin her birinde başlatın.</span><span class="sxs-lookup"><span data-stu-id="e8303-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8303-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8303-133">Next steps</span></span>
<span data-ttu-id="e8303-134">Azure'da yeni bir Linux VM oluşturma sırasında sorunlarla karşılaşırsanız, bkz: [Azure'da yeni bir Linux sanal makine oluşturma ile dağıtım sorunlarını giderme](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8303-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


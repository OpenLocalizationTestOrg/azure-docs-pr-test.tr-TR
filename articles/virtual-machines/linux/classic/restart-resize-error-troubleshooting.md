---
title: "Yeniden başlatmadan veya sorunları yeniden boyutlandırma VM | Microsoft Docs"
description: "Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Klasik dağıtım sorunlarını giderme"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="fcfa6-103">Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Klasik dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fcfa6-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcfa6-104">Klasik</span><span class="sxs-lookup"><span data-stu-id="fcfa6-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="fcfa6-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fcfa6-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="fcfa6-106">Durdurulmuş bir Azure sanal makine (VM) Başlat veya mevcut bir Azure VM'yi yeniden boyutlandırmak çalıştığınızda karşılaştığınız ortak bir ayırma hatası hatadır.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="fcfa6-107">Küme veya bölgede kullanılabilir kaynak yok veya istenen VM boyutu destekleyemez olduğunda bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fcfa6-108">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fcfa6-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fcfa6-109">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fcfa6-110">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fcfa6-111">Resource Manager sürümü için bkz: [burada](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fcfa6-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="fcfa6-112">Toplama denetim günlüklerini</span><span class="sxs-lookup"><span data-stu-id="fcfa6-112">Collect audit logs</span></span>
<span data-ttu-id="fcfa6-113">Sorun giderme başlatmak için sorunu ile ilişkili hata tanımlamak için denetim günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="fcfa6-114">Azure portalında tıklatın **Gözat** > **sanal makineleri** > *Linux sanal makineniz*  >   **Ayarları** > **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="fcfa6-115">Sorun: durmuş bir VM'yi başlatma sırasında hata</span><span class="sxs-lookup"><span data-stu-id="fcfa6-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="fcfa6-116">Durmuş bir VM'yi Başlat ancak alma ayırma hatası deneyin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fcfa6-117">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fcfa6-117">Cause</span></span>
<span data-ttu-id="fcfa6-118">Bulut hizmeti barındıran özgün kümesine denenmesi durdurulmuş VM başlatmak için bir istek aldı.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="fcfa6-119">Ancak, Küme isteği gerçekleştirmek kullanılabilir boş disk alanı yok.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="fcfa6-120">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fcfa6-120">Resolution</span></span>
* <span data-ttu-id="fcfa6-121">Yeni bir bulut hizmeti oluşturup bir bölge veya bölge tabanlı bir sanal ağ, ancak bir benzeşim grubu ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="fcfa6-122">Durdurulan VM silin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="fcfa6-123">Yeni bulut hizmeti VM diskleri kullanarak yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="fcfa6-124">Yeniden oluşturulan VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-124">Start the re-created VM.</span></span>

<span data-ttu-id="fcfa6-125">Yeni bir bulut hizmeti oluşturmaya çalışırken bir hata alırsanız, daha sonra yeniden deneyin veya Bulut hizmeti için bölge değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcfa6-126">Bu bilgi için bu bilgileri mevcut bulut hizmeti için kullandığınız tüm bağımlılıkları değiştirmeniz gerekir böylece yeni bulut hizmeti yeni bir ad ve VIP, gerekir.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="fcfa6-127">Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata</span><span class="sxs-lookup"><span data-stu-id="fcfa6-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="fcfa6-128">Mevcut bir VM'yi yeniden boyutlandırın, ancak bir ayırma hatası almak deneyin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fcfa6-129">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fcfa6-129">Cause</span></span>
<span data-ttu-id="fcfa6-130">Bulut hizmeti barındıran özgün kümesine denenmesi VM yeniden boyutlandırmak için bir istek aldı.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="fcfa6-131">Ancak, küme istenen VM boyutu desteklemez.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="fcfa6-132">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fcfa6-132">Resolution</span></span>
<span data-ttu-id="fcfa6-133">İstenen VM boyutu azaltın ve yeniden boyutlandırma isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="fcfa6-134">Tıklatın **tümüne Gözat** > **sanal makineleri (Klasik)** > *sanal makineniz* > **ayarları** > **boyutu**.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="fcfa6-135">Ayrıntılı adımlar için bkz: [sanal makine yeniden boyutlandırma](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcfa6-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="fcfa6-136">VM boyutunu azaltmak mümkün değilse, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fcfa6-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="fcfa6-137">Bir benzeşim grubuna bağlı değil ve bir benzeşim grubuna bağlı bir sanal ağ ile ilişkilendirilmemiş sağlayarak yeni bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="fcfa6-138">Yeni, büyük ölçekli bir VM içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="fcfa6-139">Aynı bulut hizmetindeki tüm Vm'leriniz birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="fcfa6-140">Mevcut bulut hizmetiniz bir bölge tabanlı sanal ağ ile ilişkili ise, yeni bulut hizmeti varolan bir sanal ağa bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="fcfa6-141">Mevcut bulut hizmeti bir bölge tabanlı sanal ağ ile ilişkili değilse, mevcut bulut hizmetindeki sanal makineleri silin ve bunları kendi disklerden yeni bulut hizmeti yeniden sahip.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="fcfa6-142">Ancak, bunlar şu anda mevcut bulut hizmeti için bu bilgileri kullanan tüm bağımlılıkları için güncelleştirmeniz gerekir böylece yeni bulut hizmeti yeni bir ad ve VIP, olacaktır unutmamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fcfa6-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcfa6-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fcfa6-143">Next steps</span></span>
<span data-ttu-id="fcfa6-144">Azure'da yeni bir Linux VM oluşturma sırasında sorunlarla karşılaşırsanız, bkz: [Azure'da yeni bir Linux sanal makine oluşturma ile dağıtım sorunlarını giderme](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fcfa6-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


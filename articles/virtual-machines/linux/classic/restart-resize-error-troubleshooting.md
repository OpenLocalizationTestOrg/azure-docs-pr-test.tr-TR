---
title: "yeniden başlatmadan veya sorunları yeniden boyutlandırma aaaVM | Microsoft Docs"
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
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="68b77-103">Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Klasik dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="68b77-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68b77-104">Klasik</span><span class="sxs-lookup"><span data-stu-id="68b77-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="68b77-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68b77-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="68b77-106">Toostart durdurulmuş Azure sanal makine (VM) deneyin ya da mevcut bir Azure VM'i yeniden boyutlandırın karşılaştığınız hello ortak bir ayırma hatası hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="68b77-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="68b77-107">Merhaba küme veya bölgede kullanılabilir kaynakları ya da yok ya da alamazsınız destek hello istenen VM boyutu bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="68b77-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="68b77-108">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="68b77-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="68b77-109">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="68b77-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="68b77-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="68b77-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="68b77-111">Merhaba Resource Manager sürümü için bkz: [burada](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68b77-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="68b77-112">Toplama denetim günlüklerini</span><span class="sxs-lookup"><span data-stu-id="68b77-112">Collect audit logs</span></span>
<span data-ttu-id="68b77-113">sorun giderme, toostart toplama hello denetim hello sorun ilişkili tooidentify hello hata günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="68b77-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="68b77-114">Hello Azure portal'ı tıklatın **Gözat** > **sanal makineleri** > *Linux sanal makineniz*  >   **Ayarları** > **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="68b77-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="68b77-115">Sorun: durmuş bir VM'yi başlatma sırasında hata</span><span class="sxs-lookup"><span data-stu-id="68b77-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="68b77-116">Toostart durmuş bir VM'yi deneyin ancak bir ayırma hatası alır.</span><span class="sxs-lookup"><span data-stu-id="68b77-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="68b77-117">Nedeni</span><span class="sxs-lookup"><span data-stu-id="68b77-117">Cause</span></span>
<span data-ttu-id="68b77-118">VM toostart hello durduruldu hello isteği hello bulut hizmeti barındıran hello özgün kümesine çalıştı toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="68b77-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="68b77-119">Ancak, hello küme boş alan kullanılabilir toofulfill hello isteği yok.</span><span class="sxs-lookup"><span data-stu-id="68b77-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="68b77-120">Çözüm</span><span class="sxs-lookup"><span data-stu-id="68b77-120">Resolution</span></span>
* <span data-ttu-id="68b77-121">Yeni bir bulut hizmeti oluşturup bir bölge veya bölge tabanlı bir sanal ağ, ancak bir benzeşim grubu ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="68b77-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="68b77-122">Silme hello VM durduruldu.</span><span class="sxs-lookup"><span data-stu-id="68b77-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="68b77-123">Merhaba yeni bulut hizmeti VM Hello hello diskleri kullanarak yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68b77-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="68b77-124">Başlangıç hello VM yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="68b77-124">Start hello re-created VM.</span></span>

<span data-ttu-id="68b77-125">Toocreate yeni bir bulut hizmeti çalışırken bir hata alırsanız, daha sonra yeniden deneyin veya hello bölge hello bulut hizmeti için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="68b77-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68b77-126">Bu bilgileri hello mevcut bulut hizmeti için kullandığınız tüm hello bağımlılıklar için bu bilgileri toochange gerekir hello yeni bulut hizmeti yeni bir ad ve VIP, gerekir.</span><span class="sxs-lookup"><span data-stu-id="68b77-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="68b77-127">Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata</span><span class="sxs-lookup"><span data-stu-id="68b77-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="68b77-128">Mevcut bir VM'yi tooresize deneyin ancak bir ayırma hatası alır.</span><span class="sxs-lookup"><span data-stu-id="68b77-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="68b77-129">Nedeni</span><span class="sxs-lookup"><span data-stu-id="68b77-129">Cause</span></span>
<span data-ttu-id="68b77-130">Merhaba isteği tooresize hello VM toobe sahip hello özgün kümesine, konaklar hello bulut hizmetinin çalıştı.</span><span class="sxs-lookup"><span data-stu-id="68b77-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="68b77-131">Ancak, hello küme desteklemediği hello istenen VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="68b77-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="68b77-132">Çözüm</span><span class="sxs-lookup"><span data-stu-id="68b77-132">Resolution</span></span>
<span data-ttu-id="68b77-133">Azaltmak hello istenen VM boyutu ve Yeniden Dene'yi hello isteği yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="68b77-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="68b77-134">Tıklatın **tümüne Gözat** > **sanal makineleri (Klasik)** > *sanal makineniz* > **ayarları** > **boyutu**.</span><span class="sxs-lookup"><span data-stu-id="68b77-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="68b77-135">Ayrıntılı adımlar için bkz: [hello sanal makine yeniden boyutlandırma](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="68b77-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="68b77-136">Olası tooreduce hello VM boyutu değilse, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="68b77-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="68b77-137">Bağlantılı tooan benzeşim grubu olmadığı ve bağlantılı tooan benzeşim grubu olan bir sanal ağ ile ilişkili olmayan sağlayarak yeni bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68b77-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="68b77-138">Yeni, büyük ölçekli bir VM içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68b77-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="68b77-139">Tüm Vm'leriniz birleştirebilir hello aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="68b77-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="68b77-140">Mevcut bulut hizmetiniz bir bölge tabanlı sanal ağ ile ilişkili ise, hello yeni bulut hizmeti toohello mevcut sanal ağa bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="68b77-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="68b77-141">Hello mevcut bulut hizmeti bir bölge tabanlı sanal ağ ile ilişkili değilse, sonra toodelete hello VM'ler hello mevcut bulut hizmetine sahip ve bunların disklerden hello yeni bulut hizmetinde yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68b77-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="68b77-142">Ancak, önemli tooremember tooupdate ihtiyacınız olacak şekilde hello yeni bulut hizmeti yeni bir ad ve VIP, bunlar şu anda bu bilgileri hello olan bulut hizmetini kullanan tüm hello bağımlılıklar için sahip olma olasılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="68b77-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68b77-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68b77-143">Next steps</span></span>
<span data-ttu-id="68b77-144">Azure'da yeni bir Linux VM oluşturma sırasında sorunlarla karşılaşırsanız, bkz: [Azure'da yeni bir Linux sanal makine oluşturma ile dağıtım sorunlarını giderme](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68b77-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


---
title: "yeniden başlatma veya yeniden boyutlandırma aaaVM sorunları Azure'da | Microsoft Docs"
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
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="86f0c-103">Yeniden başlatmadan veya varolan bir Linux VM azure'da yeniden boyutlandırma ile dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="86f0c-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="86f0c-104">Toostart durdurulmuş Azure sanal makine (VM) deneyin ya da mevcut bir Azure VM'i yeniden boyutlandırın karşılaştığınız hello ortak bir ayırma hatası hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="86f0c-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="86f0c-105">Merhaba küme veya bölgede kullanılabilir kaynakları ya da yok ya da alamazsınız destek hello istenen VM boyutu bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="86f0c-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="86f0c-106">Toplama etkinliklerini günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="86f0c-106">Collect activity logs</span></span>
<span data-ttu-id="86f0c-107">sorun giderme, toostart toplama hello etkinlik hello sorun ilişkili tooidentify hello hata günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="86f0c-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="86f0c-108">Aşağıdaki bağlantılar hello hello süreci hakkında ayrıntılı bilgiler içerir:</span><span class="sxs-lookup"><span data-stu-id="86f0c-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="86f0c-109">Dağıtım işlemlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="86f0c-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="86f0c-110">Etkinlik günlükleri toomanage Azure görüntülemek kaynakları</span><span class="sxs-lookup"><span data-stu-id="86f0c-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="86f0c-111">Sorun: durmuş bir VM'yi başlatma sırasında hata</span><span class="sxs-lookup"><span data-stu-id="86f0c-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="86f0c-112">Toostart durmuş bir VM'yi deneyin ancak bir ayırma hatası alır.</span><span class="sxs-lookup"><span data-stu-id="86f0c-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="86f0c-113">Nedeni</span><span class="sxs-lookup"><span data-stu-id="86f0c-113">Cause</span></span>
<span data-ttu-id="86f0c-114">VM toostart hello durduruldu hello isteği hello bulut hizmeti barındıran hello özgün kümesine çalıştı toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="86f0c-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="86f0c-115">Ancak, hello küme boş alan kullanılabilir toofulfill hello isteği yok.</span><span class="sxs-lookup"><span data-stu-id="86f0c-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="86f0c-116">Çözüm</span><span class="sxs-lookup"><span data-stu-id="86f0c-116">Resolution</span></span>
* <span data-ttu-id="86f0c-117">Merhaba kullanılabilirlik VM'ler ayarlayın ve her VM yeniden başlatma tüm hello durdurun.</span><span class="sxs-lookup"><span data-stu-id="86f0c-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="86f0c-118">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="86f0c-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="86f0c-119">Tüm VM'ler Dur Merhaba, durduruldu hello VM'lerin her birinde seçin ve Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="86f0c-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="86f0c-120">Merhaba yeniden başlatma isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="86f0c-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="86f0c-121">Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata</span><span class="sxs-lookup"><span data-stu-id="86f0c-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="86f0c-122">Mevcut bir VM'yi tooresize deneyin ancak bir ayırma hatası alır.</span><span class="sxs-lookup"><span data-stu-id="86f0c-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="86f0c-123">Nedeni</span><span class="sxs-lookup"><span data-stu-id="86f0c-123">Cause</span></span>
<span data-ttu-id="86f0c-124">Merhaba isteği tooresize hello VM toobe sahip hello özgün kümesine, konaklar hello bulut hizmetinin çalıştı.</span><span class="sxs-lookup"><span data-stu-id="86f0c-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="86f0c-125">Ancak, hello küme desteklemediği hello istenen VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="86f0c-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="86f0c-126">Çözüm</span><span class="sxs-lookup"><span data-stu-id="86f0c-126">Resolution</span></span>
* <span data-ttu-id="86f0c-127">Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="86f0c-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="86f0c-128">Merhaba, hello VM değiştirilemez istenen boyut:</span><span class="sxs-lookup"><span data-stu-id="86f0c-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="86f0c-129">Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="86f0c-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="86f0c-130">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="86f0c-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="86f0c-131">Tüm VM'ler Dur Merhaba, istenen hello VM tooa büyük yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="86f0c-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="86f0c-132">Select hello yeniden boyutlandırılabilir tıklayın ve VM **Başlat**, ve ardından VM'ler başlangıcı her hello durduruldu.</span><span class="sxs-lookup"><span data-stu-id="86f0c-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86f0c-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86f0c-133">Next steps</span></span>
<span data-ttu-id="86f0c-134">Azure'da yeni bir Linux VM oluşturma sırasında sorunlarla karşılaşırsanız, bkz: [Azure'da yeni bir Linux sanal makine oluşturma ile dağıtım sorunlarını giderme](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86f0c-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


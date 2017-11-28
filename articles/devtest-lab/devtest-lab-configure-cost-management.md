---
title: "aaaView hello aylık tahmini Laboratuvar maliyet eğilimi Azure DevTest Labs | Microsoft Docs"
description: "Hello Azure DevTest Labs aylık tahmini maliyet eğilim Grafiği hakkında bilgi edinin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="02b87-103">Görünüm hello aylık tahmini Laboratuvar maliyet eğilimi Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="02b87-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="02b87-104">DevTest Labs Hello maliyet yönetim özelliği Laboratuvarınızı hello maliyetini izlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="02b87-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="02b87-105">Bu makalede gösterilmektedir nasıl toouse hello **aylık tahmini maliyet eğilimi** grafik tooview geçerli Takvim ayın tahmini maliyet-to-date hello ve geçerli bir takvim ayının hello tahmini ayın son maliyeti hello.</span><span class="sxs-lookup"><span data-stu-id="02b87-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="02b87-106">Bu makalede, nasıl tooview hello hello Azure portal aylık tahmini maliyet eğilimi grafikte öğrenin.</span><span class="sxs-lookup"><span data-stu-id="02b87-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="02b87-107">Merhaba aylık tahmini maliyet eğilim grafiği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="02b87-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="02b87-108">tooview hello aylık tahmini maliyet eğilim Grafiği, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="02b87-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="02b87-109">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02b87-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="02b87-110">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="02b87-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="02b87-111">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="02b87-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="02b87-112">Merhaba Laboratuvar'ın dikey penceresinde, seçin **maliyet ayarlarına**.</span><span class="sxs-lookup"><span data-stu-id="02b87-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="02b87-113">Merhaba Laboratuvar'ın üzerinde **maliyet ayarlarına** dikey penceresinde, select **Laboratuvar maliyet eğilimi**.</span><span class="sxs-lookup"><span data-stu-id="02b87-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="02b87-114">Merhaba aşağıdaki ekran görüntüsünde bir maliyet grafik örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="02b87-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Maliyet grafik](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="02b87-116">Merhaba **maliyet tahmini** değeri geçerli bir takvim ayının ait tahmini maliyet-to-date hello.</span><span class="sxs-lookup"><span data-stu-id="02b87-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="02b87-117">Merhaba **tahmini maliyet** hello hello tamamı için tahmini maliyet geçerli Takvim ayı hello Laboratuvar maliyet Merhaba önceki beş gün kullanılarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="02b87-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="02b87-118">Merhaba maliyet tutarlar toohello sonraki tam sayıya yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="02b87-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="02b87-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="02b87-119">For example:</span></span> 

* <span data-ttu-id="02b87-120">5.01 too6 yuvarlar</span><span class="sxs-lookup"><span data-stu-id="02b87-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="02b87-121">5.50 too6 yuvarlar</span><span class="sxs-lookup"><span data-stu-id="02b87-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="02b87-122">5.99 too6 yuvarlar</span><span class="sxs-lookup"><span data-stu-id="02b87-122">5.99 rounds up too6</span></span>

<span data-ttu-id="02b87-123">Hello grafik durumları gibi hello grafikte gördüğünüz hello maliyetleri olduğundan *tahmini* kullanarak maliyetlerini [Kullandıkça Öde](https://azure.microsoft.com/offers/ms-azr-0003p/) hızları sunar.</span><span class="sxs-lookup"><span data-stu-id="02b87-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="02b87-124">Ayrıca, hello şunlardır *değil* hesaplama maliyet hello dahil:</span><span class="sxs-lookup"><span data-stu-id="02b87-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="02b87-125">CSP ve Dreamspark abonelik şu anda desteklenmiyor Azure DevTest Labs hello kullandıkça [Azure fatura API'leri](../billing/billing-usage-rate-card-overview.md) toocalculate hello Laboratuvar maliyet, CSP veya Dreamspark abonelik desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="02b87-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="02b87-126">Teklif ücretlerinizi.</span><span class="sxs-lookup"><span data-stu-id="02b87-126">Your offer rates.</span></span> <span data-ttu-id="02b87-127">Şu anda, biz mümkün toouse olmayan teklif ücretlerinizi (abonelik altında Microsoft veya Microsoft iş ortakları anlaşılan olduğunu gösterilmiştir).</span><span class="sxs-lookup"><span data-stu-id="02b87-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="02b87-128">Kullandıkça Öde oranları kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="02b87-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="02b87-129">Vergiler</span><span class="sxs-lookup"><span data-stu-id="02b87-129">Your taxes</span></span>
* <span data-ttu-id="02b87-130">İndirim</span><span class="sxs-lookup"><span data-stu-id="02b87-130">Your discounts</span></span>
* <span data-ttu-id="02b87-131">Fatura para birimi.</span><span class="sxs-lookup"><span data-stu-id="02b87-131">Your billing currency.</span></span> <span data-ttu-id="02b87-132">Şu anda hello Laboratuvar maliyet yalnızca ABD Doları para birimi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="02b87-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="02b87-133">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="02b87-133">Related blog posts</span></span>
* [<span data-ttu-id="02b87-134">İki daha fazla şey tookeep maliyetinizi DevTest Labs kanalındaki</span><span class="sxs-lookup"><span data-stu-id="02b87-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="02b87-135">Neden eşikleri maliyet?</span><span class="sxs-lookup"><span data-stu-id="02b87-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="02b87-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02b87-136">Next steps</span></span>
<span data-ttu-id="02b87-137">Sonraki bazı şeyleri tootry şunlardır:</span><span class="sxs-lookup"><span data-stu-id="02b87-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="02b87-138">[Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md) -nasıl tooset hello kullanılan çeşitli ilkeler öğrenin toogovern nasıl Laboratuvarınızı ve Vm'lerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02b87-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="02b87-139">[Özel görüntü oluşturma](devtest-lab-create-template.md) - bir VM oluşturduğunuzda, özel bir görüntü veya bir Market görüntüsü olabilecek bir taban belirtin.</span><span class="sxs-lookup"><span data-stu-id="02b87-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="02b87-140">Bu makalede nasıl toocreate özel bir görüntü bir VHD dosyasından gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="02b87-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="02b87-141">[Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) - VMs Azure Market görüntülerini temel oluşturmayı DevTest Labs destekler.</span><span class="sxs-lookup"><span data-stu-id="02b87-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="02b87-142">Bu makalede gösterilmektedir nasıl olabilen, varsa, Azure Market görüntülerini toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02b87-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="02b87-143">[Bir laboratuar ortamında bir VM oluşturma](devtest-lab-add-vm-with-artifacts.md) -gösterilmektedir nasıl toocreate temel görüntü bir VM'den (ya da özel veya Market) ve nasıl toowork yapıtlarla birlikte, VM.</span><span class="sxs-lookup"><span data-stu-id="02b87-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>


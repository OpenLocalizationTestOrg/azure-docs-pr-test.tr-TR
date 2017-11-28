---
title: "aaaAzure Danışmanı maliyet önerileri | Microsoft Docs"
description: "Azure Danışmanı toooptimize hello Azure dağıtımlarınızı maliyetini kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="e1076-103">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="e1076-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="e1076-104">En iyi duruma getirme ve genel Azure azaltmak Danışmanı yardımcı olur, boşta ve az kaynaklarını tanımlayarak ayırın.</span><span class="sxs-lookup"><span data-stu-id="e1076-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="e1076-105">Merhaba önerileri maliyet **maliyet** hello Danışmanı Pano sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="e1076-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Advisor maliyet sekmesi](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="e1076-107">En iyi duruma getirme sanal makine harcamanız az örneklerini yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e1076-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="e1076-108">Belirli uygulama senaryoları düşük kullanımı tasarım gereği neden olabilir ancak genellikle hello boyutunu ve sanal makinelerinizi sayısını yöneterek para kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1076-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="e1076-109">Advisor 14 gün boyunca, sanal makine kullanımını izler ve düşük kullanımı sanal makineleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1076-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="e1076-110">Sanal makineler, CPU kullanımı yüzde 5'idir veya daha az ve ağ kullanımını 7 MB veya daha az dört veya daha fazla gün düşük kullanımı sanal makineler olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e1076-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="e1076-111">Aşağı ya da yeniden boyutlandırmak tooshut seçebilmeleri sanal makineniz toorun etmeden tahmini maliyeti hello Danışmanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1076-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Sanal makineler yeniden boyutlandırma için öneriler maliyet Danışmanı](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="e1076-113">Birden çok SQL veritabanları, uygun maliyetli bir çözüm toomanage performans hedeflerini kullanın</span><span class="sxs-lookup"><span data-stu-id="e1076-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="e1076-114">Advisor esnek veritabanı havuzu oluşturma yararlanabilir SQL server örnekleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e1076-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="e1076-115">Esnek veritabanı havuzları basit ve ekonomik çözüm toomanage hello performans hedeflerini değişen kullanım desenlerini sahip birden çok veritabanlarının sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1076-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="e1076-116">Azure esnek havuzları hakkında daha fazla bilgi için bkz: [bir Azure esnek havuz nedir?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="e1076-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Esnek veritabanı havuzlarına ilişkin öneriler maliyet Danışmanı](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="e1076-118">Nasıl tooaccess Azure Advisor önerileri maliyet</span><span class="sxs-lookup"><span data-stu-id="e1076-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="e1076-119">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1076-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e1076-120">Merhaba sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="e1076-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="e1076-121">Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="e1076-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="e1076-122">Merhaba Danışmanı Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e1076-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="e1076-123">Hello Danışmanı Panoda hello tıklatın **maliyet** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e1076-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="e1076-124">Kendisi için tooreceive önerileri istediğiniz ve ardından hello aboneliği seçin **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="e1076-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1076-125">tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="e1076-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e1076-126">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1076-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="e1076-127">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="e1076-127">This is a *one-time operation*.</span></span> <span data-ttu-id="e1076-128">Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="e1076-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1076-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1076-129">Next steps</span></span>

<span data-ttu-id="e1076-130">Advisor önerileri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="e1076-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="e1076-131">Giriş tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="e1076-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="e1076-132">Kullanmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="e1076-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="e1076-133">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="e1076-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e1076-134">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="e1076-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e1076-135">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="e1076-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)

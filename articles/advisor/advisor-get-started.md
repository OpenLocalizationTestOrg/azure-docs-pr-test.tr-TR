---
title: "aaaGet Azure Advisor ile başlatılan | Microsoft Docs"
description: "Azure Advisor ile çalışmaya başlayın."
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: 30fc8b8f3823f6f047e46cb9000189f3ccb3d514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="0c88b-103">Azure Advisor’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0c88b-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="0c88b-104">Nasıl hello Azure portal, get önerileri aracılığıyla tooaccess Advisor önerileri uygulamak öğrenin, öneriler ve yenileme öneriler için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="0c88b-104">Learn how tooaccess Advisor through hello Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="0c88b-105">Danışman’dan öneriler alın</span><span class="sxs-lookup"><span data-stu-id="0c88b-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="0c88b-106">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c88b-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0c88b-107">Merhaba sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-107">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="0c88b-108">Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-108">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="0c88b-109">Merhaba Danışmanı Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0c88b-109">hello Advisor dashboard is displayed.</span></span>

   ![Erişim Azure hello Azure portal kullanarak Danışmanı](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="0c88b-111">Merhaba Danışmanı Panoda tooreceive önerileri istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="0c88b-111">On hello Advisor dashboard, select hello subscription for which you want tooreceive recommendations.</span></span>  
<span data-ttu-id="0c88b-112">Merhaba Danışmanı Pano seçili abonelik için kişiselleştirilmiş önerileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0c88b-112">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="0c88b-113">belirli bir kategorideki tooget önerileri hello sekmelerden birine tıklayın: **yüksek kullanılabilirlik**, **güvenlik**, **performans**, veya **maliyet**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-113">tooget recommendations for a particular category, click one of hello tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="0c88b-114">tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="0c88b-114">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="0c88b-115">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0c88b-115">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="0c88b-116">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="0c88b-116">This is a *one-time operation*.</span></span> <span data-ttu-id="0c88b-117">Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="0c88b-117">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Danışmanı Panosu](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="0c88b-119">Advisor öneri ayrıntılarını almak ve bir çözüm uygulama</span><span class="sxs-lookup"><span data-stu-id="0c88b-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="0c88b-120">Merhaba **öneri** Danışmanı dikey penceresinde hello öneri hakkında ek bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c88b-120">hello **Recommendation** blade in Advisor offers additional information about hello recommendation.</span></span> 

1. <span data-ttu-id="0c88b-121">İçinde toohello oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="0c88b-121">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="0c88b-122">Merhaba üzerinde **Danışmanı önerileri** panoyu tıklatın **önerileri almak**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-122">On hello **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="0c88b-123">Öneriler Hello listesinde ayrıntılı tooreview istediğiniz bir öneri tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c88b-123">In hello list of recommendations, click a recommendation that you want tooreview in detail.</span></span>  
<span data-ttu-id="0c88b-124">Merhaba **öneri** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0c88b-124">hello **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="0c88b-125">Merhaba üzerinde **önerileri** dikey penceresinde, tooresolve olası bir sorunu gerçekleştirmek veya bir maliyet tasarrufu fırsat yararlanmak Eylemler ilgili bilgileri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0c88b-125">On hello **Recommendations** blade, review information about actions that you can perform tooresolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Merhaba Danışmanı Önerisi dikey penceresinde](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="0c88b-127">Advisor önerileri arayın</span><span class="sxs-lookup"><span data-stu-id="0c88b-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="0c88b-128">Belirli bir abonelik veya kaynak grubu için öneriler için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c88b-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="0c88b-129">Ayrıca önerileri için duruma göre arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c88b-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="0c88b-130">İçinde toohello oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="0c88b-130">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="0c88b-131">Abonelik, kaynak grupları ve öneri durumu filtreleyerek önerileri için arama (**etkin** veya **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="0c88b-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="0c88b-132">arama filtresi ölçütlerinizi toodisplay temel alan Advisor önerileri listesini tıklatın **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-132">toodisplay a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Advisor arama filtre ölçütü](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="0c88b-134">Uykuda veya Advisor önerileri kapatın</span><span class="sxs-lookup"><span data-stu-id="0c88b-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="0c88b-135">İçinde toohello oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="0c88b-135">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="0c88b-136">Tıklatın **alma önerileri**, bir öneri önerileri hello listesinde'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0c88b-136">Click **Get recommendations**, and then, in hello list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="0c88b-137">Merhaba üzerinde **öneri** dikey penceresinde tıklatın **uykuda**.</span><span class="sxs-lookup"><span data-stu-id="0c88b-137">On hello **Recommendation** blade, click **Snooze**.</span></span>  

   ![Advisor öneri eylem örneği](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="0c88b-139">Erteleme zaman aralığını belirtin veya seçin **hiçbir zaman** toodismiss hello öneri.</span><span class="sxs-lookup"><span data-stu-id="0c88b-139">Specify a snooze time period, or select **Never** toodismiss hello recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0c88b-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c88b-140">Next steps</span></span>

<span data-ttu-id="0c88b-141">Advisor hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="0c88b-141">toolearn more about Advisor, see:</span></span>
* [<span data-ttu-id="0c88b-142">Giriş tooAzure Danışmanı</span><span class="sxs-lookup"><span data-stu-id="0c88b-142">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="0c88b-143">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="0c88b-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="0c88b-144">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="0c88b-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="0c88b-145">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="0c88b-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="0c88b-146">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="0c88b-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)

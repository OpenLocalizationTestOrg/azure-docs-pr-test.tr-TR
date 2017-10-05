---
title: "Azure Advisor ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="3091e-103">Azure Advisor’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3091e-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="3091e-104">Advisor Azure portalı üzerinden erişim, öneriler alın, önerileri uygulamak, öneriler ve yenileme öneriler için arama öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3091e-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="3091e-105">Danışman’dan öneriler alın</span><span class="sxs-lookup"><span data-stu-id="3091e-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="3091e-106">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3091e-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3091e-107">Sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="3091e-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="3091e-108">Hizmet menü bölmesinde altında **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="3091e-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="3091e-109">Advisor Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3091e-109">The Advisor dashboard is displayed.</span></span>

   ![Erişim Azure Azure portalını kullanarak Danışmanı](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="3091e-111">Advisor Panoda önerileri almak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="3091e-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="3091e-112">Advisor Pano seçili abonelik için kişiselleştirilmiş önerileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3091e-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="3091e-113">Belirli bir kategorideki önerileri almak için sekmelerden birine tıklayın: **yüksek kullanılabilirlik**, **güvenlik**, **performans**, veya **maliyet**.</span><span class="sxs-lookup"><span data-stu-id="3091e-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="3091e-114">Advisor önerileri erişmek için öncelikle *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="3091e-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="3091e-115">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* Danışmanı Pano başlatır ve tıkladığında **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3091e-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="3091e-116">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="3091e-116">This is a *one-time operation*.</span></span> <span data-ttu-id="3091e-117">Abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* bir abonelik, bir kaynak grubu ya da belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="3091e-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Danışmanı Panosu](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="3091e-119">Advisor öneri ayrıntılarını almak ve bir çözüm uygulama</span><span class="sxs-lookup"><span data-stu-id="3091e-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="3091e-120">**Öneri** dikey penceresinde Danışmanı öneri hakkında ek bilgiler sunar.</span><span class="sxs-lookup"><span data-stu-id="3091e-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="3091e-121">Oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3091e-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3091e-122">Üzerinde **Danışmanı önerileri** panoyu tıklatın **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="3091e-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="3091e-123">Öneriler listesinde ayrıntılı olarak gözden geçirmek istediğiniz bir öneri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3091e-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="3091e-124">**Öneri** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3091e-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="3091e-125">Üzerinde **önerileri** dikey penceresinde, olası bir sorunu çözmek için gerçekleştirin veya bir maliyet tasarrufu fırsat yararlanmak Eylemler ilgili bilgileri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3091e-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Advisor önerisi dikey penceresinde](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="3091e-127">Advisor önerileri arayın</span><span class="sxs-lookup"><span data-stu-id="3091e-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="3091e-128">Belirli bir abonelik veya kaynak grubu için öneriler için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3091e-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="3091e-129">Ayrıca önerileri için duruma göre arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3091e-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="3091e-130">Oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3091e-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3091e-131">Abonelik, kaynak grupları ve öneri durumu filtreleyerek önerileri için arama (**etkin** veya **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="3091e-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="3091e-132">Arama filtresi ölçütlere göre Advisor önerileri listesini görüntülemek için tıklatın **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="3091e-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Advisor arama filtre ölçütü](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="3091e-134">Uykuda veya Advisor önerileri kapatın</span><span class="sxs-lookup"><span data-stu-id="3091e-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="3091e-135">Oturum [Azure portal](https://portal.azure.com)ve ardından başlatmak [Azure Danışmanı](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3091e-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3091e-136">' I tıklatın **alma önerileri**ve ardından öneriler listesinde bir öneri tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3091e-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="3091e-137">Üzerinde **öneri** dikey penceresinde tıklatın **uykuda**.</span><span class="sxs-lookup"><span data-stu-id="3091e-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Advisor öneri eylem örneği](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="3091e-139">Erteleme zaman aralığını belirtin veya seçin **hiçbir zaman** öneri kapatılamadı.</span><span class="sxs-lookup"><span data-stu-id="3091e-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3091e-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3091e-140">Next steps</span></span>

<span data-ttu-id="3091e-141">Advisor hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="3091e-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="3091e-142">Azure Danışmanı giriş</span><span class="sxs-lookup"><span data-stu-id="3091e-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="3091e-143">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="3091e-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="3091e-144">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="3091e-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="3091e-145">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="3091e-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="3091e-146">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="3091e-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)

---
title: "Azure CDN kaynakları sağlığını izlemek | Microsoft Docs"
description: "Azure kaynak durumu kullanarak Azure CDN kaynaklarınızı sağlığını izlemek öğrenin."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="c6b58-103">Azure CDN kaynakların durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="c6b58-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="c6b58-104">Azure CDN kaynak durumu olan bir alt kümesini [Azure kaynak durumu](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6b58-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="c6b58-105">Azure kaynak durumu CDN kaynakları sağlığını izlemek ve sorunlarını gidermek için işlem yapılabilir yönergeleri almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6b58-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c6b58-106">Azure CDN kaynak durumu şu anda yalnızca sistem durumunu genel CDN teslimi ve API özellikleri için hesapları.</span><span class="sxs-lookup"><span data-stu-id="c6b58-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="c6b58-107">Azure CDN kaynak durumu tek tek CDN uç noktası doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="c6b58-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="c6b58-108">Azure CDN kaynak durumu akışı sinyalleri Gecikmeli en fazla 15 dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6b58-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="c6b58-109">Azure CDN kaynak sistem durumu bulma</span><span class="sxs-lookup"><span data-stu-id="c6b58-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="c6b58-110">İçinde [Azure portal](https://portal.azure.com), CDN profilinize gidin.</span><span class="sxs-lookup"><span data-stu-id="c6b58-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="c6b58-111">Tıklatın **ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c6b58-111">Click the **Settings** button.</span></span>

    ![Ayarlar düğmesi](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="c6b58-113">Altında *destek + sorun giderme*, tıklatın **kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="c6b58-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN kaynak durumu](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="c6b58-115">Listelenen CDN kaynakları bulabileceğiniz *kaynak durumu* parçasında *Yardım + Destek* dikey.</span><span class="sxs-lookup"><span data-stu-id="c6b58-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="c6b58-116">Hızlı bir şekilde elde edebilirsiniz *Yardım + Destek* daire içinde tıklayarak **?**</span><span class="sxs-lookup"><span data-stu-id="c6b58-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="c6b58-117">Portalın sağ üst köşesinde.</span><span class="sxs-lookup"><span data-stu-id="c6b58-117">in the upper right corner of the portal.</span></span>
>
> ![Yardım + destek](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="c6b58-119">Azure CDN özgü iletileri</span><span class="sxs-lookup"><span data-stu-id="c6b58-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="c6b58-120">Azure CDN kaynak sağlığı ile ilgili durumlar altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c6b58-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="c6b58-121">İleti</span><span class="sxs-lookup"><span data-stu-id="c6b58-121">Message</span></span> | <span data-ttu-id="c6b58-122">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="c6b58-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="c6b58-123">Durdurulmuş, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış</span><span class="sxs-lookup"><span data-stu-id="c6b58-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="c6b58-124">Durduruldu, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış.</span><span class="sxs-lookup"><span data-stu-id="c6b58-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="c6b58-125">Özür dileriz, CDN yönetim hizmeti şu anda kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c6b58-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="c6b58-126">Geri durum güncelleştirmeleri için burayı tıklatın; Beklenen çözümleme süresi sonra sorununuz devam ederse desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6b58-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="c6b58-127">CDN uç noktalarınızı bazı bizim CDN sağlayıcıları ile devam eden sorunları tarafından etkilenebilir ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="c6b58-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="c6b58-128">Geri durum güncelleştirmeleri için burayı tıklatın; Kaynak ve CDN uç noktası test etmek öğrenmek için sorun giderme aracını kullanın; Beklenen çözümleme süresi sonra sorununuz devam ederse desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6b58-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="c6b58-129">CDN uç noktası yapılandırma değişikliklerini yayma gecikmeleri yaşıyor ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="c6b58-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="c6b58-130">Geri durum güncelleştirmeleri için burayı tıklatın; Yapılandırma değişiklikleri beklenen süre içinde tam olarak yayılmaz ederse Destek'e başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6b58-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="c6b58-131">Şu ek portal yükleme sorunlar yaşıyoruz ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="c6b58-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="c6b58-132">Geri durum güncelleştirmeleri için burayı tıklatın; Beklenen çözümleme süresi sonra sorununuz devam ederse desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6b58-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="c6b58-133">Üzgünüz, şu bizim CDN sağlayıcıları bazı sorunlar yaşıyoruz</span><span class="sxs-lookup"><span data-stu-id="c6b58-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="c6b58-134">Geri durum güncelleştirmeleri için burayı tıklatın; Beklenen çözümleme süresi sonra sorununuz devam ederse desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6b58-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6b58-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6b58-135">Next steps</span></span>

- [<span data-ttu-id="c6b58-136">Azure kaynak durumu genel bir bakış okuma</span><span class="sxs-lookup"><span data-stu-id="c6b58-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="c6b58-137">CDN sıkıştırma ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="c6b58-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="c6b58-138">404 hataları ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="c6b58-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)
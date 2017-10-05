---
title: "Azure CDN içindeki gerçek zamanlı İstatistikler | Microsoft Docs"
description: "Gerçek zamanlı İstatistikler istemcilerinize içerik teslim edilirken Azure CDN performansıyla ilgili gerçek zamanlı verileri sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="16c0a-103">Microsoft Azure cdn'de gerçek zamanlı İstatistikler</span><span class="sxs-lookup"><span data-stu-id="16c0a-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="16c0a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="16c0a-104">Overview</span></span>
<span data-ttu-id="16c0a-105">Bu belgede, Microsoft Azure cdn'de gerçek zamanlı İstatistikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="16c0a-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="16c0a-106">Bu işlevsellik, istemcilerinize içerik teslim edilirken bant genişliği, önbellek durumları ve CDN profilinizi yapılan eşzamanlı bağlantı gibi gerçek zamanlı verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="16c0a-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="16c0a-107">Bu, sürekli Hizmetinizin durumunu servise olaylar dahil olmak üzere, herhangi bir zamanda izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="16c0a-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="16c0a-108">Aşağıdaki grafikleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="16c0a-108">The following graphs are available:</span></span>

* [<span data-ttu-id="16c0a-109">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="16c0a-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="16c0a-110">Durum kodları</span><span class="sxs-lookup"><span data-stu-id="16c0a-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="16c0a-111">Önbellek durumları</span><span class="sxs-lookup"><span data-stu-id="16c0a-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="16c0a-112">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="16c0a-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="16c0a-113">Gerçek zamanlı İstatistikler erişme</span><span class="sxs-lookup"><span data-stu-id="16c0a-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="16c0a-114">İçinde [Azure Portal](https://portal.azure.com), CDN profilinize gidin.</span><span class="sxs-lookup"><span data-stu-id="16c0a-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN profili dikey penceresi](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="16c0a-116">CDN profili dikey penceresinden tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="16c0a-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="16c0a-118">CDN Yönetim Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="16c0a-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="16c0a-119">Üzerine gelerek **Analytics** sekmesini ve ardından üzerine gelerek **gerçek zamanlı İstatistikler** çıkma.</span><span class="sxs-lookup"><span data-stu-id="16c0a-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="16c0a-120">Tıklayın **HTTP büyük nesne**.</span><span class="sxs-lookup"><span data-stu-id="16c0a-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN Yönetim Portalı](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="16c0a-122">Gerçek zamanlı İstatistikler grafikleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="16c0a-123">Her grafikleri sayfa yüklendiğinde başlangıç seçilen zaman aralığı için gerçek zamanlı istatistikler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="16c0a-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="16c0a-124">Grafikler, her birkaç saniyede otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="16c0a-125">**Grafiği Yenile** , varsa, Temizle düğmesi daha sonra yalnızca gösterilir ve seçili verilerin grafik.</span><span class="sxs-lookup"><span data-stu-id="16c0a-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="16c0a-126">Bant Genişliği</span><span class="sxs-lookup"><span data-stu-id="16c0a-126">Bandwidth</span></span>
![Bant genişliği grafiği](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="16c0a-128">**Bant genişliği** grafiği geçerli platform için seçilen zaman aralığı içinde kullanılan bant genişliği miktarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="16c0a-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="16c0a-129">Grafik gölgeli kısmı bant genişliği kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="16c0a-130">Tam şu anda kullanılan bant genişliği miktarını doğrudan çizgi grafiği altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="16c0a-131">Durum kodları</span><span class="sxs-lookup"><span data-stu-id="16c0a-131">Status Codes</span></span>
![Durum kodu grafiği](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="16c0a-133">**Durum kodları** grafik belirli HTTP yanıt kodları seçilen zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="16c0a-134">HTTP durum kodu seçeneğin açıklaması için bkz: [Azure CDN HTTP durum kodları](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="16c0a-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="16c0a-135">HTTP durum kodları listesini doğrudan grafik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="16c0a-136">Bu liste çizgi grafiği ve bu durum kodu için saniye başına yinelenme sayısı dahil her durum kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="16c0a-137">Varsayılan olarak, bu durum kodunun grafikteki her biri için bir satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="16c0a-138">Ancak, yalnızca CDN yapılandırmanız için özel öneme sahip durum kodları izlemek için seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16c0a-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="16c0a-139">Bunu yapmak için istenen durum kodları denetleyin ve diğer tüm seçenekleri temizleyin ve ardından **Grafiği Yenile**.</span><span class="sxs-lookup"><span data-stu-id="16c0a-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="16c0a-140">Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16c0a-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="16c0a-141">Grafiğin altındaki doğrudan göstergeden gizlemek istediğiniz durum kodu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="16c0a-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="16c0a-142">Durum kodu hemen grafikten gizlenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="16c0a-143">Bu durum kodu yeniden tıklandığında yeniden görüntülenmesi için bu seçeneği neden olur.</span><span class="sxs-lookup"><span data-stu-id="16c0a-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="16c0a-144">Önbellek durumları</span><span class="sxs-lookup"><span data-stu-id="16c0a-144">Cache Statuses</span></span>
![Önbellek durumları grafiği](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="16c0a-146">**Önbellek durumları** grafik belirli türde bir önbellek durumları seçilen zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="16c0a-147">Her önbellek durum kodu seçeneği açıklaması için bkz: [Azure CDN önbellek durum kodları](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="16c0a-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="16c0a-148">Önbellek durum kodları listesini doğrudan grafik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="16c0a-149">Bu liste çizgi grafiği ve bu durum kodu için saniye başına yinelenme sayısı dahil her durum kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="16c0a-150">Varsayılan olarak, bu durum kodunun grafikteki her biri için bir satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="16c0a-151">Ancak, yalnızca CDN yapılandırmanız için özel öneme sahip durum kodları izlemek için seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16c0a-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="16c0a-152">Bunu yapmak için istenen durum kodları denetleyin ve diğer tüm seçenekleri temizleyin ve ardından **Grafiği Yenile**.</span><span class="sxs-lookup"><span data-stu-id="16c0a-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="16c0a-153">Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16c0a-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="16c0a-154">Grafiğin altındaki doğrudan göstergeden gizlemek istediğiniz durum kodu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="16c0a-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="16c0a-155">Durum kodu hemen grafikten gizlenir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="16c0a-156">Bu durum kodu yeniden tıklandığında yeniden görüntülenmesi için bu seçeneği neden olur.</span><span class="sxs-lookup"><span data-stu-id="16c0a-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="16c0a-157">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="16c0a-157">Connections</span></span>
![Bağlantıları grafiği](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="16c0a-159">Bu grafik, kaç tane bağlantıları kenar sunucularınızı kurulmuş gösterir.</span><span class="sxs-lookup"><span data-stu-id="16c0a-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="16c0a-160">Her istek için bir bağlantı bizim CDN sonuçlarında geçtiği bir varlık.</span><span class="sxs-lookup"><span data-stu-id="16c0a-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c0a-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="16c0a-161">Next Steps</span></span>
* <span data-ttu-id="16c0a-162">İle bilgi edinin [Azure CDN gerçek zamanlı uyarılar](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="16c0a-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="16c0a-163">Dıg ile daha derin [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="16c0a-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="16c0a-164">Analiz [kullanım desenleri](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="16c0a-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>


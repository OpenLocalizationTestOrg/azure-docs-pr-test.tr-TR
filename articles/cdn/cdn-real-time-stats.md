---
title: "Azure CDN içinde aaaReal zamanı istatistikleri | Microsoft Docs"
description: "Gerçek zamanlı İstatistikler içerik tooyour istemcileri teslim edilirken Azure CDN hello performansını hakkında gerçek zamanlı verileri sağlar."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="98a57-103">Microsoft Azure cdn'de gerçek zamanlı İstatistikler</span><span class="sxs-lookup"><span data-stu-id="98a57-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="98a57-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="98a57-104">Overview</span></span>
<span data-ttu-id="98a57-105">Bu belgede, Microsoft Azure cdn'de gerçek zamanlı İstatistikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="98a57-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="98a57-106">Bu işlev içerik tooyour istemcileri teslim edilirken bant genişliği, önbellek durumları ve eşzamanlı bağlantı tooyour CDN profili gibi gerçek zamanlı verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="98a57-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="98a57-107">Bu, sürekli hello Hizmetinizin durumunu servise olaylar dahil olmak üzere, herhangi bir zamanda izlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="98a57-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="98a57-108">grafikleri aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="98a57-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="98a57-109">Bant genişliği</span><span class="sxs-lookup"><span data-stu-id="98a57-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="98a57-110">Durum kodları</span><span class="sxs-lookup"><span data-stu-id="98a57-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="98a57-111">Önbellek durumları</span><span class="sxs-lookup"><span data-stu-id="98a57-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="98a57-112">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="98a57-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="98a57-113">Gerçek zamanlı İstatistikler erişme</span><span class="sxs-lookup"><span data-stu-id="98a57-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="98a57-114">Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="98a57-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN profili dikey penceresi](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="98a57-116">Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98a57-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="98a57-118">Merhaba CDN Yönetim Portalı açar.</span><span class="sxs-lookup"><span data-stu-id="98a57-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="98a57-119">Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **gerçek zamanlı İstatistikler** çıkma.</span><span class="sxs-lookup"><span data-stu-id="98a57-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="98a57-120">Tıklayın **HTTP büyük nesne**.</span><span class="sxs-lookup"><span data-stu-id="98a57-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN Yönetim Portalı](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="98a57-122">Merhaba gerçek zamanlı İstatistikler grafikleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="98a57-123">Her hello grafikleri hello sayfa yüklendiğinde başlangıç hello seçili zaman aralığı için gerçek zamanlı istatistikler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="98a57-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="98a57-124">Merhaba grafikleri birkaç dakikada otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="98a57-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="98a57-125">Merhaba **Grafiği Yenile** , varsa, Temizle düğmesi hello grafiği, daha sonra yalnızca gösterilir seçili hello veri.</span><span class="sxs-lookup"><span data-stu-id="98a57-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="98a57-126">Bant Genişliği</span><span class="sxs-lookup"><span data-stu-id="98a57-126">Bandwidth</span></span>
![Bant genişliği grafiği](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="98a57-128">Merhaba **bant genişliği** grafiği hello hello seçili zaman aralığı içinde hello geçerli platform için kullanılan bant genişliği miktarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="98a57-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="98a57-129">Merhaba gölgeli hello grafik kısmı bant genişliği kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="98a57-130">Merhaba tam şu anda kullanılan bant genişliği miktarını doğrudan hello çizgi grafiği altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="98a57-131">Durum kodları</span><span class="sxs-lookup"><span data-stu-id="98a57-131">Status Codes</span></span>
![Durum kodu grafiği](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="98a57-133">Merhaba **durum kodları** grafik belirli HTTP yanıt kodları hello seçili zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="98a57-134">HTTP durum kodu seçeneğin açıklaması için bkz: [Azure CDN HTTP durum kodları](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="98a57-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="98a57-135">HTTP durum kodları listesini doğrudan hello grafik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="98a57-136">Bu liste hello çizgi grafiği ve hello geçerli sayısı, durum kodu için saniye başına dahil her durum kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="98a57-137">Varsayılan olarak, bu durum kodunun hello grafikteki her biri için bir satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="98a57-138">Ancak, CDN yapılandırmanız için özel öneme sahip İzleyicisi Merhaba durum kodları tooonly seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a57-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="98a57-139">toodo Bu, istenen hello durum kodları denetleyin ve diğer tüm seçeneklerini temizleyin ve ardından **Grafiği Yenile**.</span><span class="sxs-lookup"><span data-stu-id="98a57-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="98a57-140">Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a57-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="98a57-141">Doğrudan hello grafik aşağıda Hello göstergeden toohide istediğiniz hello durum kodu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="98a57-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="98a57-142">Merhaba durum kodu hemen hello grafikten gizlenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="98a57-143">Bu durum kodu yeniden tıklandığında yeniden görüntülenen bu seçeneği toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="98a57-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="98a57-144">Önbellek durumları</span><span class="sxs-lookup"><span data-stu-id="98a57-144">Cache Statuses</span></span>
![Önbellek durumları grafiği](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="98a57-146">Merhaba **önbellek durumları** grafik belirli türde bir önbellek durumları hello seçili zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="98a57-147">Her önbellek durum kodu seçeneği açıklaması için bkz: [Azure CDN önbellek durum kodları](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="98a57-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="98a57-148">Önbellek durum kodları listesini doğrudan hello grafik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="98a57-149">Bu liste hello çizgi grafiği ve hello geçerli sayısı, durum kodu için saniye başına dahil her durum kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="98a57-150">Varsayılan olarak, bu durum kodunun hello grafikteki her biri için bir satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="98a57-151">Ancak, CDN yapılandırmanız için özel öneme sahip İzleyicisi Merhaba durum kodları tooonly seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a57-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="98a57-152">toodo Bu, istenen hello durum kodları denetleyin ve diğer tüm seçeneklerini temizleyin ve ardından **Grafiği Yenile**.</span><span class="sxs-lookup"><span data-stu-id="98a57-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="98a57-153">Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a57-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="98a57-154">Doğrudan hello grafik aşağıda Hello göstergeden toohide istediğiniz hello durum kodu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="98a57-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="98a57-155">Merhaba durum kodu hemen hello grafikten gizlenir.</span><span class="sxs-lookup"><span data-stu-id="98a57-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="98a57-156">Bu durum kodu yeniden tıklandığında yeniden görüntülenen bu seçeneği toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="98a57-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="98a57-157">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="98a57-157">Connections</span></span>
![Bağlantıları grafiği](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="98a57-159">Bu grafik, kaç tane bağlantıları kurulan tooyour uç sunucuların edildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98a57-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="98a57-160">Her istek için bir bağlantı bizim CDN sonuçlarında geçtiği bir varlık.</span><span class="sxs-lookup"><span data-stu-id="98a57-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98a57-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="98a57-161">Next Steps</span></span>
* <span data-ttu-id="98a57-162">İle bilgi edinin [Azure CDN gerçek zamanlı uyarılar](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="98a57-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="98a57-163">Dıg ile daha derin [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="98a57-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="98a57-164">Analiz [kullanım desenleri](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="98a57-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>


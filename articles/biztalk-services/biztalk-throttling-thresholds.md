---
title: "BizTalk Services'da azaltma hakkında bilgi edinin | Microsoft Docs"
description: "Eşikleri azaltma ve BizTalk Services için çalışma zamanı davranışlarını kaynaklanan hakkında bilgi edinin. Azaltma, bellek kullanımı ve ileti sayısını temel alır. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="f3b44-105">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="f3b44-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="f3b44-106">Azure BizTalk Services uygulayan iki koşullara göre hizmet azaltma: bellek kullanımı ve işleme eşzamanlı iletilerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="f3b44-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="f3b44-107">Bu konuda kısıtlama eşikleri listeler ve azaltma bir koşul oluştuğunda çalışma zamanı davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f3b44-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="f3b44-108">Daraltma eşikleri</span><span class="sxs-lookup"><span data-stu-id="f3b44-108">Throttling Thresholds</span></span>
<span data-ttu-id="f3b44-109">Azaltma kaynak ve eşikleri aşağıdaki tabloda listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="f3b44-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="f3b44-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f3b44-110">Description</span></span> | <span data-ttu-id="f3b44-111">Düşük eşik</span><span class="sxs-lookup"><span data-stu-id="f3b44-111">Low Threshold</span></span> | <span data-ttu-id="f3b44-112">Yüksek eşiği</span><span class="sxs-lookup"><span data-stu-id="f3b44-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f3b44-113">Bellek</span><span class="sxs-lookup"><span data-stu-id="f3b44-113">Memory</span></span> |<span data-ttu-id="f3b44-114">Toplam sistem bellek kullanılabilir/PageFileBytes yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="f3b44-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="f3b44-115">Toplam kullanılabilir PageFileBytes yaklaşık 2 kez RAM sisteminin olur.</span><span class="sxs-lookup"><span data-stu-id="f3b44-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="f3b44-116">60%</span><span class="sxs-lookup"><span data-stu-id="f3b44-116">60%</span></span> |<span data-ttu-id="f3b44-117">70%</span><span class="sxs-lookup"><span data-stu-id="f3b44-117">70%</span></span> |
| <span data-ttu-id="f3b44-118">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="f3b44-118">Message Processing</span></span> |<span data-ttu-id="f3b44-119">Aynı anda işlenen ileti sayısı</span><span class="sxs-lookup"><span data-stu-id="f3b44-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="f3b44-120">40 * çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="f3b44-120">40 * number of cores</span></span> |<span data-ttu-id="f3b44-121">100 * çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="f3b44-121">100 * number of cores</span></span> |

<span data-ttu-id="f3b44-122">Bir üst Eşiğe ulaşıldığında, Azure BizTalk Services kısıtlama başlar.</span><span class="sxs-lookup"><span data-stu-id="f3b44-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="f3b44-123">Düşük Eşiğe ulaşıldığında durakları azaltma.</span><span class="sxs-lookup"><span data-stu-id="f3b44-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="f3b44-124">Örneğin, hizmetiniz %65 sistem bellek kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f3b44-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="f3b44-125">Bu durumda, hizmet kısıtlama yok.</span><span class="sxs-lookup"><span data-stu-id="f3b44-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="f3b44-126">Hizmetinizi % 70 sistem belleği kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="f3b44-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="f3b44-127">Bu durumda, hizmet kısıtlar ve hizmeti, % 60 (düşük eşik) sistem belleği kullanır kadar kısıtlama devam eder.</span><span class="sxs-lookup"><span data-stu-id="f3b44-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="f3b44-128">Azure BizTalk Services azaltma durumunu (daraltılmış durumu karşılaştırması normal durum) ve azaltma süresi izler.</span><span class="sxs-lookup"><span data-stu-id="f3b44-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="f3b44-129">Çalışma zamanı davranışı</span><span class="sxs-lookup"><span data-stu-id="f3b44-129">Runtime Behavior</span></span>
<span data-ttu-id="f3b44-130">Azure BizTalk Services azaltma durumuna girdiğinde, aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="f3b44-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="f3b44-131">Azaltma rol örneğidir.</span><span class="sxs-lookup"><span data-stu-id="f3b44-131">Throttling is per role instance.</span></span> <span data-ttu-id="f3b44-132">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f3b44-132">For example:</span></span><br/>
  <span data-ttu-id="f3b44-133">RoleInstanceA azaltma.</span><span class="sxs-lookup"><span data-stu-id="f3b44-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="f3b44-134">RoleInstanceB azaltma değil.</span><span class="sxs-lookup"><span data-stu-id="f3b44-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="f3b44-135">Bu durumda, RoleInstanceB iletilerinde beklendiği gibi işlenir.</span><span class="sxs-lookup"><span data-stu-id="f3b44-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="f3b44-136">RoleInstanceA iletilerinde atılır ve şu hatayı vererek başarısız:</span><span class="sxs-lookup"><span data-stu-id="f3b44-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="f3b44-137">
  **Sunucu meşgul. Lütfen yeniden deneyin.**</span><span class="sxs-lookup"><span data-stu-id="f3b44-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="f3b44-138">Herhangi bir çekme kaynağına etmeyin yoklamak veya bir ileti indirin.</span><span class="sxs-lookup"><span data-stu-id="f3b44-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="f3b44-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f3b44-139">For example:</span></span><br/>
  <span data-ttu-id="f3b44-140">Ardışık iletilerin bir dış FTP kaynaktan çeker.</span><span class="sxs-lookup"><span data-stu-id="f3b44-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="f3b44-141">Çekme yapılması rol örneği azaltma bir duruma alır.</span><span class="sxs-lookup"><span data-stu-id="f3b44-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="f3b44-142">Bu durumda, ardışık düzen azaltma rol örneği durdurur kadar ek iletilerin indirilmesi durdurur.</span><span class="sxs-lookup"><span data-stu-id="f3b44-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="f3b44-143">İstemci ileti yeniden gönderebilirsiniz şekilde yanıt istemciye gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f3b44-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="f3b44-144">Azaltma Sorun çözülene kadar beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3b44-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="f3b44-145">Özellikle, düşük eşik ulaşılana kadar beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f3b44-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="f3b44-146">Önemli Notlar</span><span class="sxs-lookup"><span data-stu-id="f3b44-146">Important notes</span></span>
* <span data-ttu-id="f3b44-147">Azaltma devre dışı bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="f3b44-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="f3b44-148">Daraltma eşikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="f3b44-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="f3b44-149">Azaltma, sistem genelinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f3b44-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="f3b44-150">Azure SQL veritabanı sunucusu, yerleşik azaltma da sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f3b44-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="f3b44-151">Ek Azure BizTalk Services konuları</span><span class="sxs-lookup"><span data-stu-id="f3b44-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="f3b44-152">Azure BizTalk Services SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="f3b44-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="f3b44-153">Öğretici: Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f3b44-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="f3b44-154">Azure BizTalk Services SDK'sını Kullanmaya Nasıl Başlarım</span><span class="sxs-lookup"><span data-stu-id="f3b44-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="f3b44-155">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f3b44-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="f3b44-156">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f3b44-156">See Also</span></span>
* [<span data-ttu-id="f3b44-157">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="f3b44-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="f3b44-158">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="f3b44-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="f3b44-159">BizTalk Services: Durum Grafiğini hazırlama</span><span class="sxs-lookup"><span data-stu-id="f3b44-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="f3b44-160">BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri</span><span class="sxs-lookup"><span data-stu-id="f3b44-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="f3b44-161">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="f3b44-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="f3b44-162">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="f3b44-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>


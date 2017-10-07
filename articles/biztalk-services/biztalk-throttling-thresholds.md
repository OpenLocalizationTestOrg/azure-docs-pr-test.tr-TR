---
title: "BizTalk Services azaltma hakkında aaaLearn | Microsoft Docs"
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="2c112-105">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="2c112-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="2c112-106">Azure BizTalk Services uygulayan iki koşullara göre hizmet azaltma: bellek kullanımı ve hello işleme eşzamanlı ileti sayısı.</span><span class="sxs-lookup"><span data-stu-id="2c112-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="2c112-107">Bu konuda daraltma eşikleri hello listeler ve azaltma bir koşul oluştuğunda hello çalışma zamanı davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2c112-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="2c112-108">Daraltma eşikleri</span><span class="sxs-lookup"><span data-stu-id="2c112-108">Throttling Thresholds</span></span>
<span data-ttu-id="2c112-109">Aşağıdaki tabloda hello azaltma kaynak ve eşikleri hello:</span><span class="sxs-lookup"><span data-stu-id="2c112-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="2c112-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2c112-110">Description</span></span> | <span data-ttu-id="2c112-111">Düşük eşik</span><span class="sxs-lookup"><span data-stu-id="2c112-111">Low Threshold</span></span> | <span data-ttu-id="2c112-112">Yüksek eşiği</span><span class="sxs-lookup"><span data-stu-id="2c112-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2c112-113">Bellek</span><span class="sxs-lookup"><span data-stu-id="2c112-113">Memory</span></span> |<span data-ttu-id="2c112-114">Toplam sistem bellek kullanılabilir/PageFileBytes yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="2c112-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="2c112-115">Toplam kullanılabilir PageFileBytes yaklaşık 2 kez hello RAM hello sisteminin olur.</span><span class="sxs-lookup"><span data-stu-id="2c112-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="2c112-116">60%</span><span class="sxs-lookup"><span data-stu-id="2c112-116">60%</span></span> |<span data-ttu-id="2c112-117">70%</span><span class="sxs-lookup"><span data-stu-id="2c112-117">70%</span></span> |
| <span data-ttu-id="2c112-118">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="2c112-118">Message Processing</span></span> |<span data-ttu-id="2c112-119">Aynı anda işlenen ileti sayısı</span><span class="sxs-lookup"><span data-stu-id="2c112-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="2c112-120">40 * çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="2c112-120">40 * number of cores</span></span> |<span data-ttu-id="2c112-121">100 * çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="2c112-121">100 * number of cores</span></span> |

<span data-ttu-id="2c112-122">Bir üst Eşiğe ulaşıldığında, Azure BizTalk Services toothrottle başlatır.</span><span class="sxs-lookup"><span data-stu-id="2c112-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="2c112-123">Merhaba düşük Eşiğe ulaşıldığında azaltma durdurur.</span><span class="sxs-lookup"><span data-stu-id="2c112-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="2c112-124">Örneğin, hizmetiniz %65 sistem bellek kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="2c112-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="2c112-125">Bu durumda, hello hizmet kısıtlama yok.</span><span class="sxs-lookup"><span data-stu-id="2c112-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="2c112-126">Hizmetinizi % 70 sistem belleği kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="2c112-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="2c112-127">Bu durumda, hello hizmeti kısıtlar ve toothrottle hello hizmeti, % 60 (düşük eşik) sistem belleği kullanır kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="2c112-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="2c112-128">Azure BizTalk Services durumunu (daraltılmış durumu karşılaştırması normal durum) azaltma hello ve süresini azaltma hello izler.</span><span class="sxs-lookup"><span data-stu-id="2c112-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="2c112-129">Çalışma zamanı davranışı</span><span class="sxs-lookup"><span data-stu-id="2c112-129">Runtime Behavior</span></span>
<span data-ttu-id="2c112-130">Azure BizTalk Services azaltma durumuna girdiğinde, hello şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="2c112-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="2c112-131">Azaltma rol örneğidir.</span><span class="sxs-lookup"><span data-stu-id="2c112-131">Throttling is per role instance.</span></span> <span data-ttu-id="2c112-132">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2c112-132">For example:</span></span><br/>
  <span data-ttu-id="2c112-133">RoleInstanceA azaltma.</span><span class="sxs-lookup"><span data-stu-id="2c112-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="2c112-134">RoleInstanceB azaltma değil.</span><span class="sxs-lookup"><span data-stu-id="2c112-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="2c112-135">Bu durumda, RoleInstanceB iletilerinde beklendiği gibi işlenir.</span><span class="sxs-lookup"><span data-stu-id="2c112-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="2c112-136">RoleInstanceA iletilerinde atılır ve hello aşağıdaki hata ile başarısız:</span><span class="sxs-lookup"><span data-stu-id="2c112-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="2c112-137">
  **Sunucu meşgul. Lütfen yeniden deneyin.**</span><span class="sxs-lookup"><span data-stu-id="2c112-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="2c112-138">Herhangi bir çekme kaynağına etmeyin yoklamak veya bir ileti indirin.</span><span class="sxs-lookup"><span data-stu-id="2c112-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="2c112-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2c112-139">For example:</span></span><br/>
  <span data-ttu-id="2c112-140">Ardışık iletilerin bir dış FTP kaynaktan çeker.</span><span class="sxs-lookup"><span data-stu-id="2c112-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="2c112-141">Merhaba çekme yapılması hello rol örneği azaltma bir duruma alır.</span><span class="sxs-lookup"><span data-stu-id="2c112-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="2c112-142">Bu durumda, azaltma hello rol örneği durdurur kadar ek iletilerin indirilmesi hello ardışık düzen durdurur.</span><span class="sxs-lookup"><span data-stu-id="2c112-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="2c112-143">Merhaba istemci selamlama iletisine yeniden gönderebilirsiniz şekilde yanıt toohello istemci gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2c112-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="2c112-144">Merhaba azaltma çözülene kadar beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c112-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="2c112-145">Özellikle, Hello düşük eşik ulaşılana kadar beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2c112-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="2c112-146">Önemli Notlar</span><span class="sxs-lookup"><span data-stu-id="2c112-146">Important notes</span></span>
* <span data-ttu-id="2c112-147">Azaltma devre dışı bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="2c112-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="2c112-148">Daraltma eşikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="2c112-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="2c112-149">Azaltma, sistem genelinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2c112-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="2c112-150">Yerleşik azaltma Hello Azure SQL veritabanı sunucusuna da sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2c112-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="2c112-151">Ek Azure BizTalk Services konuları</span><span class="sxs-lookup"><span data-stu-id="2c112-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="2c112-152">Hello Azure BizTalk Services SDK'sını yükleme</span><span class="sxs-lookup"><span data-stu-id="2c112-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="2c112-153">Öğretici: Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="2c112-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="2c112-154">I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello</span><span class="sxs-lookup"><span data-stu-id="2c112-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="2c112-155">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="2c112-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="2c112-156">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="2c112-156">See Also</span></span>
* [<span data-ttu-id="2c112-157">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="2c112-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="2c112-158">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="2c112-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="2c112-159">BizTalk Services: Durum Grafiğini hazırlama</span><span class="sxs-lookup"><span data-stu-id="2c112-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="2c112-160">BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri</span><span class="sxs-lookup"><span data-stu-id="2c112-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="2c112-161">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="2c112-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="2c112-162">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="2c112-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>


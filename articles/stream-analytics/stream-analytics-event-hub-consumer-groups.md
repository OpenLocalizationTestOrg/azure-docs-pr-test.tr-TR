---
title: "Olay hub'ı alıcıları ile aaaDebug Azure akış analizi | Microsoft Docs"
description: "Olay hub'ları tüketici grupları, Stream Analytics işlerini dikkate için en iyi uygulamaları sorgulayın."
keywords: "Olay hub'ı sınırı, tüketici grubu"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="ecf26-104">Azure Stream Analytics olay hub'ı alıcıları ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="ecf26-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="ecf26-105">Azure Event Hubs Azure akış analizi tooingest çıktı verileri veya bir iş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf26-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="ecf26-106">Olay hub'ları kullanmak için en iyi uygulama toouse olan birden çok tüketici grupları, tooensure iş ölçeklenebilirlik.</span><span class="sxs-lookup"><span data-stu-id="ecf26-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="ecf26-107">Belirli bir giriş için hello Stream Analytics işinde okuyucu hello sayısını hello tek bir tüketici grubundaki okuyucu sayısını etkiler bir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="ecf26-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="ecf26-108">Merhaba kesin alıcıları sayısı iç uygulama ayrıntılarını hello genişleme topoloji mantığı için temel alır.</span><span class="sxs-lookup"><span data-stu-id="ecf26-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="ecf26-109">Alıcıları Hello sayısı harici olarak gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="ecf26-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="ecf26-110">Okuyucu Hello sayısını hello iş başlangıç saatinde veya iş yükseltme sırasında değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf26-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf26-111">Okuyucu Hello sayısını iş yükseltme sırasında değiştiğinde geçici uyarıları tooaudit günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="ecf26-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="ecf26-112">Akış analizi işleri, bu geçici sorunları otomatik olarak kurtarın.</span><span class="sxs-lookup"><span data-stu-id="ecf26-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="ecf26-113">Bölüm başına okuyucu sayısını beş olay hub'ları sınırını aşıyor</span><span class="sxs-lookup"><span data-stu-id="ecf26-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="ecf26-114">Hangi hello bölüm başına okuyucu sayısını beş hello olay hub'ları sınırını aşıyor. senaryoları hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ecf26-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="ecf26-115">Birden çok SELECT deyimine: çok başvuran birden çok SELECT deyimine kullanırsanız**aynı** olay hub'ı girin, her SELECT deyiminin oluşturulan yeni bir alıcı toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="ecf26-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="ecf26-116">BİRLEŞİM: bir birleşim kullandığınızda, olası toohave olmasından toohello başvuran birden çok girişi **aynı** olay hub'ı ve tüketici grubu.</span><span class="sxs-lookup"><span data-stu-id="ecf26-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="ecf26-117">Kendi KENDİNE BİRLEŞİMDE: SELF katılma işlemi kullandığınızda, olası toorefer toohello olmasından **aynı** olay hub'ı birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="ecf26-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="ecf26-118">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ecf26-118">Solution</span></span>

<span data-ttu-id="ecf26-119">Merhaba aşağıdaki en iyi yöntemleri hangi hello bölüm başına okuyucu sayısını beş hello olay hub'ları sınırını aşıyor. senaryoları azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ecf26-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="ecf26-120">WITH yan tümcesini kullanarak sorgunuzu içine birden çok adımı bölme</span><span class="sxs-lookup"><span data-stu-id="ecf26-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="ecf26-121">Merhaba WITH yan tümcesi hello sorgusunda FROM yan tümcesi tarafından başvurulan bir geçici adlandırılmış sonuç kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ecf26-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="ecf26-122">Merhaba WITH yan tümcesi hello yürütme kapsamında tek bir SELECT deyimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ecf26-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="ecf26-123">Örneğin, bu sorgu yerine:</span><span class="sxs-lookup"><span data-stu-id="ecf26-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="ecf26-124">Bu sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ecf26-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="ecf26-125">Girişleri toodifferent tüketici grupları bağlamak emin olun</span><span class="sxs-lookup"><span data-stu-id="ecf26-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="ecf26-126">Üç veya daha fazla girdi bağlı toohello olan sorguları için aynı olay hub'ları tüketici grubunda, ayrı tüketici grupları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecf26-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="ecf26-127">Bu ek Stream Analytics girişleri hello oluşturulmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ecf26-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="ecf26-128">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="ecf26-128">Get help</span></span>
<span data-ttu-id="ecf26-129">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ecf26-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecf26-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ecf26-130">Next steps</span></span>
* [<span data-ttu-id="ecf26-131">Giriş tooStream analizi</span><span class="sxs-lookup"><span data-stu-id="ecf26-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ecf26-132">Stream Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ecf26-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ecf26-133">Stream Analytics işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ecf26-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ecf26-134">Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="ecf26-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ecf26-135">Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="ecf26-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

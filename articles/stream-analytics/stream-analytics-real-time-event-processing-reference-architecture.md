---
title: "Stream Analytics olay işleme ile işleme aaaReal zamanı olay | Microsoft Docs"
description: "Gerçek zamanlı Olay işleme ve analizi etkinleştirmek için Azure Hizmetleri kümesi nasıl çalışabilirler öğrenin."
keywords: "gerçek zamanlı işleme, olay işleme, referans mimarisi"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="ddd99-104">Başvuru mimarisi: Gerçek zamanlı Olay Microsoft Azure akış Analizi ile işleme</span><span class="sxs-lookup"><span data-stu-id="ddd99-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="ddd99-105">gerçek zamanlı Olay Azure akış Analizi ile işleme için Hello başvuru mimarisi hedeflenen tooprovide gerçek zamanlı bir platform Microsoft Azure ile hizmet (PaaS) akış işleme çözümü olarak dağıtmak için genel Şeması ' dir.</span><span class="sxs-lookup"><span data-stu-id="ddd99-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="ddd99-106">Özet</span><span class="sxs-lookup"><span data-stu-id="ddd99-106">Summary</span></span>
<span data-ttu-id="ddd99-107">Geleneksel olarak, analiz çözümleri yeteneklerine ETL (ayıklama, dönüştürme ve yükleme) ve veri ambarı, gibi veri depolanan önceki tooanalysis nerede dayalı.</span><span class="sxs-lookup"><span data-stu-id="ddd99-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="ddd99-108">Daha fazla hızlı bir şekilde gelen veriler dahil değişen gereksinimleri, bu varolan modeli toohello sınırı zorlayan.</span><span class="sxs-lookup"><span data-stu-id="ddd99-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="ddd99-109">Yeni bir özellik olmamasına karşın, hello yaklaşım yaygın tüm endüstri verticals benimsemiştir değil ve Hello özelliği tooanalyze veri taşıma akışları önceki toostorage içinde bir çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="ddd99-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="ddd99-110">Microsoft Azure bir dizi farklı çözüm senaryoları ve gereksinimleri destekleyebildiğini analytics teknolojilerin kapsamlı bir katalog sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddd99-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="ddd99-111">Hangi Azure Hizmetleri toodeploy uçtan uca çözümü teklifleri hello derecesini verilen zor olabilir seçme.</span><span class="sxs-lookup"><span data-stu-id="ddd99-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="ddd99-112">Bu yazı tasarlanmış toodescribe hello özellikleri olduğunu ve birlikte çalışabilirlik, hello olay akışı çözümünü destekleyen çeşitli Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ddd99-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="ddd99-113">Ayrıca müşteriler bu yaklaşım türünden yararlanabilir hello senaryolardan bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ddd99-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="ddd99-114">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="ddd99-114">Contents</span></span>
* <span data-ttu-id="ddd99-115">Yönetici Özeti</span><span class="sxs-lookup"><span data-stu-id="ddd99-115">Executive Summary</span></span>
* <span data-ttu-id="ddd99-116">Giriş tooReal zamanı analizi</span><span class="sxs-lookup"><span data-stu-id="ddd99-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="ddd99-117">Değer teklifinde Azure gerçek zamanlı veri</span><span class="sxs-lookup"><span data-stu-id="ddd99-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="ddd99-118">Gerçek zamanlı analiz için ortak senaryolar</span><span class="sxs-lookup"><span data-stu-id="ddd99-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="ddd99-119">Mimarisi ve bileşenleri</span><span class="sxs-lookup"><span data-stu-id="ddd99-119">Architecture and Components</span></span>
  * <span data-ttu-id="ddd99-120">Veri Kaynakları</span><span class="sxs-lookup"><span data-stu-id="ddd99-120">Data Sources</span></span>
  * <span data-ttu-id="ddd99-121">Veri tümleştirme katmanı</span><span class="sxs-lookup"><span data-stu-id="ddd99-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="ddd99-122">Gerçek zamanlı analiz katmanı</span><span class="sxs-lookup"><span data-stu-id="ddd99-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="ddd99-123">Veri depolama katmanı</span><span class="sxs-lookup"><span data-stu-id="ddd99-123">Data Storage Layer</span></span>
  * <span data-ttu-id="ddd99-124">Sunu / tüketim katman</span><span class="sxs-lookup"><span data-stu-id="ddd99-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="ddd99-125">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ddd99-125">Conclusion</span></span>

<span data-ttu-id="ddd99-126">**Yazar:** mükemmel, Microsoft Corporation'ın Charles Feddersen, çözümü Mimarı veri Öngörüler Merkezi</span><span class="sxs-lookup"><span data-stu-id="ddd99-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="ddd99-127">**Yayımlanan:** Ocak 2015</span><span class="sxs-lookup"><span data-stu-id="ddd99-127">**Published:** January 2015</span></span>

<span data-ttu-id="ddd99-128">**Düzeltme:** 1.0</span><span class="sxs-lookup"><span data-stu-id="ddd99-128">**Revision:** 1.0</span></span>

<span data-ttu-id="ddd99-129">**İndirin:** [gerçek zamanlı Olay Microsoft Azure akış Analizi ile işleme](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="ddd99-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="ddd99-130">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="ddd99-130">Get help</span></span>
<span data-ttu-id="ddd99-131">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="ddd99-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd99-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddd99-132">Next steps</span></span>
* [<span data-ttu-id="ddd99-133">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="ddd99-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ddd99-134">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ddd99-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ddd99-135">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ddd99-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ddd99-136">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="ddd99-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ddd99-137">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="ddd99-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


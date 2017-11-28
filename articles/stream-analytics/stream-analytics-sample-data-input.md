---
title: "Azure Stream Analytics içinde AAA örnekleme girişleri | Microsoft Docs"
description: "Akış analizi işleri giderirken sorunları belirlemenize."
keywords: "Giriş, giriş örnekleme sorun giderme"
documentationcenter: 
services: stream-analytics
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="8a2fb-104">Azure Stream Analytics Giriş akışı örnekleme</span><span class="sxs-lookup"><span data-stu-id="8a2fb-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="8a2fb-105">Azure akış analizi kullanarak, bir dosyadan gelen ve sorguları toostart gerek kalmadan hello Portalı'nda test ya da bir işi durdurmak giriş olaylarını örnek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="8a2fb-106">Sorgunuz test etme</span><span class="sxs-lookup"><span data-stu-id="8a2fb-106">Testing your query</span></span>

<span data-ttu-id="8a2fb-107">Merhaba Hello Stream Analytics işi Ayrıntılar bölmesinde, açmak **sorgu Düzenleyicisi'ni** hello sorgu adı altında dikey **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="8a2fb-108">(Hiçbir sorgu henüz oluşturulduğundan bizim örnek senaryoda hello tıklatın **< >** yer tutucu.)</span><span class="sxs-lookup"><span data-stu-id="8a2fb-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![Merhaba Stream Analytics sorgu Düzenleyicisi](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="8a2fb-110">sorgunuzu oluşturmak için zengin bir düzenleyici dikey penceresinde hello hello önceki sürümünde olduğu gibi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="8a2fb-111">Merhaba dikey yeni bir güncelleştirildi artık bu gösterir hello giriş ve hello sorgu tarafından kullanılan ve bu proje için tanımlanan çıkış sol bölme.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![Merhaba Stream Analytics sorgu Düzenleyicisi'ni girdilerin ve listeleri çıkarır](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="8a2fb-113">Ayrıca gösterilen bir ek giriş ve çıkış, tanımlanmamış'dır.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="8a2fb-114">İle başlayan hello yeni sorgu şablonu geliyor.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="8a2fb-115">Bunlar değiştirebilir veya hatta hello sorgu düzenlerken tamamen kaybolur.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="8a2fb-116">Bunları şu an için güvenle yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="8a2fb-117">Örnek giriş verilerle tootest girişlerinizi hiçbirini sağ tıklayın ve ardından **dosyasından örnek verileri yükleme**.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Stream Analytics sorgu Düzenleyicisi'ni karşıya yükleme örnek veri dosyası komutundan hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="8a2fb-119">Merhaba karşıya yükleme tamamlandıktan sonra tıklayın **Test** tootest hello bu sorgusu örnek yalnızca sağlanan verileri.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![Merhaba Stream Analytics sorgu Düzenleyicisi'ni Test düğmesi](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="8a2fb-121">Daha sonra kullanmak üzere toosave hello test çıkışı istiyorsanız, sorgunuzu hello çıktısını hello tarayıcı bağlantı toohello indirme sonuçlarını ile görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="8a2fb-122">Artık kolayca ve yinelemeli olarak Sorgunuzu değiştirin ve tekrar tekrar hello çıkış nasıl değiştiğini toosee test.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Stream Analytics sorgu Düzenleyicisi'ni örnek çıkış](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="8a2fb-124">Görüntü önceki hello içinde ikinci bir çıkış eklendi, adlı **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="8a2fb-125">Sorguda birden çok çıkış kullandığınızda, ayrı ayrı her çıktı için hello sonuçları görmek ve kolayca aralarında geçiş.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="8a2fb-126">Merhaba Sonuçlardan memnun kaldığınızda, sorgunuzu kaydedebilir, işinizi Başlat, arkanıza yaslanın ve akış analizi, hello Sihirli izleyin.</span><span class="sxs-lookup"><span data-stu-id="8a2fb-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="8a2fb-127">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="8a2fb-127">Get help</span></span>

<span data-ttu-id="8a2fb-128">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8a2fb-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a2fb-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a2fb-129">Next steps</span></span>
* [<span data-ttu-id="8a2fb-130">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="8a2fb-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8a2fb-131">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8a2fb-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8a2fb-132">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="8a2fb-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8a2fb-133">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="8a2fb-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8a2fb-134">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="8a2fb-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

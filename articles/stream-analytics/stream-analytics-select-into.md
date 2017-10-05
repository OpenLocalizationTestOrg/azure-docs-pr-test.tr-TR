---
title: "Azure Stream Analytics sorgu SELECT INTO kullanarak hata ayıklama | Microsoft Docs"
description: "Örnek veri Orta sorgu SELECT INTO deyimleri akış analizi kullanarak"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="c7933-103">Sorgular SELECT INTO deyimleri kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c7933-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="c7933-104">Gerçek zamanlı veri işleme, verileri nasıl ortasında sorgu göründüğünü bilerek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7933-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="c7933-105">Giriş veya bir Azure akış analizi işi adımlardan birden çok kez okunabilir olduğundan, ek SELECT INTO deyimleri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7933-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="c7933-106">Bunun yapılması ara veri depolama alanına çıkarır ve gibi veri doğruluğunu incelemek olanak tanır *izlemek değişkenleri* yapın, hata ayıklama bir program.</span><span class="sxs-lookup"><span data-stu-id="c7933-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="c7933-107">SELECT INTO veri akışını denetlemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c7933-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="c7933-108">Bir Azure akış analizi işi aşağıdaki örnek sorguda bir akış girişi, iki başvuru verileri girdi ve çıktı Azure tablo depolaması sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c7933-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="c7933-109">Sorgu adı ve kategori bilgilerini almak için iki başvuru BLOB'ları ve olay hub'ı verileri birleştirir:</span><span class="sxs-lookup"><span data-stu-id="c7933-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![SELECT INTO örnek sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="c7933-111">İş çalışıyor, ancak çıktıda hiçbir olay üretilen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c7933-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="c7933-112">Üzerinde **izleme** kutucuğu, burada, veriler girişi oluşturan, ancak hangi adımında tanımadığınız görebilirsiniz gösterilen **katılma** tüm olayları bırakılmasına neden oldu.</span><span class="sxs-lookup"><span data-stu-id="c7933-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![İzleme kutucuğu](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="c7933-114">Bu durumda, "Ara birleştirme sonuçlarının ve girdiden okunan verileri günlüğe kaydetmek için" birkaç ek SELECT INTO deyimleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7933-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="c7933-115">Bu örnekte, iki yeni "geçici çıkış verir." ekledik</span><span class="sxs-lookup"><span data-stu-id="c7933-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="c7933-116">Bunlar, istediğiniz herhangi bir havuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7933-116">They can be any sink you like.</span></span> <span data-ttu-id="c7933-117">Burada size Azure Storage örnek olarak kullanın:</span><span class="sxs-lookup"><span data-stu-id="c7933-117">Here we use Azure Storage as an example:</span></span>

![Ek SELECT INTO deyimleri ekleme](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="c7933-119">Ardından, sorgu şöyle yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7933-119">You can then rewrite the query like this:</span></span>

![SELECT INTO yeniden sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="c7933-121">Şimdi işi yeniden başlatın ve birkaç dakika çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="c7933-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="c7933-122">Ardından sorgu temp1 ve Visual Studio bulut aşağıdaki tablolarda üretmek için Gezgini ile temp2:</span><span class="sxs-lookup"><span data-stu-id="c7933-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="c7933-123">**temp1 tablo**
![SELECT INTO temp1 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="c7933-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="c7933-124">**temp2 tablo**
![SELECT INTO temp2 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="c7933-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="c7933-125">Gördüğünüz gibi temp1 ve temp2 veriniz varsa ve ad sütunu doğru temp2 doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7933-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="c7933-126">Ancak, hala hiçbir veri çıkışı, çünkü bir şeyler yanlış:</span><span class="sxs-lookup"><span data-stu-id="c7933-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 tablosuyla veri yok](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="c7933-128">Veri örnekleme tarafından sorunu ikinci birleşim ile neredeyse emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7933-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="c7933-129">Başvuru verileri blob üzerinden yükleyin ve bir göz atın:</span><span class="sxs-lookup"><span data-stu-id="c7933-129">You can download the reference data from the blob and take a look:</span></span>

![SELECT INTO başvuru tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="c7933-131">Gördüğünüz gibi bu başvuru verilerinde GUID biçimi biçimden farklı [sütundan] temp2.</span><span class="sxs-lookup"><span data-stu-id="c7933-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="c7933-132">İşte bu nedenle veri output1 içinde beklendiği gibi ulaşmasını alamadık.</span><span class="sxs-lookup"><span data-stu-id="c7933-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="c7933-133">Veri biçimi düzeltin, blob başvurusu ve yeniden denemek için bunu yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c7933-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![SELECT INTO geçici tablo](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="c7933-135">Bu süre, veri çıkışı biçimlendirilmiş ve beklendiği gibi doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7933-135">This time, the data in the output is formatted and populated as expected.</span></span>

![SELECT INTO son tablo](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="c7933-137">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="c7933-137">Get help</span></span>

<span data-ttu-id="c7933-138">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c7933-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7933-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7933-139">Next steps</span></span>

* [<span data-ttu-id="c7933-140">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="c7933-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c7933-141">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c7933-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c7933-142">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c7933-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c7933-143">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c7933-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c7933-144">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c7933-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


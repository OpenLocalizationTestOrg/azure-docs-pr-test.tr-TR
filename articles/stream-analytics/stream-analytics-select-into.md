---
title: Azure Stream Analytics aaaDebug sorgular SELECT INTO kullanarak | Microsoft Docs
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="75f3f-103">Sorgular SELECT INTO deyimleri kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="75f3f-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="75f3f-104">Gerçek zamanlı veri işleme, hangi hello verilerin bilerek hello Hello ortadaki sorgu yararlı olabilir görülüyor.</span><span class="sxs-lookup"><span data-stu-id="75f3f-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="75f3f-105">Giriş veya bir Azure akış analizi işi adımlardan birden çok kez okunabilir olduğundan, ek SELECT INTO deyimleri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f3f-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="75f3f-106">Bunun yapılması ara veri depolama alanına çıkarır ve gibi hello veri hello doğruluğunu incelemek olanak tanır *izlemek değişkenleri* yapın, hata ayıklama bir program.</span><span class="sxs-lookup"><span data-stu-id="75f3f-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="75f3f-107">SELECT INTO toocheck hello veri akışını kullan</span><span class="sxs-lookup"><span data-stu-id="75f3f-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="75f3f-108">Merhaba bir Azure akış analizi işi aşağıdaki örnek sorguda bir akış girişi, iki başvuru verileri girdi ve çıktı tooAzure Table Storage sahiptir.</span><span class="sxs-lookup"><span data-stu-id="75f3f-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="75f3f-109">Merhaba sorgu hello olay hub'ı ve adı ve kategori iki başvuru BLOB'lar tooget hello bilgileri verileri birleştirir:</span><span class="sxs-lookup"><span data-stu-id="75f3f-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![SELECT INTO örnek sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="75f3f-111">Merhaba işi çalışıyor, ancak hello çıktıda hiçbir olay üretilen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75f3f-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="75f3f-112">Merhaba üzerinde **izleme** hello girişi veri oluşturan, ancak Merhaba, hangi adımın tanımadığınız görebilirsiniz burada gösterilen kutucuğu **katılma** nedeniyle tüm hello bırakılan olayları toobe.</span><span class="sxs-lookup"><span data-stu-id="75f3f-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![Merhaba izleme kutucuğu](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="75f3f-114">Bu durumda, birkaç ek SELECT INTO deyimleri çok "Merhaba Ara birleştirme sonuçlarının ve hello girdiden okunan hello veri oturum" ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f3f-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="75f3f-115">Bu örnekte, iki yeni "geçici çıkış verir." ekledik</span><span class="sxs-lookup"><span data-stu-id="75f3f-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="75f3f-116">Bunlar, istediğiniz herhangi bir havuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="75f3f-116">They can be any sink you like.</span></span> <span data-ttu-id="75f3f-117">Burada size Azure Storage örnek olarak kullanın:</span><span class="sxs-lookup"><span data-stu-id="75f3f-117">Here we use Azure Storage as an example:</span></span>

![Ek SELECT INTO deyimleri ekleme](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="75f3f-119">Ardından hello sorgu şöyle yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="75f3f-119">You can then rewrite hello query like this:</span></span>

![SELECT INTO yeniden sorgu](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="75f3f-121">Şimdi hello işi yeniden başlatın ve birkaç dakika çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="75f3f-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="75f3f-122">Ardından temp1 ve temp2 tabloları izleyerek Visual Studio Cloud Explorer tooproduce hello sorgu:</span><span class="sxs-lookup"><span data-stu-id="75f3f-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="75f3f-123">**temp1 tablo**
![SELECT INTO temp1 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="75f3f-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="75f3f-124">**temp2 tablo**
![SELECT INTO temp2 tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="75f3f-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="75f3f-125">Gördüğünüz gibi temp1 ve temp2 veriniz varsa ve hello ad sütunu doğru temp2 doldurulur.</span><span class="sxs-lookup"><span data-stu-id="75f3f-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="75f3f-126">Ancak, hala hiçbir veri çıkışı, çünkü bir şeyler yanlış:</span><span class="sxs-lookup"><span data-stu-id="75f3f-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 tablosuyla veri yok](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="75f3f-128">Hello veri örnekleme tarafından hello sorunu hello ile neredeyse emin olabilirsiniz ikinci birleştirme.</span><span class="sxs-lookup"><span data-stu-id="75f3f-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="75f3f-129">Merhaba blobundan hello başvuru verileri indirin ve göz atın:</span><span class="sxs-lookup"><span data-stu-id="75f3f-129">You can download hello reference data from hello blob and take a look:</span></span>

![SELECT INTO başvuru tablosu](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="75f3f-131">Gördüğünüz gibi bu başvuru verileri hello GUID hello biçimi hello hello [sütundan] temp2 biçimlerinin farklıdır.</span><span class="sxs-lookup"><span data-stu-id="75f3f-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="75f3f-132">İşte bu nedenle hello veri beklendiği gibi output1 içinde gelmesini alamadık.</span><span class="sxs-lookup"><span data-stu-id="75f3f-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="75f3f-133">Merhaba veri biçimi düzeltin, tooreference blob karşıya yükleme ve yeniden deneyin:</span><span class="sxs-lookup"><span data-stu-id="75f3f-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![SELECT INTO geçici tablo](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="75f3f-135">Bu süre hello çıktı hello verileri biçimlendirilmiş ve beklendiği gibi doldurulur.</span><span class="sxs-lookup"><span data-stu-id="75f3f-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![SELECT INTO son tablo](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="75f3f-137">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="75f3f-137">Get help</span></span>

<span data-ttu-id="75f3f-138">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="75f3f-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75f3f-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75f3f-139">Next steps</span></span>

* [<span data-ttu-id="75f3f-140">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="75f3f-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="75f3f-141">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="75f3f-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="75f3f-142">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="75f3f-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="75f3f-143">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="75f3f-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="75f3f-144">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="75f3f-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


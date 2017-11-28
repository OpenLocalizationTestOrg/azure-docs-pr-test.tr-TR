---
title: "Stream Analytics işleri akış aaaHow toostart | Microsoft Docs"
description: "İş akışında Azure Stream Analytics çalışma şeklini | yol kesimi öğrenme."
keywords: "Akış işi"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="66d22-104">Nasıl bir akış toorun iş Azure akış analizi</span><span class="sxs-lookup"><span data-stu-id="66d22-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="66d22-105">Bir iş girişi, sorgu ve çıktı tümü hello Stream Analytics işi başlatabilirsiniz belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="66d22-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="66d22-106">toostart işinizi:</span><span class="sxs-lookup"><span data-stu-id="66d22-106">toostart your job:</span></span>

1. <span data-ttu-id="66d22-107">Merhaba iş panosundan hello Klasik Azure Portalı'nda tıklatın **Başlat** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="66d22-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Başlangıç iş düğmesi](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="66d22-109">Hello Azure portal'ı tıklatın **Başlat** hello sayfanın üst kısmındaki, iş.</span><span class="sxs-lookup"><span data-stu-id="66d22-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Azure portal başlangıç işi düğmesi](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="66d22-111">Belirtin bir **Başlat çıktı** bu işi çıkış üretmeyi başlayacağını değeri toodetermine.</span><span class="sxs-lookup"><span data-stu-id="66d22-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="66d22-112">Merhaba önceden başlatılmamış işleri için varsayılan ayar olan **iş başlangıç saati**, o hello iş başka bir deyişle, veriler işlenirken hemen başlar.</span><span class="sxs-lookup"><span data-stu-id="66d22-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="66d22-113">Ayrıca belirtebilirsiniz bir **özel** hello zaman geçmiş (için geçmiş verileri tüketme) veya hello gelecekteki (gelecekteki bir süreye kadar işleme toodelay).</span><span class="sxs-lookup"><span data-stu-id="66d22-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="66d22-114">Bir iş önceden başlatıldığında ve durdurulduğunda, durumları hello için seçenek **son durdurulma zamanı** sipariş tooresume hello hello son çıkış zamanı işten bulunur ve veri kaybını önlemek.</span><span class="sxs-lookup"><span data-stu-id="66d22-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Zaman iş akışı Başlat](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portal başlangıç akış işi zaman](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="66d22-117">Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="66d22-117">Confirm your selection.</span></span> <span data-ttu-id="66d22-118">Merhaba iş durumu çok değiştirir*başlangıç* ve kısa süre içinde çok taşınır*çalıştıran* hello işi başladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="66d22-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="66d22-119">Merhaba hello ilerlemesini izleyebilirsiniz **Başlat** hello işleminde **bildirim hub'ı**:</span><span class="sxs-lookup"><span data-stu-id="66d22-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![Akış işi ilerleme durumu](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![İşin ilerleme durumunu akış azure portalı](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="66d22-122">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="66d22-122">Get help</span></span>
<span data-ttu-id="66d22-123">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="66d22-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d22-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66d22-124">Next steps</span></span>
* [<span data-ttu-id="66d22-125">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="66d22-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="66d22-126">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="66d22-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="66d22-127">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="66d22-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="66d22-128">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="66d22-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="66d22-129">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="66d22-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


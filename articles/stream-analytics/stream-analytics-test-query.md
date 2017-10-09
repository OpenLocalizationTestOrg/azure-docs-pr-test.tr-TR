---
title: aaaAzure Stream Analytics sorgu testi | Microsoft Docs
description: "Nasıl tootest akış analizi işleri sorgularınızda."
keywords: "Sorguyu sınamak, sorgu sorun giderme"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="6eb25-104">Hello Azure portalında Azure akış analizi sorgu testi</span><span class="sxs-lookup"><span data-stu-id="6eb25-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="6eb25-105">Azure Stream Analytics'i kullanmaya toostart gerek kalmadan hello Azure portal sorguları test veya bir işi durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eb25-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="6eb25-106">Test hello giriş</span><span class="sxs-lookup"><span data-stu-id="6eb25-106">Test hello input</span></span>

1. <span data-ttu-id="6eb25-107">Örnek giriş verilerle tootest girişlerinizi hiçbirini sağ tıklayın ve ardından **dosyasından örnek verileri yükleme**.</span><span class="sxs-lookup"><span data-stu-id="6eb25-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Stream analytics sorgu Düzenleyicisi'ni test sorgusu](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="6eb25-109">Merhaba karşıya yükleme tamamlandıktan sonra tıklayın **Test** tootest hello bu sorgusu örnek sağladığınız veri.</span><span class="sxs-lookup"><span data-stu-id="6eb25-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![Stream analytics sorgu Düzenleyicisi'ni test örnek veriler](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="6eb25-111">Sorgunuzu Hello çıktısı, daha sonra kullanmak üzere toosave hello test çıkışı isterseniz hello tarayıcıda, indirme sonuçlarını bağlantıyla görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6eb25-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="6eb25-112">Artık kolayca ve yinelemeli olarak Sorgunuzu değiştirin ve tekrar tekrar hello çıkış nasıl değiştiğini toosee test.</span><span class="sxs-lookup"><span data-stu-id="6eb25-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Stream Analytics sorgu Düzenleyicisi'ni örnek çıkış](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="6eb25-114">Sorguda kullanılan birden fazla çıkış ile hem de çıkış hello sonuçları ayrı olarak görmek ve kolayca aralarında geçiş.</span><span class="sxs-lookup"><span data-stu-id="6eb25-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="6eb25-115">Sorgunuzu kaydetmek, işinizi başlatmak ve izin hello tarayıcıda gösterilen hello Sonuçlardan memnun sonra bu işlemi hata olmayan olaylar.</span><span class="sxs-lookup"><span data-stu-id="6eb25-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="6eb25-116">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="6eb25-116">Get help</span></span>

<span data-ttu-id="6eb25-117">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="6eb25-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eb25-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6eb25-118">Next steps</span></span>

* [<span data-ttu-id="6eb25-119">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="6eb25-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6eb25-120">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6eb25-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6eb25-121">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="6eb25-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6eb25-122">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="6eb25-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6eb25-123">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="6eb25-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

---
title: "Akış analizi için bir veri analizi işleme işi aaaHow toocreate | Microsoft Docs"
description: "Akış analizi için veri analizi işlem işi oluşturma | yol kesimi öğrenme."
keywords: "veri analizi işleme"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="cb4e9-104">Nasıl toocreate veri analizi işleme iş akış analizi için</span><span class="sxs-lookup"><span data-stu-id="cb4e9-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="cb4e9-105">Merhaba en üst düzey Azure akış analizi, akış analizi işi kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="cb4e9-106">Aşağıdakilerden birini oluşur veya daha fazla veri kaynakları, hello veri dönüştürme ifade bir sorgu ve sonuçları yazılan bir veya daha fazla çıkış hedefleri giriş.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="cb4e9-107">Bunlar birlikte hello kullanıcı tooperform veri analizi için veri akışı işleme senaryolarına etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="cb4e9-108">Akış analizi kullanarak toostart yeni bir akış analizi işi oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="cb4e9-109">Merhaba İş başlayana kadar bu eylem hiçbir fatura şifrelemelerini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="cb4e9-110">Çevrimiçi Hello üzerinde oturum [Klasik Azure portalı](http://manage.windowsazure.com) veya hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cb4e9-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cb4e9-111">Merhaba portalında: **Yeni'yi**, ardından **Veri Hizmetleri** veya **veri analizi** portal ve ardından bağlı olarak **Azure akış analizi** veya **akış analizi** ve ardından **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Veri analizi işleme işi Sihirbazı](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![İş işleme veri analizi oluşturma](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="cb4e9-114">Merhaba hello Stream Analytics işi için istenen yapılandırmayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="cb4e9-115">Merhaba, **iş adı** kutusunda, bir ad tooidentify hello akış analizi işi'ni girin.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="cb4e9-116">Ne zaman hello **iş adı** doğrulandı, hello iş adı kutusunda yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="cb4e9-117">Merhaba **iş adı** yalnızca alfasayısal karakterler ve hello içerebilir '-' karakteri ve 3 ile 63 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="cb4e9-118">Kullanım **bölge** hello Azure portal'ın veya **konumu** hello Azure portal toospecify hello toorun hello iş coğrafi konumu.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="cb4e9-119">Azure portal kullanarak Merhaba, seçin veya bir depolama hesabı toouse hello olarak oluşturun **bölgesel izleme depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="cb4e9-120">Bu bölgede çalıştıran tüm Stream Analytics işleri için veri izleme kullanılan toostore bu depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="cb4e9-121">Azure portal kullanarak Merhaba, yeni bir belirtin veya varolan **kaynak grubu** toohold ilgili uygulamanız için kaynakları.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="cb4e9-122">Merhaba yeni akış analizi işi seçenekleri yapılandırıldıktan sonra tıklatın **Stream Analytics işi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="cb4e9-123">Oluşturulan hello Stream Analytics işi toobe birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="cb4e9-124">toocheck hello durum hello bildirimler hub'ındaki hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Veri analizi işleme iş bildirimler hub'ı](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik işleme işi oluştur işi](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="cb4e9-127">Merhaba yeni iş durumunu gösterir **oluşturulan**.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="cb4e9-128">Bu hello fark **Başlat** düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="cb4e9-129">Merhaba işi başlatmadan önce hello iş girişi, sorgu ve çıktı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Veri analizi işleme iş durumu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik iş durumunu işleme](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="cb4e9-132">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="cb4e9-132">Get help</span></span>
<span data-ttu-id="cb4e9-133">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb4e9-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb4e9-134">Next steps</span></span>
* [<span data-ttu-id="cb4e9-135">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="cb4e9-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cb4e9-136">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cb4e9-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cb4e9-137">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cb4e9-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cb4e9-138">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="cb4e9-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cb4e9-139">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="cb4e9-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


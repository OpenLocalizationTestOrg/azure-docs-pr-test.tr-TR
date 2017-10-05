---
title: "Akış analizi için veri analizi işlem işi oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="bcf48-104">Akış analizi için veri analizi işlem işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcf48-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="bcf48-105">Üst düzey Azure akış analizi, akış analizi işi kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="bcf48-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="bcf48-106">Bir veya daha fazla giriş veri kaynağı, veri dönüştürme ifade bir sorgu ve sonuçları yazılan bir veya daha fazla çıkış hedefleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="bcf48-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="bcf48-107">Birlikte bu veri analitik veri senaryoları akış için işleme gerçekleştirmek kullanıcının etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="bcf48-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="bcf48-108">Stream Analytics kullanmaya başlamak için yeni bir akış analizi işi oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="bcf48-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="bcf48-109">İş başlatılana kadar bu eylem hiçbir fatura şifrelemelerini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bcf48-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="bcf48-110">Online'da oturum [Klasik Azure portalı](http://manage.windowsazure.com) veya [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bcf48-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bcf48-111">Portalda: **Yeni'yi**, ardından **Veri Hizmetleri** veya **veri analizi** portal ve ardından bağlı olarak **Azure akış analizi**veya **akış analizi** ve ardından **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="bcf48-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Veri analizi işleme işi Sihirbazı](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![İş işleme veri analizi oluşturma](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="bcf48-114">Stream Analytics işi için istenen yapılandırmayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="bcf48-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="bcf48-115">İçinde **iş adı** kutusuna, Stream Analytics işi tanımlamak için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="bcf48-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="bcf48-116">Zaman **iş adı** doğrulandı, iş adı kutusunda yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="bcf48-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="bcf48-117">**İş adı** yalnızca alfasayısal karakterler içerebilir ve '-' karakteri ve 3 ile 63 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bcf48-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="bcf48-118">Kullanım **bölge** Azure portalında veya **konumu** , işi çalıştırmak istediğiniz coğrafi konumu belirtmek için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="bcf48-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="bcf48-119">Azure portalını kullanıyorsanız, seçin veya olarak kullanılmak üzere depolama hesabı oluşturma **bölgesel izleme depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="bcf48-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="bcf48-120">Bu depolama hesabı, bu bölgede çalışan tüm Stream Analytics işleri izleme verilerini depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bcf48-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="bcf48-121">Azure Portalı'nı kullanarak, yeni bir belirtin veya varolan **kaynak grubu** uygulamanız için ilgili kaynakları tutmak için.</span><span class="sxs-lookup"><span data-stu-id="bcf48-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="bcf48-122">Yeni akış analizi işi seçenekleri yapılandırıldıktan sonra tıklatın **Stream Analytics işi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="bcf48-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="bcf48-123">Akış analizi işinin oluşturulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bcf48-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="bcf48-124">Durumu denetlemek için bildirim hub'ında ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcf48-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Veri analizi işleme iş bildirimler hub'ı](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik işleme işi oluştur işi](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="bcf48-127">Yeni iş durumunu gösterecektir **oluşturulan**.</span><span class="sxs-lookup"><span data-stu-id="bcf48-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="bcf48-128">Dikkat **Başlat** düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="bcf48-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="bcf48-129">İş başlamadan önce iş girişi, sorgu ve çıkış yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bcf48-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Veri analizi işleme iş durumu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal veri analitik iş durumunu işleme](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="bcf48-132">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="bcf48-132">Get help</span></span>
<span data-ttu-id="bcf48-133">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="bcf48-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcf48-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bcf48-134">Next steps</span></span>
* [<span data-ttu-id="bcf48-135">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="bcf48-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bcf48-136">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bcf48-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bcf48-137">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bcf48-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bcf48-138">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="bcf48-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bcf48-139">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="bcf48-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


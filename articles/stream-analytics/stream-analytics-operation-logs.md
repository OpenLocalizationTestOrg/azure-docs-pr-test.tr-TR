---
title: "İşlemi ile hata ayıklama ve hizmet günlüklerini akış analizi | Microsoft Docs"
description: "Nasıl kullanılır Stream Analytics işlem günlükleri"
keywords: "Hizmet Günlükleri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="8b563-104">Stream Analytics işleri hizmet ve işlem günlüklerini kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8b563-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="8b563-105">Tüm Azure hizmetlerini işletimsel günlük iletilerini için kullanıcılar için yönetim işlemleriyle ilgili kayıt ayrıntılarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8b563-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="8b563-106">Azure akış analizi, bu bilgiler hata ayıklama işi durumunu, işin ilerleme durumunu görüntüleme gibi amacıyla kullanılabilir ve gelen zaman içinde bir işin ilerleme durumunu izlemek için hata iletileri çıkış işleme için başlatın.</span><span class="sxs-lookup"><span data-stu-id="8b563-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="8b563-107">Azure Yönetim Portalı'nda işlem günlüklerini bulma</span><span class="sxs-lookup"><span data-stu-id="8b563-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="8b563-108">İşlem günlükleri iki yolla erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="8b563-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="8b563-109">Stream Analytics işi Panosu</span><span class="sxs-lookup"><span data-stu-id="8b563-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="8b563-110">Klasik Azure Portalı'nda Yönetim Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8b563-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="8b563-111">Stream Analytics işi Panosu</span><span class="sxs-lookup"><span data-stu-id="8b563-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="8b563-112">Akış analizi işi karşılık gelen günlüklerini bağlantı iş Pano sekmesinde görüntülenir. Bu bağlantıya tıklayın, onu filtreleri belirli bir iş son günlükleri gösterir şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b563-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Yönetim Hizmetleri günlükleri seçin](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="8b563-114">Yönetim Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8b563-114">Management Services</span></span>
<span data-ttu-id="8b563-115">Akış analizi ve klasik Azure portalındaki diğer hizmetler için el ile işlem günlükleri gezinmek için:</span><span class="sxs-lookup"><span data-stu-id="8b563-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="8b563-116">Tıklayın **Yönetim Hizmetleri** içinde [Klasik Azure portalında](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8b563-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8b563-117">Seçin **Stream Analytics** için **türü** ve işin adını **hizmet adı**.</span><span class="sxs-lookup"><span data-stu-id="8b563-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Akış analizi seçin](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="8b563-119">Azure portalında denetim günlüklerini bulma</span><span class="sxs-lookup"><span data-stu-id="8b563-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="8b563-120">Azure portalında Stream Analytics işiniz için işlem günlüklerini bulmak için tıklatın **Gözat** ve ardından **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="8b563-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-122">Bu, aboneliğinizin tüm kaynaklar için son 7 gün olaylarından gösteren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8b563-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="8b563-123">Tıklayarak belirt tür ya da zaman çerçevesi olayları görmek için filtreleyebilirsiniz **filtre** komutu.</span><span class="sxs-lookup"><span data-stu-id="8b563-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="8b563-125">Günlüğü ayrıntılarının alınması</span><span class="sxs-lookup"><span data-stu-id="8b563-125">Get log details</span></span>
<span data-ttu-id="8b563-126">Zaman aralığı ve işinizi günlükleri görüntülemek için durum göre filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b563-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="8b563-127">Azure Yönetim Portalı'nda tıklatın **ayrıntıları** seçili olay hakkında daha fazla ayrıntı görüntülemek için pencerenin altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8b563-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Ayrıntılarını seçin](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-129">Azure portalında bir günlük girişi içindeki ayrıntılı olayları görmek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b563-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-131">Buradan, açtığınız **ayrıntı** olayda dikey.</span><span class="sxs-lookup"><span data-stu-id="8b563-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="8b563-133">Başarısız bir işi hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8b563-133">Debug a failed job</span></span>
<span data-ttu-id="8b563-134">Azure Yönetim Portalı'nda arama simgesine ve 'başarısız oldu' türüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b563-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="8b563-135">Bu, hataları olan tüm günlükleri sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="8b563-135">This gives a result of all logs with failures.</span></span> 

  ![Başarısız bir işi hata ayıklama](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-137">Azure portalında görüntülemek için ileti düzeyine göre filtreleyebilirsiniz **kritik** olaylar.</span><span class="sxs-lookup"><span data-stu-id="8b563-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Azure portal hata ayıklama](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-139">Hataları herhangi birini seçin ve tıklayın **ayrıntıları** hata hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8b563-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="8b563-140">Bazı hata iletileri de sorunu en aza hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b563-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![İşlem ayrıntıları](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="8b563-142">İle iletişime geçmeniz durumunda [Destek](https://azure.microsoft.com/support/options/) veya takımı bilgilerini [MSDN Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), Lütfen işlem ayrıntıları özellikle dikkat **bağıntı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="8b563-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="8b563-143">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="8b563-143">Get help</span></span>
<span data-ttu-id="8b563-144">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="8b563-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b563-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b563-145">Next steps</span></span>
* [<span data-ttu-id="8b563-146">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="8b563-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8b563-147">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8b563-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8b563-148">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="8b563-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8b563-149">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="8b563-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8b563-150">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="8b563-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


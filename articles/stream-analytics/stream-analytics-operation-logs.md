---
title: "işlem ve hizmet günlükleri kullanarak Stream Analytics içinde aaaDebug | Microsoft Docs"
description: "Nasıl toouse Stream Analytics işlem günlükleri"
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
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="36282-104">Stream Analytics işleri hizmet ve işlem günlüklerini kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="36282-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="36282-105">Tüm Azure hizmetlerini tedarik işlem günlüğü iletileri toousers toorecord ayrıntıları toomanagement işlemleri ile ilgili.</span><span class="sxs-lookup"><span data-stu-id="36282-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="36282-106">Hata ayıklama gibi zamana başlangıç tooprocessing toooutput iş durumu, işin ilerleme durumunu ve hata iletileri tootrack hello işinin ilerlemesini görüntülemek amacıyla bu bilgileri Azure Stream Analytics içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36282-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="36282-107">Hello Azure Yönetim Portalı'nda işlem günlüklerini bulma</span><span class="sxs-lookup"><span data-stu-id="36282-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="36282-108">İşlem günlükleri iki yolla erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="36282-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="36282-109">Merhaba Stream Analytics işi Panosu</span><span class="sxs-lookup"><span data-stu-id="36282-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="36282-110">Yönetim Hizmetleri hello Klasik Azure portalında</span><span class="sxs-lookup"><span data-stu-id="36282-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="36282-111">Merhaba Stream Analytics işi Panosu</span><span class="sxs-lookup"><span data-stu-id="36282-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="36282-112">Akış analizi işi günlüklerini karşılık gelen bir bağlantı toohello hello işin Pano sekmesinde görüntülenir. Bu bağlantıya tıklayın, belirli bir iş son günlükleri gösterir şekilde hello filtreleri ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="36282-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Yönetim Hizmetleri günlükleri seçin](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="36282-114">Yönetim Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="36282-114">Management Services</span></span>
<span data-ttu-id="36282-115">toomanually akış analizi ve diğer hizmetleri hello Klasik Azure Portalı'nda toohello işlem günlükleri gidin:</span><span class="sxs-lookup"><span data-stu-id="36282-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="36282-116">Tıklayın **Yönetim Hizmetleri** hello içinde [Klasik Azure portalında](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="36282-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="36282-117">Seçin **Stream Analytics** için **türü** ve hello işi için hello adını **hizmet adı**.</span><span class="sxs-lookup"><span data-stu-id="36282-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Akış analizi seçin](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="36282-119">Denetim günlüklerini hello Azure portal Bul</span><span class="sxs-lookup"><span data-stu-id="36282-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="36282-120">hello Azure portal, Stream Analytics işinde için işlem günlüklerini toofind tıklatın **Gözat** ve ardından **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="36282-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-122">Bu hello olaylarından tüm kaynaklar için son 7 gün aboneliğinizde gösteren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="36282-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="36282-123">Merhaba tıklayarak toosee olayları belirtin tür ya da zaman çerçevesi filtreleyebilirsiniz **filtre** komutu.</span><span class="sxs-lookup"><span data-stu-id="36282-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Azure portal Stream Analytics seçin](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="36282-125">Günlüğü ayrıntılarının alınması</span><span class="sxs-lookup"><span data-stu-id="36282-125">Get log details</span></span>
<span data-ttu-id="36282-126">İşiniz için zaman aralığını ve durum tooview hello günlükleri göre filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36282-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="36282-127">Üzerinde hello Hello Azure Yönetim Portalı'nda tıklatın **ayrıntıları** seçili olay hakkında daha fazla ayrıntı hello penceresi tooview hello altındaki düğme.</span><span class="sxs-lookup"><span data-stu-id="36282-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Ayrıntılarını seçin](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-129">Azure portal, bir günlük girişi toosee tıklatıldığında Hello içindeki ayrıntılı olayları hello.</span><span class="sxs-lookup"><span data-stu-id="36282-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-131">Buradan, hello açabilirsiniz **ayrıntı** hello olayda dikey.</span><span class="sxs-lookup"><span data-stu-id="36282-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Azure portal ayrıntılarını seçin](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="36282-133">Başarısız bir işi hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="36282-133">Debug a failed job</span></span>
<span data-ttu-id="36282-134">Hello Azure Yönetim Portalı'nda hello arama simgesine tıklayın ve 'başarısız' yazın.</span><span class="sxs-lookup"><span data-stu-id="36282-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="36282-135">Bu, hataları olan tüm günlükleri sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="36282-135">This gives a result of all logs with failures.</span></span> 

  ![Başarısız bir işi hata ayıklama](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-137">Hello Azure portal, ileti tooview düzeyine göre filtreleyebilirsiniz **kritik** olaylar.</span><span class="sxs-lookup"><span data-stu-id="36282-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Azure portal hata ayıklama](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-139">Merhaba hataları herhangi birini seçin ve üzerinde hello tıklatın **ayrıntıları** hello hata hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="36282-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="36282-140">Bazı hata iletileri de nasıl toomitigate hello sorun hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="36282-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![İşlem ayrıntıları](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="36282-142">Toocontact gerektiğinde [Destek](https://azure.microsoft.com/support/options/) ya da bilgi toohello takım hello aracılığıyla sağlayın [MSDN Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), hello işlem ayrıntıları, lütfen unutmayın, özellikle hello **bağıntı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="36282-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="36282-143">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="36282-143">Get help</span></span>
<span data-ttu-id="36282-144">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="36282-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="36282-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36282-145">Next steps</span></span>
* [<span data-ttu-id="36282-146">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="36282-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="36282-147">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="36282-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="36282-148">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="36282-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="36282-149">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="36282-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="36282-150">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="36282-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


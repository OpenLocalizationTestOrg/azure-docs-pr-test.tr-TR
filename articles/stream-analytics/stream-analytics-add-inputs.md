---
title: "aaaAdd veri tooyour akış analizi işleri giriş | Microsoft Docs"
description: "Nasıl bir veri kaynağı tooyour Stream Analytics yukarı toohook iş Blog depolama verileri olay hub'ları veya başvuru olarak akış veri girişten öğrenin."
keywords: "veri akış girişi, veri"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="7a937-104">Akış veri girişi veya başvuru veri tooa Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="7a937-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="7a937-105">Nasıl bir veri kaynağı tooyour Stream Analytics yukarı toohook işi olay hub'ları veya başvuru verileri Blob depolama biriminden olarak akış veri girişten öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7a937-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="7a937-106">Azure Stream Analytics işleri bağlı tooone veri girişi veya daha fazla bilgi, her biri tanımlayan bir bağlantı tooan mevcut veri kaynağı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a937-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="7a937-107">Toothat veri kaynağına gönderilen veri gibi hello akış analizi işi tarafından tüketilen ve gerçek zamanlı veri akışı olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="7a937-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="7a937-108">Akış Analizi ile birinci sınıf tümleştirme sahip [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ve [Azure Blob Depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) hem içinde hem de hello işin abonelik dışında.</span><span class="sxs-lookup"><span data-stu-id="7a937-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="7a937-109">Bu makalede bir hello adımdır [Stream Analytics öğrenme yolu](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="7a937-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="7a937-110">Veri girişi: akış veri ve başvuru verileri</span><span class="sxs-lookup"><span data-stu-id="7a937-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="7a937-111">İki farklı Stream Analytics girdi vardır: veri akışlarını ve başvuru verileri.</span><span class="sxs-lookup"><span data-stu-id="7a937-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="7a937-112">**Veri akışları**: akış analizi işleri, tüketilen ve hello iş tarafından dönüştürülmüş en az bir veri akışı giriş toobe içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7a937-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="7a937-113">Azure Blob Depolama ve Azure Event Hubs veri akışı giriş kaynağı olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7a937-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="7a937-114">Azure Event Hubs kullanılan toocollect olay bağlı aygıtları, hizmetler ve uygulamalar akışlarıdır.</span><span class="sxs-lookup"><span data-stu-id="7a937-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="7a937-115">Azure Blob Depolama toplu veri akışı olarak alma için bir giriş kaynağı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a937-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="7a937-116">**Başvuru verileri**: akış analizi, ikinci bir yardımcı giriş çağrılan başvuru veri türünü destekler.</span><span class="sxs-lookup"><span data-stu-id="7a937-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="7a937-117">Hareketli karşılıklı toodata bu verileri statik veya yavaşlamasının değiştirme.</span><span class="sxs-lookup"><span data-stu-id="7a937-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="7a937-118">Genellikle, göz atmayı ve veri akışlarını toocreate daha zengin bir veri kümesi ile bağıntıları gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7a937-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="7a937-119">Azure Blob Depolama şu anda yalnızca desteklenen hello giriş başvuru verileri kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="7a937-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="7a937-120">bir giriş tooyour Stream Analytics işi tooadd:</span><span class="sxs-lookup"><span data-stu-id="7a937-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="7a937-121">Hello Azure portal'ı tıklatın **girişleri** ve ardından **bir giriş eklemek** Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="7a937-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klasik Azure portalı - bir giriş ekleyin.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="7a937-123">Hello Azure portal tıklatın hello **girişleri** döşeme Stream Analytics işinde.</span><span class="sxs-lookup"><span data-stu-id="7a937-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure portal - veri girişi ekleyin.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="7a937-125">Merhaba giriş Hello türünü belirtin: ya da **veri akışı** veya **başvuru verileri**.</span><span class="sxs-lookup"><span data-stu-id="7a937-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Merhaba doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Merhaba doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="7a937-128">Bir veri akış girişine oluşturuyorsanız, hello giriş için hello kaynak türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a937-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="7a937-129">Bu adım, yalnızca depolama birimi şu anda desteklenen Blob olarak başvuru verileri oluşturma sırasında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7a937-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="7a937-132">Bu giriş, giriş diğer adı kutusunu hello için kolay bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7a937-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="7a937-133">Bu ad, işin bir sorguyu daha sonra toorefer toohello giriş olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7a937-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="7a937-134">Merhaba gerekli bağlantı özelliklerini tooconnect tooyour veri kaynağının Hello kalan doldurun.</span><span class="sxs-lookup"><span data-stu-id="7a937-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="7a937-135">Bu alanlar giriş ve kaynak türü türüne göre değişir ve ayrıntılı olarak tanımlanan [burada](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="7a937-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Olay hub'ı veri girişi ekleme](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="7a937-137">Merhaba giriş verisi Hello serileştirme ayarları belirtin:</span><span class="sxs-lookup"><span data-stu-id="7a937-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="7a937-138">sorgularınızın beklediğiniz hello şekilde çalıştığından emin toomake belirtin hello **olayı seri hale getirme biçimi** gelen veri.</span><span class="sxs-lookup"><span data-stu-id="7a937-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="7a937-139">Desteklenen serileştirme biçimleri, JSON, CSV ve Avro olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7a937-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="7a937-140">Merhaba doğrulayın **kodlama** hello veriler için.</span><span class="sxs-lookup"><span data-stu-id="7a937-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="7a937-141">UTF-8 hello kodlama biçimi şu anda yalnızca desteklenir. ' dir.</span><span class="sxs-lookup"><span data-stu-id="7a937-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Merhaba veri girişi için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Merhaba veri girişi için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="7a937-144">Merhaba giriş oluşturmayı tamamladıktan sonra Stream Analytics toohello giriş kaynağına bağlanabildiğinizi doğrular.</span><span class="sxs-lookup"><span data-stu-id="7a937-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="7a937-145">Merhaba bildirim hub'hello bağlantıyı Test Et işlemi hello durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a937-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Giriş veri akış hello bağlantıyı sınayın](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Giriş veri akış hello bağlantıyı sınayın](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="7a937-148">Veri girişleri akış ile ilgili yardım alın</span><span class="sxs-lookup"><span data-stu-id="7a937-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="7a937-149">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="7a937-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a937-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a937-150">Next steps</span></span>
* [<span data-ttu-id="7a937-151">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="7a937-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7a937-152">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7a937-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7a937-153">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="7a937-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7a937-154">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="7a937-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7a937-155">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="7a937-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


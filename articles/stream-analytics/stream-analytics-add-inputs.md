---
title: "Akış analizi işleri için veri girişi ekleme | Microsoft Docs"
description: "Stream Analytics işiniz Blog depolama verileri olay hub'ları veya başvuru veri girişi akış olarak bir veri kaynağına bağlanacağını öğrenin."
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
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="57bbf-104">Stream Analytics işe akış veri girişi veya başvuru veri ekleme</span><span class="sxs-lookup"><span data-stu-id="57bbf-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="57bbf-105">Olay hub'ları veya başvuru verileri Blob depolama biriminden veri girişten akış olarak Stream Analytics işiniz için bir veri kaynağı bağlanacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="57bbf-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="57bbf-106">Azure akış analizi işleri, bir veri girişi veya varolan bir veri kaynağına her biri tanımlayan bir bağlantı daha fazla bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="57bbf-107">Bu veri kaynağına gönderilen veri gibi akış analizi işi tarafından tüketilen ve gerçek zamanlı veri akışı olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="57bbf-108">Akış Analizi ile birinci sınıf tümleştirme sahip [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ve [Azure Blob Depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) hem içinde hem de iş abonelik dışında.</span><span class="sxs-lookup"><span data-stu-id="57bbf-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="57bbf-109">Bu makalede bir adımdır [Stream Analytics öğrenme yolu](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="57bbf-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="57bbf-110">Veri girişi: akış veri ve başvuru verileri</span><span class="sxs-lookup"><span data-stu-id="57bbf-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="57bbf-111">İki farklı Stream Analytics girdi vardır: veri akışlarını ve başvuru verileri.</span><span class="sxs-lookup"><span data-stu-id="57bbf-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="57bbf-112">**Veri akışları**: akış analizi işleri, en az bir veri akış girişine tüketilen ve iş tarafından dönüştürülmüş içermelidir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="57bbf-113">Azure Blob Depolama ve Azure Event Hubs veri akışı giriş kaynağı olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="57bbf-114">Azure Event Hubs bağlı aygıtları, hizmetler ve uygulamalar olay akışları toplayacak şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57bbf-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="57bbf-115">Azure Blob Depolama toplu veri akışı olarak alma için bir giriş kaynağı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="57bbf-116">**Başvuru verileri**: akış analizi, ikinci bir yardımcı giriş çağrılan başvuru veri türünü destekler.</span><span class="sxs-lookup"><span data-stu-id="57bbf-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="57bbf-117">Hareket halindeki verileriniz aksine, bu verileri statik veya yavaşlamasının değiştirme.</span><span class="sxs-lookup"><span data-stu-id="57bbf-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="57bbf-118">Bu genellikle göz atmayı ve veri akışları ile bağıntıları gerçekleştirmek için daha zengin bir veri kümesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57bbf-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="57bbf-119">Azure Blob Depolama şu anda yalnızca desteklenen giriş başvuru verileri kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="57bbf-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="57bbf-120">Stream Analytics işiniz için bir giriş eklemek için:</span><span class="sxs-lookup"><span data-stu-id="57bbf-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="57bbf-121">Azure portal'ı tıklayın **girişleri** ve ardından **bir giriş eklemek** Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="57bbf-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klasik Azure portalı - bir giriş ekleyin.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="57bbf-123">Azure portal'ı tıklayın **girişleri** döşeme Stream Analytics işinde.</span><span class="sxs-lookup"><span data-stu-id="57bbf-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure portal - veri girişi ekleyin.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="57bbf-125">Giriş türünü belirtin: ya da **veri akışı** veya **başvuru verileri**.</span><span class="sxs-lookup"><span data-stu-id="57bbf-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="57bbf-128">Bir veri akış girişine oluşturuyorsanız, giriş için kaynak türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="57bbf-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="57bbf-129">Bu adım, yalnızca depolama birimi şu anda desteklenen Blob olarak başvuru verileri oluşturma sırasında atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="57bbf-132">Giriş diğer adı kutusuna bu girişi için kolay bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="57bbf-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="57bbf-133">Bu ad, işin sorguyu daha sonra giriş başvurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57bbf-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="57bbf-134">Veri kaynağına bağlanmak için gereken bağlantı özelliklerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="57bbf-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="57bbf-135">Bu alanlar giriş ve kaynak türü türüne göre değişir ve ayrıntılı olarak tanımlanan [burada](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="57bbf-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Olay hub'ı veri girişi ekleme](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="57bbf-137">Giriş verilerini seri hale getirme ayarlarını belirtin:</span><span class="sxs-lookup"><span data-stu-id="57bbf-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="57bbf-138">Sorgularınızın beklediğiniz gibi çalıştığından emin olmak için belirtmek **olayı seri hale getirme biçimi** gelen veri.</span><span class="sxs-lookup"><span data-stu-id="57bbf-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="57bbf-139">Desteklenen serileştirme biçimleri, JSON, CSV ve Avro olacaktır.</span><span class="sxs-lookup"><span data-stu-id="57bbf-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="57bbf-140">Doğrulama **kodlama** veriler için.</span><span class="sxs-lookup"><span data-stu-id="57bbf-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="57bbf-141">Şu anda desteklenen tek kodlama biçimi UTF-8'dir.</span><span class="sxs-lookup"><span data-stu-id="57bbf-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Giriş verileri için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Giriş verileri için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="57bbf-144">Giriş oluşturmayı tamamladıktan sonra Stream Analytics giriş kaynağına bağlanabildiğinizi doğrular.</span><span class="sxs-lookup"><span data-stu-id="57bbf-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="57bbf-145">Bildirim hub'ı Bağlantıyı Sına işlemin durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57bbf-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Giriş akış verilerini bağlantıyı sınayın](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Giriş akış verilerini bağlantıyı sınayın](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="57bbf-148">Veri girişleri akış ile ilgili yardım alın</span><span class="sxs-lookup"><span data-stu-id="57bbf-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="57bbf-149">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="57bbf-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="57bbf-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57bbf-150">Next steps</span></span>
* [<span data-ttu-id="57bbf-151">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="57bbf-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="57bbf-152">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="57bbf-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="57bbf-153">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="57bbf-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="57bbf-154">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="57bbf-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="57bbf-155">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="57bbf-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


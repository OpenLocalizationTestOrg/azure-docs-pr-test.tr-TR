---
title: "aaaHow tooconfigure verilerin çıktısını alır, Stream Analytics işleri | Microsoft Docs"
description: "Çıkış akış analizi işleri için yapılandırma | yol kesimi öğrenme."
keywords: "Çıkış, verileri veri taşıma"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="51905-104">Nasıl Stream Analytics işleri tooconfigure verilerin çıktısını alır</span><span class="sxs-lookup"><span data-stu-id="51905-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="51905-105">Azure Stream Analytics işleri bağlı tooone veya bağlantı tooan mevcut veri havuzunu tanımlamak daha fazla veri çıkışlarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="51905-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="51905-106">Stream Analytics işiniz işler ve gelen verileri dönüştüren gibi veri çıkış olayları akışı tooyour iş çıktısı yazılır.</span><span class="sxs-lookup"><span data-stu-id="51905-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="51905-107">Stream Analytics veri çıkışları kullanılan toosource gerçek zamanlı panolar veya uyarıları, tetikleyici veri taşıma iş akışları veya toplu iş daha sonra işlemek için yalnızca arşiv verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="51905-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="51905-108">Akış analizi birinci sınıf burada ayrıntılı şekilde belgelenen birkaç Azure hizmetleriyle tümleştirme vardır.</span><span class="sxs-lookup"><span data-stu-id="51905-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="51905-109">bir çıkış tooyour Stream Analytics işi tooadd:</span><span class="sxs-lookup"><span data-stu-id="51905-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="51905-110">Merhaba, [Azure portal](https://portal.azure.com), işinizi açın ve'ı tıklatın **çıkışları** ve ardından **Ekle** görünür hello çıkışları dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="51905-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Çıkış ekleme](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="51905-112">Hello bu çıkış için bir kolay ad **çıkış diğer adları** kutusu.</span><span class="sxs-lookup"><span data-stu-id="51905-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="51905-113">Bu ad, işin bir sorguyu daha sonra toorefer toohello çıkış kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51905-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="51905-114">Gerekli hello bağlantı özelliklerini tooconnect tooyour Çıktı Hello kalan doldurun.</span><span class="sxs-lookup"><span data-stu-id="51905-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="51905-115">Bu alanlar çıktı türüne göre değişir ve burada ayrıntılı olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="51905-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Veri taşıma türü seçin](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="51905-117">Merhaba çıktı türüne bağlı olarak nasıl hello veri seri hale getirilmiş biçimlendirilmiş veya toospecify gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="51905-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="51905-118">Her çıktı türü için Hello belirli serileştirme ayarlarını aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51905-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="51905-119">Merhaba gerekli bağlantı özelliklerini tooconnect tooyour veri kaynağının Hello kalan doldurun.</span><span class="sxs-lookup"><span data-stu-id="51905-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="51905-120">Bu alanlar giriş ve kaynak türü türüne göre değişir ve ayrıntılı hello olarak tanımlanan [işi oluştur makale](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="51905-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="51905-121">Tüm çıktı öğesi eklenen toohello işleri hello iş başlatıldı ve akan olayları başlatmak için önce bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51905-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="51905-122">Blob Depolama çıkış olarak kullanırsanız, örneğin, hello iş bir depolama hesabı otomatik olarak oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="51905-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="51905-123">Merhaba ASA işi başlatılmadan önce hello kullanıcı tarafından oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="51905-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="51905-124">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="51905-124">Get help</span></span>
<span data-ttu-id="51905-125">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="51905-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="51905-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51905-126">Next steps</span></span>
* [<span data-ttu-id="51905-127">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="51905-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="51905-128">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="51905-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="51905-129">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="51905-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="51905-130">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="51905-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="51905-131">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="51905-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


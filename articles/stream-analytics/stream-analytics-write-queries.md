---
title: Stream Analytics aaaHow toowrite sorgularda | Microsoft Docs
description: "Akış analizi ve sorgu veri sorguları yazma | yol kesimi öğrenme."
keywords: "nasıl toowrite sorgular, sorgu veri sorguları yazma, bir sorgu yazın"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="c358c-104">Toowrite Stream Analytics içinde nasıl sorgular</span><span class="sxs-lookup"><span data-stu-id="c358c-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="c358c-105">Akış işleme mantığı Azure akış analizi de sorgu yazma "bir iş başlatılır ve hello iş ulaştığında gibi verileri yürütülen önce tanımlı bir durumu sorgu" olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c358c-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="c358c-106">Merhaba veri dönüştürme SQL benzeri bir sorgu dili ifade eklenen dil uzantıları gibi büyük ölçüde T-SQL bir alt bazı olduğu [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress zamana bağlı semantiği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c358c-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="c358c-107">Sorgu yazma:</span><span class="sxs-lookup"><span data-stu-id="c358c-107">Writing Queries:</span></span>
1. <span data-ttu-id="c358c-108">Hello Azure Yönetim Portalı'da, Stream Analytics işinde tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="c358c-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Seçme sorgusu](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="c358c-110">Hello Azure Portal'ı tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="c358c-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Sorgu Önizleme'yi seçin](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="c358c-112">Yeni işlerin başlamanıza yardımcı bir sorgu şablonu toohelp vardır.</span><span class="sxs-lookup"><span data-stu-id="c358c-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="c358c-113">"geçiş" şablonu gerçekleştirir hello sorgu bu projeleri giriş olaylarını tüm alanları hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="c358c-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="c358c-114">İşiniz için en az bir giriş ve çıkış tanımladıysanız, giriş ve çıkış önce kullanmak istediğiniz hello hello diğer adları ile Merhaba yer tutucu "[YourOutputAlias]" ve "[YourInputAlias]" alanları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358c-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="c358c-115">Ayrıca, hala yazar ve sorgunuzu hello Klasik Azure portalı girişleri ve çıkışları hello işinde tanımlamadan test kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358c-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="c358c-116">Daha fazla işlem daha basit bir geçiş diski tooperform isterseniz hello sorgu tanımı düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358c-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="c358c-117">Sorgu yazma ile başlatılan tooget ele desenleri yakalanır bazı yaygın sorgusu göz [burada](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="c358c-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Sorgu veri penceresi](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="c358c-119">toovalidate sorgu verileri çalışma:</span><span class="sxs-lookup"><span data-stu-id="c358c-119">toovalidate query data is working:</span></span>
<span data-ttu-id="c358c-120">Sorgunuzu hello tarayıcıda test verileri içeren bir veya daha fazla yerel JSON dosyaları çalıştırarak beklendiği gibi davranır test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358c-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="c358c-121">Bu hello iş başlatmaz veya herhangi fatura ödenmesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c358c-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="c358c-122">Şu anda tarayıcı içi sorgu testi hello Azure Portal desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c358c-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="c358c-123">(Aksi halde hello Test düğmesi devre dışı bırakılır) hello sorguda herhangi bir hata olduğundan emin olun ve ardından hello Test düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c358c-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Test verileri Sorgulama](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="c358c-125">İstendiğinde toospecify dosyaları her hello sorguda başvurulan hello girdi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c358c-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="c358c-126">Bu örnekte, hello şablon sorgu olarak kaldığını-hello iletişim "yourinputalias" adlı bir giriş istemeden, olduğundan.</span><span class="sxs-lookup"><span data-stu-id="c358c-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Test verileri sorgusu](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="c358c-128">Tooa test dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="c358c-128">Browse tooa test file.</span></span> <span data-ttu-id="c358c-129">Birkaç örnek dosyalarını kullanılabilir [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ve kendi veri akışı girişlerini hello hello Giriş sekmesinde örnek verileri işlevi aracılığıyla gelen örnek veri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c358c-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Sorgu giriş](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="c358c-131">Merhaba iletişim kapattıktan sonra sorgunuzu hello test verileri çalışır ve hello sorgu sayfanın hello sonundaki hello sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c358c-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Sorgu özeti](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="c358c-133">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="c358c-133">Get help</span></span>
<span data-ttu-id="c358c-134">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="c358c-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c358c-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c358c-135">Next steps</span></span>
* [<span data-ttu-id="c358c-136">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="c358c-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c358c-137">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c358c-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c358c-138">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c358c-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c358c-139">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c358c-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c358c-140">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c358c-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


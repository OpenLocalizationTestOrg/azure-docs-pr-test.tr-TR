---
title: "aaaImport, veri tooAnalytics Azure Application ınsights'ta | Microsoft Docs"
description: "Statik veri toojoin uygulama telemetri ile içeri aktarma veya ayrı veri akışı tooquery Analytics ile içeri aktarın."
services: application-insights
keywords: "Şema, veri alma açın"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="04fcc-104">İçeri aktarma veri analizi</span><span class="sxs-lookup"><span data-stu-id="04fcc-104">Import data into Analytics</span></span>

<span data-ttu-id="04fcc-105">Hiç tablo verisi içine aktarmak [Analytics](app-insights-analytics.md), ya da toojoin ile [Application Insights](app-insights-overview.md) , uygulamanızdan alınan telemetri veya böylece ayrı bir akış olarak çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="04fcc-106">Analytics telemetri bir güçlü sorgu dili oldukça uygun tooanalyzing yüksek hacimli zaman damgalı Akışları ' dir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="04fcc-107">Veri kendi Şeması'nı kullanarak Analytics aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="04fcc-108">Toouse hello istek veya izleme gibi standart Application Insights şemalar sahip değil.</span><span class="sxs-lookup"><span data-stu-id="04fcc-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="04fcc-109">JSON veya DSV (sınırlayıcı virgülle ayrılmış değerler - virgül, noktalı virgül veya sekme) içe aktarabilirsiniz dosyaları.</span><span class="sxs-lookup"><span data-stu-id="04fcc-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="04fcc-110">TooAnalytics alma yararlı olduğu üç durumlar vardır:</span><span class="sxs-lookup"><span data-stu-id="04fcc-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="04fcc-111">**Uygulama telemetriyle katılın.**</span><span class="sxs-lookup"><span data-stu-id="04fcc-111">**Join with app telemetry.**</span></span> <span data-ttu-id="04fcc-112">Örneğin, gelen Web sitesi toomore okunabilir sayfa başlıklarını URL'leri eşleyen bir tablo içe aktarılamadı.</span><span class="sxs-lookup"><span data-stu-id="04fcc-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="04fcc-113">Analizleri, on en popüler sayfa, Web sitenizdeki hello gösteren bir Pano grafiği raporunu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="04fcc-114">Şimdi, sayfa başlıklarını hello URL'leri yerine hello gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="04fcc-115">**Uygulama telemetrinin bağıntısını** ağ trafiğini gibi diğer kaynaklar ile sunucu verilerini ya da CDN günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="04fcc-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="04fcc-116">**Analytics tooa ayrı veri akışı uygulayın.**</span><span class="sxs-lookup"><span data-stu-id="04fcc-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="04fcc-117">Uygulama Öngörüler Analytics seyrek, zaman damgalı akışları - SQL birçok durumda daha iyi ile iyi çalışan bir güçlü aracıdır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="04fcc-118">Bu tür bir akış başka bir kaynak sunucudan varsa Analytics ile analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="04fcc-119">Gönderen veri tooyour veri kaynağı kolaydır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="04fcc-120">(Bir saat) Verilerinizi 'veri kaynağında' Hello şeması tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="04fcc-121">(Düzenli aralıklarla) Veri tooAzure depolama alanınızı karşıya yükleme ve hello REST API toonotify yeni veri alımı için bekliyor bizi arayın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="04fcc-122">Birkaç dakika içinde hello veri analizi sorgu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="04fcc-123">Merhaba hello karşıya yükleme sıklığını sizin tarafınızdan tanımlanır ve sorgular için kullanılabilir, veri toobe ne kadar hızlı istersiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="04fcc-124">Daha verimli tooupload veri daha büyük öbek, ancak 1 GB'den büyük var.</span><span class="sxs-lookup"><span data-stu-id="04fcc-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="04fcc-125">*Çok sayıda veri kaynakları tooanalyze var mı?*</span><span class="sxs-lookup"><span data-stu-id="04fcc-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="04fcc-126">*Kullanmayı* logstash *tooship Application Insights verilerinizi.*</span><span class="sxs-lookup"><span data-stu-id="04fcc-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="04fcc-127">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="04fcc-127">Before you start</span></span>

<span data-ttu-id="04fcc-128">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="04fcc-128">You need:</span></span>

1. <span data-ttu-id="04fcc-129">Microsoft Azure Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="04fcc-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="04fcc-130">Verilerinizden ayrı olarak diğer telemetri tooanalyze istiyorsanız [yeni bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="04fcc-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="04fcc-131">Birleştirme ya da Application Insights ile zaten ayarlanmış bir uygulamadan telemetri verilerinizle karşılaştırma, bu uygulama için hello kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="04fcc-132">Katkıda bulunan veya sahibi erişim toothat kaynak.</span><span class="sxs-lookup"><span data-stu-id="04fcc-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="04fcc-133">Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="04fcc-133">Azure storage.</span></span> <span data-ttu-id="04fcc-134">TooAzure depolama yükleme ve analiz verilerinizi buradan alır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="04fcc-135">Bloblarınızın için ayrılmış depolama hesabı oluşturma öneririz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="04fcc-136">Diğer işlemlerle bloblarınızın paylaştırılmışsa bloblarınızın bizim işlemleri tooread için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="04fcc-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="04fcc-137">Şemanızı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="04fcc-137">Define your schema</span></span>

<span data-ttu-id="04fcc-138">Veri almadan önce tanımlamalısınız bir *veri kaynağı* hello şema verilerinizin belirtir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="04fcc-139">Tek bir Application Insights kaynağı too50 veri kaynaklarına sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="04fcc-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="04fcc-140">Merhaba veri kaynağı Sihirbazı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-140">Start hello data source wizard.</span></span> <span data-ttu-id="04fcc-141">"Yeni veri kaynağı Ekle" düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-141">Use "Add new data source" button.</span></span> <span data-ttu-id="04fcc-142">Alternatif olarak - sağ üst köşedeki ayarlar düğmesine tıklayın ve açılan menüde "Veri kaynakları" seçin.</span><span class="sxs-lookup"><span data-stu-id="04fcc-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Yeni veri kaynağı ekleme](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="04fcc-144">Yeni veri kaynağı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="04fcc-145">Karşıya yükleyecek hello dosyalarının biçimi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="04fcc-146">Merhaba biçimi manuel olarak tanımlamak veya bir örnek dosya karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="04fcc-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="04fcc-147">CSV biçiminde Hello veri olması durumunda hello örnek hello ilk satırında sütun üst bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="04fcc-148">Merhaba sonraki adımda hello alan adlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="04fcc-149">Merhaba örnek en az 10 satır veya veri kayıtlarının içermelidir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="04fcc-150">Sütun veya alan adı alfasayısal adlarını (olmadan, boşluk veya noktalama) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Örnek dosya karşıya yükleme](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="04fcc-152">Sihirbaz hello gözden geçirme hello şema aldım.</span><span class="sxs-lookup"><span data-stu-id="04fcc-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="04fcc-153">Bir örnek hello türlerinden çıkarımı yapılan tooadjust çıkarımı yapılan hello hello sütun türlerini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Gözden geçirme çıkarımı yapılan hello şeması](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="04fcc-155">(İsteğe bağlı.) Bir şema tanımı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="04fcc-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="04fcc-156">Aşağıdaki Hello biçimini bakın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-156">See hello format below.</span></span>

 * <span data-ttu-id="04fcc-157">Bir zaman damgası seçin.</span><span class="sxs-lookup"><span data-stu-id="04fcc-157">Select a Timestamp.</span></span> <span data-ttu-id="04fcc-158">Tüm veriler Analytics, zaman damgası alanı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="04fcc-159">Türü olmalıdır `datetime`, ancak 'timestamp' adlı toobe sahip değil.</span><span class="sxs-lookup"><span data-stu-id="04fcc-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="04fcc-160">Verilerinizi bir tarih ve saati ISO biçiminde içeren bir sütun varsa, bu hello zaman damgası sütunu olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="04fcc-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="04fcc-161">Aksi takdirde, "veri olarak gelen" seçin ve hello içeri aktarma işlemi zaman damgası alanı ekler.</span><span class="sxs-lookup"><span data-stu-id="04fcc-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="04fcc-162">Merhaba veri kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04fcc-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="04fcc-163">Şema tanımlama dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="04fcc-163">Schema definition file format</span></span>

<span data-ttu-id="04fcc-164">UI Hello şemada düzenlemek yerine, bir dosyadan hello şema tanımı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="04fcc-165">Merhaba şema tanım biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="04fcc-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="04fcc-166">Sınırlandırılmış biçimi</span><span class="sxs-lookup"><span data-stu-id="04fcc-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="04fcc-167">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="04fcc-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="04fcc-168">Her sütunun hello konumu, adı ve türü ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="04fcc-169">Konum – ayrılmış dosya biçimlendirmek için eşlenen hello değerin hello konumu değil.</span><span class="sxs-lookup"><span data-stu-id="04fcc-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="04fcc-170">JSON için onu hello jpath eşlenen hello anahtarının biçimidir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="04fcc-171">Adı – hello hello sütunun adı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="04fcc-172">Türü – bu sütunun veri türünü hello.</span><span class="sxs-lookup"><span data-stu-id="04fcc-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="04fcc-173">Örnek verileri kullanıldı ve dosya biçimi ayrılmış durumda hello şema tanımı tüm sütunları eşleme ve yeni sütunlar hello sonunda eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="04fcc-174">JSON hello veri kısmi bir eşleme sağlar, bu nedenle hello JSON biçimine şema tanımı toomap örnek verilerde bulunan her anahtar yok.</span><span class="sxs-lookup"><span data-stu-id="04fcc-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="04fcc-175">Bunu ayrıca hello örnek veri parçası olmayan sütunları eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="04fcc-176">Veri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="04fcc-176">Import data</span></span>

<span data-ttu-id="04fcc-177">tooimport veri tooAzure depolama yükleme, bir erişim anahtarı oluşturun ve ardından bir REST API çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Yeni veri kaynağı ekleme](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="04fcc-179">İşlemi el ile aşağıdaki hello gerçekleştirmek veya Otomatik Sistem toodo düzenli aralıklarla ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="04fcc-180">Tooimport istediğiniz her veri bloğu için şu adımları toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="04fcc-181">Merhaba verileri çok karşıya[Azure blob depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="04fcc-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="04fcc-182">BLOB'ları sıkıştırılmamış too1GB yukarı herhangi bir boyutta olabilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="04fcc-183">Yüzlerce MB büyük BLOB'lar performans açısından idealdir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="04fcc-184">Gzip tooimprove karşıya yükleme zamanı ve hello veri toobe sorgu için kullanılabilecek için gecikme süresine sahip sıkıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04fcc-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="04fcc-185">Kullanım hello `.gz` dosya adı uzantısı.</span><span class="sxs-lookup"><span data-stu-id="04fcc-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="04fcc-186">Bu amaçla tooavoid çağrıları performans yavaşlamasının farklı hizmetlerden en iyi toouse ayrı bir depolama hesabı içindir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="04fcc-187">Yüksek yoğunlukta veri gönderirken, her birkaç saniyede bir depolama hesabı, performans nedenleriyle birden çok toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="04fcc-188">[Merhaba blob için bir paylaşılan erişim imzası anahtar oluşturma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="04fcc-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="04fcc-189">Hello anahtarı bir sona erme süresi bir gün ve okuma erişimi sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="04fcc-190">Bir REST çağrısı toonotify veri bekleyen Application Insights olun.</span><span class="sxs-lookup"><span data-stu-id="04fcc-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="04fcc-191">Uç noktası:`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="04fcc-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="04fcc-192">HTTP yöntemini: POST</span><span class="sxs-lookup"><span data-stu-id="04fcc-192">HTTP method: POST</span></span>
 * <span data-ttu-id="04fcc-193">Yük:</span><span class="sxs-lookup"><span data-stu-id="04fcc-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="04fcc-194">Merhaba yer tutucuları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="04fcc-194">hello placeholders are:</span></span>

* <span data-ttu-id="04fcc-195">`Blob URI with Shared Access Key`:, İşlem bu bir anahtar oluşturmak için hello yordamdan alırsınız.</span><span class="sxs-lookup"><span data-stu-id="04fcc-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="04fcc-196">Belirli toohello blob var.</span><span class="sxs-lookup"><span data-stu-id="04fcc-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="04fcc-197">`Schema ID`: Merhaba, tanımlı bir şeması için oluşturulan şema kimliği.</span><span class="sxs-lookup"><span data-stu-id="04fcc-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="04fcc-198">Bu blob Hello verilerde toohello şema uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="04fcc-199">`DateTime`: hangi hello isteği gönderildi, başlangıç zamanı UTC.</span><span class="sxs-lookup"><span data-stu-id="04fcc-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="04fcc-200">Biz bu biçimlerini kabul: ISO8601 (gibi "2016-01-01 13:45:01"); Rfc822 ("Çar, 14 Ara 16 14:57:01 + 0000"); RFC850 ("Çarşamba, 14 Ara 16 14:57:00 UTC"); RFC1123 ("Çar, 14 Ara 2016 14:57:00 + 0000").</span><span class="sxs-lookup"><span data-stu-id="04fcc-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="04fcc-201">`Instrumentation key`Application Insights kaynağınıza.</span><span class="sxs-lookup"><span data-stu-id="04fcc-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="04fcc-202">Merhaba veri analizleri birkaç dakika sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="04fcc-203">Hata yanıtları</span><span class="sxs-lookup"><span data-stu-id="04fcc-203">Error responses</span></span>

* <span data-ttu-id="04fcc-204">**400 Hatalı istek**: Bu hello isteği yükü geçersiz gösterir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="04fcc-205">Denetleme:</span><span class="sxs-lookup"><span data-stu-id="04fcc-205">Check:</span></span>
 * <span data-ttu-id="04fcc-206">Doğru izleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="04fcc-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="04fcc-207">Geçerli saat değeri.</span><span class="sxs-lookup"><span data-stu-id="04fcc-207">Valid time value.</span></span> <span data-ttu-id="04fcc-208">Başlangıç zamanı, UTC şimdi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04fcc-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="04fcc-209">JSON hello olayın toohello şema uyumludur.</span><span class="sxs-lookup"><span data-stu-id="04fcc-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="04fcc-210">**403 Yasak**: hello blob gönderilen erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="04fcc-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="04fcc-211">Bu hello paylaşılan erişim anahtarı geçerli değil ve süresi geçmemiş emin olun.</span><span class="sxs-lookup"><span data-stu-id="04fcc-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="04fcc-212">**404 Bulunamadı**:</span><span class="sxs-lookup"><span data-stu-id="04fcc-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="04fcc-213">Merhaba blob yok.</span><span class="sxs-lookup"><span data-stu-id="04fcc-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="04fcc-214">Merhaba SourceId yanlış olur.</span><span class="sxs-lookup"><span data-stu-id="04fcc-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="04fcc-215">Daha ayrıntılı bilgi hello yanıt hata iletisinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="04fcc-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="04fcc-216">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="04fcc-216">Sample code</span></span>

<span data-ttu-id="04fcc-217">Bu kodu hello kullanır [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="04fcc-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="04fcc-218">Sınıfları</span><span class="sxs-lookup"><span data-stu-id="04fcc-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="04fcc-219">Veriyi çekme</span><span class="sxs-lookup"><span data-stu-id="04fcc-219">Ingest data</span></span>

<span data-ttu-id="04fcc-220">Bu kodu her bir blob için kullanın.</span><span class="sxs-lookup"><span data-stu-id="04fcc-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="04fcc-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04fcc-221">Next steps</span></span>

* [<span data-ttu-id="04fcc-222">Merhaba günlük analizi sorgu dili turu</span><span class="sxs-lookup"><span data-stu-id="04fcc-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="04fcc-223">Kullanım *Logstash* toosend veri tooApplication Öngörüler</span><span class="sxs-lookup"><span data-stu-id="04fcc-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)

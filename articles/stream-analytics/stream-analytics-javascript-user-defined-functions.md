---
title: "Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler | Microsoft Docs"
description: "JavaScript kullanıcı tanımlı işlevler ile Gelişmiş sorgu mekanizması gerçekleştirmek"
keywords: "JavaScript, kullanıcı tanımlı işlevler, udf"
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
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="83d0d-104">Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="83d0d-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="83d0d-105">Azure akış analizi, kullanıcı tanımlı işlevler JavaScript'te yazılmış destekler.</span><span class="sxs-lookup"><span data-stu-id="83d0d-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="83d0d-106">İle zengin kümesi **dize**, **RegExp**, **matematik**, **dizi**, ve **tarih** yöntemleri, JavaScript sağlar, karmaşık veri dönüşümleri ile Stream Analytics işleri oluşturmak daha kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="83d0d-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="83d0d-107">JavaScript kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="83d0d-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="83d0d-108">JavaScript kullanıcı tanımlı işlevler harici bağlantı gerektirmeyen durum bilgisiz, yalnızca işlem skaler işlevler destekler.</span><span class="sxs-lookup"><span data-stu-id="83d0d-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="83d0d-109">Bir işlevin dönüş değeri yalnızca skaler (tek) bir değer olabilir.</span><span class="sxs-lookup"><span data-stu-id="83d0d-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="83d0d-110">Kullanıcı tanımlı bir JavaScript işlevi işe ekledikten sonra işlevi herhangi bir yere sorgusunda yerleşik bir skaler işlev gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d0d-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="83d0d-111">Burada JavaScript kullanıcı tanımlı işlevler kullanışlı bulabileceğiniz bazı senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="83d0d-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="83d0d-112">Ayrıştırma ve normal ifade İşlevler, örneğin, sahip dizeleri düzenleme **Regexp_Replace()** ve **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="83d0d-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="83d0d-113">Kod çözme ve kodlama verileri, örneğin, ikili onaltılık dönüştürme</span><span class="sxs-lookup"><span data-stu-id="83d0d-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="83d0d-114">JavaScript ile mathematic hesaplamalar gerçekleştirmek **matematik** işlevleri</span><span class="sxs-lookup"><span data-stu-id="83d0d-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="83d0d-115">Sıralama, birleştirme, bulma ve dolgu gibi dizi işlemlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="83d0d-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="83d0d-116">Stream Analytics içinde JavaScript kullanıcı tanımlı işlev ile yapamayacağınız bazı noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="83d0d-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="83d0d-117">Duyurmak gerçekleştirme dış REST uç noktalar, örneğin, bir dış kaynaktan IP arama veya başvuru veri çekilmesini ters</span><span class="sxs-lookup"><span data-stu-id="83d0d-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="83d0d-118">Özel olay biçimi serileştirme gerçekleştirmek veya giriş/çıkış üzerinde seri durumundan çıkarma</span><span class="sxs-lookup"><span data-stu-id="83d0d-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="83d0d-119">Özel toplamaları oluşturun</span><span class="sxs-lookup"><span data-stu-id="83d0d-119">Create custom aggregates</span></span>

<span data-ttu-id="83d0d-120">Gibi çalışır ancak **Date.GetDate()** veya **Math.random()** engellenmediğinden işlevleri tanımı'nda, bunları yapmaktan kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="83d0d-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="83d0d-121">Bu işlevler **sağlamadığı** bunları arayın ve Azure akış analizi hizmetine işlev çağrılarını günlüğün korumaz her zaman aynı sonucu dönün ve sonuç döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="83d0d-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="83d0d-122">Bir işlev, farklı sonuç aynı olaylarına döndürürse, sizin tarafınızdan veya akış analizi hizmeti tarafından bir iş yeniden başlatıldığında Yinelenebilirlik garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="83d0d-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="83d0d-123">Azure portalında kullanıcı tanımlı bir JavaScript işlevi ekleme</span><span class="sxs-lookup"><span data-stu-id="83d0d-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="83d0d-124">Basit JavaScript kullanıcı tanımlı bir işlev altında varolan bir Stream Analytics işi oluşturmak için bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="83d0d-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="83d0d-125">Azure portalında, Stream Analytics işi bulun.</span><span class="sxs-lookup"><span data-stu-id="83d0d-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="83d0d-126">Altında **iş TOPOLOJİ**, işlevinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="83d0d-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="83d0d-127">İşlevler boş bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="83d0d-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="83d0d-128">Yeni bir kullanıcı tanımlı işlev oluşturmak için seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="83d0d-129">Üzerinde **yeni işlev** dikey penceresinde için **işlev türü**seçin **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="83d0d-130">Varsayılan işlev şablonu Düzenleyicisi'nde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="83d0d-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="83d0d-131">İçin **UDF diğer**, girin **hex2Int**ve işlev uygulama aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="83d0d-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="83d0d-132">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="83d0d-132">Select **Save**.</span></span> <span data-ttu-id="83d0d-133">İşlevinizi işlevleri listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="83d0d-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="83d0d-134">Yeni **hex2Int** işlev ve işlev tanımı kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="83d0d-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="83d0d-135">Tüm İşlevler sahip bir **UDF** işlevi diğer eklenen önek.</span><span class="sxs-lookup"><span data-stu-id="83d0d-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="83d0d-136">Yapmanız *önekini dahil* Stream Analytics sorgunuzda işlevi çağırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="83d0d-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="83d0d-137">Bu durumda, çağrı **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="83d0d-138">Sorguda kullanıcı tanımlı bir JavaScript işlevi çağırma</span><span class="sxs-lookup"><span data-stu-id="83d0d-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="83d0d-139">Sorgu Düzenleyicisi'nde altında **iş TOPOLOJİ**seçin **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="83d0d-140">Sorgunuzu düzenleme ve bu gibi kullanıcı tanımlı işlev çağrısı:</span><span class="sxs-lookup"><span data-stu-id="83d0d-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="83d0d-141">Örnek veri dosyasını karşıya yüklemek için iş girişi sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="83d0d-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="83d0d-142">Sorgunuz test etme seçeneğini belirleyin **Test**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="83d0d-143">Desteklenen JavaScript nesneleri</span><span class="sxs-lookup"><span data-stu-id="83d0d-143">Supported JavaScript objects</span></span>
<span data-ttu-id="83d0d-144">Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler, standart, yerleşik JavaScript nesneleri destekler.</span><span class="sxs-lookup"><span data-stu-id="83d0d-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="83d0d-145">Bu nesnelerin bir listesi için bkz: [genel nesneler](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="83d0d-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="83d0d-146">Akış analizi ve JavaScript tür dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="83d0d-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="83d0d-147">Stream Analytics dil ve JavaScript desteği sorgu türleri farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="83d0d-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="83d0d-148">Bu tabloda ikisi arasında dönüştürme eşlemeleri listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="83d0d-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="83d0d-149">Akış Analizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-149">Stream Analytics</span></span> | <span data-ttu-id="83d0d-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="83d0d-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="83d0d-151">bigint</span><span class="sxs-lookup"><span data-stu-id="83d0d-151">bigint</span></span> | <span data-ttu-id="83d0d-152">Sayı (JavaScript yalnızca tam olarak 2 kadar tamsayılar temsil eden ^ 53)</span><span class="sxs-lookup"><span data-stu-id="83d0d-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="83d0d-153">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="83d0d-153">DateTime</span></span> | <span data-ttu-id="83d0d-154">Tarih (JavaScript yalnızca destekler milisaniye)</span><span class="sxs-lookup"><span data-stu-id="83d0d-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="83d0d-155">Çift</span><span class="sxs-lookup"><span data-stu-id="83d0d-155">double</span></span> | <span data-ttu-id="83d0d-156">Sayı</span><span class="sxs-lookup"><span data-stu-id="83d0d-156">Number</span></span>
<span data-ttu-id="83d0d-157">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="83d0d-157">nvarchar(MAX)</span></span> | <span data-ttu-id="83d0d-158">Dize</span><span class="sxs-lookup"><span data-stu-id="83d0d-158">String</span></span>
<span data-ttu-id="83d0d-159">Kayıt</span><span class="sxs-lookup"><span data-stu-id="83d0d-159">Record</span></span> | <span data-ttu-id="83d0d-160">Nesne</span><span class="sxs-lookup"><span data-stu-id="83d0d-160">Object</span></span>
<span data-ttu-id="83d0d-161">Dizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-161">Array</span></span> | <span data-ttu-id="83d0d-162">Dizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-162">Array</span></span>
<span data-ttu-id="83d0d-163">NULL</span><span class="sxs-lookup"><span data-stu-id="83d0d-163">NULL</span></span> | <span data-ttu-id="83d0d-164">Null</span><span class="sxs-lookup"><span data-stu-id="83d0d-164">Null</span></span>


<span data-ttu-id="83d0d-165">JavaScript Stream Analytics dönüşümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="83d0d-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="83d0d-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="83d0d-166">JavaScript</span></span> | <span data-ttu-id="83d0d-167">Akış Analizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="83d0d-168">Sayı</span><span class="sxs-lookup"><span data-stu-id="83d0d-168">Number</span></span> | <span data-ttu-id="83d0d-169">Bigint (sayı yuvarlak ve uzun arasında ise. MinValue ve uzun süre. MaxValue; Aksi takdirde, çift)</span><span class="sxs-lookup"><span data-stu-id="83d0d-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="83d0d-170">Tarih</span><span class="sxs-lookup"><span data-stu-id="83d0d-170">Date</span></span> | <span data-ttu-id="83d0d-171">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="83d0d-171">DateTime</span></span>
<span data-ttu-id="83d0d-172">Dize</span><span class="sxs-lookup"><span data-stu-id="83d0d-172">String</span></span> | <span data-ttu-id="83d0d-173">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="83d0d-173">nvarchar(MAX)</span></span>
<span data-ttu-id="83d0d-174">Nesne</span><span class="sxs-lookup"><span data-stu-id="83d0d-174">Object</span></span> | <span data-ttu-id="83d0d-175">Kayıt</span><span class="sxs-lookup"><span data-stu-id="83d0d-175">Record</span></span>
<span data-ttu-id="83d0d-176">Dizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-176">Array</span></span> | <span data-ttu-id="83d0d-177">Dizi</span><span class="sxs-lookup"><span data-stu-id="83d0d-177">Array</span></span>
<span data-ttu-id="83d0d-178">Null, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="83d0d-178">Null, Undefined</span></span> | <span data-ttu-id="83d0d-179">NULL</span><span class="sxs-lookup"><span data-stu-id="83d0d-179">NULL</span></span>
<span data-ttu-id="83d0d-180">Herhangi bir türü (örneğin, bir işlev veya hata)</span><span class="sxs-lookup"><span data-stu-id="83d0d-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="83d0d-181">(Çalışma zamanı hatası sonuçlarında) desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="83d0d-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="83d0d-182">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="83d0d-182">Troubleshooting</span></span>
<span data-ttu-id="83d0d-183">JavaScript çalışma zamanı hataları önemli kabul edilir ve etkinlik günlüğü ortaya çıkmış.</span><span class="sxs-lookup"><span data-stu-id="83d0d-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="83d0d-184">Günlük almak için Azure portalında, iş'e gidin ve seçin **etkinlik günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="83d0d-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="83d0d-185">Diğer JavaScript kullanıcı tanımlı işlev desenleri</span><span class="sxs-lookup"><span data-stu-id="83d0d-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="83d0d-186">İç içe geçmiş JSON çıktısını almak için yazma</span><span class="sxs-lookup"><span data-stu-id="83d0d-186">Write nested JSON to output</span></span>
<span data-ttu-id="83d0d-187">Çıkış akış analizi işi giriş olarak kullanan bir izleme işleme adımı vardır ve bir JSON biçimi gerektiriyorsa, çıkış için bir JSON dizesi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d0d-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="83d0d-188">Sonraki örnekte çağrıları **JSON.stringify()** tüm ad/değer çiftleri giriş paketi için işlev ve bunları tek bir dize değeri çıktı olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="83d0d-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="83d0d-189">**JavaScript kullanıcı tanımlı işlev tanımı:**</span><span class="sxs-lookup"><span data-stu-id="83d0d-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="83d0d-190">**Örnek Sorgu:**</span><span class="sxs-lookup"><span data-stu-id="83d0d-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="83d0d-191">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="83d0d-191">Get help</span></span>
<span data-ttu-id="83d0d-192">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="83d0d-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83d0d-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83d0d-193">Next steps</span></span>
* [<span data-ttu-id="83d0d-194">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="83d0d-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="83d0d-195">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="83d0d-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="83d0d-196">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="83d0d-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="83d0d-197">Azure Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="83d0d-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="83d0d-198">Azure Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="83d0d-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

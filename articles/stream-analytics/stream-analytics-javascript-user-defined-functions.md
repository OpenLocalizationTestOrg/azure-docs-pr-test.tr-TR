---
title: "aaaAzure Stream Analytics JavaScript kullanıcı tanımlı işlevler | Microsoft Docs"
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
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="b3896-104">Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="b3896-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="b3896-105">Azure akış analizi, kullanıcı tanımlı işlevler JavaScript'te yazılmış destekler.</span><span class="sxs-lookup"><span data-stu-id="b3896-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="b3896-106">Merhaba zengin kümesiyle **dize**, **RegExp**, **matematik**, **dizi**, ve **tarih** yöntemleri, JavaScript sağlar, karmaşık veri dönüşümleri akış analizi işleri ile daha kolay toocreate haline gelir.</span><span class="sxs-lookup"><span data-stu-id="b3896-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="b3896-107">JavaScript kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="b3896-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="b3896-108">JavaScript kullanıcı tanımlı işlevler harici bağlantı gerektirmeyen durum bilgisiz, yalnızca işlem skaler işlevler destekler.</span><span class="sxs-lookup"><span data-stu-id="b3896-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="b3896-109">Merhaba dönüş değeri işlevinin yalnızca bir skaler (tek) olabilir.</span><span class="sxs-lookup"><span data-stu-id="b3896-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="b3896-110">Bir JavaScript kullanıcı tanımlı işlev tooa işi ekledikten sonra hello işlevi herhangi bir yere yerleşik bir skaler işlev gibi hello sorgu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3896-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="b3896-111">Burada JavaScript kullanıcı tanımlı işlevler kullanışlı bulabileceğiniz bazı senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b3896-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="b3896-112">Ayrıştırma ve normal ifade İşlevler, örneğin, sahip dizeleri düzenleme **Regexp_Replace()** ve **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="b3896-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="b3896-113">Kod çözme ve kodlama verileri, örneğin, ikili onaltılık dönüştürme</span><span class="sxs-lookup"><span data-stu-id="b3896-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="b3896-114">JavaScript ile mathematic hesaplamalar gerçekleştirmek **matematik** işlevleri</span><span class="sxs-lookup"><span data-stu-id="b3896-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="b3896-115">Sıralama, birleştirme, bulma ve dolgu gibi dizi işlemlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="b3896-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="b3896-116">Stream Analytics içinde JavaScript kullanıcı tanımlı işlev ile yapamayacağınız bazı noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b3896-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="b3896-117">Duyurmak gerçekleştirme dış REST uç noktalar, örneğin, bir dış kaynaktan IP arama veya başvuru veri çekilmesini ters</span><span class="sxs-lookup"><span data-stu-id="b3896-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="b3896-118">Özel olay biçimi serileştirme gerçekleştirmek veya giriş/çıkış üzerinde seri durumundan çıkarma</span><span class="sxs-lookup"><span data-stu-id="b3896-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="b3896-119">Özel toplamaları oluşturun</span><span class="sxs-lookup"><span data-stu-id="b3896-119">Create custom aggregates</span></span>

<span data-ttu-id="b3896-120">Gibi çalışır ancak **Date.GetDate()** veya **Math.random()** engellenmediğinden hello işlevleri tanımında bunları yapmaktan kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="b3896-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="b3896-121">Bu işlevler **sağlamadığı** dönüş hello aynı bunları arayın ve hello Azure Stream Analytics hizmeti, işlev çağrılarını günlüğü tutun değil her zaman ve neden sonuç döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="b3896-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="b3896-122">Bir işlev, farklı sonuç hello üzerinde aynı olayları döndürürse, sizin tarafınızdan veya hello Stream Analytics hizmeti tarafından bir iş yeniden başlatıldığında Yinelenebilirlik garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="b3896-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="b3896-123">Kullanıcı tanımlı bir JavaScript işlevi hello Azure portal Ekle</span><span class="sxs-lookup"><span data-stu-id="b3896-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="b3896-124">toocreate basit JavaScript kullanıcı tanımlı bir işlev var olan bir akış analizi işi altındaki adımları yapın:</span><span class="sxs-lookup"><span data-stu-id="b3896-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="b3896-125">Hello Azure portal, Stream Analytics işi bulun.</span><span class="sxs-lookup"><span data-stu-id="b3896-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="b3896-126">Altında **iş TOPOLOJİ**, işlevinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b3896-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="b3896-127">İşlevler boş bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b3896-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="b3896-128">Yeni bir kullanıcı tanımlı işlev, toocreate seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b3896-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="b3896-129">Merhaba üzerinde **yeni işlev** dikey penceresinde için **işlev türü**seçin **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="b3896-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="b3896-130">Varsayılan işlev şablonunun hello Düzenleyicisi'nde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b3896-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="b3896-131">Hello için **UDF diğer**, girin **hex2Int**ve hello işlevi uygulamasını aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b3896-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="b3896-132">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="b3896-132">Select **Save**.</span></span> <span data-ttu-id="b3896-133">İşlevinizi hello işlevleri listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b3896-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="b3896-134">Select hello yeni **hex2Int** işlev ve hello işlevi tanımını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b3896-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="b3896-135">Tüm İşlevler sahip bir **UDF** öneki eklenen toohello işlevi diğer adı.</span><span class="sxs-lookup"><span data-stu-id="b3896-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="b3896-136">Çok ihtiyacınız*hello önekini ekleyin* Stream Analytics sorgunuzu hello işlevi çağırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="b3896-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="b3896-137">Bu durumda, çağrı **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="b3896-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="b3896-138">Sorguda kullanıcı tanımlı bir JavaScript işlevi çağırma</span><span class="sxs-lookup"><span data-stu-id="b3896-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="b3896-139">Hello Düzenleyicisi altında sorgu **iş TOPOLOJİ**seçin **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="b3896-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="b3896-140">Sorgunuzu düzenleme ve hello kullanıcı tanımlı işlev, bu gibi çağırın:</span><span class="sxs-lookup"><span data-stu-id="b3896-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="b3896-141">tooupload hello örnek veri dosyası, sağ hello iş girişi.</span><span class="sxs-lookup"><span data-stu-id="b3896-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="b3896-142">tootest sorgunuzu, select **Test**.</span><span class="sxs-lookup"><span data-stu-id="b3896-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="b3896-143">Desteklenen JavaScript nesneleri</span><span class="sxs-lookup"><span data-stu-id="b3896-143">Supported JavaScript objects</span></span>
<span data-ttu-id="b3896-144">Azure Stream Analytics JavaScript kullanıcı tanımlı işlevler, standart, yerleşik JavaScript nesneleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b3896-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="b3896-145">Bu nesnelerin bir listesi için bkz: [genel nesneler](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="b3896-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="b3896-146">Akış analizi ve JavaScript tür dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="b3896-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="b3896-147">Merhaba Stream Analytics sorgu dilini ve JavaScript desteği hello türleri farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="b3896-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="b3896-148">Bu tabloda hello iki arasındaki hello dönüştürme eşlemeleri listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="b3896-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="b3896-149">Akış Analizi</span><span class="sxs-lookup"><span data-stu-id="b3896-149">Stream Analytics</span></span> | <span data-ttu-id="b3896-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b3896-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="b3896-151">bigint</span><span class="sxs-lookup"><span data-stu-id="b3896-151">bigint</span></span> | <span data-ttu-id="b3896-152">Sayı (JavaScript yalnızca tamsayı tooprecisely 2 Yukarı temsil eden ^ 53)</span><span class="sxs-lookup"><span data-stu-id="b3896-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="b3896-153">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="b3896-153">DateTime</span></span> | <span data-ttu-id="b3896-154">Tarih (JavaScript yalnızca destekler milisaniye)</span><span class="sxs-lookup"><span data-stu-id="b3896-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="b3896-155">Çift</span><span class="sxs-lookup"><span data-stu-id="b3896-155">double</span></span> | <span data-ttu-id="b3896-156">Sayı</span><span class="sxs-lookup"><span data-stu-id="b3896-156">Number</span></span>
<span data-ttu-id="b3896-157">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="b3896-157">nvarchar(MAX)</span></span> | <span data-ttu-id="b3896-158">Dize</span><span class="sxs-lookup"><span data-stu-id="b3896-158">String</span></span>
<span data-ttu-id="b3896-159">Kayıt</span><span class="sxs-lookup"><span data-stu-id="b3896-159">Record</span></span> | <span data-ttu-id="b3896-160">Nesne</span><span class="sxs-lookup"><span data-stu-id="b3896-160">Object</span></span>
<span data-ttu-id="b3896-161">Dizi</span><span class="sxs-lookup"><span data-stu-id="b3896-161">Array</span></span> | <span data-ttu-id="b3896-162">Dizi</span><span class="sxs-lookup"><span data-stu-id="b3896-162">Array</span></span>
<span data-ttu-id="b3896-163">NULL</span><span class="sxs-lookup"><span data-stu-id="b3896-163">NULL</span></span> | <span data-ttu-id="b3896-164">Null</span><span class="sxs-lookup"><span data-stu-id="b3896-164">Null</span></span>


<span data-ttu-id="b3896-165">JavaScript Stream Analytics dönüşümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b3896-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="b3896-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b3896-166">JavaScript</span></span> | <span data-ttu-id="b3896-167">Akış Analizi</span><span class="sxs-lookup"><span data-stu-id="b3896-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="b3896-168">Sayı</span><span class="sxs-lookup"><span data-stu-id="b3896-168">Number</span></span> | <span data-ttu-id="b3896-169">Bigint (Merhaba numarası yuvarlak ve uzun arasında ise. MinValue ve uzun süre. MaxValue; Aksi takdirde, çift)</span><span class="sxs-lookup"><span data-stu-id="b3896-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="b3896-170">Tarih</span><span class="sxs-lookup"><span data-stu-id="b3896-170">Date</span></span> | <span data-ttu-id="b3896-171">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="b3896-171">DateTime</span></span>
<span data-ttu-id="b3896-172">Dize</span><span class="sxs-lookup"><span data-stu-id="b3896-172">String</span></span> | <span data-ttu-id="b3896-173">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="b3896-173">nvarchar(MAX)</span></span>
<span data-ttu-id="b3896-174">Nesne</span><span class="sxs-lookup"><span data-stu-id="b3896-174">Object</span></span> | <span data-ttu-id="b3896-175">Kayıt</span><span class="sxs-lookup"><span data-stu-id="b3896-175">Record</span></span>
<span data-ttu-id="b3896-176">Dizi</span><span class="sxs-lookup"><span data-stu-id="b3896-176">Array</span></span> | <span data-ttu-id="b3896-177">Dizi</span><span class="sxs-lookup"><span data-stu-id="b3896-177">Array</span></span>
<span data-ttu-id="b3896-178">Null, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="b3896-178">Null, Undefined</span></span> | <span data-ttu-id="b3896-179">NULL</span><span class="sxs-lookup"><span data-stu-id="b3896-179">NULL</span></span>
<span data-ttu-id="b3896-180">Herhangi bir türü (örneğin, bir işlev veya hata)</span><span class="sxs-lookup"><span data-stu-id="b3896-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="b3896-181">(Çalışma zamanı hatası sonuçlarında) desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="b3896-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b3896-182">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b3896-182">Troubleshooting</span></span>
<span data-ttu-id="b3896-183">JavaScript çalışma zamanı hataları önemli kabul edilir ve hello etkinlik günlüğü ortaya çıkmış.</span><span class="sxs-lookup"><span data-stu-id="b3896-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="b3896-184">hello Azure portal, Git tooyour işi seçip tooretrieve hello günlük **etkinlik günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="b3896-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="b3896-185">Diğer JavaScript kullanıcı tanımlı işlev desenleri</span><span class="sxs-lookup"><span data-stu-id="b3896-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="b3896-186">İç içe geçmiş JSON toooutput yazma</span><span class="sxs-lookup"><span data-stu-id="b3896-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="b3896-187">Çıkış akış analizi işi giriş olarak kullanan bir izleme işleme adımı vardır ve bir JSON biçimi gerektiriyorsa, JSON dizesi toooutput yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3896-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="b3896-188">Merhaba sonraki örneği çağırır hello **JSON.stringify()** hello tüm ad/değer çiftlerini giriş ve çıkış tek bir dize değer olarak yazma toopack işlev.</span><span class="sxs-lookup"><span data-stu-id="b3896-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="b3896-189">**JavaScript kullanıcı tanımlı işlev tanımı:**</span><span class="sxs-lookup"><span data-stu-id="b3896-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="b3896-190">**Örnek Sorgu:**</span><span class="sxs-lookup"><span data-stu-id="b3896-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="b3896-191">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="b3896-191">Get help</span></span>
<span data-ttu-id="b3896-192">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b3896-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3896-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3896-193">Next steps</span></span>
* [<span data-ttu-id="b3896-194">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="b3896-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b3896-195">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b3896-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b3896-196">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b3896-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b3896-197">Azure Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="b3896-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b3896-198">Azure Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b3896-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

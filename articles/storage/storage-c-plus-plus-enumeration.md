---
title: "Merhaba C++ için depolama istemci kitaplığı ile aaaList Azure Storage kaynaklarını | Microsoft Docs"
description: "C++ tooenumerate kapsayıcıları, blobları, Microsoft Azure Storage istemci kitaplığı API'leri listeleme toouse hello nasıl kuyruklar, bilgi tabloları ve varlıkları."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="2d346-103">C++'ta Azure Storage kaynakları listeler</span><span class="sxs-lookup"><span data-stu-id="2d346-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="2d346-104">Liste, Azure Storage ile anahtar toomany geliştirme senaryolarını işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="2d346-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="2d346-105">Bu makalede nasıl toomost verimli bir şekilde listeleme C++ için Microsoft Azure Storage istemci kitaplığı hello API'lerinden listeleme hello kullanarak Azure storage'da nesneleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2d346-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="2d346-106">Bu kılavuzda C++ sürümü için Azure Storage istemci kitaplığı hello hedefler aracılığıyla kullanıma 2.x [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="2d346-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="2d346-107">Merhaba depolama istemci kitaplığı çeşitli yöntemleri toolist veya Azure Storage sorgu nesneleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2d346-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="2d346-108">Bu makalede senaryoları aşağıdaki hello ele alır:</span><span class="sxs-lookup"><span data-stu-id="2d346-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="2d346-109">Bir hesap listesi kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="2d346-109">List containers in an account</span></span>
* <span data-ttu-id="2d346-110">Liste BLOB bir kapsayıcı veya sanal blob dizini</span><span class="sxs-lookup"><span data-stu-id="2d346-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="2d346-111">Bir hesap listesi kuyruklar</span><span class="sxs-lookup"><span data-stu-id="2d346-111">List queues in an account</span></span>
* <span data-ttu-id="2d346-112">Bir hesap listede tablolar</span><span class="sxs-lookup"><span data-stu-id="2d346-112">List tables in an account</span></span>
* <span data-ttu-id="2d346-113">Bir tablodaki sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="2d346-113">Query entities in a table</span></span>

<span data-ttu-id="2d346-114">Bu yöntemlerin her biri için farklı senaryolar farklı aşırı yüklemeleri kullanarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="2d346-115">Zaman uyumlu ve zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="2d346-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="2d346-116">Merhaba C++ için depolama istemci kitaplığı hello üzerine inşa edildiğinden [C++ REST Kitaplığı](https://github.com/Microsoft/cpprestsdk), kendiliğinden zaman uyumsuz işlemleri kullanarak destekliyoruz [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="2d346-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="2d346-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2d346-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="2d346-118">Zaman uyumlu işlemler hello karşılık gelen zaman uyumsuz işlemleri kaydır:</span><span class="sxs-lookup"><span data-stu-id="2d346-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="2d346-119">Birden çok iş parçacıklı uygulamalar veya hizmetler ile çalışıyorsanız, doğrudan bir iş parçacığı toocall hello eşitleme, performansı önemli ölçüde etkiler API ' larını oluşturmak yerine hello zaman uyumsuz API'leri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2d346-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="2d346-120">Bölümlenmiş listeleme</span><span class="sxs-lookup"><span data-stu-id="2d346-120">Segmented listing</span></span>
<span data-ttu-id="2d346-121">Bulut depolama Hello ölçeğini bölümlenmiş listeleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2d346-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="2d346-122">Örneğin, bir Azure blob kapsayıcısındaki bir milyon BLOB veya bir Azure tablosu bir milyar varlıklarda üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="2d346-123">Bunlar teorik numaraları, ancak gerçek müşteri kullanım durumları olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="2d346-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="2d346-124">Bu nedenle, tüm nesneleri tek bir yanıtta pratik toolist olur.</span><span class="sxs-lookup"><span data-stu-id="2d346-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="2d346-125">Bunun yerine, disk belleği kullanarak nesneleri listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d346-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="2d346-126">Her API listeleme hello sahip bir *kesimli* aşırı yükleme.</span><span class="sxs-lookup"><span data-stu-id="2d346-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="2d346-127">bölümlenmiş listeleme işlemi Hello yanıtı içerir:</span><span class="sxs-lookup"><span data-stu-id="2d346-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="2d346-128"><i>_segment</i>, API listeleyen tek çağrı toohello için döndürülen sonuçları hello kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="2d346-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="2d346-129">*continuation_token*, hangi geçirilir toohello sonraki çağrı sırası tooget hello sonraki sonuç sayfasını içinde.</span><span class="sxs-lookup"><span data-stu-id="2d346-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="2d346-130">Daha fazla hiçbir sonuç tooreturn olduğunda hello devamlılık belirteci null.</span><span class="sxs-lookup"><span data-stu-id="2d346-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="2d346-131">Örneğin, tipik çağrısı toolist bir kapsayıcıdaki tüm blob'lara hello kod parçacığını aşağıdaki gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="2d346-132">Merhaba kodudur bulunan bizim [örnekleri](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="2d346-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="2d346-133">Bir sayfa döndürülen sonuç sayısı Hello hello parametresiyle denetlenebilir Not *max_results* örneğin her API hello yüklemesini içinde:</span><span class="sxs-lookup"><span data-stu-id="2d346-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="2d346-134">Merhaba belirtmezseniz *max_results* parametresi, hello varsayılan too5000 sonuçları yukarı en büyük değer olan tek bir sayfayla döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2d346-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="2d346-135">Ayrıca, Azure Table storage bir sorgu kayıt yok veya hello hello değerinden daha az sayıda kayıt döndürebilir unutmayın *max_results* hello devamlılık belirteci boş olsa bile, belirtilen parametre.</span><span class="sxs-lookup"><span data-stu-id="2d346-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="2d346-136">Nedenlerinden biri, o hello sorgu beş saniye içinde tamamlanamadı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="2d346-137">Hello devamlılık belirteci boş değil sürece hello sorgu devam etmesi gerektiğini ve kodunuzu segment sonuçları hello boyutunu varsayımında bulunmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="2d346-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="2d346-138">Çoğu senaryo için desen kodlama listeleme listeleme veya sorgulama açık ilerleme sağlayan bölümlenmiş ve hello hizmet tooeach isteği nasıl yanıt vereceğini Hello önerilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="2d346-139">Özellikle C++ uygulamalar veya hizmetler için alt düzey denetim ilerleme listeleme hello denetim bellek ve performans yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="2d346-140">Doyumsuz listeleme</span><span class="sxs-lookup"><span data-stu-id="2d346-140">Greedy listing</span></span>
<span data-ttu-id="2d346-141">Merhaba C++ için depolama istemci Kitaplığı'nın önceki sürümlerini (sürümleri 0.5.0 Önizleme ve önceki sürümler) kesimli olmayan listeleme API'leri tablolar ve Kuyruklar aşağıdaki örneğine hello olduğu için dahil:</span><span class="sxs-lookup"><span data-stu-id="2d346-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="2d346-142">Bu yöntemleri bölümlenmiş API'leri sarmalayıcılar olarak oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2d346-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="2d346-143">Her yanıtı bölümlenmiş dökümün hello kod hello sonuçları tooa vektör eklenmiş ve tam Merhaba kapsayıcılara taranan sonra tüm sonuç döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="2d346-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="2d346-144">Az sayıda nesne Hello depolama hesabı veya tablo içerdiğinde, bu yaklaşım çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="2d346-145">Ancak, tüm sonuçları bellekte kalan çünkü bir artış ile Merhaba nesnelerin sayısı, gerekli hello bellek sınırı arttırabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="2d346-146">Bir listeleme işlemi sırasında hangi hello ilerleme durumunu hakkında hiçbir bilgi arayan sahip bir çok uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="2d346-147">Doyumsuz bu hello SDK API'leri listeleme C# ' ta, Java, yok veya JavaScript Node.js ortamı hello.</span><span class="sxs-lookup"><span data-stu-id="2d346-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="2d346-148">doyumsuz bu API'leri kullanarak tooavoid hello olası sorunları, biz onları kaldırmış sürüm 0.6.0 Önizleme.</span><span class="sxs-lookup"><span data-stu-id="2d346-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="2d346-149">Kodunuzu bu doyumsuz API çağırıyorsa:</span><span class="sxs-lookup"><span data-stu-id="2d346-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="2d346-150">Kodunuzu değiştirmelisiniz sonra toouse hello kesimli API'leri listeleme:</span><span class="sxs-lookup"><span data-stu-id="2d346-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="2d346-151">Merhaba belirterek *max_results* parametresi hello kesiminin, Bakiye hello sayıda isteği ve uygulamanız için bellek kullanım toomeet başarım düşünceleri arasında.</span><span class="sxs-lookup"><span data-stu-id="2d346-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="2d346-152">Bölümlenmiş listeleme API'leri kullanarak ancak bir "Hızlı" stili yerel bir koleksiyondaki hello verilerini depolamak olduğunuz, ayrıca, aynı zamanda dikkatle ölçekte yerel bir koleksiyondaki veri depolama, kod toohandle yeniden düzenlemeniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="2d346-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="2d346-153">Yavaş listeleme</span><span class="sxs-lookup"><span data-stu-id="2d346-153">Lazy listing</span></span>
<span data-ttu-id="2d346-154">Doyumsuz listeleme olası sorunları ortaya hello kapsayıcısında çok fazla nesne değilse bu kullanışlı olsa da.</span><span class="sxs-lookup"><span data-stu-id="2d346-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="2d346-155">C# veya Oracle Java SDK'ları da kullanıyorsanız, bir yavaş, gerekirse burada hello belirli uzaklığındaki veri yalnızca alınmadığı listeleme stili sunan hello numaralandırılabilir programlama modeli, tanımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d346-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="2d346-156">C++'da, hello yineleyici tabanlı şablonunu de benzer bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="2d346-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="2d346-157">Tipik yavaş listeleme API'sini kullanarak **list_blobs** örnek olarak, şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="2d346-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="2d346-158">Merhaba yavaş listeleme desen kullanan bir tipik kod parçacığını şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="2d346-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="2d346-159">Yavaş listeleme yalnızca zaman uyumlu modda kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2d346-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="2d346-160">Doyumsuz listesi ile karşılaştırıldığında, yavaş listeleme verileri yalnızca gerekli olduğunda getirir.</span><span class="sxs-lookup"><span data-stu-id="2d346-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="2d346-161">Yalnızca hello sonraki yineleyici sonraki segmentin taşındığında hello perde arkasında bu verileri Azure depolama biriminden getirir.</span><span class="sxs-lookup"><span data-stu-id="2d346-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="2d346-162">Bu nedenle, bellek kullanımı ile sınırlanmış bir boyutu denetlenir ve hello hızlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2d346-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="2d346-163">Yavaş listeleme API'leri dahil edilir hello depolama istemci kitaplığı C++ için sürüm 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="2d346-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2d346-164">Sonuç</span><span class="sxs-lookup"><span data-stu-id="2d346-164">Conclusion</span></span>
<span data-ttu-id="2d346-165">Bu makalede, C++ için depolama istemci kitaplığı hello çeşitli nesneler için API listeleme için farklı aşırı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2d346-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="2d346-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="2d346-166">toosummarize:</span></span>

* <span data-ttu-id="2d346-167">Zaman uyumsuz API'leri birden çok iş parçacığı senaryolarda önerilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="2d346-168">Bölümlenmiş listeleme çoğu senaryolar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="2d346-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="2d346-169">Yavaş listeleme kullanışlı bir sarmalayıcı zaman uyumlu senaryolarda olarak hello Kitaplığı'nda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2d346-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="2d346-170">Doyumsuz listeleme tavsiye edilmez ve hello Kitaplığı'ndan kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="2d346-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d346-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d346-171">Next steps</span></span>
<span data-ttu-id="2d346-172">C++ için Azure Storage istemci Kitaplığı hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="2d346-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="2d346-173">Nasıl toouse Blob depolama alanından C++</span><span class="sxs-lookup"><span data-stu-id="2d346-173">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="2d346-174">Nasıl toouse C++ tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="2d346-174">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="2d346-175">Nasıl toouse C++ içinden kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="2d346-175">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="2d346-176">C++ API belgeleri için Azure Storage istemci kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="2d346-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="2d346-177">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="2d346-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="2d346-178">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="2d346-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)


---
title: "C++ için depolama istemci kitaplığı ile Azure Storage kaynaklarını listesi | Microsoft Docs"
description: "Kapsayıcı, BLOB, kuyruklar, tabloları ve varlıkları numaralandırmak için C++ için Microsoft Azure depolama istemci Kitaplığı'ndaki listenin API'leri kullanmayı öğrenin."
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
ms.openlocfilehash: 9844412739f4f6f95416f81347f0f2eeeca62bea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="a54c0-103">C++'ta Azure Storage kaynakları listeler</span><span class="sxs-lookup"><span data-stu-id="a54c0-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="a54c0-104">Liste, Azure Storage ile birçok geliştirme senaryolarını anahtarına işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="a54c0-105">Bu makalede, Azure listenin C++ için Microsoft Azure depolama istemci Kitaplığı'nda sağlanan API'leri kullanarak depolama en verimli bir şekilde derlemesindeki açıklar.</span><span class="sxs-lookup"><span data-stu-id="a54c0-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="a54c0-106">Bu kılavuz hedefleyen C++ sürümü için Azure Storage istemci kitaplığı aracılığıyla kullanıma 2.x [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="a54c0-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="a54c0-107">Depolama istemcisi kitaplığı çeşitli Azure Storage liste veya sorgu nesneleri için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a54c0-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="a54c0-108">Bu makalede aşağıdaki senaryolar ele alır:</span><span class="sxs-lookup"><span data-stu-id="a54c0-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="a54c0-109">Bir hesap listesi kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="a54c0-109">List containers in an account</span></span>
* <span data-ttu-id="a54c0-110">Liste BLOB bir kapsayıcı veya sanal blob dizini</span><span class="sxs-lookup"><span data-stu-id="a54c0-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="a54c0-111">Bir hesap listesi kuyruklar</span><span class="sxs-lookup"><span data-stu-id="a54c0-111">List queues in an account</span></span>
* <span data-ttu-id="a54c0-112">Bir hesap listede tablolar</span><span class="sxs-lookup"><span data-stu-id="a54c0-112">List tables in an account</span></span>
* <span data-ttu-id="a54c0-113">Bir tablodaki sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="a54c0-113">Query entities in a table</span></span>

<span data-ttu-id="a54c0-114">Bu yöntemlerin her biri için farklı senaryolar farklı aşırı yüklemeleri kullanarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="a54c0-115">Zaman uyumlu ve zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="a54c0-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="a54c0-116">C++ için depolama istemci kitaplığı üzerine inşa edildiğinden [C++ REST Kitaplığı](https://github.com/Microsoft/cpprestsdk), kendiliğinden zaman uyumsuz işlemleri kullanarak destekliyoruz [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="a54c0-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="a54c0-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a54c0-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="a54c0-118">Zaman uyumlu işlemler karşılık gelen zaman uyumsuz işlemleri kaydır:</span><span class="sxs-lookup"><span data-stu-id="a54c0-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="a54c0-119">Birden çok iş parçacıklı uygulamalar veya hizmetler ile çalışıyorsanız, zaman uyumsuz API'lerini doğrudan bir iş parçacığı oluşturma yerine eşitleme, performansı önemli ölçüde etkiler API'leri çağırmak için kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a54c0-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="a54c0-120">Bölümlenmiş listeleme</span><span class="sxs-lookup"><span data-stu-id="a54c0-120">Segmented listing</span></span>
<span data-ttu-id="a54c0-121">Bulut depolama ölçeğini bölümlenmiş listeleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="a54c0-122">Örneğin, bir Azure blob kapsayıcısındaki bir milyon BLOB veya bir Azure tablosu bir milyar varlıklarda üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="a54c0-123">Bunlar teorik numaraları, ancak gerçek müşteri kullanım durumları olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="a54c0-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="a54c0-124">Bu nedenle, tek bir yanıt tüm nesneleri listelemek için zordur.</span><span class="sxs-lookup"><span data-stu-id="a54c0-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="a54c0-125">Bunun yerine, disk belleği kullanarak nesneleri listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a54c0-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="a54c0-126">Her API listeleme sahip bir *kesimli* aşırı yükleme.</span><span class="sxs-lookup"><span data-stu-id="a54c0-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="a54c0-127">Bölümlenmiş listeleme işlemi yanıtı içerir:</span><span class="sxs-lookup"><span data-stu-id="a54c0-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="a54c0-128"><i>_segment</i>, tek bir çağrı listeleme API için döndürülen sonuç kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="a54c0-129">*continuation_token*, sonraki sonuç sayfasını alabilmek için sonraki çağrı geçirildi.</span><span class="sxs-lookup"><span data-stu-id="a54c0-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="a54c0-130">Devamlılık belirteci dönmek için daha fazla sonuç olduğunda null olur.</span><span class="sxs-lookup"><span data-stu-id="a54c0-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="a54c0-131">Örneğin, bir kapsayıcıdaki tüm blobları listelemek için tipik bir çağrı aşağıdaki kod parçacığını gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="a54c0-132">Kod kullanılabilir bizim [örnekleri](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="a54c0-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="a54c0-133">Bir sayfa döndürülen sonuç sayısı parametresiyle denetlenebilir Not *max_results* örneğin her API yüklemesini içinde:</span><span class="sxs-lookup"><span data-stu-id="a54c0-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="a54c0-134">Belirtmezseniz, *max_results* parametresi, varsayılan en büyük değer en fazla 5000 sonuçlarını tek bir sayfayla döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a54c0-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="a54c0-135">Ayrıca, Azure Table storage bir sorgu kayıt yok veya değerinden daha az sayıda kayıt döndürebilir unutmayın *max_results* devamlılık belirteci boş olsa bile, belirtilen parametre.</span><span class="sxs-lookup"><span data-stu-id="a54c0-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="a54c0-136">Nedenlerinden biri, sorgu beş saniye içinde tamamlanamadı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="a54c0-137">Devamlılık belirteci boş değil sürece, sorgu devam etmesi gerektiğini ve kodunuzu segment sonuçları boyutunu varsayımında bulunmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a54c0-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="a54c0-138">Çoğu senaryo için önerilen kodlama düzeni listeleme, liste veya sorgulama ve hizmetin her istek nasıl yanıt vereceğini açık ilerlemesini sağlayan kesimli.</span><span class="sxs-lookup"><span data-stu-id="a54c0-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="a54c0-139">Özellikle C++ uygulamalar veya hizmetler için alt düzey denetim listesi ilerleme denetim bellek ve performans yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="a54c0-140">Doyumsuz listeleme</span><span class="sxs-lookup"><span data-stu-id="a54c0-140">Greedy listing</span></span>
<span data-ttu-id="a54c0-141">C++ için depolama istemci Kitaplığı'nın önceki sürümlerini (sürümleri 0.5.0 Önizleme ve önceki sürümler) bölümlenmiş listesine API'leri tablolar ve Kuyruklar, aşağıdaki örnekte olduğu gibi dahil:</span><span class="sxs-lookup"><span data-stu-id="a54c0-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="a54c0-142">Bu yöntemleri bölümlenmiş API'leri sarmalayıcılar olarak oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a54c0-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="a54c0-143">Her yanıtı bölümlenmiş dökümün için kod sonuçları bir vektörüne eklenen ve tam kapsayıcıları taranan sonra tüm sonuç döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="a54c0-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="a54c0-144">Az sayıda nesne depolama hesabı veya tablo içerdiğinde, bu yaklaşım çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="a54c0-145">Ancak, tüm sonuçları bellekte kalan çünkü bir artış ile nesnelerin sayısı, gerekli bellek sınırı arttırabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="a54c0-146">Bir listeleme işlemi sırasında ilerleme durumunu hakkında hiçbir bilgi arayan sahip bir çok uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="a54c0-147">Bu doyumsuz listeleme SDK API'leri C#, Java veya JavaScript Node.js ortamında mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="a54c0-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="a54c0-148">Doyumsuz bu API'leri kullanarak olası sorunları önlemek için biz bunları 0.6.0 sürümde kaldırılan Önizleme.</span><span class="sxs-lookup"><span data-stu-id="a54c0-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="a54c0-149">Kodunuzu bu doyumsuz API çağırıyorsa:</span><span class="sxs-lookup"><span data-stu-id="a54c0-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="a54c0-150">Ardından kodunuzu bölümlenmiş listenin API'leri kullanmak için değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a54c0-150">Then you should modify your code to use the segmented listing APIs:</span></span>

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

<span data-ttu-id="a54c0-151">Belirterek *max_results* parametresi kesiminin, Bakiye isteklerinin sayısı ve uygulamanız için başarım düşünceleri karşılamak için bellek kullanımını arasında.</span><span class="sxs-lookup"><span data-stu-id="a54c0-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="a54c0-152">Bölümlenmiş listeleme API'leri kullanıyorsanız, ancak bir "Hızlı" stilde yerel bir koleksiyondaki verileri depolamak, ayrıca, aynı zamanda dikkatle ölçekte yerel bir koleksiyondaki veri depolama işlemek için kodunuzu yeniden düzenlemeniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="a54c0-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="a54c0-153">Yavaş listeleme</span><span class="sxs-lookup"><span data-stu-id="a54c0-153">Lazy listing</span></span>
<span data-ttu-id="a54c0-154">Doyumsuz listeleme olası sorunları ortaya kapsayıcısında çok fazla nesne değilse bu kullanışlı olsa da.</span><span class="sxs-lookup"><span data-stu-id="a54c0-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="a54c0-155">C# veya Oracle Java SDK'ları da kullanıyorsanız, bir yavaş, gerekirse burada belirli uzaklığındaki verileri yalnızca alınmadığı listeleme stili sunan numaralandırılabilir programlama modeli, tanımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="a54c0-156">C++'da, yineleyici tabanlı şablonunu de benzer bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="a54c0-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="a54c0-157">Tipik yavaş listeleme API'sini kullanarak **list_blobs** örnek olarak, şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="a54c0-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="a54c0-158">Yavaş listeleme desen kullanan bir tipik kod parçacığını şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="a54c0-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="a54c0-159">Yavaş listeleme yalnızca zaman uyumlu modda kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a54c0-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="a54c0-160">Doyumsuz listesi ile karşılaştırıldığında, yavaş listeleme verileri yalnızca gerekli olduğunda getirir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="a54c0-161">Yalnızca sonraki yineleyici sonraki segmentin taşındığında perde arkasında, verileri Azure depolama biriminden getirir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="a54c0-162">Bu nedenle, bellek kullanımı ile sınırlanmış bir boyutu denetlenir ve hızlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="a54c0-163">Yavaş listeleme API'leri dahil edilir depolama istemci Kitaplığı'nda C++ için sürüm 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="a54c0-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a54c0-164">Sonuç</span><span class="sxs-lookup"><span data-stu-id="a54c0-164">Conclusion</span></span>
<span data-ttu-id="a54c0-165">Bu makalede, C++ için depolama istemci Kitaplığı'nda çeşitli nesneler için API listeleme için farklı aşırı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a54c0-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="a54c0-166">Özetlemek için:</span><span class="sxs-lookup"><span data-stu-id="a54c0-166">To summarize:</span></span>

* <span data-ttu-id="a54c0-167">Zaman uyumsuz API'leri birden çok iş parçacığı senaryolarda önerilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="a54c0-168">Bölümlenmiş listeleme çoğu senaryolar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="a54c0-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="a54c0-169">Yavaş listeleme kullanışlı bir sarmalayıcı zaman uyumlu senaryolarda olarak kitaplıkta sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a54c0-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="a54c0-170">Doyumsuz listeleme tavsiye edilmez ve Kitaplığı'ndan kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="a54c0-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a54c0-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a54c0-171">Next steps</span></span>
<span data-ttu-id="a54c0-172">C++ için Azure Storage istemci Kitaplığı hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.</span><span class="sxs-lookup"><span data-stu-id="a54c0-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="a54c0-173">C++ içinden BLOB Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="a54c0-173">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="a54c0-174">Tablo depolama C++ içinden kullanma</span><span class="sxs-lookup"><span data-stu-id="a54c0-174">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="a54c0-175">C++ içinden kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="a54c0-175">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="a54c0-176">C++ API belgeleri için Azure Storage istemci kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="a54c0-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="a54c0-177">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="a54c0-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="a54c0-178">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="a54c0-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)


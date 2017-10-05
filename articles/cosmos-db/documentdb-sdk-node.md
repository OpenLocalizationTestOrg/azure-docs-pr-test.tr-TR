---
title: "Azure Cosmos DB Node.js API, SDK & kaynakları | Microsoft Docs"
description: "Node.js API ve yayın tarih, sona erme tarihlerini ve her Azure Cosmos DB Node.js SDK'sı sürüm arasında yapılan değişiklikler dahil olmak üzere SDK'sı hakkında bilgi edinin."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="384e2-103">Azure DB Cosmos Node.js SDK: sürüm notları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="384e2-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="384e2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="384e2-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="384e2-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="384e2-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="384e2-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="384e2-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="384e2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="384e2-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="384e2-108">Java</span><span class="sxs-lookup"><span data-stu-id="384e2-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="384e2-109">Python</span><span class="sxs-lookup"><span data-stu-id="384e2-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="384e2-110">REST</span><span class="sxs-lookup"><span data-stu-id="384e2-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="384e2-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="384e2-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="384e2-112">SQL</span><span class="sxs-lookup"><span data-stu-id="384e2-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="384e2-113">**SDK'sını indirin**</span><span class="sxs-lookup"><span data-stu-id="384e2-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="384e2-114">NPM</span><span class="sxs-lookup"><span data-stu-id="384e2-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="384e2-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="384e2-115">**API documentation**</span></span></td><td>[<span data-ttu-id="384e2-116">Node.js API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="384e2-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="384e2-117">**SDK yükleme yönergeleri**</span><span class="sxs-lookup"><span data-stu-id="384e2-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="384e2-118">Yükleme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="384e2-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="384e2-119">**SDK katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="384e2-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="384e2-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="384e2-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="384e2-121">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="384e2-121">**Samples**</span></span></td><td>[<span data-ttu-id="384e2-122">Node.js kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="384e2-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="384e2-123">**Başlangıç eğitmeni**</span><span class="sxs-lookup"><span data-stu-id="384e2-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="384e2-124">Node.js SDK'sı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="384e2-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="384e2-125">**Web uygulaması Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="384e2-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="384e2-126">Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="384e2-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="384e2-127">**Geçerli desteklenen platformlar**</span><span class="sxs-lookup"><span data-stu-id="384e2-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="384e2-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="384e2-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="384e2-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="384e2-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="384e2-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="384e2-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="384e2-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="384e2-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="384e2-132">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="384e2-132">Release notes</span></span>

### <span data-ttu-id="384e2-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="384e2-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="384e2-134">Sabit npm belgeleri.</span><span class="sxs-lookup"><span data-stu-id="384e2-134">npm documentation fixed.</span></span>

### <span data-ttu-id="384e2-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="384e2-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="384e2-136">Bir hata, burada ilgili belgelerini özel Unicode karakterler (LS, PS) b executeStoredProcedure içinde sabit.</span><span class="sxs-lookup"><span data-stu-id="384e2-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="384e2-137">Bölüm anahtarı Unicode karakterler içeren belgeleri işlemedeki hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="384e2-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="384e2-138">Sabit koleksiyonlar ile ad ortamı oluşturma desteği.</span><span class="sxs-lookup"><span data-stu-id="384e2-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="384e2-139">Github sorunu #114.</span><span class="sxs-lookup"><span data-stu-id="384e2-139">Github issue #114.</span></span>
* <span data-ttu-id="384e2-140">İzni yetkilendirme belirtecini sabit desteği.</span><span class="sxs-lookup"><span data-stu-id="384e2-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="384e2-141">Github sorunu #178.</span><span class="sxs-lookup"><span data-stu-id="384e2-141">Github issue #178.</span></span>

### <span data-ttu-id="384e2-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="384e2-143">Yeni bir desteği eklendi [tutarlılık düzeyi](consistency-levels.md) ConsistentPrefix çağrılır.</span><span class="sxs-lookup"><span data-stu-id="384e2-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="384e2-144">UriFactory desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="384e2-145">Unicode desteği hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="384e2-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="384e2-146">GitHub sorunu #171.</span><span class="sxs-lookup"><span data-stu-id="384e2-146">GitHub issue #171.</span></span>

### <span data-ttu-id="384e2-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="384e2-148">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="384e2-149">Çapraz bölüm sorgular için paralellik derecesi denetleme seçenek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="384e2-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="384e2-150">SSL doğrulama Azure Cosmos DB öykünücüsüne karşı çalıştırırken devre dışı bırakmak için seçenek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="384e2-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="384e2-151">En düşük işleme 2500 RU/s 10,100 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.</span><span class="sxs-lookup"><span data-stu-id="384e2-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="384e2-152">Tek bölümlü bir koleksiyon için devamlılık belirteci hata sabit.</span><span class="sxs-lookup"><span data-stu-id="384e2-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="384e2-153">Github sorunu #107.</span><span class="sxs-lookup"><span data-stu-id="384e2-153">Github issue #107.</span></span>
* <span data-ttu-id="384e2-154">0 tek param işlemedeki executeStoredProcedure hata sabit.</span><span class="sxs-lookup"><span data-stu-id="384e2-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="384e2-155">Github sorunu #155.</span><span class="sxs-lookup"><span data-stu-id="384e2-155">Github issue #155.</span></span>

### <span data-ttu-id="384e2-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="384e2-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="384e2-157">SDK sürümü dahil etmek için sabit user-agent üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="384e2-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="384e2-158">Küçük kod temizleme.</span><span class="sxs-lookup"><span data-stu-id="384e2-158">Minor code cleanup.</span></span>

### <span data-ttu-id="384e2-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="384e2-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="384e2-160">SSL doğrulama SDK emulator(hostname=localhost) hedeflemek için kullanırken devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="384e2-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="384e2-161">Saklı yordam yürütme sırasında betik günlüğünü etkinleştirme için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="384e2-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="384e2-163">Bölüm paralel sorgular çapraz eklenen desteği.</span><span class="sxs-lookup"><span data-stu-id="384e2-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="384e2-164">ÜST/ORDER BY sorguları bölümlenmiş koleksiyonlar için desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="384e2-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="384e2-166">Daraltılmış istekleri için eklenen yeniden deneme ilkesi desteği.</span><span class="sxs-lookup"><span data-stu-id="384e2-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="384e2-167">(Daraltılmış isteklerini bir istek oranı çok büyük özel durumu, hata kodu 429 alır.) Hata kodu 429 karşılaşıldığında, varsayılan olarak, Azure Cosmos DB dokuz kez her istek için yanıt üst bilgisi retryAfter zamanında uygularken yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="384e2-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="384e2-168">Yeniden denemeler arasında sunucu tarafından döndürülen retryAfter zaman yoksay istiyorsanız sabit yeniden deneme zaman aralığını şimdi RetryOptions özelliğinin bir parçası olarak ConnectionPolicy nesne üzerinde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="384e2-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="384e2-169">Azure Cosmos DB şimdi en fazla (bağımsız olarak yeniden deneme sayısı) kısıtlanan ve 429 hata koduyla yanıt döndüren her istek için 30 saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="384e2-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="384e2-170">Bu süre de ConnectionPolicy nesnesindeki RetryOptions özelliği geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="384e2-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="384e2-171">Yanıt üstbilgilerini kısıtlama belirtmek için her istekte yeniden deneme sayısı ve isteği yeniden denemeler arasında beklenen toplam süre gibi cosmos DB x-ms-kısıtlama-yeniden deneme-sayısı ve x-ms-throttle-retry-wait-time-ms şimdi döndürür.</span><span class="sxs-lookup"><span data-stu-id="384e2-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="384e2-172">Bazı varsayılan yeniden deneme seçeneklerini geçersiz kılmak için kullanılan ConnectionPolicy sınıfı RetryOptions özellikte gösterme RetryOptions sınıfı eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="384e2-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="384e2-174">Bölgeli veritabanı hesaplarını desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="384e2-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="384e2-176">Belgeler için zaman için Live(TTL) özelliği için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="384e2-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="384e2-178">Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="384e2-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="384e2-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="384e2-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="384e2-180">Burada, hatalı concat sonuçları nedeniyle bağlantıları döndürdü olmayan sabit RangePartitionResolver.resolveForRead hata.</span><span class="sxs-lookup"><span data-stu-id="384e2-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="384e2-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="384e2-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="384e2-182">HashParitionResolver resolveForRead() sabit: ne zaman sağlanan hiçbir bölüm anahtarı atma tüm kayıtlı bağlantıların listesini döndürme yerine bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="384e2-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="384e2-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="384e2-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="384e2-184">Sorunu giderir [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -ayrılmış HTTPS aracısı: Azure Cosmos DB amacıyla genel Aracısı değiştirme kaçının.</span><span class="sxs-lookup"><span data-stu-id="384e2-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="384e2-185">Ayrılmış bir aracı tüm lib'ın istekleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="384e2-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="384e2-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="384e2-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="384e2-187">Sorunu giderir [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - düzgün işleyecek medya kimlikleri tire.</span><span class="sxs-lookup"><span data-stu-id="384e2-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="384e2-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="384e2-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="384e2-189">Sorunu giderir [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -EventEmitter dinleyicisi sızıntısı uyarı.</span><span class="sxs-lookup"><span data-stu-id="384e2-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="384e2-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="384e2-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="384e2-191">Sorunu giderir [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -klasör karma büyük küçük harfe duyarlı sistemler için karma yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="384e2-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="384e2-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="384e2-193">Karma & aralığı bölüm çözümleyiciler ekleyerek parçalama destek uygular.</span><span class="sxs-lookup"><span data-stu-id="384e2-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="384e2-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="384e2-195">Upsert uygulayın.</span><span class="sxs-lookup"><span data-stu-id="384e2-195">Implement Upsert.</span></span> <span data-ttu-id="384e2-196">DocumentClient yeni upsertXXX yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="384e2-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="384e2-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="384e2-198">Sürüm numaraları diğer SDK ile hizalama getirilecek atlandı.</span><span class="sxs-lookup"><span data-stu-id="384e2-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="384e2-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="384e2-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="384e2-200">Bölünmüş Q yeni bir havuz için sarmalayıcı taahhüt eder.</span><span class="sxs-lookup"><span data-stu-id="384e2-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="384e2-201">Paket dosyası npm kayıt defteri için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="384e2-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="384e2-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="384e2-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="384e2-203">Implements tabanlı yönlendirme kimliği.</span><span class="sxs-lookup"><span data-stu-id="384e2-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="384e2-204">Sorunu giderir [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -geçerli özellik yöntemi current() ile çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="384e2-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="384e2-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="384e2-206">Jeo-uzamsal dizin desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="384e2-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="384e2-207">ID özelliği tüm kaynaklar için doğrular.</span><span class="sxs-lookup"><span data-stu-id="384e2-207">Validates id property for all resources.</span></span> <span data-ttu-id="384e2-208">Kaynaklar için kimlikleri içeremez?, /, # &#47; &#47; karakter veya boşluk ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="384e2-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="384e2-209">Yeni Üstbilgi "dizini dönüştürme ilerleme durumu" için ResourceResponse ekler.</span><span class="sxs-lookup"><span data-stu-id="384e2-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="384e2-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="384e2-211">V2 dizin oluşturma ilkesini uygular.</span><span class="sxs-lookup"><span data-stu-id="384e2-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="384e2-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="384e2-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="384e2-213">Sorun [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - uygulanan eslint grunt çekirdek yapılandırmalarını ve SDK veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="384e2-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="384e2-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="384e2-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="384e2-215">Sorun [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -öneriler sarmalayıcı hata üstbilgiyle içermez.</span><span class="sxs-lookup"><span data-stu-id="384e2-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="384e2-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="384e2-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="384e2-217">Sorgu readConflicts, readConflictAsync ve queryConflicts ekleyerek çakışmaları için uygulanan yeteneği.</span><span class="sxs-lookup"><span data-stu-id="384e2-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="384e2-218">Güncelleştirilmiş API belgeleri.</span><span class="sxs-lookup"><span data-stu-id="384e2-218">Updated API documentation.</span></span>
* <span data-ttu-id="384e2-219">Sorun [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync hata.</span><span class="sxs-lookup"><span data-stu-id="384e2-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="384e2-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="384e2-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="384e2-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="384e2-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="384e2-222">Yayın & sona erme tarihlerini</span><span class="sxs-lookup"><span data-stu-id="384e2-222">Release & Retirement Dates</span></span>
<span data-ttu-id="384e2-223">Microsoft'un sağladığı bildirim en az **12 ay** yeni/desteklenen bir sürüme geçiş kesintisiz için bir SDK devre dışı bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="384e2-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="384e2-224">Yeni özellikler ve işlevsellik ve en iyi duruma getirme geçerli SDK'sı yalnızca eklenir, bu nedenle, her zaman en son SDK sürüme erken mümkün olduğunca yükseltmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="384e2-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="384e2-225">Kullanımdan Kaldırılan SDK Cosmos DB kullanarak herhangi bir istek hizmeti tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="384e2-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="384e2-226">Sürüm</span><span class="sxs-lookup"><span data-stu-id="384e2-226">Version</span></span> | <span data-ttu-id="384e2-227">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="384e2-227">Release Date</span></span> | <span data-ttu-id="384e2-228">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="384e2-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="384e2-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="384e2-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="384e2-230">10 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="384e2-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="384e2-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="384e2-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="384e2-232">10 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="384e2-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="384e2-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="384e2-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="384e2-234">10 Mayıs 2017</span><span class="sxs-lookup"><span data-stu-id="384e2-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="384e2-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="384e2-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="384e2-236">16 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="384e2-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="384e2-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="384e2-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="384e2-238">27 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="384e2-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="384e2-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="384e2-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="384e2-240">22 aralık 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="384e2-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="384e2-242">03 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="384e2-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="384e2-244">07 Temmuz 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="384e2-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="384e2-246">14 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="384e2-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="384e2-248">26 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="384e2-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="384e2-250">29 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="384e2-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="384e2-252">08 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="384e2-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="384e2-254">02 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="384e2-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="384e2-256">01 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="384e2-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="384e2-258">26 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="384e2-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="384e2-260">22 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="384e2-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="384e2-262">4 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="384e2-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="384e2-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="384e2-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="384e2-264">31 Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="384e2-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="384e2-266">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="384e2-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="384e2-268">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="384e2-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="384e2-270">10 Eylül 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="384e2-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="384e2-272">15 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="384e2-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="384e2-274">05 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="384e2-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="384e2-276">09 Temmuz 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="384e2-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="384e2-278">04 Haziran 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="384e2-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="384e2-280">23 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="384e2-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="384e2-282">15 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="384e2-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="384e2-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="384e2-284">08 Nisan 2015</span><span class="sxs-lookup"><span data-stu-id="384e2-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="384e2-285">SSS</span><span class="sxs-lookup"><span data-stu-id="384e2-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="384e2-286">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="384e2-286">See also</span></span>
<span data-ttu-id="384e2-287">Cosmos DB hakkında daha fazla bilgi için bkz: [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="384e2-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


---
title: "aaaAzure Cosmos DB Node.js API SDK & kaynakları | Microsoft Docs"
description: "Node.js API ve SDK sürüm tarih, sona erme tarihlerini ve her hello Azure Cosmos DB Node.js SDK'sı sürüm arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında bilgi edinin."
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
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="6a98b-103">Azure DB Cosmos Node.js SDK: sürüm notları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="6a98b-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a98b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6a98b-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="6a98b-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="6a98b-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="6a98b-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6a98b-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="6a98b-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a98b-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="6a98b-108">Java</span><span class="sxs-lookup"><span data-stu-id="6a98b-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="6a98b-109">Python</span><span class="sxs-lookup"><span data-stu-id="6a98b-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="6a98b-110">REST</span><span class="sxs-lookup"><span data-stu-id="6a98b-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="6a98b-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="6a98b-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="6a98b-112">SQL</span><span class="sxs-lookup"><span data-stu-id="6a98b-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="6a98b-113">**SDK'sını indirin**</span><span class="sxs-lookup"><span data-stu-id="6a98b-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="6a98b-114">NPM</span><span class="sxs-lookup"><span data-stu-id="6a98b-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="6a98b-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="6a98b-115">**API documentation**</span></span></td><td>[<span data-ttu-id="6a98b-116">Node.js API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="6a98b-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="6a98b-117">**SDK yükleme yönergeleri**</span><span class="sxs-lookup"><span data-stu-id="6a98b-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="6a98b-118">Yükleme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="6a98b-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="6a98b-119">**TooSDK katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="6a98b-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="6a98b-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="6a98b-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="6a98b-121">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="6a98b-121">**Samples**</span></span></td><td>[<span data-ttu-id="6a98b-122">Node.js kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="6a98b-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="6a98b-123">**Başlangıç eğitmeni**</span><span class="sxs-lookup"><span data-stu-id="6a98b-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="6a98b-124">Merhaba Node.js SDK'sı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6a98b-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="6a98b-125">**Web uygulaması Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="6a98b-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="6a98b-126">Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a98b-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="6a98b-127">**Geçerli desteklenen platformlar**</span><span class="sxs-lookup"><span data-stu-id="6a98b-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="6a98b-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="6a98b-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="6a98b-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="6a98b-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="6a98b-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="6a98b-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="6a98b-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="6a98b-132">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6a98b-132">Release notes</span></span>

### <span data-ttu-id="6a98b-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="6a98b-134">Sabit npm belgeleri.</span><span class="sxs-lookup"><span data-stu-id="6a98b-134">npm documentation fixed.</span></span>

### <span data-ttu-id="6a98b-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="6a98b-136">Bir hata, burada ilgili belgelerini özel Unicode karakterler (LS, PS) b executeStoredProcedure içinde sabit.</span><span class="sxs-lookup"><span data-stu-id="6a98b-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="6a98b-137">Merhaba bölüm anahtarı Unicode karakterler içeren belgeleri işlemedeki hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="6a98b-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="6a98b-138">Sabit koleksiyonlar ile Merhaba ad ortamı oluşturma desteği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="6a98b-139">Github sorunu #114.</span><span class="sxs-lookup"><span data-stu-id="6a98b-139">Github issue #114.</span></span>
* <span data-ttu-id="6a98b-140">İzni yetkilendirme belirtecini sabit desteği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="6a98b-141">Github sorunu #178.</span><span class="sxs-lookup"><span data-stu-id="6a98b-141">Github issue #178.</span></span>

### <span data-ttu-id="6a98b-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="6a98b-143">Yeni bir desteği eklendi [tutarlılık düzeyi](consistency-levels.md) ConsistentPrefix çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6a98b-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="6a98b-144">UriFactory desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="6a98b-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="6a98b-145">Unicode desteği hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="6a98b-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="6a98b-146">GitHub sorunu #171.</span><span class="sxs-lookup"><span data-stu-id="6a98b-146">GitHub issue #171.</span></span>

### <span data-ttu-id="6a98b-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="6a98b-148">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi hello.</span><span class="sxs-lookup"><span data-stu-id="6a98b-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="6a98b-149">Çapraz bölüm sorgular için paralellik derecesi denetleme eklenen hello seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="6a98b-150">SSL doğrulama Azure Cosmos DB öykünücüsüne karşı çalıştırırken devre dışı bırakmak için eklenen hello seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="6a98b-151">En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.</span><span class="sxs-lookup"><span data-stu-id="6a98b-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="6a98b-152">Tek bölümlü bir koleksiyon için sabit hello devamlılık belirteci hata.</span><span class="sxs-lookup"><span data-stu-id="6a98b-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="6a98b-153">Github sorunu #107.</span><span class="sxs-lookup"><span data-stu-id="6a98b-153">Github issue #107.</span></span>
* <span data-ttu-id="6a98b-154">0 tek param işlemedeki sabit hello executeStoredProcedure hata.</span><span class="sxs-lookup"><span data-stu-id="6a98b-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="6a98b-155">Github sorunu #155.</span><span class="sxs-lookup"><span data-stu-id="6a98b-155">Github issue #155.</span></span>

### <span data-ttu-id="6a98b-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="6a98b-157">Sabit Kullanıcı Aracısı üstbilgisi tooinclude hello SDK sürümü.</span><span class="sxs-lookup"><span data-stu-id="6a98b-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="6a98b-158">Küçük kod temizleme.</span><span class="sxs-lookup"><span data-stu-id="6a98b-158">Minor code cleanup.</span></span>

### <span data-ttu-id="6a98b-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="6a98b-160">SSL doğrulama hello SDK tootarget hello emulator(hostname=localhost) kullanırken devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="6a98b-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="6a98b-161">Saklı yordam yürütme sırasında betik günlüğünü etkinleştirme için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="6a98b-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="6a98b-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="6a98b-163">Bölüm paralel sorgular çapraz eklenen desteği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="6a98b-164">ÜST/ORDER BY sorguları bölümlenmiş koleksiyonlar için desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="6a98b-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="6a98b-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="6a98b-166">Daraltılmış istekleri için eklenen yeniden deneme ilkesi desteği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="6a98b-167">(Daraltılmış isteklerini bir istek oranı çok büyük özel durumu, hata kodu 429 alır.) Hata kodu 429 karşılaşıldığında, varsayılan olarak, Azure Cosmos DB dokuz kez her istek için uygularken hello retryAfter hello yanıt üstbilgisi sürede yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="6a98b-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="6a98b-168">Merhaba yeniden denemeler arasında sunucu tarafından döndürülen tooignore hello retryAfter zaman istiyorsanız sabit yeniden deneme zaman aralığını şimdi hello RetryOptions özelliğinin bir parçası olarak hello ConnectionPolicy nesne üzerinde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6a98b-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="6a98b-169">Azure Cosmos DB şimdi en fazla (bağımsız olarak yeniden deneme sayısı) kısıtlanan ve 429 hata koduyla hello yanıt döndüren her istek için 30 saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="6a98b-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="6a98b-170">Bu süre ayrıca hello ConnectionPolicy nesnesindeki RetryOptions özelliği geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="6a98b-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="6a98b-171">Cosmos DB şimdi x-ms-kısıtlama-yeniden deneme-sayısı ve x-ms-throttle-retry-wait-time-ms döndürür her isteği toodenote hello kısıtlama Hello yanıt üstbilgileri hello yeniden denemeler arasında beklenen hello isteği sayısını ve hello toplu süre yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6a98b-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="6a98b-172">Merhaba RetryOptions sınıfı eklendi, hello RetryOptions özelliği gösterme kullanılan toooverride olabilir hello ConnectionPolicy sınıfı üzerinde bazı hello varsayılan seçenekleri yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6a98b-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="6a98b-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="6a98b-174">Eklenen hello bölgeli veritabanı hesaplarını desteği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="6a98b-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="6a98b-176">Eklenen hello zamanı tooLive(TTL) özelliğini belgeler için destek.</span><span class="sxs-lookup"><span data-stu-id="6a98b-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="6a98b-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="6a98b-178">Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6a98b-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="6a98b-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="6a98b-180">Burada, bağlantılar tooa hatalı concat sonuçlarının son döndürdü değil sabit RangePartitionResolver.resolveForRead hata.</span><span class="sxs-lookup"><span data-stu-id="6a98b-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="6a98b-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="6a98b-182">HashParitionResolver resolveForRead() sabit: ne zaman sağlanan hiçbir bölüm anahtarı atma tüm kayıtlı bağlantıların listesini döndürme yerine bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="6a98b-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="6a98b-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="6a98b-184">Sorunu giderir [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -ayrılmış HTTPS aracısı: hello genel Aracısı Azure Cosmos DB amacıyla değiştirme kaçının.</span><span class="sxs-lookup"><span data-stu-id="6a98b-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="6a98b-185">Ayrılmış bir aracı tüm hello lib'ın istekleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a98b-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="6a98b-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="6a98b-187">Sorunu giderir [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - düzgün işleyecek medya kimlikleri tire.</span><span class="sxs-lookup"><span data-stu-id="6a98b-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="6a98b-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="6a98b-189">Sorunu giderir [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -EventEmitter dinleyicisi sızıntısı uyarı.</span><span class="sxs-lookup"><span data-stu-id="6a98b-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="6a98b-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="6a98b-191">Sorunu giderir [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -klasör karma toohash büyük küçük harfe duyarlı sistemler için yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="6a98b-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="6a98b-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="6a98b-193">Karma & aralığı bölüm çözümleyiciler ekleyerek parçalama destek uygular.</span><span class="sxs-lookup"><span data-stu-id="6a98b-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="6a98b-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="6a98b-195">Upsert uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6a98b-195">Implement Upsert.</span></span> <span data-ttu-id="6a98b-196">DocumentClient yeni upsertXXX yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="6a98b-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="6a98b-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="6a98b-198">Diğer SDK ile hizalama toobring sürüm numaraları atlandı.</span><span class="sxs-lookup"><span data-stu-id="6a98b-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="6a98b-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="6a98b-200">Bölünmüş Q sarmalayıcı toonew depo taahhüt eder.</span><span class="sxs-lookup"><span data-stu-id="6a98b-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="6a98b-201">Npm kayıt defteri toopackage dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6a98b-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="6a98b-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="6a98b-203">Implements tabanlı yönlendirme kimliği.</span><span class="sxs-lookup"><span data-stu-id="6a98b-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="6a98b-204">Sorunu giderir [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -geçerli özellik yöntemi current() ile çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="6a98b-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="6a98b-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="6a98b-206">Jeo-uzamsal dizin desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="6a98b-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="6a98b-207">ID özelliği tüm kaynaklar için doğrular.</span><span class="sxs-lookup"><span data-stu-id="6a98b-207">Validates id property for all resources.</span></span> <span data-ttu-id="6a98b-208">Kaynaklar için kimlikleri içeremez?, /, # &#47; &#47; karakter veya boşluk ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="6a98b-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="6a98b-209">Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.</span><span class="sxs-lookup"><span data-stu-id="6a98b-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="6a98b-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="6a98b-211">V2 dizin oluşturma ilkesini uygular.</span><span class="sxs-lookup"><span data-stu-id="6a98b-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="6a98b-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="6a98b-213">Sorun [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - uygulanan eslint grunt hello çekirdek yapılandırmalarını ve SDK veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="6a98b-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="6a98b-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="6a98b-215">Sorun [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -öneriler sarmalayıcı hata üstbilgiyle içermez.</span><span class="sxs-lookup"><span data-stu-id="6a98b-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="6a98b-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="6a98b-217">Çakışmaları özelliği tooquery readConflicts, readConflictAsync ve queryConflicts ekleyerek uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="6a98b-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="6a98b-218">Güncelleştirilmiş API belgeleri.</span><span class="sxs-lookup"><span data-stu-id="6a98b-218">Updated API documentation.</span></span>
* <span data-ttu-id="6a98b-219">Sorun [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync hata.</span><span class="sxs-lookup"><span data-stu-id="6a98b-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="6a98b-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="6a98b-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="6a98b-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="6a98b-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="6a98b-222">Yayın & sona erme tarihlerini</span><span class="sxs-lookup"><span data-stu-id="6a98b-222">Release & Retirement Dates</span></span>
<span data-ttu-id="6a98b-223">Microsoft'un sağladığı bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="6a98b-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="6a98b-224">Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle önerilir, her zaman yükseltme toohello en son SDK sürümünün olabildiğince erken.</span><span class="sxs-lookup"><span data-stu-id="6a98b-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="6a98b-225">TooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB olan herhangi bir istek hello hizmeti tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="6a98b-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="6a98b-226">Sürüm</span><span class="sxs-lookup"><span data-stu-id="6a98b-226">Version</span></span> | <span data-ttu-id="6a98b-227">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="6a98b-227">Release Date</span></span> | <span data-ttu-id="6a98b-228">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="6a98b-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="6a98b-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="6a98b-230">10 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="6a98b-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="6a98b-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="6a98b-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="6a98b-232">10 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="6a98b-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="6a98b-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="6a98b-234">10 Mayıs 2017</span><span class="sxs-lookup"><span data-stu-id="6a98b-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="6a98b-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="6a98b-236">16 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="6a98b-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="6a98b-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="6a98b-238">27 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="6a98b-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="6a98b-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="6a98b-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="6a98b-240">22 aralık 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="6a98b-242">03 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="6a98b-244">07 Temmuz 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="6a98b-246">14 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="6a98b-248">26 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="6a98b-250">29 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="6a98b-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="6a98b-252">08 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="6a98b-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="6a98b-254">02 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="6a98b-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="6a98b-256">01 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="6a98b-258">26 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="6a98b-260">22 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="6a98b-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="6a98b-262">4 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="6a98b-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="6a98b-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="6a98b-264">31 Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="6a98b-266">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="6a98b-268">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="6a98b-270">10 Eylül 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="6a98b-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="6a98b-272">15 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="6a98b-274">05 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="6a98b-276">09 Temmuz 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="6a98b-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="6a98b-278">04 Haziran 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="6a98b-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="6a98b-280">23 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="6a98b-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="6a98b-282">15 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="6a98b-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="6a98b-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="6a98b-284">08 Nisan 2015</span><span class="sxs-lookup"><span data-stu-id="6a98b-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="6a98b-285">SSS</span><span class="sxs-lookup"><span data-stu-id="6a98b-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="6a98b-286">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6a98b-286">See also</span></span>
<span data-ttu-id="6a98b-287">toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="6a98b-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


---
title: "Azure Cosmos DB: DocumentDB Java API, SDK & kaynakları | Microsoft Docs"
description: "Java API ve SDK sürüm tarih, sona erme tarihlerini ve her hello Azure Cosmos DB DocumentDB Java SDK'sı sürüm arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında bilgi edinin."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="b0061-103">Azure Cosmos DB: DocumentDB Java SDK'sı sürüm notları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="b0061-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0061-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b0061-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="b0061-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="b0061-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="b0061-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b0061-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="b0061-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="b0061-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="b0061-108">Java</span><span class="sxs-lookup"><span data-stu-id="b0061-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="b0061-109">Python</span><span class="sxs-lookup"><span data-stu-id="b0061-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="b0061-110">REST</span><span class="sxs-lookup"><span data-stu-id="b0061-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="b0061-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="b0061-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="b0061-112">SQL</span><span class="sxs-lookup"><span data-stu-id="b0061-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="b0061-113">**SDK yükleme**</span><span class="sxs-lookup"><span data-stu-id="b0061-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="b0061-114">Maven</span><span class="sxs-lookup"><span data-stu-id="b0061-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="b0061-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="b0061-115">**API documentation**</span></span></td><td>[<span data-ttu-id="b0061-116">Java API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="b0061-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="b0061-117">**TooSDK katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="b0061-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="b0061-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="b0061-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="b0061-119">**Kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="b0061-119">**Get started**</span></span></td><td>[<span data-ttu-id="b0061-120">Merhaba Java SDK'sı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b0061-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="b0061-121">**Web uygulaması Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="b0061-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="b0061-122">Azure Cosmos DB ile Web uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="b0061-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="b0061-123">**Geçerli desteklenen çalışma zamanı**</span><span class="sxs-lookup"><span data-stu-id="b0061-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="b0061-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="b0061-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b0061-125">Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="b0061-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="b0061-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="b0061-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="b0061-127">Kritik hata düzeltmeleri toorequest sırasında bölümü işlemeye böler.</span><span class="sxs-lookup"><span data-stu-id="b0061-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="b0061-128">Hello güçlü ve BoundedStaleness tutarlılık düzeyleri ile ilgili bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0061-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="b0061-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="b0061-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="b0061-130">Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b0061-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="b0061-131">Oturum modu koleksiyonunda okuma hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="b0061-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="b0061-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="b0061-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="b0061-133">Etkin bölümlenmiş koleksiyonuyla desteği 2.500 RU/sn düşük ve 100 RU/sn artışlarla ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="b0061-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="b0061-134">Bir hata NullRef özel bazı sorgular neden hello yerel derleme sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="b0061-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="b0061-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="b0061-136">Merhaba sorgu altyapısı yapılandırmasında sorguları için özel durumlar ağ geçidi modunda neden olabilecek bir hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="b0061-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="b0061-137">"Sahip kaynak bulunamadı" için bir özel durum isteklerinin koleksiyonu oluşturulduktan hemen sonra neden olabilecek hello oturum kapsayıcısında birkaç düzeltilen.</span><span class="sxs-lookup"><span data-stu-id="b0061-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="b0061-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="b0061-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="b0061-139">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="b0061-140">Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="b0061-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="b0061-141">Akış değişiklik desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-141">Added support for change feed.</span></span>
* <span data-ttu-id="b0061-142">Koleksiyon kota bilgileri RequestOptions.setPopulateQuotaInfo aracılığıyla desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="b0061-143">Saklı yordam komut dosyası günlük RequestOptions.setScriptLoggingEnabled aracılığıyla desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="b0061-144">Kısıtlama hataları karşılaşıldığında DirectHttps modunda sorgu burada kilitlenebilir hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="b0061-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="b0061-145">Bir hatayı oturum tutarlılığı modunda sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="b0061-146">İstek oranı yüksek olduğunda bu NullReferenceException içinde HttpContext neden olabilecek bir hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="b0061-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="b0061-147">DirectHttps modu performansı geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="b0061-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="b0061-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="b0061-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="b0061-149">ConnectionPolicy.setProxy() API ile eklenen basit istemci örnek tabanlı proxy desteği.</span><span class="sxs-lookup"><span data-stu-id="b0061-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="b0061-150">Eklenen DocumentClient.close() API tooproperly kapatma DocumentClient örneği.</span><span class="sxs-lookup"><span data-stu-id="b0061-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="b0061-151">İyileştirilmiş sorgu performansı hello yerel derleme hello ağ geçidi yerine hello sorgu planı türetme tarafından doğrudan bağlantı modunda.</span><span class="sxs-lookup"><span data-stu-id="b0061-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="b0061-152">Ayarlama FAIL_ON_UNKNOWN_PROPERTIES böylece kullanıcılar kendi POJO'ya JsonIgnoreProperties toodefine = false.</span><span class="sxs-lookup"><span data-stu-id="b0061-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="b0061-153">Günlük toouse SLF4J bulunanad.</span><span class="sxs-lookup"><span data-stu-id="b0061-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="b0061-154">Birkaç diğer tutarlılık okuyucusunda düzeltilen.</span><span class="sxs-lookup"><span data-stu-id="b0061-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="b0061-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="b0061-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="b0061-156">Bir hata hello bağlantı yönetimi tooprevent bağlantı sızıntıları doğrudan bağlantı modunda sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="b0061-157">Bir hata, burada NullReferenece özel durum atabilir hello üst sorguda sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="b0061-158">Merhaba iç önbellekler için ağ çağrısı hello sayısını azaltarak performansı.</span><span class="sxs-lookup"><span data-stu-id="b0061-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="b0061-159">Eklenen durum kodu, ActivityID ve daha iyi sorun giderme için DocumentClientException, istek URI'si.</span><span class="sxs-lookup"><span data-stu-id="b0061-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="b0061-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="b0061-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="b0061-161">Merhaba bağlantı yönetiminde kararlılık için bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0061-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="b0061-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="b0061-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="b0061-163">BoundedStaleness tutarlılık düzeyi desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="b0061-164">Bölümlenmiş koleksiyonlar için CRUD işlemleri için doğrudan bağlantı desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="b0061-165">SQL veritabanıyla sorgulama içinde hatanın düzeltildiğini.</span><span class="sxs-lookup"><span data-stu-id="b0061-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="b0061-166">Bir hata burada oturum belirteci yanlış ayarlanmış olabilir hello oturumu önbelleğinde sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="b0061-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="b0061-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="b0061-168">Bölüm paralel sorgular çapraz eklenen desteği.</span><span class="sxs-lookup"><span data-stu-id="b0061-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="b0061-169">ÜST/ORDER BY sorguları bölümlenmiş koleksiyonlar için desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="b0061-170">Güçlü tutarlılık desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="b0061-171">Doğrudan bağlantı kullanırken ad tabanlı istekleri için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="b0061-172">Sabit toomake ActivityID kalmak tutarlı tüm istek yeniden denemeler arasında.</span><span class="sxs-lookup"><span data-stu-id="b0061-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="b0061-173">Hatanın düzeltildiğini hello koleksiyonuyla yeniden zaman toohello oturum önbelleğini ilgili aynı adı.</span><span class="sxs-lookup"><span data-stu-id="b0061-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="b0061-174">Eklenen Çokgen ve LineString İlkesi coğrafı uzamsal sorguları için dizin oluşturma koleksiyonunu belirten sırasında veri türleri.</span><span class="sxs-lookup"><span data-stu-id="b0061-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="b0061-175">Giderilen sorunlar Java 1.8 için Java belge ile.</span><span class="sxs-lookup"><span data-stu-id="b0061-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="b0061-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="b0061-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="b0061-177">İçinde PartitionKeyDefinitionMap hatanın düzeltildiğini toocache tek bölüm koleksiyonları ve değil fazladan yapma anahtar istekleri bölüm getirin.</span><span class="sxs-lookup"><span data-stu-id="b0061-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="b0061-178">Yanlış bölüm anahtarı değerini sağlandığında hata toonot yeniden sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="b0061-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="b0061-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="b0061-180">Eklenen hello bölgeli veritabanı hesaplarını desteği.</span><span class="sxs-lookup"><span data-stu-id="b0061-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="b0061-181">Otomatik yeniden deneme seçeneklerini toocustomize hello en fazla ile daraltılmış isteklerde desteği eklendi yeniden deneme sayısı ve en fazla yeniden deneme bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="b0061-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="b0061-182">RetryOptions ve ConnectionPolicy.getRetryOptions() bakın.</span><span class="sxs-lookup"><span data-stu-id="b0061-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="b0061-183">Kullanım dışı IPartitionResolver özel bölümleme kod tabanlı.</span><span class="sxs-lookup"><span data-stu-id="b0061-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="b0061-184">Lütfen bölümlenmiş koleksiyonlar, daha yüksek depolama ve işleme için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0061-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="b0061-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="b0061-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="b0061-186">Azaltma için eklenen yeniden deneme ilkesi desteği.</span><span class="sxs-lookup"><span data-stu-id="b0061-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="b0061-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="b0061-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="b0061-188">Belgeler için zaman toolive (TTL) desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="b0061-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="b0061-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="b0061-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="b0061-190">Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b0061-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="b0061-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="b0061-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="b0061-192">Bir hata HashPartitionResolver toogenerate karma değerleri little endian toobe diğer SDK'ları ile tutarlı sabit.</span><span class="sxs-lookup"><span data-stu-id="b0061-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="b0061-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="b0061-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="b0061-194">Karma & aralığı Ekle Bölüm çözümleyiciler tooassist birden çok bölüm arasında parçalama uygulamalarla.</span><span class="sxs-lookup"><span data-stu-id="b0061-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="b0061-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="b0061-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="b0061-196">Upsert uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b0061-196">Implement Upsert.</span></span> <span data-ttu-id="b0061-197">Yeni upsertXXX yöntemler toosupport Upsert özellik eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="b0061-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="b0061-198">Temel kimlik yönlendirme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b0061-198">Implement ID Based Routing.</span></span> <span data-ttu-id="b0061-199">Genel API değişiklik, tüm değişiklikleri iç.</span><span class="sxs-lookup"><span data-stu-id="b0061-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="b0061-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="b0061-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="b0061-201">Yayın toobring sürüm numarası diğer SDK ile hizalama atlandı</span><span class="sxs-lookup"><span data-stu-id="b0061-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="b0061-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="b0061-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="b0061-203">Destekler Jeo-uzamsal dizin</span><span class="sxs-lookup"><span data-stu-id="b0061-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="b0061-204">ID özelliği tüm kaynaklar için doğrular.</span><span class="sxs-lookup"><span data-stu-id="b0061-204">Validates id property for all resources.</span></span> <span data-ttu-id="b0061-205">Kaynaklar için kimlikleri içeremez?, /, #, \, karakter veya boşluk ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="b0061-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="b0061-206">Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.</span><span class="sxs-lookup"><span data-stu-id="b0061-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="b0061-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="b0061-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="b0061-208">V2 dizin oluşturma ilkesini uygular</span><span class="sxs-lookup"><span data-stu-id="b0061-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b0061-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b0061-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="b0061-210">GA SDK'SI</span><span class="sxs-lookup"><span data-stu-id="b0061-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="b0061-211">Yayın & sona erme tarihlerini</span><span class="sxs-lookup"><span data-stu-id="b0061-211">Release & Retirement Dates</span></span>
<span data-ttu-id="b0061-212">Microsoft sağlayacaktır bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="b0061-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="b0061-213">Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle olduğundan bu, her zaman yükseltme toohello son SDK sürümü olabildiğince erken öneririz.</span><span class="sxs-lookup"><span data-stu-id="b0061-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="b0061-214">Tüm istek tooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="b0061-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="b0061-215">Java önceki tooversion Merhaba DocumentDB SDK'in tüm sürümleri **1.0.0** üzerinde Çekildi **29 Şubat 2016**.</span><span class="sxs-lookup"><span data-stu-id="b0061-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="b0061-216">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b0061-216">Version</span></span> | <span data-ttu-id="b0061-217">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="b0061-217">Release Date</span></span> | <span data-ttu-id="b0061-218">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="b0061-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b0061-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="b0061-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="b0061-220">11 Temmuz 2017</span><span class="sxs-lookup"><span data-stu-id="b0061-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="b0061-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="b0061-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="b0061-222">10 Mayıs 2017</span><span class="sxs-lookup"><span data-stu-id="b0061-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="b0061-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="b0061-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="b0061-224">11 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="b0061-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="b0061-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="b0061-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="b0061-226">21 Şubat 2017</span><span class="sxs-lookup"><span data-stu-id="b0061-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="b0061-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="b0061-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="b0061-228">31 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="b0061-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="b0061-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="b0061-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="b0061-230">24 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="b0061-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="b0061-232">30 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="b0061-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="b0061-234">28 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="b0061-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="b0061-236">26 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="b0061-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="b0061-238">03 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="b0061-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="b0061-240">30 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="b0061-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="b0061-242">14 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="b0061-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="b0061-244">30 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="b0061-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="b0061-246">27 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="b0061-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="b0061-248">29 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="b0061-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="b0061-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="b0061-250">31 Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="b0061-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="b0061-252">04 Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="b0061-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="b0061-254">05 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="b0061-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="b0061-256">05 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b0061-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="b0061-258">05 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b0061-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="b0061-260">09 Temmuz 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="b0061-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="b0061-262">12 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="b0061-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b0061-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b0061-264">07 Nisan 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="b0061-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-265">0.9.5-prelease</span></span> |<span data-ttu-id="b0061-266">09 Mar 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-266">Mar 09, 2015</span></span> |<span data-ttu-id="b0061-267">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-267">February 29, 2016</span></span> |
| <span data-ttu-id="b0061-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-268">0.9.4-prelease</span></span> |<span data-ttu-id="b0061-269">17 Şubat 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-269">February 17, 2015</span></span> |<span data-ttu-id="b0061-270">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-270">February 29, 2016</span></span> |
| <span data-ttu-id="b0061-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-271">0.9.3-prelease</span></span> |<span data-ttu-id="b0061-272">13 Ocak 2015</span><span class="sxs-lookup"><span data-stu-id="b0061-272">January 13, 2015</span></span> |<span data-ttu-id="b0061-273">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-273">February 29, 2016</span></span> |
| <span data-ttu-id="b0061-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-274">0.9.2-prelease</span></span> |<span data-ttu-id="b0061-275">19 Aralık 2014</span><span class="sxs-lookup"><span data-stu-id="b0061-275">December 19, 2014</span></span> |<span data-ttu-id="b0061-276">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-276">February 29, 2016</span></span> |
| <span data-ttu-id="b0061-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-277">0.9.1-prelease</span></span> |<span data-ttu-id="b0061-278">19 Aralık 2014</span><span class="sxs-lookup"><span data-stu-id="b0061-278">December 19, 2014</span></span> |<span data-ttu-id="b0061-279">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-279">February 29, 2016</span></span> |
| <span data-ttu-id="b0061-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="b0061-280">0.9.0-prelease</span></span> |<span data-ttu-id="b0061-281">10 Aralık 2014</span><span class="sxs-lookup"><span data-stu-id="b0061-281">December 10, 2014</span></span> |<span data-ttu-id="b0061-282">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="b0061-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="b0061-283">SSS</span><span class="sxs-lookup"><span data-stu-id="b0061-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="b0061-284">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b0061-284">See Also</span></span>
<span data-ttu-id="b0061-285">toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="b0061-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


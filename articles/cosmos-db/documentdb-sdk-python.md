---
title: "aaaAzure Cosmos DB Python API SDK & kaynakları | Microsoft Docs"
description: "Python API ve SDK sürüm tarih, sona erme tarihlerini ve her hello Azure Cosmos DB Python SDK'sı sürüm arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında öğrenin."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="59d0d-103">Azure DB Cosmos Python SDK: sürüm notları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="59d0d-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59d0d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="59d0d-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="59d0d-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="59d0d-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="59d0d-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="59d0d-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="59d0d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="59d0d-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="59d0d-108">Java</span><span class="sxs-lookup"><span data-stu-id="59d0d-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="59d0d-109">Python</span><span class="sxs-lookup"><span data-stu-id="59d0d-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="59d0d-110">REST</span><span class="sxs-lookup"><span data-stu-id="59d0d-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="59d0d-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="59d0d-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="59d0d-112">SQL</span><span class="sxs-lookup"><span data-stu-id="59d0d-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="59d0d-113">**SDK'sını indirin**</span><span class="sxs-lookup"><span data-stu-id="59d0d-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="59d0d-114">Pypı</span><span class="sxs-lookup"><span data-stu-id="59d0d-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="59d0d-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="59d0d-115">**API documentation**</span></span></td><td>[<span data-ttu-id="59d0d-116">Python API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="59d0d-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="59d0d-117">**SDK yükleme yönergeleri**</span><span class="sxs-lookup"><span data-stu-id="59d0d-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="59d0d-118">Python SDK yükleme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="59d0d-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="59d0d-119">**TooSDK katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="59d0d-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="59d0d-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="59d0d-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="59d0d-121">**Kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="59d0d-121">**Get started**</span></span></td><td>[<span data-ttu-id="59d0d-122">Merhaba Python SDK'sı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="59d0d-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="59d0d-123">**Geçerli desteklenen platformlar**</span><span class="sxs-lookup"><span data-stu-id="59d0d-123">**Current supported platform**</span></span></td><td><span data-ttu-id="59d0d-124">[Python 2.7](https://www.python.org/downloads/) ve [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="59d0d-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="59d0d-125">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="59d0d-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="59d0d-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="59d0d-127">Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.</span><span class="sxs-lookup"><span data-stu-id="59d0d-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="59d0d-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="59d0d-129">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="59d0d-130">SSL doğrulama Cosmos DB öykünücüsüne karşı çalıştırırken devre dışı bırakmak için bir seçenek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="59d0d-131">Bağımlı istekleri modülü toobe tam olarak 2.10.0 Hello kısıtlamasını kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="59d0d-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="59d0d-132">En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.</span><span class="sxs-lookup"><span data-stu-id="59d0d-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="59d0d-133">Saklı yordam yürütme sırasında betik günlüğünü etkinleştirme için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="59d0d-134">REST API sürümü indirgenmesine çok ' 2017-01-19' Bu sürümde.</span><span class="sxs-lookup"><span data-stu-id="59d0d-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="59d0d-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="59d0d-136">Toodocumentation açıklamaları düzenleme değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="59d0d-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="59d0d-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="59d0d-138">Python 3.5 desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="59d0d-139">İstekleri modülünü kullanarak bağlantı havuzu için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="59d0d-140">Oturum tutarlılığı desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-140">Added support for session consistency.</span></span>
* <span data-ttu-id="59d0d-141">Bölümlenmiş koleksiyonlar için üst/ORDERBY sorgular için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="59d0d-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="59d0d-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="59d0d-143">Daraltılmış istekleri için eklenen yeniden deneme ilkesi desteği.</span><span class="sxs-lookup"><span data-stu-id="59d0d-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="59d0d-144">(Daraltılmış isteklerini bir istek oranı çok büyük özel durumu, hata kodu 429 alır.) Hata kodu 429 karşılaşıldığında, varsayılan olarak, Azure Cosmos DB dokuz kez her istek için uygularken hello retryAfter hello yanıt üstbilgisi sürede yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="59d0d-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="59d0d-145">Merhaba yeniden denemeler arasında sunucu tarafından döndürülen tooignore hello retryAfter zaman istiyorsanız sabit yeniden deneme zaman aralığını şimdi hello RetryOptions özelliğinin bir parçası olarak hello ConnectionPolicy nesne üzerinde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="59d0d-146">Azure Cosmos DB şimdi en fazla (bağımsız olarak yeniden deneme sayısı) kısıtlanan ve 429 hata koduyla hello yanıt döndüren her istek için 30 saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="59d0d-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="59d0d-147">Bu süre hello ConnectionPolicy nesnesindeki RetryOptions özelliği kılınmadı de olabilir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="59d0d-148">Cosmos DB şimdi x-ms-kısıtlama-yeniden deneme-sayısı ve x-ms-throttle-retry-wait-time-ms döndürür her isteği toodenote hello kısıtlama Hello yanıt üstbilgileri hello yeniden denemeler arasında beklenen hello isteği sayısını ve hello cummulative süre yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="59d0d-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="59d0d-149">Kaldırılan hello RetryPolicy sınıfı ve hello karşılık gelen özelliği (retry_policy) hello document_client sınıfında gösterilir ve bunun yerine hello RetryOptions kullanılan toooverride olabilir ConnectionPolicy sınıfı özellikte gösterme RetryOptions sınıfı sunulan Bazı hello varsayılan seçenekleri yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="59d0d-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="59d0d-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="59d0d-151">Eklenen hello bölgeli veritabanı hesaplarını desteği.</span><span class="sxs-lookup"><span data-stu-id="59d0d-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="59d0d-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="59d0d-153">Eklenen hello zamanı tooLive(TTL) özelliğini belgeler için destek.</span><span class="sxs-lookup"><span data-stu-id="59d0d-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="59d0d-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="59d0d-155">Hata düzeltmeleri partitionkey yolundaki tooallow özel karakterlerin bölümleme tooserver yan ilgili.</span><span class="sxs-lookup"><span data-stu-id="59d0d-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="59d0d-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="59d0d-157">Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="59d0d-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="59d0d-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="59d0d-159">Karma & aralığı Ekle Bölüm çözümleyiciler tooassist birden çok bölüm arasında parçalama uygulamalarla.</span><span class="sxs-lookup"><span data-stu-id="59d0d-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="59d0d-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="59d0d-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="59d0d-161">Upsert uygulayın.</span><span class="sxs-lookup"><span data-stu-id="59d0d-161">Implement Upsert.</span></span> <span data-ttu-id="59d0d-162">Yeni UpsertXXX yöntemler toosupport Upsert özellik eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="59d0d-163">Temel kimlik yönlendirme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="59d0d-163">Implement ID Based Routing.</span></span> <span data-ttu-id="59d0d-164">Genel API değişiklik, tüm değişiklikleri iç.</span><span class="sxs-lookup"><span data-stu-id="59d0d-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="59d0d-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="59d0d-166">Jeo-uzamsal dizin destekler.</span><span class="sxs-lookup"><span data-stu-id="59d0d-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="59d0d-167">ID özelliği tüm kaynaklar için doğrular.</span><span class="sxs-lookup"><span data-stu-id="59d0d-167">Validates id property for all resources.</span></span> <span data-ttu-id="59d0d-168">Kaynaklar için kimlikleri içeremez?, /, #, \, karakter veya boşluk ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="59d0d-169">Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.</span><span class="sxs-lookup"><span data-stu-id="59d0d-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="59d0d-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="59d0d-171">V2 dizin oluşturma ilkesini uygular.</span><span class="sxs-lookup"><span data-stu-id="59d0d-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="59d0d-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="59d0d-173">Proxy bağlantı destekler.</span><span class="sxs-lookup"><span data-stu-id="59d0d-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="59d0d-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="59d0d-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="59d0d-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="59d0d-176">Yayın & sona erme tarihleri</span><span class="sxs-lookup"><span data-stu-id="59d0d-176">Release & retirement dates</span></span>
<span data-ttu-id="59d0d-177">Microsoft sağlayacaktır bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="59d0d-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="59d0d-178">Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle olduğundan bu, her zaman yükseltme toohello son SDK sürümü olabildiğince erken öneririz.</span><span class="sxs-lookup"><span data-stu-id="59d0d-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="59d0d-179">Tüm istek tooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="59d0d-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="59d0d-180">Python önceki tooversion Merhaba Azure DocumentDB SDK'in tüm sürümleri **1.0.0** üzerinde Çekildi **29 Şubat 2016**.</span><span class="sxs-lookup"><span data-stu-id="59d0d-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="59d0d-181">Sürüm</span><span class="sxs-lookup"><span data-stu-id="59d0d-181">Version</span></span> | <span data-ttu-id="59d0d-182">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="59d0d-182">Release Date</span></span> | <span data-ttu-id="59d0d-183">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="59d0d-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="59d0d-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="59d0d-185">10 Mayıs 2017</span><span class="sxs-lookup"><span data-stu-id="59d0d-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="59d0d-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="59d0d-187">01 May 2017</span><span class="sxs-lookup"><span data-stu-id="59d0d-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="59d0d-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="59d0d-189">30 Ekim 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="59d0d-191">29 Eylül 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="59d0d-193">07 Temmuz 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="59d0d-195">14 Haziran 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="59d0d-197">26 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="59d0d-199">08 Nisan 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="59d0d-201">29 Mart 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="59d0d-203">03 Ocak 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="59d0d-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="59d0d-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="59d0d-205">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="59d0d-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="59d0d-207">06 Ekim 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="59d0d-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="59d0d-209">06 Ağustos 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="59d0d-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="59d0d-211">09 Temmuz 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="59d0d-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="59d0d-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="59d0d-213">25 Mayıs 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="59d0d-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="59d0d-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="59d0d-215">07 Nisan 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="59d0d-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="59d0d-216">0.9.4-prelease</span></span> |<span data-ttu-id="59d0d-217">14 Ocak 2015</span><span class="sxs-lookup"><span data-stu-id="59d0d-217">January 14, 2015</span></span> |<span data-ttu-id="59d0d-218">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-218">February 29, 2016</span></span> |
| <span data-ttu-id="59d0d-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="59d0d-219">0.9.3-prelease</span></span> |<span data-ttu-id="59d0d-220">09 aralık 2014</span><span class="sxs-lookup"><span data-stu-id="59d0d-220">December 09, 2014</span></span> |<span data-ttu-id="59d0d-221">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-221">February 29, 2016</span></span> |
| <span data-ttu-id="59d0d-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="59d0d-222">0.9.2-prelease</span></span> |<span data-ttu-id="59d0d-223">25 Kasım 2014</span><span class="sxs-lookup"><span data-stu-id="59d0d-223">November 25, 2014</span></span> |<span data-ttu-id="59d0d-224">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-224">February 29, 2016</span></span> |
| <span data-ttu-id="59d0d-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="59d0d-225">0.9.1-prelease</span></span> |<span data-ttu-id="59d0d-226">23 Eylül 2014</span><span class="sxs-lookup"><span data-stu-id="59d0d-226">September 23, 2014</span></span> |<span data-ttu-id="59d0d-227">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-227">February 29, 2016</span></span> |
| <span data-ttu-id="59d0d-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="59d0d-228">0.9.0-prelease</span></span> |<span data-ttu-id="59d0d-229">21 Ağustos 2014</span><span class="sxs-lookup"><span data-stu-id="59d0d-229">August 21, 2014</span></span> |<span data-ttu-id="59d0d-230">29 Şubat 2016</span><span class="sxs-lookup"><span data-stu-id="59d0d-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="59d0d-231">SSS</span><span class="sxs-lookup"><span data-stu-id="59d0d-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="59d0d-232">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="59d0d-232">See also</span></span>
<span data-ttu-id="59d0d-233">toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="59d0d-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


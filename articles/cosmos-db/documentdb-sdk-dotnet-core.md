---
title: "Azure Cosmos DB .NET Core API, SDK & kaynakları | Microsoft Docs"
description: ".NET Core API ve yayın tarih, sona erme tarihlerini ve her Azure Cosmos DB .NET Core SDK sürümü arasında yapılan değişiklikler dahil olmak üzere SDK'sı hakkında bilgi edinin."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="ae03d-103">Azure Cosmos DB .NET Core SDK: sürüm notları ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="ae03d-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae03d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ae03d-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="ae03d-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="ae03d-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="ae03d-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ae03d-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="ae03d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="ae03d-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="ae03d-108">Java</span><span class="sxs-lookup"><span data-stu-id="ae03d-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="ae03d-109">Python</span><span class="sxs-lookup"><span data-stu-id="ae03d-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="ae03d-110">REST</span><span class="sxs-lookup"><span data-stu-id="ae03d-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="ae03d-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ae03d-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="ae03d-112">SQL</span><span class="sxs-lookup"><span data-stu-id="ae03d-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="ae03d-113">**SDK yükleme**</span><span class="sxs-lookup"><span data-stu-id="ae03d-113">**SDK download**</span></span></td><td>[<span data-ttu-id="ae03d-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="ae03d-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="ae03d-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="ae03d-115">**API documentation**</span></span></td><td>[<span data-ttu-id="ae03d-116">.NET API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="ae03d-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="ae03d-117">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ae03d-117">**Samples**</span></span></td><td>[<span data-ttu-id="ae03d-118">.NET kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="ae03d-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="ae03d-119">**Kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="ae03d-119">**Get started**</span></span></td><td>[<span data-ttu-id="ae03d-120">Azure Cosmos DB .NET Core SDK ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ae03d-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="ae03d-121">**Web uygulaması Öğreticisi**</span><span class="sxs-lookup"><span data-stu-id="ae03d-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="ae03d-122">Azure Cosmos DB ile Web uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="ae03d-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="ae03d-123">**Geçerli desteklenen çerçevelerden**</span><span class="sxs-lookup"><span data-stu-id="ae03d-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="ae03d-124">.NET standart 1.6 ve standart 1.5</span><span class="sxs-lookup"><span data-stu-id="ae03d-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="ae03d-125">Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="ae03d-125">Release Notes</span></span>

<span data-ttu-id="ae03d-126">Özellik eşliği en son sürümü ile Azure Cosmos DB .NET Core SDK sahip [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ae03d-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="ae03d-127">Azure Cosmos DB .NET Core SDK henüz Evrensel Windows Platformu (UWP) uygulamaları ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="ae03d-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="ae03d-128">.NET Core UWP uygulamaları destekleyen SDK'ın ilgileniyorsanız, e-posta Gönder [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ae03d-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="ae03d-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="ae03d-130">Sorgu Sonuçları belirli bir bölüm anahtarı aralığının değerine kapsamı için bir FeedOption olarak PartitionKeyRangeId desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="ae03d-131">Bundan sonra değişikliklerin aramaya başlamak için bir ChangeFeedOption olarak StartTime desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="ae03d-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="ae03d-133">Bir yığın taşması özel durumu neden olabilir JsonSerializable sınıfında bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ae03d-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="ae03d-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="ae03d-135">Örnek oluşturma sırasında özel JsonSerializerSettings belirtmek için destek eklenmiştir bir [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) örneği.</span><span class="sxs-lookup"><span data-stu-id="ae03d-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="ae03d-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="ae03d-137">.NET standart 1.5 tek bir hedef çerçeve olarak destekleme.</span><span class="sxs-lookup"><span data-stu-id="ae03d-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="ae03d-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="ae03d-139">X64 etkilenen bir sorun sabit olmayan SSE4 yönerge destekleyen ve Azure Cosmos DB sorgu çalıştırırken SEHException throw makineler.</span><span class="sxs-lookup"><span data-stu-id="ae03d-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="ae03d-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="ae03d-141">Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ae03d-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="ae03d-142">Tek tek bölümler için sorgu ölçümleri desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="ae03d-143">Sorgular için devamlılık belirteci boyutunu sınırlamak için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="ae03d-144">Başarısız istekler için ayrıntılı izleme desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="ae03d-145">SDK'ın bazı performans geliştirmeleri yapıldı.</span><span class="sxs-lookup"><span data-stu-id="ae03d-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="ae03d-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="ae03d-147">Toplama sorguları için FeedOptions içinde sağlanan PartitionKey değeri göz ardı bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ae03d-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="ae03d-148">Bölüm yönetim saydam işleme Orta uçuş çapraz bölüm Order By sorgu yürütme sırasında bir sorun sabit.</span><span class="sxs-lookup"><span data-stu-id="ae03d-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="ae03d-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="ae03d-150">Zaman uyumsuz ASP.NET bağlam içinde kullanıldığında API'leri bazılarını kilitlenmeleri neden bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ae03d-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="ae03d-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="ae03d-152">Otomatik Yük devretme belirli koşullar altında daha esnektir SDK yapmak giderir.</span><span class="sxs-lookup"><span data-stu-id="ae03d-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="ae03d-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="ae03d-154">Bazen WebException neden olan bir sorunu düzeltin: uzak ad çözümlenemedi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="ae03d-155">Doğrudan ReadDocumentAsync API'sine yeni aşırı ekleyerek yazılı belgeyi okumak için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="ae03d-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="ae03d-157">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) için LINQ destek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ae03d-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="ae03d-158">Olay işleyicisi kullanımına neden ConnectionPolicy nesnesi için bellek sızıntısı sorunu düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ae03d-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="ae03d-159">ETag kullanıldığında; burada görüntülerle UpsertAttachmentAsync çalışır durumda olmayan bir sorunu düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ae03d-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="ae03d-160">Burada görüntülerle sorgu devamlılığı sırası tarafından çapraz bölüm sıralarken dize alanı üzerinde çalıştığı olmayan bir sorunu düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ae03d-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="ae03d-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="ae03d-162">Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ae03d-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="ae03d-163">Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="ae03d-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="ae03d-164">En düşük işleme 2500 RU/s 10,100 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.</span><span class="sxs-lookup"><span data-stu-id="ae03d-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="ae03d-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="ae03d-166">Azure Cosmos DB .NET Core SDK hızlı, platformlar arası oluşturmanıza olanak sağlayan [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) uygulamaların Windows, Mac ve Linux üzerinde çalışması için.</span><span class="sxs-lookup"><span data-stu-id="ae03d-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="ae03d-167">En son Azure Cosmos DB .NET Core SDK'ın tam olarak sürümdür [Xamarin](https://www.xamarin.com) uyumlu iOS, Android ve Mono (Linux) kullanan uygulamalar oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ae03d-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="ae03d-168"><a name="0.1.0-preview"/>0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="ae03d-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="ae03d-169">Azure Cosmos DB .NET Core Preview SDK'sı platformlar arası hızlı oluşturmanıza olanak sağlayan [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) uygulamaların Windows, Mac ve Linux üzerinde çalışması için.</span><span class="sxs-lookup"><span data-stu-id="ae03d-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="ae03d-170">Özellik eşliği en son sürümü ile Azure Cosmos DB .NET Core Önizleme SDK sahip [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md) ve aşağıdakileri destekler:</span><span class="sxs-lookup"><span data-stu-id="ae03d-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="ae03d-171">Tüm [bağlantı modlarını](performance-tips.md#networking): ağ geçidi modu, doğrudan TCP ve doğrudan HTTPs.</span><span class="sxs-lookup"><span data-stu-id="ae03d-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="ae03d-172">Tüm [tutarlılık düzeylerini](consistency-levels.md): güçlü, oturum, sınırlanmış eskime durumu ve Eventual.</span><span class="sxs-lookup"><span data-stu-id="ae03d-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="ae03d-173">[Bölümlenmiş koleksiyonlar](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="ae03d-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="ae03d-174">[Bölgeli veritabanı hesapları ve coğrafi çoğaltma](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ae03d-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="ae03d-175">Bu SDK ile ilgili sorularınız varsa, deftere [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), veya bir sorunu dosya [github deposunu](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="ae03d-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="ae03d-176">Yayın & sona erme tarihlerini</span><span class="sxs-lookup"><span data-stu-id="ae03d-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="ae03d-177">Sürüm</span><span class="sxs-lookup"><span data-stu-id="ae03d-177">Version</span></span> | <span data-ttu-id="ae03d-178">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="ae03d-178">Release Date</span></span> | <span data-ttu-id="ae03d-179">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="ae03d-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="ae03d-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="ae03d-181">10 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="ae03d-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="ae03d-183">07 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="ae03d-185">02 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="ae03d-187">12 Haziran 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="ae03d-189">23 May 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="ae03d-191">10 Mayıs 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="ae03d-193">19 Nisan 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="ae03d-195">29 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="ae03d-197">25 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="ae03d-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="ae03d-199">20 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="ae03d-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="ae03d-201">14 Mart 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="ae03d-203">16 Şubat 2017</span><span class="sxs-lookup"><span data-stu-id="ae03d-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="ae03d-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ae03d-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="ae03d-205">21 aralık 2016</span><span class="sxs-lookup"><span data-stu-id="ae03d-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="ae03d-206">0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="ae03d-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="ae03d-207">15 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="ae03d-207">November 15, 2016</span></span> |<span data-ttu-id="ae03d-208">31 Aralık 2016</span><span class="sxs-lookup"><span data-stu-id="ae03d-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="ae03d-209">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ae03d-209">See Also</span></span>
<span data-ttu-id="ae03d-210">Cosmos DB hakkında daha fazla bilgi için bkz: [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="ae03d-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


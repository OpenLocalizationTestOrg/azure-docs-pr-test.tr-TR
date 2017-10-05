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
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Azure Cosmos DB .NET Core SDK: sürüm notları ve kaynakları
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET değişiklik besleme](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST Kaynak Sağlayıcısı](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK yükleme**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**API belgeleri**</td><td>[.NET API başvuru belgeleri](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Örnekler**</td><td>[.NET kodu örnekleri](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Kullanmaya başlama**</td><td>[Azure Cosmos DB .NET Core SDK ile çalışmaya başlama](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Web uygulaması Öğreticisi**</td><td>[Azure Cosmos DB ile Web uygulaması geliştirme](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Geçerli desteklenen çerçevelerden**</td><td>[.NET standart 1.6 ve standart 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm Notları

Özellik eşliği en son sürümü ile Azure Cosmos DB .NET Core SDK sahip [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Azure Cosmos DB .NET Core SDK henüz Evrensel Windows Platformu (UWP) uygulamaları ile uyumlu değil. .NET Core UWP uygulamaları destekleyen SDK'ın ilgileniyorsanız, e-posta Gönder [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Sorgu Sonuçları belirli bir bölüm anahtarı aralığının değerine kapsamı için bir FeedOption olarak PartitionKeyRangeId desteği eklendi. 
* Bundan sonra değişikliklerin aramaya başlamak için bir ChangeFeedOption olarak StartTime desteği eklendi. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Bir yığın taşması özel durumu neden olabilir JsonSerializable sınıfında bir sorun düzeltilmiştir.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Örnek oluşturma sırasında özel JsonSerializerSettings belirtmek için destek eklenmiştir bir [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) örneği.

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   .NET standart 1.5 tek bir hedef çerçeve olarak destekleme.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   X64 etkilenen bir sorun sabit olmayan SSE4 yönerge destekleyen ve Azure Cosmos DB sorgu çalıştırırken SEHException throw makineler.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.
*   Tek tek bölümler için sorgu ölçümleri desteği eklendi.
*   Sorgular için devamlılık belirteci boyutunu sınırlamak için destek eklendi.
*   Başarısız istekler için ayrıntılı izleme desteği eklendi.
*   SDK'ın bazı performans geliştirmeleri yapıldı.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Toplama sorguları için FeedOptions içinde sağlanan PartitionKey değeri göz ardı bir sorun düzeltilmiştir.
* Bölüm yönetim saydam işleme Orta uçuş çapraz bölüm Order By sorgu yürütme sırasında bir sorun sabit.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Zaman uyumsuz ASP.NET bağlam içinde kullanıldığında API'leri bazılarını kilitlenmeleri neden bir sorun düzeltilmiştir.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Otomatik Yük devretme belirli koşullar altında daha esnektir SDK yapmak giderir.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Bazen WebException neden olan bir sorunu düzeltin: uzak ad çözümlenemedi.
* Doğrudan ReadDocumentAsync API'sine yeni aşırı ekleyerek yazılı belgeyi okumak için destek eklendi.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) için LINQ destek eklenmiştir.
* Olay işleyicisi kullanımına neden ConnectionPolicy nesnesi için bellek sızıntısı sorunu düzeltin.
* ETag kullanıldığında; burada görüntülerle UpsertAttachmentAsync çalışır durumda olmayan bir sorunu düzeltin.
* Burada görüntülerle sorgu devamlılığı sırası tarafından çapraz bölüm sıralarken dize alanı üzerinde çalıştığı olmayan bir sorunu düzeltin.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi. Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).
* En düşük işleme 2500 RU/s 10,100 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Azure Cosmos DB .NET Core SDK hızlı, platformlar arası oluşturmanıza olanak sağlayan [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) uygulamaların Windows, Mac ve Linux üzerinde çalışması için. En son Azure Cosmos DB .NET Core SDK'ın tam olarak sürümdür [Xamarin](https://www.xamarin.com) uyumlu iOS, Android ve Mono (Linux) kullanan uygulamalar oluşturmak için kullanılır.  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-Preview

Azure Cosmos DB .NET Core Preview SDK'sı platformlar arası hızlı oluşturmanıza olanak sağlayan [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) uygulamaların Windows, Mac ve Linux üzerinde çalışması için.

Özellik eşliği en son sürümü ile Azure Cosmos DB .NET Core Önizleme SDK sahip [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md) ve aşağıdakileri destekler:
* Tüm [bağlantı modlarını](performance-tips.md#networking): ağ geçidi modu, doğrudan TCP ve doğrudan HTTPs. 
* Tüm [tutarlılık düzeylerini](consistency-levels.md): güçlü, oturum, sınırlanmış eskime durumu ve Eventual.
* [Bölümlenmiş koleksiyonlar](partition-data.md). 
* [Bölgeli veritabanı hesapları ve coğrafi çoğaltma](distribute-data-globally.md).

Bu SDK ile ilgili sorularınız varsa, deftere [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), veya bir sorunu dosya [github deposunu](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Yayın & sona erme tarihlerini

| Sürüm | Sürüm tarihi | Sona erme tarihi |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 Ağustos 2017 |--- | 
| [1.4.1](#1.4.1) |07 Ağustos 2017 |--- |
| [1.4.0](#1.4.0) |02 Ağustos 2017 |--- |
| [1.3.2](#1.3.2) |12 Haziran 2017 |--- |
| [1.3.1](#1.3.1) |23 May 2017 |--- |
| [1.3.0](#1.3.0) |10 Mayıs 2017 |--- |
| [1.2.2](#1.2.2) |19 Nisan 2017 |--- |
| [1.2.1](#1.2.1) |29 Mart 2017 |--- |
| [1.2.0](#1.2.0) |25 Mart 2017 |--- |
| [1.1.2](#1.1.2) |20 Mart 2017 |--- |
| [1.1.1](#1.1.1) |14 Mart 2017 |--- |
| [1.1.0](#1.1.0) |16 Şubat 2017 |--- |
| [1.0.0](#1.0.0) |21 aralık 2016 |--- |
| [0.1.0-Preview](#0.1.0-preview) |15 Kasım 2016 |31 Aralık 2016 |

## <a name="see-also"></a>Ayrıca Bkz.
Cosmos DB hakkında daha fazla bilgi için bkz: [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası. 


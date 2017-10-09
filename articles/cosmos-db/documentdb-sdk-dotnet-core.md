---
title: "aaaAzure Cosmos DB .NET Core API SDK & kaynakları | Microsoft Docs"
description: ".NET Core API ve SDK sürüm tarih, sona erme tarihlerini ve her bir hello Azure Cosmos DB .NET Core SDK sürümü arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında bilgi edinin."
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
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
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

<tr><td>**Kullanmaya başlama**</td><td>[Hello Azure Cosmos DB .NET Core SDK ile çalışmaya başlama](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Web uygulaması Öğreticisi**</td><td>[Azure Cosmos DB ile Web uygulaması geliştirme](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Geçerli desteklenen çerçevelerden**</td><td>[.NET standart 1.6 ve standart 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm Notları

Hello Azure Cosmos DB .NET Core SDK sahip özellik eşliği hello hello en son sürümü ile [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Hello Azure Cosmos DB .NET Core SDK henüz Evrensel Windows Platformu (UWP) uygulamaları ile uyumlu değil. Merhaba UWP uygulamaları destekleyen .NET Core SDK ilgileniyorsanız, e-posta çok gönderme[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Sorgu sonuçları tooa belirli bir bölüm anahtarı aralığının değeri kapsamı için bir FeedOption olarak PartitionKeyRangeId desteği eklendi. 
* Bundan sonra hello değişiklikleri arayan ChangeFeedOption toostart olarak StartTime desteği eklendi. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Bir sorun hello bir yığın taşması özel durumu neden olabilecek JsonSerializable sınıfı sabit.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Örnek oluşturma sırasında özel JsonSerializerSettings belirtmek için destek eklenmiştir bir [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) örneği.

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   .NET standart 1.5 hello hedef çerçeveyi biri olarak destekleme.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   X64 etkilenen bir sorun sabit olmayan SSE4 yönerge destekleyen ve Azure Cosmos DB sorgu çalıştırırken SEHException throw makineler.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.
*   Tek tek bölümler için sorgu ölçümleri desteği eklendi.
*   Sorgular için hello devamlılık belirteci hello boyutunu sınırlamak için destek eklendi.
*   Başarısız istekler için ayrıntılı izleme desteği eklendi.
*   Bazı performans geliştirmeleri hello SDK yapıldı.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Toplama sorguları için FeedOptions içinde sağlanan hello PartitionKey değeri göz ardı bir sorun düzeltilmiştir.
* Bölüm yönetim saydam işleme Orta uçuş çapraz bölüm Order By sorgu yürütme sırasında bir sorun sabit.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Bazı hello zaman uyumsuz ASP.NET bağlam içinde kullanıldığında API'leri kilitlenmeleri neden bir sorun düzeltilmiştir.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Daha fazla toomake SDK düzeltmeler belirli koşullar altında dayanıklı tooautomatic yük devretme.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Bazen WebException neden olan bir sorunu düzeltin: hello uzak ad çözümlenemedi.
* Eklenen hello desteği doğrudan yeni aşırı tooReadDocumentAsync API ekleyerek yazılı belgeyi okumak için.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) için LINQ destek eklenmiştir.
* Olay işleyicisi hello kullanımına neden hello ConnectionPolicy nesnesi için bellek sızıntısı sorunu düzeltin.
* ETag kullanıldığında; burada görüntülerle UpsertAttachmentAsync çalışır durumda olmayan bir sorunu düzeltin.
* Burada görüntülerle sorgu devamlılığı sırası tarafından çapraz bölüm sıralarken dize alanı üzerinde çalıştığı olmayan bir sorunu düzeltin.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi. Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).
* En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK toobuild hızlı, platformlar arası sağlar [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac ve Linux uygulamaları toorun. Merhaba hello Azure Cosmos DB .NET Core SDK en son sürümünü tam olarak olan [Xamarin](https://www.xamarin.com) uyumlu ve iOS, Android ve Mono (Linux) hedef kullanılan toobuild uygulamalar.  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-Preview

Hello Azure Cosmos DB .NET Core Önizleme SDK toobuild hızlı, platformlar arası sağlar [ASP.NET Core](https://www.asp.net/core) ve [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac ve Linux uygulamaları toorun.

Hello Azure Cosmos DB .NET Core Önizleme SDK sahip özellik eşliği hello hello en son sürümü ile [Azure Cosmos DB .NET SDK'sı](documentdb-sdk-dotnet.md) ve hello aşağıdakileri destekler:
* Tüm [bağlantı modlarını](performance-tips.md#networking): ağ geçidi modu, doğrudan TCP ve doğrudan HTTPs. 
* Tüm [tutarlılık düzeylerini](consistency-levels.md): güçlü, oturum, sınırlanmış eskime durumu ve Eventual.
* [Bölümlenmiş koleksiyonlar](partition-data.md). 
* [Bölgeli veritabanı hesapları ve coğrafi çoğaltma](distribute-data-globally.md).

Sorular ilgili toothis SDK varsa, çok sonrası[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), veya bir sorunu hello dosya [github deposunu](https://github.com/Azure/azure-documentdb-dotnet/issues). 

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
toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası. 


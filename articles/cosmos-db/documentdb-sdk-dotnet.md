---
title: "aaaAzure Cosmos DB .NET SDK'sını & kaynakları | Microsoft Docs"
description: ".NET API ve SDK sürüm tarih, sona erme tarihlerini ve her hello Azure Cosmos DB .NET SDK'sı sürüm arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında öğrenin."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure Cosmos DB .NET SDK'sı: İndirme ve sürüm notları
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

<tr><td>**SDK yükleme**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**API belgeleri**</td><td>[.NET API başvuru belgeleri](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Örnekler**</td><td>[.NET kodu örnekleri](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Kullanmaya başlama**</td><td>[Hello Azure Cosmos DB .NET SDK ile çalışmaya başlama](documentdb-get-started.md)</td></tr>

<tr><td>**Web uygulaması Öğreticisi**</td><td>[Azure Cosmos DB ile Web uygulaması geliştirme](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Geçerli desteklenen çerçevelerden**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm notları

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Sorgu sonuçları tooa belirli bir bölüm anahtarı aralığının değeri kapsamı için bir FeedOption olarak PartitionKeyRangeId desteği eklendi. 
* Bundan sonra hello değişiklikleri arayan ChangeFeedOption toostart olarak StartTime desteği eklendi.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Bir sorun hello bir yığın taşması özel durumu neden olabilecek JsonSerializable sınıfı sabit.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Bir sorun nedeniyle JsonSerializerSettings toohello giriş hello uygulamanın hello DocumentClient Oluşturucusu isteğe bağlı bir parametre olarak yeniden derlenmesi gereken sabit.
* JsonSerializerSettings ConnectionPolicy ve ConsistencyLevel parametrelerinin varsayılan değerleri için son parametre tooallow JsonSerializerSettings parametresinde geçirilirken hello gibi gerekli işaretli hello DocumentClient Oluşturucu artık kullanılmıyor.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Örnek oluşturma sırasında özel JsonSerializerSettings belirtmek için destek eklenmiştir [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   X64 etkilenen bir sorun sabit olmayan SSE4 yönerge destekleyen ve bir SEHException Azure Cosmos DB DocumentDB API sorgu çalıştırırken throw makineler.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.
*   Tek tek bölümler için sorgu ölçümleri desteği eklendi.
*   Sorgular için hello devamlılık belirteci hello boyutunu sınırlamak için destek eklendi.
*   Başarısız istekler için ayrıntılı izleme desteği eklendi.
*   Bazı performans geliştirmeleri hello SDK yapıldı.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* 1.13.3 işlevsel olarak aynıdır. İç bazı değişiklikler yaptınız.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* 1.13.2 işlevsel olarak aynıdır. İç bazı değişiklikler yaptınız.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Toplama sorguları için FeedOptions içinde sağlanan hello PartitionKey değeri göz ardı bir sorun düzeltilmiştir.
* Bölüm yönetim saydam işleme Orta uçuş çapraz bölüm Order By sorgu yürütme sırasında bir sorun sabit.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Bazı hello zaman uyumsuz ASP.NET bağlam içinde kullanıldığında API'leri kilitlenmeleri neden bir sorun düzeltilmiştir.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Daha fazla toomake SDK düzeltmeler belirli koşullar altında dayanıklı tooautomatic yük devretme.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Bazen WebException neden olan bir sorunu düzeltin: hello uzak ad çözümlenemedi.
* Eklenen hello desteği doğrudan yeni aşırı tooReadDocumentAsync API ekleyerek yazılı belgeyi okumak için.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) için LINQ destek eklenmiştir.
* Olay işleyicisi hello kullanımına neden hello ConnectionPolicy nesnesi için bellek sızıntısı sorunu düzeltin.
* ETag kullanıldığında; burada görüntülerle UpsertAttachmentAsync çalışır durumda olmayan bir sorunu düzeltin.
* Burada görüntülerle sorgu devamlılığı sırası tarafından çapraz bölüm sıralarken dize alanı üzerinde çalıştığı olmayan bir sorunu düzeltin.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi. Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).
* En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Burada görüntülerle bazı hello çapraz bölüm sorguları hello 32-bit ana işleminde başarısız bir sorun için düzeltme.
* Burada görüntülerle hello oturum kapsayıcı ağ geçidi modunda başarısız istekler için hello belirteci ile güncelleştirilmedi bir sorun için düzeltme.
* Bazı durumlarda bir sorgu projeksiyon UDF çağrılarında; burada görüntülerle başarısız sorunu düzeltin.
* İstemci tarafı performans düzeltmeleri'hello artırmak için okuma ve hello isteklerin verimini yazma.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Burada görüntülerle hello oturum kapsayıcı başarısız istekler için hello belirteci ile güncelleştirilmedi bir sorun için düzeltme.
* 32-bit barındırma işlemi içinde hello SDK toowork desteği eklendi. Not çapraz bölüm sorguları kullanıyorsanız, 64-bit ana bilgisayar işleme Gelişmiş performans için önerilir.
* Çok sayıda bölüm anahtarı değerleri IN deyimde sorgularıyla ilgili senaryoları için geliştirilmiş performans.
* PopulateQuotaInfo isteği seçenek ayarlandığında belge koleksiyonunu okuma istekleri için çeşitli kaynak kotası istatistikleri hello ResourceResponse olarak doldurulur.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Merhaba CreateDocumentCollectionIfNotExistsAsync 1.11.0 içinde sunulan API için küçük performans düzeltme.
* Merhaba SDK yüksek derecede eşzamanlı istek gerektiren senaryolar için performans düzeltme.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Yeni sınıflar ve yöntemler tooprocess hello desteği [akış değiştirmek](change-feed.md) bir koleksiyon içinde belgelerin.
* Çapraz bölüm sorgusu devamlılık ve çapraz bölüm sorgular için bazı performans geliştirmeleri için destek.
* Ayrıca CreateDatabaseIfNotExistsAsync ve CreateDocumentCollectionIfNotExistsAsync yöntemleri.
* LINQ sistem işlevleri için destek: IsDefined, IsNull ve IsPrimitive.
* Microsoft.Azure.Documents.ServiceInterop.dll ve DocumentDB.Spatial.Sql.dll derlemeleri tooapplication ait bin klasörü otomatik binplacing için hello Nuget paketi project.json araç projeleri ile kullanırken düzeltin.
* Senaryoları hata ayıklamaya yardımcı olabilir istemci tarafı ETW izlerini yayma desteği.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Bölümlenmiş koleksiyonlar için eklenen doğrudan bağlantı desteği.
* Merhaba sınırlanmış eskime durumu tutarlılığı düzeyi için performansı geliştirildi.
* Eklenen Çokgen ve LineString İlkesi coğrafı uzamsal sorguları için dizin oluşturma koleksiyonunu belirten sırasında veri türleri.
* Koşulları çevrilirken LINQ desteği eklendi StringEnumConverter, IsoDateTimeConverter ve UnixDateTimeConverter.
* Çeşitli SDK hata düzeltmeleri.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Bir sorun nedeniyle bu hello NotFoundException aşağıdaki sabit: hello okuma oturum hello giriş Oturum belirteci için kullanılabilir değil. Bu durum bazı durumlarda hello okuma-bölge için bir coğrafi olarak dağıtılan hesabının sorgulanırken oluştu.
* Merhaba ResponseStream hello doğrudan erişim toohello temel alınan akıştan bir yanıt sağlar ResourceResponse sınıfı özelliğinde açık.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Böylece dağıtım (TDD) güdümlü test için mocked ortak arabirimi karşılık gelen değiştirilmiş hello ResourceResponse, FeedResponse, StoredProcedureResponse ve MediaResponse sınıfları tooimplement hello.
* Özel bir JsonSerializerSettings nesnesi için verilerin serileştirilmesi kullanırken hatalı biçimlendirilmiş bölüm anahtar üstbilgi neden bir sorun düzeltilmiştir.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Uzun süre çalışan sorgular toofail ile hataya neden olan bir sorunu sabit: Yetkilendirme belirteci geçerli değil hello geçerli saati.
* Sabit kaldırılmış bir sorun hello gelen özgün SqlParameterCollection bölüm üst/order-by sorguları arası.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Bölümlenmiş koleksiyonlar için paralel sorgular için destek eklendi.
* Bölümlenmiş koleksiyonlar için bölüm sıralama ve üst sorguları çapraz eklenen desteği.
* Sabit hello Azure Cosmos DB projesindeki bir başvurusu toohello Azure Cosmos DB Nuget paketi ile başvururken gerekli başvuruları tooDocumentDB.Spatial.Sql.dll ve Microsoft.Azure.Documents.ServiceInterop.dll eksik.
* Kullanıcı tanımlı işlevler LINQ kullanırken farklı türde sabit hello özelliği toouse parametreler. 
* Genel olarak çoğaltılmış hesapları için bir hata Upsert çağrıları yönlendirilmiş tooread konumları yazma konumları yerine burada olan sabit.
* Eksik toohello IDocumentClient arabirimi eklenen yöntemleri: 
  * MediaStream ve seçenekleri parametre olarak alır UpsertAttachmentAsync yöntemi
  * Parametre olarak seçeneklerini alır CreateAttachmentAsync yöntemi
  * Bir parametre olarak querySpec geçen CreateOfferQuery yöntemi.
* Merhaba IDocumentClient arabiriminde gösterilen korumasız ortak sınıflar.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Eklenen hello bölgeli veritabanı hesaplarını desteği.
* Yeniden deneme daraltılmış isteklerinde desteği eklendi.  Merhaba en fazla bekleme süresi hello ConnectionPolicy.RetryOptions özelliğini yapılandırarak ve kullanıcı yeniden deneme sayısı hello özelleştirebilirsiniz.
* Tüm DocumenClient özellikleri ve yöntemleri hello imzalarını tanımlayan yeni bir IDocumentClient arabirimi eklendi.  Bu değişikliğin bir parçası olarak, aynı zamanda Iqueryable ve IOrderedQueryable toomethods DocumentClient sınıfının kendisi hello üzerinde oluşturma genişletme yöntemleri değiştirildi.
* Verilen Azure Cosmos DB uç noktası URI için yapılandırma seçeneği tooset hello ServicePoint.ConnectionLimit eklendi.  Too50 ayarlanan ConnectionPolicy.MaxConnectionLimit toochange hello varsayılan değeri kullanın.
* Kullanım dışı IPartitionResolver ve kendi uygulama.  IPartitionResolver desteği artık kullanılmıyor. Daha yüksek depolama ve işleme için bölümlenmiş koleksiyonlar kullanmanız önerilir.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Bir parametre olarak RequestOptions geçen ExecuteStoredProcedureAsync yöntemi aşırı tooUri dayalı eklendi.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Belgeler için zaman toolive (TTL) desteği eklendi.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Bir hata, bir Azure bulut hizmeti çözümü parçası olarak paketlemek için .NET SDK'sı Nuget paketleme, sabit.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Sabit]**  Sorgulama Azure Cosmos DB uç noktası oluşturur: ' System.Net.Http.HttpRequestException: içerik tooa akış kopyalarken hata oluştu '.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Genişletilmiş LINQ sayfalama, koşullu ifadeleri için yeni işleçleri dahil olmak üzere destek ve karşılaştırma aralığı.
  * LINQ işleci tooenable seçin üst davranışı alın
  * CompareTo işleci tooenable dize aralığı karşılaştırmaları
  * Koşullu (?) ve işleçler (?) birleşim
* **[Sabit]**  Modeli projeksiyon ile birleştirilirken ArgumentOutOfRangeException Where bileşeninde LINQ sorgusu. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Sabit]**  Seçin hello son deyim hello değilse LINQ sağlayıcısı projeksiyon kabul ve SELECT üretilen * yanlış.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Uygulanan Upsert, eklenen UpsertXXXAsync yöntemleri
* Tüm istekleri için performans iyileştirmeleri
* Koşullu, LINQ sağlayıcı desteği birleşim ve dizeleri CompareTo yöntemleri
* **[Sabit]**  LINQ sağlayıcısı--> Uygulama listesi toogenerate yöntemi IEnumerable ve dizi gibi aynı SQL hello içerir
* **[Sabit]**  BackoffRetryUtility kullanan yeni bir yeniden deneme oluşturma yerine aynı HttpRequestMessage hello
* **[Geçersiz]**  UriFactory.CreateCollection--> şimdi UriFactory.CreateDocumentCollection kullanmanız gerekir

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Sabit]**  Yerelleştirme sorunları olmayan tr kültür bilgisi nl-NL, vb. gibi kullanırken. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Kimliği tabanlı yönlendirme eklendi
  * Kaynak Kimliği tabanlı bağlantıları oluşturma ile yeni UriFactory yardımcı tooassist
  * DocumentClient tootake URI üzerinde yeni aşırı yüklemeleri
* IsValid() ve Jeo-uzamsal LINQ IsValidDetailed() eklendi
* LINQ sağlayıcı desteği geliştirilmiştir:
  * **Matematik** -Abs Acos, Asin, Ceiling Exp, Floor, günlük, Log10, Pow, hepsini, oturum, Sinüs, Sqrt, Tan Cos Atan kesme
  * **Dize** -EndsWith, IndexOf, Count, ToLower, TrimStart Concat, içerir, Değiştir, tersine, TrimEnd, StartsWith, SubString, ToUpper
  * **Dizi** -Concat, içerir, sayısı
  * **IN** işleci

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Dizin oluşturma ilkeleri değiştirmek için destek eklendi.
  * DocumentClient yeni ReplaceDocumentCollectionAsync yöntemi
  * ResourceResponse yeni IndexTransformationProgress özelliğinde<T> dizin ilke değişikliklerini yüzde ilerlemesini izlemek için
  * DocumentCollection.IndexingPolicy artık değişebilir
* Uzamsal dizin oluşturma ve sorgu için destek eklendi.
  * Seri hale getirme/uzamsal türler seri durumdan çıkarmak için yeni Microsoft.Azure.Documents.Spatial ad alanı gibi noktası ve Çokgen
  * Cosmos DB içinde depolanan GeoJSON verileri dizin oluşturma için yeni SpatialIndex sınıfı
* **[Sabit]**  Yanlış SQL sorgu LINQ ifadesinden [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Bir bağımlılık Newtonsoft.Json v5.0.7 üzerinde eklendi.
* Order By toosupport yapılan değişiklikler:
  
  * LINQ sağlayıcı desteği OrderBy() veya OrderByDescending()
  * Order By IndexingPolicy toosupport 
    
    **Olası önemli değişiklik** 
    
    Bu hükümleri koleksiyonları özel bir dizin oluşturma ilkesi ile var olan kodu varsa, varolan Kod gereksinimlerini toobe toosupport hello yeni IndexingPolicy sınıfı güncelleştirildi. Daha sonra özel bir dizin oluşturma ilkesi varsa, bu değişiklik, etkilemez.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Merhaba yeni HashPartitionResolver ve RangePartitionResolver sınıfları ve hello IPartitionResolver kullanarak veri bölümlendirme için destek eklendi.
* Eklenen DataContract seri hale getirme.
* Eklenen GUID LINQ sağlayıcısında destekler.
* Eklenen UDF LINQ destekler.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK'SI

## <a name="release--retirement-dates"></a>Yayın & sona erme tarihleri
Microsoft'un sağladığı bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.

Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle önerilir, her zaman yükseltme toohello en son SDK sürümünün olabildiğince erken. 

Tüm istekleri tooAzure Cosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.

<br/>

| Sürüm | Sürüm tarihi | Sona erme tarihi |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 Ağustos 2017 |--- |
| [1.16.1](#1.16.1) |07 Ağustos 2017 |--- |
| [1.16.0](#1.16.0) |02 Ağustos 2017 |--- |
| [1.15.0](#1.15.0) |30 Haziran 2017 |--- |
| [1.14.1](#1.14.1) |23 May 2017 |--- |
| [1.14.0](#1.14.0) |10 Mayıs 2017 |--- |
| [1.13.4](#1.13.4) |09 May 2017 |--- |
| [1.13.3](#1.13.3) |06 May 2017 |--- |
| [1.13.2](#1.13.2) |19 Nisan 2017 |--- |
| [1.13.1](#1.13.1) |29 Mart 2017 |--- |
| [1.13.0](#1.13.0) |24 Mart 2017 |--- |
| [1.12.2](#1.12.2) |20 Mart 2017 |--- |
| [1.12.1](#1.12.1) |14 Mart 2017 |--- |
| [1.12.0](#1.12.0) |15 Şubat 2017 |--- |
| [1.11.4](#1.11.4) |06 Şubat 2017 |--- |
| [1.11.3](#1.11.3) |26 Ocak 2017 |--- |
| [1.11.1](#1.11.1) |21 aralık 2016 |--- |
| [1.11.0](#1.11.0) |08 Aralık 2016 |--- |
| [1.10.0](#1.10.0) |27 Eylül 2016 |--- |
| [1.9.5](#1.9.5) |01 Eylül 2016 |--- |
| [1.9.4](#1.9.4) |24 Ağustos 2016 |--- |
| [1.9.3](#1.9.3) |15 Ağustos 2016 |--- |
| [1.9.2](#1.9.2) |23 Temmuz 2016 |--- |
| [1.8.0](#1.8.0) |14 Haziran 2016 |--- |
| [1.7.1](#1.7.1) |06 Mayıs 2016 |--- |
| [1.7.0](#1.7.0) |26 Nisan 2016 |--- |
| [1.6.3](#1.6.3) |08 Nisan 2016 |--- |
| [1.6.2](#1.6.2) |29 Mart 2016 |--- |
| [1.5.3](#1.5.3) |19 Şubat 2016 |--- |
| [1.5.2](#1.5.2) |14 Aralık 2015 |--- |
| [1.5.1](#1.5.1) |23 Kasım 2015 |--- |
| [1.5.0](#1.5.0) |05 Ekim 2015 |--- |
| [1.4.1](#1.4.1) |25 Ağustos 2015 |--- |
| [1.4.0](#1.4.0) |13 Ağustos 2015 |--- |
| [1.3.0](#1.3.0) |05 Ağustos 2015 |--- |
| [1.2.0](#1.2.0) |06 Temmuz 2015 |--- |
| [1.1.0](#1.1.0) |30 Nisan 2015 |--- |
| [1.0.0](#1.0.0) |08 Nisan 2015 |--- |


## <a name="faq"></a>SSS
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Ayrıca bkz.
toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası. 


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
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB: DocumentDB Java SDK'sı sürüm notları ve kaynakları
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

<tr><td>**SDK yükleme**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**API belgeleri**</td><td>[Java API başvuru belgeleri](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**TooSDK katkıda bulunan**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Kullanmaya başlama**</td><td>[Merhaba Java SDK'sı ile çalışmaya başlama](documentdb-java-get-started.md)</td></tr>

<tr><td>**Web uygulaması Öğreticisi**</td><td>[Azure Cosmos DB ile Web uygulaması geliştirme](documentdb-java-application.md)</td></tr>

<tr><td>**Geçerli desteklenen çalışma zamanı**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm Notları

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Kritik hata düzeltmeleri toorequest sırasında bölümü işlemeye böler.
* Hello güçlü ve BoundedStaleness tutarlılık düzeyleri ile ilgili bir sorun düzeltilmiştir.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.
* Oturum modu koleksiyonunda okuma hatanın düzeltildiğini.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Etkin bölümlenmiş koleksiyonuyla desteği 2.500 RU/sn düşük ve 100 RU/sn artışlarla ölçeklendirin.
* Bir hata NullRef özel bazı sorgular neden hello yerel derleme sabit.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Merhaba sorgu altyapısı yapılandırmasında sorguları için özel durumlar ağ geçidi modunda neden olabilecek bir hatanın düzeltildiğini.
* "Sahip kaynak bulunamadı" için bir özel durum isteklerinin koleksiyonu oluşturulduktan hemen sonra neden olabilecek hello oturum kapsayıcısında birkaç düzeltilen.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi. Bkz: [toplama Destek](documentdb-sql-query.md#Aggregates).
* Akış değişiklik desteği eklendi.
* Koleksiyon kota bilgileri RequestOptions.setPopulateQuotaInfo aracılığıyla desteği eklendi.
* Saklı yordam komut dosyası günlük RequestOptions.setScriptLoggingEnabled aracılığıyla desteği eklendi.
* Kısıtlama hataları karşılaşıldığında DirectHttps modunda sorgu burada kilitlenebilir hatanın düzeltildiğini.
* Bir hatayı oturum tutarlılığı modunda sabit.
* İstek oranı yüksek olduğunda bu NullReferenceException içinde HttpContext neden olabilecek bir hatanın düzeltildiğini.
* DirectHttps modu performansı geliştirildi.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* ConnectionPolicy.setProxy() API ile eklenen basit istemci örnek tabanlı proxy desteği.
* Eklenen DocumentClient.close() API tooproperly kapatma DocumentClient örneği.
* İyileştirilmiş sorgu performansı hello yerel derleme hello ağ geçidi yerine hello sorgu planı türetme tarafından doğrudan bağlantı modunda.
* Ayarlama FAIL_ON_UNKNOWN_PROPERTIES böylece kullanıcılar kendi POJO'ya JsonIgnoreProperties toodefine = false.
* Günlük toouse SLF4J bulunanad.
* Birkaç diğer tutarlılık okuyucusunda düzeltilen.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Bir hata hello bağlantı yönetimi tooprevent bağlantı sızıntıları doğrudan bağlantı modunda sabit.
* Bir hata, burada NullReferenece özel durum atabilir hello üst sorguda sabit.
* Merhaba iç önbellekler için ağ çağrısı hello sayısını azaltarak performansı.
* Eklenen durum kodu, ActivityID ve daha iyi sorun giderme için DocumentClientException, istek URI'si.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Merhaba bağlantı yönetiminde kararlılık için bir sorun düzeltilmiştir.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* BoundedStaleness tutarlılık düzeyi desteği eklendi.
* Bölümlenmiş koleksiyonlar için CRUD işlemleri için doğrudan bağlantı desteği eklendi.
* SQL veritabanıyla sorgulama içinde hatanın düzeltildiğini.
* Bir hata burada oturum belirteci yanlış ayarlanmış olabilir hello oturumu önbelleğinde sabit.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Bölüm paralel sorgular çapraz eklenen desteği.
* ÜST/ORDER BY sorguları bölümlenmiş koleksiyonlar için desteği eklendi.
* Güçlü tutarlılık desteği eklendi.
* Doğrudan bağlantı kullanırken ad tabanlı istekleri için destek eklendi.
* Sabit toomake ActivityID kalmak tutarlı tüm istek yeniden denemeler arasında.
* Hatanın düzeltildiğini hello koleksiyonuyla yeniden zaman toohello oturum önbelleğini ilgili aynı adı.
* Eklenen Çokgen ve LineString İlkesi coğrafı uzamsal sorguları için dizin oluşturma koleksiyonunu belirten sırasında veri türleri.
* Giderilen sorunlar Java 1.8 için Java belge ile.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* İçinde PartitionKeyDefinitionMap hatanın düzeltildiğini toocache tek bölüm koleksiyonları ve değil fazladan yapma anahtar istekleri bölüm getirin.
* Yanlış bölüm anahtarı değerini sağlandığında hata toonot yeniden sabit.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Eklenen hello bölgeli veritabanı hesaplarını desteği.
* Otomatik yeniden deneme seçeneklerini toocustomize hello en fazla ile daraltılmış isteklerde desteği eklendi yeniden deneme sayısı ve en fazla yeniden deneme bekleme süresi.  RetryOptions ve ConnectionPolicy.getRetryOptions() bakın.
* Kullanım dışı IPartitionResolver özel bölümleme kod tabanlı. Lütfen bölümlenmiş koleksiyonlar, daha yüksek depolama ve işleme için kullanın.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Azaltma için eklenen yeniden deneme ilkesi desteği.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Belgeler için zaman toolive (TTL) desteği eklendi.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Bir hata HashPartitionResolver toogenerate karma değerleri little endian toobe diğer SDK'ları ile tutarlı sabit.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Karma & aralığı Ekle Bölüm çözümleyiciler tooassist birden çok bölüm arasında parçalama uygulamalarla.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Upsert uygulayın. Yeni upsertXXX yöntemler toosupport Upsert özellik eklemiştir.
* Temel kimlik yönlendirme uygulayın. Genel API değişiklik, tüm değişiklikleri iç.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Yayın toobring sürüm numarası diğer SDK ile hizalama atlandı

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Destekler Jeo-uzamsal dizin
* ID özelliği tüm kaynaklar için doğrular. Kaynaklar için kimlikleri içeremez?, /, #, \, karakter veya boşluk ile bitmelidir.
* Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* V2 dizin oluşturma ilkesini uygular

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK'SI

## <a name="release--retirement-dates"></a>Yayın & sona erme tarihlerini
Microsoft sağlayacaktır bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.

Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle olduğundan bu, her zaman yükseltme toohello son SDK sürümü olabildiğince erken öneririz.

Tüm istek tooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.

> [!WARNING]
> Java önceki tooversion Merhaba DocumentDB SDK'in tüm sürümleri **1.0.0** üzerinde Çekildi **29 Şubat 2016**.
> 
> 

<br/>

| Sürüm | Sürüm tarihi | Sona erme tarihi |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 Temmuz 2017 |--- |
| [1.11.0](#1.11.0) |10 Mayıs 2017 |--- |
| [1.10.0](#1.10.0) |11 Mart 2017 |--- |
| [1.9.6](#1.9.6) |21 Şubat 2017 |--- |
| [1.9.5](#1.9.5) |31 Ocak 2017 |--- |
| [1.9.4](#1.9.4) |24 Kasım 2016 |--- |
| [1.9.3](#1.9.3) |30 Ekim 2016 |--- |
| [1.9.2](#1.9.2) |28 Ekim 2016 |--- |
| [1.9.1](#1.9.1) |26 Ekim 2016 |--- |
| [1.9.0](#1.9.0) |03 Ekim 2016 |--- |
| [1.8.1](#1.8.1) |30 Haziran 2016 |--- |
| [1.8.0](#1.8.0) |14 Haziran 2016 |--- |
| [1.7.1](#1.7.1) |30 Nisan 2016 |--- |
| [1.7.0](#1.7.0) |27 Nisan 2016 |--- |
| [1.6.0](#1.6.0) |29 Mart 2016 |--- |
| [1.5.1](#1.5.1) |31 Aralık 2015 |--- |
| [1.5.0](#1.5.0) |04 Aralık 2015 |--- |
| [1.4.0](#1.4.0) |05 Ekim 2015 |--- |
| [1.3.0](#1.3.0) |05 Ekim 2015 |--- |
| [1.2.0](#1.2.0) |05 Ağustos 2015 |--- |
| [1.1.0](#1.1.0) |09 Temmuz 2015 |--- |
| [1.0.1](#1.0.1) |12 Mayıs 2015 |--- |
| [1.0.0](#1.0.0) |07 Nisan 2015 |--- |
| 0.9.5-prelease |09 Mar 2015 |29 Şubat 2016 |
| 0.9.4-prelease |17 Şubat 2015 |29 Şubat 2016 |
| 0.9.3-prelease |13 Ocak 2015 |29 Şubat 2016 |
| 0.9.2-prelease |19 Aralık 2014 |29 Şubat 2016 |
| 0.9.1-prelease |19 Aralık 2014 |29 Şubat 2016 |
| 0.9.0-prelease |10 Aralık 2014 |29 Şubat 2016 |

## <a name="faq"></a>SSS
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Ayrıca Bkz.
toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.


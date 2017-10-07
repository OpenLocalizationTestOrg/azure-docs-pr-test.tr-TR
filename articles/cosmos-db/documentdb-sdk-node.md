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
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Azure DB Cosmos Node.js SDK: sürüm notları ve kaynakları
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

<tr><td>**SDK'sını indirin**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**API belgeleri**</td><td>[Node.js API başvuru belgeleri](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**SDK yükleme yönergeleri**</td><td>[Yükleme yönergeleri](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**TooSDK katkıda bulunan**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Örnekler**</td><td>[Node.js kod örnekleri](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Başlangıç eğitmeni**</td><td>[Merhaba Node.js SDK'sı ile çalışmaya başlama](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Web uygulaması Öğreticisi**</td><td>[Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Geçerli desteklenen platformlar**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm notları

### <a name="1.12.2"/>1.12.2</a>
*   Sabit npm belgeleri.

### <a name="1.12.1"/>1.12.1</a>
* Bir hata, burada ilgili belgelerini özel Unicode karakterler (LS, PS) b executeStoredProcedure içinde sabit.
* Merhaba bölüm anahtarı Unicode karakterler içeren belgeleri işlemedeki hatanın düzeltildiğini.
* Sabit koleksiyonlar ile Merhaba ad ortamı oluşturma desteği. Github sorunu #114.
* İzni yetkilendirme belirtecini sabit desteği. Github sorunu #178.

### <a name="1.12.0"/>1.12.0</a>
* Yeni bir desteği eklendi [tutarlılık düzeyi](consistency-levels.md) ConsistentPrefix çağrılır.
* UriFactory desteği eklendi.
* Unicode desteği hatanın düzeltildiğini. GitHub sorunu #171.

### <a name="1.11.0"/>1.11.0</a>
* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi hello.
* Çapraz bölüm sorgular için paralellik derecesi denetleme eklenen hello seçeneği.
* SSL doğrulama Azure Cosmos DB öykünücüsüne karşı çalıştırırken devre dışı bırakmak için eklenen hello seçeneği.
* En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.
* Tek bölümlü bir koleksiyon için sabit hello devamlılık belirteci hata. Github sorunu #107.
* 0 tek param işlemedeki sabit hello executeStoredProcedure hata. Github sorunu #155.

### <a name="1.10.2"/>1.10.2</a>
* Sabit Kullanıcı Aracısı üstbilgisi tooinclude hello SDK sürümü.
* Küçük kod temizleme.

### <a name="1.10.1"/>1.10.1</a>
* SSL doğrulama hello SDK tootarget hello emulator(hostname=localhost) kullanırken devre dışı bırakılıyor.
* Saklı yordam yürütme sırasında betik günlüğünü etkinleştirme için destek eklendi.

### <a name="1.10.0"/>1.10.0</a>
* Bölüm paralel sorgular çapraz eklenen desteği.
* ÜST/ORDER BY sorguları bölümlenmiş koleksiyonlar için desteği eklendi.

### <a name="1.9.0"/>1.9.0</a>
* Daraltılmış istekleri için eklenen yeniden deneme ilkesi desteği. (Daraltılmış isteklerini bir istek oranı çok büyük özel durumu, hata kodu 429 alır.) Hata kodu 429 karşılaşıldığında, varsayılan olarak, Azure Cosmos DB dokuz kez her istek için uygularken hello retryAfter hello yanıt üstbilgisi sürede yeniden dener. Merhaba yeniden denemeler arasında sunucu tarafından döndürülen tooignore hello retryAfter zaman istiyorsanız sabit yeniden deneme zaman aralığını şimdi hello RetryOptions özelliğinin bir parçası olarak hello ConnectionPolicy nesne üzerinde ayarlanabilir. Azure Cosmos DB şimdi en fazla (bağımsız olarak yeniden deneme sayısı) kısıtlanan ve 429 hata koduyla hello yanıt döndüren her istek için 30 saniye bekler. Bu süre ayrıca hello ConnectionPolicy nesnesindeki RetryOptions özelliği geçersiz kılınabilir.
* Cosmos DB şimdi x-ms-kısıtlama-yeniden deneme-sayısı ve x-ms-throttle-retry-wait-time-ms döndürür her isteği toodenote hello kısıtlama Hello yanıt üstbilgileri hello yeniden denemeler arasında beklenen hello isteği sayısını ve hello toplu süre yeniden deneyin.
* Merhaba RetryOptions sınıfı eklendi, hello RetryOptions özelliği gösterme kullanılan toooverride olabilir hello ConnectionPolicy sınıfı üzerinde bazı hello varsayılan seçenekleri yeniden deneyin.

### <a name="1.8.0"/>1.8.0</a>
* Eklenen hello bölgeli veritabanı hesaplarını desteği.

### <a name="1.7.0"/>1.7.0</a>
* Eklenen hello zamanı tooLive(TTL) özelliğini belgeler için destek.

### <a name="1.6.0"/>1.6.0</a>
* Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Burada, bağlantılar tooa hatalı concat sonuçlarının son döndürdü değil sabit RangePartitionResolver.resolveForRead hata.

### <a name="1.5.5"/>1.5.5</a>
* HashParitionResolver resolveForRead() sabit: ne zaman sağlanan hiçbir bölüm anahtarı atma tüm kayıtlı bağlantıların listesini döndürme yerine bir özel durum.

### <a name="1.5.4"/>1.5.4</a>
* Sorunu giderir [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -ayrılmış HTTPS aracısı: hello genel Aracısı Azure Cosmos DB amacıyla değiştirme kaçının. Ayrılmış bir aracı tüm hello lib'ın istekleri için kullanın.

### <a name="1.5.3"/>1.5.3</a>
* Sorunu giderir [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - düzgün işleyecek medya kimlikleri tire.

### <a name="1.5.2"/>1.5.2</a>
* Sorunu giderir [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -EventEmitter dinleyicisi sızıntısı uyarı.

### <a name="1.5.1"/>1.5.1</a>
* Sorunu giderir [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -klasör karma toohash büyük küçük harfe duyarlı sistemler için yeniden adlandırın.

### <a name="1.5.0"/>1.5.0</a>
* Karma & aralığı bölüm çözümleyiciler ekleyerek parçalama destek uygular.

### <a name="1.4.0"/>1.4.0</a>
* Upsert uygulayın. DocumentClient yeni upsertXXX yöntemleri.

### <a name="1.3.0"/>1.3.0</a>
* Diğer SDK ile hizalama toobring sürüm numaraları atlandı.

### <a name="1.2.2"/>1.2.2</a>
* Bölünmüş Q sarmalayıcı toonew depo taahhüt eder.
* Npm kayıt defteri toopackage dosyasını güncelleştirin.

### <a name="1.2.1"/>1.2.1</a>
* Implements tabanlı yönlendirme kimliği.
* Sorunu giderir [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -geçerli özellik yöntemi current() ile çakışıyor.

### <a name="1.2.0"/>1.2.0</a>
* Jeo-uzamsal dizin desteği eklendi.
* ID özelliği tüm kaynaklar için doğrular. Kaynaklar için kimlikleri içeremez?, /, # &#47; &#47; karakter veya boşluk ile bitmelidir.
* Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.

### <a name="1.1.0"/>1.1.0</a>
* V2 dizin oluşturma ilkesini uygular.

### <a name="1.0.3"/>1.0.3</a>
* Sorun [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - uygulanan eslint grunt hello çekirdek yapılandırmalarını ve SDK veriyoruz.

### <a name="1.0.2"/>1.0.2</a>
* Sorun [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -öneriler sarmalayıcı hata üstbilgiyle içermez.

### <a name="1.0.1"/>1.0.1</a>
* Çakışmaları özelliği tooquery readConflicts, readConflictAsync ve queryConflicts ekleyerek uygulanmadı.
* Güncelleştirilmiş API belgeleri.
* Sorun [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync hata.

### <a name="1.0.0"/>1.0.0</a>
* GA SDK.

## <a name="release--retirement-dates"></a>Yayın & sona erme tarihlerini
Microsoft'un sağladığı bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.

Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle önerilir, her zaman yükseltme toohello en son SDK sürümünün olabildiğince erken.

TooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB olan herhangi bir istek hello hizmeti tarafından reddedilir.

<br/>

| Sürüm | Sürüm tarihi | Sona erme tarihi |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 Ağustos 2017 |--- |
| [1.12.1](#1.12.1) |10 Ağustos 2017 |--- |
| [1.12.0](#1.12.0) |10 Mayıs 2017 |--- |
| [1.11.0](#1.11.0) |16 Mart 2017 |--- |
| [1.10.2](#1.10.2) |27 Ocak 2017 |--- |
| [1.10.1](#1.10.1) |22 aralık 2016 |--- |
| [1.10.0](#1.10.0) |03 Ekim 2016 |--- |
| [1.9.0](#1.9.0) |07 Temmuz 2016 |--- |
| [1.8.0](#1.8.0) |14 Haziran 2016 |--- |
| [1.7.0](#1.7.0) |26 Nisan 2016 |--- |
| [1.6.0](#1.6.0) |29 Mart 2016 |--- |
| [1.5.6](#1.5.6) |08 Mart 2016 |--- |
| [1.5.5](#1.5.5) |02 Şubat 2016 |--- |
| [1.5.4](#1.5.4) |01 Şubat 2016 |--- |
| [1.5.2](#1.5.2) |26 Ocak 2016 |--- |
| [1.5.2](#1.5.2) |22 Ocak 2016 |--- |
| [1.5.1](#1.5.1) |4 Ocak 2016 |--- |
| [1.5.0](#1.5.0) |31 Aralık 2015 |--- |
| [1.4.0](#1.4.0) |06 Ekim 2015 |--- |
| [1.3.0](#1.3.0) |06 Ekim 2015 |--- |
| [1.2.2](#1.2.2) |10 Eylül 2015 |--- |
| [1.2.1](#1.2.1) |15 Ağustos 2015 |--- |
| [1.2.0](#1.2.0) |05 Ağustos 2015 |--- |
| [1.1.0](#1.1.0) |09 Temmuz 2015 |--- |
| [1.0.3](#1.0.3) |04 Haziran 2015 |--- |
| [1.0.2](#1.0.2) |23 Mayıs 2015 |--- |
| [1.0.1](#1.0.1) |15 Mayıs 2015 |--- |
| [1.0.0](#1.0.0) |08 Nisan 2015 |--- |

## <a name="faq"></a>SSS
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Ayrıca bkz.
toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.


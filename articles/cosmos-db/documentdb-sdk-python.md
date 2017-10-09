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
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Azure DB Cosmos Python SDK: sürüm notları ve kaynakları
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

<tr><td>**SDK'sını indirin**</td><td>[Pypı](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**API belgeleri**</td><td>[Python API başvuru belgeleri](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**SDK yükleme yönergeleri**</td><td>[Python SDK yükleme yönergeleri](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**TooSDK katkıda bulunan**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Kullanmaya başlama**</td><td>[Merhaba Python SDK'sı ile çalışmaya başlama](documentdb-python-application.md)</td></tr>

<tr><td>**Geçerli desteklenen platformlar**</td><td>[Python 2.7](https://www.python.org/downloads/) ve [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Sürüm notları
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Yeni bir tutarlılık düzeyi için destek eklendi ConsistentPrefix çağrılır.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Toplama sorguları (sayısı, MIN, MAX, toplam ve ortalama) desteği eklendi.
* SSL doğrulama Cosmos DB öykünücüsüne karşı çalıştırırken devre dışı bırakmak için bir seçenek eklenmiştir.
* Bağımlı istekleri modülü toobe tam olarak 2.10.0 Hello kısıtlamasını kaldırıldı.
* En düşük işleme 10,100 RU/s too2500 RU/s bölümlenmiş koleksiyonlar üzerinde düşürdü.
* Saklı yordam yürütme sırasında betik günlüğünü etkinleştirme için destek eklendi.
* REST API sürümü indirgenmesine çok ' 2017-01-19' Bu sürümde.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Toodocumentation açıklamaları düzenleme değişiklikleri.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Python 3.5 desteği eklendi.
* İstekleri modülünü kullanarak bağlantı havuzu için destek eklendi.
* Oturum tutarlılığı desteği eklendi.
* Bölümlenmiş koleksiyonlar için üst/ORDERBY sorgular için destek eklendi.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Daraltılmış istekleri için eklenen yeniden deneme ilkesi desteği. (Daraltılmış isteklerini bir istek oranı çok büyük özel durumu, hata kodu 429 alır.) Hata kodu 429 karşılaşıldığında, varsayılan olarak, Azure Cosmos DB dokuz kez her istek için uygularken hello retryAfter hello yanıt üstbilgisi sürede yeniden dener. Merhaba yeniden denemeler arasında sunucu tarafından döndürülen tooignore hello retryAfter zaman istiyorsanız sabit yeniden deneme zaman aralığını şimdi hello RetryOptions özelliğinin bir parçası olarak hello ConnectionPolicy nesne üzerinde ayarlanabilir. Azure Cosmos DB şimdi en fazla (bağımsız olarak yeniden deneme sayısı) kısıtlanan ve 429 hata koduyla hello yanıt döndüren her istek için 30 saniye bekler. Bu süre hello ConnectionPolicy nesnesindeki RetryOptions özelliği kılınmadı de olabilir.
* Cosmos DB şimdi x-ms-kısıtlama-yeniden deneme-sayısı ve x-ms-throttle-retry-wait-time-ms döndürür her isteği toodenote hello kısıtlama Hello yanıt üstbilgileri hello yeniden denemeler arasında beklenen hello isteği sayısını ve hello cummulative süre yeniden deneyin.
* Kaldırılan hello RetryPolicy sınıfı ve hello karşılık gelen özelliği (retry_policy) hello document_client sınıfında gösterilir ve bunun yerine hello RetryOptions kullanılan toooverride olabilir ConnectionPolicy sınıfı özellikte gösterme RetryOptions sınıfı sunulan Bazı hello varsayılan seçenekleri yeniden deneyin.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Eklenen hello bölgeli veritabanı hesaplarını desteği.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Eklenen hello zamanı tooLive(TTL) özelliğini belgeler için destek.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Hata düzeltmeleri partitionkey yolundaki tooallow özel karakterlerin bölümleme tooserver yan ilgili.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Uygulanan [bölümlenmiş koleksiyonlar](partition-data.md) ve [kullanıcı tanımlı performans düzeyleri](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Karma & aralığı Ekle Bölüm çözümleyiciler tooassist birden çok bölüm arasında parçalama uygulamalarla.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Upsert uygulayın. Yeni UpsertXXX yöntemler toosupport Upsert özellik eklemiştir.
* Temel kimlik yönlendirme uygulayın. Genel API değişiklik, tüm değişiklikleri iç.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Jeo-uzamsal dizin destekler.
* ID özelliği tüm kaynaklar için doğrular. Kaynaklar için kimlikleri içeremez?, /, #, \, karakter veya boşluk ile bitmelidir.
* Yeni Üstbilgi "dizini dönüştürme ilerleme" tooResourceResponse ekler.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* V2 dizin oluşturma ilkesini uygular.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Proxy bağlantı destekler.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>Yayın & sona erme tarihleri
Microsoft sağlayacaktır bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.

Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle olduğundan bu, her zaman yükseltme toohello son SDK sürümü olabildiğince erken öneririz. 

Tüm istek tooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.

> [!WARNING]
> Python önceki tooversion Merhaba Azure DocumentDB SDK'in tüm sürümleri **1.0.0** üzerinde Çekildi **29 Şubat 2016**. 
> 
> 

<br/>

| Sürüm | Sürüm tarihi | Sona erme tarihi |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 Mayıs 2017 |--- |
| [2.1.0](#2.1.0) |01 May 2017 |--- |
| [2.0.1](#2.0.1) |30 Ekim 2016 |--- |
| [2.0.0](#2.0.0) |29 Eylül 2016 |--- |
| [1.9.0](#1.9.0) |07 Temmuz 2016 |--- |
| [1.8.0](#1.8.0) |14 Haziran 2016 |--- |
| [1.7.0](#1.7.0) |26 Nisan 2016 |--- |
| [1.6.1](#1.6.1) |08 Nisan 2016 |--- |
| [1.6.0](#1.6.0) |29 Mart 2016 |--- |
| [1.5.0](#1.5.0) |03 Ocak 2016 |--- |
| [1.4.2](#1.4.2) |06 Ekim 2015 |--- |
| [1.4.1](#1.4.1) |06 Ekim 2015 |--- |
| [1.2.0](#1.2.0) |06 Ağustos 2015 |--- |
| [1.1.0](#1.1.0) |09 Temmuz 2015 |--- |
| [1.0.1](#1.0.1) |25 Mayıs 2015 |--- |
| [1.0.0](#1.0.0) |07 Nisan 2015 |--- |
| 0.9.4-prelease |14 Ocak 2015 |29 Şubat 2016 |
| 0.9.3-prelease |09 aralık 2014 |29 Şubat 2016 |
| 0.9.2-prelease |25 Kasım 2014 |29 Şubat 2016 |
| 0.9.1-prelease |23 Eylül 2014 |29 Şubat 2016 |
| 0.9.0-prelease |21 Ağustos 2014 |29 Şubat 2016 |

## <a name="faq"></a>SSS
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Ayrıca bkz.
toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası. 


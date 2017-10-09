---
title: "aaaHow tooconfigure Redis bir Premium Azure Redis önbelleği için kümeleri | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Azure Redis önbelleği örnekleri için Premium katman kümeleme Redis yönetme"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Tooconfigure nasıl Redis bir Premium Azure Redis önbelleği için kümeleri
Azure Redis önbelleği önbellek boyutu ve özelliklerin Premium katmanı özellikleri kümeleme, sürdürme ve sanal ağ desteği gibi hello seçimi esneklik sağlayan farklı önbellek teklifleri vardır. Nasıl bir premium kümeleme tooconfigure Azure Redis önbelleği bu makalede örneği.

Diğer premium önbellek özellikleri hakkında daha fazla bilgi için bkz: [giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Redis kümesi nedir?
Azure Redis önbelleği Redis kümesi olarak sunar [Redis içinde uygulanan](http://redis.io/topics/cluster-tutorial). Redis kümesi ile aşağıdaki faydaları hello alın: 

* Merhaba özelliği tooautomatically birden çok düğüm arasında veri kümenizi bölün. 
* Merhaba özelliği toocontinue bir alt hello düğümlerinin hataları yaşıyor veya işlemlerini hello küme hello kalanıyla oluşturulamıyor toocommunicate şunlardır. 
* Daha fazla verimlilik: verimliliğini artırır doğrusal olarak parça hello sayısı arttıkça. 
* Daha fazla bellek boyutu: hello parça sayısı arttıkça doğrusal olarak artırır.  

Boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla bilgi için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

Azure'da Redis kümesi her parça çoğaltma birincil/çoğaltma çiftiyle hello çoğaltma Azure Redis önbelleği hizmeti tarafından yönetildiği sahip olduğu birincil/çoğaltma modeli olarak sunulur. 

## <a name="clustering"></a>Kümeleme
Kümeleme hello üzerinde etkin **yeni Redis önbelleği** dikey önbellek oluşturma sırasında. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Kümeleme hello üzerinde yapılandırılmış **Redis küme** dikey.

![Kümeleme][redis-cache-clustering]

Too10 parça hello kümedeki ayarlamak sahip olabilir. Tıklatın **etkin** hello kaydırıcısını kaydırın ve 1 ile 10 arasında bir sayı yazın **parça sayısı** tıklatıp **Tamam**.

Her parça Azure tarafından yönetilen bir birincil/çoğaltma önbelleği çiftidir ve hello önbelleğinin toplam boyutu hello hello fiyatlandırma katmanı seçili hello önbellek boyutu parça hello sayısını çarparak hesaplanır. 

![Kümeleme][redis-cache-clustering-selected]

Merhaba önbellek oluşturulduktan sonra tooit bağlanın ve yalnızca kümelenmiş olmayan bir önbellek ister ve Redis kullanın hello veri hello önbellek parça genelinde dağıtır. Tanılama ise [etkin](cache-how-to-monitor.md#enable-cache-diagnostics), ölçümleri her parça için ayrı ayrı yakalanır ve olabilir [görüntülenen](cache-how-to-monitor.md) hello Redis önbelleği dikey penceresinde. 

> [!NOTE]
> 
> Kümeleme yapılandırıldığında, istemci uygulamanız gereken bazı küçük farklar vardır. Daha fazla bilgi için bkz: [toomake kümeleme tüm değişiklikleri toomy istemci uygulaması toouse ihtiyacım var?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Merhaba örnek kod hello StackExchange.Redis istemcisi ile kümeleme ile çalışma hakkında bkz [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello kısmı [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) örnek.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Değiştirme hello küme boyutu üzerinde çalışan bir premium önbelleği
Önbellek kümeleme etkinleştirilmiş tıklatmayla toochange hello küme boyutu üzerinde çalışan bir premium **Redis küme boyutu** hello gelen **kaynak menü**.

> [!NOTE]
> Merhaba katmanı bırakıldı Azure Redis önbelleği Premium yayımlanan tooGeneral kullanılabilirlik olsa da, hello Redis küme boyutu özelliği şu anda önizlemede değil.
> 
> 

![Küme boyutu redis][redis-cache-redis-cluster-size]

toochange hello küme boyutu, hello kaydırıcıyı kullanın veya hello 1 ile 10 arasında bir sayı yazın **parça sayısı** metin kutusu ve tıklatın **Tamam** toosave.

> [!NOTE]
> Küme ölçeklendirme çalıştıran hello [geçirme](https://redis.io/commands/migrate) pahalı bir komuttur, komutu, bu nedenle düşük etkili için göz önünde bulundurun yoğun olmayan saatlerde bu işlem çalıştırılmadan. Merhaba geçiş işlemi sırasında bir ani artış sunucu iş yükü görürsünüz. Küme ölçeklendirme uzun işlemi çalışmıyor ve geçen süre miktarı hello anahtarları hello sayısı ve boyutu bu anahtarla ilişkili hello değerlerin bağlıdır.
> 
> 

## <a name="clustering-faq"></a>Kümeleme SSS
Merhaba aşağıdaki listede Azure Redis önbelleği Kümeleme hakkında sorular yanıtlar toocommonly içerir.

* [Kümeleme tüm değişiklikleri toomy istemci uygulaması toouse toomake gerekiyor mu?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Anahtarları bir kümede nasıl dağıtıldığını?](#how-are-keys-distributed-in-a-cluster)
* [Merhaba oluşturabilmeniz için en büyük önbellek boyutu nedir?](#what-is-the-largest-cache-size-i-can-create)
* [Tüm Redis istemcileri kümeleme destekliyor musunuz?](#do-all-redis-clients-support-clustering)
* [Kümeleme etkinleştirildiğinde nasıl toomy önbellek bağlayabilirim?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Doğrudan de toohello tek tek parça my önbelleğin bağlanabilir miyim?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Önceden oluşturulmuş bir önbelleği için kümeleri yapılandırabilir miyim?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Bir temel veya standart önbelleği için kümeleri yapılandırabilir miyim?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Merhaba Redis ASP.NET oturum durumu ve çıktı önbelleği sağlayıcılarıyla kümeleme kullanabilir miyim?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [StackExchange.Redis kullanırken TAŞIMA özel durumlar alıyorum ve kümeleme, ne yapmalıyım?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>Kümeleme tüm değişiklikleri toomy istemci uygulaması toouse toomake gerekiyor mu?
* Yalnızca veritabanı 0 Kümeleme etkin olduğunda kullanılabilir. İstemci uygulamanız birden çok veritabanını kullanır ve 0 dışında tooread veya yazma tooa veritabanı çalışırsa, hello aşağıdaki özel durum oluşur. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Daha fazla bilgi için bkz: [küme belirtimi Redis - uygulanan alt](http://redis.io/topics/cluster-spec#implemented-subset).
* Kullanıyorsanız [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), 1.0.481 kullanın veya sonraki bir sürümü. Toohello önbellek bağlanmak kullanarak, hello aynı [uç noktaları, bağlantı noktalarını ve anahtarları](cache-configure.md#properties) kümeleme özelliği etkinleştirilmiş yok tooa önbellek bağlanırken kullandığınız. Merhaba yalnızca toodatabase 0 tüm okuma ve yazma işlemleri yapılmalıdır farktır.
  
  * Diğer istemciler farklı gereksinimlere sahip. Bkz: [yapmak, tüm Redis istemcileri desteklemek kümeleme?](#do-all-redis-clients-support-clustering)
* Uygulamanız birden çok anahtar işlemleri tek bir komut toplu kullanıyorsa, tüm anahtarları hello bulunmalıdır aynı parça. toolocate anahtarları içinde Merhaba aynı parça, bkz: [nasıl anahtarları dağıtılır bir kümede mi?](#how-are-keys-distributed-in-a-cluster)
* Redis ASP.NET oturum durumu sağlayıcısı kullanıyorsanız 2.0.1 kullanmanız gerekir ya da daha yüksek. Bkz: [hello Redis ASP.NET oturum durumu ve çıktı önbelleği sağlayıcılarıyla kümeleme kullanabilir miyim?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Anahtarları bir kümede nasıl dağıtıldığını?
Merhaba Redis başına [anahtarları dağıtım modeli](http://redis.io/topics/cluster-spec#keys-distribution-model) belgelerine: hello anahtar alanı 16384 yuvaları bölünür. Her anahtar karma ve hello hello küme düğümleri arasında dağıtılmış bu yuva tooone atanmış. Birden çok anahtar bulunan karma tooensure hangi hello anahtarının parçası olan yapılandırabilirsiniz hello karma etiketleri kullanarak aynı parça.

* Başlangıç anahtarı, herhangi bir parçası olarak arasına alınmışsa karma etiketiyle - anahtarları `{` ve `}`, yalnızca başlangıç anahtarı kısmı hello karma yuvası anahtar belirleme hello amacıyla karma haline getirilir. Örneğin, 3 anahtarları aşağıdaki hello hello bulunur aynı parça: `{key}1`, `{key}2`, ve `{key}3` yalnızca hello itibaren `key` hello adının bir parçası karma. Anahtarları karma etiketi belirtimleri tam bir listesi için bkz: [anahtarları karma etiketleri](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Anahtarları bir karma etiketi - hello tüm anahtar adı olmadan, karma oluşturma için kullanılır. Bu bir istatistiksel olarak bile dağıtım hello önbellek hello parça sonuçlanır.

En iyi performans ve verimlilik için hello anahtarları eşit dağıtma öneririz. Bir karma etiketiyle anahtarları kullanıyorsanız hello uygulamanın sorumluluk tooensure hello anahtarları dağılımla yoktur.

Daha fazla bilgi için bkz: [anahtarları dağıtım modeli](http://redis.io/topics/cluster-spec#keys-distribution-model), [küme Redis veri parçalama](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), ve [anahtarları karma etiketleri](http://redis.io/topics/cluster-spec#keys-hash-tags).

Merhaba StackExchange.Redis istemcisi ile aynı parça örnek kod, kümeleme ve anahtarları hello bulma çalışmak için hello bkz [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) hello kısmı [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) örnek.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Merhaba oluşturabilmeniz için en büyük önbellek boyutu nedir?
Merhaba en büyük premium önbellek boyutu 53 GB'dir. En büyük boyutu 530 GB vermiş too10 parça oluşturabilirsiniz. Daha büyük bir boyutu gerekiyorsa yapabilecekleriniz [daha fazla isteği](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Daha fazla bilgi için bkz: [Azure Redis önbelleği fiyatlandırma](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Tüm Redis istemcileri kümeleme destekliyor musunuz?
Merhaba kümeleme tüm istemcileri desteklemek şimdiki zaman Redis. StackExchange.Redis için destek biridir. Merhaba diğer istemciler hakkında daha fazla bilgi için bkz [hello kümeyle çalma](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) hello bölümünü [Redis küme Öğreticisi](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> StackExchange.Redis istemcisi olarak kullanıyorsanız, hello en son sürümünü kullandığınızdan emin olun [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 veya toowork doğru kümeleme daha yeni. Taşıma özel durumlar herhangi bir sorun varsa, bkz: [özel durumlar taşıma](#move-exceptions) daha fazla bilgi için.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Kümeleme etkinleştirildiğinde nasıl toomy önbellek bağlayabilirim?
Tooyour önbellek bağlanabilir kullanarak, hello aynı [uç noktaları](cache-configure.md#properties), [bağlantı noktalarını](cache-configure.md#properties), ve [anahtarları](cache-configure.md#access-keys) kümeleme özelliği etkinleştirilmiş yok tooa önbellek bağlanırken kullandığınız. Redis toomanage aktarıp hello arka uçta kümeleme hello yönetir, istemcisinden.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Doğrudan de toohello tek tek parça my önbelleğin bağlanabilir miyim?
Bu resmi olarak desteklenmez. İle denirse her parça topluca bir önbellek örneği olarak bilinen bir birincil/çoğaltma önbelleği çifti oluşur. Hello hello redis CLI yardımcı programını kullanarak toothese önbelleği örnekleri bağlanabilir [kararsız](http://redis.io/download) github'da hello Redis deponun dalı. Bu sürüm ile Merhaba başlatıldığında temel destek uygulayan `-c` geçin. Daha fazla bilgi için bkz: [hello kümeyle çalma](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) üzerinde [http://redis.io](http://redis.io) hello içinde [Redis küme Öğreticisi](http://redis.io/topics/cluster-tutorial).

Ssl olmayan için aşağıdaki komutları hello kullanın.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

SSL için değiştirme `1300N` ile `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Önceden oluşturulmuş bir önbelleği için kümeleri yapılandırabilir miyim?
Şu anda bir önbellek oluşturduğunuzda, kümeleme yalnızca etkinleştirebilirsiniz. Merhaba küme boyutu hello önbellek oluşturuldu, ancak küme tooa premium önbelleği ekleyemez veya hello önbellek oluşturulduktan sonra bir premium önbellekten kümeleme kaldırmak sonra değiştirebilirsiniz. Premium Önbelleği Etkin kümeleme ve yalnızca bir parça, aynı hiçbir kümeleme boyut hello premium önbelleği farklıdır.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Bir temel veya standart önbelleği için kümeleri yapılandırabilir miyim?
Kümeleme yalnızca premium önbellekler için kullanılabilir.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Merhaba Redis ASP.NET oturum durumu ve çıktı önbelleği sağlayıcılarıyla kümeleme kullanabilir miyim?
* **Çıkış önbelleği sağlayıcısı redis** -gerekli herhangi bir değişiklik.
* **Redis oturum durumu sağlayıcısı** -kümeleme, toouse kullanmalısınız [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ya da daha yüksek veya farklı bir özel durum oluşturulur. Önemli bir değişiklik budur; Daha fazla bilgi için bkz: [v2.0.0 sonu değişiklik ayrıntıları](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>StackExchange.Redis kullanırken TAŞIMA özel durumlar alıyorum ve kümeleme, ne yapmalıyım?
StackExchange.Redis kullanıyorsanız ve alma `MOVE` kümeleme, kullanırken özel durumlar emin olun, kullandığınız [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) veya sonraki bir sürümü. .NET uygulamaları toouse StackExchange.Redis yapılandırma ile ilgili yönergeler için bkz: [hello önbellek istemcilerini yapılandırın](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Sonraki adımlar
Toouse daha premium özellikleri nasıl önbelleğe alma hakkında bilgi edinin.

* [Giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png








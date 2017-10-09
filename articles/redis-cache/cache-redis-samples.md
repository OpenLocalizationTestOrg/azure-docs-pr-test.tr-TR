---
title: "aaaAzure Redis önbelleği örnekleri | Microsoft Docs"
description: "Nasıl toouse Azure Redis önbelleği öğrenin"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Azure Redis önbelleği örnekleri
Bu konu Azure Redis önbelleği örnekleri, tooa önbellek bağlanma, okuma ve bir önbellekten veri tooand yazma ve hello ASP.NET Redis önbelleği sağlayıcılarını kullanma gibi senaryolar kapsayan bir listesini sağlar. Merhaba örnekleri indirilebilir projeleri bazıları ve bazı adım adım yönergeler sağlar ve kod parçaları içeren ancak tooa indirilebilir proje bağlamayın.

## <a name="hello-world-samples"></a>Hello world örnekleri
Bu bölümdeki Hello örnekler hello temellerini tooan Azure Redis önbelleği örneğine bağlanmayı ve okuma ve yazma çeşitli dillerde kullanarak veri toohello önbelleği Göster ve istemcilerin Redis.

Merhaba [Merhaba Dünya](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) örnek gösterir nasıl tooperform çeşitli önbelleğe hello kullanarak işlemleri [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET istemci.

Bu örnek göstermektedir nasıl yapılır:

* Çeşitli bağlantı seçenekleri kullanın
* Zaman uyumlu ve zaman uyumsuz işlemler kullanarak hello önbelleğinden okuma ve yazma nesneleri tooand
* Belirtilen anahtarların Redis MGET/MSET komutları tooreturn değerlerini kullanın
* Redis işlem işlemleri
* Redis listeleri ve sıralanmış kümeleri ile çalışma
* Mağaza .NET nesneleri JsonConvert serileştiricileri kullanma
* Kullanım Redis ayarlar tooimplement etiketleme
* Redis kümesi ile çalışma

Daha fazla bilgi için bkz: Merhaba [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) github'da ve daha fazla kullanım senaryoları için belgelere bakın hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) birim testleri.

[Nasıl toouse Azure Redis önbelleği ile Python](cache-python-get-started.md) tooget Azure Python ve hello kullanarak Redis önbelleği ile çalışmaya nasıl gösterir [redis-py](https://github.com/andymccurdy/redis-py) istemci.

[Merhaba önbelleğinde .NET nesneleriyle çalışma](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) tooand yazmak için tek yönlü tooserialize .NET nesnelerini gösterir okuma bunları bir Azure Redis önbelleği örneği. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>ASP.NET SignalR için bir genişletme devre kartı olarak Redis önbelleği kullanma
Merhaba [genişletme ASP.NET SignalR için devre kartı olarak Redis önbelleği kullanma](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) örneği, Azure Redis önbelleği SignalR devre kartı olarak nasıl kullanabileceğinizi gösterir. Devre kartına hakkında daha fazla bilgi için bkz: [SignalR genişletme Redis ile](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Redis önbelleği müşteri sorgu örnek
Bu örnek bir önbellekten veri erişimi ve kalıcı depolama biriminden verilere erişme arasında karşılaştırır performans gösterir. Bu örnek iki proje yok.

* [Verileri önbelleğe alarak Redis önbelleği performansı nasıl geliştirebilir gösteri](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Çekirdek hello gösteri için veritabanı ve önbellek hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>ASP.NET oturum durumu ve çıktı önbelleği
Merhaba [kullanım Azure Redis önbelleği toostore ASP.NET SessionState ve OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) örnek gösterilmektedir, toouse Azure Redis önbelleği toostore ASP.NET oturumunu ve çıkış önbelleği kullanılarak SessionState ve OutputCache sağlayıcıları için nasıl hello Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Azure Redis önbelleği ile aynı anda MAML Yönet
Merhaba [yönetmek Azure Azure yönetim kitaplıklarını kullanarak Redis önbelleği](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) örnek gösterilmektedir nasıl kullandığınız Azure yönetim kitaplıklarını toomanage - (oluştur / güncelleştir / Sil) önbelleğiniz. 

## <a name="custom-monitoring-sample"></a>Özel örnek izleme
Merhaba [erişim Redis önbelleği izleme verileri](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) örnek gösterilmektedir, Azure Redis önbelleği hello Azure Portal dışında için izleme verilerini nasıl erişebilirsiniz.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>PHP ve Redis kullanılarak yazılmış bir Twitter tarzı kopyalama
Merhaba [Retwis](https://github.com/SyntaxC4-MSFT/retwis) Redis Hello World hello örnektir. Redis ve hello kullanarak PHP kullanılarak yazılmış en az bir Twitter tarzı sosyal ağ kopya olan [Predis](https://github.com/nrk/predis) istemci. Merhaba kaynak kodu tasarlanmış toobe çok basit ve hello aynı tooshow farklı Redis veri yapılarını zaman.

## <a name="bandwidth-monitor"></a>Bant genişliği İzleyicisi
Merhaba [bant genişliği İzleyici](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) örnek hello istemcide kullanılan toomonitor hello bant genişliği sağlar. toomeasure bant genişliği hello hello örnek hello önbellek istemci makine üzerinde çalışan çağrıları toohello önbellek yapmak ve hello bant genişliği İzleyici örnek tarafından bildirilen hello bant genişliği inceleyin.


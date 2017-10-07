---
title: "aaaCache ASP.NET çıktı önbelleği sağlayıcısı"
description: "Bilgi Azure Redis önbelleği kullanılarak toocache ASP.NET sayfa çıktısı nasıl"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>ASP.NET çıktı önbelleği sağlayıcısı Azure Redis önbelleği
Merhaba Redis çıkış önbelleği sağlayıcısı, çıktı önbelleği veriler için bir işlem dışı depolama mekanizmasıdır. Bu veriler için özellikle tam HTTP yanıtları edinilebilir (sayfa çıkış önbelleğe alma). noktasına ASP.NET 4'te tanıtılan hello yeni çıkış önbelleği sağlayıcısı genişletilebilirlik Hello sağlayıcısı takılan.

toouse hello Redis çıkış önbelleği sağlayıcısı önbelleğinizi önce yapılandırın ve hello Redis çıkış önbelleği sağlayıcısı NuGet paketi kullanarak ASP.NET uygulamanızı yapılandırın. Bu konu, uygulama toouse hello Redis çıktı önbelleği sağlayıcısını yapılandırma hakkında yönergeler sağlar. Oluşturma ve bir Azure Redis önbelleği örneği yapılandırma hakkında daha fazla bilgi için bkz: [bir önbellek oluşturma](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>ASP.NET sayfa çıktısının hello önbelleğine depolayabilirsiniz.
tooconfigure hello Redis önbelleği oturum durumu NuGet paketini kullanarak Visual Studio'da bir istemci uygulaması tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.

Çalışma hello hello komuttan aşağıdaki `Package Manager Console` penceresi.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

Merhaba Redis çıkış önbelleği sağlayıcısı NuGet paketi hello StackExchange.Redis.StrongName paketi bir bağımlılığa sahiptir. Merhaba StackExchange.Redis.StrongName paket projenizde mevcut değilse, yüklenir. Merhaba hello Redis çıkış önbelleği sağlayıcısı NuGet paketi hakkında daha fazla bilgi için bkz: [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet sayfası.

>[!NOTE]
>Toplama toohello tanımlayıcı adlı StackExchange.Redis.StrongName paketinde ayrıca hello StackExchange.Redis olmayan-tanımlayıcı adlı sürümü yoktur. Projenizi hello olmayan-tanımlayıcı adlı StackExchange.Redis sürümü kaldırmanız gerekir kullanıyorsanız, aksi takdirde, projenizde adlandırma çakışmaları alın. Bu paketleri hakkında daha fazla bilgi için bkz: [yapılandırma .NET önbellek istemcilerinin](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello paketi indirir ve hello ekler NuGet gerekli derleme başvuruyor ve bölümü web.config dosyanıza aşağıdaki hello ekler. Bu bölümde, ASP.NET uygulama toouse hello Redis çıkış önbelleği sağlayıcısı için hello gerekli yapılandırmayı içerir.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

Merhaba geçersiz kılınan bölüm hello özniteliklerinin ve örnek ayarlarını her özniteliği için bir örnek sağlar.

Merhaba Microsoft Azure Portalı'nda önbellek dikey pencerenizin hello değerlerle Hello öznitelikleri yapılandırmak ve yapılandırmak istediğiniz gibi diğer değerleri hello. Önbellek özelliklerine erişme ile ilgili yönergeler için bkz: [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).

* **ana bilgisayar** – önbellek uç noktasını belirtin.
* **bağlantı noktası** – SSL olmayan bağlantı noktası veya hello ssl ayarlarına bağlı olarak, SSL bağlantı noktası kullanın.
* **accessKey** – önbelleğiniz için ya da hello birincil veya ikincil anahtarı kullanın.
* **SSL** – toosecure önbellek/istemci iletişimleri ile ssl istiyorsanız True, aksi takdirde false. Emin toospecify hello doğru bağlantı noktası olabilir.
  * Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışıdır. Bu ayar toouse hello SSL bağlantı noktası için true belirtin. Merhaba hello SSL olmayan bağlantı noktası etkinleştirme hakkında daha fazla bilgi için bkz: [erişim bağlantı noktaları](cache-configure.md#access-ports) hello bölümünde [bir önbellek yapılandırma](cache-configure.md) konu.
* **Databaseıd** – hangi veritabanı toouse önbelleği için çıktı verilerini belirtilen. Belirtilmezse, 0 hello varsayılan değeri kullanılır.
* **applicationName** – anahtarları redis depolanır `<AppName>_<SessionId>_Data`. Bu adlandırma şeması birden çok uygulamaları tooshare hello etkinleştirir aynı anahtarı. Bu parametre isteğe bağlıdır ve onu belirtmezseniz, varsayılan değer kullanılır.
* **connectionTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello connectTimeout sağlar. Belirtilmezse, 5000 hello varsayılan connectTimeout ayarı kullanılır. Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello syncTimeout sağlar. Belirtilmezse, 1000 hello varsayılan syncTimeout ayar kullanılır. Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).

Toocache hello çıkış istediğiniz bir OutputCache yönergesi tooeach sayfası ekleyin.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

Merhaba önceki örnekte hello sayfası veri kalır hello önbelleğinde 60 saniye boyunca önbelleğe ve hello sayfanın farklı bir sürümünü her parametre birleşimi için önbelleğe alınır. Merhaba OutputCache yönergesi hakkında daha fazla bilgi için bkz: [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Bu adımları gerçekleştirdikten sonra yapılandırılmış toouse hello Redis çıkış önbelleği sağlayıcısı uygulamasıdır.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba denetleyin [Azure Redis önbelleği için ASP.NET oturum durumu sağlayıcısı](cache-aspnet-session-state-provider.md).


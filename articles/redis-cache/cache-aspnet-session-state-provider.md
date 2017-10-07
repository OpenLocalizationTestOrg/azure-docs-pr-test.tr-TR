---
title: "ASP.NET oturum durumu sağlayıcısı aaaCache | Microsoft Docs"
description: "Bilgi toostore ASP.NET oturum durumunu nasıl Azure Redis önbelleği kullanma"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Azure Redis Önbelleği için ASP.NET Oturum Durumu Sağlayıcısı
Azure Redis önbelleği, oturum durumu bellek içi yerine bir önbellek toostore kullanın veya bir SQL Server veritabanı oturum durumu sağlayıcısı sağlar. toouse önbelleğe alma oturum durumu sağlayıcısı Merhaba, önbelleğinizi önce yapılandırın ve hello Redis önbelleği oturum durumu NuGet paketi kullanarak önbelleği için ASP.NET uygulamanızı yapılandırın.

Bu durumu çeşit depolamak için bir kullanıcı oturumu gerçek bulut uygulama tooavoid pratik çoğunlukla değildir, ancak bazı yaklaşımlar diğerlerinden daha fazla performans ve ölçeklenebilirliği etkileyen. Toostore durumu varsa, hello en iyi çözüm durumu küçük tookeep hello miktarı ve tanımlama bilgilerini saklayın. Uygun değilse, hello sonraki en iyi dağıtılmış, bellek içi önbellek için bir sağlayıcı ile toouse ASP.NET oturum durumu çözümüdür. Merhaba kötü performans ve ölçeklenebilirlik açısından toouse veritabanı yedeklenmiş oturum durumu sağlayıcısı çözümüdür. Bu konu, Azure Redis önbelleği için ASP.NET oturum durumu sağlayıcısı hello kullanma hakkında yönergeler sağlar. Diğer oturum durumu seçenekleri hakkında daha fazla bilgi için bkz: [ASP.NET oturum durumu seçenekleri](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Merhaba önbellekte ASP.NET oturum durumunu saklama
tooconfigure hello Redis önbelleği oturum durumu NuGet paketini kullanarak Visual Studio'da bir istemci uygulaması tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.

Çalışma hello hello komuttan aşağıdaki `Package Manager Console` penceresi.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Merhaba hello premium Katmanı'ndan Kümelemesi özelliğini kullanıyorsanız, kullanmalısınız [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ya da daha yüksek veya farklı bir özel durum oluşturulur. Too2.0.1 taşıma veya önemli bir değişiklik daha yüksektir; Daha fazla bilgi için bkz: [v2.0.0 sonu değişiklik ayrıntıları](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Bu makalede güncelleştirme Hello anda hello geçerli bu paket 2.2.3 sürümüdür.
> 
> 

Merhaba Redis oturum durumu sağlayıcısı NuGet paketi hello StackExchange.Redis.StrongName paketi bir bağımlılığa sahiptir. Merhaba StackExchange.Redis.StrongName paket projenizde mevcut değilse, yüklenir.

>[!NOTE]
>Toplama toohello tanımlayıcı adlı StackExchange.Redis.StrongName paketinde ayrıca hello StackExchange.Redis olmayan-tanımlayıcı adlı sürümü yoktur. Projenizi hello olmayan-tanımlayıcı adlı StackExchange.Redis sürümü kaldırmanız gerekir kullanıyorsanız, aksi takdirde, projenizde adlandırma çakışmaları alın. Bu paketleri hakkında daha fazla bilgi için bkz: [yapılandırma .NET önbellek istemcilerinin](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello paketi indirir ve hello ekler NuGet gerekli derleme başvuruyor ve bölümü web.config dosyanıza aşağıdaki hello ekler. Bu bölümde, ASP.NET uygulama toouse hello Redis önbelleği oturum durumu sağlayıcısı için hello gerekli yapılandırmayı içerir.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Merhaba geçersiz kılınan bölüm hello özniteliklerinin ve örnek ayarlarını her özniteliği için bir örnek sağlar.

Merhaba Microsoft Azure Portalı'nda önbellek dikey pencerenizin hello değerlerle Hello öznitelikleri yapılandırmak ve yapılandırmak istediğiniz gibi diğer değerleri hello. Önbellek özelliklerine erişme ile ilgili yönergeler için bkz: [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).

* **ana bilgisayar** – önbellek uç noktasını belirtin.
* **bağlantı noktası** – SSL olmayan bağlantı noktası veya hello ssl ayarlarına bağlı olarak, SSL bağlantı noktası kullanın.
* **accessKey** – önbelleğiniz için ya da hello birincil veya ikincil anahtarı kullanın.
* **SSL** – toosecure önbellek/istemci iletişimleri ile ssl istiyorsanız True, aksi takdirde false. Emin toospecify hello doğru bağlantı noktası olabilir.
  * Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışıdır. Bu ayar toouse hello SSL bağlantı noktası için true belirtin. Merhaba hello SSL olmayan bağlantı noktası etkinleştirme hakkında daha fazla bilgi için bkz: [erişim bağlantı noktaları](cache-configure.md#access-ports) hello bölümünde [bir önbellek yapılandırma](cache-configure.md) konu.
* **throwOnError** – varsa bir hata ya da false hello işlemi toofail sessizce istiyorsanız oluşturulan bir özel durum toobe istiyorsanız true. Merhaba statik Microsoft.Web.Redis.RedisSessionStateProvider.LastException özelliğini kontrol ederek için bir hata kontrol edebilirsiniz. Merhaba varsayılan değer true şeklindedir.
* **retryTimeoutInMilliseconds** – başarısız olan işlemleri milisaniye cinsinden belirtilen bu aralığında denenecek. Merhaba ilk yeniden deneme 20 milisaniye sonra gerçekleşir ve saniyede hello retryTimeoutInMilliseconds aralığı sona erene kadar yeniden denemeler meydana gelir. Bu aralık hemen sonra hello işlemi bir son kez yeniden denenir. Merhaba işlem yine başarısız olursa, hello özel geri hello throwOnError ayarı bağlı olarak toohello çağıran durum oluşur. yeniden deneme yok anlamına gelir 0 Hello varsayılan değerdir.
* **Databaseıd** – hangi veritabanı toouse önbelleği için çıktı verilerini belirtir. Belirtilmezse, 0 hello varsayılan değeri kullanılır.
* **applicationName** – anahtarları redis depolanır `{<Application Name>_<Session ID>}_Data`. Bu adlandırma şeması birden çok uygulama etkinleştirir tooshare hello aynı Redis örneği. Bu parametre isteğe bağlıdır ve onu belirtmezseniz, varsayılan değer kullanılır.
* **connectionTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello connectTimeout sağlar. Belirtilmezse, 5000 hello varsayılan connectTimeout ayarı kullanılır. Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – Bu ayar, hello StackExchange.Redis istemci ayarı toooverride hello syncTimeout sağlar. Belirtilmezse, 1000 hello varsayılan syncTimeout ayar kullanılır. Daha fazla bilgi için bkz: [StackExchange.Redis yapılandırma modeli](http://go.microsoft.com/fwlink/?LinkId=398705).

Bu özellikler hakkında daha fazla bilgi için bkz: hello özgün blog yayını duyurusuna en [Redis için ASP.NET oturum durumu sağlayıcısı Duyurusu](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Merhaba standart InProc oturum durumu sağlayıcısı bölümünde web.config çıkışı toocomment unutmayın.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Bu adımları gerçekleştirdikten sonra yapılandırılmış toouse hello Redis önbelleği oturum durumu sağlayıcısı uygulamasıdır. Uygulamanızda oturum durumu kullandığınızda, bir Azure Redis önbelleği örneği depolanır.

> [!IMPORTANT]
> Merhaba önbellekte depolanan veriler, seri hale getirilebilir, hello depolanabilir hello veri aksine bellek içi ASP.NET oturum durumu sağlayıcısı varsayılan. Merhaba Redis oturum durumu Sağlayıcısı kullanıldığında, oturum durumu içinde depolanan hello veri türleri seri hale getirilebilir olduğundan emin olun.
> 
> 

## <a name="aspnet-session-state-options"></a>ASP.NET oturum durumu seçenekleri
* Bellek oturum durumu sağlayıcısı - bu sağlayıcı hello oturum durumu bellekte depolar. Bu sağlayıcı kullanmanın hello avantajı, basit ve hızlı ' dir. Ancak değil dağıtılmış beri bellek sağlayıcısında kullanıyorsanız, Web uygulamalarınızı ölçeklendirme olamaz.
* SQL Server oturum durumu sağlayıcısı - bu sağlayıcı hello oturum durumu Sql Server içinde depolar. Toostore hello oturum durumu kalıcı depolama alanına istiyorsanız bu sağlayıcıyı kullanın. Web uygulamanızı ölçeklendirebilirsiniz ancak oturum açmak için Sql Server kullanan Web uygulamanıza bir performans etkisi olur.
* Dağıtılmış bellek oturum durumu sağlayıcısı gibi Redis, önbelleği oturum durumu sağlayıcısı - iki açıdan da hello bu sağlayıcı sağlar. Web uygulamanızı basit, hızlı ve ölçeklenebilir bir oturum durumu sağlayıcısı olabilir. Bu sağlayıcı depoları hello bir önbellekte uygulamanız oturum durumu tootake dikkate sahip olduğu tüm tooa geçici ağ hataları gibi belirli bir önbellek dağıtılmış konuşurken ilişkili özelliklere hello. Önbellek kullanımı en iyi uygulamalar için bkz: [Kılavuzu önbelleğe alma](../best-practices-caching.md) Microsoft Patterns & yöntemler [Azure bulut uygulama tasarımı ve Uygulama Kılavuzu](https://github.com/mspnp/azure-guidance).

Oturum durumu ve diğer en iyi uygulamalar hakkında daha fazla bilgi için bkz: [Web geliştirme en iyi yöntemler (yapı gerçek bulut uygulamaları Azure ile)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Sonraki adımlar
Merhaba denetleyin [Azure Redis önbelleği için ASP.NET çıktı önbelleği sağlayıcısı](cache-aspnet-output-cache-provider.md).


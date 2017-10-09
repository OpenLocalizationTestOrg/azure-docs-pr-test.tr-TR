---
title: "Azure App Service'teki Azure Redis önbelleği ile aaaSession durumu"
description: "Toouse nasıl hello Azure önbellek hizmeti toosupport ASP.NET oturum durumu önbelleğe alma hakkında bilgi edinin."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Azure App Service’teki Azure Redis Cache ile oturum durumu
Bu konuda nasıl toouse hello Azure Redis önbelleği hizmeti oturum durumu için açıklanmaktadır.

ASP.NET web uygulamanız oturum durumu kullanıyorsa, tooconfigure bir dış oturum durumu sağlayıcısı (Merhaba Redis önbelleği hizmeti veya SQL Server oturum durumu sağlayıcısı) gerekir. Oturum durumu kullanıyor ancak dış sağlayıcı kullanmayın, web uygulamanızın sınırlı tooone örneği olacaktır. Merhaba Redis önbelleği hizmeti hello hızlı ve kolay tooenable ' dir.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Merhaba önbelleği oluşturma
İzleyin [şu yönergeleri](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello önbelleği.

## <a id="configureproject"></a>Merhaba RedisSessionStateProvider NuGet paketi tooyour web uygulaması Ekle
Merhaba NuGet yükleme `RedisSessionStateProvider` paket.  Kullanım hello şu komutu tooinstall hello Paket Yöneticisi Konsolu'ndan (**Araçları** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

gelen tooinstall **Araçları** > **NuGet Paket Yöneticisi** > **çözüm için NugGet paketlerini Yönet**, arama `RedisSessionStateProvider`.

Daha fazla bilgi için bkz: Merhaba [NuGet RedisSessionStateProvider sayfası](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) ve [yapılandırma hello önbellek istemcisi](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Merhaba Web.Config dosyasını değiştirme
Ayrıca önbelleği için toomaking bütünleştirilmiş koduna başvuruyor, hello NuGet paketi hello saplama girdileri ekler *web.config* dosya. 

1. Açık hello *web.config* ve hello hello bulur **sessionState** öğesi.
2. Merhaba değerlerini girin `host`, `accessKey`, `port` (Merhaba SSL bağlantı noktası 6380 olmalıdır) ve `SSL` çok`true`. Bu değerleri hello elde edilebilir [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) dikey penceresinde, önbellek örneğinizin. Daha fazla bilgi için bkz: [toohello Önbelleği'ne bağlama](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışı olduğunu unutmayın. Merhaba hello SSL olmayan bağlantı noktası etkinleştirme hakkında daha fazla bilgi için bkz: [erişim bağlantı noktaları](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) hello bölümünde [Azure Redis Önbelleği'nde bir önbellek yapılandırma](https://msdn.microsoft.com/library/azure/dn793612.aspx) konu. Merhaba aşağıdaki biçimlendirmeyi gösterir hello değişiklikleri toohello *web.config* dosya, özellikle hello değişiklikleri çok*bağlantı noktası*, *konak*, accessKey *, ve *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Merhaba oturum nesnesi kullanma
Merhaba son adım, ASP.NET kodunuzda hello oturum nesnesi kullanarak toobegin ' dir. Hello kullanarak nesneleri toosession durumu eklemek **Session.Add** yöntemi. Bu yöntem, anahtar-değer çiftleri toostore öğeleri hello oturum durumu önbelleğine kullanır.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

koddan hello oturum durumundan bu değeri alır.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

Web uygulamanızda hello Redis önbelleği toocache nesneler de kullanabilirsiniz. Daha fazla bilgi için bkz. [15 dakikada Azure Redis Cache ile MVC film uygulaması](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Nasıl hakkında daha fazla ayrıntı için toouse ASP.NET oturum durumu, bkz: [ASP.NET oturum durumuna genel bakış][ASP.NET Session State Overview].

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png


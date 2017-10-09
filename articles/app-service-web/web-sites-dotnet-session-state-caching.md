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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="041f9-103">Azure App Service’teki Azure Redis Cache ile oturum durumu</span><span class="sxs-lookup"><span data-stu-id="041f9-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="041f9-104">Bu konuda nasıl toouse hello Azure Redis önbelleği hizmeti oturum durumu için açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="041f9-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="041f9-105">ASP.NET web uygulamanız oturum durumu kullanıyorsa, tooconfigure bir dış oturum durumu sağlayıcısı (Merhaba Redis önbelleği hizmeti veya SQL Server oturum durumu sağlayıcısı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="041f9-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="041f9-106">Oturum durumu kullanıyor ancak dış sağlayıcı kullanmayın, web uygulamanızın sınırlı tooone örneği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="041f9-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="041f9-107">Merhaba Redis önbelleği hizmeti hello hızlı ve kolay tooenable ' dir.</span><span class="sxs-lookup"><span data-stu-id="041f9-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="041f9-108"><a id="createcache"></a>Merhaba önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="041f9-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="041f9-109">İzleyin [şu yönergeleri](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello önbelleği.</span><span class="sxs-lookup"><span data-stu-id="041f9-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="041f9-110"><a id="configureproject"></a>Merhaba RedisSessionStateProvider NuGet paketi tooyour web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="041f9-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="041f9-111">Merhaba NuGet yükleme `RedisSessionStateProvider` paket.</span><span class="sxs-lookup"><span data-stu-id="041f9-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="041f9-112">Kullanım hello şu komutu tooinstall hello Paket Yöneticisi Konsolu'ndan (**Araçları** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**):</span><span class="sxs-lookup"><span data-stu-id="041f9-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="041f9-113">gelen tooinstall **Araçları** > **NuGet Paket Yöneticisi** > **çözüm için NugGet paketlerini Yönet**, arama `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="041f9-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="041f9-114">Daha fazla bilgi için bkz: Merhaba [NuGet RedisSessionStateProvider sayfası](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) ve [yapılandırma hello önbellek istemcisi](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="041f9-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="041f9-115"><a id="configurewebconfig"></a>Merhaba Web.Config dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="041f9-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="041f9-116">Ayrıca önbelleği için toomaking bütünleştirilmiş koduna başvuruyor, hello NuGet paketi hello saplama girdileri ekler *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="041f9-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="041f9-117">Açık hello *web.config* ve hello hello bulur **sessionState** öğesi.</span><span class="sxs-lookup"><span data-stu-id="041f9-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="041f9-118">Merhaba değerlerini girin `host`, `accessKey`, `port` (Merhaba SSL bağlantı noktası 6380 olmalıdır) ve `SSL` çok`true`.</span><span class="sxs-lookup"><span data-stu-id="041f9-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="041f9-119">Bu değerleri hello elde edilebilir [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) dikey penceresinde, önbellek örneğinizin.</span><span class="sxs-lookup"><span data-stu-id="041f9-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="041f9-120">Daha fazla bilgi için bkz: [toohello Önbelleği'ne bağlama](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="041f9-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="041f9-121">Merhaba SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="041f9-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="041f9-122">Merhaba hello SSL olmayan bağlantı noktası etkinleştirme hakkında daha fazla bilgi için bkz: [erişim bağlantı noktaları](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) hello bölümünde [Azure Redis Önbelleği'nde bir önbellek yapılandırma](https://msdn.microsoft.com/library/azure/dn793612.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="041f9-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="041f9-123">Merhaba aşağıdaki biçimlendirmeyi gösterir hello değişiklikleri toohello *web.config* dosya, özellikle hello değişiklikleri çok*bağlantı noktası*, *konak*, accessKey *, ve *ssl*.</span><span class="sxs-lookup"><span data-stu-id="041f9-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="041f9-124"><a id="usesessionobject"></a>Merhaba oturum nesnesi kullanma</span><span class="sxs-lookup"><span data-stu-id="041f9-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="041f9-125">Merhaba son adım, ASP.NET kodunuzda hello oturum nesnesi kullanarak toobegin ' dir.</span><span class="sxs-lookup"><span data-stu-id="041f9-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="041f9-126">Hello kullanarak nesneleri toosession durumu eklemek **Session.Add** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="041f9-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="041f9-127">Bu yöntem, anahtar-değer çiftleri toostore öğeleri hello oturum durumu önbelleğine kullanır.</span><span class="sxs-lookup"><span data-stu-id="041f9-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="041f9-128">koddan hello oturum durumundan bu değeri alır.</span><span class="sxs-lookup"><span data-stu-id="041f9-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="041f9-129">Web uygulamanızda hello Redis önbelleği toocache nesneler de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="041f9-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="041f9-130">Daha fazla bilgi için bkz. [15 dakikada Azure Redis Cache ile MVC film uygulaması](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="041f9-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="041f9-131">Nasıl hakkında daha fazla ayrıntı için toouse ASP.NET oturum durumu, bkz: [ASP.NET oturum durumuna genel bakış][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="041f9-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="041f9-132">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="041f9-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="041f9-133">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="041f9-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="041f9-134">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="041f9-134">What's changed</span></span>
* <span data-ttu-id="041f9-135">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="041f9-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="041f9-136">*Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="041f9-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

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


---
title: "Azure App Service’teki Azure Redis Cache ile oturum durumu"
description: "ASP.NET oturum durumu önbelleğe alma işlemini desteklemek için Azure Önbellek Hizmeti’ni nasıl kullanacağınızı öğrenin."
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="aeb17-103">Azure App Service’teki Azure Redis Cache ile oturum durumu</span><span class="sxs-lookup"><span data-stu-id="aeb17-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="aeb17-104">Bu konuda, oturum durumu için Azure Redis Cache Hizmetini nasıl kullanacağınız açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aeb17-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="aeb17-105">ASP.NET web uygulamanız oturum durumu kullanıyorsa, bir dış oturum durumu sağlayıcısı (Redis Cache Hizmeti veya SQL Server oturum durumu sağlayıcısı) yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aeb17-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="aeb17-106">Oturum durumu kullanıyor, ancak dış sağlayıcı kullanmıyorsanız; web uygulamanızın tek bir örneği ile sınırlı kalırsınız.</span><span class="sxs-lookup"><span data-stu-id="aeb17-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="aeb17-107">Redis Cache Hizmeti etkinleştirmesi en hızlı ve en kolay hizmettir.</span><span class="sxs-lookup"><span data-stu-id="aeb17-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="aeb17-108"><a id="createcache"></a>Önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="aeb17-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="aeb17-109">Önbelleği oluşturmak için [şu yönergeleri](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) uygulayın.</span><span class="sxs-lookup"><span data-stu-id="aeb17-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="aeb17-110"><a id="configureproject"></a>Web uygulamanıza RedisSessionStateProvider NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="aeb17-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="aeb17-111">NuGet `RedisSessionStateProvider` paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aeb17-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="aeb17-112">Paket yöneticisi konsolundan (**Araçlar** > **NuGet Paketi Yöneticisi** > **Paket Yöneticisi Konsolu**) yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="aeb17-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="aeb17-113">**Araçlar** > **NuGet Paketi Yöneticisi** > **Çözüm için NugGet Paketlerini Yönet** konumuna gidin ve `RedisSessionStateProvider` araması yapın.</span><span class="sxs-lookup"><span data-stu-id="aeb17-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="aeb17-114">Daha fazla bilgi için bkz. [NuGet RedisSessionStateProvider sayfası](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) ve [Önbellek istemcisini yapılandırma](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="aeb17-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="aeb17-115"><a id="configurewebconfig"></a>Web.Config Dosyasını Değiştirme</span><span class="sxs-lookup"><span data-stu-id="aeb17-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="aeb17-116">NuGet paketi derleme başvuruları için yapmanın yanı sıra, *web.config* dosyasında saplama girdileri ekler.</span><span class="sxs-lookup"><span data-stu-id="aeb17-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="aeb17-117">*web.config* dosyasını açın ve **sessionState** öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="aeb17-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="aeb17-118">`host`, `accessKey`, `port` için değerleri girin (SSL bağlantı noktası 6380 olmalıdır) `SSL` değerini `true` olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="aeb17-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="aeb17-119">Bu değerleri, önbellek örneğinizin [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) dikey penceresinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aeb17-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="aeb17-120">Daha fazla bilgi için bkz. [Önbelleğe bağlanma](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="aeb17-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="aeb17-121">SSL olmayan bağlantı noktasının yeni önbellekler için varsayılan olarak devre dışı bırakıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aeb17-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="aeb17-122">SSL olmayan bağlantı noktasını etkinleştirme hakkında daha fazla bilgi için [Azure Redis Cache’te bir önbellek yapılandırma](https://msdn.microsoft.com/library/azure/dn793612.aspx) konusundaki [Erişim Bağlantı Noktaları](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="aeb17-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="aeb17-123">Aşağıdaki biçimlendirmede değişiklikler gösterilir *web.config* dosya, özellikle *bağlantı noktası*, *konak*, accessKey *, ve *ssl* .</span><span class="sxs-lookup"><span data-stu-id="aeb17-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="aeb17-124"><a id="usesessionobject"></a>Kodlarda Oturum Nesnesi Kullanma</span><span class="sxs-lookup"><span data-stu-id="aeb17-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="aeb17-125">Son adım, ASP.NET kodunuzda Oturum nesnesi kullanmaya başlamaktır.</span><span class="sxs-lookup"><span data-stu-id="aeb17-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="aeb17-126">**Session.Add** yöntemini kullanarak nesneleri oturum durumuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aeb17-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="aeb17-127">Bu yöntem, öğeleri oturum durumu önbelleğine depolamak için anahtar-değer çiftlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="aeb17-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="aeb17-128">Aşağıdaki kod, oturum durumundan bu değeri alır.</span><span class="sxs-lookup"><span data-stu-id="aeb17-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="aeb17-129">Web uygulamanızdaki nesneleri önbelleğe almak için Redis Cache’i de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aeb17-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="aeb17-130">Daha fazla bilgi için bkz. [15 dakikada Azure Redis Cache ile MVC film uygulaması](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="aeb17-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="aeb17-131">ASP.NET oturum durumu kullanma hakkında daha fazla ayrıntı için bkz. [ASP.NET Oturum Durumuna Genel Bakış][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="aeb17-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="aeb17-132">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="aeb17-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="aeb17-133">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aeb17-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="aeb17-134">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="aeb17-134">What's changed</span></span>
* <span data-ttu-id="aeb17-135">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="aeb17-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="aeb17-136">*Gönderen [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="aeb17-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png


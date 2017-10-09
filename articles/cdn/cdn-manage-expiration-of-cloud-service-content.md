---
title: "web içeriğinin Azure CDN aaaManage sona erme | Microsoft Docs"
description: "Bilgi nasıl Azure CDN Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS içeriğinde toomanage sona erme tarihi."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Azure CDN Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS içeriğinin kullanım süresini yönetme
> [!div class="op_single_selector"]
> * [Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure depolama blob hizmeti](cdn-manage-expiration-of-blob-content.md)
> 
> 

Kendi yaşam süresi (TTL) geçen kadar herhangi bir genel olarak erişilebilir kaynak web sunucusuna dosyalarından Azure CDN'de önbelleğe alınabilir.  Merhaba TTL hello tarafından belirlenir [ *Cache-Control* üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello kaynak sunucudan hello HTTP yanıt.  Bu makalede nasıl tooset `Cache-Control` Azure Web uygulamaları, Azure bulut Hizmetleri, ASP.NET uygulamaları ve bunların tümü benzer şekilde yapılandırılmış, Internet Information Services siteleri için üstbilgiler.

> [!TIP]
> Bir dosya üzerinde hiçbir TTL tooset seçebilirsiniz.  Bu durumda, Azure CDN varsayılan TTL yedi gün otomatik olarak uygular.
> 
> Hello Azure CDN toospeed erişim toofiles ve diğer kaynakların nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Cache-Control üstbilgileri yapılandırmasında ayarlama
Görüntüleri ve stil sayfalarını gibi statik içerik hello güncelleştirme sıklığı hello değiştirerek denetleyebilirsiniz **applicationHost.config** veya **web.config** web uygulamanız için dosyaları.  Merhaba **system.webServer\staticContent\clientCache** hello yapılandırma dosyası öğesi hello ayarlayacak `Cache-Control` içeriğiniz için üstbilgi. İçin **web.config**, hello yapılandırma ayarlarını etkiler her şeyi hello klasör ve tüm alt klasörlerde hello alt düzeyinde geçersiz kılınmadığı sürece.  Örneğin, bir varsayılan yaşam süresi sırasında tüm statik içeriği 3 gün boyunca önbelleğe alınmış, ancak daha fazla değişken 6 saat ile bir önbellek ayarı içerik sahip bir alt klasörünüz hello kök toohave ayarlayabilirsiniz.  İçin **applicationHost.config**, hello sitedeki tüm uygulamaları etkiler ancak geçersiz kılınabilir **web.config** hello uygulamalarında dosyaları.

Merhaba aşağıdaki XML örneği ayarı gösterilmektedir **clientCache** en uzun geçerlilik süresi 3 günlük bir toospecify:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Belirtme **UseMaxAge** ekler bir `Cache-Control: max-age=<nnn>` hello belirtilen hello değere dayanarak üstbilgi toohello yanıt **CacheControlMaxAge** özniteliği. Merhaba hello timespan biçimidir Merhaba **cacheControlMaxAge** özniteliği <days>.<hours>:<min>:<sec>. Merhaba hakkında daha fazla bilgi için **clientCache** düğümü, bkz: [istemci önbelleği <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Cache-Control üstbilgileri kodda ayarlama
ASP.NET uygulamaları için hello CDN önbelleğe alma davranışını programlı olarak ayarlama hello tarafından ayarlayabileceğiniz **HttpResponse.Cache** özelliği. Merhaba hakkında daha fazla bilgi için **HttpResponse.Cache** özelliği, bkz: [HttpResponse.Cache özelliği](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) ve [HttpCachePolicy sınıfı](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

ASP.NET tooprogrammatically önbellek uygulama içeriği istiyorsanız hello içerik HttpCacheability çok ayarlayarak olarak alınabilir işaretli olduğundan emin olun*ortak*. Ayrıca, bir önbellek Doğrulayıcı ayarlandığından emin olun. Merhaba önbellek Doğrulayıcı son değişiklik olabilir SetLastModified ya da bir etag değeri aranarak zaman damgası ayarlamak SetETag çağırarak. İsteğe bağlı olarak, SetExpires çağırarak bir önbellek süre sonu zamanı belirtebilirsiniz veya hello varsayılan önbellek buluşsal yöntemler bu belgenin önceki bölümlerinde açıklanan bağlı.  

Örneğin, bir saat toocache içerik hello aşağıdakileri ekleyin:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Sonraki Adımlar
* [Merhaba ayrıntılarını okumak **clientCache** öğesi](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Merhaba Hello belgelerini okuyun **HttpResponse.Cache** özelliği](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Merhaba Hello belgelerini okuyun **HttpCachePolicy sınıfı**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  


---
title: "bir App Service web uygulaması tooRedis hello Memcache Protokolü - Azure aracılığıyla aaaConnect | Microsoft Docs"
description: "Bir web uygulamasını Azure App service tooRedis önbellek bağlanmak hello Memcache protokolünü kullanarak"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Bir web uygulamasını Azure App Service tooRedis önbellek hello Memcache protokolü aracılığıyla bağlanma
Bu makalede, nasıl tooconnect bir WordPress web uygulamasında öğreneceksiniz [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) çok[Azure Redis önbelleği] [ 12] hello kullanarak [Memcache] [ 13] protokolü. Bellek içi önbelleğe alma işlemi için Memcached sunucusu kullanan mevcut bir web uygulaması varsa, tooAzure uygulama hizmeti ve kullanım hello birinci taraf önbelleğe alma çözümünü Microsoft Azure'un çok az kayıpla veya hiç değişiklik tooyour uygulama kodu ile geçirebilirsiniz. Ayrıca, mevcut Memcache UZMANLIĞINIZDAN toocreate düzeyde ölçeklenebilir, dağıtılmış uygulamalarınızı Azure Redis önbelleği ile Azure App Service'te bellek içi, .NET, PHP, Node.js, Java ve Python gibi popüler uygulama çerçevelerini kullanırken önbelleğe alma için kullanabilirsiniz.  

App Service Web Apps çağrıları tooAzure Redis önbelleği önbelleğe alma işlemi için bir Memcache Ara sunucusu olarak davranan yerel bir Memcached sunucusu olan hello Web Apps Memcache dolgusu ile bu uygulama senaryosuna sağlar. Redis önbelleği ile Merhaba Memcache Protokolü toocache verileri kullanarak iletişim kuran herhangi bir uygulama sağlar. Merhaba Memcache protokolünü kullanarak iletişim kurdukları sürece, herhangi bir uygulama veya uygulama çerçevesi tarafından kullanılabilmesi için bu Memcache dolgusu hello protokol düzeyinde çalışır.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Ön koşullar
Merhaba Memcache protokolünü kullanarak iletişim sağlanan hello Web Apps Memcache dolgusunu herhangi bir uygulama ile kullanılabilir. Söz konusu örnekte hello Azure Marketi sağlanabilir bir ölçeklenebilir WordPress sitesi hello başvuru uygulamasıdır.

Aşağıdaki makalelerde açıklanan başlangıç adımları izleyin:

* [Hello Azure Redis önbelleği hizmeti örneği sağlama][0]
* [Azure'da Ölçeklenebilir WordPress sitesi dağıtma][1]

Dağıtılan hello ölçeklenebilir WordPress sitesini ve sağlanan bir Redis önbelleği örneğine sahip olduktan sonra hello Azure App Service Web Apps Memcache dolgusunu etkinleştirme ile hazır tooproceed olacaktır.

## Merhaba Web Apps Memcache dolgusunu etkinleştirme
Sipariş tooconfigure Memcache dolgusunu üç uygulama ayarı oluşturmanız gerekir. Bu yapılabilir çeşitli hello dahil olmak üzere yöntemler kullanarak [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), hello [Klasik portal][3], hello [Azure PowerShell cmdlet'leri] [ 5] veya hello [Azure komut satırı arabirimi][5]. Bu post Hello amaçlarla toouse hello yapacağım [Azure Portal] [ 4] tooset hello uygulaması ayarları. Merhaba aşağıdaki değerleri penceresinden alınabilir **ayarları** Redis önbelleği örneğinizi dikey.

![Azure Redis Cache Ayarları Dikey Penceresi](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### REDIS_HOST uygulama ayarı ekleme
Merhaba ilk uygulama ayarı toocreate olan hello **REDIS\_KONAK** uygulama ayarı. Bu ayar hello hedef toowhich hello dolgusu ileten hello önbellek bilgilerini ayarlar. Merhaba hello redıs_host uygulama ayarı hello alınabilir için gereken değer **özellikleri** Redis önbelleği örneğinizi dikey.

![Azure Redis Cache Ana Bilgisayar Adı](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Merhaba uygulama çok ayar kümesi hello anahtar**REDIS\_KONAK** ve hello uygulama ayarı toohello hello değerini **ana bilgisayar adı** hello Redis önbelleği örneğinin.

![Web Uygulaması Uygulama Ayarı REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### REDIS_KEY uygulama ayarı ekleme
Merhaba ikinci uygulama ayarı toocreate olan hello **REDIS\_anahtar** uygulama ayarı. Bu ayar hello kimlik doğrulama belirteci gerekli toosecurely erişim hello Redis önbelleği örneği sağlar. Merhaba değer hello hello redıs_key uygulama ayarı için gerekli alabilir **erişim anahtarları** dikey penceresinde hello Redis önbelleği örneğinin.

![Azure Redis Cache Birincil Anahtarı](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Merhaba uygulama çok ayar kümesi hello anahtar**REDIS\_anahtar** ve hello uygulama ayarı toohello hello değerini **birincil anahtar** hello Redis önbelleği örneğinin.

![Azure Web Sitesi Uygulama Ayarı REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### MEMCACHESHIM_REDIS_ENABLE uygulama ayarı ekleme
Merhaba son uygulama ayarı redıs_host ve redıs_key tooconnect toohello Azure Redis önbelleği ve iletme hello önbellek çağrıları kullanan hello Web Apps Memcache dolgusunu kullanılan tooenable hello ' dir. Merhaba uygulama çok ayar kümesi hello anahtar**MEMCACHESHIM\_REDIS\_etkinleştirmek** ve değeri çok hello**doğru**.

![Web Uygulaması Uygulama Ayarı MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Ekleme hello üç (3) uygulama ayarları tamamladıktan sonra tıklatın **kaydetmek**.

## PHP için Memcache uzantısını etkinleştirme
Merhaba uygulama toospeak hello Memcache protokolü için sırayla gerekli tooinstall hello Memcache uzantısını tooPHP--hello WordPress sitenizin dil çerçevesi olan.

### Merhaba php_memcache uzantısını indirme
Çok Gözat[PECL][6]. Kategori önbelleğe alma hello altında tıklatın [memcache][7]. Merhaba yüklemeleri sütunu altında hello DLL bağlantısına tıklayın.

![PHP PECL Web Sitesi](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Merhaba olmayan iş parçacığı güvenli (NTS) x86 bağlantı hello Web Apps'de etkin PHP sürümü için indirin. (Varsayılan PHP 5.4 sürümüdür)

![PHP PECL Web Sitesi Memcache Paketi](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Merhaba php_memcache uzantısını etkinleştirme
Merhaba dosyasını indirdikten sonra sıkıştırmasını açın ve hello karşıya **php\_memcache.dll** hello içine **d:\\ev\\site\\wwwroot\\bin\\ext\\**  dizini. Merhaba php_memcache.dll hello web uygulamasına yüklendikten sonra tooenable hello uzantısı toohello PHP çalışma zamanı gerekir. tooenable hello hello Azure Portal, açık hello Memcache uzantısını **uygulama ayarları** hello web uygulaması dikey penceresinde hello anahtarıyla sonra yeni bir uygulama ayarı Ekle **PHP\_UZANTILARI** ve hello değer **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Hello web uygulaması birden fazla PHP uzantısı tooload gerekirse, php_extensıons hello değerini göreli yollar tooDLL dosyaları virgülle ayrılmış listesi olmalıdır.
> 
> 

![Web Uygulaması Uygulama Ayarı PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

İşlemi tamamladıktan sonra **Kaydet**’e tıklayın.

## Memcache WordPress eklentisini yükleme
> [!NOTE]
> Merhaba de indirebilirsiniz [Memcached nesne önbelleği eklentisi](https://wordpress.org/plugins/memcached/) WordPress.org gelen.
> 
> 

Merhaba WordPress eklentileri sayfasında, tıklatın **yeni Ekle**.

![WordPress Eklenti Sayfası](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Merhaba arama kutusuna yazın **memcached** ve basın **Enter**.

![WordPress Yeni Eklenti Ekleme](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Bul **Memcached nesne önbelleği** hello listesinde, ardından **Şimdi Yükle**.

![WordPress Memcache Eklentisini Yükleme](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Merhaba Memcache WordPress eklentisini etkinleştirme
> [!NOTE]
> Bu Web günlüğündeki Hello yönergelerini izleyin [nasıl tooenable Site uzantısı Web uygulamaları '] [ 8] tooinstall Visual Studio Team Services.
> 
> 

Merhaba, `wp-config.php` dosya, hello Dur düzenleme yorum hello dosya hello sona yukarıdaki kodu aşağıdaki hello ekleyin.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Bu kod yapıştırıldıktan sonra monaco hello belgeyi otomatik olarak kaydedin.

Merhaba sonraki tooenable hello nesne önbelleği eklentisini adımdır. Bu sürükleme ve bırakma yapılır **object-cache.php** gelen **wp-içerik/plugins/memcached** klasörü toohello **wp-content** klasörü tooenable hello Memcache nesne Önbellek işlevselliği.

![Merhaba memcache object-cache.php eklentisini bulma](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Şimdi bu hello **object-cache.php** dosyasıdır hello **wp-content** klasörü, hello Memcached nesne önbelleği şimdi etkinleştirildi.

![Merhaba memcache object-cache.php eklentisini etkinleştirme](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Merhaba Memcache nesne önbelleği uzantısının çalıştığını doğrulayın
Tüm hello adımları tooenable hello Web Apps Memcache dolgusunu şimdi tamamlandı. Merhaba tek şey hello veri Redis önbelleği örneğinizi doldurduğunu tooverify ' dir.

### Azure Redis önbelleği Hello SSL olmayan bağlantı noktası desteğini etkinleştir
> [!NOTE]
> Bu makale yazıldığı hello zaman hello Redis CLI SSL bağlantısını desteklemez, dolayısıyla hello aşağıdaki adımlar gereklidir.
> 
> 

Hello Azure portalı, bu web uygulaması için oluşturduğunuz toohello Redis önbelleği örneğine göz atın. Merhaba önbelleğin dikey penceresi açıldıktan sonra hello tıklatın **ayarları** simgesi.

![Azure Redis Cache Ayarları Düğmesi](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Seçin **erişim bağlantı noktaları** hello listeden.

![Azure Redis Cache Erişim Bağlantı Noktası](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

**Yalnızca SSL aracılığıyla erişime izin ver** seçeneği için **Hayır**’a tıklayın.

![Azure Redis Cache Erişim Bağlantı Noktası Yalnızca SSL](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Merhaba SSL olmayan bağlantı noktasının şimdi ayarlandığını görürsünüz. **Kaydet** düğmesine tıklayın.

![Azure Redis Cache Redis Erişim Portalı SSL Olmayan](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### TooAzure Redis önbelleği redis-cli Bağlan
> [!NOTE]
> Bu adım için redis’in geliştirme makinenizde yerel olarak yüklendiği varsayılır. [Bu yönergeleri kullanarak Redis’i yerel olarak yükleme][9].
> 
> 

Seçim ve türü hello komutu aşağıdaki komut satırı konsolunu açın:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Hello yerine  **&lt;ana bilgisayar adı için redis önbelleği&gt;**  hello gerçek xxxxx.redis.cache.windows.net ana bilgisayar adı ve hello  **&lt;birincil-anahtar-için-redis-cache&gt;**  hello önbelleği için hello erişim anahtarı ile tuşuna **Enter**. Merhaba CLI toohello Redis önbelleği örneğine bağlandığında, herhangi bir redis komutu gönderin. Merhaba ekran görüntüsünde, t toolist hello anahtarları seçtiniz.

![TooAzure Redis önbelleği Redis CLI Terminal bağlayın](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

Merhaba çağrısı toolist hello anahtarları bir değer döndürmelidir. Aksi durumda, toohello web uygulamasına gidin ve yeniden deneyin.

## Sonuç
Tebrikler! Merhaba WordPress uygulaması artık işlemenin artırılmasına içinde merkezi bellek içi önbellek tooaid sahiptir. Unutmayın, hello Web Apps Memcache Dolgusu'nun programlama dili veya uygulama framework bağımsız olarak Memcache istemcisi ile kullanılabilir. tooprovide geri bildirim veya tooask hello Web Apps Memcache dolgusu hakkında sorularınızı çok[MSDN Forumları] [ 10] veya [Stackoverflow][11].

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org

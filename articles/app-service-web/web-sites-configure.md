---
title: "Azure App Service'te web uygulamalarını aaaConfigure"
description: "Nasıl tooconfigure bir web uygulamasını Azure uygulama hizmetleri"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde Web uygulamalarını yapılandırma
Bu konuda, bir web uygulamasını kullanarak tooconfigure nasıl hello açıklanmaktadır [Azure Portal].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Uygulama ayarları
1. Merhaba, [Azure Portal]açın hello dikey penceresinde hello web uygulaması için.
2. Tıklatın **tüm ayarları**.
3. Tıklatın **uygulama ayarları**.

![Uygulama ayarları][configure01]

Merhaba **uygulama ayarları** dikey birkaç kategoriler altında gruplanmış ayarlara sahip.

### <a name="general-settings"></a>Genel ayarları
**Framework sürümlerini**. Uygulamanız herhangi bu çerçeveleri kullanıyorsa bu seçenekleri ayarlayın: 

* **.NET framework**: kümesi hello .NET framework sürümü. 
* **PHP**: kümesi hello PHP sürümünü veya **OFF** toodisable PHP. 
* **Java**: Select hello Java sürümü veya **OFF** toodisable Java. Kullanım hello **Web kapsayıcısına** seçeneği toochoose Tomcat ve Jetty sürümleri arasında.
* **Python**: Select hello Python sürümü veya **OFF** toodisable Python.

Teknik nedenlerle hello .NET, PHP ve Python seçenekleri uygulamanız için Java'yı etkinleştirme devre dışı bırakır.

<a name="platform"></a>
**Platform**. Web uygulamanızı 32 bit veya 64-bit bir ortamda çalışır olup olmadığını belirler. Merhaba 64-bit ortamı temel veya standart modu gerektirir. Ücretsiz ve paylaşılan modları her zaman bir 32 bit ortamda çalıştırılabilir.

**Web yuvaları**. Ayarlama **ON** tooenable hello WebSocket Protokolü; Örneğin, web uygulamanızı kullanıyorsa [ASP.NET SignalR] veya [Socket.IO].

<a name="alwayson"></a>
**Always On**. Varsayılan olarak, belirli bir süre için boşta olmaları durumunda web uygulamaları kaldırılır. Bu hello sistem kaynakların tasarrufu sağlar. Temel veya standart modunda etkinleştirebilirsiniz **her zaman açık** tookeep hello uygulama yüklenen tüm hello zaman. Sürekli Webjob'lar uygulamanızın çalıştırdığı veya çalıştığı Web işleri tetiklenen CRON ifade kullanılarak, etkinleştirmeniz gerekir **her zaman açık**, veya hello web işleri güvenilir bir şekilde çalıştıramıyor.

**Yönetilen ardışık düzen sürüm**. Ayarlar hello IIS [ardışık düzen modu]. Bırakın IIS daha eski bir sürümü gerektiren eski bir uygulama yoksa bu tooIntegrated (Merhaba varsayılan) ayarlayın.

**Otomatik Takas**. Otomatik Takas için bir dağıtım yuvası etkinleştirirseniz, bir güncelleştirme toothat yuvaya bastığınızda uygulama hizmeti otomatik olarak başlangıç web uygulaması üretime değiştireceksiniz. Daha fazla bilgi için bkz: [toostaging yuvaları için Azure App Service'te web uygulamalarını dağıtma](web-sites-staged-publishing.md).

### <a name="debugging"></a>Hata ayıklama
**Uzaktan hata ayıklama**. Uzaktan hata ayıklamayı etkinleştirir. Tooyour web doğrudan uygulama etkinleştirildiğinde, Visual Studio tooconnect hello uzaktan hata ayıklayıcı kullanabilirsiniz. Uzaktan hata ayıklama 48 saat boyunca etkin kalır. 

### <a name="app-settings"></a>Uygulama ayarları
Bu bölümde, web ad/değer çiftleri içeren uygulama başlangıç yükler. 

* .NET yapılandırmanızı eklenen .NET uygulamaları için bu ayarları `AppSettings` çalışma zamanında mevcut ayarları geçersiz kılar. 
* PHP, Python, Java ve düğüm uygulamalar, bu ayarlar çalışma zamanında ortam değişkenleri olarak erişebilir. Her uygulama ayarı için iki ortam değişkenin oluşturulur; bir hello uygulama ayarı girişi ve APPSETTING_ önekine sahip başka bir tarafından belirtilen hello ada sahip. Her ikisi de hello içeren aynı değeri.

### <a name="connection-strings"></a>Bağlantı dizeleri
Bağlantılı kaynaklar için bağlantı dizelerini. 

.NET uygulamaları için bu bağlantı dizeleri .NET yapılandırmanızı eklenmiş `connectionStrings` burada hello anahtar eşittir girişlerin ayarlar çalışma zamanında hello bağlantılı veritabanı adı. 

PHP, Python, Java ve düğüm uygulamalar için bu ayarları hello bağlantı türüyle önekli zamanında ortam değişkenleri olarak kullanılabilir. Merhaba ortam değişkeni önekleri aşağıdaki gibidir: 

* SQL sunucusu:`SQLCONNSTR_`
* MySQL:`MYSQLCONNSTR_`
* SQL veritabanı:`SQLAZURECONNSTR_`
* Özel:`CUSTOMCONNSTR_`

Örneğin, bir MySql bağlantı dizesi olarak adlandırılmışsa `connectionstring1`, hello ortam değişkeni erişilebilecek `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Varsayılan belgeler
Hello varsayılan belge hello web hello kök URL'de bir Web sitesi için görüntülenen sayfadır.  Merhaba ilk eşleşen dosya hello listesinde kullanılır. 

Web uygulamaları rota URL'sine bağlı yerine, bu nedenle bir varsayılan belge statik içerik vardır; bu durumda hizmet olan modülleri kullanabilir.    

### <a name="handler-mappings"></a>İşleyici eşlemeleri
Bu alan tooadd özel komut dosyası işlemciler toohandle istekleri için belirli dosya uzantılarını kullanın. 

* **Uzantı**. Merhaba dosya uzantısı toobe *.php veya handler.fcgi gibi işlenir. 
* **Betik işleyici yolu**. Merhaba hello betik işlemcisi mutlak yolu. Merhaba dosya uzantısı ile eşleşen istekleri toofiles hello betik işleyici tarafından işlenir. Merhaba yolu kullan `D:\home\site\wwwroot` toorefer tooyour uygulamanızın kök dizini.
* **Ek bağımsız değişkenler**. Merhaba betik işleyici için isteğe bağlı komut satırı bağımsız değişkenleri 

### <a name="virtual-applications-and-directories"></a>Sanal uygulamalar ve dizinler
tooconfigure sanal uygulamalar ve dizinler, her sanal dizini ve karşılık gelen fiziksel yolu göreli toohello Web sitesi kökü belirtin. İsteğe bağlı olarak, hello seçebilirsiniz **uygulama** onay kutusunu toomark bir uygulama olarak bir sanal dizin.

## <a name="enabling-diagnostic-logs"></a>Tanılama günlüklerini etkinleştirme
tooenable tanılama günlükleri:

1. Web uygulamanız için Hello dikey penceresinde tıklayın **tüm ayarları**.
2. Tıklatın **tanılama günlükleri**. 

Bir web uygulamasından tanılama günlüklerini yazma seçenekleri, günlük kaydı destekler: 

* **Uygulama günlüğü**. Uygulama günlüklerini toohello dosya sistemi yazar. Lasts 12 saatlik bir dönem için günlüğe kaydetme. 

**Düzey**. Uygulama günlüğü etkinleştirildiğinde, bu seçenek kayıtlı (hata, uyarı, bilgi veya ayrıntılı) olacak bilgileri hello miktarını belirtir.

**Web sunucusu günlüğü**. Günlükleri hello W3C Genişletilmiş günlük dosyası biçiminde kaydedilir. 

**Ayrıntılı hata iletileri**. .Htm dosyaları kaydeder ayrıntılı hata iletileri. Merhaba dosyaları /LogFiles/DetailedErrors altında kaydedilir. 

**Başarısız istek izleme**. Günlükleri istekleri tooXML dosyaları başarısız oldu. Merhaba dosyalar/LogFiles/altında W3SVC kaydedilir*xxx*, burada xxx benzersiz bir tanımlayıcıdır. Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir. Biçimlendirme ve hello XML dosyaları Merhaba içeriğine filtreleme için işlevsellik sağlar olduğundan emin toodownload hello XSL dosyasını olun.

tooview hello günlük dosyaları, FTP kimlik bilgileri, şu şekilde oluşturmanız gerekir:

1. Web uygulamanız için Hello dikey penceresinde tıklayın **tüm ayarları**.
2. Tıklatın **dağıtım kimlik bilgileri**.
3. Bir kullanıcı adı ve parola girin.
4. **Kaydet** düğmesine tıklayın.

![Dağıtım kimlik bilgilerini ayarlama][configure03]

Merhaba tam FTP kullanıcı adı. "app\username" nerede *uygulama* web uygulamanızı hello adıdır. Merhaba kullanıcıadı hello web uygulaması dikey penceresinde altında listelenen **Essentials**.  

![FTP dağıtımı kimlik bilgileri][configure02]

## <a name="other-configuration-tasks"></a>Diğer yapılandırma görevleri
### <a name="ssl"></a>SSL
Temel veya standart modunda özel bir etki alanı için SSL sertifikalarını karşıya yükleyebilirsiniz. [Web uygulaması için HTTPS'yi etkinleştir] daha fazla bilgi için bkz. 

Karşıya yüklenen sertifikalarınızı tooview tıklatın **tüm ayarları** > **özel etki alanları ve SSL**.

### <a name="domain-names"></a>Etki alanı adları
Web uygulamanız için özel etki alanı adlarını ekleyin. Daha fazla bilgi için bkz: [yapılandırma Azure App Service'te bir web uygulaması için bir özel etki alanı adı].

etki alanı adlarınızı tooview tıklatın **tüm ayarları** > **özel etki alanları ve SSL**.

### <a name="deployments"></a>Dağıtımlar
* Sürekli dağıtım ayarlayın. Bkz: [kullanarak Git toodeploy Azure App Service'te Web uygulamalarını](web-sites-deploy.md).
* Dağıtım yuvaları. Bkz: [tooStaging ortamlar için Azure App Service'te Web uygulamalarını dağıtma].

tooview tıklatın, dağıtım yuvası **tüm ayarları** > **dağıtım yuvası**.

### <a name="monitoring"></a>İzleme
Temel veya standart modunda hello kullanılabilirlik HTTP veya HTTPS uç noktaları, gelen toothree coğrafi olarak dağıtılan konumları test edebilirsiniz. Merhaba HTTP yanıt kodu bir hata (4xx veya 5xx) ya da 30 saniyeden fazla hello yanıt alır, izleme testi başarısız olur. Bir uç nokta hello izleme sınamalarını tümünden başarılı kullanılabilir sayılması hello belirtilen konumları. 

Daha fazla bilgi için bkz: [nasıl yapılır: izleme web uç noktası durumu].

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin], burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Azure App Service'te özel etki alanı adını yapılandırma]
* [Azure uygulama hizmetinde bir uygulama için HTTPS'yi etkinleştir]
* [Bir web uygulamasını Azure App Service'te ölçeklendirme]
* [Azure App Service'deki Web uygulamaları için izleme temelleri]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Azure App Service'te özel etki alanı adını yapılandırma]: ./app-service-web-tutorial-custom-domain.md
[tooStaging ortamlar için Azure App Service'te Web uygulamalarını dağıtma]: ./web-sites-staged-publishing.md
[Azure uygulama hizmetinde bir uygulama için HTTPS'yi etkinleştir]: ./app-service-web-tutorial-custom-ssl.md
[nasıl yapılır: izleme web uç noktası durumu]: http://go.microsoft.com/fwLink/?LinkID=279906
[Azure App Service'deki Web uygulamaları için izleme temelleri]: ./web-sites-monitor.md
[ardışık düzen modu]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Bir web uygulamasını Azure App Service'te ölçeklendirme]: ./web-sites-scale.md
[Socket.IO]: ./web-sites-nodejs-chat-app-socketio.md
[App Service'i deneyin]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png

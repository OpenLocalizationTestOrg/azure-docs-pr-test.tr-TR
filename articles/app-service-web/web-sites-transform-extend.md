---
title: "aaaAzure App Service web uygulaması Gelişmiş yapılandırması ve uzantıları"
description: "XML belge Transformation(XDT) bildirimleri tootransform hello ApplicationHost.config dosyası, Azure App Service web app ve tooadd özel uzantıları tooenable özel yönetim eylemlerini kullanın."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Azure App Service web uygulaması Gelişmiş yapılandırması ve uzantıları
Kullanarak [XML belge dönüştürme](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) bildirimleri hello dönüştürebilirsiniz [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) web uygulamanızı Azure App Service'te dosyasında. XDT bildirimleri tooadd özel uzantıları tooenable özel web uygulama yönetim eylemleri de kullanabilirsiniz. Bu makalede bir web arabirimi aracılığıyla PHP ayarlarının yönetim sağlayan bir örnek PHP Yöneticisi web uygulaması uzantısı içerir.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>ApplicationHost.config aracılığıyla Gelişmiş Yapılandırma
Merhaba App Service platformu, web uygulama yapılandırması için esneklik ve denetim sağlar. Hello standart IIS ApplicationHost.config yapılandırma dosyasını doğrudan App Service içinde düzenlemek için kullanılabilir olsa da hello platform XML belge dönüştürme (XDT) dayalı bir bildirim temelli ApplicationHost.config dönüştürme modelini destekler.

tooleverage bu dönüştürme işlevleri, bir ApplicationHost.xdt dosyası ile XDT içerik oluşturabilir ve yerleştirebilirsiniz hello site kökü (d:\home\site) hello'nün altında [Kudu konsol](https://github.com/projectkudu/kudu/wiki/Kudu-console). Toorestart hello Web uygulaması için değişiklikleri tootake efekti gerekebilir.

applicationHost.xdt örnek aşağıdaki hello nasıl tooadd yeni bir özel ortam değişkeni tooa web PHP 5.4 kullanan uygulamalarda gösterir.

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

Dönüştürme durumu ve ayrıntıları içeren bir günlük dosyası hello FTP kök LogFiles\Transform altında kullanılabilir.

Ek örnekler için bkz: [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Not**<br />
Modüller'in altında hello listesinden öğeleri `system.webServer` kaldırılan veya kaldırılmasında, ancak eklemeleri toohello listesi mümkün.

## <a id="extend"></a>Web uygulamanızı genişletme
### <a id="overview"></a>Özel web uygulaması uzantınız genel bakış
App Service web uygulaması uzantınız yönetim eylemleri için genişletilebilirlik noktası olarak destekler. Aslında, bazı App Service platformu özellikleri önceden yüklenmiş uzantıları olarak uygulanır. Merhaba önceden yüklenmiş platform uzantıları değiştirilemez, ancak oluşturun ve kendi web uygulaması için özel uzantıları yapılandırın. Bu işlev da XDT bildirimlerinde dayanır. Özel web uygulaması uzantısı oluşturmak için temel adımlar hello hello şunlardır:

1. Web uygulaması uzantısı **içerik**: App Service tarafından desteklenen herhangi bir web uygulaması oluşturma
2. Web uygulaması uzantısı **bildirimi**: ApplicationHost.xdt dosyası oluşturma
3. Web uygulaması uzantısı **dağıtım**: içerik altında hello SiteExtensions klasöre yerleştirin`root`

Merhaba web uygulaması için iç bağlantıları tooa yolu göreli toohello uygulama yolu hello ApplicationHost.xdt dosyasında belirtilen işaret etmelidir. Herhangi bir değişiklik toohello ApplicationHost.xdt dosyasını bir web uygulaması geri dönüşüm gerektirir.

**Not**: ek bilgi için bu anahtar öğeler, şu adreste [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Oluşturma ve özel web uygulaması uzantısı etkinleştirme dahil tooillustrate hello adımları buna ayrıntılı bir örnektir. Merhaba aşağıdaki gibi yüklenebilir Merhaba PHP Manager örneği için kaynak kodunu [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Web uygulaması uzantısı örnek: PHP Yöneticisi
PHP, web uygulama yöneticileri tooeasily görünümü sağlar ve toomodify PHP .ini dosyaları zorunda yerine doğrudan bir web arabirimi kullanarak PHP ayarlarını yapılandırdığınız bir web uygulaması uzantısı yöneticisidir. PHP için yaygın yapılandırma dosyalarını Program dosyaları ve hello altında bulunan hello php.ini dosyasını içerir. web uygulamanızın hello kök klasöründe yer alan user.ini dosyası. Merhaba php.ini dosyası hello App Service platformu üzerinde doğrudan düzenlenebilir olmadığından hello hello PHP Yöneticisi uzantısı kullanır. user.ini dosya tooapply değişiklikleri ayarlama.

#### <a id="PHPwebapp"></a>Merhaba PHP Yöneticisi web uygulaması
Merhaba, hello PHP Yöneticisi dağıtım hello giriş sayfasının aşağıdadır:

![TransformSitePHPUI][TransformSitePHPUI]

Gördüğünüz gibi bir web uygulaması uzantısı normal web uygulaması gibi ancak bir ek ApplicationHost.xdt dosyasıyla (Merhaba ApplicationHost.xdt dosyası hakkında daha fazla ayrıntı hello sonraki bölümde bu kullanılabilir hello web uygulamasının hello kök klasöre yerleştirilir gereklidir. makale).

Merhaba PHP Yöneticisi uzantısı hello Visual Studio ASP.NET MVC 4 Web uygulaması şablonu kullanılarak oluşturuldu. Merhaba Çözüm Gezgini'nden aşağıdaki görünümü hello PHP Yöneticisi uzantısı hello yapısını gösterir.

![TransformSiteSolEx][TransformSiteSolEx]

Merhaba yalnızca dosya g/ç için gereken özel mantığı tooindicate hello wwwroot dizinini hello web uygulamasının bulunduğu ' dir. Ortam değişkeni "HOME" Merhaba aşağıdaki kod örneğinde gösterildiği hello gibi web uygulamanızın kök yolu hello ve hello wwwroot yolu "site\wwwroot" ekleyerek oluşturulabilir gösterir:

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


Merhaba dizin yolu oluşturduktan sonra normal dosya g/ç işlemleri tooread ve toofiles yazma kullanabilirsiniz.

Web uygulaması uzantınız dikkatli bir noktasını hello işleme iç bağlantıların tahminini.  Mutlak yollar, web uygulamanıza toointernal bağlantılarını verin, HTML dosyaları herhangi bir bağlantı varsa, bu bağlantılar, kök olarak uzantısı adıyla $a emin olmalısınız. Merhaba kök Uzantınız için artık olduğundan bu gerekiyor "/`[your-extension-name]`/" olmak yerine yalnızca "/", böylece her iç bağlantılar uygun şekilde güncelleştirilmesi gerekir. Örneğin, kodunuzu bir bağlantı toohello şunlardır varsayın:

`"<a href="/Home/Settings">PHP Settings</a>"`

Merhaba bağlantı bir web uygulaması uzantısı parçası olduğunda hello bağlantı form aşağıdaki hello olmalıdır:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Hello kullanarak ASP.NET uygulamaları durumunun göreli yollar veya web uygulamanızı işinde hello yalnızca her iki kullanarak bu gereksinim çalışabilirsiniz `@Html.ActionLink` hello uygun bağlantıları sizin için oluşturduğu yöntemi.

#### <a id="XDT"></a>Merhaba applicationHost.xdt dosyası
web uygulaması uzantısı Hello kodunu gider altında %HOME%\SiteExtensions\[-genişletme-adınız]. Bu hello uzantısı kök arayacağız.  

tooregister web uygulaması uzantısı hello applicationHost.config dosyasını tooplace hello uzantısı kök ApplicationHost.xdt adlı bir dosya gerekir. Merhaba ApplicationHost.xdt dosyanın Merhaba içeriğine şu şekilde olmalıdır:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

uzantı adı olarak seçtiğiniz hello adı hello aynı adı uzantısı kök klasör olarak olması gerekir.

Bu yeni bir uygulama yolu toohello ekleme hello etkisi `system.applicationHost` siteler listesine hello SCM site altında. özel erişim kimlik bilgilerine sahip bir site yönetim uç noktası Hello SCM sitedir. Merhaba URL'ye sahip `https://[your-site-name].scm.azurewebsites.net`.  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a>Web uygulaması uzantısı dağıtımı
tooinstall, web uygulaması uzantısı, web uygulama toohello tüm hello dosyaları FTP toocopy kullanabilirsiniz `\SiteExtensions\[your-extension-name]` hello web uygulamasının tooinstall hello uzantısı istediğiniz klasör.  Emin toocopy hello ApplicationHost.xdt dosya toothis konumu da olabilir. Web uygulaması tooenable hello uzantınızı yeniden başlatın.

Konumunda, web uygulaması uzantısı mümkün toosee olmalıdır:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

URL HTTPS kullanır ve ".scm" içerir ancak bu yalnızca bir URL hello gibi web uygulamanız için arar. Bu hello unutmayın.

Web uygulamanız için olası toodisable tüm özel (önceden yüklü değil) uzantıları geliştirme ve araştırmalar sırasında hello anahtara sahip bir uygulama ayarı ekleyerek olmasından `WEBSITE_PRIVATE_EXTENSIONS` ve değerini `0`.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png


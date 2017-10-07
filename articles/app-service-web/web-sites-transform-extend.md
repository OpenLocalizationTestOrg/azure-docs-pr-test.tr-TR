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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="24465-103">Azure App Service web uygulaması Gelişmiş yapılandırması ve uzantıları</span><span class="sxs-lookup"><span data-stu-id="24465-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="24465-104">Kullanarak [XML belge dönüştürme](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) bildirimleri hello dönüştürebilirsiniz [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) web uygulamanızı Azure App Service'te dosyasında.</span><span class="sxs-lookup"><span data-stu-id="24465-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="24465-105">XDT bildirimleri tooadd özel uzantıları tooenable özel web uygulama yönetim eylemleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24465-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="24465-106">Bu makalede bir web arabirimi aracılığıyla PHP ayarlarının yönetim sağlayan bir örnek PHP Yöneticisi web uygulaması uzantısı içerir.</span><span class="sxs-lookup"><span data-stu-id="24465-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="24465-107"><a id="transform"></a>ApplicationHost.config aracılığıyla Gelişmiş Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24465-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="24465-108">Merhaba App Service platformu, web uygulama yapılandırması için esneklik ve denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="24465-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="24465-109">Hello standart IIS ApplicationHost.config yapılandırma dosyasını doğrudan App Service içinde düzenlemek için kullanılabilir olsa da hello platform XML belge dönüştürme (XDT) dayalı bir bildirim temelli ApplicationHost.config dönüştürme modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="24465-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="24465-110">tooleverage bu dönüştürme işlevleri, bir ApplicationHost.xdt dosyası ile XDT içerik oluşturabilir ve yerleştirebilirsiniz hello site kökü (d:\home\site) hello'nün altında [Kudu konsol](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="24465-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="24465-111">Toorestart hello Web uygulaması için değişiklikleri tootake efekti gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="24465-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="24465-112">applicationHost.xdt örnek aşağıdaki hello nasıl tooadd yeni bir özel ortam değişkeni tooa web PHP 5.4 kullanan uygulamalarda gösterir.</span><span class="sxs-lookup"><span data-stu-id="24465-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="24465-113">Dönüştürme durumu ve ayrıntıları içeren bir günlük dosyası hello FTP kök LogFiles\Transform altında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24465-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="24465-114">Ek örnekler için bkz: [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="24465-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="24465-115">**Not**</span><span class="sxs-lookup"><span data-stu-id="24465-115">**Note**</span></span><br />
<span data-ttu-id="24465-116">Modüller'in altında hello listesinden öğeleri `system.webServer` kaldırılan veya kaldırılmasında, ancak eklemeleri toohello listesi mümkün.</span><span class="sxs-lookup"><span data-stu-id="24465-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="24465-117"><a id="extend"></a>Web uygulamanızı genişletme</span><span class="sxs-lookup"><span data-stu-id="24465-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="24465-118"><a id="overview"></a>Özel web uygulaması uzantınız genel bakış</span><span class="sxs-lookup"><span data-stu-id="24465-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="24465-119">App Service web uygulaması uzantınız yönetim eylemleri için genişletilebilirlik noktası olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="24465-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="24465-120">Aslında, bazı App Service platformu özellikleri önceden yüklenmiş uzantıları olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="24465-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="24465-121">Merhaba önceden yüklenmiş platform uzantıları değiştirilemez, ancak oluşturun ve kendi web uygulaması için özel uzantıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24465-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="24465-122">Bu işlev da XDT bildirimlerinde dayanır.</span><span class="sxs-lookup"><span data-stu-id="24465-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="24465-123">Özel web uygulaması uzantısı oluşturmak için temel adımlar hello hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="24465-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="24465-124">Web uygulaması uzantısı **içerik**: App Service tarafından desteklenen herhangi bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="24465-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="24465-125">Web uygulaması uzantısı **bildirimi**: ApplicationHost.xdt dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="24465-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="24465-126">Web uygulaması uzantısı **dağıtım**: içerik altında hello SiteExtensions klasöre yerleştirin`root`</span><span class="sxs-lookup"><span data-stu-id="24465-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="24465-127">Merhaba web uygulaması için iç bağlantıları tooa yolu göreli toohello uygulama yolu hello ApplicationHost.xdt dosyasında belirtilen işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="24465-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="24465-128">Herhangi bir değişiklik toohello ApplicationHost.xdt dosyasını bir web uygulaması geri dönüşüm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="24465-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="24465-129">**Not**: ek bilgi için bu anahtar öğeler, şu adreste [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="24465-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="24465-130">Oluşturma ve özel web uygulaması uzantısı etkinleştirme dahil tooillustrate hello adımları buna ayrıntılı bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="24465-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="24465-131">Merhaba aşağıdaki gibi yüklenebilir Merhaba PHP Manager örneği için kaynak kodunu [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="24465-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="24465-132"><a id="SiteSample"></a>Web uygulaması uzantısı örnek: PHP Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="24465-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="24465-133">PHP, web uygulama yöneticileri tooeasily görünümü sağlar ve toomodify PHP .ini dosyaları zorunda yerine doğrudan bir web arabirimi kullanarak PHP ayarlarını yapılandırdığınız bir web uygulaması uzantısı yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="24465-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="24465-134">PHP için yaygın yapılandırma dosyalarını Program dosyaları ve hello altında bulunan hello php.ini dosyasını içerir. web uygulamanızın hello kök klasöründe yer alan user.ini dosyası.</span><span class="sxs-lookup"><span data-stu-id="24465-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="24465-135">Merhaba php.ini dosyası hello App Service platformu üzerinde doğrudan düzenlenebilir olmadığından hello hello PHP Yöneticisi uzantısı kullanır. user.ini dosya tooapply değişiklikleri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="24465-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="24465-136"><a id="PHPwebapp"></a>Merhaba PHP Yöneticisi web uygulaması</span><span class="sxs-lookup"><span data-stu-id="24465-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="24465-137">Merhaba, hello PHP Yöneticisi dağıtım hello giriş sayfasının aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="24465-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="24465-139">Gördüğünüz gibi bir web uygulaması uzantısı normal web uygulaması gibi ancak bir ek ApplicationHost.xdt dosyasıyla (Merhaba ApplicationHost.xdt dosyası hakkında daha fazla ayrıntı hello sonraki bölümde bu kullanılabilir hello web uygulamasının hello kök klasöre yerleştirilir gereklidir. makale).</span><span class="sxs-lookup"><span data-stu-id="24465-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="24465-140">Merhaba PHP Yöneticisi uzantısı hello Visual Studio ASP.NET MVC 4 Web uygulaması şablonu kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="24465-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="24465-141">Merhaba Çözüm Gezgini'nden aşağıdaki görünümü hello PHP Yöneticisi uzantısı hello yapısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="24465-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="24465-143">Merhaba yalnızca dosya g/ç için gereken özel mantığı tooindicate hello wwwroot dizinini hello web uygulamasının bulunduğu ' dir.</span><span class="sxs-lookup"><span data-stu-id="24465-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="24465-144">Ortam değişkeni "HOME" Merhaba aşağıdaki kod örneğinde gösterildiği hello gibi web uygulamanızın kök yolu hello ve hello wwwroot yolu "site\wwwroot" ekleyerek oluşturulabilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="24465-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

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


<span data-ttu-id="24465-145">Merhaba dizin yolu oluşturduktan sonra normal dosya g/ç işlemleri tooread ve toofiles yazma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24465-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="24465-146">Web uygulaması uzantınız dikkatli bir noktasını hello işleme iç bağlantıların tahminini.</span><span class="sxs-lookup"><span data-stu-id="24465-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="24465-147">Mutlak yollar, web uygulamanıza toointernal bağlantılarını verin, HTML dosyaları herhangi bir bağlantı varsa, bu bağlantılar, kök olarak uzantısı adıyla $a emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="24465-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="24465-148">Merhaba kök Uzantınız için artık olduğundan bu gerekiyor "/`[your-extension-name]`/" olmak yerine yalnızca "/", böylece her iç bağlantılar uygun şekilde güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24465-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="24465-149">Örneğin, kodunuzu bir bağlantı toohello şunlardır varsayın:</span><span class="sxs-lookup"><span data-stu-id="24465-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="24465-150">Merhaba bağlantı bir web uygulaması uzantısı parçası olduğunda hello bağlantı form aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="24465-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="24465-151">Hello kullanarak ASP.NET uygulamaları durumunun göreli yollar veya web uygulamanızı işinde hello yalnızca her iki kullanarak bu gereksinim çalışabilirsiniz `@Html.ActionLink` hello uygun bağlantıları sizin için oluşturduğu yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24465-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="24465-152"><a id="XDT"></a>Merhaba applicationHost.xdt dosyası</span><span class="sxs-lookup"><span data-stu-id="24465-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="24465-153">web uygulaması uzantısı Hello kodunu gider altında %HOME%\SiteExtensions\[-genişletme-adınız].</span><span class="sxs-lookup"><span data-stu-id="24465-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="24465-154">Bu hello uzantısı kök arayacağız.</span><span class="sxs-lookup"><span data-stu-id="24465-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="24465-155">tooregister web uygulaması uzantısı hello applicationHost.config dosyasını tooplace hello uzantısı kök ApplicationHost.xdt adlı bir dosya gerekir.</span><span class="sxs-lookup"><span data-stu-id="24465-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="24465-156">Merhaba ApplicationHost.xdt dosyanın Merhaba içeriğine şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="24465-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

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

<span data-ttu-id="24465-157">uzantı adı olarak seçtiğiniz hello adı hello aynı adı uzantısı kök klasör olarak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24465-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="24465-158">Bu yeni bir uygulama yolu toohello ekleme hello etkisi `system.applicationHost` siteler listesine hello SCM site altında.</span><span class="sxs-lookup"><span data-stu-id="24465-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="24465-159">özel erişim kimlik bilgilerine sahip bir site yönetim uç noktası Hello SCM sitedir.</span><span class="sxs-lookup"><span data-stu-id="24465-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="24465-160">Merhaba URL'ye sahip `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="24465-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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

### <span data-ttu-id="24465-161"><a id="deploy"></a>Web uygulaması uzantısı dağıtımı</span><span class="sxs-lookup"><span data-stu-id="24465-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="24465-162">tooinstall, web uygulaması uzantısı, web uygulama toohello tüm hello dosyaları FTP toocopy kullanabilirsiniz `\SiteExtensions\[your-extension-name]` hello web uygulamasının tooinstall hello uzantısı istediğiniz klasör.</span><span class="sxs-lookup"><span data-stu-id="24465-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="24465-163">Emin toocopy hello ApplicationHost.xdt dosya toothis konumu da olabilir.</span><span class="sxs-lookup"><span data-stu-id="24465-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="24465-164">Web uygulaması tooenable hello uzantınızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="24465-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="24465-165">Konumunda, web uygulaması uzantısı mümkün toosee olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="24465-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="24465-166">URL HTTPS kullanır ve ".scm" içerir ancak bu yalnızca bir URL hello gibi web uygulamanız için arar. Bu hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="24465-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="24465-167">Web uygulamanız için olası toodisable tüm özel (önceden yüklü değil) uzantıları geliştirme ve araştırmalar sırasında hello anahtara sahip bir uygulama ayarı ekleyerek olmasından `WEBSITE_PRIVATE_EXTENSIONS` ve değerini `0`.</span><span class="sxs-lookup"><span data-stu-id="24465-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="24465-168">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24465-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="24465-169">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="24465-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="24465-170">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="24465-170">What's changed</span></span>
* <span data-ttu-id="24465-171">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="24465-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png


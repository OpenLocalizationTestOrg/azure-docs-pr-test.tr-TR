---
title: "özel bir Java web uygulaması tooAzure aaaUpload"
description: "Bu öğretici nasıl tooupload özel bir Java web uygulaması tooAzure App Service Web Apps gösterir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="0aaa3-103">Özel bir Java web uygulaması tooAzure karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0aaa3-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="0aaa3-104">Bu konuda, nasıl tooupload özel bir Java web uygulaması çok açıklanmaktadır[Azure App Service] Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="0aaa3-105">Tooany Java Web sitesi veya web uygulaması ve ayrıca bazı örnekler belirli uygulamalar için geçerli olan bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="0aaa3-106">Azure hello Azure Portal'ın yapılandırma kullanıcı Arabirimi kullanarak Java web uygulamaları oluşturmak için bir yol sağlar not edin ve Azure Marketi adresindeki açıklandığı gibi hello [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0aaa3-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="0aaa3-107">İçinde istememiş toouse hello Azure Portal yapılandırma kullanıcı Arabirimi veya Azure Marketi hello senaryoları için öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="0aaa3-108">Yapılandırma yönergeleri</span><span class="sxs-lookup"><span data-stu-id="0aaa3-108">Configuration guidelines</span></span>
<span data-ttu-id="0aaa3-109">Hello azure'daki özel Java web uygulamaları için beklenen hello ayarları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="0aaa3-110">Merhaba Java işlemi tarafından kullanılan hello HTTP bağlantı noktası dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="0aaa3-111">Merhaba işlem, başlangıç bağlantı noktasından hello ortam değişkeni kullanmalıdır `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="0aaa3-112">Merhaba tek HTTP dinleyicisi devre dışı bırakılmalıdır dışındaki tüm bağlantı noktalarını dinler.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="0aaa3-113">Tomcat'te hello kapatma, HTTPS ve AJP içeren bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="0aaa3-114">Merhaba kapsayıcı yalnızca IPv4 trafiği için yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="0aaa3-115">Merhaba **başlangıç** toobe Merhaba uygulaması gereken için komut hello yapılandırmasında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="0aaa3-116">Dizinleri yazma izni gerektiren uygulamalar ihtiyacınız olan hello Azure web uygulamanızın içerik, dizininde toobe **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="0aaa3-117">Merhaba ortam değişkeni `HOME` tooD:\home başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="0aaa3-118">Ortam değişkenleri gerektiği gibi hello web.config dosyasında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="0aaa3-119">Web.config httpPlatform yapılandırması</span><span class="sxs-lookup"><span data-stu-id="0aaa3-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="0aaa3-120">Merhaba aşağıdaki bilgileri açıklar hello **httpPlatform** web.config içinde biçimi.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="0aaa3-121">**bağımsız değişkenler** (varsayılan = "").</span><span class="sxs-lookup"><span data-stu-id="0aaa3-121">**arguments** (Default="").</span></span> <span data-ttu-id="0aaa3-122">Bağımsız değişkenler toohello çalıştırılabilir veya hello belirtilen komut dosyası **processPath** ayarı.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="0aaa3-123">Örnekler (ile gösterilen **processPath** dahil):</span><span class="sxs-lookup"><span data-stu-id="0aaa3-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="0aaa3-124">**processPath** -yol toohello çalıştırılabilir veya HTTP isteklerini dinlemeye bir işlem başlatır komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="0aaa3-125">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="0aaa3-126">**rapidFailsPerMinute** (varsayılan = 10.) Sayısı hello işlemi belirtilen zaman **processPath** toocrash dakikada izin verilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="0aaa3-127">Bu sınır aşılırsa, **HttpPlatformHandler** hello dakika hello kalanı için hello işlemi başlatmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="0aaa3-128">**requestTimeout** (varsayılan = "00: 02:00".) Hangi süresince **HttpPlatformHandler** dinlemede hello işleminden yanıt bekleyeceği `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="0aaa3-129">**startupRetryCount** (varsayılan = 10.) Kaç kez **HttpPlatformHandler** belirtilen toolaunch hello işlem deneyecek **processPath**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="0aaa3-130">Bkz: **startupTimeLimit** daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="0aaa3-131">**startupTimeLimit** (varsayılan = 10 saniye.) Hangi süresince **HttpPlatformHandler** hello yürütülebilir/komut dosyası toostart için başlangıç bağlantı noktasını dinleyen bir işlem bekler.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="0aaa3-132">Bu süre aşılırsa **HttpPlatformHandler** KILL hello işlemi ve toolaunch deneyin yeniden **startupRetryCount** kez.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="0aaa3-133">**stdoutLogEnabled** (varsayılan = "true".) TRUE ise, **stdout** ve **stderr** hello belirtilen hello işlemi için **processPath** ayarı belirtilen yeniden yönlendirilen toohello dosya olacaktır  **stdoutLogFile** (bkz **stdoutLogFile** bölümü).</span><span class="sxs-lookup"><span data-stu-id="0aaa3-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="0aaa3-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Mutlak dosya yolunu **stdout** ve **stderr** belirtilen hello işleminden **processPath** günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="0aaa3-135">`%HTTP_PLATFORM_PORT%`toospecified parçası olarak ya da gereken özel bir yer tutucudur **bağımsız değişkenleri** veya hello parçası olarak **httpPlatform** **environmentVariables** listesi.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="0aaa3-136">Bu tarafından dahili olarak oluşturulan bir bağlantı noktası tarafından değiştirilecek **HttpPlatformHandler** böylece hello işlemi tarafından belirtilen **processPath** Bu bağlantı noktasında dinleme.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="0aaa3-137">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="0aaa3-137">Deployment</span></span>
<span data-ttu-id="0aaa3-138">Java tabanlı web uygulamalarını kolayca hello Internet Information Services (IIS) tabanlı web uygulamaları ile kullanılan aynı anlamına gelir hello çoğunu üzerinden dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="0aaa3-139">FTP, Git ve Kudu tümü olduğu hello gibi web uygulamaları için tümleşik SCM yeteneğini dağıtım düzenekleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="0aaa3-140">Java Visual Studio'da geliştirilen değil gibi bir protokol olarak WebDeploy çalışır ancak WebDeploy Java web uygulama dağıtım kullanım örnekleri ile uyuşmaz.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="0aaa3-141">Uygulama yapılandırması örnekleri</span><span class="sxs-lookup"><span data-stu-id="0aaa3-141">Application configuration Examples</span></span>
<span data-ttu-id="0aaa3-142">Aşağıdaki uygulamalar, bir web.config dosyası ve hello hello için uygulama yapılandırma örnekleri tooshow nasıl sağlandığını tooenable Java uygulamanızı App Service Web Apps üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="0aaa3-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="0aaa3-143">Tomcat</span></span>
<span data-ttu-id="0aaa3-144">App Service Web Apps ile sağlanan iki Tomcat çeşidi olsa da, mümkün oldukça tooupload müşteri belirli örnekler hala geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="0aaa3-145">Aşağıda, Tomcat bir farklı Java sanal makine (JVM) ile yüklenmesini örneğidir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="0aaa3-146">Merhaba Tomcat yan üzerinde yapılan toobe gereken birkaç yapılandırma değişikliği yok.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="0aaa3-147">Merhaba server.xml düzenlenen toobe tooset gerekir:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="0aaa3-148">Kapatma bağlantı noktası = -1</span><span class="sxs-lookup"><span data-stu-id="0aaa3-148">Shutdown port = -1</span></span>
* <span data-ttu-id="0aaa3-149">HTTP Bağlayıcısı bağlantı noktası = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="0aaa3-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="0aaa3-150">HTTP Bağlayıcısı adresi = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="0aaa3-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="0aaa3-151">HTTPS ve AJP Bağlayıcılarına açıklama</span><span class="sxs-lookup"><span data-stu-id="0aaa3-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="0aaa3-152">Merhaba IPv4 ayarı, ekleyebileceğiniz hello catalina.properties dosyasında da ayarlanabilir.`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="0aaa3-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="0aaa3-153">App Service Web Apps üzerinde Direct3D çağrıları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="0aaa3-154">toodisable olanlar, ekleyin uygulamanız bu tür çağrılar olmalısınız Java seçenekten hello:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="0aaa3-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="0aaa3-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="0aaa3-155">Jetty</span></span>
<span data-ttu-id="0aaa3-156">Merhaba Tomcat için olduğu gibi müşteriler kendi örnekleri için Jetty karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="0aaa3-157">Jetty çalışan hello tam yüklemesi Hello durumda hello yapılandırma şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="0aaa3-158">Merhaba Jetty yapılandırması gereken hello start.ini tooset değiştirilen toobe `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="0aaa3-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="0aaa3-159">Springboot</span></span>
<span data-ttu-id="0aaa3-160">Sipariş tooget çalıştırdığınız Springboot uygulama JAR veya WAR dosyası tooupload gerekir ve hello aşağıdaki web.config dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="0aaa3-161">Merhaba web.config dosyasında hello wwwroot klasörüne gider.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="0aaa3-162">Merhaba web.config dosyasında hello bağımsız değişkenleri toopoint tooyour JAR dosyasını ayarlamak için hello aşağıdaki örnek hello JAR dosyasına da hello wwwroot klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="0aaa3-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="0aaa3-163">Hudson</span></span>
<span data-ttu-id="0aaa3-164">Kullanılan bizim test Hudson 3.1.2 war hello ve varsayılan Tomcat 7.0.50 örnek hello ancak hello UI tooset şeyler kullanmadan.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="0aaa3-165">Hudson yazılımları yapı aracı, bunu tavsiye edilir tooinstall olduğundan üzerinde ayrılmış örnekleri hello burada **AlwaysOn** bayrak hello web uygulaması üzerinde ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="0aaa3-166">Yani, web uygulamanızın içinde dizin, kök **d:\home\site\wwwroot**, oluşturma bir **webapps** dizini (yoksa) ve Hudson.war içinde yerleştirin **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="0aaa3-167">Apache maven 3.0.5 (Hudson ile uyumlu) indirin ve yerleştirileceği **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="0aaa3-168">Web.config dosyasında oluşturma **d:\home\site\wwwroot** Yapıştır hello izleyerek, içeriği:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="0aaa3-169">Bu noktada hello web uygulaması yeniden tootake hello değişiklikler olabilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="0aaa3-170">Toohttp://yourwebapp/hudson toostart Hudson bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="0aaa3-171">Hudson kendisini yapılandırdıktan sonra aşağıdaki ekran hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="0aaa3-173">Erişim hello Hudson yapılandırma sayfası: tıklatın **yönetmek Hudson**ve ardından **yapılandırma sistem**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="0aaa3-174">Merhaba aşağıda gösterildiği gibi JDK yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-174">Configure hello JDK as shown below:</span></span>
   
    ![Hudson yapılandırma](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="0aaa3-176">Maven aşağıda gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-176">Configure Maven as shown below:</span></span>
   
    ![Maven yapılandırma](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="0aaa3-178">Hello ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-178">Save hello settings.</span></span> <span data-ttu-id="0aaa3-179">Hudson artık yapılandırıldı ve kullanım için hazır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="0aaa3-180">Hudson hakkında ek bilgi için bkz: [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="0aaa3-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="0aaa3-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="0aaa3-181">Liferay</span></span>
<span data-ttu-id="0aaa3-182">Liferay App Service Web Apps üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="0aaa3-183">Liferay önemli bellek gerektirebilir olduğundan, yeterli bellek sağlayabilen bir orta veya büyük adanmış çalışan üzerinde toorun hello web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="0aaa3-184">Liferay birkaç dakika toostart da alır.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="0aaa3-185">Bu nedenle, hello web uygulaması çok ayarlamanız önerilir**her zaman açık**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="0aaa3-186">Tomcat ile Liferay Community Edition GA3 paketlenmiş 6.1.2 kullanarak hello aşağıdaki dosyaları Liferay indirdikten sonra düzenlendi:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="0aaa3-187">**Server.XML**</span><span class="sxs-lookup"><span data-stu-id="0aaa3-187">**Server.xml**</span></span>

* <span data-ttu-id="0aaa3-188">Kapatma bağlantı noktası çok-1 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="0aaa3-189">HTTP Bağlayıcısı çok değiştirme`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="0aaa3-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="0aaa3-190">Merhaba AJP bağlayıcı açıklama.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="0aaa3-191">Merhaba, **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** klasör adında bir dosya oluşturun **portal ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="0aaa3-192">Bu dosya toocontain bir satır, aşağıda gösterildiği gibi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="0aaa3-193">Merhaba hello tomcat 7.0.40 klasörü, aynı dizin düzeyinde adlı bir dosya oluşturmak **web.config** içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="0aaa3-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="0aaa3-194">Merhaba altında **httpPlatform** hello bloğunu **requestTimeout** çok Ayarla "00: 10:00".</span><span class="sxs-lookup"><span data-stu-id="0aaa3-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="0aaa3-195">Sınırlı ancak sonra büyük olasılıkla toosee sırasında bazı zaman aşımı hataları var Liferay önyükleme.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="0aaa3-196">Bu değer değiştiyse, ardından hello **connectionTimeout** hello tomcat'te server.xml değiştirilmeleri.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="0aaa3-197">Bu hello JRE_HOME ortama varariable hello web.config toopoint toohello yukarıda belirtilen dikkate değerdir 64-bit JDK.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="0aaa3-198">Merhaba varsayılandır 32-bit, ancak yüksek düzeyde bellek Liferay gerekebileceği toouse önerilir 64-bit JDK hello.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="0aaa3-199">Sonra web uygulamanızı Liferay yeniden, bu değişiklikleri yaptıktan sonra http://yourwebapp açın.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="0aaa3-200">Merhaba Liferay portal hello web uygulama kökünden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0aaa3-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0aaa3-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0aaa3-201">Next steps</span></span>
<span data-ttu-id="0aaa3-202">Liferay hakkında daha fazla bilgi için bkz: [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="0aaa3-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="0aaa3-203">Java hakkında daha fazla bilgi için ziyaret [Java geliştiriciler için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="0aaa3-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714

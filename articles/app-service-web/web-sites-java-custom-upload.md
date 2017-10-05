---
title: "Azure’a özel bir Java web uygulaması yükleme"
description: "Bu öğreticide Azure App Service Web Apps için özel bir Java web uygulaması karşıya nasıl yükleneceğini gösterir."
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
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="f039d-103">Azure’a özel bir Java web uygulaması yükleme</span><span class="sxs-lookup"><span data-stu-id="f039d-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="f039d-104">Bu konuda bir özel Java web uygulaması karşıya nasıl yükleneceğini açıklar [Azure App Service] Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="f039d-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="f039d-105">Herhangi bir Java Web sitesi veya web uygulama ve ayrıca bazı örnekler belirli uygulamalar için geçerli olan bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f039d-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="f039d-106">Azure konumundaki açıklandığı gibi Azure Portal'ın yapılandırma kullanıcı Arabirimi ve Azure Marketi kullanarak Java web uygulamaları oluşturmak için bir yol sağlar Not [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f039d-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="f039d-107">Bu öğreticide Azure Portal yapılandırmasını kullanmasını istediğiniz olmayan senaryolar için kullanıcı Arabirimi veya Azure Marketi değil.</span><span class="sxs-lookup"><span data-stu-id="f039d-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="f039d-108">Yapılandırma yönergeleri</span><span class="sxs-lookup"><span data-stu-id="f039d-108">Configuration guidelines</span></span>
<span data-ttu-id="f039d-109">Azure'daki özel Java web uygulamaları için beklenen ayarlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="f039d-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="f039d-110">Java işlemi tarafından kullanılan HTTP bağlantı noktası dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="f039d-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="f039d-111">İşlemi bağlantı noktasından ortam değişkeni kullanmalısınız `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="f039d-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="f039d-112">Tek HTTP dinleyicisi dışındaki tüm dinleme bağlantı noktaları devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f039d-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="f039d-113">Tomcat'te kapatma, HTTPS ve AJP içeren bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="f039d-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="f039d-114">Kapsayıcı yalnızca IPv4 trafiği için yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f039d-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="f039d-115">**Başlangıç** uygulama yapılandırmasında ayarlanması gerekiyor için komutu.</span><span class="sxs-lookup"><span data-stu-id="f039d-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="f039d-116">Dizinleri yazma izni gerektiren uygulamalar olan Azure web uygulamanızın içerik, dizinde olması gereken **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="f039d-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="f039d-117">Ortam değişkeni `HOME` için D:\home başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="f039d-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="f039d-118">Ortam değişkenleri gerektiği gibi web.config dosyasında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f039d-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="f039d-119">Web.config httpPlatform yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f039d-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="f039d-120">Aşağıdaki bilgiler açıklanır **httpPlatform** web.config içinde biçimi.</span><span class="sxs-lookup"><span data-stu-id="f039d-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="f039d-121">**bağımsız değişkenler** (varsayılan = "").</span><span class="sxs-lookup"><span data-stu-id="f039d-121">**arguments** (Default="").</span></span> <span data-ttu-id="f039d-122">Yürütülebilir dosyayı veya belirtilen komut bağımsız değişkenleri **processPath** ayarı.</span><span class="sxs-lookup"><span data-stu-id="f039d-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="f039d-123">Örnekler (ile gösterilen **processPath** dahil):</span><span class="sxs-lookup"><span data-stu-id="f039d-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="f039d-124">**processPath** -çalıştırılabilir veya HTTP isteklerini dinlemeye bir işlem başlatır komut dosyası yolu.</span><span class="sxs-lookup"><span data-stu-id="f039d-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="f039d-125">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="f039d-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="f039d-126">**rapidFailsPerMinute** (varsayılan = 10.) İşlem belirtilen sayıda **processPath** dakikada kilitlenmesine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f039d-127">Bu sınır aşılırsa, **HttpPlatformHandler** dakikanın geri kalan işlemi başlatmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="f039d-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="f039d-128">**requestTimeout** (varsayılan = "00: 02:00".) Hangi süresince **HttpPlatformHandler** üzerinde dinleme işleminden yanıt bekleyeceği `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="f039d-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="f039d-129">**startupRetryCount** (varsayılan = 10.) Kaç kez **HttpPlatformHandler** belirtilen işlemini başlatmayı deneme **processPath**.</span><span class="sxs-lookup"><span data-stu-id="f039d-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="f039d-130">Bkz: **startupTimeLimit** daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="f039d-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="f039d-131">**startupTimeLimit** (varsayılan = 10 saniye.) Hangi süresince **HttpPlatformHandler** yürütülebilir/bağlantı noktasında dinleme işlemini başlatmak komut dosyası bekler.</span><span class="sxs-lookup"><span data-stu-id="f039d-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="f039d-132">Bu süre aşılırsa **HttpPlatformHandler** işlemi sonlandırır ve yeniden başlatmayı deneyin **startupRetryCount** kez.</span><span class="sxs-lookup"><span data-stu-id="f039d-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="f039d-133">**stdoutLogEnabled** (varsayılan = "true".) TRUE ise, **stdout** ve **stderr** belirtilen işlem için **processPath** ayarı, belirtilen dosyaya yönlendirilirsiniz **stdoutLogFile** (bkz **stdoutLogFile** bölümü).</span><span class="sxs-lookup"><span data-stu-id="f039d-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="f039d-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Mutlak dosya yolunu **stdout** ve **stderr** belirtilen işleminden **processPath** günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="f039d-135">`%HTTP_PLATFORM_PORT%`Belirtilen bir parçası olarak ya da gereken özel bir yer tutucudur **bağımsız değişkenleri** veya parçası olarak **httpPlatform** **environmentVariables** listesi.</span><span class="sxs-lookup"><span data-stu-id="f039d-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="f039d-136">Bu tarafından dahili olarak oluşturulan bir bağlantı noktası tarafından değiştirilecek **HttpPlatformHandler** böylece işlemi tarafından belirtilen **processPath** Bu bağlantı noktasında dinleme.</span><span class="sxs-lookup"><span data-stu-id="f039d-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="f039d-137">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="f039d-137">Deployment</span></span>
<span data-ttu-id="f039d-138">Java tabanlı web uygulamaları kolayca çoğu Internet Information Services (IIS) ile kullanılan aynı anlamına gelir üzerinden dağıtılabilir tabanlı web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="f039d-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="f039d-139">Web uygulamaları için tümleşik SCM yeteneğini olarak FTP, Git ve Kudu tüm dağıtım düzenekleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f039d-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="f039d-140">Java Visual Studio'da geliştirilen değil gibi bir protokol olarak WebDeploy çalışır ancak WebDeploy Java web uygulama dağıtım kullanım örnekleri ile uyuşmaz.</span><span class="sxs-lookup"><span data-stu-id="f039d-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="f039d-141">Uygulama yapılandırması örnekleri</span><span class="sxs-lookup"><span data-stu-id="f039d-141">Application configuration Examples</span></span>
<span data-ttu-id="f039d-142">Aşağıdaki uygulamalar, bir web.config dosyası ve uygulama için yapılandırma Java uygulamanızı App Service Web Apps etkinleştirme göstermek için örnek olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f039d-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="f039d-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="f039d-143">Tomcat</span></span>
<span data-ttu-id="f039d-144">App Service Web Apps ile sağlanan iki Tomcat çeşidi olsa da, hala müşteri belirli örnekleri karşıya yüklemek oldukça mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f039d-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="f039d-145">Aşağıda, Tomcat bir farklı Java sanal makine (JVM) ile yüklenmesini örneğidir.</span><span class="sxs-lookup"><span data-stu-id="f039d-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="f039d-146">Tomcat tarafında yapılması gereken birkaç yapılandırma değişiklikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f039d-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="f039d-147">Server.xml ayarlamak için düzenlenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f039d-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="f039d-148">Kapatma bağlantı noktası = -1</span><span class="sxs-lookup"><span data-stu-id="f039d-148">Shutdown port = -1</span></span>
* <span data-ttu-id="f039d-149">HTTP Bağlayıcısı bağlantı noktası = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="f039d-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="f039d-150">HTTP Bağlayıcısı adresi = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="f039d-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="f039d-151">HTTPS ve AJP Bağlayıcılarına açıklama</span><span class="sxs-lookup"><span data-stu-id="f039d-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="f039d-152">IPv4 ayarı, ekleyebileceğiniz catalina.properties dosyasında da ayarlanabilir.`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="f039d-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="f039d-153">App Service Web Apps üzerinde Direct3D çağrıları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f039d-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="f039d-154">Bu devre dışı bırakmak için uygulamanızın tür çağrılar olmalısınız şu Java seçeneğini ekleyin:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="f039d-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="f039d-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="f039d-155">Jetty</span></span>
<span data-ttu-id="f039d-156">Tomcat için olduğu gibi müşterilerin kendi örnekleri için Jetty karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f039d-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="f039d-157">Jetty'nin tam yüklemesini çalıştıran söz konusu olduğunda, yapılandırma şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="f039d-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

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

<span data-ttu-id="f039d-158">Jetty yapılandırması ayarlamak için start.ini değiştirilmesi gereken `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="f039d-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="f039d-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="f039d-159">Springboot</span></span>
<span data-ttu-id="f039d-160">Bir Springboot alabilmek için JAR veya WAR dosyasını karşıya yükleyin ve aşağıdaki web.config dosyası ekleyin, çalışan uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="f039d-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="f039d-161">Web.config dosyasına wwwroot klasörüne gider.</span><span class="sxs-lookup"><span data-stu-id="f039d-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="f039d-162">Web.config dosyasında JAR dosyasını da wwwroot klasöründe bulunan aşağıdaki örnekte, JAR dosyasını işaret edecek şekilde bağımsız değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f039d-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="f039d-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="f039d-163">Hudson</span></span>
<span data-ttu-id="f039d-164">Bizim test Hudson 3.1.2 war ve varsayılan Tomcat 7.0.50 örnek kullanılan şeyler ayarlamak için kullanıcı arabirimini kullanarak olmadan.</span><span class="sxs-lookup"><span data-stu-id="f039d-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="f039d-165">Bir yazılım derleme aracını Hudson olduğu için ayrılmış örneklerinde yüklemek için önerilir nerede **AlwaysOn** bayrak web uygulamasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="f039d-166">Yani, web uygulamanızın içinde dizin, kök **d:\home\site\wwwroot**, oluşturma bir **webapps** dizini (yoksa) ve Hudson.war içinde yerleştirin **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="f039d-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="f039d-167">Apache maven 3.0.5 (Hudson ile uyumlu) indirin ve yerleştirileceği **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="f039d-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="f039d-168">Web.config dosyasında oluşturma **d:\home\site\wwwroot** ve aşağıdaki içeriği yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="f039d-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
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
   
    <span data-ttu-id="f039d-169">Bu noktada web uygulaması değişiklikleri almak için yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="f039d-170">Hudson başlatmak için http://yourwebapp/hudson için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f039d-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="f039d-171">Hudson kendisini yapılandırdıktan sonra aşağıdaki ekran görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f039d-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="f039d-173">Erişim Hudson yapılandırma sayfası: tıklatın **yönetmek Hudson**ve ardından **yapılandırma sistem**.</span><span class="sxs-lookup"><span data-stu-id="f039d-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="f039d-174">JDK aşağıda gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f039d-174">Configure the JDK as shown below:</span></span>
   
    ![Hudson yapılandırma](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="f039d-176">Maven aşağıda gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f039d-176">Configure Maven as shown below:</span></span>
   
    ![Maven yapılandırma](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="f039d-178">Ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f039d-178">Save the settings.</span></span> <span data-ttu-id="f039d-179">Hudson artık yapılandırıldı ve kullanım için hazır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f039d-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="f039d-180">Hudson hakkında ek bilgi için bkz: [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="f039d-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="f039d-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="f039d-181">Liferay</span></span>
<span data-ttu-id="f039d-182">Liferay App Service Web Apps üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f039d-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="f039d-183">Liferay önemli bellek gerektirebilir olduğundan, yeterli bellek sağlayabilen bir orta veya büyük adanmış çalışan üzerinde çalıştırmak için web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f039d-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="f039d-184">Liferay de başlatılması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="f039d-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="f039d-185">Bu nedenle, web uygulaması ayarlamak önerilir **her zaman açık**.</span><span class="sxs-lookup"><span data-stu-id="f039d-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="f039d-186">Liferay Community Edition GA3 paketlenmiş 6.1.2 Tomcat kullanarak, aşağıdaki dosyaları Liferay indirdikten sonra düzenlendi:</span><span class="sxs-lookup"><span data-stu-id="f039d-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="f039d-187">**Server.XML**</span><span class="sxs-lookup"><span data-stu-id="f039d-187">**Server.xml**</span></span>

* <span data-ttu-id="f039d-188">Kapatma bağlantı noktası -1 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f039d-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="f039d-189">Değişiklik HTTP Bağlayıcısı`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="f039d-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="f039d-190">Out AJP bağlayıcı açıklama.</span><span class="sxs-lookup"><span data-stu-id="f039d-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="f039d-191">İçinde **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** klasör adında bir dosya oluşturun **portal ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="f039d-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="f039d-192">Bu dosya, aşağıda gösterildiği gibi tek bir çizgi içeren gerekir:</span><span class="sxs-lookup"><span data-stu-id="f039d-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="f039d-193">Tomcat 7.0.40 klasörüyle aynı dizin düzeyinde adlı bir dosya oluşturun **web.config** aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="f039d-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

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

<span data-ttu-id="f039d-194">Altında **httpPlatform** bloğu **requestTimeout** ayarlamak "00: 10:00".</span><span class="sxs-lookup"><span data-stu-id="f039d-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="f039d-195">Sınırlı, ancak ardından, Liferay önyükleme sırasında bazı zaman aşımı hatalar görmeniz olasıdır.</span><span class="sxs-lookup"><span data-stu-id="f039d-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="f039d-196">Bu değer değiştiyse, sonra **connectionTimeout** tomcat server.xml değiştirilmeleri.</span><span class="sxs-lookup"><span data-stu-id="f039d-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="f039d-197">Bu, 64-bit JDK işaret edecek şekilde yukarıdaki web.config JRE_HOME ortama varariable belirtilen dikkate değerdir.</span><span class="sxs-lookup"><span data-stu-id="f039d-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="f039d-198">Varsayılan, 32-bit olmakla birlikte Liferay yüksek düzeyde bellek gerekebileceği için 64-bit JDK kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="f039d-199">Sonra web uygulamanızı Liferay yeniden, bu değişiklikleri yaptıktan sonra http://yourwebapp açın.</span><span class="sxs-lookup"><span data-stu-id="f039d-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="f039d-200">Web uygulaması kökünden Liferay portal kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f039d-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f039d-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f039d-201">Next steps</span></span>
<span data-ttu-id="f039d-202">Liferay hakkında daha fazla bilgi için bkz: [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="f039d-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="f039d-203">Java hakkında daha fazla bilgi için ziyaret [Java geliştiriciler için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="f039d-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714

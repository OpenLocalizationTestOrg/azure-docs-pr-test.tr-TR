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
# <a name="upload-a-custom-java-web-app-tooazure"></a>Özel bir Java web uygulaması tooAzure karşıya yükle
Bu konuda, nasıl tooupload özel bir Java web uygulaması çok açıklanmaktadır[Azure App Service] Web uygulamaları. Tooany Java Web sitesi veya web uygulaması ve ayrıca bazı örnekler belirli uygulamalar için geçerli olan bilgileri içerir.

Azure hello Azure Portal'ın yapılandırma kullanıcı Arabirimi kullanarak Java web uygulamaları oluşturmak için bir yol sağlar not edin ve Azure Marketi adresindeki açıklandığı gibi hello [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md). İçinde istememiş toouse hello Azure Portal yapılandırma kullanıcı Arabirimi veya Azure Marketi hello senaryoları için öğreticidir.  

## <a name="configuration-guidelines"></a>Yapılandırma yönergeleri
Hello azure'daki özel Java web uygulamaları için beklenen hello ayarları açıklanmıştır.

* Merhaba Java işlemi tarafından kullanılan hello HTTP bağlantı noktası dinamik olarak atanır.  Merhaba işlem, başlangıç bağlantı noktasından hello ortam değişkeni kullanmalıdır `HTTP_PLATFORM_PORT`.
* Merhaba tek HTTP dinleyicisi devre dışı bırakılmalıdır dışındaki tüm bağlantı noktalarını dinler.  Tomcat'te hello kapatma, HTTPS ve AJP içeren bağlantı noktaları.
* Merhaba kapsayıcı yalnızca IPv4 trafiği için yapılandırılmış toobe gerekir.
* Merhaba **başlangıç** toobe Merhaba uygulaması gereken için komut hello yapılandırmasında ayarlayın.
* Dizinleri yazma izni gerektiren uygulamalar ihtiyacınız olan hello Azure web uygulamanızın içerik, dizininde toobe **D:\home**.  Merhaba ortam değişkeni `HOME` tooD:\home başvuruyor.  

Ortam değişkenleri gerektiği gibi hello web.config dosyasında ayarlayabilirsiniz.

## <a name="webconfig-httpplatform-configuration"></a>Web.config httpPlatform yapılandırması
Merhaba aşağıdaki bilgileri açıklar hello **httpPlatform** web.config içinde biçimi.

**bağımsız değişkenler** (varsayılan = ""). Bağımsız değişkenler toohello çalıştırılabilir veya hello belirtilen komut dosyası **processPath** ayarı.

Örnekler (ile gösterilen **processPath** dahil):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -yol toohello çalıştırılabilir veya HTTP isteklerini dinlemeye bir işlem başlatır komut dosyası.

Örnekler:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (varsayılan = 10.) Sayısı hello işlemi belirtilen zaman **processPath** toocrash dakikada izin verilir. Bu sınır aşılırsa, **HttpPlatformHandler** hello dakika hello kalanı için hello işlemi başlatmayı durdurur.

**requestTimeout** (varsayılan = "00: 02:00".) Hangi süresince **HttpPlatformHandler** dinlemede hello işleminden yanıt bekleyeceği `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (varsayılan = 10.) Kaç kez **HttpPlatformHandler** belirtilen toolaunch hello işlem deneyecek **processPath**. Bkz: **startupTimeLimit** daha fazla ayrıntı için.

**startupTimeLimit** (varsayılan = 10 saniye.) Hangi süresince **HttpPlatformHandler** hello yürütülebilir/komut dosyası toostart için başlangıç bağlantı noktasını dinleyen bir işlem bekler.  Bu süre aşılırsa **HttpPlatformHandler** KILL hello işlemi ve toolaunch deneyin yeniden **startupRetryCount** kez.

**stdoutLogEnabled** (varsayılan = "true".) TRUE ise, **stdout** ve **stderr** hello belirtilen hello işlemi için **processPath** ayarı belirtilen yeniden yönlendirilen toohello dosya olacaktır  **stdoutLogFile** (bkz **stdoutLogFile** bölümü).

**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Mutlak dosya yolunu **stdout** ve **stderr** belirtilen hello işleminden **processPath** günlüğe kaydedilir.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`toospecified parçası olarak ya da gereken özel bir yer tutucudur **bağımsız değişkenleri** veya hello parçası olarak **httpPlatform** **environmentVariables** listesi. Bu tarafından dahili olarak oluşturulan bir bağlantı noktası tarafından değiştirilecek **HttpPlatformHandler** böylece hello işlemi tarafından belirtilen **processPath** Bu bağlantı noktasında dinleme.
> 
> 

## <a name="deployment"></a>Dağıtım
Java tabanlı web uygulamalarını kolayca hello Internet Information Services (IIS) tabanlı web uygulamaları ile kullanılan aynı anlamına gelir hello çoğunu üzerinden dağıtılabilir.  FTP, Git ve Kudu tümü olduğu hello gibi web uygulamaları için tümleşik SCM yeteneğini dağıtım düzenekleri desteklenir. Java Visual Studio'da geliştirilen değil gibi bir protokol olarak WebDeploy çalışır ancak WebDeploy Java web uygulama dağıtım kullanım örnekleri ile uyuşmaz.

## <a name="application-configuration-examples"></a>Uygulama yapılandırması örnekleri
Aşağıdaki uygulamalar, bir web.config dosyası ve hello hello için uygulama yapılandırma örnekleri tooshow nasıl sağlandığını tooenable Java uygulamanızı App Service Web Apps üzerinde.

### <a name="tomcat"></a>Tomcat
App Service Web Apps ile sağlanan iki Tomcat çeşidi olsa da, mümkün oldukça tooupload müşteri belirli örnekler hala geçerlidir. Aşağıda, Tomcat bir farklı Java sanal makine (JVM) ile yüklenmesini örneğidir.

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

Merhaba Tomcat yan üzerinde yapılan toobe gereken birkaç yapılandırma değişikliği yok. Merhaba server.xml düzenlenen toobe tooset gerekir:

* Kapatma bağlantı noktası = -1
* HTTP Bağlayıcısı bağlantı noktası = ${port.http}
* HTTP Bağlayıcısı adresi = "127.0.0.1"
* HTTPS ve AJP Bağlayıcılarına açıklama
* Merhaba IPv4 ayarı, ekleyebileceğiniz hello catalina.properties dosyasında da ayarlanabilir.`java.net.preferIPv4Stack=true`

App Service Web Apps üzerinde Direct3D çağrıları desteklenmez. toodisable olanlar, ekleyin uygulamanız bu tür çağrılar olmalısınız Java seçenekten hello:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Merhaba Tomcat için olduğu gibi müşteriler kendi örnekleri için Jetty karşıya yükleyebilirsiniz. Jetty çalışan hello tam yüklemesi Hello durumda hello yapılandırma şöyle olabilir:

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

Merhaba Jetty yapılandırması gereken hello start.ini tooset değiştirilen toobe `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
Sipariş tooget çalıştırdığınız Springboot uygulama JAR veya WAR dosyası tooupload gerekir ve hello aşağıdaki web.config dosyasına ekleyin. Merhaba web.config dosyasında hello wwwroot klasörüne gider. Merhaba web.config dosyasında hello bağımsız değişkenleri toopoint tooyour JAR dosyasını ayarlamak için hello aşağıdaki örnek hello JAR dosyasına da hello wwwroot klasöründe bulunur.  

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


### <a name="hudson"></a>Hudson
Kullanılan bizim test Hudson 3.1.2 war hello ve varsayılan Tomcat 7.0.50 örnek hello ancak hello UI tooset şeyler kullanmadan.  Hudson yazılımları yapı aracı, bunu tavsiye edilir tooinstall olduğundan üzerinde ayrılmış örnekleri hello burada **AlwaysOn** bayrak hello web uygulaması üzerinde ayarlanabilir.

1. Yani, web uygulamanızın içinde dizin, kök **d:\home\site\wwwroot**, oluşturma bir **webapps** dizini (yoksa) ve Hudson.war içinde yerleştirin **d:\home\site\wwwroot\webapps**.
2. Apache maven 3.0.5 (Hudson ile uyumlu) indirin ve yerleştirileceği **d:\home\site\wwwroot**.
3. Web.config dosyasında oluşturma **d:\home\site\wwwroot** Yapıştır hello izleyerek, içeriği:
   
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
   
    Bu noktada hello web uygulaması yeniden tootake hello değişiklikler olabilir.  Toohttp://yourwebapp/hudson toostart Hudson bağlayın.
4. Hudson kendisini yapılandırdıktan sonra aşağıdaki ekran hello görmeniz gerekir:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Erişim hello Hudson yapılandırma sayfası: tıklatın **yönetmek Hudson**ve ardından **yapılandırma sistem**.
6. Merhaba aşağıda gösterildiği gibi JDK yapılandırın:
   
    ![Hudson yapılandırma](./media/web-sites-java-custom-upload/hudson2.png)
7. Maven aşağıda gösterildiği gibi yapılandırın:
   
    ![Maven yapılandırma](./media/web-sites-java-custom-upload/maven.png)
8. Hello ayarları kaydedin. Hudson artık yapılandırıldı ve kullanım için hazır olması gerekir.

Hudson hakkında ek bilgi için bkz: [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay App Service Web Apps üzerinde desteklenir. Liferay önemli bellek gerektirebilir olduğundan, yeterli bellek sağlayabilen bir orta veya büyük adanmış çalışan üzerinde toorun hello web uygulaması gerekir. Liferay birkaç dakika toostart da alır. Bu nedenle, hello web uygulaması çok ayarlamanız önerilir**her zaman açık**.  

Tomcat ile Liferay Community Edition GA3 paketlenmiş 6.1.2 kullanarak hello aşağıdaki dosyaları Liferay indirdikten sonra düzenlendi:

**Server.XML**

* Kapatma bağlantı noktası çok-1 olarak değiştirin.
* HTTP Bağlayıcısı çok değiştirme`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Merhaba AJP bağlayıcı açıklama.

Merhaba, **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** klasör adında bir dosya oluşturun **portal ext.properties**. Bu dosya toocontain bir satır, aşağıda gösterildiği gibi gerekir:

    liferay.home=%HOME%/site/wwwroot/liferay

Merhaba hello tomcat 7.0.40 klasörü, aynı dizin düzeyinde adlı bir dosya oluşturmak **web.config** içeriği aşağıdaki hello ile:

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

Merhaba altında **httpPlatform** hello bloğunu **requestTimeout** çok Ayarla "00: 10:00".  Sınırlı ancak sonra büyük olasılıkla toosee sırasında bazı zaman aşımı hataları var Liferay önyükleme.  Bu değer değiştiyse, ardından hello **connectionTimeout** hello tomcat'te server.xml değiştirilmeleri.  

Bu hello JRE_HOME ortama varariable hello web.config toopoint toohello yukarıda belirtilen dikkate değerdir 64-bit JDK. Merhaba varsayılandır 32-bit, ancak yüksek düzeyde bellek Liferay gerekebileceği toouse önerilir 64-bit JDK hello.

Sonra web uygulamanızı Liferay yeniden, bu değişiklikleri yaptıktan sonra http://yourwebapp açın. Merhaba Liferay portal hello web uygulama kökünden kullanılabilir. 

## <a name="next-steps"></a>Sonraki adımlar
Liferay hakkında daha fazla bilgi için bkz: [http://www.liferay.com](http://www.liferay.com).

Java hakkında daha fazla bilgi için ziyaret [Java geliştiriciler için Azure](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714

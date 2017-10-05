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
# <a name="upload-a-custom-java-web-app-to-azure"></a>Azure’a özel bir Java web uygulaması yükleme
Bu konuda bir özel Java web uygulaması karşıya nasıl yükleneceğini açıklar [Azure App Service] Web uygulamaları. Herhangi bir Java Web sitesi veya web uygulama ve ayrıca bazı örnekler belirli uygulamalar için geçerli olan bilgileri içerir.

Azure konumundaki açıklandığı gibi Azure Portal'ın yapılandırma kullanıcı Arabirimi ve Azure Marketi kullanarak Java web uygulamaları oluşturmak için bir yol sağlar Not [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md). Bu öğreticide Azure Portal yapılandırmasını kullanmasını istediğiniz olmayan senaryolar için kullanıcı Arabirimi veya Azure Marketi değil.  

## <a name="configuration-guidelines"></a>Yapılandırma yönergeleri
Azure'daki özel Java web uygulamaları için beklenen ayarlarını açıklar.

* Java işlemi tarafından kullanılan HTTP bağlantı noktası dinamik olarak atanır.  İşlemi bağlantı noktasından ortam değişkeni kullanmalısınız `HTTP_PLATFORM_PORT`.
* Tek HTTP dinleyicisi dışındaki tüm dinleme bağlantı noktaları devre dışı bırakılması gerekir.  Tomcat'te kapatma, HTTPS ve AJP içeren bağlantı noktaları.
* Kapsayıcı yalnızca IPv4 trafiği için yapılandırılması gerekir.
* **Başlangıç** uygulama yapılandırmasında ayarlanması gerekiyor için komutu.
* Dizinleri yazma izni gerektiren uygulamalar olan Azure web uygulamanızın içerik, dizinde olması gereken **D:\home**.  Ortam değişkeni `HOME` için D:\home başvuruyor.  

Ortam değişkenleri gerektiği gibi web.config dosyasında ayarlayabilirsiniz.

## <a name="webconfig-httpplatform-configuration"></a>Web.config httpPlatform yapılandırması
Aşağıdaki bilgiler açıklanır **httpPlatform** web.config içinde biçimi.

**bağımsız değişkenler** (varsayılan = ""). Yürütülebilir dosyayı veya belirtilen komut bağımsız değişkenleri **processPath** ayarı.

Örnekler (ile gösterilen **processPath** dahil):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -çalıştırılabilir veya HTTP isteklerini dinlemeye bir işlem başlatır komut dosyası yolu.

Örnekler:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (varsayılan = 10.) İşlem belirtilen sayıda **processPath** dakikada kilitlenmesine izin verilir. Bu sınır aşılırsa, **HttpPlatformHandler** dakikanın geri kalan işlemi başlatmayı durdurur.

**requestTimeout** (varsayılan = "00: 02:00".) Hangi süresince **HttpPlatformHandler** üzerinde dinleme işleminden yanıt bekleyeceği `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (varsayılan = 10.) Kaç kez **HttpPlatformHandler** belirtilen işlemini başlatmayı deneme **processPath**. Bkz: **startupTimeLimit** daha fazla ayrıntı için.

**startupTimeLimit** (varsayılan = 10 saniye.) Hangi süresince **HttpPlatformHandler** yürütülebilir/bağlantı noktasında dinleme işlemini başlatmak komut dosyası bekler.  Bu süre aşılırsa **HttpPlatformHandler** işlemi sonlandırır ve yeniden başlatmayı deneyin **startupRetryCount** kez.

**stdoutLogEnabled** (varsayılan = "true".) TRUE ise, **stdout** ve **stderr** belirtilen işlem için **processPath** ayarı, belirtilen dosyaya yönlendirilirsiniz **stdoutLogFile** (bkz **stdoutLogFile** bölümü).

**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Mutlak dosya yolunu **stdout** ve **stderr** belirtilen işleminden **processPath** günlüğe kaydedilir.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`Belirtilen bir parçası olarak ya da gereken özel bir yer tutucudur **bağımsız değişkenleri** veya parçası olarak **httpPlatform** **environmentVariables** listesi. Bu tarafından dahili olarak oluşturulan bir bağlantı noktası tarafından değiştirilecek **HttpPlatformHandler** böylece işlemi tarafından belirtilen **processPath** Bu bağlantı noktasında dinleme.
> 
> 

## <a name="deployment"></a>Dağıtım
Java tabanlı web uygulamaları kolayca çoğu Internet Information Services (IIS) ile kullanılan aynı anlamına gelir üzerinden dağıtılabilir tabanlı web uygulamaları.  Web uygulamaları için tümleşik SCM yeteneğini olarak FTP, Git ve Kudu tüm dağıtım düzenekleri desteklenir. Java Visual Studio'da geliştirilen değil gibi bir protokol olarak WebDeploy çalışır ancak WebDeploy Java web uygulama dağıtım kullanım örnekleri ile uyuşmaz.

## <a name="application-configuration-examples"></a>Uygulama yapılandırması örnekleri
Aşağıdaki uygulamalar, bir web.config dosyası ve uygulama için yapılandırma Java uygulamanızı App Service Web Apps etkinleştirme göstermek için örnek olarak sağlanır.

### <a name="tomcat"></a>Tomcat
App Service Web Apps ile sağlanan iki Tomcat çeşidi olsa da, hala müşteri belirli örnekleri karşıya yüklemek oldukça mümkündür. Aşağıda, Tomcat bir farklı Java sanal makine (JVM) ile yüklenmesini örneğidir.

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

Tomcat tarafında yapılması gereken birkaç yapılandırma değişiklikleri vardır. Server.xml ayarlamak için düzenlenmesi gerekir:

* Kapatma bağlantı noktası = -1
* HTTP Bağlayıcısı bağlantı noktası = ${port.http}
* HTTP Bağlayıcısı adresi = "127.0.0.1"
* HTTPS ve AJP Bağlayıcılarına açıklama
* IPv4 ayarı, ekleyebileceğiniz catalina.properties dosyasında da ayarlanabilir.`java.net.preferIPv4Stack=true`

App Service Web Apps üzerinde Direct3D çağrıları desteklenmez. Bu devre dışı bırakmak için uygulamanızın tür çağrılar olmalısınız şu Java seçeneğini ekleyin:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Tomcat için olduğu gibi müşterilerin kendi örnekleri için Jetty karşıya yükleyebilirsiniz. Jetty'nin tam yüklemesini çalıştıran söz konusu olduğunda, yapılandırma şöyle olabilir:

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

Jetty yapılandırması ayarlamak için start.ini değiştirilmesi gereken `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
Bir Springboot alabilmek için JAR veya WAR dosyasını karşıya yükleyin ve aşağıdaki web.config dosyası ekleyin, çalışan uygulama gerekir. Web.config dosyasına wwwroot klasörüne gider. Web.config dosyasında JAR dosyasını da wwwroot klasöründe bulunan aşağıdaki örnekte, JAR dosyasını işaret edecek şekilde bağımsız değişkenleri ayarlayın.  

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
Bizim test Hudson 3.1.2 war ve varsayılan Tomcat 7.0.50 örnek kullanılan şeyler ayarlamak için kullanıcı arabirimini kullanarak olmadan.  Bir yazılım derleme aracını Hudson olduğu için ayrılmış örneklerinde yüklemek için önerilir nerede **AlwaysOn** bayrak web uygulamasında ayarlanabilir.

1. Yani, web uygulamanızın içinde dizin, kök **d:\home\site\wwwroot**, oluşturma bir **webapps** dizini (yoksa) ve Hudson.war içinde yerleştirin **d:\home\site\wwwroot\webapps**.
2. Apache maven 3.0.5 (Hudson ile uyumlu) indirin ve yerleştirileceği **d:\home\site\wwwroot**.
3. Web.config dosyasında oluşturma **d:\home\site\wwwroot** ve aşağıdaki içeriği yapıştırın:
   
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
   
    Bu noktada web uygulaması değişiklikleri almak için yeniden başlatılabilir.  Hudson başlatmak için http://yourwebapp/hudson için bağlayın.
4. Hudson kendisini yapılandırdıktan sonra aşağıdaki ekran görmeniz gerekir:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Erişim Hudson yapılandırma sayfası: tıklatın **yönetmek Hudson**ve ardından **yapılandırma sistem**.
6. JDK aşağıda gösterildiği gibi yapılandırın:
   
    ![Hudson yapılandırma](./media/web-sites-java-custom-upload/hudson2.png)
7. Maven aşağıda gösterildiği gibi yapılandırın:
   
    ![Maven yapılandırma](./media/web-sites-java-custom-upload/maven.png)
8. Ayarları kaydedin. Hudson artık yapılandırıldı ve kullanım için hazır olması gerekir.

Hudson hakkında ek bilgi için bkz: [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay App Service Web Apps üzerinde desteklenir. Liferay önemli bellek gerektirebilir olduğundan, yeterli bellek sağlayabilen bir orta veya büyük adanmış çalışan üzerinde çalıştırmak için web uygulaması gerekir. Liferay de başlatılması birkaç dakika sürer. Bu nedenle, web uygulaması ayarlamak önerilir **her zaman açık**.  

Liferay Community Edition GA3 paketlenmiş 6.1.2 Tomcat kullanarak, aşağıdaki dosyaları Liferay indirdikten sonra düzenlendi:

**Server.XML**

* Kapatma bağlantı noktası -1 olarak değiştirin.
* Değişiklik HTTP Bağlayıcısı`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Out AJP bağlayıcı açıklama.

İçinde **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** klasör adında bir dosya oluşturun **portal ext.properties**. Bu dosya, aşağıda gösterildiği gibi tek bir çizgi içeren gerekir:

    liferay.home=%HOME%/site/wwwroot/liferay

Tomcat 7.0.40 klasörüyle aynı dizin düzeyinde adlı bir dosya oluşturun **web.config** aşağıdaki içeriğe sahip:

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

Altında **httpPlatform** bloğu **requestTimeout** ayarlamak "00: 10:00".  Sınırlı, ancak ardından, Liferay önyükleme sırasında bazı zaman aşımı hatalar görmeniz olasıdır.  Bu değer değiştiyse, sonra **connectionTimeout** tomcat server.xml değiştirilmeleri.  

Bu, 64-bit JDK işaret edecek şekilde yukarıdaki web.config JRE_HOME ortama varariable belirtilen dikkate değerdir. Varsayılan, 32-bit olmakla birlikte Liferay yüksek düzeyde bellek gerekebileceği için 64-bit JDK kullanmak için önerilir.

Sonra web uygulamanızı Liferay yeniden, bu değişiklikleri yaptıktan sonra http://yourwebapp açın. Web uygulaması kökünden Liferay portal kullanılabilir. 

## <a name="next-steps"></a>Sonraki adımlar
Liferay hakkında daha fazla bilgi için bkz: [http://www.liferay.com](http://www.liferay.com).

Java hakkında daha fazla bilgi için ziyaret [Java geliştiriciler için Azure](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714

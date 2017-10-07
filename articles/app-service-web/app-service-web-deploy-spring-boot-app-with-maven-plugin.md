---
title: "Azure Web Apps toodeploy yay önyükleme uygulama tooAzure aaaHow toouse Merhaba Maven eklentisi"
description: "Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy yay önyükleme uygulama tooAzure öğrenin."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy yay önyükleme uygulama tooAzure

Merhaba [Azure Web uygulamaları için Maven eklentisi](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) için [Apache Maven](http://maven.apache.org/) Maven projelerine Azure App Service'in sorunsuz tümleştirme sağlar ve geliştiriciler toodeploy web uygulamaları için hello işlemini kolaylaştırır Uygulama hizmeti tooAzure.

Bu makalede Azure Web Apps toodeploy hello Maven eklentisi kullanarak bir örnek yay önyükleme uygulama tooAzure uygulama hizmetleri gösterilmektedir.

> [!NOTE]
>
> Hello Azure Web uygulamaları için Maven eklentisi şu anda önizleme olarak kullanılabilir. Ek özellikler hello gelecek için planlanan olsa da, şimdilik yalnızca FTP Yayımlama, desteklenir.
>

## <a name="prerequisites"></a>Ön koşullar

Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:

* Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].
* Merhaba [Azure komut satırı arabirimi (CLI)].
* Güncel [Java Geliştirme Seti (JDK)], 1,7 veya sonraki bir sürümü.
* Apache'nın [Maven] aracını (sürüm 3) yapılandırma.
* A [Git] istemci.

## <a name="clone-hello-sample-spring-boot-web-app"></a>Kopya hello örnek yay önyükleme web uygulaması

Bu bölümde, tamamlanmış bir yay önyükleme uygulama kopyalama ve yerel olarak test.

1. Bir komut istemi veya terminal penceresi açın ve yerel dizin toohold yay önyükleme uygulama ve değişiklik toothat dizin oluşturun; Örneğin:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   --ya da--
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Kopya hello [yay önyükleme Başlarken] örnek proje hello dizinine oluşturduğunuz; örneğin:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Dizin tamamlandı toohello proje Değiştir; Örneğin:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:
   ```shell
   mvn clean package
   ```

1. Merhaba web uygulaması oluşturduğunuzda Maven kullanarak hello web uygulaması başlatın; Örneğin:
   ```shell
   mvn spring-boot:run
   ```

1. Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın. Örneğin, hello curl kullanılabilir varsa, aşağıdaki komutu kullanabilirsiniz:
   ```shell
   curl http://localhost:8080
   ```

1. Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**

## <a name="create-an-azure-service-principal"></a>Bir Azure hizmet sorumlusu oluşturma

Bu bölümde, bir Azure web uygulaması tooAzure dağıtırken Maven eklentisi kullanır hello hizmet sorumlusu oluşturun.

1. Bir komut istemi açın.

1. Azure CLI kullanarak Azure hesabınızda oturum hello:
   ```shell
   az login
   ```
   Oturum açma Hello yönergeleri toocomplete hello süreci izleyin.

1. Bir Azure hizmet sorumlusu oluşturun:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Burada `uuuuuuuu` hello kullanıcı adı ve `pppppppp` hello hizmet sorumlusu hello parolası.

1. Azure aşağıdaki örneğine hello benzer JSON ile yanıt verir:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Web uygulaması tooAzure hello Maven eklentisi toodeploy yapılandırdığınızda bu JSON yanıt hello değerleri kullanır. Merhaba `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, ve `tttttttt` olan yer tutucu değerlerini olduğunuz isteğe bağlı olarak bu örnek toomake daha kolay toomap kullanılan, Maven yapılandırdığınızda bu değerleri tootheir ilgili öğeleri `settings.xml` hello sonraki dosyayı bölüm.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Maven toouse, Azure hizmet sorumlusu yapılandırın

Bu bölümde, web uygulaması tooAzure dağıtırken Maven kullanan, Azure hizmet asıl tooconfigure hello kimlik doğrulamasını hello değerleri kullanın.

1. Maven açmak `settings.xml` dosyasını bir metin düzenleyicisinde; bu dosya yolunda hello örnekler aşağıdaki gibi olabilir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Azure hizmet asıl ayarlarınızı hello önceki Bu öğretici toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Konumlar:
   Öğesi | Açıklama
   ---|---|---
   `<id>` | Web uygulaması tooAzure dağıttığınızda, Maven toolook, güvenlik ayarlarını kullanan benzersiz bir ad belirtir.
   `<client>` | Merhaba içeren `appId` hizmet sorumlusu değeri.
   `<tenant>` | Merhaba içeren `tenant` hizmet sorumlusu değeri.
   `<key>` | Merhaba içeren `password` hizmet sorumlusu değeri.
   `<environment>` | Olan hello hedef Azure bulut ortamı tanımlar `AZURE` Bu örnekte. (Tam bir listesi ortamlarının hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri)

1. Kaydet ve Kapat hello *settings.xml* dosya.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>İsteğe bağlı:, pom.xml web uygulama tooAzure dağıtmadan önce özelleştirme

Açık hello `pom.xml` dosyasını bir metin düzenleyicisinde yay önyükleme uygulamanız için ve hello bulun `<plugin>` öğesi için `azure-webapp-maven-plugin`. Bu öğe aşağıdaki örneğine hello benzemelidir:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Merhaba Maven eklentisi için değiştirebileceğiniz birkaç değer vardır ve bu öğelerin her biri için ayrıntılı bir açıklama hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri. Denirse, bu makaledeki vurgulama değer olan birkaç değerleri vardır:

Öğesi | Açıklama
---|---|---
`<version>` | Merhaba Hello sürümünü belirtir [Azure Web uygulamaları için Maven eklentisi]. Hello listelenen hello sürüm denetlemelisiniz [Maven merkezi depo](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) kullanmakta olduğunuz tooensure hello en son sürümü.
`<authentication>` | Merhaba kimlik doğrulama bilgilerini içeren bu örnekte Azure belirtir bir `<serverId>` içeren öğeyi `azure-auth`; Maven Maven içinde bu değer toolook hello Azure hizmet asıl değerleri kullanan *settings.xml* bu makalenin önceki bölümde tanımlanan dosya.
`<resourceGroup>` | Olan hello hedef kaynak grubu belirtir `maven-plugin` Bu örnekte. Merhaba kaynak grubu, zaten yoksa, dağıtım sırasında oluşturulur.
`<appName>` | Web uygulamanız için Hello hedef adını belirtir. Bu örnekte hello hedef adıdır `maven-web-app-${maven.build.timestamp}`, hello burada `${maven.build.timestamp}` soneki, bu örnek tooavoid çakışması eklenir. (Merhaba zaman damgası isteğe bağlıdır; hello uygulama adı için benzersiz bir dize belirtin.)
`<region>` | Olan bu örnekte hello hedef bölgesi belirtir `westus`. (Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)
`<javaVersion>` | Web uygulamanız için Hello Java Çalışma zamanı sürümü belirler. (Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)
`<deploymentType>` | Web uygulamanız için dağıtım türünü belirtir. Şu an yalnızca `ftp` desteklenir, ancak diğer dağıtım türlerinde geliştirme desteği.
`<resources>` | Kaynakları ve web uygulama tooAzure dağıtırken Maven kullanan hedef konumları belirtir. Bu örnekte, iki `<resource>` öğelerini belirtmek Maven hello ve web uygulaması için hello JAR dosyasını dağıtacağınız *web.config* hello yay önyükleme proje dosyasından.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Derleme ve web uygulama tooAzure dağıtma

Bölümler, bu makalenin önceki hello tüm hello ayarlarını yapılandırdıktan sonra hazır toodeploy olan web uygulaması tooAzure. toodo, bu nedenle, hello aşağıdaki adımları kullanın:

1. Merhaba komut istemi veya daha önce kullandığınız terminal penceresinden, tüm değişiklikleri toohello yaptıysanız Maven kullanarak hello JAR dosyasını yeniden *pom.xml* dosya; örneğin:
   ```shell
   mvn clean package
   ```

1. Web uygulaması tooAzure Maven kullanarak dağıtabilirsiniz; Örneğin:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven web uygulama tooAzure dağıtacağınız; Merhaba web uygulaması zaten mevcut değilse oluşturulur.

Web dağıtıldığında mümkün toomanage olacaktır hello kullanarak [Azure portal].

* Web uygulamanızı listelenen **uygulama hizmetleri**:

   ![Azure portalında uygulama hizmetleri listelenen web uygulaması][AP01]

* Ve web uygulamanızı hello listelenir URL hello **genel bakış** web uygulamanız için:

   ![Web uygulamanız için Hello URL belirleme][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede ele alınan çeşitli teknolojiler hello hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Azure Web uygulamaları için Maven eklentisi]

* [TooAzure hello Azure CLI gelen oturum](/azure/xplat-cli-connect)

* [Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy kapsayıcılı yay önyükleme uygulama tooAzure](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven ayarları başvurusu](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[yay önyükleme Başlarken]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web uygulamaları için Maven eklentisi]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png

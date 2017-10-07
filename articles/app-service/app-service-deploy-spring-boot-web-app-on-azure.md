---
title: "aaaDeploy yay önyükleme uygulama toohello Azure App Service | Microsoft Docs"
description: "Bu öğretici, başlangıç adımları toodeploy hello yay önyükleme Başlarken web uygulama tooAzure uygulama hizmeti aracılığıyla geliştiricilerin yol gösterecektir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Yay önyükleme uygulama toohello Azure App Service'e dağıtma

Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynak çözümüdür ve bu platformu üzerine kurulmuştur hello daha popüler projeleri biridir [Yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

Bu öğretici ancak hello örnek yay önyükleme Başlarken web uygulaması oluşturma ve çok dağıtma anlatılır[Azure App Service].

### <a name="prerequisites"></a>Ön koşullar

Sipariş toocomplete hello adımlarda Bu öğreticide, toohave hello aşağıdaki gerekir:

* Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].
* Güncel bir [Java Geliştirme Seti (JDK)].
* Apache'nın [Maven] aracını (sürüm 3) yapılandırma.
* A [Git] istemci.

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Merhaba yay önyükleme Başlarken web uygulaması oluşturma

Merhaba aşağıdaki adımlar, gerekli toocreate basit bir yay önyükleme web uygulaması ve yerel olarak test hello adımlarda size yol gösterir.

1. Bir komut istemi açın ve yerel dizin toohold uygulama ve değişiklik toothat dizin oluşturun; Örneğin:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   --ya da--
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Kopya hello [yay önyükleme Başlarken] örnek proje hello dizinine yeni oluşturduğunuz; örneğin:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Dizin tamamlandı toohello proje Değiştir; Örneğin:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:
   ```
   mvn package
   ```

1. Merhaba web uygulaması oluşturulduktan sonra dizin toohello JAR dosyasını değiştirin ve hello web uygulaması başlatın; Örneğin:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Bir web tarayıcısı kullanarak toohttp://localhost:8080 göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:
   ```
   curl http://localhost:8080
   ```

1. Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**

   ![Örnek uygulaması Gözat][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Java ile kullanmak için bir Azure web uygulaması oluşturma

Aşağıdaki adımları hello Azure Web uygulaması başlangıç adımları toocreate yol, Java için gerekli hello ayarlarını yapılandırmak ve FTP kimlik bilgilerinizi yapılandırın.

1. Toohello Gözat [Azure portal] ve oturum açın.

1. Hello Azure portalı üzerinde hesabınızda oturum açtıktan sonra hello menü simgesini **uygulama hizmetleri**:
   
   ![Azure portalına][AZ01]

1. Ne zaman hello **uygulama hizmetleri** sayfası görüntülenirse, tıklatın **+ Ekle** toocreate yeni bir uygulama hizmeti.

   ![Uygulama hizmeti oluşturma][AZ02]

1. Web uygulama şablonları Hello listesi gösterildiğinde, hello hello bağlantısına tıklayın temel Microsoft Web uygulaması.

   ![Web Uygulama Şablonları][AZ03]

1. Merhaba Web uygulaması şablonu için başlangıç bilgileri sayfası görüntülendiğinde tıklayın **oluşturma**.

   ![Web Uygulaması Oluşturma][AZ04]

1. Web uygulamanız için benzersiz bir ad sağlayın ve herhangi bir ek ayarları belirtin ve ardından **oluşturma**.

   ![Web uygulaması ayarları oluşturma][AZ05]

1. Web uygulamanız oluşturulduktan sonra hello menü simgesini **uygulama hizmetleri**ve yeni oluşturulan web uygulamanız'ye tıklayın:

   ![Liste Web uygulamaları][AZ06]

1. Web uygulamanızı görüntülendiğinde hello Java Sürüm hello aşağıdaki adımları kullanarak belirtin:

   a. Merhaba tıklatın **uygulama ayarları** menü öğesi.

   b. Seçin **Java 8** hello Java sürümü için.

   c. Seçin **Newest** hello alt Java Sürüm için.

   d. Seçin **yeni Tomcat 8.5** hello web kapsayıcısı için. (Aslında bu kapsayıcı kullanılmaz; Azure hello kapsayıcı yay önyükleme uygulamanızdan kullanır.)

   e. **Kaydet** düğmesine tıklayın.

   ![Uygulama ayarları][AZ07]

1. FTP dağıtım kimlik bilgilerinizi hello aşağıdaki adımları kullanarak belirtin:

   a. Merhaba tıklatın **dağıtım kimlik bilgileri** menü öğesi.

   b. Kullanıcı adı ve parola belirtin.

   c. **Kaydet** düğmesine tıklayın.

   ![Dağıtım kimlik bilgilerini belirtin][AZ08]

1. FTP bağlantı bilgileri hello aşağıdaki adımları kullanarak Al:

   a. Merhaba tıklatın **dağıtım kimlik bilgileri** menü öğesi.

   b. Tam FTP kullanıcı adı ve URL kopyalayın ve bunları hello için bu öğreticinin sonraki bölümde kaydedin.

   ![FTP URL ve kimlik bilgileri][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Yay önyükleme web uygulama tooAzure dağıtma

Aşağıdaki adımları hello yay önyükleme web uygulama tooAzure hello adımları toodeploy yol gösterir.

1. Windows Not Defteri gibi bir metin düzenleyicide açın ve yeni bir belgeye metin aşağıdaki hello yapıştırın, ardından hello dosyası olarak kaydetmeniz *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Merhaba kaydettikten sonra *web.config* dosya tooyour sistemi, tooyour web uygulaması hello URL, kullanıcı adı ve bölüm bu öğreticinin önceki hello paroladan kullanarak FTP aracılığıyla bağlanır. Örneğin:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Web uygulamanızın hello Uzak dizin toohello kök klasörünü Değiştir (olduğu anda */site/wwwroot*), ardından yay önyükleme uygulamanızdan hello JAR dosyasını kopyalayın ve hello *web.config* daha önce gelen. Örneğin:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. JAR dağıttıktan sonra ve *web.config* dosyaları tooyour web uygulaması, toorestart hello Azure portal kullanarak web uygulamanız gerekir:

   ![][AZ10]

1. Bir web tarayıcısı kullanarak tooyour web uygulamanızın URL'sine göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**

   ![Örnek uygulaması Gözat][SB02]

## <a name="next-steps"></a>Sonraki adımlar

Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Linux üzerinde bir yay önyükleme uygulamasının hello Azure kapsayıcı hizmeti dağıtma](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

FTP kullanarak depoying web apps tooAzure hakkında ek bilgi için bkz: [, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak].

Merhaba yay önyükleme örnek proje hakkında daha fazla ayrıntı için bkz: [yay önyükleme Başlarken].

Hello kendi yay önyükleme uygulamaları ile çalışmaya başlama hakkında bilgi için bkz: **yay Initializr** https://start.spring.io/ adresindeki.

Web uygulamanız için ek ayarlarını yapılandırma hakkında daha fazla bilgi için bkz: [Azure App Service'te web uygulamalarını yapılandırma].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Azure App Service'te web uygulamalarını yapılandırma]: /azure/app-service-web/web-sites-configure
[, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Yay önyükleme]: http://projects.spring.io/spring-boot/
[yay önyükleme Başlarken]: https://github.com/spring-guides/gs-spring-boot
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png

---
title: "aaaDeploy Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme Web uygulaması | Microsoft Docs"
description: "Bu öğreticide, ancak Microsoft Azure'da hello adımları toodeploy yay önyükleme uygulama Linux web uygulaması olarak açıklanmaktadır."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Linux'ta hello Azure kapsayıcı hizmeti bir yay önyükleme uygulama dağıtma

Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

**[Docker]**  olan geliştiricilere yardımcı açık kaynak çözümleri otomatikleştirmek hello dağıtım, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimi.

Bu öğretici Docker toodevelop kullanarak kılavuzluk ve hello bir yay önyükleme uygulama tooa Linux ana dağıtma [Azure kapsayıcı Hizmeti'ni (ACS)].

## <a name="prerequisites"></a>Ön koşullar

Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:

* Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].
* Merhaba [Azure komut satırı arabirimi (CLI)].
* Güncel bir [Java Geliştirme Seti (JDK)].
* Apache'nın [Maven] aracını (sürüm 3) yapılandırma.
* A [Git] istemci.
* A [Docker] istemci.

> [!NOTE]
>
> Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Hello yay önyükleme Docker Başlarken web uygulaması oluşturma

Merhaba aşağıdaki adımlar, gerekli toocreate basit bir yay önyükleme web uygulaması ve yerel olarak test hello adımlarda size yol.

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

1. Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizinine oluşturduğunuz; örneğin:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Dizin tamamlandı toohello proje Değiştir; Örneğin:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:
   ```
   mvn package
   ```

1. Merhaba web uygulaması oluşturulduktan sonra dizin toohello değiştirmek `target` burada hello JAR dosyasını bulunur ve hello web uygulaması; başlangıç dizini örneğin:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın. Varsa, örneğin, curl kullanılabilir ve hello Tomcat sunucu toorun bağlantı noktası 80 üzerinde yapılandırılmış:
   ```
   curl http://localhost
   ```

1. Görüntülenen iletiden hello görmeniz gerekir: **Docker Merhaba Dünya!**

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Bir Azure kapsayıcı kayıt defteri toouse özel bir Docker kayıt defteri oluşturma

Merhaba aşağıdaki adımlar hello Azure portal toocreate Azure kapsayıcı kayıt defteri kullanılarak üzerinden yol.

> [!NOTE]
>
> Hello Azure portal yerine toouse hello Azure CLI istiyorsanız hello adımları [hello Azure CLI 2.0 kullanarak özel bir Docker kapsayıcısı kayıt](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Toohello Gözat [Azure portal] ve oturum açın.

   Hello Azure portalı üzerinde tooyour hesabında oturum açtıktan sonra hello hello adımları takip edebilirsiniz [hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt] hello için adımlara hello açıklanır makale artırmak amacıyla expediency biri.

1. Merhaba menü simgesini **+ yeni**, ardından **kapsayıcıları**ve ardından **Azure kapsayıcı kayıt defteri**.
   
   ![Yeni bir Azure kapsayıcı kayıt defteri oluşturma][AR01]

1. Hello Azure kapsayıcı kayıt defteri şablonu için başlangıç bilgileri sayfası görüntülendiğinde tıklayın **oluşturma**. 

   ![Yeni bir Azure kapsayıcı kayıt defteri oluşturma][AR02]

1. Ne zaman hello **oluşturma kapsayıcı kayıt defteri** sayfası görüntülenirse, girin, **kayıt defteri adı** ve **kaynak grubu**, seçin **etkinleştirmek** için Merhaba **yönetici kullanıcı**ve ardından **oluşturma**.

   ![Azure kapsayıcı kayıt defteri ayarlarını yapılandırma][AR03]

1. Kapsayıcı kaydınız oluşturulduktan sonra tooyour kapsayıcı kayıt defterinde hello Azure portalına gidin ve ardından **erişim tuşları**. Merhaba kullanıcı adı ve parola hello sonraki adımlar için not edin.

   ![Azure kapsayıcı kayıt defteri erişim tuşları][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Azure kapsayıcı kayıt defteri erişim tuşlarınızı Maven toouse yapılandırın

1. Maven yüklemenizi toohello yapılandırma dizinine gidin ve açmak hello *settings.xml* dosyasını bir metin düzenleyicisiyle.

1. Azure kapsayıcı kayıt defteri erişim ayarlarınız hello önceki Bu öğretici toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin (örneğin: "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker / tam*") ve açık hello *pom.xml* dosyasını bir metin düzenleyicisiyle.

1. Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla, Azure kapsayıcı kayıt defteri hello önceki bölümdeki Bu öğreticinin; örneğin:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Güncelleştirme hello `<plugins>` hello koleksiyonunda *pom.xml* , hello şekilde dosya `<plugin>` hello oturum açma sunucusu adresi ve kayıt defteri adı için bu öğreticinin önceki bölümdeki hello Azure kapsayıcı kayıt içerir. Örneğin:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toorebuild Merhaba uygulaması aşağıdaki hello çalıştırın ve hello kapsayıcı tooyour Azure kapsayıcı kayıt defteri gönderme:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Docker kapsayıcısı tooAzure Ftp'den, Docker kapsayıcısı başarıyla oluşturuldu olsa bile, hello aşağıdaki benzer tooone bir hata iletisi alabilirsiniz:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Bu durumda, tooyour hello Docker komut satırından Azure hesabı toosign gerekebilir; Örneğin:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Ardından, kapsayıcı hello komut satırından anında; Örneğin:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Linux kapsayıcı görüntünüzü kullanarak Azure App Service'te bir web uygulaması oluşturma

1. Toohello Gözat [Azure portal] ve oturum açın.

1. Merhaba menü simgesini **+ yeni**, ardından **Web + mobil**ve ardından **Linux üzerinde Web uygulaması**.
   
   ![Hello Azure portalında yeni bir web uygulaması oluşturma][LX01]

1. Ne zaman hello **Linux üzerinde Web uygulaması** sayfası görüntülenirse, aşağıdaki bilgilerle hello girin:

   a. Hello için benzersiz bir ad girin **uygulama adı**; örneğin: "*wingtiptoyslinux*."

   b. Seçin, **abonelik** hello aşağı açılan listeden.

   c. Var olan seçin **kaynak grubu**, veya bir ad toocreate yeni bir kaynak grubu belirtin.

   d. Tıklatın **yapılandırma kapsayıcısı** ve aşağıdaki bilgilerle hello girin:

      * Seçin **özel kayıt defteri**.

      * **Görüntü ve isteğe bağlı etiket**: daha önce; Örneğin, kapsayıcı adı belirtin: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **Sunucu URL'si**: kayıt defteri URL'den belirtin önceki; örneğin: "*https://wingtiptoysregistry.azurecr.io*"

      * **Oturum açma kullanıcı** ve **parola**: oturum açma kimlik bilgilerinizi belirtin, **erişim tuşları** önceki adımlarda kullanılan.
   
   e. Tüm bilgileri yukarıda hello girdikten sonra tıklayın **Tamam**.

   ![Web uygulaması ayarlarını yapılandır][LX02]

1. **Oluştur**'a tıklayın.

> [!NOTE]
>
> Azure hello standart bağlantı noktaları 80 veya 8080 üzerinde çalışan Internet istekleri tooembedded Tomcat sunucusunu otomatik olarak eşlenir. Ancak, özel bir bağlantı noktası üzerinde katıştırılmış Tomcat sunucu toorun yapılandırdıysanız, tooadd katıştırılmış Tomcat sunucunuz için başlangıç bağlantı noktası tanımlayan bir ortam değişken tooyour web uygulaması gerekir. toodo, bu nedenle, hello aşağıdaki adımları kullanın:
>
> 1. Toohello Gözat [Azure portal] ve oturum açın.
> 
> 2. Merhaba simgesini **uygulama hizmetleri**. (Aşağıdaki hello görüntü #1 öğesinde bakın.)
>
> 3. Web uygulamanızı hello listeden seçin. (Aşağıdaki hello görüntü #2 öğe.)
>
> 4. Tıklatın **uygulama ayarları**. (Aşağıdaki hello görüntü #3 öğe.)
>
> 5. Merhaba, **uygulama ayarları** bölümünde, adlı yeni bir ortam değişkeni ekleyin **bağlantı noktası** ve hello değeri için özel bağlantı noktası numarası girin. (Aşağıdaki hello görüntü #4 öğe.)
>
> 6. **Kaydet** düğmesine tıklayın. (Aşağıdaki hello görüntü #5 öğe.)
>
> ![Özel bir bağlantı noktası hello Azure portalına kaydediliyor][LX03]
>

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

Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Yay önyükleme uygulama toohello Azure App Service'e dağıtma](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma](container-service-deploy-spring-boot-app-on-kubernetes.md)

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

Docker örnek proje üzerinde hello yay önyükleme hakkında daha fazla ayrıntı için bkz: [Docker Başlarken yay önyüklemede].

Hello kendi yay önyükleme uygulamaları ile çalışmaya başlama hakkında bilgi için bkz: **yay Initializr** https://start.spring.io/ adresindeki.

Basit bir yay önyükleme uygulaması oluşturma ile çalışmaya başlama hakkında daha fazla bilgi için hello yay Initializr https://start.spring.io/ adresindeki bakın.

Toouse özel Docker Azure ile nasıl görüntüler için ek örnekler için bkz: [Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak].

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure kapsayıcı Hizmeti'ni (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt]: /azure/container-registry/container-registry-get-started-portal
[Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png

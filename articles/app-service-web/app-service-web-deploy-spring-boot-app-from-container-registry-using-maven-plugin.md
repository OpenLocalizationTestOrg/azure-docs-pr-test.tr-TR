---
title: "Azure Web Apps toodeploy Azure kapsayıcı kayıt defteri tooAzure uygulama hizmeti yay önyükleme uygulamada aaaHow toouse Merhaba Maven eklentisi"
description: "Bu öğretici, ancak hello adımları toodeploy yay önyükleme uygulaması Azure kapsayıcı kayıt defteri tooAzure tooAzure uygulama hizmeti Maven eklentisi kullanarak yol gösterir."
services: 
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
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy Azure kapsayıcı kayıt defteri tooAzure App Service içinde Spring önyükleme uygulama

Merhaba  **[yay Framework]**  , Java geliştiricilerinin web, mobil ve API uygulamaları oluşturma yardımcı olan bir popüler açık kaynak çerçevedir. Bu öğretici kullanılarak oluşturulmuş bir örnek uygulama kullanır [yay önyükleme], kuralı güdümlü bir yaklaşım yay tooget kullanma çalışmaya hızla.

Bu makalede, nasıl toodeploy bir örnek yay önyükleme uygulama tooAzure kapsayıcı kayıt defteri ve ardından Maven eklentisi için Azure Web Apps toodeploy, uygulama tooAzure uygulama hizmeti hello gösterilmektedir.

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
* A [Docker] istemci.

> [!NOTE]
>
> Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Docker web uygulaması üzerinde kopya hello örnek yay önyükleme

Bu bölümde kapsayıcılı yay önyükleme uygulama kopyalamak ve yerel olarak test.

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

1. Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizinine oluşturduğunuz; örneğin:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Dizin tamamlandı toohello proje Değiştir; Örneğin:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Görüntülenen iletiden hello görmeniz gerekir: **Docker Hello World**

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-service-principal"></a>Bir Azure hizmet sorumlusu oluşturma

Bu bölümde, Azure kapsayıcı tooAzure dağıtırken Maven eklentisi kullanır hello hizmet sorumlusu oluşturun.

1. Bir komut istemi açın.

1. Azure CLI kullanarak Azure hesabınızda oturum hello:
   ```azurecli
   az login
   ```
   Oturum açma Hello yönergeleri toocomplete hello süreci izleyin.

1. Bir Azure hizmet sorumlusu oluşturun:
   ```azurecli
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
   > Kapsayıcı tooAzure hello Maven eklentisi toodeploy yapılandırdığınızda bu JSON yanıt hello değerleri kullanır. Merhaba `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, ve `tttttttt` olan yer tutucu değerlerini olduğunuz isteğe bağlı olarak bu örnek toomake daha kolay toomap kullanılan, Maven yapılandırdığınızda bu değerleri tootheir ilgili öğeleri `settings.xml` hello sonraki dosyayı bölüm.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Azure kapsayıcı hello Azure CLI kullanarak bir kayıt oluşturun

1. Bir komut istemi açın.

1. Azure hesabı tooyour oturum:
   ```azurecli
   az login
   ```

1. Hello için bir kaynak grubu, bu makaledeki kullanacağınız Azure kaynakları oluşturun:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Değiştir `wingtiptoysresources` Bu örnekte, kaynak grubu için benzersiz bir ada sahip.

1. Merhaba kaynak grubunda yay önyükleme uygulamanız için bir özel Azure kapsayıcı kayıt defteri oluşturun: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Değiştir `wingtiptoysregistry` Bu örnekte, kapsayıcı kayıt defteri için benzersiz bir ad ile.

1. Kapsayıcı kaydınız Hello parolasını Al:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure parolanızla yanıt verir; Örneğin:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Azure kapsayıcı kayıt defteri ve Azure hizmet asıl tooyour Maven ayarları ekleme

1. Maven açmak `settings.xml` dosyasını bir metin düzenleyicisinde; bu dosya yolunda hello örnekler aşağıdaki gibi olabilir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Azure kapsayıcı kayıt defteri erişim ayarlarınız hello önceki Bu makale toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Konumlar:
   Öğesi | Açıklama
   ---|---|---
   `<id>` | Özel Azure kapsayıcı kaydınız Hello adını içerir.
   `<username>` | Özel Azure kapsayıcı kaydınız Hello adını içerir.
   `<password>` | Bu makalenin hello önceki bölümde alınan hello parola içerir.

1. Bu makale toohello önceki bir bölümünden Azure hizmet asıl ayarlarınızı ekleme `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Docker kapsayıcısı yansıması oluştur ve tooyour Azure kapsayıcı kayıt defteri gönderme

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizin (örneğin gidin "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") ve açık hello *pom.xml* ile dosya bir Metin Düzenleyici.

1. Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla, Azure kapsayıcı kayıt defteri hello önceki bölümdeki Bu öğreticinin; örneğin:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Konumlar:
   Öğesi | Açıklama
   ---|---|---
   `<azure.containerRegistry>` | Özel Azure kapsayıcı kaydınız Hello adını belirtir.
   `<docker.image.prefix>` | Ekleyerek türetilmiş özel Azure kapsayıcı kaydınız Hello URL'sini belirtir ". azurecr.io" özel kapsayıcı kaydınız toohello adı.

1. Doğrulayın `<plugin>` hello Docker eklentisi için *pom.xml* dosyası Bu öğreticide hello oturum açma sunucusu adresi ve kayıt defteri adı hello önceki adımdaki hello doğru özellikler içerir. Örneğin:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Konumlar:
   Öğesi | Açıklama
   ---|---|---
   `<serverId>` | Özel Azure kapsayıcı kayıt defteri adını içeren hello özelliği belirtir.
   `<registryUrl>` | Özel Azure kapsayıcı kaydınız hello URL'sini içeren hello özelliği belirtir.

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toorebuild Merhaba uygulaması aşağıdaki hello çalıştırın ve hello kapsayıcı tooyour Azure kapsayıcı kayıt defteri gönderme:

   ```
   mvn package docker:build -DpushImage 
   ```

1. İsteğe bağlı: Gözat toohello [Azure portal] ve Docker kapsayıcısı görüntü adlı olduğundan emin olun **yay önyükleme docker gs** kapsayıcı kayıt defterinizde.

   ![Azure portalında kapsayıcı doğrulayın][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Pom.xml özelleştirme sonra derleme ve kapsayıcı tooAzure dağıtma

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Merhaba Maven eklentisi için değiştirebileceğiniz birkaç değer vardır ve bu öğelerin her biri için ayrıntılı bir açıklama hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri. Denirse, bu makaledeki vurgulama değer olan birkaç değerleri vardır:

Öğesi | Açıklama
---|---|---
`<version>` | Merhaba Hello sürümünü belirtir [Azure Web uygulamaları için Maven eklentisi]. Hello listelenen hello sürüm denetlemelisiniz [Maven merkezi depo](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) kullanmakta olduğunuz tooensure hello en son sürümü.
`<authentication>` | Merhaba kimlik doğrulama bilgilerini içeren bu örnekte Azure belirtir bir `<serverId>` içeren öğeyi `azure-auth`; Maven Maven içinde bu değer toolook hello Azure hizmet asıl değerleri kullanan *settings.xml* bu makalenin önceki bölümde tanımlanan dosya.
`<resourceGroup>` | Olan hello hedef kaynak grubu belirtir `wingtiptoysresources` Bu örnekte. zaten yoksa, dağıtım sırasında hello kaynak grubu oluşturulur.
`<appName>` | Web uygulamanız için Hello hedef adını belirtir. Bu örnekte hello hedef adıdır `maven-linux-app-${maven.build.timestamp}`, hello burada `${maven.build.timestamp}` soneki, bu örnek tooavoid çakışması eklenir. (Merhaba zaman damgası isteğe bağlıdır; hello uygulama adı için benzersiz bir dize belirtin.)
`<region>` | Olan bu örnekte hello hedef bölgesi belirtir `westus`. (Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)
`<containerSettings>` | Merhaba adı ve URL, kapsayıcının içeren hello özellikleri belirtir.
`<appSettings>` | Web uygulaması tooAzure dağıtırken Maven toouse benzersiz ayarlarını belirtir. Bu örnekte, bir `<property>` öğesi içeren bir ad/değer çifti alt öğelerinin uygulamanızı hello bağlantı noktasını belirtin.

> [!NOTE]
>
> Hello ayarları toochange hello bağlantı noktası numarasını bu örnekte yalnızca gerekli olan hello varsayılandan hello noktası değiştirilirken.
>

1. Merhaba komut istemi veya daha önce kullandığınız terminal penceresinden, tüm değişiklikleri toohello yaptıysanız Maven kullanarak hello JAR dosyasını yeniden *pom.xml* dosya; örneğin:
   ```shell
   mvn clean package
   ```

1. Web uygulaması tooAzure Maven kullanarak dağıtabilirsiniz; Örneğin:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven web uygulama tooAzure dağıtacağınız; Merhaba web uygulaması zaten mevcut değilse oluşturulur.

> [!NOTE]
>
> Varsa hello belirten hello bölge `<region>` öğesi, *pom.xml* dağıtımınızı başlattığınızda dosya sunucuları yeterli yok, aşağıdaki örnek bir hata benzer toohello görebilirsiniz:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Bu durumda, başka bir bölgeye ve yeniden çalıştırın, uygulamanızın Maven komutunu toodeploy hello belirtebilirsiniz.
>
>

Web dağıtıldığında mümkün toomanage olacaktır hello kullanarak [Azure portal].

* Web uygulamanızı listelenen **uygulama hizmetleri**:

   ![Azure portalında uygulama hizmetleri listelenen web uygulaması][AP01]

* Ve web uygulamanızı hello listelenir URL hello **genel bakış** web uygulamanız için:

   ![Web uygulamanız için Hello URL belirleme][AP02]

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede ele alınan çeşitli teknolojiler hello hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Azure Web uygulamaları için Maven eklentisi]

* [TooAzure hello Azure CLI gelen oturum](/azure/xplat-cli-connect)

* [Bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven ayarları başvurusu](https://maven.apache.org/settings.html)

* [Maven için docker eklentisi]

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Azure Web uygulamaları için Maven eklentisi]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Maven için docker eklentisi]: https://github.com/spotify/docker-maven-plugin
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png

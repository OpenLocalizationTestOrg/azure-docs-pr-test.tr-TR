---
title: "aaaDeploy Kubernetes Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını | Microsoft Docs"
description: "Bu öğretici Microsoft Azure üzerinde bir Kubernetes kümede ancak hello adımları toodeploy yay önyükleme uygulama anlatılmaktadır."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma

Merhaba  **[yay Framework]**  , Java geliştiricilerinin web, mobil ve API uygulamaları oluşturma yardımcı olan bir popüler açık kaynak çerçevedir. Bu öğretici kullanılarak oluşturulmuş bir örnek uygulama kullanır [yay önyükleme], kuralı güdümlü bir yaklaşım yay tooget kullanma çalışmaya hızla.

**[Kubernetes]**  ve  **[Docker]**  olan, geliştiricilerin açık kaynak çözümleri otomatikleştirmek hello dağıtım, ölçeklendirme ve çalışan kendi uygulamalarını Yönetimi kapsayıcı.

Bu öğretici, bu iki yaygın olarak kullanılan, açık kaynak teknolojisi toodevelop birleştirme olsa açıklanmaktadır ve yay önyükleme uygulama tooMicrosoft Azure dağıtın. Daha belirgin olarak kullandığınız  *[yay önyükleme]*  uygulama geliştirme için  *[Kubernetes]*  kapsayıcı dağıtım ve hello [Azure kapsayıcı Hizmeti'ni (ACS)] toohost uygulamanızı.

### <a name="prerequisites"></a>Ön koşullar

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

Aşağıdaki adımları hello yay önyükleme web uygulaması oluşturma ve yerel olarak test size yol.

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

1. Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizine.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Dizin tamamlandı toohello proje değiştirin.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Maven toobuild ve çalışma hello örnek uygulaması kullanın.
   ```
   mvn package spring-boot:run
   ```

1. Test hello web uygulaması toohttp://localhost:8080 gözatarak veya hello aşağıdaki `curl` komutu:
   ```
   curl http://localhost:8080
   ```

1. Görüntülenen iletiden hello görmeniz gerekir: **Docker Hello World**

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Azure kapsayıcı hello Azure CLI kullanarak bir kayıt oluşturun

1. Bir komut istemi açın.

1. Azure hesabı tooyour oturum:
   ```azurecli
   az login
   ```

1. Bu öğreticide kullanılan Azure kaynaklarını hello için bir kaynak grubu oluşturun.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Bir özel Azure kapsayıcı kayıt defteri hello kaynak grubunda oluşturun. Başlangıç Öğreticisi hello örnek uygulaması Docker görüntü toothis kayıt defteri daha sonraki adımlarda olarak iter. Değiştir `wingtiptoysregistry` kayıt için benzersiz bir ad ile.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Uygulama toohello kapsayıcı kaydınız bildirme

1. Maven yüklemenizi toohello yapılandırma dizinine gidin (varsayılan ~/.m2/ veya C:\Users\username\.m2) ve açık hello *settings.xml* dosyasını bir metin düzenleyicisiyle.

1. Kapsayıcı kaydınız Hello parolasını hello Azure CLI ' alın.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Azure kapsayıcı kayıt kimliği ve parolası tooa yeni Ekle `<server>` hello koleksiyonunda *settings.xml* dosya.
Merhaba `id` ve `username` hello kayıt defteri hello adı. Kullanım hello `password` değerinden (tırnaklar olmadan) hello önceki komutu.

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin (örneğin, "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker / tam*") ve açık hello *pom.xml* dosyasını bir metin düzenleyicisiyle.

1. Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla Azure kapsayıcı kayıt için.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Güncelleştirme hello `<plugins>` hello koleksiyonunda *pom.xml* , hello şekilde dosya `<plugin>` hello oturum açma sunucusu adresi ve kayıt defteri adı için Azure kapsayıcı kayıt içerir.

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

1. Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toobuild hello Docker kapsayıcısı ve anında iletme hello görüntü toohello kayıt defteri aşağıdaki hello çalıştırın:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Maven hello görüntü tooAzure iter kurarken, benzer tooone hello aşağıdaki hata iletisini alabilirsiniz:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Bu hata alırsanız, hello Docker komut satırından tooAzure oturum açın.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Ardından, kapsayıcı gönderin:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Kubernetes küme üzerinde ACS hello Azure CLI kullanarak oluşturma

1. Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesi oluşturun. Merhaba aşağıdaki komut oluşturur bir *kubernetes* hello kümede *wingtiptoys kubernetes* kaynak grubu ile *wingtiptoys containerservice* hello kümesi olarak ad ve *wingtiptoys kubernetes* hello DNS öneki olarak:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Bu komut zaman alabilir toocomplete.

1. Yükleme `kubectl` hello Azure CLI kullanarak. Linux kullanıcıları bu komutla tooprefix olabilir `sudo` hello Kubernetes CLI çok dağıtır beri`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Merhaba Kubernetes web arabiriminden kümenizi yönetebilirsiniz hello küme yapılandırma bilgilerini karşıdan yüklemek ve `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Merhaba görüntü tooyour Kubernetes kümesi dağıtma

Merhaba uygulamasını kullanarak bu öğreticinin dağıtır `kubectl`, ardından hello Kubernetes web arabirimi üzerinden tooexplore hello dağıtımına izin.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Merhaba Kubernetes web arabirimiyle dağıtma

1. Bir komut istemi açın.

1. Merhaba yapılandırma Web sitesi Kubernetes kümeniz için varsayılan tarayıcınızda açın:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Merhaba Kubernetes yapılandırma Web tarayıcınızda oturum açtığında, hello çok bağlantısı**kapsayıcılı uygulamasını dağıtmak**:

   ![Kubernetes yapılandırma Web sitesi][KB01]

1. Ne zaman hello **kapsayıcılı uygulamasını dağıtmak** sayfası görüntülenirse, aşağıdaki seçenekleri şu hello belirtin:

   a. Seçin **aşağıda uygulama ayrıntılarını belirtin**.

   b. Hello için yay önyükleme uygulama adınızı girin **uygulama adı**; örneğin: "*gs yay önyükleme docker*".

   c. Merhaba, oturum açma sunucusu ve kapsayıcı görüntüden daha önce girin **kapsayıcı görüntü**; örneğin: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Seçin **dış** hello için **hizmet**.

   e. İç ve dış bağlantı noktaları hello belirtin **bağlantı noktası** ve **hedef bağlantı noktası** metin kutuları.

   ![Kubernetes yapılandırma Web sitesi][KB02]


1. Tıklatın **dağıtma** toodeploy hello kapsayıcı.

   ![Kapsayıcı dağıtma][KB05]

1. Uygulamanız dağıtıldıktan sonra altında listelenen yay önyükleme uygulamanızı görürsünüz **Hizmetleri**.

   ![Kubernetes Hizmetleri][KB06]

1. Merhaba bağlantısına tıklarsanız **dış uç noktalar**, Azure üzerinde çalışan yay önyükleme uygulamanızı görebilirsiniz.

   ![Kubernetes Hizmetleri][KB07]

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


### <a name="deploy-with-kubectl"></a>Kubectl ile dağıtma

1. Bir komut istemi açın.

1. Hello kullanarak, kapsayıcı hello Kubernetes kümede çalışmasını `kubectl run` komutu. Bir hizmet adı uygulamanızı Kubernetes ve hello tam görüntü adı verin. Örneğin:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   Bu komutta:

   * Merhaba kapsayıcı adı `gs-spring-boot-docker` hemen sonra hello belirtilen `run` komutu

   * Merhaba `--image` parametresi belirtir hello birleştirilmiş oturum açma sunucusu ve görüntü adı olarak`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Harici olarak hello kullanarak Kubernetes kümenizi kullanıma `kubectl expose` komutu. Genel kullanıma yönelik TCP bağlantı noktası kullanılan tooaccess hello uygulama ve uygulamanızı dinlediği hello iç hedef bağlantı noktası Merhaba, hizmet adı belirtin. Örneğin:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   Bu komutta:

   * Merhaba kapsayıcı adı `gs-spring-boot-docker` hemen sonra hello belirtilen `expose deployment` komutu

   * Merhaba `--type` parametresi, o hello kümesi kullanan yük dengeleyici belirtir

   * Merhaba `--port` parametresi hello genel kullanıma yönelik TCP bağlantı noktası 80 belirtir. Merhaba uygulamanın bu bağlantı noktasına erişim.

   * Merhaba `--target-port` parametresi hello iç TCP bağlantı noktası 8080 belirtir. Merhaba yük dengeleyici, bu bağlantı noktasında istekleri tooyour uygulama iletir.

1. Merhaba uygulama dağıtıldıktan sonra toohello küme hello dış IP adresi sorgulamak ve web tarayıcınızda açın:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


## <a name="next-steps"></a>Sonraki adımlar

Azure üzerinde yay önyükleme kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Yay önyükleme uygulama toohello Azure App Service'e dağıtma](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Linux'ta hello Azure kapsayıcı hizmeti bir yay önyükleme uygulama dağıtma](container-service-deploy-spring-boot-app-on-linux.md)

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

Docker örnek proje hello yay önyükleme hakkında daha fazla bilgi için bkz: [Docker Başlarken yay önyüklemede].

Aşağıdaki bağlantılar hello yay önyükleme uygulamaları oluşturma hakkında ek bilgi sağlar:

* Basit bir yay önyükleme uygulama oluşturma hakkında daha fazla bilgi için hello yay Initializr https://start.spring.io/ adresindeki bakın.

Merhaba aşağıdaki bağlantılar Kubernetes Azure ile kullanma hakkında ek bilgi sağlar:

* [Kapsayıcı hizmeti Kubernetes kümede kullanmaya başlama](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Kubernetes web kullanıcı Arabirimi Azure kapsayıcı hizmeti ile Merhaba kullanma](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Kubernetes komut satırı arabirimini kullanma hakkında daha fazla bilgi hello kullanılabilir **kubectl** adresindeki Kullanıcı Kılavuzu'na <https://kubernetes.io/docs/user-guide/kubectl/>.

Merhaba Kubernetes Web sitesi özel kayıt defterleri görüntüleri görüşmeniz çeşitli makaleler vardır:

* [Hizmet yapılandırma pod'ları için hesapları]
* [Ad alanları]
* [Özel bir kayıt defterinden görüntüyü çekme]

Toouse özel Docker Azure ile nasıl görüntüler için ek örnekler için bkz: [Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak].

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure kapsayıcı Hizmeti'ni (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/
[Hizmet yapılandırma pod'ları için hesapları]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Ad alanları]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Özel bir kayıt defterinden görüntüyü çekme]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png

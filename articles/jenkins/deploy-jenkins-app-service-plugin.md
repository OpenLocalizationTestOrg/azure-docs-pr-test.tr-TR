---
title: aaaDeploy tooAzure Jenkins eklentisi ile App Service | Microsoft Docs
description: "Nasıl toouse Azure App Service Jenkins eklentisi toodeploy bir Java web uygulaması tooAzure Jenkins içinde bilgi edinin"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Uygulama hizmeti tooAzure Jenkins eklentisi ile dağıtma 
toodeploy bir Java web uygulaması tooAzure, Azure CLI kullanabilir [Jenkins ardışık düzen](/azure/jenkins/execute-cli-jenkins-pipeline) veya yapabilirsiniz hello kullan [Azure App Service Jenkins eklentisi](https://plugins.jenkins.io/azure-app-service). Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Jenkins toodeploy tooAzure FTP aracılığıyla uygulama hizmetini yapılandırma 
> * Docker aracılığıyla Linux'ta Jenkins toodeploy tooAzure uygulama hizmetini yapılandırma 

## <a name="create-and-configure-jenkins-instance"></a>Oluşturma ve yapılandırma Jenkins örneği
Jenkins asıl zaten yoksa, hello ile başlangıç [çözüm şablonu](install-jenkins-solution-template.md), JDK8 ve gerekli eklentileri aşağıdaki hello içerir:

* [Jenkins Git istemcisi eklentisi](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons eklentisi](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure kimlik](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure uygulama hizmeti](https://plugins.jenkins.io/azure-app-server) v.0.1

Merhaba uygulama hizmeti eklentisi toodeploy Web uygulamasını Azure App Service tarafından desteklenen tüm dillerde (örneğin, C#, PHP, Java ve node.js vb.) kullanabilirsiniz. Bu öğreticide, hello örnek Java uygulaması kullanıyoruz [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample). toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.  

Java JDK ve Maven hello Java projesi oluşturmak için gereklidir. Sürekli tümleştirme için kullanırsanız, hello bileşenleri hello Jenkins asıl veya hello VM Aracısı yüklediğinizden emin olun. 

tooinstall, SSH kullanarak toohello Jenkins örneğinde oturum ve hello aşağıdaki komutları çalıştırın:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

TooApp Linux hizmet dağıtmak için tooinstall Docker hello Jenkins ana veya yapı için kullanılan hello VM Aracısı da gerekir. Toothis makale tooinstall Docker bakın: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure hizmet asıl tooJenkins kimlik bilgisi Ekle

Bir Azure hizmet sorumlusu gerekli toodeploy tooAzure ' dir. 

<ol>
<li>Kullanım [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) veya [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate bir Azure hizmet sorumlusu</li>
<li>Merhaba Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**. Tıklatın **genel credentials(unrestricted)**.</li>
<li>Tıklatın **kimlik bilgilerini eklemek** tooadd hello abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak bir Microsoft Azure hizmet sorumlusu. Bir kimliği sağlayın **bileşene mySp**, sonraki adımlarda kullanılacak.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure uygulama hizmeti eklentisi

Azure uygulama hizmeti eklentisi v1.0 destekleyen sürekli dağıtım tooAzure Web uygulaması aracılığıyla:

* Git ve FTP
* Linux üzerinde Web uygulaması için docker

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Jenkins toodeploy hello Jenkins Panoyu kullanarak FTP üzerinden Web uygulaması yapılandırma

toodeploy, proje tooAzure Web uygulaması derleme yapıtları (örneğin, Java .war dosyası) karşıya yükleyebilir Git veya FTP kullanma.

Jenkins hello işinde ayarlamadan önce çalışan hello Java uygulaması için bir Azure uygulama hizmeti planı ve bir Web uygulaması gerekir.


1. Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu. Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar. Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır.
2. Bir Web Uygulaması oluşturun. Ya da kullanım hello yapabilecekleriniz [Azure portal](/azure/app-service-web/web-sites-configure) veya kullanım hello aşağıdaki Az CLI komutu:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Uygulamanız gereken hello Java Çalışma zamanı yapılandırmasını ayarladığınızdan emin olun. Azure CLI komutu aşağıdaki hello üzerinde yeni bir Java 8 JDK hello web uygulama toorun yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Merhaba Jenkins iş ayarlayın


1. Yeni bir **freestyle** Jenkins Pano projesinde
2. Yapılandırma **kaynak kodu Yönetimi** toouse, yerel, çatalı [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) hello sağlayarak **depo URL'si**. Örneğin: http://github.com/&lt;yourID > / javawebappsample.
3. Maven kullanarak bir derleme adımı toobuild hello projeye ekleyin. Ekleyerek bunu bir **Kabuk yürütme**. Bu örnekte, bir ek adım toorename hello *.war dosyasında hedef klasörü tooROOT.war gerekir.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.
5. Tedarik, "bileşene mySp", önceki adımda depolanan hello Azure hizmet sorumlusu.
6. İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde hello kaynak grubu ve web uygulaması seçin. Merhaba eklentisi otomatik olarak algılar hello Web uygulaması Windows olup olmadığını veya Linux tabanlı. Bir Windows tabanlı Web uygulaması için "Yayımlama dosyalar" Merhaba seçeneği sunulur.
7. Dolgu hello dosyalarında istediğiniz toodeploy (Java kullanıyorsanız, örneğin, bir war package.) Kaynak dizin ve hedef dizin isteğe bağlıdır. Merhaba parametreler toospecify kaynak ve hedef klasörler, dosyaları karşıya yüklenirken sağlar. Azure'da Java web uygulaması Tomcat Server'da çalıştırılır. Karşıya yüklediğiniz şekilde, paket webapps klasörüne war. Bu örnek için set **kaynak dizin** çok "hedef" ve "webapps" sağlamak için **hedef dizin**.
8. Üretim dışında toodeploy tooa yuvası isterseniz, ayrıca ayarlayabilirsiniz **yuvası** adı.
9. Merhaba projeyi kaydedin ve onu oluşturun. Yapı tamamlandığında, web uygulamanızın dağıtılan tooAzure olur.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Jenkins ardışık düzen kullanarak FTP üzerinden Web uygulaması dağıtma

Merhaba eklentisi ardışık düzeni için hazır olur. Merhaba GitHub deposuna tooa örnek başvurabilir.

1. GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_ftp_plugin** dosya. Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 11 ve 12 satırındaki'ı tıklatın.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Jenkins Örneğinizde satır 14 tooupdate kimlik bilgisi Kimliğini değiştirin.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Jenkins işlem hattı oluşturma

1. Jenkins bir web tarayıcısında açın, **yeni öğe**.
2. Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**. **Tamam** düğmesine tıklayın.
3. Merhaba tıklatın **ardışık düzen** sekmesinde sonraki.
4. İçin **tanımı**seçin **kanal SCM betikten**.
5. İçin **SCM**seçin **Git**. Merhaba GitHub URL forked depodaki girin: https:&lt;forked depodaki > .git
6. Güncelleştirme **betik yolu** çok "Jenkinsfile_ftp_plugin"
7. Tıklatın **kaydetmek** ve çalışma hello işi.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Docker aracılığıyla Linux'ta Jenkins toodeploy Web uygulamasını yapılandırma

Git/FTP dışında Linux üzerinde Web uygulaması Docker kullanarak dağıtımı destekler. Docker, kullanarak toodeploy tooprovide docker görüntüsüne web uygulamanızı hizmet çalışma zamanı paketleri bir Dockerfile gerekir. Ardından hello eklentisi hello görüntü oluşturur, tooa docker kayıt defteri iter ve hello görüntü tooyour web uygulamasına dağıtır.

Web uygulaması Linux'ta geleneksel yolları Git ve FTP gibi ancak yalnızca yerleşik dilleri (.NET Core, Node.js, PHP ve Ruby) da destekler. Diğer diller için toopackage, uygulama kodu ve hizmet çalışma zamanı birlikte docker görüntüsüne gerekir ve docker toodeploy kullanın.

Jenkins hello işinde ayarlamadan önce bir Azure uygulama hizmeti Linux'ta gerekir. Bir kapsayıcı kayıt defteri zamanda gerekli toostore ve özel Docker kapsayıcısı görüntülerinizi yönetin. DockerHub kullanabilirsiniz; Bu örnek için Azure kapsayıcı kayıt defteri kullanıyoruz.

* Merhaba adımları izleyebilirsiniz [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux üzerinde bir Web uygulaması 
* Azure kapsayıcı kayıt defteri olan bir yönetilen [Docker kayıt defteri] göre (https://docs.docker.com/registry/) hizmeti hello açık kaynak Docker kayıt defteri 2.0. [Burada] Hello adımları izleyin (/ azure/container-registry/container-registry-get-started-azure-cli) konusunda daha fazla yardım için toodo şekilde. DockerHub de kullanabilirsiniz.

### <a name="toodeploy-using-docker"></a>docker kullanarak toodeploy:

1. Yeni bir Serbest stilde projesi Jenkins panosunda oluşturun.
2. Yapılandırma **kaynak kodu Yönetimi** toouse, yerel, çatalı [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) hello sağlayarak **depo URL'si**. Örneğin: http://github.com/&lt;yourid > / javawebappsample.
Maven kullanarak bir derleme adımı toobuild hello projeye ekleyin. Ekleyerek bunu bir **Kabuk yürütme** ve satırında aşağıdaki hello ekleyin **komutu**:    
```bash
mvn clean package
```

3. Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.
4. Tedarik, **bileşene mySp**, önceki adımda Azure kimlik bilgileri olarak depolanan hello Azure hizmet sorumlusu.
5. İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde hello kaynak grubu ve Linux web uygulaması seçin.
6. Seçin Docker yayımlayın.
7. Doldurmak **Dockerfile** yolu. Merhaba varsayılan koruyabilirsiniz "/ Dockerfile" için **Docker kayıt defteri URL**, https:// hello biçiminde sağlar&lt;myRegistry >. Azure kapsayıcı kayıt defteri kullanırsanız azurecr.io. DockerHub kullanıyorsanız, boş bırakın.
8. İçin **kayıt defteri kimlik bilgilerini**, hello Azure kapsayıcı kayıt defteri için hello kimlik bilgisi ekleyin. Azure CLI komutları aşağıdaki hello çalıştırarak hello kullanıcı kimliği ve parola alabilirsiniz. Merhaba ilk komut hello yönetici hesabını etkinleştirir.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Merhaba docker görüntü adı ve etiketinde **Gelişmiş** sekmesi isteğe bağlı. Varsayılan olarak, görüntü adı elde edilir hello görüntüden Azure portal (inç Docker kapsayıcısı ayarı) hello etiketinde yapılandırılmış ad $BUILD_NUMBER oluşturulur. Emin olun ya da Azure portalında hello görüntü adı belirtin veya için bir değer sağlamanız **Docker görüntü** içinde **Gelişmiş** sekmesi. Bu örnekte, tedarik "&lt;yourRegistry >.azurecr.io/calculator" için **Docker görüntü** bırakıp **Docker resim etiketi** boş.
10. Yerleşik Docker görüntü ayarını kullanırsanız Not dağıtımı başarısız olur. Docker config toouse özel görüntüyü Azure portalında Docker kapsayıcısı ayarında değiştirdiğinizden emin olun. Yerleşik görüntü için dosya karşıya yükleme yaklaşımını toodeploy kullanın.
11. Benzer toofile karşıya yükleme yaklaşım, üretim dışındaki başka bir yuvaya seçebilirsiniz.
12. Kaydedin ve Merhaba projeyi oluşturun. Kapsayıcı görüntünüzü tooyour kayıt defteri gönderilir ve web uygulama bakın.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>TooWeb Docker kullanılarak Jenkins ardışık düzeni aracılığıyla Linux'ta uygulama dağıtma

1. GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_container_plugin** dosya. Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 11 ve 12 satırındaki'ı tıklatın.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Satır 13 tooyour kapsayıcı kayıt sunucusunu değiştirme    
```java
def registryServer = '<registryURL>'
```    

3. Satır 16 tooupdate kimlik bilgisi kimliği Jenkins Örneğinizde değiştirme    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Jenkins işlem hattı oluşturma    

1. Jenkins bir web tarayıcısında açın, **yeni öğe**.
2. Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**. **Tamam** düğmesine tıklayın.
3. Merhaba tıklatın **ardışık düzen** sekmesinde sonraki.
4. İçin **tanımı**seçin **kanal SCM betikten**.
5. İçin **SCM**seçin **Git**.
6. Merhaba GitHub URL forked depodaki girin: https:&lt;forked depodaki > .git</li>
7, güncelleştirme **betik yolu** çok "Jenkinsfile_container_plugin"
8. Tıklatın **kaydetmek** ve çalışma hello işi.

## <a name="verify-your-web-app"></a>Web uygulamanızı doğrulayın

1. tooverify hello WAR dosyası başarıyla dağıtılan tooyour web uygulaması. Bir web tarayıcısı açın.
2. Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping görürsünüz:    
     TooJava Web uygulaması'na Hoş Geldiniz!!! Bu güncelleştirilmiş!
   Sun Haz 17 16:39:10 UTC 2017
3. Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y        
    ![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Linux için uygulama hizmeti

* tooverify, Azure CLI'da çalıştırın:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Sonuç aşağıdaki hello alın:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping. Selamlama iletisine bakın: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y
    
## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello Azure uygulama hizmeti eklentisi toodeploy tooAzure kullanın.

Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Jenkins toodeploy FTP aracılığıyla Azure uygulama hizmeti yapılandırın 
> * Docker aracılığıyla Linux'ta Jenkins toodeploy tooAzure uygulama hizmetini yapılandırma 

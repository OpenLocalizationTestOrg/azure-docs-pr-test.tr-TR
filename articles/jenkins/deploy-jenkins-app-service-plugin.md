---
title: "Jenkins eklentisi ile Azure App Service'e dağıtma | Microsoft Docs"
description: "Java web uygulaması Jenkins Azure'da dağıtmak için Azure App Service Jenkins eklentisi kullanmayı öğrenin"
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a>Jenkins eklentisi ile Azure App Service'e dağıtma 
Java web uygulaması Azure'a dağıtmak için Azure CLI kullanabileceğiniz [Jenkins ardışık düzen](/azure/jenkins/execute-cli-jenkins-pipeline) veya yapabileceğiniz kullanımı [Azure App Service Jenkins eklentisi](https://plugins.jenkins.io/azure-app-service). Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * FTP aracılığıyla Azure uygulama hizmeti dağıtmak için Jenkins yapılandırın 
> * Azure uygulama hizmeti Docker aracılığıyla Linux'ta dağıtmak için Jenkins yapılandırın 

## <a name="create-and-configure-jenkins-instance"></a>Oluşturma ve yapılandırma Jenkins örneği
Jenkins asıl zaten yoksa başlayın [çözüm şablonu](install-jenkins-solution-template.md), JDK8 ve aşağıdaki gerekli eklentileri içerir:

* [Jenkins Git istemcisi eklentisi](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons eklentisi](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure kimlik](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure uygulama hizmeti](https://plugins.jenkins.io/azure-app-server) v.0.1

Uygulama hizmeti eklentisi, Web uygulamasını Azure App Service tarafından desteklenen tüm dillerde (örneğin, C#, PHP, Java ve node.js vb.) dağıtmak için kullanabilirsiniz. Bu öğreticide, örnek Java uygulaması kullanıyoruz [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample). Kendi GitHub hesabınızda depoyu çatallaştırma için tıklatın **çatalı** sağ üst köşesindeki düğmesi.  

Java JDK ve Maven Java projesi oluşturmak için gereklidir. Sürekli tümleştirme için kullanırsanız, bileşenlerin Jenkins asıl veya VM Aracısı yüklediğinizden emin olun. 

Yüklemek için SSH kullanarak Jenkins örneğine oturum açın ve aşağıdaki komutları çalıştırın:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Uygulama hizmeti Linux'ta dağıtmak için aynı zamanda Docker Jenkins asıl veya yapı için kullanılan VM aracısı yüklemeniz gerekir. Docker yüklemek için bu makaleye bakın: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-to-jenkins-credential"></a>Azure hizmet sorumlusu için Jenkins kimlik bilgileri ekleme

Bir Azure hizmet sorumlusu Azure'a dağıtmak için gereklidir. 

<ol>
<li>Kullanım [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) veya [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) bir Azure hizmet sorumlusu oluşturmak için</li>
<li>Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**. Tıklatın **genel credentials(unrestricted)**.</li>
<li>Tıklatın **kimlik bilgilerini eklemek** abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak bir Microsoft Azure hizmet sorumlusu eklemek için. Bir kimliği sağlayın **bileşene mySp**, sonraki adımlarda kullanılacak.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure uygulama hizmeti eklentisi

Azure uygulama hizmeti eklentisi v1.0 Azure Web uygulaması için sürekli dağıtım destekler:

* Git ve FTP
* Linux üzerinde Web uygulaması için docker

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a>Jenkins Panoyu kullanarak FTP üzerinden Web uygulaması dağıtma Jenkins yapılandırın

Projenizi Azure Web uygulamasına dağıtmak için derleme yapıtları (örneğin, Java .war dosyası) karşıya yükleyebilir Git veya FTP kullanma.

Jenkins işinde ayarlamadan önce Azure App Service planı ve bir Web uygulaması Java uygulaması çalıştırmak için gerekir.


1. İle bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu. Uygulama hizmeti planı, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları tanımlar. Bir uygulama hizmeti planı atanan tüm uygulamalar maliyet birden fazla uygulama barındırdığında kaydetmenize izin vererek, bu kaynakları paylaşır.
2. Bir Web Uygulaması oluşturun. Kullanabilir [Azure portal](/azure/app-service-web/web-sites-configure) veya aşağıdaki Az CLI komutu kullanın:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Uygulamanızın gerektiğini Java Çalışma zamanı yapılandırma ayarladığınızdan emin olun. Yeni bir Java 8 JDK üzerinde çalıştırmak için web uygulama aşağıdaki Azure CLI komutu yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a>Jenkins iş ayarlayın


1. Yeni bir **freestyle** Jenkins Pano projesinde
2. Yapılandırma **kaynak kodu Yönetimi** , yerel çatalı, kullanılacak [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) sağlayarak **depo URL'si**. Örneğin: http://github.com/&lt;yourID > / javawebappsample.
3. Maven kullanarak Projeyi derlemek için derleme adımı ekleyin. Ekleyerek bunu bir **Kabuk yürütme**. Bu örnekte, hedef klasör *.war dosyasında ROOT.war için yeniden adlandırmak için ek bir adım gerekir.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.
5. , Önceki adımda depolanan Azure hizmet sorumlusu "bileşene" mySp sağlayın.
6. İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde kaynak grubu ve web uygulaması seçin. Web uygulaması Windows olup olmadığını eklentisi otomatik olarak algılar ve Linux tabanlı. Windows tabanlı Web uygulaması'için bir seçenek "yayımlama dosyaları" sunulur.
7. (Örneğin, Java kullanılıyorsa bir war paketi.) dağıtmak istediğiniz dosyaları doldurun Kaynak dizin ve hedef dizin isteğe bağlıdır. Parametreler kaynak ve hedef klasörler dosyaları karşıya yüklenirken belirtmenize olanak sağlar. Azure'da Java web uygulaması Tomcat Server'da çalıştırılır. Karşıya yüklediğiniz şekilde, paket webapps klasörüne war. Bu örnek için set **kaynak dizin** "hedef" ve "webapps" sağlamanız için **hedef dizin**.
8. Bir yuva üretim dışında dağıtmak istiyorsanız, ayrıca ayarlayabilirsiniz **yuvası** adı.
9. Projeyi kaydedin ve onu oluşturun. Yapı tamamlandığında, web uygulamanızı Azure'a dağıtılır.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Jenkins ardışık düzen kullanarak FTP üzerinden Web uygulaması dağıtma

Eklenti ardışık düzeni için hazır olur. GitHub depo örnekte başvurabilirsiniz.

1. GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_ftp_plugin** dosya. Web uygulamanızı 11 ve 12 satırındaki adını ve kaynak grubu sırasıyla güncelleştirmek için bu dosyayı düzenlemek için Kalem simgesine tıklayın.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Satır kimlik bilgisi kimliği Jenkins Örneğinizde güncelleştirmek için 14 değiştirin.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Jenkins işlem hattı oluşturma

1. Jenkins bir web tarayıcısında açın, **yeni öğe**.
2. Seçin ve iş için bir ad **ardışık düzen**. **Tamam** düğmesine tıklayın.
3. Tıklatın **ardışık düzen** sekmesinde sonraki.
4. İçin **tanımı**seçin **kanal SCM betikten**.
5. İçin **SCM**seçin **Git**. Forked, depodaki için GitHub URL'yi girin: https:&lt;forked depodaki > .git
6. Güncelleştirme **komut dosyası yolu** "Jenkinsfile_ftp_plugin" için
7. Tıklatın **kaydetmek** ve işini çalıştırın.

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a>Web uygulaması Docker aracılığıyla Linux'ta dağıtma Jenkins yapılandırın

Git/FTP dışında Linux üzerinde Web uygulaması Docker kullanarak dağıtımı destekler. Docker kullanarak dağıtmak için web uygulamanızı hizmet çalışma zamanı docker görüntüsüne paketleri bir Dockerfile sağlamanız gerekir. Ardından eklentisi görüntü oluşturur, docker kayıt defterine iter ve web uygulamanıza görüntüyü dağıtır.

Web uygulaması Linux'ta geleneksel yolları Git ve FTP gibi ancak yalnızca yerleşik dilleri (.NET Core, Node.js, PHP ve Ruby) da destekler. Diğer diller için uygulama kodu ve hizmet çalışma zamanı birlikte docker görüntüsüne paketini ve dağıtmak için docker kullanmanız gerekir.

Jenkins işinde ayarlamadan önce bir Azure uygulama hizmeti Linux'ta gerekir. Bir kapsayıcı kayıt defteri, depolamak ve özel Docker kapsayıcısı görüntülerinizi yönetmek için de gereklidir. DockerHub kullanabilirsiniz; Bu örnek için Azure kapsayıcı kayıt defteri kullanıyoruz.

* Adımları izleyebilirsiniz [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) Linux üzerinde bir Web uygulaması oluşturmak için 
* Azure kapsayıcı kayıt defteri olan bir yönetilen [Docker kayıt defteri] (https://docs.docker.com/registry/) hizmet tabanlı açık kaynak Docker kayıt defteri 2.0. [Burada] adımları (/ azure/container-registry/container-registry-get-started-azure-cli) bunun nasıl yapılacağı hakkında daha fazla yönergeler için. DockerHub de kullanabilirsiniz.

### <a name="to-deploy-using-docker"></a>Docker kullanarak dağıtmak için:

1. Yeni bir Serbest stilde projesi Jenkins panosunda oluşturun.
2. Yapılandırma **kaynak kodu Yönetimi** , yerel çatalı, kullanılacak [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) sağlayarak **depo URL'si**. Örneğin: http://github.com/&lt;yourid > / javawebappsample.
Maven kullanarak Projeyi derlemek için derleme adımı ekleyin. Ekleyerek bunu bir **Kabuk yürütme** ve aşağıdaki satırı ekleyin **komutu**:    
```bash
mvn clean package
```

3. Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.
4. Tedarik, **bileşene mySp**, önceki adımda Azure kimlik bilgileri olarak depolanan Azure hizmet sorumlusu.
5. İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde kaynak grubu ve Linux web uygulaması seçin.
6. Seçin Docker yayımlayın.
7. Doldurmak **Dockerfile** yolu. Varsayılan koruyabilirsiniz "/ Dockerfile" için **Docker kayıt defteri URL**, https:// biçiminde sağlar&lt;myRegistry >. Azure kapsayıcı kayıt defteri kullanırsanız azurecr.io. DockerHub kullanıyorsanız, boş bırakın.
8. İçin **kayıt defteri kimlik bilgilerini**, Azure kapsayıcı kayıt için kimlik bilgisi ekleyin. Azure CLI aşağıdaki komutları çalıştırarak kullanıcı kimliği ve parola alabilirsiniz. İlk komut yönetici hesabını etkinleştirir.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Docker görüntü adı ve etiketinde **Gelişmiş** sekmesi isteğe bağlı. Varsayılan olarak, Azure portalında (Docker kapsayıcısı ayarı.) için yapılandırdığınız görüntü adından görüntü adı elde edilir Etiket $BUILD_NUMBER oluşturulur. Emin olun ya da Azure Portalı'nda Görüntü adı belirtin veya için bir değer sağlamanız **Docker görüntü** içinde **Gelişmiş** sekmesi. Bu örnekte, tedarik "&lt;yourRegistry >.azurecr.io/calculator" için **Docker görüntü** bırakıp **Docker resim etiketi** boş.
10. Yerleşik Docker görüntü ayarını kullanırsanız Not dağıtımı başarısız olur. Azure portalında Docker kapsayıcısı ayarında özel görüntü kullanmak için docker config değiştirdiğinizden emin olun. Yerleşik görüntü için dosya karşıya yükleme yaklaşımı dağıtmak için kullanın.
11. Benzer şekilde dosya karşıya yükleme yaklaşım, üretim dışındaki başka bir yuvaya seçebilirsiniz.
12. Kaydedin ve projeyi oluşturun. Kapsayıcı görüntünüzü kayıt defterine gönderilir ve web uygulama bakın.

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a>Docker kullanılarak Jenkins ardışık düzeni aracılığıyla Linux'ta Web uygulamasına dağıtma

1. GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_container_plugin** dosya. Web uygulamanızı 11 ve 12 satırındaki adını ve kaynak grubu sırasıyla güncelleştirmek için bu dosyayı düzenlemek için Kalem simgesine tıklayın.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Kapsayıcı kayıt defteri sunucunuza satır 13 değiştirme    
```java
def registryServer = '<registryURL>'
```    

3. Satır kimlik bilgisi kimliği Jenkins Örneğinizde güncelleştirmek için 16 değiştirme    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Jenkins işlem hattı oluşturma    

1. Jenkins bir web tarayıcısında açın, **yeni öğe**.
2. Seçin ve iş için bir ad **ardışık düzen**. **Tamam** düğmesine tıklayın.
3. Tıklatın **ardışık düzen** sekmesinde sonraki.
4. İçin **tanımı**seçin **kanal SCM betikten**.
5. İçin **SCM**seçin **Git**.
6. Forked, depodaki için GitHub URL'yi girin: https:&lt;forked depodaki > .git</li>
7, güncelleştirme **komut dosyası yolu** "Jenkinsfile_container_plugin" için
8. Tıklatın **kaydetmek** ve işini çalıştırın.

## <a name="verify-your-web-app"></a>Web uygulamanızı doğrulayın

1. WAR doğrulamak için dosyası, web uygulamanızın başarıyla dağıtılır. Bir web tarayıcısı açın.
2. Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/ping görürsünüz:    
     Java Web uygulaması'na Hoş!!! Bu güncelleştirilmiş!
   Sun Haz 17 16:39:10 UTC 2017
3. Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (alternatif &lt;x > ve &lt;y > sayılar içeren) x toplamını almak için ve y        
    ![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Linux için uygulama hizmeti

* , Azure CLI'da doğrulamak için çalıştırın:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Aşağıdaki sonucu alın:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/ping. İletiyi görürsünüz: 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (alternatif &lt;x > ve &lt;y > sayılar içeren) x toplamını almak için ve y
    
## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure App Service eklentisi Azure'a dağıtmak için kullanın.

Size nasıl öğrenilen için:

> [!div class="checklist"]
> * FTP aracılığıyla Azure uygulama hizmeti dağıtmak için Jenkins yapılandırın 
> * Azure uygulama hizmeti Docker aracılığıyla Linux'ta dağıtmak için Jenkins yapılandırın 
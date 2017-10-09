---
title: aaaExecute hello Jenkins ile Azure CLI | Microsoft Docs
description: "Nasıl toouse Azure CLI toodeploy bir Java web uygulaması tooAzure Jenkins ardışık düzeninde öğrenin"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>TooAzure Jenkins ile uygulama hizmeti dağıtma ve Azure CLI hello
toodeploy bir Java web uygulaması tooAzure, Azure CLI kullanabileceğiniz [Jenkins ardışık düzen](https://jenkins.io/doc/book/pipeline/). Bu öğreticide, Azure VM temelinde CI/CD işlem hattı oluşturmak için nasıl dahil:

> [!div class="checklist"]
> * Jenkins VM oluşturma
> * Jenkins yapılandırın
> * Bir web uygulaması oluşturma
> * GitHub depo hazırlama
> * Jenkins işlem hattı oluşturma
> * Merhaba ardışık düzen çalıştırın ve başlangıç web uygulaması doğrulayın

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. çalıştırma toofind hello sürüm `az --version`. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Oluşturma ve yapılandırma Jenkins örneği
Jenkins asıl zaten yoksa, hello ile başlangıç [çözüm şablonu](install-jenkins-solution-template.md), gerekli hello içerir [Azure kimlik bilgilerini](https://plugins.jenkins.io/azure-credentials) varsayılan eklentisi. 

Hello Azure kimlik bilgisi eklentisi içinde Jenkins toostore Microsoft Azure hizmet asıl kimlik bilgileri sağlar. Bu Jenkins ardışık düzen hello Azure kimlik alabilmek için sürüm 1.2 biz hello desteği eklendi. 

1.2 veya sonraki bir sürümü olduğundan emin olun:
* Merhaba Jenkins Pano içinde tıklatın **Jenkins Yönet -> eklentisi Yöneticisi ->** arayın ve **Azure kimlik bilgisi**. 
* Merhaba sürüm 1.2 eskiyse hello eklentisi güncelleştirin.

Ayrıca Java JDK ve Maven hello Jenkins yöneticisinde gereklidir. tooinstall, SSH kullanarak tooJenkins yöneticisinde oturum ve hello aşağıdaki komutları çalıştırın:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure hizmet asıl tooJenkins kimlik bilgisi Ekle

Azure kimlik bilgisi gerekli tooexecute Azure CLI ' dir.

* Merhaba Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**. Tıklatın **genel credentials(unrestricted)**.
* Tıklatın **kimlik bilgilerini eklemek** tooadd bir [Microsoft Azure hizmet sorumlusu](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) hello abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak. Sonraki adımda kullanmak için bir kimlik belirtin.

![Kimlik bilgileri Ekle](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Merhaba Java web uygulaması dağıtmak için bir Azure uygulama hizmeti oluşturma

Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu. Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar. Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Hello planı hazır olduğunda, Azure CLI benzer gösterir hello aşağıdaki örneğine toohello çıktı:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Bir Azure Web uygulaması oluşturma

 Kullanım hello [az webapp oluşturma](/cli/azure/appservice/web#create) CLI komutu toocreate bir web uygulaması tanımı'nda hello `myAppServicePlan` uygulama hizmeti planı. Merhaba web uygulaması tanımı URL tooaccess uygulamanızla sağlar ve çeşitli seçenekler toodeploy kod tooAzure yapılandırır. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Yedek hello `<app_name>` kendi benzersiz uygulama adıyla yer tutucu. Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için bir parçasıdır. Tooyour kullanıcılar kullanıma önce bir özel etki alanı adı girişi toohello web uygulaması eşleyebilirsiniz.

Merhaba web uygulaması tanımı hazır olduğunda, aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Java yapılandırın 

Uygulamanızın ile Merhaba gerektiğini hello Java Çalışma zamanı yapılandırma ayarlama [az appservice web yapılandırma güncelleştirmesi](/cli/azure/appservice/web/config#update) komutu.

Merhaba aşağıdaki komutu hello web uygulama toorun üzerinde yeni bir Java 8 JDK yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>GitHub depo hazırlama
Açık hello [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) deposu. toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.

* GitHub web kullanıcı Arabirimi, açık **Jenkinsfile** dosya. Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 20 ve 21 satırındaki'ı tıklatın.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Satırı 23 tooupdate kimlik bilgisi kimliği Jenkins Örneğinizde değiştirme

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Jenkins işlem hattı oluşturma
Jenkins bir web tarayıcısında açın, **yeni öğe**. 

* Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**. **Tamam** düğmesine tıklayın.
* Merhaba tıklatın **ardışık düzen** sekmesinde sonraki. 
* İçin **tanımı**seçin **kanal SCM betikten**.
* İçin **SCM**seçin **Git**.
* Merhaba GitHub URL forked depodaki girin: https:\<forked repo\>.git
* Tıklatın **Kaydet**

## <a name="test-your-pipeline"></a>İşlem hattınızı test
* Oluşturduğunuz toohello ardışık gidin, tıklatın **şimdi derleme**
* Birkaç saniye içinde bir yapı başarılı olması gerekir ve Git toohello yapı ve tıklatın **konsol çıktısı** toosee hello ayrıntıları

## <a name="verify-your-web-app"></a>Web uygulamanızı doğrulayın
tooverify hello WAR dosyası başarıyla dağıtılan tooyour web uygulaması. Bir web tarayıcısı açın:

* Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping  
Görürsünüz:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y

![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>TooAzure Linux üzerinde Web uygulaması dağıtma
Nasıl toouse, Jenkins Azure CLI kanal bildiğinize göre hello betik toodeploy tooan Azure Web uygulaması Linux'ta değiştirebilirsiniz.

Web uygulaması Linux'ta toouse Docker olan bir farklı bir şekilde toodo hello dağıtımını destekler. toodeploy, tooprovide Docker görüntüsüne web uygulamanızı hizmet çalışma zamanı paketleri bir Dockerfile gerekir. Merhaba eklentisi hello görüntüsünü oluşturabilirsiniz, tooa Docker kayıt defteri anında sonra hello görüntü tooyour web uygulaması dağıtma.

* Merhaba adımları [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) Azure Web uygulaması Linux üzerinde çalışan bir toocreate.
* Bu hello yönergeleri izleyerek Jenkins örneğinde Docker yükleme [makale](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Merhaba adımları kullanarak bir kapsayıcı kayıt defteri hello Azure portal oluşturma [burada](/azure/container-registry/container-registry-get-started-azure-cli).
* İçinde aynı hello [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) , çatallanmış, depodaki Düzenle hello **Jenkinsfile2** dosyası:
    * 18-21 satır, kaynak grubu, web uygulaması ve ACR toohello adlarını sırasıyla güncelleştirin. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Satır 24, güncelleştirme \<azsrvprincipal\> tooyour kimlik bilgisi kimliği
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Windows, yalnızca bu kez, kullanım tooAzure web uygulamasında dağıtırken yaptığınız gibi yeni Jenkins işlem hattı oluşturma **Jenkinsfile2** yerine.
* Yeni işinizi çalıştırmak.
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
Bu öğreticide, GitHub deposuna hello kaynak kodunda kullanıma Jenkins ardışık yapılandırılmış. Maven toobuild war dosyasını çalıştırır ve Azure CLI toodeploy tooAzure uygulama hizmeti kullanır. Şunları öğrendiniz:

> [!div class="checklist"]
> * Jenkins VM oluşturma
> * Jenkins yapılandırın
> * Bir web uygulaması oluşturma
> * GitHub depo hazırlama
> * Jenkins işlem hattı oluşturma
> * Merhaba ardışık düzen çalıştırın ve başlangıç web uygulaması doğrulayın

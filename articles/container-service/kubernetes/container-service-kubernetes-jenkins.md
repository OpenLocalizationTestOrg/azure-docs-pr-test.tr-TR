---
title: "aaaJenkins CI/CD Azure kapsayıcı Hizmeti'nde Kubernetes ile | Microsoft Docs"
description: "Tooautomate bir CI/CD işleminin nasıl Jenkins toodeploy ve Kubernetes Azure kapsayıcı Hizmeti'nde bir kapsayıcılı uygulamasını yükseltme"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, kapsayıcıları, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Azure kapsayıcı hizmeti ve Kubernetes Jenkins tümleştirme 
Bu öğreticide, biz hello işlem tooset sürekli tümleştirme çok kapsayıcı uygulamasının Azure kapsayıcı hizmeti hello Jenkins platformu kullanılarak Kubernetes yol. Merhaba iş akışı Docker hub'a hello kapsayıcı görüntüyü güncelleştirir ve dağıtımı sunumu kullanarak hello Kubernetes pod'ları yükseltir. 

## <a name="high-level-process"></a>Yüksek düzeyli işlem
Bu makalede ayrıntılı hello temel adımlar şunlardır: 
- Kapsayıcı Hizmeti'nde bir Kubernetes küme yükleyin
- Jenkins ayarlama ve erişimi tooContainer hizmetini yapılandırma
- Jenkins iş akışı oluşturma
- Merhaba CI/CD işlemi son tooend test

## <a name="install-a-kubernetes-cluster"></a>Kubernetes küme yükleyin
    
Merhaba Kubernetes hello aşağıdaki adımları kullanarak Azure kapsayıcı hizmeti kümesinde dağıtın. Tam belgelerine bulunduğu [burada](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>1. adım: bir kaynak grubu oluşturma
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>2. adım: hello küme dağıtma
> [!NOTE]
> Merhaba aşağıdaki adımları hello ~/.ssh klasöründe bulunan yerel bir SSH ortak anahtarı gerektirir.
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Jenkins ayarlama ve erişimi tooContainer hizmetini yapılandırma

### <a name="step-1-install-jenkins"></a>1. adım: Jenkins yükleme
1. Ubuntu 16.04 ile bir Azure VM oluşturma LTS.  Hello sonraki adımlar bu yana tooconnect toothis VM kullanarak kümesi hello 'Kimlik doğrulama türü' too'SSH ortak anahtar, yerel makinenize bash ' ve ~/.ssh klasörünüzde yerel olarak depolanan Yapıştır hello SSH ortak anahtarı.  Ayrıca, bu kullanıcı adı gerekli tooview hello Jenkins Pano olacağından ve daha sonraki adımlarda toohello Jenkins VM bağlama belirtin hello 'User name' not edin.
2. Jenkins yüklemeniz [yönergeleri](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Daha ayrıntılı bir öğretici altındadır [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview Jenkins Pano yerel makinenizde Merhaba, erişim tooport 8080 izin veren bir gelen kuralı ekleyerek hello Azure ağ güvenlik grubu tooallow bağlantı noktası 8080 güncelleştirin.  Alternatif olarak, şu komutu çalıştırarak bağlantı noktası iletme Kurulum:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Toohello genel IP giderek Hello tarayıcı kullanarak tooyour Jenkins sunucusuna (http:// < your_jenkins_public_ip >: 8080) ve hello hello Jenkins panosunu hello ilk yönetici parolası ile ilk kez kilidini açın.  Merhaba yönetici parolası hello Jenkins VM üzerinde /var/lib/jenkins/secrets/initialAdminPassword konumunda depolanır.  Bu paroladır tooSSH içine bir kolay bir yolu tooget Jenkins VM hello: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Ardından, çalıştırın: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Bunlar aracılığıyla hello Jenkins makinenize Docker yüklemek [yönergeleri](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Docker komutları toobe Jenkins işlerini çalıştırmak için bu sağlar.
6. Docker izinleri tooallow Jenkins tooaccess hello Docker uç noktasını yapılandırın.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Yükleme `kubectl` CLI Jenkins üzerinde. Daha fazla ayrıntı altındadır [yükleme ve kubectl ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).  Jenkins işleri 'kubectl' toomanage kullanabilir ve toohello Kubernetes küme dağıtabilirsiniz.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>2. adım: erişim toohello Kubernetes kümesi

> [!NOTE]
> Aşağıdaki adımları birden çok yaklaşımlar tooaccomplishing hello vardır. Sizin için en kolayıdır hello yaklaşımı kullanın.
>

1. Kopya hello `kubectl` Jenkins, böylece Jenkins işleri erişim toohello Kubernetes küme makine yapılandırma dosyası toohello. Bu yönergeleri varsayar Jenkins VM hello olandan farklı bir makineden bash kullanıyorsanız ve yerel bir SSH ortak anahtarını hello makinenin ~/.ssh klasöründe depolanır.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Bu hello Kubernetes Jenkins doğrulama kümedir erişilebilir.  toodo hello Jenkins VM içine bu, SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Ardından, Jenkins tooyour küme başarıyla bağlanabilir doğrulayın: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Jenkins iş akışı oluşturma

### <a name="prerequisites"></a>Ön koşullar

- Kod deposu için GitHub hesabı.
- Toostore ve güncelleştirme docker hub'a hesabı görüntüler.
- Yeniden ve güncelleştirilmiş kapsayıcılı uygulama. Bu örnek kapsayıcı uygulaması Golang içinde yazılmış kullanabilirsiniz: https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Merhaba aşağıdaki adımlarda kendi GitHub hesabınızda gerçekleştirilmesi gerekir. Depodaki, yukarıda ücretsiz tooclone hello eşitleyerek ancak Jenkins erişmek ve kendi hesabı tooconfigure hello kancalarını kullanmanız gerekir.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>1. adım: uygulamanın ilk v1 dağıtma
1. Merhaba uygulama hello Geliştirici makineden komutları aşağıdaki hello ile oluşturun. Değiştir `myrepo` kendi değerlerinizle.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Görüntü tooDocker Hub iletin.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Toohello Kubernetes küme dağıtın.
    
    > [!NOTE] 
    > Merhaba Düzenle `go-web.yaml` tooupdate kapsayıcı görüntü ve depo dosya.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>2. adım: Jenkins sistem yapılandırma
1. Tıklatın **Jenkins yönetmek** > **sistem yapılandırma**.
2. Altında **GitHub**seçin **GitHub Sunucu Ekle**.
3. Bırakın **API URL** varsayılan olarak.
4. Altında **kimlik bilgileri**, Jenkins kimlik bilgilerini kullanarak eklemek **gizli metin**. GitHub kullanıcı hesap ayarlarınızda yapılandırılmış GitHub kişisel erişim belirteçleri kullanmanızı öneririz. Bunun hakkında daha fazla ayrıntı [burada.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Tıklatın **Bağlantıyı Sına** tooensure bu doğru yapılandırılmış.
6. Altında **genel özellikleri**, bir ortam değişkeni ekleyin `DOCKER_HUB` ve Docker hub'a parolanızı girin. (Bu gösteride kullanışlıdır ancak bir üretim senaryosu daha güvenli bir yöntem gerektirir.)
7. Kaydedin.

![Jenkins GitHub erişim](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>3. adım: Merhaba Jenkins iş akışı oluşturma
1. Jenkins öğesi oluşturun.
2. Bir ad girin (örneğin, "Web'de Git") seçip **Freestyle proje**. 
3. Denetleme **GitHub proje** ve hello URL tooyour GitHub deposuna sağlayın.
4. İçinde **kaynak kodu Yönetimi**, hello GitHub deposuna URL ve kimlik bilgilerini sağlayın. 
5. Ekleme bir **derleme adımı** türü **Kabuk yürütme** ve kullanım hello aşağıdaki metin:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Başka bir tane eklemek **derleme adımı** türü **Kabuk yürütme** ve kullanım hello aşağıdaki metin:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins derleme adımları](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Merhaba Jenkins öğeyi kaydetmek ve test **şimdi yapı**.

### <a name="step-4-connect-github-webhook"></a>4. adım: GitHub Web kancası bağlanma
1. Merhaba Jenkins öğeyi oluşturduğunuz tıklatın **yapılandırma**.
2. Altında **yapı tetikleyicileri**seçin **GITScm yoklama için GitHub kanca tetikleyici** ve **kaydetmek**. Bu, hello GitHub Web kancası otomatik olarak yapılandırır.
3. Web Git, GitHub deposuna içinde tıklatın **ayarlar > Web Kancalarını**.
4. Bu hello Jenkins Web kancası URL'si başarıyla eklendi doğrulayın. Merhaba URL "github-Web kancası" bitmelidir.

![Jenkins Web kancası yapılandırma](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Merhaba CI/CD işlemi son tooend test

1. Merhaba depodaki ve anında iletme/eşitlemesi için kod hello GitHub deposuyla güncelleştirin.
2. Merhaba Jenkins konsolundan hello denetleyin **yapı geçmiş** ve o hello doğrulama işi çalıştıktan. Konsol çıkış toosee ayrıntıları görüntüleyin.
3. Kubernetes hello ayrıntılarını görüntüleme dağıtım yükseltme:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Sonraki adımlar

- Azure kapsayıcı kayıt defteri dağıtın ve güvenli bir depoda görüntüleri saklamak. Bkz: [Azure kapsayıcı kayıt defteri belgeleri](https://docs.microsoft.com/azure/container-registry).
- Yan yana dağıtım ve otomatikleştirilmiş testleri Jenkins içeren daha karmaşık bir iş akışı oluşturma.
- Merhaba CI/CD Jenkins ve Kubernetes hakkında daha fazla bilgi için bkz: [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).

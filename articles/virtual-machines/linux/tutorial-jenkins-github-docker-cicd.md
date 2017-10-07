---
title: "aaaCreate Jenkins ile azure'da geliştirme ardışık | Microsoft Docs"
description: "Nasıl toocreate Jenkins sanal makine github'dan çeken her kodunda kaydetmek ve yeni bir Docker kapsayıcısı toorun derlemeler Azure'da uygulamanızı öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Nasıl toocreate Jenkins, GitHub ve Docker ile azure'da bir Linux VM üzerinde geliştirme altyapısı
tooautomate hello yapı ve test aşaması uygulama geliştirme, bir sürekli tümleştirme ve dağıtım (CI/CD) ardışık düzen kullanabilirsiniz. Bu öğreticide, Azure VM temelinde CI/CD işlem hattı oluşturmak için nasıl dahil:

> [!div class="checklist"]
> * Jenkins VM oluşturma
> * Yükleme ve Jenkins yapılandırma
> * GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma
> * Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler
> * Uygulamanız için Docker görüntü oluşturma
> * Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Jenkins örneği oluşturma
Önceki bir öğretici içinde [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md), size nasıl öğrenilen tooautomate VM özelleştirme bulut init ile. Bu öğretici, bir VM üzerinde bir bulut init dosya tooinstall Jenkins ve Docker kullanır. 

Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma. Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun. Girin `sensible-editor cloud-init-jenkins.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz. Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupJenkins* hello içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create). Kullanım hello `--custom-data` parametresi toopass bulut init yapılandırma dosyası. Merhaba tam yol çok sağlamak*bulut init jenkins.txt* mevcut çalışma dizininizi dışında hello dosyasını kaydettiyseniz.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Oluşturulan ve yapılandırılan hello VM toobe birkaç dakika sürer.

tooallow web trafiği tooreach kullanım VM'nizi [az vm Aç-port](/cli/azure/vm#open-port) tooopen bağlantı noktası *8080* Jenkins trafiği ve bağlantı noktası için *1337* kullanılan toorun örnek bir uygulama olan hello Node.js uygulaması için:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Jenkins yapılandırın
tooaccess, Jenkins örneği, VM'yi hello genel IP adresi edinin:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Güvenlik nedeniyle, Jenkins yüklemek, VM toostart hello üzerindeki bir metin dosyasında depolanan tooenter hello ilk yönetici parolası gerekir. Merhaba önceki adım tooSSH tooyour içinde VM elde hello ortak IP adresini kullan:

```bash
ssh azureuser@<publicIps>
```

Görünüm hello `initialAdminPassword` , Jenkins yükleyin ve onu kopyalamak için:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Merhaba dosya henüz kullanılabilir durumda değilse, bulut init toocomplete hello Jenkins ve Docker yükleme için birkaç dakika daha bekleyin.

Şimdi bir web tarayıcısı açın ve çok Git`http://<publicIps>:8080`. Merhaba ilk Jenkins Kurulum aşağıdaki gibi tamamlayın:

- Merhaba girin *initialAdminPassword* hello VM hello önceki adımda elde.
- Tıklatın **eklentileri tooinstall seçin**
- Arama *GitHub* hello metin kutusunda hello üstte hello seçin *GitHub eklentisi*, ardından **yükleyin**
- toocreate Jenkins kullanıcı hesabını istediğiniz gibi hello formu doldurun. Güvenlik açısından bakıldığında, hello varsayılan yönetici hesabı olarak etmeden yerine bu ilk Jenkins kullanıcı oluşturmanız gerekir.
- Tamamlandığında tıklatarak **Jenkins kullanmaya başlama**


## <a name="create-github-webhook"></a>GitHub Web kancası oluşturma
GitHub, açık hello ile tooconfigure hello tümleştirme [Node.js Hello World örnek uygulaması](https://github.com/Azure-Samples/nodejs-docs-hello-world) hello Azure örneklerinden depodaki gelen. toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.

Oluşturduğunuz hello çatalı içinde bir Web kancası oluşturun:

- Tıklatın **ayarları**seçeneğini belirleyip **tümleştirmeler & Hizmetleri** hello sol taraftaki.
- Tıklatın **Hizmet Ekle**, enter *Jenkins* filtre kutusuna.
- Seçin *Jenkins (GitHub eklentisi)*
- Hello için **Jenkins kanca URL**, girin `http://<publicIps>:8080/github-webhook/`. Merhaba sondaki eklediğinizden emin olun /
- Tıklatın **Hizmet Ekle**

![GitHub Web kancası çatallanmış tooyour depo Ekle](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Jenkins işi oluşturma
kod yürütme gibi toohave Jenkins yanıt tooan olay github'da Jenkins iş oluşturun. 

Jenkins siteniz tıklatın **yeni işleri oluşturmak** hello giriş sayfasından:

- Girin *HelloWorld* iş adı olarak. Seçin **Serbest stilde proje**seçeneğini belirleyip **Tamam**.
- Merhaba altında **genel** bölümünde, select **GitHub** proje ve çatallanmış depodaki URL'nizi girin *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Merhaba altında **kaynak kodu Yönetimi** bölümünde, select **Git**, forked depodaki girin *.git* URL gibi *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Merhaba altında **yapı tetikleyicileri** bölümünde, select **GITscm yoklama için GitHub kanca tetikleyici**.
- Merhaba altında **yapı** bölümünde, seçin **Ekle derleme adımı**. Seçin **Kabuk yürütme**, enter `echo "Testing"` toocommand penceresinde.
- Tıklatın **kaydetmek** hello altındaki hello işler penceresi.


## <a name="test-github-integration"></a>Test GitHub tümleştirme
tootest hello Jenkins, GitHub tümleştirme, çatalı değişikliği uygulayın. 

Geri Github'da web kullanıcı Arabirimi, forked depoyu seçin ve hello ardından **index.js** dosya. Satır 6 okunacak şekilde hello Kurşun Kalem simgesini tooedit bu dosyayı tıklatın:

```nodejs
response.end("Hello World!");
```

toocommit yaptığınız değişiklikleri tıklatın hello **değişiklikleri** hello altındaki düğmesi.

Jenkins içinde yeni bir yapı altında hello başlatır **yapı geçmiş** hello sol alt köşesindeki iş sayfanızı bölümü. Merhaba yapı numarası bağlantısına ve Seç'i tıklatın **konsol çıkış** hello sol boyutu. Jenkins alır, kodunuzu GitHub ve hello yapı eylemi çıkışları hello iletiden çekildiğinde hello adımları görüntüleyebilirsiniz `Testing` toohello konsol. Github'da, her bir işleme yapıldığında hello Web kancası tooJenkins ulaştığında ve bu şekilde yeni bir derlemeyi tetiklemeyi.


## <a name="define-docker-build-image"></a>Docker derleme görüntüyü tanımlayın
toosee hello Node.js uygulaması, GitHub yürütme üzerinde temelinde çalışmasına olanak tanır bir Docker görüntü toorun hello uygulaması oluşturma. Merhaba görüntü nasıl tooconfigure hello hello uygulamanın çalıştığı kapsayıcı tanımlayan bir Dockerfile yerleşik olarak bulunur. 

Merhaba SSH bağlantı tooyour VM, bir önceki adımda oluşturduğunuz hello iş sonra adlı toohello Jenkins çalışma dizini değiştirin. Bizim örneğimizde, adlandırılması *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Bu çalışma alanı dizindeki bir dosya oluşturmak `sudo sensible-editor Dockerfile` Yapıştır hello izleyerek içeriği. Tüm Dockerfile olduğundan bu hello özellikle hello ilk satırı doğru şekilde kopyalandığından emin olun:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Bu Dockerfile hello Alpine Linux kullanarak temel Node.js görüntü kullanır, Hello World uygulama hello çıkarır bağlantı 1337 çalışan sonra hello uygulama dosyaları kopyalar ve onu başlatır.


## <a name="create-jenkins-build-rules"></a>Jenkins derleme kuralları oluşturma
Önceki adımda, bir ileti toohello konsol çıktısı temel bir Jenkins yapı kuralı oluşturuldu. Bizim Dockerfile Hello derleme adımı toouse oluşturma ve hello uygulama çalıştırma olanak sağlar.

Geri Jenkins örneğinizi içinde bir önceki adımda oluşturduğunuz hello işi seçin. Tıklatın **yapılandırma** hello taraftaki ve toohello aşağı kaydırın **yapı** bölümü:

- Var olan kaldırmak `echo "Test"` adım oluşturma. Merhaba kırmızı çapraz ya hello üst sağ köşesinde hello varolan derleme adımı kutusu üzerinde'ı tıklatın.
- Tıklatın **Ekle derleme adımı**seçeneğini belirleyip **Kabuk yürütme**
- Merhaba, **komutu** kutusunda, Docker komutları aşağıdaki hello girin, ardından seçin **kaydetmek**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

Merhaba Docker derleme adımları imaj ve hello Jenkins ile yapı numarası görüntüleri bir geçmişini sağlamak için etiketi oluşturun. Merhaba uygulamayı çalıştıran herhangi bir varolan kapsayıcıdaki durdurulur ve sonra kaldırılır. Merhaba görüntü kullanmaya ve hello son yürütme github'da göre Node.js uygulamanızı çalıştıran yeni bir kapsayıcıdır.


## <a name="test-your-pipeline"></a>İşlem hattınızı test
Eylem içinde toosee hello tüm ardışık Düzenle hello *index.js* , forked GitHub deposuna dosya yeniden ve'ı tıklatın **Commit değişiklik**. Jenkins için GitHub hello Web kancası dayalı yeni bir iş başlatır. Toocreate hello Docker görüntü birkaç saniye sürer ve yeni bir kapsayıcı uygulamanızı başlatın.

Gerekirse, hello genel IP adresi, bir VM'nin yeniden alın:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Bir web tarayıcısı açın ve girin `http://<publicIps>:1337`. Node.js uygulamanızı görüntülenir ve GitHub çatalı içinde hello son yürütme gibi yansıtır:

![Çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Artık başka bir düzen toohello olun *index.js* GitHub ve yürütme hello değişiklik dosyasında. Merhaba iş toocomplete Jenkins, birkaç saniye bekleyin, sonra da web tarayıcı toosee hello güncelleştirilmiş sürümü yeni bir kapsayıcı şu şekilde çalışan, uygulamanızın yenileyin:

![Başka bir GitHub yürütme sonrasında çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide her kod tamamlama GitHub toorun Jenkins derleme işi yapılandırılmış ve Docker kapsayıcısı tootest uygulamanızı dağıtabilirsiniz. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Jenkins VM oluşturma
> * Yükleme ve Jenkins yapılandırma
> * GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma
> * Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler
> * Uygulamanız için Docker görüntü oluşturma
> * Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın

Toohello sonraki öğretici toolearn hakkında daha fazla ilerletmek toointegrate Jenkins Visual Studio Team Services ile.

> [!div class="nextstepaction"]
> [Jenkins ve Team Services ile uygulamaları dağıtma](tutorial-build-deploy-jenkins.md)
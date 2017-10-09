---
title: "aaaUse Docker Compose azure'da bir Linux VM üzerinde | Microsoft Docs"
description: "Azure CLI toouse Docker ve oluşturma ile Linux sanal makinelerde nasıl hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Docker ve oluşturma toodefine ile başlatılan alın ve Azure'da çok kapsayıcı uygulamayı çalıştırın
İle [oluşturma](http://github.com/docker/compose), basit bir metin dosyası toodefine birden çok Docker kapsayıcıları için oluşan bir uygulama kullanın. Ardından, her şeyi yapar tek bir komut uygulamanızda Yukarı Döndür toodeploy tanımlanan ortamınızı. Örnek olarak, bu makalede nasıl tooquickly bir arka uç ile bir WordPress blog MariaDB SQL veritabanı bir Ubuntu VM ayarlanacağını gösterir. Daha karmaşık uygulamaları oluşturma tooset de kullanabilirsiniz.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Bir Linux VM Docker ana bilgisayar olarak ayarlama
Çeşitli Azure yordamları ve kullanılabilir görüntüler veya Resource Manager şablonları hello Azure Marketi toocreate bir Linux VM kullanın ve Docker ana bilgisayar olarak ayarlayın. Örneğin, [hello Docker VM uzantısı toodeploy ortamınızı kullanarak](dockerextension.md) tooquickly oluşturma bir Ubuntu VM hello Azure Docker VM uzantısı ile kullanarak bir [hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Merhaba Docker VM uzantısı kullandığınızda, VM otomatik olarak Docker ana bilgisayar olarak ayarlanır ve oluşturma zaten yüklü.


### <a name="create-docker-host-with-azure-cli-20"></a>Azure CLI 2.0 ile Docker konak oluştur
Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).

İlk olarak, Docker ortamınız için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) hello Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Merhaba dağıtım toofinish birkaç dakika sürer. Merhaba dağıtım tamamlandıktan sonra [toonext adım taşıma](#verify-that-compose-is-installed) tooSSH tooyour VM. 

İsteğe bağlı olarak tooinstead dönüş denetimi toohello istemi ve let hello dağıtım hello arka planda devam hello ekleyin `--no-wait` komutu önceki toohello bayrak. Bu işlem tooperform sağlar hello hello dağıtım için bir kaç dakika devam ederken CLI diğer iş. Ardından hello Docker ana bilgisayar durumu ile ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show). Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Bu komut döndüğünde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM adım aşağıdaki hello de kullanabilirsiniz.


## <a name="verify-that-compose-is-installed"></a>Oluşturma yüklü olduğunu doğrulayın
Merhaba DNS adını kullanarak SSH tooyour yeni Docker ana bilgisayar Hello dağıtım tamamlandıktan sonra dağıtım sırasında sağladığınız. Kullanabileceğiniz `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` hello DNS adı dahil olmak üzere, VM tooview ayrıntıları.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Oluşturan toocheck hello üzerinde VM, komutu aşağıdaki hello çalıştırmak yüklenir:

```bash
docker-compose --version
```

Çok benzer bir çıktı görmeniz*1.6.2 docker compose'u, 4 d 72027 yapı*.

> [!TIP]
> Başka bir yöntem toocreate Docker ana kullanılan ve tooinstall kendiniz oluşturan varsa hello bkz [belgeleri oluşturma](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Docker-compose.yml yapılandırma dosyası oluşturma
Ardından, oluşturduğunuz bir `docker-compose.yml` yalnızca bir metin yapılandırma dosyası, toodefine hello Docker kapsayıcıları toorun hello VM üzerinde dosya. Merhaba dosya her kapsayıcı hello görüntü toorun belirtir (veya bir Dockerfile derleme olabilir), gerekli ortam değişkenleri ve bağımlılıkları, bağlantı noktalarını ve kapsayıcılar arasındaki hello bağlantılar. Yml dosya sözdizimi hakkında daha fazla bilgi için bkz: [dosya başvurusu oluşturan](https://docs.docker.com/compose/compose-file/).

Merhaba oluşturma *docker-compose.yml* gibi dosya:

```bash
touch docker-compose.yml
```

Sık kullandığınız metin düzenleyicisi tooadd bazı veri toohello dosyasını kullanın. Merhaba aşağıdaki örnek kullanır hello *VI* Düzenleyicisi:

```bash
vi docker-compose.yml
```

Örnek metin dosyanıza aşağıdaki hello yapıştırın. Bu yapılandırma hello görüntülerden kullanıyor [DockerHub kayıt defteri](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Merhaba açık kaynak blog ve içerik yönetim sistemi) ve bağlantılı arka uç MariaDB SQL veritabanı. Kendi girin *MYSQL_ROOT_PASSWORD* gibi:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Merhaba kapsayıcılara oluşturma ile Başlat
İçinde aynı hello olarak dizin, *docker-compose.yml* dosyası, komut aşağıdaki hello çalıştırın (ortamınıza bağlı olarak toorun gerekebilecek `docker-compose` kullanarak `sudo`):

```bash
docker-compose up -d
```

Bu komut belirtilen hello Docker kapsayıcıları başlatır *docker-compose.yml*. Bir veya iki Bu adım toocomplete için dakika sürer. Aşağıdaki örnek çıkış benzer toohello bakın:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Emin toouse hello olması **-d** Merhaba kapsayıcılara hello arka planda sürekli çalışmasını böylece üzerinde başlatma seçeneği.


Merhaba kapsayıcılara hazır tooverify türü `docker-compose ps`. Benzer bir şey görmeniz gerekir:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Şimdi doğrudan hello VM bağlantı noktası 80 üzerinde tooWordPress bağlanabilir. Bir web tarayıcısı açın ve VM hello DNS adını girin (gibi `http://mypublicdns.westus.cloudapp.azure.com`). WordPress başlangıç ekranında, burada hello yüklemeyi tamamlamak ve Merhaba uygulaması ile çalışmaya başlama hello görmelisiniz.

![WordPress başlangıç ekranı][wordpress_start]

## <a name="next-steps"></a>Sonraki adımlar
* Toohello Git [Docker VM uzantısı Kullanıcı Kılavuzu'na](https://github.com/Azure/azure-docker-extension/blob/master/README.md) daha fazla seçenekleri tooconfigure Docker ve Docker VM oluşturma. Örneğin, bir seçenek tooput hello oluşturma yml (dönüştürülen tooJSON) doğrudan hello Docker VM uzantısı hello yapılandırmasını dosyasıdır.
* Merhaba denetleyin [komut satırı başvurusu oluşturan](http://docs.docker.com/compose/reference/) ve [Kullanıcı Kılavuzu](http://docs.docker.com/compose/) oluşturma ve birden çok kapsayıcı uygulamaları dağıtmaya diğer örnekler için.
* Bir Azure Resource Manager şablonu ya da kullanmak, veya bir tane katkıda hello [topluluk](https://azure.microsoft.com/documentation/templates/), toodeploy Docker ve bir uygulama ile bir Azure VM oluşturma ile ayarlayın. Örneğin, hello [bir WordPress blog docker'la dağıtmak](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) oluşturma tooquickly bir Ubuntu VM bir MySQL arka uç ile WordPress dağıtmak ve şablonu Docker kullanır.
* Docker Compose Docker Swarm kümesi ile tümleştirme deneyin. Bkz: [kullanarak oluşturan Swarm ile](https://docs.docker.com/compose/swarm/) senaryoları için.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png

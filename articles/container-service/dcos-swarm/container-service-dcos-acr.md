---
title: "bir Azure DC/OS kümesi ile aaaUsing ACR | Microsoft Docs"
description: "Azure kapsayıcı hizmeti DC/OS kümesinde ile bir Azure kapsayıcı kayıt defteri kullanma"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, kapsayıcıları, mikro hizmetler, Mesos, Azure, dosya paylaşımı, CIFS"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>ACR DC/OS kümesi toodeploy ile uygulamanızı kullanın.

Bu makalede, biz keşfedin nasıl toouse Azure kapsayıcı kayıt defteri DC/OS kümesine sahip. ACR kullanarak tooprivately deposu sağlar ve kapsayıcı görüntüleri yönetin. Bu öğretici hello aşağıdaki görevleri içerir:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri (gerekirse) dağıtın
> * DC/OS kümesinde ACR kimlik doğrulamasını yapılandırma
> * Bir görüntü toohello Azure kapsayıcı kayıt defteri karşıya
> * Bir kapsayıcı görüntüsü hello Azure kapsayıcı kayıt defteri ' çalıştırın

Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir. Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Azure kapsayıcı kayıt defteri dağıtın

Gerekiyorsa, Azure kapsayıcı kayıt defteri ile Merhaba oluşturun [az acr oluşturmak](/cli/azure/acr#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur kayıt defteri ile bir rastgele adı oluşturmak. Merhaba kayıt defteri hello kullanarak bir yönetici hesabıyla aynı zamanda yapılandırılmış `--admin-enabled` bağımsız değişkeni.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Merhaba kayıt defteri oluşturulduktan sonra veri benzer toohello aşağıdaki hello Azure CLI çıkarır. Merhaba not edin `name` ve `loginServer`, bunlar daha sonraki adımlarda kullanılır.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Merhaba kapsayıcı kayıt defteri Hello kullanarak kimlik bilgilerini alma [az acr kimlik bilgisi Göster](/cli/azure/acr/credential) komutu. Yedek hello `--name` bir hello son adımda not ettiğiniz hello ile. Not bir parola bir sonraki adımda gereklidir.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Azure kapsayıcı kayıt defteri hakkında daha fazla bilgi için bkz: [giriş tooprivate Docker kapsayıcısı kayıt defterleri](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>ACR kimlik doğrulamasını yönetmek

toofirst özel bir kayıt defteri toopush ve çekme görüntüdür hello geleneksel şekilde hello kayıt defteri ile kimlik doğrulaması. toodo Merhaba, kullanacağınız `docker login` tooaccess hello özel kayıt defteri gereken herhangi bir istemci üzerinde komutu. DC/OS kümesi tümü ACR hello ile kimlik doğrulaması toobe gerekir, birçok düğümleri içerebileceğinden bu işlem boyunca yararlı tooautomate olduğundan her düğümü. 

### <a name="create-shared-storage"></a>Paylaşılan depolama alanı oluşturma

Bu işlem, hello kümedeki her düğümde takıldıktan bir Azure dosya paylaşımı kullanır. Paylaşılan depolama alanı zaten ayarlamadıysanız bkz [bir DC/OS küme içindeki bir dosya paylaşımı Kurulum](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>ACR kimlik doğrulamasını yapılandırma

İlk olarak, hello DC/OS ana ve bir değişkende saklayın hello FQDN'sini alın.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Bir SSH bağlantısı hello Yöneticisi (ya da hello ilk ana) DC/OS tabanlı kümenizin oluşturun. Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin.

```azurecli-interactive
ssh azureuser@$FQDN
```

Komut toologin toohello Azure kapsayıcı kayıt defteri aşağıdaki hello çalıştırın. Hello yerine `--username` hello kapsayıcı kayıt defteri ve hello hello adıyla `--password` sağlanan hello parolaları biriyle. Merhaba son bağımsız değişken Değiştir *mycontainerregistry.azurecr.io* hello kapsayıcı kayıt defteri hello örnekte hello loginServer ada sahip. 

Bu komut hello kimlik doğrulaması değerleri hello altında yerel olarak depolar `~/.docker` yolu.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Merhaba kapsayıcı kayıt defteri kimlik doğrulama değerleri içeren sıkıştırılmış bir dosya oluşturun.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Bu dosya toohello Küme Paylaşılan depolama kopyalayın. Bu adım hello dosya hello DC/OS kümenin tüm düğümlerinde kullanılabilir hale getirir.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Görüntü tooACR karşıya yükle

Şimdi bir geliştirme makine ya da herhangi bir yüklü Docker sistemiyle, bir görüntü oluşturun ve toohello Azure kapsayıcı kayıt defteri yükleyin.

Merhaba Ubuntu görüntüsünden bir kapsayıcı oluşturun.

```azurecli-interactive
docker run ubunut --name base-image
```

Şimdi hello kapsayıcı yeni bir görüntüsünü yakalayın. Merhaba görüntü adı gerekiyor tooinclude hello `loginServer` hello kapsayıcı registrywith biçimlerinin bir adı `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Hello Azure kapsayıcı kayıt defteri uygulamasına oturum açın. Merhaba adı hello loginServer adla değiştirin,--kullanıcıadı hello adını hello kapsayıcı kayıt defteri ve hello--sağlanan hello parolaları biriyle parola ile Merhaba.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Son olarak, hello görüntü toohello ACR kayıt defteri karşıya yükleyin. Bu örnek dcos demo adlı bir resim yükler.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Bir görüntü ACR çalıştırın

Resmin hello ACR kayıt defterinden toouse adları bir dosya oluşturun *acrDemo.json* ve kopyalama hello aşağıdaki metni içine. Örneğin hello kapsayıcı kayıt defteri loginServer adı ve görüntü adı ile Hello görüntü adı yerine `loginServer/imageName`. Merhaba not edin `uris` özelliği. Bu özellik hello hello DC/OS kümedeki her düğümde takılı hello Azure dosya paylaşımı bu durumda olan hello kapsayıcı kayıt defteri kimlik doğrulaması dosyasının konumunu, tutar.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Merhaba uygulaması hello DC/OC CLI ile dağıtın.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide sahip yapılandırdığınız Azure kapsayıcı aşağıdaki hello dahil olmak üzere kayıt defteri görevleri DC/OS toouse:

> [!div class="checklist"]
> * Azure kapsayıcı kayıt defteri (gerekirse) dağıtın
> * DC/OS kümesinde ACR kimlik doğrulamasını yapılandırma
> * Bir görüntü toohello Azure kapsayıcı kayıt defteri karşıya
> * Bir kapsayıcı görüntüsü hello Azure kapsayıcı kayıt defteri ' çalıştırın

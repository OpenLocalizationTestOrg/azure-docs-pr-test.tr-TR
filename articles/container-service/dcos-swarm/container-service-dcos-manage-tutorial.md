---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Azure kapsayıcı hizmeti Öğreticisi - DC/OS yönetme

DC/OS çalışan modern ve kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar. Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır DC/OS kümesi sağlama. Bu hızlı başlangıç ayrıntıları temel adımlar, bir DC/OS kümesi ve çalışma temel iş yükü toodeploy gerekir.

> [!div class="checklist"]
> * Bir ACS DC/OS kümesi oluşturma
> * Toohello kümesine bağlanın
> * Merhaba DC/OS CLI yükleme
> * Bir uygulama toohello kümeyi dağıtma
> * Merhaba kümede uygulama ölçeklendirme
> * Merhaba DC/OS küme düğümleri ölçeklendirme
> * Temel DC/OS Yönetimi
> * Merhaba DC/OS kümesi Sil

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>DC/OS kümesi oluşturma

İlk olarak, bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Ardından, DC/OS kümesi ile Merhaba oluşturun [az acs oluşturmak](/cli/azure/acs#create) komutu.

Merhaba aşağıdaki örnek adlı bir DC/OS kümesi oluşturur *myDCOSCluster* ve zaten mevcut değilse SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Birkaç dakika sonra hello komut tamamlandıktan ve hello dağıtımı hakkında bilgi döndürür.

## <a name="connect-toodcos-cluster"></a>TooDC/OS kümesine bağlanın

DC/OS kümesi oluşturulduktan sonra bir SSH tüneli üzerinden erişimleri olabilir. Çalışma hello aşağıdaki hello DC/OS ana tooreturn hello genel IP adresi komutu. Bu IP adresi bir değişkende depolanan ve hello sonraki adımda kullanılır.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate SSH tüneli Merhaba, komutu aşağıdaki hello çalıştırın ve hello ekrandaki yönergeleri izleyin. Bağlantı noktası 80 kullanımda hello komutu başarısız olur. Güncelleştirme hello tünelli kullanılmadığı, bağlantı noktası tooone gibi `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>DC/OS CLI'yi yükleyin

Hello kullanarak hello DC/OS CLI'yı yükleme [az acs dcos yükleme-CLI](/azure/acs/dcos#install-cli) komutu. Azure CloudShell kullanıyorsanız, hello DC/OS CLI zaten yüklü. Hello Azure CLI macOS ya da Linux üzerinde çalıştırıyorsanız, sudo toorun hello komutuyla gerekebilir.

```azurecli
az acs dcos install-cli
```

CLI hello kümeyle kullanılabilir hello önce yapılandırılmış toouse hello SSH tüneli olmalıdır. toodo, bu nedenle, aşağıdaki komut, başlangıç bağlantı noktası gerekiyorsa ayarlama hello çalıştırın.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Bir uygulamayı çalıştırın

bir ACS DC/OS kümesi için mekanizma zamanlama hello Marathon varsayılandır. Marathon kullanılan toostart bir uygulamasıdır ve Merhaba uygulaması hello DC/OS kümesinde hello durumunu yönetin. bir uygulama, Marathon aracılığıyla tooschedule adlı bir dosya oluşturmak **marathon app.json**, kopya hello izleyerek içeriği içine. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Komut tooschedule hello uygulama toorun hello DC/OS kümesinde aşağıdaki hello çalıştırın.

```azurecli
dcos marathon app add marathon-app.json
```

toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.

```azurecli
dcos marathon app list
```

Ne zaman hello **görevleri** sütun değeri geçer *0/1* çok*1/1*, uygulama dağıtımı tamamlandı.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Marathon uygulamayı Ölçeklendir

Merhaba önceki örnekte, bir tek örnek uygulaması oluşturuldu. Bu dağıtım hello uygulamanın üç örneğine kullanılabilir, böylece hello açmak tooupdate **marathon app.json** dosya ve hello örnek özellik too3 güncelleştirin.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Merhaba uygulaması Hello kullanarak güncelleştirme `dcos marathon app update` komutu.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.

```azurecli
dcos marathon app list
```

Ne zaman hello **görevleri** sütun değeri geçer *1/3* çok*3/1*, uygulama dağıtımı tamamlandı.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Internet erişilebilir uygulamayı çalıştırma

Merhaba ACS DC/OS kümesi oluşan iki düğüm kümesi üzerinde erişilebilir olan bir ortak hello Internet ve Internet üzerinde erişilemeyen bir özel hello. Merhaba varsayılan hello özel düğümler, hangi hello Son örnekte kullanılan kümesidir.

toomake erişilebilir bir uygulama üzerinde Internet Merhaba, bunları toohello ortak düğüm kümesi dağıtabilirsiniz. toodo, bu nedenle, hello vermek `acceptedResourceRoles` değerini nesne `slave_public`.

Adlı bir dosya oluşturun **nginx public.json** ve kopyalama hello aşağıdaki içeriği içine.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Komut tooschedule hello uygulama toorun hello DC/OS kümesinde aşağıdaki hello çalıştırın.

```azurecli 
dcos marathon app add nginx-public.json
```

Merhaba DC/OS ortak küme aracıları Hello genel IP adresi alın.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Toothis adresi gözatma hello varsayılan NGINX site döndürür.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Ölçek DC/OS kümesi

Merhaba önceki örneklerde, ölçeklendirilmiş toomultiple örnek bir uygulama oluştu. Merhaba DC/OS altyapı da daha fazla veya daha az işlem kapasitesini ölçeklendirilmiş tooprovide olabilir. Bu hello ile yapılır [az acs ölçeklendirme]() komutu. 

DC/OS aracılarının toosee hello geçerli sayısını hello kullan [acs az göster](/cli/azure/acs#show) komutu.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease sayısı too5 Merhaba, hello kullan [az acs ölçeklendirme](/cli/azure/acs#scale) komutu. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>DC/OS kümesi Sil

Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, DC/OS kümesi ve tüm ilişkili kaynakları komutu.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri içeren temel DC/OS yönetim görevle ilgili öğrendiniz. 

> [!div class="checklist"]
> * Bir ACS DC/OS kümesi oluşturma
> * Toohello kümesine bağlanın
> * Merhaba DC/OS CLI yükleme
> * Bir uygulama toohello kümeyi dağıtma
> * Merhaba kümede uygulama ölçeklendirme
> * Merhaba DC/OS küme düğümleri ölçeklendirme
> * Merhaba DC/OS kümesi Sil

Gelişmiş toohello sonraki öğretici toolearn hakkında Yük Dengeleme uygulamada DC/OS Azure üzerinde. 

> [!div class="nextstepaction"]
> [Uygulamalarda yük dengeleme gerçekleştirme](container-service-load-balancing.md)
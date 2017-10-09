---
title: "aaaAzure kapsayıcı hizmeti hızlı başlangıç - DC/OS kümesi dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti hızlı başlangıç - DC/OS kümesi dağıtma"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>DC/OS kümesi dağıtma

DC/OS çalışan modern ve kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar. Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır DC/OS kümesi sağlama. Bu hızlı başlangıç ayrıntıları hello temel adımlar bir DC/OS kümesi ve çalışma temel iş yükü toodeploy gerekir.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum 

Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>DC/OS kümesi oluşturma

DC/OS kümesi ile Merhaba oluşturma [az acs oluşturmak](/cli/azure/acs#create) komutu.

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

Merhaba SSH tüneli çok göz atarak test edilmiş`http://localhost`. Bir bağlantı noktası, diğer 80 oluşturulduğunu hello konumu toomatch ayarlayın. 

Merhaba SSH tüneli başarıyla oluşturulduysa hello DC/OS portal döndürülür.

![DCOS KULLANICI ARABİRİMİ](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>DC/OS CLI'yi yükleyin

Merhaba DC/OS komut satırı arabirimi kullanılan toomanage hello komut satırı DC/OS kümeden ' dir. Hello kullanarak hello DC/OS CLI'yı yükleme [az acs dcos yükleme-CLI](/azure/acs/dcos#install-cli) komutu. Azure CloudShell kullanıyorsanız, hello DC/OS CLI zaten yüklü. 

Hello Azure CLI macOS ya da Linux üzerinde çalıştırıyorsanız, sudo toorun hello komutuyla gerekebilir.

```azurecli
az acs dcos install-cli
```

CLI hello kümeyle kullanılabilir hello önce yapılandırılmış toouse hello SSH tüneli olmalıdır. toodo, bu nedenle, aşağıdaki komut, başlangıç bağlantı noktası gerekiyorsa ayarlama hello çalıştırın.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Bir uygulamayı çalıştırın

bir ACS DC/OS kümesi için mekanizma zamanlama hello Marathon varsayılandır. Marathon kullanılan toostart bir uygulamasıdır ve Merhaba uygulaması hello DC/OS kümesinde hello durumunu yönetin. bir uygulama, Marathon aracılığıyla tooschedule adlı bir dosya oluşturmak *marathon app.json*, kopya hello izleyerek içeriği içine. 

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
dcos marathon app add marathon-app.json
```

toosee hello dağıtım durumunu hello uygulama, komutu aşağıdaki hello çalıştırın.

```azurecli
dcos marathon app list
```

Ne zaman hello **BEKLEYEN** sütun değeri geçer *True* çok*yanlış*, uygulama dağıtımı tamamlandı.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Merhaba DC/OS kümesi aracıları Hello genel IP adresi alın.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Toothis adresi gözatma hello varsayılan NGINX site döndürür.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>DC/OS kümesi Sil

Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, DC/OS kümesi ve tüm ilişkili kaynakları komutu.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Sonraki adımlar

Bu Hızlı Başlangıç, DC/OS kümesi dağıttıktan sonra ve basit bir Docker kapsayıcısı hello kümede çalışan. Azure kapsayıcı hizmeti hakkında daha fazla toolearn toohello ACS öğreticileri devam edin.

> [!div class="nextstepaction"]
> [Bir ACS DC/OS kümesi yönetme](container-service-dcos-manage-tutorial.md)
---
title: "aaaQuickstart - Linux Azure Docker CE küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate hello Azure CLI ile Azure kapsayıcı Hizmeti'nde Linux kapsayıcıları bir Docker CE küme öğrenin."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Docker CE kümesi dağıtma

Bu Hızlı Başlangıç, Docker CE küme hello Azure CLI kullanarak dağıtılır. Web ön uç ve bir Redis örneği oluşan çok kapsayıcı uygulama sonra dağıtılan ve hello kümede çalıştırın. Tamamlandığında, Merhaba uygulaması üzerinden erişilebilen Internet hello.

Azure Container Service’teki Docker CE önizlemededir ve **üretim iş yükleri için kullanılmamalıdır**.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *ukwest* konumu.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

Çıktı:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Docker Swarm kümesi oluşturma

Docker CE küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu. 

Merhaba aşağıdaki örnek adlı bir küme oluşturur *mySwarmCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Birkaç dakika sonra hello komut tamamlandıktan ve biçimlendirilmiş json hello kümesi hakkında bilgi verir.

## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın

Bu hızlı başlangıç hello FQDN'si hello Docker Swarm ana ve hello Docker aracı havuzu gerekir. Tooreturn, her ikisi de hello ana ve aracısını FQDN'lere komutu aşağıdaki hello çalıştırın.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Çıktı:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Bir SSH tünel toohello Swarm şablonu oluşturun. Değiştir `MasterFQDN` hello Swarm yöneticisinin hello FQDN adresine sahip.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Set hello `DOCKER_HOST` ortam değişkeni. Bu işlem, toospecify hello hello ana bilgisayar adını gerek kalmadan hello Docker Swarm karşı toorun docker komutları sağlar.

```bash
export DOCKER_HOST=localhost:2374
```

Merhaba Docker Swarm hazır toorun Docker hizmetlerini sunulmuştur.


## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Adlı bir dosya oluşturun `azure-vote.yaml` ve kopyalama hello aşağıdaki içerik içine.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Merhaba çalıştırmak [docker yığın dağıtmak](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure oy hizmet komutu.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Çıktı:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Kullanım hello [docker yığın ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) komut tooreturn hello hello uygulama dağıtım durumu.

```bash
docker stack ps azure-vote
```

Bir kez hello `CURRENT STATE` her hizmetidir `Running`, Merhaba uygulaması hazır.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Merhaba uygulamayı test etme

Toohello hello Swarm aracı havuzu tootest hello Azure oy uygulama çıkışı FQDN'sini göz atın.

![TooAzure oy göz atma görüntüsü](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Kümeyi silme
Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Merhaba kod alın

Bu Hızlı Başlangıç, önceden oluşturulmuş kapsayıcı görüntüleri kullanılan toocreate Docker hizmet olmuştur. uygulama kodu, Dockerfile, Hello ilgili ve oluşturma dosya Github'da bulunmaktadır.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Sonraki adımlar

Bu Hızlı Başlangıç, Docker Swarm kümesi dağıtılan ve çok kapsayıcı uygulama tooit dağıtılır.

Docker sıcak Visual Studio Team Services ile tümleştirme hakkında toolearn toohello CI/CD Docker Swarm ve VSTS ile devam edin.

> [!div class="nextstepaction"]
> [Docker Swarm ve VSTS ile CI/CD](./container-service-docker-swarm-setup-ci-cd.md)
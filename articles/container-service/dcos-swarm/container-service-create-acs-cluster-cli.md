---
title: "aaaDeploy Docker kapsayıcısı küme - Azure CLI | Microsoft Docs"
description: "Bir Kubernetes, DC/OS veya Docker Swarm çözümünü, Azure CLI 2.0 kullanarak Azure Container Service’e dağıtın"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>Barındırma çözümünüzü Hello Azure CLI 2.0 kullanarak bir Docker kapsayıcısı dağıtma

Kullanım hello `az acs` komutları hello Azure CLI 2.0 toocreate ve Azure kapsayıcı hizmeti kümelerde yönetin. Hello kullanarak Azure kapsayıcı hizmeti kümesi dağıtabilirsiniz [Azure portal](container-service-deployment.md) veya Azure kapsayıcı hizmeti API'leri hello.

İlgili Yardım `az acs` komutlar geçmesi hello `-h` parametresi tooany komutu. Örneğin: `az acs create -h`.



## <a name="prerequisites"></a>Ön koşullar
bir Azure kapsayıcı hizmeti kümesi kullanarak toocreate Merhaba Azure CLI 2.0, şunları yapmalısınız:
* bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/))
* yüklü ve hello ayarlanmış olması [Azure CLI 2.0](/cli/azure/install-az-cli2)

## <a name="get-started"></a>başlarken 
### <a name="log-in-tooyour-account"></a>Tooyour hesabında oturum
```azurecli
az login 
```

Merhaba istemleri toolog etkileşimli olarak izleyin. İçin diğer yöntemleri toolog içinde bkz [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-az-cli2).

### <a name="set-your-azure-subscription"></a>Azure aboneliğinizi ayarlama

Birden fazla Azure aboneliğiniz varsa, hello varsayılan abonelik ayarlayın. Örneğin:

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Her küme için bir kaynak grubu oluşturmanız önerilir. Azure Container Service’in [kullanılabilir](https://azure.microsoft.com/en-us/regions/services/) olduğu bir Azure bölgesi belirtin. Örneğin:

```azurecli
az group create -n acsrg1 -l "westus"
```
Çıktı benzer toohello aşağıda verilmiştir:

![Kaynak grubu oluşturma](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Azure Container Service Kümesi oluşturma

toocreate bir küme kullanın `az acs create`.
Merhaba küme için ad ve hello hello önceki adımda oluşturduğunuz hello kaynak grubunun adını zorunlu parametreleridir. 

Diğer girdileridir kümesi toodefault değerleri (ekran aşağıdaki hello bakın) kendi ilgili anahtarları kullanma üzerine sürece. Örneğin, hello orchestrator varsayılan tooDC/işletim sistemi tarafından ayarlanır. Ve bir belirtmezseniz, bir DNS adı ön ekini hello küme adına göre oluşturulur.

![az acs create usage](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>Varsayılan değerleri kullanarak hızlı `acs create`
Bir SSH RSA ortak anahtar dosyanız varsa `id_rsa.pub` hello varsayılan konumuna (veya biri için oluşturulan [OS X ve Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../../virtual-machines/linux/ssh-from-windows.md)), hello aşağıdaki gibi bir komutu kullanın:

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
SSH ortak anahtarınız yoksa, bu ikinci komutu kullanın. Bu komutla hello `--generate-ssh-keys` sizin için bir anahtar oluşturur.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

Merhaba komutu girdikten sonra oluşturulan hello küme toobe için yaklaşık 10 dakika bekleyin. Merhaba komutu çıktısı hello ana Aracısı düğümleri ve bir SSH komutu tooconnect toohello ilk ana tam etki alanı adlarını (FQDN) içerir. Kısaltılmış çıktı şu şekildedir:

![ACS oluşturma görüntüsü](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> Merhaba [Kubernetes izlenecek](../kubernetes/container-service-kubernetes-walkthrough.md) gösterir nasıl toouse `az acs create` varsayılan değerleri toocreate bir Kubernetes küme.
>

## <a name="manage-acs-clusters"></a>ACS kümelerini yönetme

Ek kullanım `az acs` toomanage kümenizi komutları. Bazı örnekler aşağıda verilmiştir.

### <a name="list-clusters-under-a-subscription"></a>Bir abonelik altındaki kümeleri listeleme

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>Bir kaynak grubundaki kümeleri listeleme

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>Bir kapsayıcı hizmeti kümesinin ayrıntılarını görüntüleme

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>Ölçek hello küme
Aracı düğümlerinde hem ölçek artırma hem de ölçek azaltma yapılabilir. parametre hello `new-agent-count` hello yeni hello ACS kümedeki aracıları sayısıdır.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>Kapsayıcı hizmeti kümesini silme
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
Bu komut hello kapsayıcı hizmeti oluşturulurken oluşturulan tüm kaynaklar (Ağ ve depolama) silmez. toodelete tüm kaynakları ayrı kaynak grubundaki her küme dağıttığınız kolayca tavsiye edilir. Ardından, Hello küme artık gerekli olmadığında hello kaynak grubunu silin.

## <a name="next-steps"></a>Sonraki adımlar
Artık çalışan bir kümeniz olduğuna göre, bağlantı ve yönetim ayrıntıları için aşağıdaki belgelere bakın:

* [Tooan Azure kapsayıcı hizmeti kümesine bağlanma](../container-service-connect.md)
* [Azure Container Service ve DC/OS ile çalışma](container-service-mesos-marathon-rest.md)
* [Azure Container Service ve Docker Swarm ile çalışma](container-service-docker-swarm.md)
* [Azure Container Service ve Kubernetes ile çalışma](../kubernetes/container-service-kubernetes-walkthrough.md)
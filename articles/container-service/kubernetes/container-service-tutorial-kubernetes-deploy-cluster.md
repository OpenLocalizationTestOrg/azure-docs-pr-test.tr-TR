---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - küme dağıtma | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - küme dağıtma"
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesini dağıtma

Kubernetes kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar. Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır Kubernetes kümenin sağlama. Bu öğreticide, 7, 3 parçası Azure kapsayıcı hizmeti Kubernetes küme dağıtılır. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Kubernetes ACS kümesini dağıtma
> * Merhaba Kubernetes CLI (kubectl) yükleme
> * Kubectl yapılandırması

Sonraki öğreticilerde, Azure uygulama oy toohello küme, ölçeği, dağıtılan hello güncelleştirildi ve Operations Management Suite yapılandırılmış toomonitor hello Kubernetes kümedir.

## <a name="before-you-begin"></a>Başlamadan önce

Önceki öğreticileri, bir kapsayıcı görüntüsü oluşturuldu ve tooan Azure kapsayıcı kayıt defteri örneği karşıya. Bu adımları yapmadıysanız ve boyunca toofollow istersiniz, çok dönmek[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Kubernetes kümesi oluşturma

Merhaba, [önceki öğretici](./container-service-tutorial-kubernetes-prepare-acr.md), bir kaynak grubu *myResourceGroup* oluşturuldu. Bunu yapmadıysanız şimdi bu kaynak grubu oluşturun.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu. 

Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Birkaç dakika sonra hello komutu tamamlandıktan ve hello ACS dağıtımı hakkında bilgi döndürür json biçimli.

## <a name="install-hello-kubectl-cli"></a>Merhaba kubectl CLI yükleme

tooconnect toohello Kubernetes küme kullanımı, istemci bilgisayardan [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi. 

Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür. Tooinstall istiyorsanız hello yerel olarak kullanmak [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.

Linux veya macOS çalıştırılıyorsa, sudo ile toorun gerekebilir. Windows üzerinde Kabuk yönetici olarak çalıştır emin olun.

```azurecli-interactive 
az acs kubernetes install-cli 
```

Windows hello varsayılan yüklemedir *c:\program files (x86)\kubectl.exe*. Bu dosya toohello Windows yolu tooadd gerekebilir. 

## <a name="connect-with-kubectl"></a>kubectl ile bağlanma

tooconfigure `kubectl` tooconnect tooyour Kubernetes küme hello çalıştırmak, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

Merhaba çalıştırmak tooverify hello bağlantı tooyour küme, [kubectl alma düğümleri](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.

```azurecli-interactive
kubectl get nodes
```

Çıktı:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Eğitmen tamamlandığında, bir ACS Kubernetes küme iş yükleri için hazır olması. Sonraki öğreticilerde, birden çok kapsayıcı uygulama çıkışı ölçeği, güncelleştirilmiş ve izlenen dağıtılan toothis kümesidir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure kapsayıcı hizmeti Kubernetes küme dağıtıldı. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Bir Kubernetes ACS kümesi dağıtılmış
> * Yüklü hello Kubernetes CLI (kubectl)
> * Yapılandırılmış kubectl

Uygulama hello kümede çalışan hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Kubernetes uygulamasında dağıtma](./container-service-tutorial-kubernetes-deploy-application.md)

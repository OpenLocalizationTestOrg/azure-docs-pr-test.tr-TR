---
title: "Azure kapsayıcı hizmeti Öğreticisi - küme dağıtma | Microsoft Docs"
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
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesini dağıtma

Kubernetes kapsayıcılı uygulamaları için Dağıtılmış bir platform sağlar. Azure kapsayıcı hizmeti ile basit ve hızlı bir üretim hazır Kubernetes kümenin sağlama. Bu öğreticide, 7, 3 parçası Azure kapsayıcı hizmeti Kubernetes küme dağıtılır. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Kubernetes ACS kümesini dağıtma
> * Kubernetes CLI (kubectl) yükleme
> * Kubectl yapılandırması

Sonraki öğreticilerde, Azure oy uygulama olduğundan kümeye dağıtılan, ölçeği, güncelleştirilmiş ve Operations Management Suite Kubernetes küme izlemek için yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Önceki eğitimlerine bir kapsayıcı görüntüsü oluşturuldu ve Azure kapsayıcı kayıt defteri örneğine yüklenir. Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Kubernetes kümesi oluşturma

İçinde [önceki öğretici](./container-service-tutorial-kubernetes-prepare-acr.md), bir kaynak grubu *myResourceGroup* oluşturuldu. Bunu yapmadıysanız şimdi bu kaynak grubu oluşturun.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Azure Container Service'te [az acs create](/cli/azure/acs#create) komutuyla Kubernetes kümesi oluşturun. 

Aşağıdaki örnekte, bir Linux ana düğümü ve üç Linux aracı düğümüyle *myK8sCluster* adlı bir küme oluşturulmuştur.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Birkaç dakika sonra komutu tamamlandıktan ve ACS dağıtımı hakkında bilgi döndürür json biçimli.

## <a name="install-the-kubectl-cli"></a>CLI kubectl yükleyin

İstemci bilgisayarından Kubernetes kümeye bağlanmak için [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), Kubernetes komut satırı istemcisi. 

Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür. Yerel olarak yüklemek istiyorsanız, kullanmak [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.

Linux veya macOS çalıştırılıyorsa, sudo çalıştırmanız gerekebilir. Windows üzerinde Kabuk yönetici olarak çalıştır emin olun.

```azurecli-interactive 
az acs kubernetes install-cli 
```

Windows, varsayılan yüklemedir *c:\program files (x86)\kubectl.exe*. Bu dosyayı Windows yoluna eklemeniz gerekebilir. 

## <a name="connect-with-kubectl"></a>kubectl ile bağlanma

`kubectl` öğesini Kubernetes kümenize bağlanacak şekilde yapılandırmak için [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) komutunu çalıştırın.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

Kümenize bağlantıyı doğrulamak için Çalıştır [kubectl alma düğümleri](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu.

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

Eğitmen tamamlandığında, bir ACS Kubernetes küme iş yükleri için hazır olması. Sonraki öğreticilerde, bir çok kapsayıcı uygulama bu kümeye dağıtılan, çıkışı ölçeği, güncelleştirilmiş ve izlenen.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure kapsayıcı hizmeti Kubernetes küme dağıtıldı. Aşağıdaki adımlar tamamlandı:

> [!div class="checklist"]
> * Bir Kubernetes ACS kümesi dağıtılmış
> * Kubernetes CLI (kubectl) yüklü
> * Yapılandırılmış kubectl

Uygulama küme üzerinde çalışan hakkında bilgi edinmek için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [Kubernetes uygulamasında dağıtma](./container-service-tutorial-kubernetes-deploy-application.md)

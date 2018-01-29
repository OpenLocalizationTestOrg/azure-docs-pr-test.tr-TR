---
title: "Azure Öğreticisi - güncelleştirme küme üzerinde Kubernetes"
description: "Azure Öğreticisi - güncelleştirme küme üzerinde Kubernetes"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5fd9a1890c1940cdd4e79cc32e0b3984edd043e8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="upgrade-kubernetes-in-azure-container-service-aks"></a>Azure kapsayıcı Hizmeti'nde (AKS) yükseltme Kubernetes

Azure CLI kullanarak Azure kapsayıcı hizmeti (AKS) küme yükseltilebilir. Yükseltme işlemi sırasında Kubernetes düğümleri dikkatle olan [cordoned ve boşaltmış] [ kubernetes-drain] çalışan uygulamalar engellemeyi en aza indirmek için.

Bu öğreticide sekiz sekizlisi kısım, Kubernetes küme yükseltilir. Tamamlamanız görevler aşağıdakileri içerir:

> [!div class="checklist"]
> * Geçerli ve kullanılabilir Kubernetes sürümleri tanımlayın
> * Kubernetes düğümleri yükseltin
> * Başarılı bir yükseltme doğrula

## <a name="before-you-begin"></a>Başlamadan önce

Önceki eğitimlerine bir uygulama bir kapsayıcı görüntü, Azure kapsayıcı kayıt defterine karşıya bu görüntü ve oluşturulan Kubernetes küme paketlenmiştir. Uygulama sonra Kubernetes kümede çalıştırıldı.

Bu adımları yapmadıysanız ve izlemek istediğiniz, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri][aks-tutorial-prepare-app].


## <a name="get-cluster-versions"></a>Küme sürümlerindeki Al

Bir kümeyi yükseltmeden önce, `az aks get-versions` komutunu kullanarak hangi Kubernetes sürümlerinin yükseltme için kullanılabilir olduğunu öğrenin.

```azurecli-interactive
az aks get-versions --name myK8sCluster --resource-group myResourceGroup --output table
```

Burada, geçerli düğüm sürümü olduğunu görebilirsiniz `1.7.7` ve bu sürüm `1.7.9`, `1.8.1`, ve `1.8.2` kullanılabilir.

```
Name     ResourceGroup    MasterVersion    MasterUpgrades       NodePoolVersion     NodePoolUpgrades
-------  ---------------  ---------------  -------------------  ------------------  -------------------
default  myAKSCluster     1.7.7            1.8.2, 1.7.9, 1.8.1  1.7.7               1.8.2, 1.7.9, 1.8.1
```

## <a name="upgrade-cluster"></a>Küme yükseltme

Kullanım `az aks upgrade` komutu küme düğümlerini yükseltin. Aşağıdaki örnekler küme sürüme güncelleştirir `1.8.2`.

```azurecli-interactive
az aks upgrade --name myK8sCluster --resource-group myResourceGroup --kubernetes-version 1.8.2
```

Çıktı:

```json
{
  "id": "/subscriptions/4f48eeae-9347-40c5-897b-46af1b8811ec/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myK8sCluster",
  "location": "eastus",
  "name": "myK8sCluster",
  "properties": {
    "accessProfiles": {
      "clusterAdmin": {
        "kubeConfig": "..."
      },
      "clusterUser": {
        "kubeConfig": "..."
      }
    },
    "agentPoolProfiles": [
      {
        "count": 1,
        "dnsPrefix": null,
        "fqdn": null,
        "name": "myK8sCluster",
        "osDiskSizeGb": null,
        "osType": "Linux",
        "ports": null,
        "storageProfile": "ManagedDisks",
        "vmSize": "Standard_D2_v2",
        "vnetSubnetId": null
      }
    ],
    "dnsPrefix": "myK8sClust-myResourceGroup-4f48ee",
    "fqdn": "myk8sclust-myresourcegroup-4f48ee-406cc140.hcp.eastus.azmk8s.io",
    "kubernetesVersion": "1.8.2",
    "linuxProfile": {
      "adminUsername": "azureuser",
      "ssh": {
        "publicKeys": [
          {
            "keyData": "..."
          }
        ]
      }
    },
    "provisioningState": "Succeeded",
    "servicePrincipalProfile": {
      "clientId": "e70c1c1c-0ca4-4e0a-be5e-aea5225af017",
      "keyVaultSecretRef": null,
      "secret": null
    }
  },
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "type": "Microsoft.ContainerService/ManagedClusters"
}
```

## <a name="validate-upgrade"></a>Yükseltme doğrula

Artık `az aks show` komutuyla yükseltmenin başarılı olup olmadığını doğrulayabilirsiniz.

```azurecli-interactive
az aks show --name myK8sCluster --resource-group myResourceGroup --output table
```

Çıktı:

```json
Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------------
myK8sCluster  eastus     myResourceGroup  1.8.2                Succeeded            myk8sclust-myresourcegroup-3762d8-2f6ca801.hcp.eastus.azmk8s.io
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir AKS küme Kubernetes yükseltilmiştir. Aşağıdaki görevler tamamlandı:

> [!div class="checklist"]
> * Geçerli ve kullanılabilir Kubernetes sürümleri tanımlayın
> * Kubernetes düğümleri yükseltin
> * Başarılı bir yükseltme doğrula

AKS hakkında daha fazla bilgi için bu bağlantıyı izleyin.

> [!div class="nextstepaction"]
> [AKS genel bakış][aks-intro]

<!-- LINKS - external -->
[kubernetes-drain]: https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/

<!-- LINKS - internal -->
[aks-intro]: ./intro-kubernetes.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
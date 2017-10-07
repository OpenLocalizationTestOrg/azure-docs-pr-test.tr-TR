---
title: "aaaQuickstart - Windows için Azure Kubernetes küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate bir Kubernetes kümesi için Windows hello Azure CLI ile Azure kapsayıcı hizmeti kapsayıcı öğrenin."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Windows kapsayıcıları için Kubernetes kümesi dağıtma

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntılarını bir [Kubernetes](https://kubernetes.io/docs/home/) kümesi [Azure kapsayıcı hizmeti](../container-service-intro.md). Merhaba küme dağıtıldıktan sonra Kubernetes hello ile tooit bağlanmak `kubectl` komut satırı aracı ve dağıtmak, ilk Windows kapsayıcı.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

> [!NOTE]
> Azure Container Service'te Kubernetes için Windows kapsayıcıları desteği önizleme aşamasındadır. 
>

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Kubernetes kümesi oluşturma
Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu. 

Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğüm ve iki Windows aracı düğümü. Bu örnek SSH anahtarları gerekli tooconnect toohello Linux ana oluşturur. Bu örnekte *azureuser* bir yönetici kullanıcı adı ve *myPassword12* hello parolasını hello Windows düğümlerinde olarak. Bu değerleri toosomething uygun tooyour ortamı güncelleştirin. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Birkaç dakika sonra hello komut tamamlandıktan ve dağıtımınız hakkında bilgi gösterir.

## <a name="install-kubectl"></a>Kubectl yükleyin

tooconnect toohello Kubernetes küme kullanımı, istemci bilgisayardan [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi. 

Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür. Tooinstall isterseniz, yerel olarak kullanabileceğiniz hello [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.

Azure CLI örnek yükler aşağıdaki hello `kubectl` tooyour sistem. Windows'da bu komutu yönetici olarak çalıştırın.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>kubectl ile bağlanma

tooconfigure `kubectl` tooconnect tooyour Kubernetes küme hello çalıştırmak, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu. Merhaba aşağıdaki örnek Kubernetes kümenizin hello küme yapılandırmasını indirir.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello bağlantı tooyour küme makinenizden, çalıştırmayı deneyin:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Hello Yöneticisi ve Aracısı düğümleri listeler.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Windows IIS kapsayıcısı dağıtma

Bir veya daha fazla kapsayıcı içeren bir Kubernetes *pod*'unun içinde Docker kapsayıcısı çalıştırabilirsiniz. 

Bu temel örnek bir JSON dosyası toospecify Microsoft Internet Information Server (IIS) kapsayıcı kullanır ve ardından hello kullanarak hello pod oluşturur `kubctl apply` komutu. 

Adlı bir yerel dosya oluşturma `iis.json` ve kopyalama hello aşağıdaki metin. Bu dosya, bir ortak kapsayıcı görüntüsünü kullanarak Windows Server 2016 Nano Server üzerinde Kubernetes toorun IIS söyler [Docker hub'a](https://hub.docker.com/r/nanoserver/iis/). Merhaba kapsayıcı 80 numaralı bağlantı noktasını kullanır, ancak başlangıçta yalnızca hello küme ağdan erişilebilir.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello pod, türü:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

tootrack hello dağıtım türü:
  
```azurecli-interactive
kubectl get pods
```

Merhaba pod dağıtma sırasında hello durumudur `ContainerCreating`. Merhaba kapsayıcı tooenter hello birkaç dakika sürebilir `Running` durumu.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Görünüm hello IIS Karşılama sayfası

tooexpose hello pod toohello dünyayla komutu aşağıdaki türü hello bir ortak IP adresi:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Bu komutla bir hizmet Kubernetes oluşturur ve bir [Azure yük dengeleyici kuralı](container-service-kubernetes-load-balancing.md) hello hizmeti için genel IP adresine sahip. 

Komut toosee hello hello hizmetinin durumunu izleyen hello çalıştırın.

```azurecli-interactive
kubectl get svc
```

Başlangıç IP adresi başlangıçta görünür `pending`. Birkaç dakika sonra hello dış IP adresi hello `iis` pod ayarlanır:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Merhaba dış IP adresinde seçim toosee hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz:

![TooIIS göz atma görüntüsü](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Kümeyi silme
Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta, `kubectl` bağlantılı bir Kubernetes kümesi ve IIS kapsayıcısı ile birlikte bir pod dağıttınız. Azure kapsayıcı hizmeti hakkında daha fazla toolearn toohello Kubernetes öğretici devam edin.

> [!div class="nextstepaction"]
> [ACS Kubernetes kümesini yönetme](container-service-tutorial-kubernetes-prepare-app.md)

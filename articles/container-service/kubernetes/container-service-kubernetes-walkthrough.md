---
title: "aaaQuickstart - Linux Azure Kubernetes küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate Kubernetes küme hello Azure CLI ile Azure kapsayıcı Hizmeti'nde Linux kapsayıcıları için öğrenin."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Linux kapsayıcıları için Kubernetes kümesi dağıtma

Bu Hızlı Başlangıç, Kubernetes küme hello Azure CLI kullanarak dağıtılır. Web ön uç ve bir Redis örneği oluşan çok kapsayıcı uygulama sonra dağıtılan ve hello kümede çalıştırın. Tamamlandığında, Merhaba uygulaması üzerinden erişilebilen Internet hello. 

Bu belgede kullanılan Merhaba örnek uygulaması Python içinde yazılmış olmalıdır. Merhaba kavramlar ve burada ayrıntılı adımlar herhangi bir kapsayıcısına görüntü Kubernetes kümesine kullanılan toodeploy olabilir. Merhaba kodu, Dockerfile ve önceden oluşturulmuş Kubernetes bildirim dosyaları ilgili toothis proje kullanılabilir [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![TooAzure oy göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)

Bu hızlı başlangıç Kubernetes kavramları temel bir anlayış varsayar, hello Kubernetes hakkında ayrıntılı bilgi için bkz: [Kubernetes belgelerine]( https://kubernetes.io/docs/home/).

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Çıktı:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Kubernetes kümesi oluşturma

Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu. Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Birkaç dakika sonra hello komut tamamlandıktan ve biçimlendirilmiş json hello kümesi hakkında bilgi verir. 

## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın

toomanage Kubernetes küme kullanmak [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi. 

Azure CloudShell kullanıyorsanız kubectl zaten yüklüdür. Tooinstall isterseniz, yerel olarak kullanabileceğiniz hello [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.

Merhaba çalıştırmak tooconfigure kubectl tooconnect tooyour Kubernetes küme, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu. Bu adım kimlik bilgileri indirmeleri ve hello Kubernetes CLI toouse yapılandırır bunları.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello bağlantı tooyour küme, kullanım hello [kubectl almak](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu tooreturn hello küme düğümlerinin bir listesi.

```azurecli-interactive
kubectl get nodes
```

Çıktı:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Kubernetes bildirim dosyası kapsayıcı görüntüleri çalıştırma dahil hello küme için istenen bir durum tanımlar. Bu örnekte, bir bildirim tüm nesneleri toorun Azure oy uygulama hello kullanılan toocreate ' dir. 

Adlı bir dosya oluşturun `azure-vote.yml` kopyalayıp içine hello YAML. Azure Cloud Shell'de çalışıyorsanız, bu dosya bir sanal veya fiziksel sistemde olduğu gibi vi veya Nano kullanılarak oluşturulabilir.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Kullanım hello [kubectl oluşturma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun Merhaba uygulaması komutu.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Çıktı:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Merhaba uygulamayı test etme

Merhaba uygulaması çalıştırılırken bir [Kubernetes hizmet](https://kubernetes.io/docs/concepts/services-networking/service/) düzenlemenizi sağlayan uygulama ön uç toohello hello oluşturulan Internet. Bu işlem birkaç dakika toocomplete alabilir. 

toomonitor ilerleme, kullanım hello [kubectl alma hizmeti](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) hello komutunu `--watch` bağımsız değişkeni.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Başlangıçta hello **dış IP** hello için *azure oy ön* hizmeti görünür olarak *bekleyen*. Merhaba dış IP adresi değiştiğinden sonra *bekleyen* tooan *IP adresi*, kullanın `CTRL-C` toostop hello kubectl izleme işlemi. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Toohello dış IP adresi toosee hello Azure oylama uygulaması gözatabilirsiniz.

![TooAzure oy göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Kümeyi silme
Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Merhaba kod alın

Bu Hızlı Başlangıç, önceden oluşturulmuş kapsayıcı görüntüleri kullanılan toocreate Kubernetes dağıtım silinmiş. uygulama kodu, Dockerfile, Hello ilgili ve Kubernetes bildirim dosyası Github'da bulunmaktadır.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç Kubernetes küme dağıtılan ve çok kapsayıcı uygulama tooit dağıtılır. 

Azure kapsayıcı hizmeti ve tam bir kod toodeployment örnek aracılığıyla ilerlemesi hakkında daha fazla toolearn toohello Kubernetes küme öğretici devam edin.

> [!div class="nextstepaction"]
> [ACS Kubernetes kümesini yönetme](./container-service-tutorial-kubernetes-prepare-app.md)

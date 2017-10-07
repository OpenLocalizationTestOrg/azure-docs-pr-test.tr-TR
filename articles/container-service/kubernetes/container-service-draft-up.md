---
title: "Azure kapsayıcı hizmeti ve Azure kapsayıcı kayıt defteri ile taslak aaaUse | Microsoft Docs"
description: "Bir ACS Kubernetes kümesi ve bir Azure kapsayıcı kayıt defteri toocreate taslak ile azure'da ilk uygulamanızı oluşturun."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, Kapsayıcılar, mikro hizmetler, Kubernetes, Draft, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Azure kapsayıcı hizmeti ve Azure kapsayıcı kayıt defteri toobuild ile taslak kullanın ve bir uygulama tooKubernetes dağıtma

[Taslak](https://aka.ms/draft) kolay toodevelop kapsayıcı tabanlı uygulamalar kolaylaştıran yeni bir açık kaynak aracıdır ve bunları çok Docker ve Kubernetes--hakkında bilmek veya hatta bunları yükleme tooKubernetes kümeleri dağıtabilirsiniz. Taslak gibi araçları kullanarak ve takımlar odağınız olanak Kubernetes ile Merhaba uygulaması oluşturma, kadar dikkat tooinfrastructure ödeme değil.

Draft’ı yerel kullanım dahil olmak üzere herhangi bir Docker görüntü kayıt defteri ve herhangi bir Kubernetes kümesiyle kullanabilirsiniz. Bu öğretici toouse ACS Kubernetes, ACR ve Azure DNS toocreate ile canlı CI/CD Geliştirici nasıl kanal taslak kullanarak gösterir.


## <a name="create-an-azure-container-registry"></a>Azure Container Registry oluşturma
Kolayca [yeni bir Azure kapsayıcı kayıt](../../container-registry/container-registry-get-started-azure-cli.md), ancak hello adımlar aşağıdaki gibidir:

1. Bir Azure kaynak grubu toomanage ACS ACR kayıt defteri ve hello Kubernetes kümenizi oluşturun.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Şu komutu kullanarak bir ACR görüntü kayıt defteri oluşturun: [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Kubernetes ile Azure Container Service oluşturma

Yaptığınız artık hazır toouse [az acs oluşturma](/cli/azure/acs#create) Kubernetes hello kullanarak bir ACS toocreate küme `--orchestrator-type` değeri.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Kubernetes hello varsayılan orchestrator türü olmadığından hello kullandığınızdan emin olun `--orchestrator-type kubernetes` geçin.

Merhaba çıkış başarılı olduğunda benzer toohello aşağıdaki görünür.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Bir kümeye sahip olduğunuza göre hello kullanarak hello kimlik bilgileri içe aktarabilirsiniz [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu. Şimdi ne Helm ve taslak tooget işlerini gerekiyor kümeniz için yerel yapılandırma dosyasına sahip.

## <a name="install-and-configure-draft"></a>Draft’ı yükleme ve yapılandırma
Merhaba yükleme yönergeleri için taslak olan hello [taslak depo](https://github.com/Azure/draft/blob/master/docs/install.md). Görece basit ancak bağımlı gibi bazı yapılandırmalar gerektirir [Helm](https://aka.ms/helm) toocreate ve Helm grafik hello Kubernetes kümesine dağıtabilirsiniz.

1. [Helm’i indirip yükleyin](https://aka.ms/helm#install).
2. Helm toosearch için kullanır ve yüklerseniz `stable/traefik`ve istekleri derlemeleriniz için gelen giriş denetleyicisi tooenable.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Bir izleme üzerinde hello kümesini şimdi `ingress` dağıtıldığında denetleyicisi toocapture hello dış IP değeri. Bu IP adresinin bir hello olacak [tooyour dağıtım etki alanı eşlenen](#wire-up-deployment-domain) hello sonraki bölümde.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    Merhaba dağıtım etki alanı için bu durumda, dış IP hello `13.64.108.240`. Şimdi, etki alanı toothat IP eşleyebilirsiniz.

## <a name="wire-up-deployment-domain"></a>Dağıtım etki alanının bağlantılarını ayarlama

Draft, oluşturduğu her Helm grafiği (üzerinde çalıştığınız her uygulama) için bir yayın oluşturur. Her biri taslak olarak tarafından kullanılan oluşturulan bir ad alır bir _alt etki alanı_ hello kök üstünde _dağıtım etki alanı_ , sizin denetlediğiniz. (Bu örnekte, kullandığımız `squillace.io` olarak hello dağıtım etki alanı) tooenable bu alt etki alanı davranışı için bir A kaydı oluşturmanız gerekir `'*'` dağıtım etki alanınız için DNS girdiler, alt etki alanı yönlendirilmiş toohello Kubernetes olarak, böylelikle her oluşturulan kümenin giriş denetleyicisi.

Kendi etki alanı sağlayıcı kendi yolu tooassign DNS sunucularını; yine de sahip istiyor musunuz? çok[, etki alanı nameservers tooAzure DNS temsilci](../../dns/dns-delegate-domain-azure-dns.md), hello aşağıdaki adımları gerçekleştirin:

1. Bölgeniz için bir kaynak grubu oluşturun.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Etki alanınız için bir DNS bölgesi oluşturun.
Kullanım hello [az ağ dns bölgesi oluşturma](/cli/azure/network/dns/zone#create) tooobtain hello nameservers toodelegate DNS etki alanınız için DNS tooAzure kontrol komutu.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. İstediğiniz etki alanınızın, toouse Azure DNS toorepoint sağlayan dağıtım etki alanınız için toohello etki alanı sağlayıcısı verilen hello DNS sunucularını ekleyin.
4. Dağıtım etki alanı eşleme toohello için bir A kayıt kümesi girişi oluşturmak `ingress` IP hello önceki bölümde, adım 2.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
Merhaba çıktı şöyle görünür:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Taslak toouse, kayıt defterini yapılandırın ve oluşturduğu her Helm grafik alt etki alanları oluşturun. tooconfigure Taslak, şunlar gerekir:
  - Azure Container Registry adınız (bu örnekte `draft` kullanılmıştır)
  - `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"` dosyasından kayıt defteri anahtarınız veya parolanız.
  - Merhaba kök dağıtım toomap toohello Kubernetes giriş dış IP adresi yapılandırılmış etki alanının (burada, `squillace.io`)

  Çağrı `draft init` ve hello yapılandırma işlemi için hello değerleri yukarıdaki ister. Merhaba aşağıdaki ilk defa çalıştırmadan hello hello işlem bir şey görülüyor.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Şimdi hazır toodeploy uygulamanın demektir.


## <a name="build-and-deploy-an-application"></a>Uygulama oluşturma ve dağıtma

Merhaba taslak bağlantıların bulunması olan [altı basit bir örnek uygulamaları](https://github.com/Azure/draft/tree/master/examples). Merhaba depoyu kopyalama ve hello kullanalım [Python örnek](https://github.com/Azure/draft/tree/master/examples/python). Merhaba örnekler/Python dizin ve türünü değiştirme `draft create` toobuild Merhaba uygulaması. Merhaba örnek aşağıdaki gibi görünmelidir.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

Merhaba çıktı, bir Dockerfile ve Helm grafik içerir. toobuild ve dağıtmak için yalnızca yazın `draft up`. Merhaba çıkış kapsamlıdır, ancak aşağıdaki örneğine hello gibi başlar.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

ne zaman ve benzeri toohello aşağıdaki örneğine başarılı biter.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Grafiğin adı ne olursa olsun, artık `curl http://gangly-bronco.squillace.io` tooreceive hello yanıt `Hello World!`.

## <a name="next-steps"></a>Sonraki adımlar

Bir ACS Kubernetes küme sahip olduğunuza göre kullanarak araştırabilirsiniz [Azure kapsayıcı kayıt defteri](../../container-registry/container-registry-intro.md) toocreate bu senaryo hakkında daha fazla ve farklı dağıtımları. Örneğin, belirli ACS dağıtımları için ayarları daha derin bir alt etki alanından denetleyen bir draft._basedomain.toplevel_ etki alanı DNS kayıt kümesi oluşturabilirsiniz.







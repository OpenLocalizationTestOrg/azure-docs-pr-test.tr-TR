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
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="6996d-104">Azure kapsayıcı hizmeti ve Azure kapsayıcı kayıt defteri toobuild ile taslak kullanın ve bir uygulama tooKubernetes dağıtma</span><span class="sxs-lookup"><span data-stu-id="6996d-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="6996d-105">[Taslak](https://aka.ms/draft) kolay toodevelop kapsayıcı tabanlı uygulamalar kolaylaştıran yeni bir açık kaynak aracıdır ve bunları çok Docker ve Kubernetes--hakkında bilmek veya hatta bunları yükleme tooKubernetes kümeleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="6996d-106">Taslak gibi araçları kullanarak ve takımlar odağınız olanak Kubernetes ile Merhaba uygulaması oluşturma, kadar dikkat tooinfrastructure ödeme değil.</span><span class="sxs-lookup"><span data-stu-id="6996d-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="6996d-107">Draft’ı yerel kullanım dahil olmak üzere herhangi bir Docker görüntü kayıt defteri ve herhangi bir Kubernetes kümesiyle kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="6996d-108">Bu öğretici toouse ACS Kubernetes, ACR ve Azure DNS toocreate ile canlı CI/CD Geliştirici nasıl kanal taslak kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="6996d-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="6996d-109">Azure Container Registry oluşturma</span><span class="sxs-lookup"><span data-stu-id="6996d-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="6996d-110">Kolayca [yeni bir Azure kapsayıcı kayıt](../../container-registry/container-registry-get-started-azure-cli.md), ancak hello adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6996d-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="6996d-111">Bir Azure kaynak grubu toomanage ACS ACR kayıt defteri ve hello Kubernetes kümenizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6996d-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="6996d-112">Şu komutu kullanarak bir ACR görüntü kayıt defteri oluşturun: [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="6996d-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="6996d-113">Kubernetes ile Azure Container Service oluşturma</span><span class="sxs-lookup"><span data-stu-id="6996d-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="6996d-114">Yaptığınız artık hazır toouse [az acs oluşturma](/cli/azure/acs#create) Kubernetes hello kullanarak bir ACS toocreate küme `--orchestrator-type` değeri.</span><span class="sxs-lookup"><span data-stu-id="6996d-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="6996d-115">Kubernetes hello varsayılan orchestrator türü olmadığından hello kullandığınızdan emin olun `--orchestrator-type kubernetes` geçin.</span><span class="sxs-lookup"><span data-stu-id="6996d-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="6996d-116">Merhaba çıkış başarılı olduğunda benzer toohello aşağıdaki görünür.</span><span class="sxs-lookup"><span data-stu-id="6996d-116">hello output when successful looks similar toohello following.</span></span>

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

<span data-ttu-id="6996d-117">Bir kümeye sahip olduğunuza göre hello kullanarak hello kimlik bilgileri içe aktarabilirsiniz [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu.</span><span class="sxs-lookup"><span data-stu-id="6996d-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="6996d-118">Şimdi ne Helm ve taslak tooget işlerini gerekiyor kümeniz için yerel yapılandırma dosyasına sahip.</span><span class="sxs-lookup"><span data-stu-id="6996d-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="6996d-119">Draft’ı yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6996d-119">Install and configure draft</span></span>
<span data-ttu-id="6996d-120">Merhaba yükleme yönergeleri için taslak olan hello [taslak depo](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="6996d-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="6996d-121">Görece basit ancak bağımlı gibi bazı yapılandırmalar gerektirir [Helm](https://aka.ms/helm) toocreate ve Helm grafik hello Kubernetes kümesine dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="6996d-122">[Helm’i indirip yükleyin](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="6996d-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="6996d-123">Helm toosearch için kullanır ve yüklerseniz `stable/traefik`ve istekleri derlemeleriniz için gelen giriş denetleyicisi tooenable.</span><span class="sxs-lookup"><span data-stu-id="6996d-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="6996d-124">Bir izleme üzerinde hello kümesini şimdi `ingress` dağıtıldığında denetleyicisi toocapture hello dış IP değeri.</span><span class="sxs-lookup"><span data-stu-id="6996d-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="6996d-125">Bu IP adresinin bir hello olacak [tooyour dağıtım etki alanı eşlenen](#wire-up-deployment-domain) hello sonraki bölümde.</span><span class="sxs-lookup"><span data-stu-id="6996d-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="6996d-126">Merhaba dağıtım etki alanı için bu durumda, dış IP hello `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="6996d-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="6996d-127">Şimdi, etki alanı toothat IP eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="6996d-128">Dağıtım etki alanının bağlantılarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="6996d-128">Wire up deployment domain</span></span>

<span data-ttu-id="6996d-129">Draft, oluşturduğu her Helm grafiği (üzerinde çalıştığınız her uygulama) için bir yayın oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6996d-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="6996d-130">Her biri taslak olarak tarafından kullanılan oluşturulan bir ad alır bir _alt etki alanı_ hello kök üstünde _dağıtım etki alanı_ , sizin denetlediğiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="6996d-131">(Bu örnekte, kullandığımız `squillace.io` olarak hello dağıtım etki alanı) tooenable bu alt etki alanı davranışı için bir A kaydı oluşturmanız gerekir `'*'` dağıtım etki alanınız için DNS girdiler, alt etki alanı yönlendirilmiş toohello Kubernetes olarak, böylelikle her oluşturulan kümenin giriş denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6996d-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="6996d-132">Kendi etki alanı sağlayıcı kendi yolu tooassign DNS sunucularını; yine de sahip istiyor musunuz? çok[, etki alanı nameservers tooAzure DNS temsilci](../../dns/dns-delegate-domain-azure-dns.md), hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6996d-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="6996d-133">Bölgeniz için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6996d-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="6996d-134">Etki alanınız için bir DNS bölgesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6996d-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="6996d-135">Kullanım hello [az ağ dns bölgesi oluşturma](/cli/azure/network/dns/zone#create) tooobtain hello nameservers toodelegate DNS etki alanınız için DNS tooAzure kontrol komutu.</span><span class="sxs-lookup"><span data-stu-id="6996d-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
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
3. <span data-ttu-id="6996d-136">İstediğiniz etki alanınızın, toouse Azure DNS toorepoint sağlayan dağıtım etki alanınız için toohello etki alanı sağlayıcısı verilen hello DNS sunucularını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6996d-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="6996d-137">Dağıtım etki alanı eşleme toohello için bir A kayıt kümesi girişi oluşturmak `ingress` IP hello önceki bölümde, adım 2.</span><span class="sxs-lookup"><span data-stu-id="6996d-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="6996d-138">Merhaba çıktı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="6996d-138">hello output looks something like:</span></span>
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

5. <span data-ttu-id="6996d-139">Taslak toouse, kayıt defterini yapılandırın ve oluşturduğu her Helm grafik alt etki alanları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6996d-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="6996d-140">tooconfigure Taslak, şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="6996d-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="6996d-141">Azure Container Registry adınız (bu örnekte `draft` kullanılmıştır)</span><span class="sxs-lookup"><span data-stu-id="6996d-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="6996d-142">`az acr credential show -n <registry name> --output tsv --query "passwords[0].value"` dosyasından kayıt defteri anahtarınız veya parolanız.</span><span class="sxs-lookup"><span data-stu-id="6996d-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="6996d-143">Merhaba kök dağıtım toomap toohello Kubernetes giriş dış IP adresi yapılandırılmış etki alanının (burada, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="6996d-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="6996d-144">Çağrı `draft init` ve hello yapılandırma işlemi için hello değerleri yukarıdaki ister.</span><span class="sxs-lookup"><span data-stu-id="6996d-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="6996d-145">Merhaba aşağıdaki ilk defa çalıştırmadan hello hello işlem bir şey görülüyor.</span><span class="sxs-lookup"><span data-stu-id="6996d-145">hello process looks something like hello following hello first time you run it.</span></span>
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

<span data-ttu-id="6996d-146">Şimdi hazır toodeploy uygulamanın demektir.</span><span class="sxs-lookup"><span data-stu-id="6996d-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="6996d-147">Uygulama oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="6996d-147">Build and deploy an application</span></span>

<span data-ttu-id="6996d-148">Merhaba taslak bağlantıların bulunması olan [altı basit bir örnek uygulamaları](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="6996d-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="6996d-149">Merhaba depoyu kopyalama ve hello kullanalım [Python örnek](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="6996d-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="6996d-150">Merhaba örnekler/Python dizin ve türünü değiştirme `draft create` toobuild Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6996d-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="6996d-151">Merhaba örnek aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="6996d-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="6996d-152">Merhaba çıktı, bir Dockerfile ve Helm grafik içerir.</span><span class="sxs-lookup"><span data-stu-id="6996d-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="6996d-153">toobuild ve dağıtmak için yalnızca yazın `draft up`.</span><span class="sxs-lookup"><span data-stu-id="6996d-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="6996d-154">Merhaba çıkış kapsamlıdır, ancak aşağıdaki örneğine hello gibi başlar.</span><span class="sxs-lookup"><span data-stu-id="6996d-154">hello output is extensive, but begins like hello following example.</span></span>
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

<span data-ttu-id="6996d-155">ne zaman ve benzeri toohello aşağıdaki örneğine başarılı biter.</span><span class="sxs-lookup"><span data-stu-id="6996d-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="6996d-156">Grafiğin adı ne olursa olsun, artık `curl http://gangly-bronco.squillace.io` tooreceive hello yanıt `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="6996d-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6996d-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6996d-157">Next steps</span></span>

<span data-ttu-id="6996d-158">Bir ACS Kubernetes küme sahip olduğunuza göre kullanarak araştırabilirsiniz [Azure kapsayıcı kayıt defteri](../../container-registry/container-registry-intro.md) toocreate bu senaryo hakkında daha fazla ve farklı dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="6996d-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="6996d-159">Örneğin, belirli ACS dağıtımları için ayarları daha derin bir alt etki alanından denetleyen bir draft._basedomain.toplevel_ etki alanı DNS kayıt kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6996d-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>







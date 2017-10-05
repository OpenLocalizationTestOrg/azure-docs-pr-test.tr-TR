---
title: "Draft’ı Azure Container Service ve Azure Container Registry ile kullanma | Microsoft Docs"
description: "Draft ile Azure’da ilk uygulamanızı oluşturmak için bir ACS Kubernetes kümesi ve bir Azure Container Registry oluşturun."
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="90ea1-104">Draft’ı Azure Container Service ve Azure Container Registry ile kullanarak bir uygulama oluşturma ve Kubernetes’e dağıtma</span><span class="sxs-lookup"><span data-stu-id="90ea1-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="90ea1-105">[Draft](https://aka.ms/draft), Docker ve Kubernetes hakkında pek fazla bilginiz olmadan, hatta bunları yüklemeden kapsayıcı tabanlı uygulamalar geliştirmeyi ve bu uygulamaları Kubernetes kümelerine dağıtmayı kolaylaştıran yeni bir açık kaynak araçtır.</span><span class="sxs-lookup"><span data-stu-id="90ea1-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="90ea1-106">Draft gibi araçların kullanılması, sizin ve ekiplerinizin altyapıya eskisi kadar dikkat etmesine gerek kalmadan Kubernetes ile uygulama oluşturmaya odaklanmasına imkan sağlar.</span><span class="sxs-lookup"><span data-stu-id="90ea1-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="90ea1-107">Draft’ı yerel kullanım dahil olmak üzere herhangi bir Docker görüntü kayıt defteri ve herhangi bir Kubernetes kümesiyle kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="90ea1-108">Bu öğreticide, Draft’ı kullanarak canlı bir CI/CD geliştirici işlem hattı oluşturmak amacıyla ACS’nin Kubernetes, ACR ve Azure DNS ile birlikte nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90ea1-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="90ea1-109">Azure Container Registry oluşturma</span><span class="sxs-lookup"><span data-stu-id="90ea1-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="90ea1-110">Kolayca [yeni Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md) oluşturabilirsiniz, ancak adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="90ea1-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="90ea1-111">ACS’de ACR kayıt defterinizi ve Kubernetes kümenizi yönetmek için br Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="90ea1-112">Şu komutu kullanarak bir ACR görüntü kayıt defteri oluşturun: [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="90ea1-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="90ea1-113">Kubernetes ile Azure Container Service oluşturma</span><span class="sxs-lookup"><span data-stu-id="90ea1-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="90ea1-114">Artık [az acs create](/cli/azure/acs#create) komutu ile `--orchestrator-type` değeri olarak Kubernetes’i kullanarak bir ACS kümesi oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="90ea1-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="90ea1-115">Kubernetes varsayılan düzenleyici olmadığından, `--orchestrator-type kubernetes` anahtarını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="90ea1-116">İşlem başarılı olursa çıktı aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="90ea1-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="90ea1-117">Artık bir kümeniz olduğuna göre, [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) komutunu kullanarak kimlik bilgilerini içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="90ea1-118">Artık kümeniz için yerel bir yapılandırma dosyanız vardır ve Helm ile Draft’ın işlerini yapabilmesi için bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="90ea1-119">Draft’ı yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90ea1-119">Install and configure draft</span></span>
<span data-ttu-id="90ea1-120">Draft için yükleme yönergeleri [Draft deposunda](https://github.com/Azure/draft/blob/master/docs/install.md) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="90ea1-121">Bu yönergeler görece basittir, ancak bir Helm oluşturup bunu Kubernetes kümesine dağıtmak için [Helm](https://aka.ms/helm)’e bağımlı olduğundan bazı yapılandırma işlemleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="90ea1-122">[Helm’i indirip yükleyin](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="90ea1-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="90ea1-123">`stable/traefik` aracını bulup yüklemek için Helm’i; derlemelerinize yönelik gelen istekleri etkinleştirmek için giriş denetleyicisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="90ea1-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="90ea1-124">Şimdi, dış IP değeri dağıtıldığında bu değeri yakalaması için `ingress` denetleyicisinde bir izleme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90ea1-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="90ea1-125">Bu IP adresi, bir sonraki bölümde [dağıtım etki alanınızla eşleştirilecek](#wire-up-deployment-domain) adrestir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="90ea1-126">Bu durumda, dağıtım etki alanının dış IP’si şudur: `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="90ea1-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="90ea1-127">Artık etki alanınızı bu IP ile eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="90ea1-128">Dağıtım etki alanının bağlantılarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="90ea1-128">Wire up deployment domain</span></span>

<span data-ttu-id="90ea1-129">Draft, oluşturduğu her Helm grafiği (üzerinde çalıştığınız her uygulama) için bir yayın oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90ea1-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="90ea1-130">Her biri için, sizin denetlediğiniz kök _dağıtım etki alanı_ üzerine bir _alt etki alanı_ olarak taslak tarafından kullanılan bir ad oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="90ea1-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="90ea1-131">(Bu örnekte, dağıtım etki alanı olarak `squillace.io`’yu kullanıyoruz.) Bu alt etki alanı davranışını etkinleştirmek istiyorsanız, oluşturulan her alt etki alanının Kubernetes kümesinin giriş denetleyicisine yönlendirilmesi için dağıtım etki alanınıza yönelik DNS girişlerinizde `'*'` için bir A kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="90ea1-132">Etki alanı sağlayıcınız, DNS sunucularını atamak için kendi yöntemini kullanır; [Azure DNS’yi etki alanı ad sunucularınızın temsilcisi olarak atamak için](../../dns/dns-delegate-domain-azure-dns.md) aşağıdaki adımları gerçekleştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90ea1-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="90ea1-133">Bölgeniz için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="90ea1-134">Etki alanınız için bir DNS bölgesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="90ea1-135">Etki alanınız için Azure DNS’yi DNS denetimi temsilcisi olarak atamak istiyorsanız [az network dns zone create](/cli/azure/network/dns/zone#create) komutunu kullanarak ad sunucularını edinin.</span><span class="sxs-lookup"><span data-stu-id="90ea1-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="90ea1-136">Size döndürülen DNS sunucularını, dağıtım etki alanınızın etki alanı sağlayıcısına ekleyin. Bunu yaptığınızda, Azure DNS’nizi kullanarak etki alanınızı istediğiniz yeri gösterecek şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="90ea1-137">Önceki bölümün 2. adımında `ingress` IP’si ile eşlenen dağıtım etki alanınız için bir A kayıt kümesi girişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="90ea1-138">Çıktı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="90ea1-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="90ea1-139">Draft’ı kayıt defterinizi kullanacak şekilde yapılandırın ve Draft’ın oluşturduğu her Helm grafiği için alt etki alanları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90ea1-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="90ea1-140">Draft’ı yapılandırmak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="90ea1-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="90ea1-141">Azure Container Registry adınız (bu örnekte `draft` kullanılmıştır)</span><span class="sxs-lookup"><span data-stu-id="90ea1-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="90ea1-142">`az acr credential show -n <registry name> --output tsv --query "passwords[0].value"` dosyasından kayıt defteri anahtarınız veya parolanız.</span><span class="sxs-lookup"><span data-stu-id="90ea1-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="90ea1-143">Kubernetes giriş dış IP adresi (burada `squillace.io` kullanılmıştır) ile eşlenecek şekilde yapılandırdığınız kök dağıtım etki alanı</span><span class="sxs-lookup"><span data-stu-id="90ea1-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="90ea1-144">`draft init` çağrısı yaptığınızda, yapılandırma işlemi sizden yukarıdaki değerleri girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="90ea1-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="90ea1-145">İşlem ilk çalıştırıldığında aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="90ea1-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="90ea1-146">Artık uygulama dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="90ea1-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="90ea1-147">Uygulama oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="90ea1-147">Build and deploy an application</span></span>

<span data-ttu-id="90ea1-148">Draft deposunda [altı basit örnek uygulama](https://github.com/Azure/draft/tree/master/examples) yer alır.</span><span class="sxs-lookup"><span data-stu-id="90ea1-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="90ea1-149">Depoyu kopyalayalım ve [Python örneğini](https://github.com/Azure/draft/tree/master/examples/python) kullanalım.</span><span class="sxs-lookup"><span data-stu-id="90ea1-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="90ea1-150">Bulunduğunuz dizini samples/Python olarak değiştirin ve uygulamayı oluşturmak için `draft create` yazın.</span><span class="sxs-lookup"><span data-stu-id="90ea1-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="90ea1-151">Aşağıdaki örnekteki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="90ea1-152">Çıktı bir Docker dosyası ve Helm grafiği içerir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="90ea1-153">Derlemek ve dağıtmak için `draft up` yazmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="90ea1-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="90ea1-154">Çıktı kapsamlıdır, ancak başlangıcı aşağıdaki örnekteki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="90ea1-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="90ea1-155">Başarılı olduğunda ise aşağıdaki örneğe benzer bir şekilde biter.</span><span class="sxs-lookup"><span data-stu-id="90ea1-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="90ea1-156">Grafiğinizin adından bağımsız olarak artık `curl http://gangly-bronco.squillace.io` işlemiyle `Hello World!` olan yanıtı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90ea1-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90ea1-157">Next steps</span></span>

<span data-ttu-id="90ea1-158">Artık bir ACS Kubernetes kümeniz olduğuna göre, bu senaryonun daha fazla sayıda ve daha farklı dağıtımlarını oluşturmak için [Azure Container Registry](../../container-registry/container-registry-intro.md)’yi kullanarak araştırma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="90ea1-159">Örneğin, belirli ACS dağıtımları için ayarları daha derin bir alt etki alanından denetleyen bir draft._basedomain.toplevel_ etki alanı DNS kayıt kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90ea1-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>







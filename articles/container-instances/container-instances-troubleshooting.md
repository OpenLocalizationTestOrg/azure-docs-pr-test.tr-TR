---
title: "aaaTroubleshooting Azure kapsayıcı örnekleri"
description: "Azure kapsayıcı örnekleriyle tootroubleshoot nasıl sorunları öğrenin"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="f21e9-103">Azure kapsayıcı örnekleri dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f21e9-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="f21e9-104">Bu makalede nasıl tootroubleshoot kapsayıcıları tooAzure kapsayıcı örnekleri dağıtırken sorunları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f21e9-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="f21e9-105">Ayrıca bazı içine çalışabilir hello yaygın sorunları açıklar.</span><span class="sxs-lookup"><span data-stu-id="f21e9-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="f21e9-106">Tanılama Olayları Alma</span><span class="sxs-lookup"><span data-stu-id="f21e9-106">Getting diagnostic events</span></span>

<span data-ttu-id="f21e9-107">bir kapsayıcı içindeki uygulama kodunuzdan tooview günlükleri, kullanabileceğiniz hello [az kapsayıcı günlükleri](/cli/azure/container#logs) komutu.</span><span class="sxs-lookup"><span data-stu-id="f21e9-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="f21e9-108">Ancak, kapsayıcı başarıyla dağıtma, hello Azure kapsayıcı örnekleri kaynak sağlayıcısı tarafından sağlanan tooreview hello tanılama bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="f21e9-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="f21e9-109">tooview hello olayları hello aşağıdaki komutu çalıştırın, kapsayıcı için:</span><span class="sxs-lookup"><span data-stu-id="f21e9-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="f21e9-110">Merhaba çıktı dağıtım olayları yanı sıra, kapsayıcının hello çekirdek özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="f21e9-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="f21e9-111">Genel dağıtım sorunları</span><span class="sxs-lookup"><span data-stu-id="f21e9-111">Common deployment issues</span></span>

<span data-ttu-id="f21e9-112">Bu hesaba hataların çoğu dağıtımda bazı yaygın sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="f21e9-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="f21e9-113">%S toopull görüntüsü</span><span class="sxs-lookup"><span data-stu-id="f21e9-113">Unable toopull image</span></span>

<span data-ttu-id="f21e9-114">Azure kapsayıcı örneği oluşturulamıyor toopull ise görüntünüzü başlangıçta, onu sonunda başarısız önce belirli bir süre için yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="f21e9-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="f21e9-115">Merhaba görüntü çekilen, olayları hello aşağıdaki gibi gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f21e9-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="f21e9-116">tooresolve, hello kapsayıcısını silmek ve hello görüntü adı doğru yazdığınızı ödeyen Kapat dikkat dağıtımınızı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f21e9-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="f21e9-117">Kapsayıcı sürekli olarak çıkar ve yeniden başlatır</span><span class="sxs-lookup"><span data-stu-id="f21e9-117">Container continually exits and restarts</span></span>

<span data-ttu-id="f21e9-118">Şu anda, Azure kapsayıcı örnekleri yalnızca uzun süre çalışan hizmetleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f21e9-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="f21e9-119">Kapsayıcı toocompletion ve çıkış çalıştırıyorsa, otomatik olarak yeniden başlatılır ve yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f21e9-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="f21e9-120">Bu durumda, olayları olanlar aşağıdaki gibi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f21e9-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="f21e9-121">Bu hello kapsayıcı başarıyla başlar, sonra hızlı bir şekilde yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f21e9-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="f21e9-122">Merhaba kapsayıcı örnekleri API içeren bir `retryCount` belirli bir kapsayıcıda kaç kez gösteren özelliği başlatıldıktan.</span><span class="sxs-lookup"><span data-stu-id="f21e9-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="f21e9-123">Linux dağıtımları için çoğu kapsayıcı görüntüleri bash gibi bir kabuk hello varsayılan komut olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f21e9-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="f21e9-124">Kendi başına bir kabuk uzun süre çalışan hizmet olmadığından, bu kapsayıcılar hemen çıkmak ve yeniden başlatma döngüye ayrılır.</span><span class="sxs-lookup"><span data-stu-id="f21e9-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="f21e9-125">Uzun süre toostart kapsayıcı alır</span><span class="sxs-lookup"><span data-stu-id="f21e9-125">Container takes a long time toostart</span></span>

<span data-ttu-id="f21e9-126">Kapsayıcı uzun süre toostart alır, ancak sonunda başarılı, kapsayıcı görüntünüzü hello boyutta bakarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="f21e9-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="f21e9-127">Azure kapsayıcı örnekleri kapsayıcı görüntünüzü isteğe bağlı olarak çeker, karşılaştığınız hello başlangıç zamanını doğrudan ilgili tooits çünkü boyutu.</span><span class="sxs-lookup"><span data-stu-id="f21e9-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="f21e9-128">Kapsayıcı görüntünüzün hello Docker CLI kullanarak hello boyutunu görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f21e9-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="f21e9-129">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f21e9-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="f21e9-130">Merhaba anahtar tookeeping görüntü boyutları küçük olduğundan olmanın son görüntünüzü çalışma zamanında gerekli olmayan bir şey içermediğini.</span><span class="sxs-lookup"><span data-stu-id="f21e9-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="f21e9-131">Bu durumdayken tek yönlü toodo [çok aşama derlemeleri](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="f21e9-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="f21e9-132">Çok aşama derlemeleri kolay tooensure sunun hello son görüntüsünü içeren, uygulamanız için gereken tek hello yapıları ve herhangi bir ek hello içerik derleme zamanında gerekli.</span><span class="sxs-lookup"><span data-stu-id="f21e9-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="f21e9-133">Merhaba diğer yolu tooreduce hello hello görüntü çekme, kapsayıcının başlangıç zamanında hello Azure kapsayıcı kayıt defteri hello kullanarak toohost hello kapsayıcı görüntüsü etkisidir düşündüğünüz nerede toouse Azure kapsayıcı örnekleri aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="f21e9-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="f21e9-134">Bu kapsayıcı görüntü gereksinimlerini tootravel, önemli ölçüde hello karşıdan yükleme süresini kısaltmak hello hello ağ yolu kısaltır.</span><span class="sxs-lookup"><span data-stu-id="f21e9-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>

---
title: "Azure kapsayıcı örnekleri sorunlarını giderme"
description: "Azure kapsayıcı örnekleri ile ilgili sorunları giderme hakkında bilgi edinin"
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
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="5971c-103">Azure kapsayıcı örnekleri dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="5971c-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="5971c-104">Bu makalede kapsayıcıları Azure kapsayıcı örnekleri dağıtırken ilgili sorunları gidermek nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5971c-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="5971c-105">Ayrıca bazı içine çalışabilir yaygın sorunları açıklar.</span><span class="sxs-lookup"><span data-stu-id="5971c-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="5971c-106">Tanılama Olayları Alma</span><span class="sxs-lookup"><span data-stu-id="5971c-106">Getting diagnostic events</span></span>

<span data-ttu-id="5971c-107">Bir kapsayıcı içindeki uygulama kodunuzdan günlükleri görüntülemek için kullanabileceğiniz [az kapsayıcı günlükleri](/cli/azure/container#logs) komutu.</span><span class="sxs-lookup"><span data-stu-id="5971c-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="5971c-108">Ancak, kapsayıcı başarıyla dağıtma, Azure kapsayıcı örnekleri kaynak sağlayıcısı tarafından sağlanan tanı bilgilerini gözden geçirmek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5971c-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="5971c-109">Kapsayıcı olayları görüntülemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5971c-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="5971c-110">Çıktı dağıtım olayları yanı sıra, kapsayıcı çekirdek özelliklerini içerir:</span><span class="sxs-lookup"><span data-stu-id="5971c-110">The output includes the core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="5971c-111">Genel dağıtım sorunları</span><span class="sxs-lookup"><span data-stu-id="5971c-111">Common deployment issues</span></span>

<span data-ttu-id="5971c-112">Bu hesaba hataların çoğu dağıtımda bazı yaygın sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="5971c-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="5971c-113">Çekme görüntü oluşturulamıyor</span><span class="sxs-lookup"><span data-stu-id="5971c-113">Unable to pull image</span></span>

<span data-ttu-id="5971c-114">Azure kapsayıcı örnek görüntünüzü başlangıçta çekmesini kaydedemediği sonunda başarısız önce belirli bir süre için yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="5971c-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="5971c-115">Görüntü çekilen, olayları aşağıdaki gibi gösterilir:</span><span class="sxs-lookup"><span data-stu-id="5971c-115">If the image cannot be pulled, events like the following are shown:</span></span>

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
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
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

<span data-ttu-id="5971c-116">Çözümlemek için kapsayıcıyı silin ve görüntü adı doğru yazdığınızı ödeyen Kapat dikkat dağıtımınızı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="5971c-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="5971c-117">Kapsayıcı sürekli olarak çıkar ve yeniden başlatır</span><span class="sxs-lookup"><span data-stu-id="5971c-117">Container continually exits and restarts</span></span>

<span data-ttu-id="5971c-118">Şu anda, Azure kapsayıcı örnekleri yalnızca uzun süre çalışan hizmetleri destekler.</span><span class="sxs-lookup"><span data-stu-id="5971c-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="5971c-119">Kapsayıcı tamamlama ve çıkar çalıştırıyorsa, otomatik olarak yeniden başlatılır ve yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5971c-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="5971c-120">Bu durumda, olayları olanlar aşağıdaki gibi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5971c-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="5971c-121">Kapsayıcı sorunsuz başlatıldıktan sonra hızlı bir şekilde yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5971c-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="5971c-122">Kapsayıcı örnekleri API içeren bir `retryCount` belirli bir kapsayıcıda kaç kez gösteren özelliği başlatıldıktan.</span><span class="sxs-lookup"><span data-stu-id="5971c-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="5971c-123">Linux dağıtımları için çoğu kapsayıcı görüntüleri bash gibi bir kabuk varsayılan komut olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5971c-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="5971c-124">Kendi başına bir kabuk uzun süre çalışan hizmet olmadığından, bu kapsayıcılar hemen çıkmak ve yeniden başlatma döngüye ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5971c-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="5971c-125">Kapsayıcı başlatmak için çok uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="5971c-125">Container takes a long time to start</span></span>

<span data-ttu-id="5971c-126">Kapsayıcı başlatma, ancak sonuç uzun süren, başarılı, kapsayıcı görüntünüzü boyutta bakarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="5971c-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="5971c-127">Azure kapsayıcı örnekleri kapsayıcı görüntünüzü isteğe bağlı olarak çeker çünkü karşılaştığınız başlangıç zamanını boyutuna doğrudan ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="5971c-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="5971c-128">Docker CLI kullanarak kapsayıcı görüntünüzün boyutunu görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5971c-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="5971c-129">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="5971c-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="5971c-130">Görüntü boyutları küçük tutmak için anahtarı son görüntünüzü çalışma zamanında gerekli olmayan bir şey içermediğinden emin olmaktır.</span><span class="sxs-lookup"><span data-stu-id="5971c-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="5971c-131">Yapmanın bir yolu bu olan [çok aşama derlemeleri](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="5971c-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="5971c-132">Çok aşama yapma, yalnızca uygulamanız için gereksinim duyduğunuz yapıları son görüntüsünü içeren ve herhangi bir ek içerik sağlamak kolay derleme zamanında gerekli oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5971c-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="5971c-133">Kapsayıcının başlangıç zamanında görüntü çekme etkisini azaltmak için diğer Azure kapsayıcı örneği kullanmak istiyorsanız, aynı bölgede Azure kapsayıcı kayıt defterini kullanarak kapsayıcı görüntüsü barındırmak için bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="5971c-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="5971c-134">Bu, kapsayıcı görüntü seyahat gereken ağ yolu önemli ölçüde karşıdan yükleme süresini kısaltmak kısaltır.</span><span class="sxs-lookup"><span data-stu-id="5971c-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>
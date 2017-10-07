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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Azure kapsayıcı örnekleri dağıtım sorunlarını giderme

Bu makalede nasıl tootroubleshoot kapsayıcıları tooAzure kapsayıcı örnekleri dağıtırken sorunları gösterir. Ayrıca bazı içine çalışabilir hello yaygın sorunları açıklar.

## <a name="getting-diagnostic-events"></a>Tanılama Olayları Alma

bir kapsayıcı içindeki uygulama kodunuzdan tooview günlükleri, kullanabileceğiniz hello [az kapsayıcı günlükleri](/cli/azure/container#logs) komutu. Ancak, kapsayıcı başarıyla dağıtma, hello Azure kapsayıcı örnekleri kaynak sağlayıcısı tarafından sağlanan tooreview hello tanılama bilgileri gerekir. tooview hello olayları hello aşağıdaki komutu çalıştırın, kapsayıcı için:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

Merhaba çıktı dağıtım olayları yanı sıra, kapsayıcının hello çekirdek özellikleri içerir:

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

## <a name="common-deployment-issues"></a>Genel dağıtım sorunları

Bu hesaba hataların çoğu dağıtımda bazı yaygın sorunlar vardır.

### <a name="unable-toopull-image"></a>%S toopull görüntüsü

Azure kapsayıcı örneği oluşturulamıyor toopull ise görüntünüzü başlangıçta, onu sonunda başarısız önce belirli bir süre için yeniden deneme sayısı. Merhaba görüntü çekilen, olayları hello aşağıdaki gibi gösterilir:

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

tooresolve, hello kapsayıcısını silmek ve hello görüntü adı doğru yazdığınızı ödeyen Kapat dikkat dağıtımınızı yeniden deneyin.

### <a name="container-continually-exits-and-restarts"></a>Kapsayıcı sürekli olarak çıkar ve yeniden başlatır

Şu anda, Azure kapsayıcı örnekleri yalnızca uzun süre çalışan hizmetleri destekler. Kapsayıcı toocompletion ve çıkış çalıştırıyorsa, otomatik olarak yeniden başlatılır ve yeniden çalıştırır. Bu durumda, olayları olanlar aşağıdaki gibi gösterilir. Bu hello kapsayıcı başarıyla başlar, sonra hızlı bir şekilde yeniden unutmayın. Merhaba kapsayıcı örnekleri API içeren bir `retryCount` belirli bir kapsayıcıda kaç kez gösteren özelliği başlatıldıktan.

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
> Linux dağıtımları için çoğu kapsayıcı görüntüleri bash gibi bir kabuk hello varsayılan komut olarak ayarlayın. Kendi başına bir kabuk uzun süre çalışan hizmet olmadığından, bu kapsayıcılar hemen çıkmak ve yeniden başlatma döngüye ayrılır.

### <a name="container-takes-a-long-time-toostart"></a>Uzun süre toostart kapsayıcı alır

Kapsayıcı uzun süre toostart alır, ancak sonunda başarılı, kapsayıcı görüntünüzü hello boyutta bakarak başlatın. Azure kapsayıcı örnekleri kapsayıcı görüntünüzü isteğe bağlı olarak çeker, karşılaştığınız hello başlangıç zamanını doğrudan ilgili tooits çünkü boyutu.

Kapsayıcı görüntünüzün hello Docker CLI kullanarak hello boyutunu görüntüleyebilirsiniz:

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

Merhaba anahtar tookeeping görüntü boyutları küçük olduğundan olmanın son görüntünüzü çalışma zamanında gerekli olmayan bir şey içermediğini. Bu durumdayken tek yönlü toodo [çok aşama derlemeleri](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Çok aşama derlemeleri kolay tooensure sunun hello son görüntüsünü içeren, uygulamanız için gereken tek hello yapıları ve herhangi bir ek hello içerik derleme zamanında gerekli.

Merhaba diğer yolu tooreduce hello hello görüntü çekme, kapsayıcının başlangıç zamanında hello Azure kapsayıcı kayıt defteri hello kullanarak toohost hello kapsayıcı görüntüsü etkisidir düşündüğünüz nerede toouse Azure kapsayıcı örnekleri aynı bölgede. Bu kapsayıcı görüntü gereksinimlerini tootravel, önemli ölçüde hello karşıdan yükleme süresini kısaltmak hello hello ağ yolu kısaltır.

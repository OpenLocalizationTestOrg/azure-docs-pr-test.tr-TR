---
title: "Azure DC/OS kümesi aaaLoad Bakiye kapsayıcılarında | Microsoft Docs"
description: "Bir Azure kapsayıcı hizmeti DC/OS kümesinde birden çok kapsayıcı arasında Yük Dengelemesi."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, Mikro hizmetler, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Bir Azure kapsayıcı hizmeti DC/OS kümesi Yük Dengelemesi kapsayıcıları
Bu makalede, Marathon-LB kullanarak Azure kapsayıcı hizmeti DC/OS bir iç yük dengeleyicisi toocreate nasıl yönetileceğini keşfedin. Bu yapılandırma, tooscale yatay uygulamalarınızı etkinleştirir. Ayrıca, hello ortak ve özel aracı kümeleri tootake avantajlarından hello ortak küme ve uygulama kapsayıcılarınızı hello özel kümede yük dengeleyici koyarak sağlar. Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Marathon yük dengeleyici yapılandırma
> * Merhaba yük dengeleyici kullanarak bir uygulamayı dağıtma
> * Yapılandırma ve Azure yük dengeleyici

Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir. Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Yükü Dengeleme'ye genel bakış

Bir Azure kapsayıcı hizmeti DC/OS kümesinde iki yük dengeleyici katmanı vardır: 

**Azure yük dengeleyici** ortak giriş noktaları (olanları, son kullanıcıların erişim hello) sağlar. Bir Azure LB otomatik olarak Azure kapsayıcı hizmeti tarafından sağlanır ve, varsayılan olarak, yapılandırılmış tooexpose bağlantı noktası 80, 443 ve 8080.

**Merhaba Marathon yük dengeleyici (marathon-lb)** yollar gelen istekleri servis istekleri toocontainer örnekleri. Biz bizim web hizmeti sağlayan hello kapsayıcıları ölçeklendirirken hello marathon-lb dinamik olarak uyum sağlar. Bu yük dengeleyici varsayılan olarak, kapsayıcı hizmeti tarafından sağlanan değil ancak kolay tooinstall işlem.

## <a name="configure-marathon-load-balancer"></a>Marathon yük dengeleyici yapılandırma

Marathon yük dengeleyici kendisini dağıttıktan sonra Merhaba kapsayıcılara göre dinamik olarak yeniden yapılandırır. Bu olursa, Apache Mesos başka yerde hello kapsayıcıyı yeniden başlatır ve marathon-lb uyum de kapsayıcı ya da bir aracı - esnek toohello kaybı olabilir.

Çalışma hello aşağıdaki tooinstall hello marathon yük dengeleyici hello ortak aracısının kümede komutu.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Yük dengeli uygulama dağıtma

Biz hello marathon-lb paketine sahip olduğunuza göre biz tooload Bakiye istediğimiz bir uygulama kapsayıcısı dağıtabilirsiniz. 

İlk olarak, hello genel olarak kullanıma sunulan hello aracıları FQDN'sini alın.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Ardından, adlı bir dosya oluşturun *hello web.json* ve hello kopyasında aşağıdaki içeriği. Merhaba `HAPROXY_0_VHOST` etiket hello hello DC/OS aracıları FQDN'si ile güncelleştirilmiş toobe gerekiyor. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Merhaba DC/OS CLI toorun hello uygulaması kullanın. Varsayılan olarak Marathon hello hello uygulama toohello özel küme dağıtır. Dağıtım hello Bunun anlamı yalnızca, genellikle istenen hello davranış olduğu, yük dengeleyici erişilebilir.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Merhaba uygulama dağıtıldıktan sonra toohello Merhaba Aracısı küme tooview yükü dengelenmiş uygulaması'nın FQDN'si göz atın.

![Yük dengeli uygulama görüntüsü](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Azure yük dengeleyici yapılandırma

Varsayılan olarak, Azure Load Balancer 80, 8080 ve 443 bağlantı noktalarını ortaya çıkarır. Kullanıyorsanız (Yukarıdaki örnek hello içinde yaptığımız) üç bağlantı noktaları ardından toodo gereken bir şey yok. Mümkün toohit olmalıdır, aracı yük dengeleyicinin FQDN ve her yenilediğinizde, üç web sunucusundan bir hepsini şekilde birini isabet. 

Tooadd bir hepsini bir kez deneme kuralı ve bir araştırma hello yük dengeleyici üzerinde farklı bir bağlantı noktası kullanıyorsanız, kullandığınız hello için bağlantı noktası gerekir. Hello bunu yapabilirsiniz [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), hello komutlarla `azure network lb rule create` ve `azure network lb probe create`.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, yük dengelemeyi hello Marathon hem Azure yük dengeleyicileri dahil olmak üzere aşağıdaki eylemler hello ACS hakkında öğrenilen:

> [!div class="checklist"]
> * Marathon yük dengeleyici yapılandırma
> * Merhaba yük dengeleyici kullanarak bir uygulamayı dağıtma
> * Yapılandırma ve Azure yük dengeleyici

Azure depolama DC/OS Azure ile tümleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [DC/OS kümesi bağlama Azure dosya paylaşımı](container-service-dcos-fileshare.md)
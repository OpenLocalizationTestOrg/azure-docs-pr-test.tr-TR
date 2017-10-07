---
title: "aaaManage Azure DC/OS kümesi Marathon REST API'si ile | Microsoft Docs"
description: "Kapsayıcıları tooan Azure kapsayıcı hizmeti DC/OS kümesi hello Marathon REST API kullanarak dağıtın."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>DC/OS hello Marathon REST API'si aracılığıyla kapsayıcı Yönetimi
DC/OS dağıtma ve hello temel donanımı özetlerken, kümelenmiş iş yükleri ölçekleme için bir ortam sağlar. DC/OS’nin en üstünde, hesaplama iş yüklerini zamanlamayı ve yürütmeyi yöneten bir çerçeve vardır. Çerçeveler çok sayıda yaygın iş yükü için kullanılabilir, ancak bu belgenin oluşturma ve kapsayıcı dağıtımlarını hello Marathon REST API kullanarak ölçeklendirme başlamanızı sağlar. 

## <a name="prerequisites"></a>Ön koşullar

Bu örneklerin üzerinden geçmeden önce, Azure Kapsayıcı Hizmeti’nde yapılandırılan bir DC/OS kümeniz olması gerekir. Ayrıca toohave uzak bağlantı toothis küme gerekir. Bu öğeler hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Azure Container Service kümesini dağıtma](container-service-deployment.md)
* [Tooan Azure kapsayıcı hizmeti kümesine bağlanma](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Erişim hello DC/OS API'leri
Bağlı toohello Azure kapsayıcı hizmeti kümesi sonra hello DC/OS ve ilgili REST API'lerine http://localhost: Local-port aracılığıyla erişebilirsiniz. Bu belgedeki Hello örneklerde, bağlantı noktası 80 üzerinde tünel varsayılmaktadır. Örneğin, URI'ler hello Marathon uç noktaları erişilebildiğini itibaren `http://localhost/marathon/v2/`. 

Çeşitli API'ler hello hakkında daha fazla bilgi için hello hello Mesosphere belgelerine bakın [Marathon API'si](https://mesosphere.github.io/marathon/docs/rest-api.html) ve [Chronos API'si](https://mesos.github.io/chronos/docs/api.html)ve hello için Apache belgelerine [Mesos Scheduler API'si ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>DC/OS’den ve Marathon’dan bilgi toplama
Toohello DC/OS kümesine kapsayıcıları dağıtmadan önce hello adları ve hello DC/OS aracıların durumu gibi hello DC/OS kümesi hakkında bazı bilgileri toplayın. Bu nedenle, sorgu hello toodo `master/slaves` hello DC/OS REST API uç noktası. Her şey yolunda giderse hello sorgu her biri için DC/OS aracıları ve çeşitli özellikler listesini döndürür.

```bash
curl http://localhost/mesos/master/slaves
```

Şimdi hello Marathon kullanın `/apps` geçerli uygulama dağıtımlarını toohello DC/OS kümesi için uç nokta toocheck. Bu yeni bir küme ise, uygulamalar için boş bir dizi görürsünüz.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Docker biçimli kapsayıcı dağıtma
Docker biçimli kapsayıcıları hello Marathon REST API aracılığıyla hello hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın. Merhaba aşağıdaki örnek Nginx bir kapsayıcı tooa özel aracı hello kümedeki dağıtır. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy Docker biçimli bir kapsayıcıyı hello JSON dosyası erişilebilecek bir konuma depolayın. Komutu aşağıdaki hello çalıştırmak İleri toodeploy hello kapsayıcı. Merhaba hello JSON dosyasının adını belirtin (`marathon.json` Bu örnekte).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

Merhaba çıkış benzer toohello aşağıda verilmiştir:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Şimdi, uygulamalar için marathon'u, bu yeni uygulama hello çıkışında görünür.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Merhaba kapsayıcı ulaşmak

Nginx bir kapsayıcıda hello özel aracıları hello kümedeki birini çalıştıran bu hello doğrulayabilirsiniz. toofind hello ana bilgisayarı ve bağlantı noktası hello kapsayıcı çalıştığı çalışan görevlerin hello için Marathon sorgu: 

```bash
curl localhost/marathon/v2/tasks
```

Merhaba değerini bulur `host` hello çıktısında (bir IP adresi benzer çok`10.32.0.x`) ve hello değerini `ports`.


Artık bir SSH terminal bağlantısı (tünel bağlantısı değil) toohello yönetim FQDN hello kümesinin olun. Bağlantı kurulduktan sonra istek aşağıdaki, hello doğru değerini değiştirerek hello olun `host` ve `ports`:

```bash
curl http://host:ports
```

Merhaba Nginx server çıktısı benzer toohello aşağıda verilmiştir:

![Kapsayıcısından Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Kapsayıcılarınızı ölçeklendirme
Uygulama dağıtımlarını hello Marathon API'si tooscale çıkışı veya ölçek kullanabilirsiniz. Merhaba önceki örnekte, uygulamanın bir örneği dağıtıldı. Şimdi bu uygulamanın toothree örneklerini çıkışı ölçeklendirin. toodo bu nedenle, JSON metnini aşağıdaki hello kullanarak bir JSON dosyası oluşturun ve erişilebilir bir yerde saklayın.

```json
{ "instances": 3 }
```

Tünel bağlantısından hello uygulama çıkış komut tooscale aşağıdaki hello çalıştırın.

> [!NOTE]
> Hello URI, http://localhost/marathon/v2/apps/ hello uygulama tooscale hello Kimliğine göre ve ardından ' dir. Burada sağlanan hello Nginx örneğini kullanıyorsanız, hello URI http://localhost/marathon/v2/apps/nginx olacaktır.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Son olarak, uygulamalar için hello Marathon uç noktaya sorgu. Artık üç adet Nginx kapsayıcısı olduğunu görürsünüz.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Eşdeğer PowerShell komutları
Bir Windows sisteminde PowerShell komutlarını kullanarak aynı eylemleri gerçekleştirebilirsiniz.

Aracı adları ve aracı durumu gibi hello DC/OS kümesi hakkında bilgi toogather hello aşağıdaki komutu çalıştırın:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Docker biçimli kapsayıcıları Marathon aracılığıyla hello hedeflenen dağıtımı açıklayan bir JSON dosyası kullanarak dağıtın. Merhaba aşağıdaki örnek hello kapsayıcısının hello DC/OS Aracısı tooport 80 bağlantı noktası 80 bağlama hello Nginx kapsayıcısı dağıtır.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy Docker biçimli bir kapsayıcıyı hello JSON dosyası erişilebilecek bir konuma depolayın. Komutu aşağıdaki hello çalıştırmak İleri toodeploy hello kapsayıcı. Merhaba yolu toohello JSON dosyasını belirtin (`marathon.json` Bu örnekte).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

Uygulama dağıtımlarını hello Marathon API'si tooscale çıkışı veya ölçek de kullanabilirsiniz. Merhaba önceki örnekte, uygulamanın bir örneği dağıtıldı. Şimdi bu uygulamanın toothree örneklerini çıkışı ölçeklendirin. toodo bu nedenle, JSON metnini aşağıdaki hello kullanarak bir JSON dosyası oluşturun ve erişilebilir bir yerde saklayın.

```json
{ "instances": 3 }
```

Merhaba uygulama çıkış komut tooscale aşağıdaki hello çalıştırın:

> [!NOTE]
> Hello URI, http://localhost/marathon/v2/apps/ hello uygulama tooscale hello Kimliğine göre ve ardından ' dir. Burada sağlanan hello Nginx örneğini kullanıyorsanız, hello URI http://localhost/marathon/v2/apps/nginx olacaktır.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Mesos HTTP uç noktaları hakkında daha fazla bilgi](http://mesos.apache.org/documentation/latest/endpoints/)
* [Merhaba Marathon REST API'si hakkında daha fazla bilgi](https://mesosphere.github.io/marathon/docs/rest-api.html)


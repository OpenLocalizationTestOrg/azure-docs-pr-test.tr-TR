---
title: "aaaManage Azure Swarm Docker API'si ile küme | Microsoft Docs"
description: "Azure kapsayıcı hizmetinde kapsayıcıları tooa Docker Swarm kümesi dağıtma"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Docker Swarm ile kapsayıcı yönetimi
Docker Swarm, havuza alınmış Docker ana bilgisayarları grubuna kapsayıcılı iş yükleri dağıtmak için bir ortam sağlar. Docker Swarm hello yerel Docker API'sini kullanır. Docker Swarm kapsayıcılarında yönetmek için hello bir tek kapsayıcılı ana bilgisayardakiyle neredeyse aynı toowhat iş akışıdır. Bu belge Docker Swarm’ın Azure Kapsayıcı Hizmeti örneğine kapsayıcılı iş yüklerini dağıtmaya ilişkin basit örnekler sağlar. Docker Swarm hakkında daha fazla ayrıntılı belgeler için bkz. [Docker.com’da Docker Swarm ](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Bu belge toohello alıştırmalarda Önkoşullar:

[Azure Container Service'te Swarm kümesi oluşturma](container-service-deployment.md)

[Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Yeni bir kapsayıcı dağıtma
toocreate hello Docker Swarm, yeni bir kapsayıcıda kullanmak hello `docker run` (bir SSH tünel toohello yöneticileri hello Önkoşullar yukarıdaki göredir açtığınız sağlama) komutu. Bu örnek, hello bir kapsayıcı oluşturur `yeasy/simple-web` görüntü:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Merhaba kapsayıcıyı oluşturduktan sonra kullanmak `docker ps` hello kapsayıcı hakkında tooreturn bilgi. Burada hello kapsayıcıyı barındıran bu hello Swarm aracının listelendiğine dikkat edin:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Merhaba hello Swarm aracı yük dengeleyicinin Genel DNS adı aracılığıyla bu kapsayıcıda çalışan Merhaba uygulaması artık erişebilirsiniz. Bu bilgileri hello Azure portalında bulabilirsiniz:  

![Gerçek ziyaret sonuçları](./media/container-service-docker-swarm/real-visit.jpg)  

Varsayılan olarak bağlantı noktası 80, hello yük dengeleyiciye sahip 8080 ve 443 numaralı açın. Başka bir bağlantı noktasında tooconnect istiyorsanız aracı havuzu hello için bu bağlantı noktasını hello Azure yük dengeleyici tooopen gerekir.

## <a name="deploy-multiple-containers"></a>Birden çok kapsayıcı dağıtma
Birden çok kapsayıcı başlatıldığında, birden çok kez 'docker run' yürüterek hello kullanabilirsiniz `docker ps` üzerinde çalışan Merhaba kapsayıcılara barındıran komutu toosee. Merhaba aşağıdaki örnekte, üç kapsayıcı hello üç Swarm aracısında eşit olarak yayılır:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Docker Compose kullanarak kapsayıcıları dağıtma
Docker Compose tooautomate hello dağıtımını ve yapılandırmasını birden çok kapsayıcı kullanabilirsiniz. toodo, bir güvenli Kabuk (SSH) tüneli oluşturulduğundan ve (Merhaba ön koşullar yukarıdaki bakın) bu hello DOCKER_HOST değişkeninin ayarlandığından, olun.

Yerel sisteminizde docker-compose.yml dosyası oluşturun. toodo Bu, bunu kullanın [örnek](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

Çalıştırma `docker-compose up -d` toostart hello kapsayıcı dağıtımlarını:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

Son olarak, çalışan kapsayıcılar hello listesi döndürülür. Bu liste, Docker Compose kullanarak dağıtılan Merhaba kapsayıcılara yansıtır:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Doğal olarak, kullanabileceğiniz `docker-compose ps` tooexamine yalnızca tanımlanan kapsayıcıları Merhaba, `compose.yml` dosya.

## <a name="next-steps"></a>Sonraki adımlar
[Docker Swarm hakkında daha fazla bilgi edinme](https://docs.docker.com/swarm/)


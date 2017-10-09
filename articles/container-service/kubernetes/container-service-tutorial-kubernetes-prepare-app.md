---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - App hazırlama | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - App hazırlama"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Azure kapsayıcı hizmeti ile kullanılan kapsayıcı görüntüleri toobe oluşturma

Bu öğreticide, bölümü yedi, biri çok kapsayıcı uygulama Kubernetes kullanım için hazırlanır. Tamamlanan adımları içerir:  

> [!div class="checklist"]
> * GitHub’dan uygulama kaynağını kopyalama  
> * Merhaba uygulama kaynağından bir kapsayıcı görüntü oluşturma
> * Merhaba uygulaması yerel bir Docker ortamında test etme

Tamamlandığında, uygulama aşağıdaki hello yerel geliştirme ortamınızda erişilebilir.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

Sonraki öğreticilerde, hello kapsayıcı görüntüdür karşıya yüklenen tooan Azure kapsayıcı kayıt defteri ve ardından Azure çalıştırmada Kubernetes küme barındırılan.

## <a name="before-you-begin"></a>Başlamadan önce

Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır. Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/). 

toocomplete Bu öğreticide, bir Docker geliştirme ortamı gerekir. Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.

## <a name="get-application-code"></a>Uygulama kodunu alma

Bu öğreticide kullanılan hello örnek temel bir oylama uygulama uygulamasıdır. Merhaba uygulaması, ön uç web bileşeni ve bir arka uç Redis örneği oluşur. Merhaba web bileşeni özel kapsayıcı görüntüsüne paketlenmiştir. Merhaba Redis örneği Docker hub'a değiştirilmemiş bir görüntüden kullanır.  

Git toodownload hello uygulama tooyour geliştirme ortamı bir kopyasını kullanın.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

İç hello kopyalanan dizin hello uygulama kaynak koduna, önceden oluşturulmuş bir Docker compose dosyası ve bir Kubernetes bildirim dosyası. Bu dosyalar hello öğretici kümesi boyunca kullanılan toocreate varlıkları içerir. 

## <a name="create-container-images"></a>Kapsayıcı görüntüleri oluşturma

[Docker Compose](https://docs.docker.com/compose/) olabilir kapsayıcı görüntüleri ve birden çok kapsayıcı uygulamaları hello dağıtımı dışında tooautomate hello yapı kullanılır.

Merhaba docker-compose.yml dosyası toocreate hello kapsayıcı resmi çalıştırmak, indirme Merhaba, görüntü Redis ve hello uygulamasını başlatın.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Tamamlandığında, hello kullan [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) komut toosee oluşturulan hello görüntüler.

```bash
docker images
```

Üç görüntüleri indirilebilir veya oluşturulan dikkat edin. Merhaba *azure oy ön* görüntü Merhaba uygulaması içerir. Merhaba türetilmiş *nginx flask* görüntü. Merhaba Redis görüntü Docker Hub'ından yüklendi.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Merhaba çalıştırmak [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) komutu toosee Merhaba kapsayıcılara çalıştıran.

```bash
docker ps
```

Çıktı:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Uygulamayı yerel olarak test etme

Uygulama çalıştıran toohttp://localhost:8080 toosee hello göz atın.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Uygulama işlevselliği doğrulandı, çalışan kapsayıcılar hello durdurulur ve kaldırılmış. Merhaba kapsayıcı görüntüleri silmeyin. Merhaba *azure oy ön* karşıya yüklenen tooan Azure kapsayıcı kayıt defteri örneği hello sonraki öğreticide görüntüdür.

Çalışan kapsayıcılar toostop hello aşağıdaki hello çalıştırın.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Durdurulmuş Merhaba kapsayıcılara komutu aşağıdaki hello ile silin.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Tamamlandığında, hello Azure oy uygulamayı içeren bir kapsayıcı görüntüsüne sahip.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir uygulamayı test edilmiştir ve kapsayıcı görüntüleri hello uygulaması için oluşturulmuş. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Merhaba Uygulama kaynağı github'dan kopyalama  
> * Uygulama kaynağından bir kapsayıcı görüntüsü oluşturuldu
> * Bir yerel Docker ortamında test edilmiş hello uygulama

Kapsayıcı görüntüleri bir Azure kapsayıcı kayıt defterine depolama hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Anında iletme görüntüleri tooAzure kapsayıcı kayıt defteri](./container-service-tutorial-kubernetes-prepare-acr.md)

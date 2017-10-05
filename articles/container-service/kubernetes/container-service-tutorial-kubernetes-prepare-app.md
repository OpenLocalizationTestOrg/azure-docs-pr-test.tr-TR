---
title: "Azure kapsayıcı hizmeti Öğreticisi - App hazırlama | Microsoft Docs"
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
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a>Azure kapsayıcı hizmeti ile kullanılmak üzere kapsayıcı görüntüleri oluşturma

Bu öğreticide, bölümü yedi, biri çok kapsayıcı uygulama Kubernetes kullanım için hazırlanır. Tamamlanan adımları içerir:  

> [!div class="checklist"]
> * GitHub’dan uygulama kaynağını kopyalama  
> * Uygulama kaynağından bir kapsayıcı görüntü oluşturma
> * Uygulamayı bir yerel Docker ortamında test etme

Tamamlandığında, aşağıdaki uygulama yerel geliştirme ortamınızda erişilebilir.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

Sonraki öğreticilerde, kapsayıcı görüntünün bir Azure kapsayıcı kayıt defterine yüklenir ve ardından Azure çalıştırmada Kubernetes küme barındırılan.

## <a name="before-you-begin"></a>Başlamadan önce

Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır. Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/). 

Bu öğreticiyi tamamlamak için Docker geliştirme ortamı gerekir. Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.

## <a name="get-application-code"></a>Uygulama kodunu alma

Bu öğreticide kullanılan örnek temel bir oylama uygulama uygulamasıdır. Uygulama bir ön uç web bileşeni ve bir arka uç Redis örneği oluşur. Web bileşeni özel kapsayıcı görüntüsüne paketlenmiştir. Redis örneği Docker hub'a değiştirilmemiş bir görüntüden kullanır.  

Geliştirme ortamınızı uygulamaya bir kopyasını indirmek için Git kullanın.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Kopyalanan dizini içinde uygulama kaynak koduna, önceden oluşturulmuş bir Docker compose dosyası ve bir Kubernetes bildirim dosyası. Bu dosyalar, öğretici kümesi boyunca varlıklar oluşturmak için kullanılır. 

## <a name="create-container-images"></a>Kapsayıcı görüntüleri oluşturma

[Docker Compose](https://docs.docker.com/compose/) yapı kapsayıcı görüntüler ve birden çok kapsayıcı uygulamalarının dağıtımını otomatik hale getirmek için kullanılabilir.

Kapsayıcı görüntü oluşturma, Redis görüntüsünü karşıdan yüklemek ve uygulamayı başlatmak için docker-compose.yml dosyasını çalıştırın.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Tamamlandığında kullanmak [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) oluşturulan görüntüleri görmek için komutu.

```bash
docker images
```

Üç görüntüleri indirilebilir veya oluşturulan dikkat edin. *Azure oy ön* görüntü, uygulama içerir. Türetilmiş *nginx flask* görüntü. Redis görüntü Docker Hub'ından yüklendi.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Çalıştırma [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) çalışan kapsayıcıları görmek için komutu.

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

Çalışan uygulama görmek için http://localhost: 8080 için göz atın.

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Uygulama işlevselliği doğrulandı, çalışan kapsayıcılar durdurulur ve kaldırılmış. Kapsayıcı görüntüleri silmeyin. *Azure oy ön* görüntü sonraki öğreticide Azure kapsayıcı kayıt defteri örneğine yüklenir.

Çalışan kapsayıcılar durdurmak için aşağıdaki komutu çalıştırın.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Aşağıdaki komutla durdurulmuş kapsayıcıları silin.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Tamamlandığında, Azure oy uygulamayı içeren bir kapsayıcı görüntüsüne sahip.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir uygulamayı test edilmiştir ve kapsayıcı görüntüleri uygulama için oluşturulan. Aşağıdaki adımlar tamamlandı:

> [!div class="checklist"]
> * GitHub’dan uygulama kaynağını kopyalama  
> * Uygulama kaynağından bir kapsayıcı görüntüsü oluşturuldu
> * Uygulamayı yerel bir Docker ortamında test

Kapsayıcı görüntülerini bir Azure Container Registry’de depolama hakkında bilgi edinmek için sonraki öğreticiye geçin.

> [!div class="nextstepaction"]
> [Azure Container Registry’ye görüntüleri gönderme](./container-service-tutorial-kubernetes-prepare-acr.md)
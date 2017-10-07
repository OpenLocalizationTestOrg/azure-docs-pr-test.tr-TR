---
title: "aaaAzure kapsayıcı örnekleri Öğreticisi - uygulamanızı hazırlama | Azure belgeleri"
description: "Bir uygulama dağıtım tooAzure kapsayıcı örnekleri için hazırlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Dağıtım tooAzure kapsayıcı örnekleri için kapsayıcı oluşturma

Azure Container Instances, Docker kapsayıcılarının herhangi bir sanal makine sağlama veya herhangi bir üst düzey hizmet benimsenmesi gerekmeden Azure altyapısına dağıtılmasını sağlar. Bu öğreticide, Node.js içinde basit bir web uygulaması oluşturacak ve bu uygulamayı Azure Container Instances kullanılarak çalıştırılabilir bir kapsayıcıda paketleyeceksiniz. Şu konular yer almaktadır:

> [!div class="checklist"]
> * GitHub’dan uygulama kaynağını kopyalama  
> * Uygulama kaynağından kapsayıcı görüntüsü oluşturma
> * Merhaba görüntüleri yerel bir Docker ortamında test etme

Sonraki öğreticilerde, görüntü tooan Azure kapsayıcı kayıt defteri karşıya yükleyin ve ardından bunları tooAzure kapsayıcı örneği dağıtın.

## <a name="before-you-begin"></a>Başlamadan önce

Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır. Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/). 

toocomplete Bu öğreticide, bir Docker geliştirme ortamı gerekir. Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.

## <a name="get-application-code"></a>Uygulama kodunu alma

Bu öğreticide Hello örnek içeren yerleşik basit bir web uygulaması [Node.js](http://nodejs.org). Merhaba uygulama bir statik HTML sayfası sunar ve şöyle görünür:

![Tarayıcıda gösterilen öğretici uygulama][aci-tutorial-app]

Git toodownload hello örneği kullanın:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Merhaba kapsayıcı yansıması oluştur

Merhaba hello örnek deposuna sağlanan Dockerfile hello kapsayıcı nasıl yapılandırıldığını gösterir. Gelen başlatır bir [resmi Node.js görüntü] [ dockerhub-nodeimage] göre [Alpine Linux](https://alpinelinux.org/), kapsayıcılarla uygun toouse olan küçük bir dağıtımı. Ardından hello kapsayıcıya hello uygulama dosyalarını kopyalar, hello düğüm paketi Yöneticisi kullanarak bağımlılıkları yükler ve son olarak hello uygulamayı başlatır.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Kullanım hello `docker build` olarak etiketleme komutu toocreate hello kapsayıcı görüntüsü, *aci öğretici uygulama*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Kullanım hello `docker images` toosee yerleşik hello görüntü:

```bash
docker images
```

Çıktı:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Merhaba kapsayıcı yerel olarak çalıştırma

Merhaba kapsayıcı tooAzure kapsayıcı örnekleri dağıtma denemeden önce yerel olarak çalıştırma çalıştığını tooconfirm. Merhaba `-d` anahtar hello arka planda çalışan hello kapsayıcı sağlar ancak `-p` toomap, işlem tooport 80 hello kapsayıcısında rastgele bir bağlantı noktası sağlar.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Kapsayıcı hello açık hello tarayıcı toohttp://localhost:8080 tooconfirm çalışıyor.

![Merhaba tarayıcıda yerel olarak çalışan hello uygulama][aci-tutorial-app-local]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, dağıtılan tooAzure kapsayıcı örnekleri olabilir bir kapsayıcı görüntüsü oluşturuldu. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Merhaba Uygulama kaynağı github'dan kopyalama  
> * Uygulama kaynağından kapsayıcı görüntüsü oluşturma
> * Merhaba kapsayıcı yerel olarak test etme

Kapsayıcı görüntüleri bir Azure kapsayıcı kayıt defterine depolama hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [Anında iletme görüntüleri tooAzure kapsayıcı kayıt defteri](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png
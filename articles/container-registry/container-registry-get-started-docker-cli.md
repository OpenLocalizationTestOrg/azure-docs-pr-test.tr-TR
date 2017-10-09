---
title: "aaaPush Docker görüntü tooprivate Azure kayıt defteri | Microsoft Docs"
description: "İtme ve görüntüleri tooa özel kapsayıcı kayıt hello Docker CLI kullanarak azure'da Docker çekme"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Merhaba Docker CLI kullanarak ilk görüntü tooa özel Docker kapsayıcısı kaydınız bildirme
Azure kapsayıcı kayıt defteri depolar ve özel yönetir [Docker](http://hub.docker.com) kapsayıcı görüntüler, benzer toohello şekilde [Docker hub'a](https://hub.docker.com/) ortak Docker görüntüleri depolar. Merhaba kullandığınız [Docker komut satırı arabirimi](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) için [oturum açma](https://docs.docker.com/engine/reference/commandline/login/), [itme](https://docs.docker.com/engine/reference/commandline/push/), [çekme](https://docs.docker.com/engine/reference/commandline/pull/)ve, kapsayıcı üzerinde başka işlemler kayıt defteri.

Daha fazla arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)



## <a name="prerequisites"></a>Ön koşullar
* **Azure kapsayıcısı kayıt defteri** -Azure aboneliğinizde bir kapsayıcı kayıt defteri oluşturun. Örneğin, hello kullan [Azure portal](container-registry-get-started-portal.md) veya hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak, yerel bilgisayarınıza yüklemek [Docker altyapısına](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Tooa kayıt defterinde oturum
Çalıştırma `docker login` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](container-registry-authentication.md).

Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md). Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Emin toospecify hello tam kayıt defteri adı (tümü küçük harf) olun. Bu örnekte bu değer `myregistry.azurecr.io`’dur.

## <a name="steps-toopull-and-push-an-image"></a>Adımları toopull ve anında iletme görüntü
Merhaba yüklemeleri hello ortak Docker hub'a kayıt defteri, Nginx görüntüden özel Azure kapsayıcı kaydınız için tooyour kayıt defteri iter, ardından yeniden çeker etiketleri hello örnek izleyin.

**1. Merhaba Docker resmi görüntü için Nginx isteme**

İlk çekme hello ortak Nginx görüntü tooyour yerel bilgisayar.

```
docker pull nginx
```
**2. Merhaba Nginx kapsayıcısı Başlat**

Hello aşağıdaki komut hello yerel Nginx kapsayıcısı etkileşimli olarak Nginx toosee çıkışı sağlayan bağlantı noktası 8080 üzerinde başlatır. Bir kez durduruldu kapsayıcı çalıştıran hello kaldırır.

```
docker run -it --rm -p 8080:80 nginx
```

Çok Gözat[http://localhost: 8080](http://localhost:8080) kapsayıcı çalıştıran tooview hello. Bir aşağıdaki ekrana benzer toohello bakın.

![Yerel bilgisayarda Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

toostop çalışan kapsayıcı Merhaba, basın [CTRL] + [C].

**3. Merhaba görüntünün bir diğer ad, kayıt defterinde oluşturun**

Merhaba aşağıdaki komutu bir diğer ad hello görüntünün tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur. Bu örnek hello belirtir `samples` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Anında iletme hello görüntü tooyour kayıt defteri**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Çekme hello görüntü, kayıt defteri**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Kayıt defterinden Hello Nginx kapsayıcısı Başlat**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Çok Gözat[http://localhost: 8080](http://localhost:8080) kapsayıcı çalıştıran tooview hello.

toostop çalışan kapsayıcı Merhaba, basın [CTRL] + [C].

**7. (İsteğe bağlı) Merhaba görüntüsünü kaldırın**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Eşzamanlı İşlem Limitleri
Bazı senaryolarda çağrıların eşzamanlı olarak yürütülmesi hatalara neden olabilir. Aşağıdaki tablonun hello Azure kapsayıcı kayıt defteri "Gönderme" ve "Çekme" işlemlerini ile eşzamanlı çağrıları hello sınırları içerir:

| İşlem  | Sınır                                  |
| ---------- | -------------------------------------- |
| PULL       | Kayıt defteri too10 eşzamanlı çeker |
| PUSH       | Kayıt defteri too5 eşzamanlı iter |

## <a name="next-steps"></a>Sonraki adımlar
Merhaba temelleri bildiğinize göre kayıt defterini kullanarak hazır toostart olduğunuz! Örneğin, kapsayıcı görüntüleri tooan dağıtmaya başlamadan [Azure kapsayıcı hizmeti](https://azure.microsoft.com/documentation/services/container-service/) küme.

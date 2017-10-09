---
title: "aaaAzure kapsayıcı örnekleri Öğreticisi - app dağıtma | Microsoft Docs"
description: "Azure kapsayıcı örnekleri Öğreticisi - app dağıtma"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Kapsayıcı tooAzure kapsayıcı örnekleri dağıtma

Merhaba budur üç bölümlük öğreticinin son. Önceki bölümlerde [bir kapsayıcı görüntüsü oluşturuldu](container-instances-tutorial-prepare-app.md) ve [tooan Azure kapsayıcı kayıt defteri gönderilen](container-instances-tutorial-prepare-acr.md). Bu bölümde, hello kapsayıcı tooAzure kapsayıcı örnekleri dağıtarak hello öğretici tamamlar. Tamamlanan adımları içerir:

> [!div class="checklist"]
> * Bir Azure Resource Manager şablonu kullanarak bir kapsayıcı grubu tanımlama
> * Hello Azure CLI kullanarak hello kapsayıcı grubu dağıtma
> * Kapsayıcı günlükleri görüntüleme

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Hello Azure CLI kullanarak hello kapsayıcı dağıtma

Hello Azure CLI tek bir komut bir kapsayıcı tooAzure kapsayıcı örnekleri dağıtımını sağlar. Merhaba kapsayıcı görüntü barındırılan beri içinde özel Azure kapsayıcı kayıt defteri Merhaba, hello kimlik bilgileri gerekli tooaccess içermelidir. Gerekirse, aşağıda gösterildiği gibi bunları sorgulayabilirsiniz.

Kapsayıcı kayıt defteri oturum açma sunucusu (kayıt defteri adınızı güncelleştirmesiyle):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Kapsayıcı kayıt defteri parola:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy kapsayıcı görüntünüzü bir kaynakla hello kapsayıcı kayıt defterinden 1 CPU Çekirdeği ve 1 GB bellek, komutu aşağıdaki hello çalıştırma isteği:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Birkaç saniye içinde Azure Kaynak Yöneticisi'nden bir ilk yanıtı alırsınız. tooview hello durumu hello dağıtımının kullanın:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Biz hello durumu değişiklikleri kadar bu komut çalışmaya devam *bekleyen* çok*çalıştıran*. Ardından biz geçebilirsiniz.

## <a name="view-hello-application-and-container-logs"></a>Merhaba uygulama ve kapsayıcı günlüklerini görüntüle

Merhaba dağıtım başarılı olduktan sonra komutu aşağıdaki hello hello çıktıda gösterilen tarayıcı toohello IP adresiniz açın:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world hello tarayıcı uygulamasında][aci-app-browser]

Merhaba kapsayıcı hello günlük çıktısı de görüntüleyebilirsiniz:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Çıktı:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, kapsayıcıları tooAzure kapsayıcı örnekleri dağıtma hello işlemi tamamlandı. Aşağıdaki adımları hello tamamlandı:

> [!div class="checklist"]
> * Azure CLI hello Azure kapsayıcı kayıt defteri hello kullanarak hello kapsayıcı dağıtma
> * Merhaba uygulaması hello tarayıcıda görüntüleme
> * Görüntüleme hello kapsayıcı günlükleri

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

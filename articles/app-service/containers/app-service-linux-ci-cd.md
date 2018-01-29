---
title: "Docker kapsayıcısı kayıt defterinden sürekli dağıtımı kapsayıcıları - Azure için Web uygulaması ile | Microsoft Docs"
description: "Web uygulaması için kapsayıcıları bir Docker kapsayıcısı kayıt defteri Kurulum sürekli dağıtım nasıl."
keywords: Azure uygulama hizmeti, linux, docker, acr, oss
services: app-service
documentationcenter: 
author: ahmedelnably
manager: cfowler
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: cccbd4952c66d3d8140e2a03e3b76afaa5ba3fbf
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/25/2017
---
# <a name="continuous-deployment-with-web-app-for-containers"></a>Kapsayıcıları için Web uygulaması ile sürekli dağıtımı

Bu öğreticide, yapılandırdığınız yönetilen özel kapsayıcı görüntüden için sürekli dağıtım [Azure kapsayıcı kayıt defteri](https://azure.microsoft.com/services/container-registry/) depoları veya [Docker hub'a](https://hub.docker.com).

## <a name="sign-in-to-azure"></a>Azure'da oturum açma

Oturum [Azure portalı](https://portal.azure.com)

## <a name="enable-container-continuous-deployment-feature"></a>Kapsayıcı sürekli dağıtım özelliğini etkinleştir

Sürekli dağıtım özelliğini kullanarak etkinleştirebilirsiniz [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) ve aşağıdaki komutu yürütme

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
```

İçinde  **[Azure portal](https://portal.azure.com/)**, tıklatın **uygulama hizmeti** sayfanın sol seçeneği.

Docker hub'a sürekli dağıtımı için yapılandırmak istediğiniz, uygulamanızın adına tıklayın.

İçinde **uygulama ayarları**, denilen bir uygulama ekleyin `DOCKER_ENABLE_CI` değerle `true`.

![uygulama ayarı görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="prepare-webhook-url"></a>Web kancası URL'si hazırlama

Web kancası URL'si kullanarak elde edebilirsiniz [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) ve aşağıdaki komutu yürütme

```azurecli-interactive
az webapp deployment container show-cd-url -n sname1 -g rgname
```

Web kancası URL'si, aşağıdaki uç nokta içerecek şekilde gerekir: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Elde edebilirsiniz, `publishingusername` ve `publishingpwd` yayımlama profili Azure Portalı'nı kullanarak web uygulamasını yükleyerek.

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="add-a-web-hook"></a>Bir web kancası ekleme

### <a name="azure-container-registry"></a>Azure Container Kayıt Defteri

Kayıt defteri portal dikey penceresinde, tıklayın **Kancalarını**, tıklatarak yeni bir Web kancası oluşturma **Ekle**. İçinde **Web kancası oluşturma** dikey penceresinde, Web kancası bir ad verin. Web kancası URI'sini elde URL sağlamanız gerekir. **3. adım**

Kapsayıcı görüntüsünü içeren depo kapsamını tanımlamak emin olun.

![Web kancası görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Görüntü güncelleştirilir, web uygulaması otomatik olarak güncelleştirilen sahip yeni bir görüntü.

### <a name="docker-hub"></a>Docker hub'a

Docker hub'a sayfanızı tıklatın **Kancalarını**, ardından **bir Web KANCASI oluşturma**.

![Web kancası 1 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Web kancası URL'si, alınan URL sağlamanız gerekir. **3. adım**

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Görüntü güncelleştirilir, web uygulaması otomatik olarak güncelleştirilen sahip yeni bir görüntü.

## <a name="next-steps"></a>Sonraki adımlar

* [Linux üzerinde Azure App Service nedir?](./app-service-linux-intro.md)
* [Azure kapsayıcı kayıt defteri](https://azure.microsoft.com/services/container-registry/)
* [Azure uygulama hizmetinde Linux'ta .NET Core kullanma](quickstart-dotnetcore.md)
* [Azure uygulama hizmetinde Linux'ta Ruby kullanma](quickstart-ruby.md)
* [Kapsayıcıları için Web uygulaması için özel bir Docker görüntü kullanma](quickstart-custom-docker-image.md)
* [Azure App Service Web uygulaması için kapsayıcı SSS](./app-service-linux-faq.md)
* [Web uygulaması için Azure CLI 2.0 kullanarak kapsayıcıları yönetme](./app-service-linux-cli.md)
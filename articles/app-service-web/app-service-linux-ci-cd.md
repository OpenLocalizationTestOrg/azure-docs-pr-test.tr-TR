---
title: "aaaContinuous Linux Azure Web uygulaması ile dağıtımı | Microsoft Docs"
description: "Nasıl Linux Azure Web uygulamasında sürekli dağıtım toosetup."
keywords: Azure uygulama hizmeti, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Bu öğreticide, yapılandırdığınız yönetilen özel kapsayıcı görüntüden için sürekli dağıtım [Azure kapsayıcı kayıt defteri](https://azure.microsoft.com/en-us/services/container-registry/) depoları veya [Docker hub'a](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>1. adım - oturum açma tooAzure

İçinde toohello http://portal.azure.com Azure portalında oturum açın

## <a name="step-2---enable-container-continuous-deployment-feature"></a>2. adım - etkinleştirme kapsayıcı sürekli dağıtım özelliği

Merhaba sürekli dağıtım özelliğini kullanarak etkinleştirebilirsiniz [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ve komut aşağıdaki hello yürütme

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

Merhaba,  **[Azure portal](https://portal.azure.com/)**, hello tıklatın **uygulama hizmeti** hello sayfasının hello soldaki seçeneği.

Uygulamanızın tooconfigure Docker hub'a sürekli dağıtımı için istediğiniz hello adına tıklayın.

Merhaba, **uygulama ayarları**, denilen bir uygulama ekleyin `DOCKER_ENABLE_CI` hello değerle `true`.

![uygulama ayarı görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>3. adım - Web kancası URL'si hazırlama

Web kancası URL'si hello kullanarak elde edebilirsiniz [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ve komut aşağıdaki hello yürütme

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Hello Web kancası URL'si için uç nokta aşağıdaki toohave hello gerekir: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Elde edebilirsiniz, `publishingusername` ve `publishingpwd` yayımlama hello Azure portal kullanarak profili hello web uygulamasını yükleyerek.

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>4. adım - bir web kancası ekleme

### <a name="azure-container-registry"></a>Azure Container Kayıt Defteri

Kayıt defteri portal dikey penceresinde, tıklayın **Kancalarını**, tıklatarak yeni bir Web kancası oluşturma **Ekle**. Merhaba, **Web kancası oluşturma** dikey penceresinde, Web kancası bir ad verin. Hello Web kancası URI tooprovide hello URL alınan ihtiyacınız **3. adım**

Kapsayıcı görüntüsünü içeren depo hello gibi hello kapsamını tanımlamak emin olun.

![Web kancası görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Merhaba görüntüsü güncelleştirildiğinde, bu hello web uygulaması otomatik olarak güncelleştirilen hello yeni görüntüsüyle.

### <a name="docker-hub"></a>Docker hub'a

Docker hub'a sayfanızı tıklatın **Kancalarını**, ardından **bir Web KANCASI oluşturma**.

![Web kancası 1 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Hello Web kancası URL'si için tooprovide hello URL alınan ihtiyacınız **3. adım**

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Merhaba görüntüsü güncelleştirildiğinde, bu hello web uygulaması otomatik olarak güncelleştirilen hello yeni görüntüsüyle.

## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Azure Web uygulaması nedir?](./app-service-linux-intro.md)
* [Azure kapsayıcı kayıt defteri](https://azure.microsoft.com/en-us/services/container-registry/)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](app-service-linux-using-nodejs-pm2.md)
* [.NET Core Linux Azure Web uygulamasında kullanma](app-service-linux-using-dotnetcore.md)
* [Ruby Linux Azure Web uygulamasında kullanma](app-service-linux-ruby-get-started.md)
* [Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü](./app-service-linux-using-custom-docker-image.md)
* [Azure App Service Web uygulaması Linux SSS](./app-service-linux-faq.md) 
* [Web uygulaması Azure CLI 2.0 kullanarak Linux üzerinde yönetme](./app-service-linux-cli.md)




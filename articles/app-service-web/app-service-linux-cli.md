---
title: "aaaManage Azure CLI 2.0 kullanarak Linux üzerinde Web uygulaması | Microsoft Docs"
description: "Web uygulaması Azure CLI kullanarak Linux'ta yönetin."
keywords: "Azure uygulama hizmeti, web uygulaması, CLI, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Web uygulaması Linux Azure CLI kullanarak yönetme

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Mümkün toocreate olan bu makalede Hello komutları kullanarak ve bir Web uygulaması Azure CLI 2.0 kullanarak Linux'ta yönetebilirsiniz.
İki yolla hello CLI'ın yeni sürümü hello kullanarak başlatabilirsiniz:

* [Azure CLI 2.0 yükleme](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde.
* Kullanarak [Azure bulut Kabuğu (Önizleme)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Linux uygulama hizmeti planı oluştur

toocreate bir Linux uygulama hizmeti planı, komutu aşağıdaki hello kullanabilirsiniz:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Özel bir Docker kapsayıcısı Web uygulaması oluşturma

toocreate bir web uygulaması ve toorun özel bir Docker kapsayıcısı yapılandırma, komutu aşağıdaki hello kullanabilirsiniz:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Merhaba Docker kapsayıcısı günlüğe kaydetmeyi etkinleştirmek

tooactivate Docker kapsayıcısı günlük Merhaba, komutu aşağıdaki hello kullanabilirsiniz:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Var olan bir Web uygulamasının Linux uygulama üzerinde değişiklik hello özel Docker kapsayıcısı

toochange görüntüden hello geçerli Docker görüntü tooa yeni, önceden oluşturulmuş bir uygulama hello aşağıdaki komutu kullanabilirsiniz:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Özel bir kayıt defterinden Docker görüntüleri kullanma

Uygulama toouse görüntülerinizi özel bir kayıt defteri yapılandırabilirsiniz. Kayıt defteri, kullanıcı adı ve parola tooprovide hello url gerekir. Bu komutu aşağıdaki hello kullanarak yapabiliriz:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Özel Docker görüntüleri için sürekli dağıtımı etkinleştirme

Komutu aşağıdaki hello ile Merhaba CD işlevselliğini etkinleştirmek ve hello Web kancası URL'si alın. Bu url, DockerHub ya da Azure kapsayıcı kayıt depoları kullanılan tooconfigure olabilir.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Linux uygulamasını bizim yerleşik çalışma zamanı çerçeveleri birini kullanarak bir Web uygulaması oluşturma

toocreate Linux komutu aşağıdaki hello kullanmak, uygulama üzerinde bir PHP 5.6 Web uygulaması.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Linux uygulamada var olan bir Web uygulaması için framework sürümünü Değiştir

toochange hello geçerli framework sürümü tooNode.js 6.11, bir önceden oluşturulmuş uygulamadan hello aşağıdaki komutu kullanabilirsiniz:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Web uygulamanız için Git dağıtımları ayarlama

tooset Git dağıtımların uygulamanız için komutu aşağıdaki hello kullanabilirsiniz:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Azure Web uygulaması nedir?](app-service-linux-intro.md)
* [Azure CLI 2.0 yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure bulut Kabuğu (Önizleme)](../cloud-shell/overview.md)
* [Hazırlık Azure App Service ortamları ayarlama](./web-sites-staged-publishing.md)
* [Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı](./app-service-linux-ci-cd.md)

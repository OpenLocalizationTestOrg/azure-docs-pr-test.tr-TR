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
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="f66db-104">Web uygulaması Linux Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="f66db-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="f66db-105">Mümkün toocreate olan bu makalede Hello komutları kullanarak ve bir Web uygulaması Azure CLI 2.0 kullanarak Linux'ta yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f66db-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="f66db-106">İki yolla hello CLI'ın yeni sürümü hello kullanarak başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="f66db-107">[Azure CLI 2.0 yükleme](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde.</span><span class="sxs-lookup"><span data-stu-id="f66db-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="f66db-108">Kullanarak [Azure bulut Kabuğu (Önizleme)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="f66db-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="f66db-109">Linux uygulama hizmeti planı oluştur</span><span class="sxs-lookup"><span data-stu-id="f66db-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="f66db-110">toocreate bir Linux uygulama hizmeti planı, komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="f66db-111">Özel bir Docker kapsayıcısı Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f66db-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="f66db-112">toocreate bir web uygulaması ve toorun özel bir Docker kapsayıcısı yapılandırma, komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="f66db-113">Merhaba Docker kapsayıcısı günlüğe kaydetmeyi etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="f66db-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="f66db-114">tooactivate Docker kapsayıcısı günlük Merhaba, komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="f66db-115">Var olan bir Web uygulamasının Linux uygulama üzerinde değişiklik hello özel Docker kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="f66db-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="f66db-116">toochange görüntüden hello geçerli Docker görüntü tooa yeni, önceden oluşturulmuş bir uygulama hello aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="f66db-117">Özel bir kayıt defterinden Docker görüntüleri kullanma</span><span class="sxs-lookup"><span data-stu-id="f66db-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="f66db-118">Uygulama toouse görüntülerinizi özel bir kayıt defteri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f66db-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="f66db-119">Kayıt defteri, kullanıcı adı ve parola tooprovide hello url gerekir.</span><span class="sxs-lookup"><span data-stu-id="f66db-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="f66db-120">Bu komutu aşağıdaki hello kullanarak yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="f66db-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="f66db-121">Özel Docker görüntüleri için sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f66db-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="f66db-122">Komutu aşağıdaki hello ile Merhaba CD işlevselliğini etkinleştirmek ve hello Web kancası URL'si alın.</span><span class="sxs-lookup"><span data-stu-id="f66db-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="f66db-123">Bu url, DockerHub ya da Azure kapsayıcı kayıt depoları kullanılan tooconfigure olabilir.</span><span class="sxs-lookup"><span data-stu-id="f66db-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="f66db-124">Linux uygulamasını bizim yerleşik çalışma zamanı çerçeveleri birini kullanarak bir Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f66db-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="f66db-125">toocreate Linux komutu aşağıdaki hello kullanmak, uygulama üzerinde bir PHP 5.6 Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f66db-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="f66db-126">Linux uygulamada var olan bir Web uygulaması için framework sürümünü Değiştir</span><span class="sxs-lookup"><span data-stu-id="f66db-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="f66db-127">toochange hello geçerli framework sürümü tooNode.js 6.11, bir önceden oluşturulmuş uygulamadan hello aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="f66db-128">Web uygulamanız için Git dağıtımları ayarlama</span><span class="sxs-lookup"><span data-stu-id="f66db-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="f66db-129">tooset Git dağıtımların uygulamanız için komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f66db-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="f66db-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f66db-130">Next steps</span></span>
* [<span data-ttu-id="f66db-131">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="f66db-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="f66db-132">Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="f66db-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="f66db-133">Azure bulut Kabuğu (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="f66db-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="f66db-134">Hazırlık Azure App Service ortamları ayarlama</span><span class="sxs-lookup"><span data-stu-id="f66db-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="f66db-135">Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="f66db-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

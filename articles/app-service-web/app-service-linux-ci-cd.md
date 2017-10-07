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
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="ab539-104">Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ab539-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="ab539-105">Bu öğreticide, yapılandırdığınız yönetilen özel kapsayıcı görüntüden için sürekli dağıtım [Azure kapsayıcı kayıt defteri](https://azure.microsoft.com/en-us/services/container-registry/) depoları veya [Docker hub'a](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="ab539-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="ab539-106">1. adım - oturum açma tooAzure</span><span class="sxs-lookup"><span data-stu-id="ab539-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="ab539-107">İçinde toohello http://portal.azure.com Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="ab539-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="ab539-108">2. adım - etkinleştirme kapsayıcı sürekli dağıtım özelliği</span><span class="sxs-lookup"><span data-stu-id="ab539-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="ab539-109">Merhaba sürekli dağıtım özelliğini kullanarak etkinleştirebilirsiniz [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ve komut aşağıdaki hello yürütme</span><span class="sxs-lookup"><span data-stu-id="ab539-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="ab539-110">Merhaba,  **[Azure portal](https://portal.azure.com/)**, hello tıklatın **uygulama hizmeti** hello sayfasının hello soldaki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ab539-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="ab539-111">Uygulamanızın tooconfigure Docker hub'a sürekli dağıtımı için istediğiniz hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab539-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="ab539-112">Merhaba, **uygulama ayarları**, denilen bir uygulama ekleyin `DOCKER_ENABLE_CI` hello değerle `true`.</span><span class="sxs-lookup"><span data-stu-id="ab539-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![uygulama ayarı görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="ab539-114">3. adım - Web kancası URL'si hazırlama</span><span class="sxs-lookup"><span data-stu-id="ab539-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="ab539-115">Web kancası URL'si hello kullanarak elde edebilirsiniz [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ve komut aşağıdaki hello yürütme</span><span class="sxs-lookup"><span data-stu-id="ab539-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="ab539-116">Hello Web kancası URL'si için uç nokta aşağıdaki toohave hello gerekir: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="ab539-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="ab539-117">Elde edebilirsiniz, `publishingusername` ve `publishingpwd` yayımlama hello Azure portal kullanarak profili hello web uygulamasını yükleyerek.</span><span class="sxs-lookup"><span data-stu-id="ab539-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="ab539-119">4. adım - bir web kancası ekleme</span><span class="sxs-lookup"><span data-stu-id="ab539-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="ab539-120">Azure Container Kayıt Defteri</span><span class="sxs-lookup"><span data-stu-id="ab539-120">Azure Container Registry</span></span>

<span data-ttu-id="ab539-121">Kayıt defteri portal dikey penceresinde, tıklayın **Kancalarını**, tıklatarak yeni bir Web kancası oluşturma **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ab539-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="ab539-122">Merhaba, **Web kancası oluşturma** dikey penceresinde, Web kancası bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="ab539-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="ab539-123">Hello Web kancası URI tooprovide hello URL alınan ihtiyacınız **3. adım**</span><span class="sxs-lookup"><span data-stu-id="ab539-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="ab539-124">Kapsayıcı görüntüsünü içeren depo hello gibi hello kapsamını tanımlamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab539-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![Web kancası görüntüsü Ekle](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="ab539-126">Merhaba görüntüsü güncelleştirildiğinde, bu hello web uygulaması otomatik olarak güncelleştirilen hello yeni görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="ab539-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="ab539-127">Docker hub'a</span><span class="sxs-lookup"><span data-stu-id="ab539-127">Docker Hub</span></span>

<span data-ttu-id="ab539-128">Docker hub'a sayfanızı tıklatın **Kancalarını**, ardından **bir Web KANCASI oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ab539-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Web kancası 1 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="ab539-130">Hello Web kancası URL'si için tooprovide hello URL alınan ihtiyacınız **3. adım**</span><span class="sxs-lookup"><span data-stu-id="ab539-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![Web kancası 2 ekleme görüntü ekleme](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="ab539-132">Merhaba görüntüsü güncelleştirildiğinde, bu hello web uygulaması otomatik olarak güncelleştirilen hello yeni görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="ab539-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab539-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab539-133">Next steps</span></span>
* [<span data-ttu-id="ab539-134">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="ab539-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="ab539-135">Azure kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="ab539-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="ab539-136">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="ab539-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="ab539-137">.NET Core Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="ab539-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="ab539-138">Ruby Linux Azure Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="ab539-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="ab539-139">Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü</span><span class="sxs-lookup"><span data-stu-id="ab539-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="ab539-140">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="ab539-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="ab539-141">Web uygulaması Azure CLI 2.0 kullanarak Linux üzerinde yönetme</span><span class="sxs-lookup"><span data-stu-id="ab539-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)




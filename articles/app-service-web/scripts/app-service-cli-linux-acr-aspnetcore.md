---
title: "Azure CLI betik örnek - bir ASP.NET Core web uygulaması Azure kapsayıcı kayıt defterinden Docker kapsayıcısı oluşturun. | Microsoft Docs"
description: "Azure CLI betik örnek - bir ASP.NET Core web uygulaması Azure kapsayıcı kayıt defterinden Docker kapsayıcısı oluşturun."
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="a9d04-103">Azure kapsayıcı kayıt defterinden Docker kapsayıcısı içinde bir ASP.NET Core web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9d04-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="a9d04-104">Bu senaryoda, bir kaynak grubu, Linux uygulama hizmeti planı ve web uygulaması oluşturun ve Azure kapsayıcı kayıt defterinden Docker kapsayıcısı kullanarak bir ASP.NET Core uygulama dağıtmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a9d04-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9d04-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9d04-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9d04-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9d04-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a9d04-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9d04-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a9d04-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a9d04-108">Sample script</span></span>

<span data-ttu-id="a9d04-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure kapsayıcı kayıt defteri")]</span><span class="sxs-lookup"><span data-stu-id="a9d04-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a9d04-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a9d04-110">Script explanation</span></span>

<span data-ttu-id="a9d04-111">Bu komut, bir kaynak grubu, web uygulaması ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9d04-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="a9d04-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="a9d04-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a9d04-113">Komut</span><span class="sxs-lookup"><span data-stu-id="a9d04-113">Command</span></span> | <span data-ttu-id="a9d04-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="a9d04-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9d04-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9d04-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a9d04-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9d04-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9d04-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9d04-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a9d04-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9d04-118">Creates an App Service plan.</span></span> <span data-ttu-id="a9d04-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="a9d04-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a9d04-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9d04-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a9d04-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9d04-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a9d04-122">az webapp yapılandırma kapsayıcısı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a9d04-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="a9d04-123">Azure web uygulaması için Docker kapsayıcısı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a9d04-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9d04-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9d04-124">Next steps</span></span>

<span data-ttu-id="a9d04-125">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9d04-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9d04-126">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a9d04-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

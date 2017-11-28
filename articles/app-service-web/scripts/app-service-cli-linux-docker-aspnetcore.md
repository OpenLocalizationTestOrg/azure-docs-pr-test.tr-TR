---
title: "aaaAzure CLI komut dosyası örneği - Docker kapsayıcısı içinde bir ASP.NET Core web uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - Docker kapsayıcısı içinde bir ASP.NET Core web uygulaması oluşturma"
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
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="fc497-103">Bir ASP.NET Core web uygulaması bir Docker kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc497-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="fc497-104">Bu senaryoda, nasıl toocreate bir kaynak grubu Linux app service planı ve web uygulaması ve bir Docker kapsayıcısı kullanarak bir ASP.NET Core uygulamayı dağıtmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fc497-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc497-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fc497-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fc497-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="fc497-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fc497-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc497-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="fc497-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fc497-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fc497-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fc497-109">Script explanation</span></span>

<span data-ttu-id="fc497-110">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması ve tüm ilişkili kaynakları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc497-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="fc497-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="fc497-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fc497-112">Komut</span><span class="sxs-lookup"><span data-stu-id="fc497-112">Command</span></span> | <span data-ttu-id="fc497-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="fc497-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc497-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc497-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc497-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc497-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc497-116">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc497-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fc497-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc497-117">Creates an App Service plan.</span></span> <span data-ttu-id="fc497-118">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="fc497-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fc497-119">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc497-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fc497-120">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc497-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fc497-121">az webapp yapılandırma kapsayıcısı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc497-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="fc497-122">Merhaba Docker kapsayıcısı'hello Azure web uygulaması için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="fc497-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc497-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc497-123">Next steps</span></span>

<span data-ttu-id="fc497-124">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc497-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc497-125">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc497-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

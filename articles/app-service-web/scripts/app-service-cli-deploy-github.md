---
title: "aaaAzure CLI komut dosyası örneği - github'dan dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - github'dan dağıtımı ile bir web uygulaması oluşturma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="3a7fb-103">Github'dan dağıtımı ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a7fb-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="3a7fb-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve web uygulama kodunuzdan (olmadan sürekli dağıtımı) genel bir GitHub depo dağıtır.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="3a7fb-105">Sürekli dağıtım GitHub dağıtımı için bkz: [github'dan sürekli dağıtımı ile bir web uygulaması oluşturma](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="3a7fb-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3a7fb-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3a7fb-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3a7fb-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3a7fb-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3a7fb-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3a7fb-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3a7fb-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3a7fb-110">Script explanation</span></span> 

<span data-ttu-id="3a7fb-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-111">This script uses hello following commands.</span></span> <span data-ttu-id="3a7fb-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3a7fb-113">Komut</span><span class="sxs-lookup"><span data-stu-id="3a7fb-113">Command</span></span> | <span data-ttu-id="3a7fb-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="3a7fb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a7fb-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a7fb-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3a7fb-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a7fb-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a7fb-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3a7fb-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3a7fb-119">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a7fb-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="3a7fb-120">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3a7fb-121">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="3a7fb-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="3a7fb-122">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="3a7fb-123">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="3a7fb-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="3a7fb-124">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="3a7fb-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a7fb-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a7fb-125">Next steps</span></span>

<span data-ttu-id="3a7fb-126">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a7fb-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a7fb-127">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3a7fb-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

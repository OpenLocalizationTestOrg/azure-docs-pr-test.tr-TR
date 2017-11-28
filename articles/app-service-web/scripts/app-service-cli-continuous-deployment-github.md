---
title: "aaaAzure CLI komut dosyası örneği - github'dan sürekli dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - github'dan sürekli dağıtımı ile bir web uygulaması oluşturma"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="0cbf8-103">Sürekli dağıtım github'dan bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cbf8-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="0cbf8-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve GitHub depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="0cbf8-105">Sürekli dağıtım olmadan GitHub dağıtımı için bkz: [bir web uygulaması oluşturma ve dağıtma github'dan kod](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="0cbf8-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="0cbf8-106">Bu örnekte, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0cbf8-106">In this sample, you will need:</span></span>

* <span data-ttu-id="0cbf8-107">Yönetici izinlerine sahip uygulama kodu, GitHub deposuyla.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="0cbf8-108">A [kişisel erişim belirteci (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) GitHub hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0cbf8-109">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0cbf8-110">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0cbf8-111">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0cbf8-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0cbf8-112">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0cbf8-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0cbf8-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0cbf8-113">Script explanation</span></span>

<span data-ttu-id="0cbf8-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-114">This script uses hello following commands.</span></span> <span data-ttu-id="0cbf8-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0cbf8-116">Komut</span><span class="sxs-lookup"><span data-stu-id="0cbf8-116">Command</span></span> | <span data-ttu-id="0cbf8-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="0cbf8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0cbf8-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cbf8-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0cbf8-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0cbf8-120">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cbf8-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0cbf8-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0cbf8-122">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cbf8-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0cbf8-123">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0cbf8-124">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="0cbf8-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="0cbf8-125">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="0cbf8-126">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="0cbf8-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="0cbf8-127">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="0cbf8-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0cbf8-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0cbf8-128">Next steps</span></span>

<span data-ttu-id="0cbf8-129">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0cbf8-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0cbf8-130">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0cbf8-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

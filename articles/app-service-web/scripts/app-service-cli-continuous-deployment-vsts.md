---
title: "aaaAzure CLI komut dosyası örneği - Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="c6a35-103">Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6a35-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="c6a35-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve ardından Visual Studio Team Services depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c6a35-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="c6a35-105">Bu örnek için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c6a35-105">For this sample, you will need:</span></span>

* <span data-ttu-id="c6a35-106">Yönetici izinlerine sahip uygulama koduna sahip bir Visual Studio Team Services deposu.</span><span class="sxs-lookup"><span data-stu-id="c6a35-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c6a35-107">A [kişisel erişim belirteci (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) Visual Studio Team Services hesabınızın.</span><span class="sxs-lookup"><span data-stu-id="c6a35-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c6a35-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c6a35-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6a35-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="c6a35-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c6a35-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c6a35-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c6a35-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c6a35-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c6a35-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c6a35-112">Script explanation</span></span>

<span data-ttu-id="c6a35-113">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6a35-113">This script uses hello following commands.</span></span> <span data-ttu-id="c6a35-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c6a35-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c6a35-115">Komut</span><span class="sxs-lookup"><span data-stu-id="c6a35-115">Command</span></span> | <span data-ttu-id="c6a35-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="c6a35-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6a35-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6a35-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c6a35-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6a35-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6a35-119">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6a35-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c6a35-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6a35-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c6a35-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6a35-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c6a35-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6a35-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c6a35-123">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c6a35-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c6a35-124">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c6a35-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c6a35-125">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="c6a35-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c6a35-126">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="c6a35-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6a35-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6a35-127">Next steps</span></span>

<span data-ttu-id="c6a35-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6a35-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6a35-129">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c6a35-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

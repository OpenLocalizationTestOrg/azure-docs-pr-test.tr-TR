---
title: "Azure CLI betik örnek - Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="859a8-103">Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="859a8-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="859a8-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve ardından Visual Studio Team Services depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="859a8-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="859a8-105">Bu örnek için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="859a8-105">For this sample, you will need:</span></span>

* <span data-ttu-id="859a8-106">Yönetici izinlerine sahip uygulama koduna sahip bir Visual Studio Team Services deposu.</span><span class="sxs-lookup"><span data-stu-id="859a8-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="859a8-107">A [kişisel erişim belirteci (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) Visual Studio Team Services hesabınızın.</span><span class="sxs-lookup"><span data-stu-id="859a8-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="859a8-108">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="859a8-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="859a8-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="859a8-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="859a8-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="859a8-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="859a8-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="859a8-111">Sample script</span></span>

<span data-ttu-id="859a8-112">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Visual Studio Team Services sürekli dağıtımı ile bir web uygulaması oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="859a8-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="859a8-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="859a8-113">Script explanation</span></span>

<span data-ttu-id="859a8-114">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="859a8-114">This script uses the following commands.</span></span> <span data-ttu-id="859a8-115">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="859a8-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="859a8-116">Komut</span><span class="sxs-lookup"><span data-stu-id="859a8-116">Command</span></span> | <span data-ttu-id="859a8-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="859a8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="859a8-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="859a8-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="859a8-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="859a8-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="859a8-120">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="859a8-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="859a8-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="859a8-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="859a8-122">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="859a8-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="859a8-123">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="859a8-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="859a8-124">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="859a8-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="859a8-125">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="859a8-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="859a8-126">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="859a8-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="859a8-127">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="859a8-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="859a8-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="859a8-128">Next steps</span></span>

<span data-ttu-id="859a8-129">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="859a8-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="859a8-130">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="859a8-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

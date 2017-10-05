---
title: "Azure CLI betik örnek - github'dan sürekli dağıtımı ile bir web uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="8b90a-103">Sürekli dağıtım github'dan bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b90a-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="8b90a-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve GitHub depodan sürekli dağıtım ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8b90a-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="8b90a-105">Sürekli dağıtım olmadan GitHub dağıtımı için bkz: [bir web uygulaması oluşturma ve dağıtma github'dan kod](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="8b90a-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="8b90a-106">Bu örnekte, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8b90a-106">In this sample, you will need:</span></span>

* <span data-ttu-id="8b90a-107">Yönetici izinlerine sahip uygulama kodu, GitHub deposuyla.</span><span class="sxs-lookup"><span data-stu-id="8b90a-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="8b90a-108">A [kişisel erişim belirteci (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) GitHub hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="8b90a-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b90a-109">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b90a-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8b90a-110">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8b90a-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="8b90a-111">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b90a-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8b90a-112">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8b90a-112">Sample script</span></span>

<span data-ttu-id="8b90a-113">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "github'dan sürekli dağıtımı ile bir web uygulaması oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="8b90a-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8b90a-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8b90a-114">Script explanation</span></span>

<span data-ttu-id="8b90a-115">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b90a-115">This script uses the following commands.</span></span> <span data-ttu-id="8b90a-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8b90a-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8b90a-117">Komut</span><span class="sxs-lookup"><span data-stu-id="8b90a-117">Command</span></span> | <span data-ttu-id="8b90a-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="8b90a-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8b90a-119">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b90a-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8b90a-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b90a-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8b90a-121">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b90a-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8b90a-122">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b90a-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8b90a-123">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b90a-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8b90a-124">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b90a-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8b90a-125">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="8b90a-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="8b90a-126">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="8b90a-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="8b90a-127">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="8b90a-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="8b90a-128">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="8b90a-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8b90a-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b90a-129">Next steps</span></span>

<span data-ttu-id="8b90a-130">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8b90a-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8b90a-131">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8b90a-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

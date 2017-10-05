---
title: "Azure CLI komut dosyası örneği - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="6cca2-103">Bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma</span><span class="sxs-lookup"><span data-stu-id="6cca2-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="6cca2-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve bir yerel Git deposu, web uygulama kodunuzda dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6cca2-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6cca2-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cca2-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6cca2-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6cca2-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6cca2-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6cca2-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6cca2-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6cca2-108">Sample script</span></span>

<span data-ttu-id="6cca2-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma")]</span><span class="sxs-lookup"><span data-stu-id="6cca2-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6cca2-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6cca2-110">Script explanation</span></span>

<span data-ttu-id="6cca2-111">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="6cca2-111">This script uses the following commands.</span></span> <span data-ttu-id="6cca2-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="6cca2-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6cca2-113">Komut</span><span class="sxs-lookup"><span data-stu-id="6cca2-113">Command</span></span> | <span data-ttu-id="6cca2-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="6cca2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6cca2-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cca2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6cca2-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cca2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6cca2-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cca2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6cca2-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cca2-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6cca2-119">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cca2-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6cca2-120">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cca2-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6cca2-121">az webapp dağıtım kullanıcısı ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="6cca2-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="6cca2-122">Hesap düzeyinde dağıtım kimlik bilgileri App Service için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6cca2-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="6cca2-123">az webapp dağıtım kaynağı config-yerel-git</span><span class="sxs-lookup"><span data-stu-id="6cca2-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="6cca2-124">Yerel bir Git deposu için bir kaynak denetimini yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6cca2-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="6cca2-125">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="6cca2-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="6cca2-126">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="6cca2-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6cca2-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6cca2-127">Next steps</span></span>

<span data-ttu-id="6cca2-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6cca2-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6cca2-129">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6cca2-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

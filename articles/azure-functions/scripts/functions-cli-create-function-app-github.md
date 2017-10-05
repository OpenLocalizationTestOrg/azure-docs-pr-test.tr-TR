---
title: "Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="06ad4-103">Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="06ad4-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="06ad4-104">Bu örnek komut dosyası kullanarak bir işlev uygulaması oluşturur [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve ortak bir GitHub deposuna (sürekli dağıtımı) olmadan işlev kodunuzdan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="06ad4-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="06ad4-105">İşlev kodu github'dan kesintisiz teslim okuma [bir işlev uygulaması oluşturma ve sürekli olarak Github'dan dağıtma](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="06ad4-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="06ad4-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06ad4-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="06ad4-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06ad4-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="06ad4-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06ad4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="06ad4-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="06ad4-109">Sample script</span></span>

<span data-ttu-id="06ad4-110">Bu örnek bir Azure işlevi uygulamasını oluşturur ve işlev kodu github'dan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="06ad4-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="06ad4-111">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "github'dan dağıtım ile işlev uygulaması oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="06ad4-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="06ad4-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="06ad4-112">Script explanation</span></span>

<span data-ttu-id="06ad4-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="06ad4-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="06ad4-114">Bu komut dosyasını aşağıdaki komutları kullanır:</span><span class="sxs-lookup"><span data-stu-id="06ad4-114">This script uses the following commands:</span></span>

| <span data-ttu-id="06ad4-115">Komut</span><span class="sxs-lookup"><span data-stu-id="06ad4-115">Command</span></span> | <span data-ttu-id="06ad4-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="06ad4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06ad4-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="06ad4-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="06ad4-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06ad4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06ad4-119">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06ad4-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="06ad4-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06ad4-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="06ad4-121">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="06ad4-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="06ad4-122">Bir Azure işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06ad4-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="06ad4-123">az appservice web kaynak denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06ad4-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="06ad4-124">Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="06ad4-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06ad4-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06ad4-125">Next steps</span></span>

<span data-ttu-id="06ad4-126">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06ad4-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="06ad4-127">Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="06ad4-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>

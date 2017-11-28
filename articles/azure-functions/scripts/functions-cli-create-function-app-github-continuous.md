---
title: "bir işlev uygulaması aaaCreate ve işlev kodu github'dan dağıtma | Microsoft Docs"
description: "Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="240f8-103">Bir uygulama hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="240f8-103">Create an App Service</span></span>

<span data-ttu-id="240f8-104">Bu örnek betik hello kullanarak bir işlev uygulaması oluşturur [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve sürekli olarak GitHub deposunu işlevi kodunuzdan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="240f8-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="240f8-105">Bu örnekte, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="240f8-105">In this sample, you need:</span></span>

* <span data-ttu-id="240f8-106">Yönetici izinlerine sahip işlevleri kodu, GitHub deposuyla.</span><span class="sxs-lookup"><span data-stu-id="240f8-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="240f8-107">A [kişisel erişim belirteci (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) GitHub hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="240f8-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="240f8-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="240f8-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="240f8-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="240f8-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="240f8-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="240f8-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="240f8-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="240f8-111">Sample script</span></span>

<span data-ttu-id="240f8-112">Bu örnek bir Azure işlevi uygulamasını oluşturur ve işlev kodu github'dan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="240f8-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="240f8-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="240f8-113">Script explanation</span></span>

<span data-ttu-id="240f8-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="240f8-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="240f8-115">Bu komut dosyası hello şunları kullanır:</span><span class="sxs-lookup"><span data-stu-id="240f8-115">This script uses hello following:</span></span>

| <span data-ttu-id="240f8-116">Komut</span><span class="sxs-lookup"><span data-stu-id="240f8-116">Command</span></span> | <span data-ttu-id="240f8-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="240f8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="240f8-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="240f8-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="240f8-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="240f8-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="240f8-120">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="240f8-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="240f8-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="240f8-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="240f8-122">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="240f8-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="240f8-123">az appservice web kaynak denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="240f8-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="240f8-124">Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="240f8-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="240f8-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="240f8-125">Next steps</span></span>

<span data-ttu-id="240f8-126">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="240f8-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="240f8-127">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="240f8-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>

---
title: "bir işlev uygulaması aaaCreate ve işlev kodu github'dan dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="1aae0-103">Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="1aae0-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="1aae0-104">Bu örnek betik hello kullanarak bir işlev uygulaması oluşturur [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve ortak bir GitHub deposuna (sürekli dağıtımı) olmadan işlev kodunuzdan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="1aae0-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="1aae0-105">İşlev kodu github'dan kesintisiz teslim okuma [bir işlev uygulaması oluşturma ve sürekli olarak Github'dan dağıtma](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="1aae0-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1aae0-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1aae0-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1aae0-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="1aae0-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1aae0-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1aae0-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1aae0-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1aae0-109">Sample script</span></span>

<span data-ttu-id="1aae0-110">Bu örnek bir Azure işlevi uygulamasını oluşturur ve işlev kodu github'dan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="1aae0-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1aae0-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1aae0-111">Script explanation</span></span>

<span data-ttu-id="1aae0-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="1aae0-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="1aae0-113">Bu komut dosyası komutları aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="1aae0-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="1aae0-114">Komut</span><span class="sxs-lookup"><span data-stu-id="1aae0-114">Command</span></span> | <span data-ttu-id="1aae0-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="1aae0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1aae0-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1aae0-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1aae0-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1aae0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1aae0-118">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1aae0-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="1aae0-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1aae0-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1aae0-120">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="1aae0-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="1aae0-121">Bir Azure işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1aae0-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="1aae0-122">az appservice web kaynak denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1aae0-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="1aae0-123">Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="1aae0-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1aae0-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1aae0-124">Next steps</span></span>

<span data-ttu-id="1aae0-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1aae0-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1aae0-126">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1aae0-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>

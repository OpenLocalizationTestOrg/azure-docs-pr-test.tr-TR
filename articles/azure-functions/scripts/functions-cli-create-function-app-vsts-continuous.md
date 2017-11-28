---
title: "bir işlev uygulaması aaaCreate ve Visual Studio Team Services işlevi koddan dağıtma | Microsoft Docs"
description: "Bir işlev uygulaması oluşturma ve Visual Studio Team Services işlevi koddan dağıtma"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="09c9d-103">Bir uygulama hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="09c9d-103">Create an App Service</span></span>

<span data-ttu-id="09c9d-104">Bu senaryoda, nasıl işlevini kullanarak uygulama toocreate hello öğreneceksiniz [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve sürekli olarak bir Visual Studio Team Services (VSTS) deposu işlevi kodunuzdan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="09c9d-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="09c9d-105">Bu örnekte, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="09c9d-105">In this sample, you will need:</span></span>

* <span data-ttu-id="09c9d-106">VSTS deposu, yönetici izinlerine sahip işlevleri koda sahip.</span><span class="sxs-lookup"><span data-stu-id="09c9d-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="09c9d-107">A [kişisel erişim belirteci (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) GitHub hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="09c9d-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="09c9d-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09c9d-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="09c9d-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="09c9d-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="09c9d-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="09c9d-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="09c9d-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="09c9d-111">Sample script</span></span>

<span data-ttu-id="09c9d-112">Bu örnek bir Azure işlevi uygulamasını oluşturur ve Visual Studio Team Services işlevi koddan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="09c9d-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="09c9d-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="09c9d-113">Script explanation</span></span>

<span data-ttu-id="09c9d-114">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması, documentdb ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="09c9d-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="09c9d-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="09c9d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="09c9d-116">Komut</span><span class="sxs-lookup"><span data-stu-id="09c9d-116">Command</span></span> | <span data-ttu-id="09c9d-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="09c9d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="09c9d-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="09c9d-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="09c9d-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09c9d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="09c9d-120">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09c9d-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="09c9d-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09c9d-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="09c9d-122">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="09c9d-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="09c9d-123">az appservice web kaynak denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09c9d-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="09c9d-124">Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="09c9d-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09c9d-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09c9d-125">Next steps</span></span>

<span data-ttu-id="09c9d-126">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09c9d-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="09c9d-127">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="09c9d-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>

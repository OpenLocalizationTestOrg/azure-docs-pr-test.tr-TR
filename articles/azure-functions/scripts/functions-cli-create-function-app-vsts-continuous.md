---
title: "Bir işlev uygulaması oluşturma ve Visual Studio Team Services işlevi koddan dağıtma | Microsoft Docs"
description: "Bir işlev uygulaması oluşturma ve Visual Studio Team Services işlevi koddan dağıtma"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="8ff66-103">Bir uygulama hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ff66-103">Create an App Service</span></span>

<span data-ttu-id="8ff66-104">Bu senaryoda işlevini kullanarak uygulama oluşturma hakkında bilgi edineceksiniz [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve sürekli olarak bir Visual Studio Team Services (VSTS) deposu işlevi kodunuzdan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="8ff66-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="8ff66-105">Bu örnekte, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ff66-105">In this sample, you will need:</span></span>

* <span data-ttu-id="8ff66-106">VSTS deposu, yönetici izinlerine sahip işlevleri koda sahip.</span><span class="sxs-lookup"><span data-stu-id="8ff66-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="8ff66-107">A [kişisel erişim belirteci (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) GitHub hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="8ff66-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8ff66-108">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff66-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8ff66-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8ff66-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="8ff66-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ff66-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8ff66-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8ff66-111">Sample script</span></span>

<span data-ttu-id="8ff66-112">Bu örnek bir Azure işlevi uygulamasını oluşturur ve Visual Studio Team Services işlevi koddan dağıtır.</span><span class="sxs-lookup"><span data-stu-id="8ff66-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="8ff66-113">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure hizmeti")]</span><span class="sxs-lookup"><span data-stu-id="8ff66-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8ff66-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8ff66-114">Script explanation</span></span>

<span data-ttu-id="8ff66-115">Bu komut, bir kaynak grubu, web uygulaması, documentdb ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8ff66-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="8ff66-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8ff66-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8ff66-117">Komut</span><span class="sxs-lookup"><span data-stu-id="8ff66-117">Command</span></span> | <span data-ttu-id="8ff66-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="8ff66-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ff66-119">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ff66-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8ff66-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ff66-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8ff66-121">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ff66-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8ff66-122">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ff66-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8ff66-123">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ff66-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="8ff66-124">az appservice web kaynak denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ff66-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="8ff66-125">Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="8ff66-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ff66-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ff66-126">Next steps</span></span>

<span data-ttu-id="8ff66-127">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ff66-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8ff66-128">Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8ff66-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>

---
title: "aaaAzure CLI komut dosyası örneği - bir uygulama hizmeti planında bir işlev uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir uygulama hizmeti planında bir işlev uygulaması oluşturma"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="7a104-103">Bir uygulama hizmeti planında işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a104-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="7a104-104">Bu örnek betik işlevlerinizi için bir kapsayıcı olan bir Azure işlevi uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a104-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="7a104-105">Merhaba işlev uygulaması server kaynaklarınızı her zaman açıktır anlamına gelir adanmış bir uygulama hizmeti planı kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7a104-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7a104-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7a104-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7a104-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="7a104-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7a104-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7a104-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7a104-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7a104-109">Sample script</span></span>

<span data-ttu-id="7a104-110">Bu komut dosyası ayrılmış bir kullanarak bir Azure işlevi uygulamasını oluşturur [uygulama hizmeti planı](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="7a104-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7a104-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="7a104-111">Script explanation</span></span>

<span data-ttu-id="7a104-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="7a104-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="7a104-113">Bu komut dosyası komutları aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="7a104-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="7a104-114">Komut</span><span class="sxs-lookup"><span data-stu-id="7a104-114">Command</span></span> | <span data-ttu-id="7a104-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="7a104-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a104-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a104-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a104-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a104-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a104-118">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a104-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="7a104-119">Bir Azure Storage hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a104-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="7a104-120">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a104-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="7a104-121">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a104-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7a104-122">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a104-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="7a104-123">Bir Azure işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a104-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a104-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a104-124">Next steps</span></span>

<span data-ttu-id="7a104-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a104-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a104-126">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7a104-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>

---
title: "Azure CLI betik örnek - sunucusuz yürütme için bir işlev uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - sunucusuz yürütme için bir işlev uygulaması oluşturma"
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="201a2-103">Sunucusuz yürütme için bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="201a2-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="201a2-104">Bu örnek betik işlevlerinizi için bir kapsayıcı olan bir Azure işlevi uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="201a2-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="201a2-105">İşlev uygulaması kullanılarak oluşturulan [tüketim planı](../functions-scale.md#consumption-plan), olay denetimli sunucusuz iş yükleri için ideal olduğu.</span><span class="sxs-lookup"><span data-stu-id="201a2-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="201a2-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="201a2-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="201a2-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="201a2-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="201a2-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="201a2-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="201a2-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="201a2-109">Sample script</span></span>

<span data-ttu-id="201a2-110">Bir Azure işlevi uygulamasını kullanarak bu betiği oluşturur [tüketim planı](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="201a2-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="201a2-111">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "tüketim plan üzerinde bir Azure işlevi oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="201a2-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="201a2-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="201a2-112">Script explanation</span></span>

<span data-ttu-id="201a2-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="201a2-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="201a2-114">Bu komut dosyasını aşağıdaki komutları kullanır:</span><span class="sxs-lookup"><span data-stu-id="201a2-114">This script uses the following commands:</span></span>

| <span data-ttu-id="201a2-115">Komut</span><span class="sxs-lookup"><span data-stu-id="201a2-115">Command</span></span> | <span data-ttu-id="201a2-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="201a2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="201a2-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="201a2-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="201a2-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="201a2-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="201a2-119">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="201a2-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="201a2-120">Bir Azure Storage hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="201a2-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="201a2-121">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="201a2-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="201a2-122">Bir Azure işlevi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="201a2-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="201a2-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="201a2-123">Next steps</span></span>

<span data-ttu-id="201a2-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="201a2-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="201a2-125">Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="201a2-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>

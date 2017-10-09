---
title: "aaaAzure CLI komut dosyası örneği - sunucusuz yürütme için bir işlev uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="48e59-103">Sunucusuz yürütme için bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="48e59-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="48e59-104">Bu örnek betik işlevlerinizi için bir kapsayıcı olan bir Azure işlevi uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48e59-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="48e59-105">Merhaba işlev uygulaması hello kullanılarak oluşturulan [tüketim planı](../functions-scale.md#consumption-plan), olay denetimli sunucusuz iş yükleri için ideal olduğu.</span><span class="sxs-lookup"><span data-stu-id="48e59-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48e59-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="48e59-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48e59-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="48e59-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="48e59-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48e59-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="48e59-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="48e59-109">Sample script</span></span>

<span data-ttu-id="48e59-110">Bir Azure işlevi uygulamasına hello'ı kullanarak bu betiği oluşturur [tüketim planı](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="48e59-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="48e59-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="48e59-111">Script explanation</span></span>

<span data-ttu-id="48e59-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="48e59-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="48e59-113">Bu komut dosyası komutları aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="48e59-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="48e59-114">Komut</span><span class="sxs-lookup"><span data-stu-id="48e59-114">Command</span></span> | <span data-ttu-id="48e59-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="48e59-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="48e59-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="48e59-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="48e59-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48e59-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="48e59-118">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48e59-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="48e59-119">Bir Azure Storage hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48e59-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="48e59-120">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="48e59-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="48e59-121">Bir Azure işlevi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48e59-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="48e59-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48e59-122">Next steps</span></span>

<span data-ttu-id="48e59-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48e59-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="48e59-124">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="48e59-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>

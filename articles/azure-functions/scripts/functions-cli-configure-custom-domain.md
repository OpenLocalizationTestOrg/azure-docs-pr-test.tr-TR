---
title: "Azure CLI komut dosyası örneği - eşlemesi bir işlev uygulaması için özel bir etki alanı | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - eşlemesi bir işlev uygulaması Azure için özel bir etki alanı."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="23a31-103">Eşlemesi bir işlev uygulaması için özel bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="23a31-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="23a31-104">Bu örnek komut dosyası ile ilgili kaynaklar bir işlev uygulaması oluşturur ve ardından eşler `www.<yourdomain>` ona.</span><span class="sxs-lookup"><span data-stu-id="23a31-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="23a31-105">Özel bir etki alanına eşlemek için işlevi uygulamanıza bir uygulama hizmeti planı yer alan ve tüketim planı oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="23a31-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="23a31-106">Azure işlevleri yalnızca destekleyen bir A kaydı kullanarak özel bir etki alanı eşleme.</span><span class="sxs-lookup"><span data-stu-id="23a31-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="23a31-107">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23a31-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="23a31-108">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="23a31-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="23a31-109">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23a31-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="23a31-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="23a31-110">Sample script</span></span>

<span data-ttu-id="23a31-111">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "bir işlev uygulaması için özel bir etki alanı eşleme")]</span><span class="sxs-lookup"><span data-stu-id="23a31-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="23a31-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="23a31-112">Script explanation</span></span>

<span data-ttu-id="23a31-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="23a31-113">This script uses the following commands.</span></span> <span data-ttu-id="23a31-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="23a31-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="23a31-115">Komut</span><span class="sxs-lookup"><span data-stu-id="23a31-115">Command</span></span> | <span data-ttu-id="23a31-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="23a31-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="23a31-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="23a31-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="23a31-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="23a31-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="23a31-119">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="23a31-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="23a31-120">İşlev uygulaması tarafından gerekli bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="23a31-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="23a31-121">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="23a31-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="23a31-122">Özel etki alanını eşlemek için gerekli bir uygulama hizmeti planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="23a31-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="23a31-123">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="23a31-123">az functionapp create</span></span>]() | <span data-ttu-id="23a31-124">Bir işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="23a31-124">Creates a function app.</span></span> |
| [<span data-ttu-id="23a31-125">az appservice web yapılandırma ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="23a31-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="23a31-126">Özel bir etki alanı için bir işlev uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="23a31-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23a31-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23a31-127">Next steps</span></span>

<span data-ttu-id="23a31-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23a31-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="23a31-129">Ek işlevler CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine]().</span><span class="sxs-lookup"><span data-stu-id="23a31-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>

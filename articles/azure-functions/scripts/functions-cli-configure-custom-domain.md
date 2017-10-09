---
title: "aaaAzure CLI komut dosyası örneği - eşleme özel etki alanı tooa işlev uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - harita Azure özel etki alanı tooa işlevi uygulamada."
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="80378-103">Özel etki alanı tooa işlev uygulaması eşleme</span><span class="sxs-lookup"><span data-stu-id="80378-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="80378-104">Bu örnek komut dosyası ile ilgili kaynaklar bir işlev uygulaması oluşturur ve ardından eşler `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="80378-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="80378-105">toomap tooa özel etki alanı işlev uygulamanızı tüketim planı içinde değil, bir uygulama hizmeti planındaki oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="80378-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="80378-106">Azure işlevleri yalnızca destekleyen bir A kaydı kullanarak özel bir etki alanı eşleme.</span><span class="sxs-lookup"><span data-stu-id="80378-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="80378-107">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="80378-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="80378-108">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="80378-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="80378-109">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="80378-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="80378-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="80378-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="80378-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="80378-111">Script explanation</span></span>

<span data-ttu-id="80378-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="80378-112">This script uses hello following commands.</span></span> <span data-ttu-id="80378-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="80378-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80378-114">Komut</span><span class="sxs-lookup"><span data-stu-id="80378-114">Command</span></span> | <span data-ttu-id="80378-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="80378-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80378-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="80378-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="80378-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80378-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80378-118">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80378-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="80378-119">Merhaba işlevi uygulama tarafından gerekli bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80378-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="80378-120">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80378-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="80378-121">Bir uygulama hizmeti planı gerekli toomap özel bir etki alanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80378-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="80378-122">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="80378-122">az functionapp create</span></span>]() | <span data-ttu-id="80378-123">Bir işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80378-123">Creates a function app.</span></span> |
| [<span data-ttu-id="80378-124">az appservice web yapılandırma ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="80378-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="80378-125">Özel etki alanı tooa işlev uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="80378-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80378-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80378-126">Next steps</span></span>

<span data-ttu-id="80378-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80378-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="80378-128">Ek işlevler CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine]().</span><span class="sxs-lookup"><span data-stu-id="80378-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>

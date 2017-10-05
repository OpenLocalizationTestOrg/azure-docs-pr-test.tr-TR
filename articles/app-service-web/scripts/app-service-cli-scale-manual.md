---
title: "Azure CLI komut dosyası örneği - ölçek el ile Azure CLI 2.0 kullanan bir Web uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - ölçek el ile Azure CLI 2.0 kullanan bir Web uygulaması"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="b2025-103">Bir web uygulaması elle ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b2025-103">Scale a web app manually</span></span>

<span data-ttu-id="b2025-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı ve web uygulaması oluşturmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b2025-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="b2025-105">Ardından, uygulama hizmeti planı tek bir örnekten birden çok örneklerine ölçeklenir.</span><span class="sxs-lookup"><span data-stu-id="b2025-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b2025-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2025-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b2025-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b2025-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="b2025-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2025-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b2025-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b2025-109">Sample script</span></span>

<span data-ttu-id="b2025-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "el ile ölçek")]</span><span class="sxs-lookup"><span data-stu-id="b2025-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b2025-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b2025-111">Script explanation</span></span>

<span data-ttu-id="b2025-112">Bu komut, bir kaynak grubu, web uygulaması ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2025-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="b2025-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="b2025-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b2025-114">Komut</span><span class="sxs-lookup"><span data-stu-id="b2025-114">Command</span></span> | <span data-ttu-id="b2025-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="b2025-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2025-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2025-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b2025-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2025-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b2025-118">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2025-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b2025-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2025-119">Creates an App Service plan.</span></span> <span data-ttu-id="b2025-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="b2025-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b2025-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2025-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b2025-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2025-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b2025-123">az uygulama hizmeti planı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b2025-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="b2025-124">Uygulama hizmeti planının özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b2025-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2025-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2025-125">Next steps</span></span>

<span data-ttu-id="b2025-126">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2025-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b2025-127">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2025-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

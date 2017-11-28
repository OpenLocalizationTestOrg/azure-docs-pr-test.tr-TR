---
title: "aaaAzure CLI komut dosyası örneği - Azure CLI 2.0 kullanarak el ile bir Web uygulaması ölçeklendirin | Microsoft Docs"
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
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="120d9-103">Bir web uygulaması elle ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="120d9-103">Scale a web app manually</span></span>

<span data-ttu-id="120d9-104">Bu senaryoda, bir kaynak grubu toocreate öğreneceksiniz uygulama hizmeti planı ve web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="120d9-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="120d9-105">Ardından hello App Service planı tek örnek toomultiple örneklerinden ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="120d9-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="120d9-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="120d9-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="120d9-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="120d9-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="120d9-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="120d9-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="120d9-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="120d9-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="120d9-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="120d9-110">Script explanation</span></span>

<span data-ttu-id="120d9-111">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması ve tüm ilişkili kaynakları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="120d9-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="120d9-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="120d9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="120d9-113">Komut</span><span class="sxs-lookup"><span data-stu-id="120d9-113">Command</span></span> | <span data-ttu-id="120d9-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="120d9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="120d9-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="120d9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="120d9-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="120d9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="120d9-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="120d9-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="120d9-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="120d9-118">Creates an App Service plan.</span></span> <span data-ttu-id="120d9-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="120d9-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="120d9-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="120d9-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="120d9-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="120d9-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="120d9-122">az uygulama hizmeti planı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="120d9-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="120d9-123">Uygulama hizmeti planı hello özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="120d9-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="120d9-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="120d9-124">Next steps</span></span>

<span data-ttu-id="120d9-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="120d9-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="120d9-126">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="120d9-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

---
title: "aaaAzure CLI komut dosyası örneği - harita bir özel etki alanı tooa web uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - harita bir özel etki alanı tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="e4a4c-103">Bir özel etki alanı tooa web uygulaması eşleme</span><span class="sxs-lookup"><span data-stu-id="e4a4c-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="e4a4c-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve ardından eşler `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e4a4c-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e4a4c-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e4a4c-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e4a4c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e4a4c-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e4a4c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e4a4c-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e4a4c-109">Script explanation</span></span>

<span data-ttu-id="e4a4c-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-110">This script uses hello following commands.</span></span> <span data-ttu-id="e4a4c-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e4a4c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="e4a4c-112">Command</span></span> | <span data-ttu-id="e4a4c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="e4a4c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4a4c-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a4c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e4a4c-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e4a4c-116">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a4c-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e4a4c-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e4a4c-118">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a4c-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e4a4c-119">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e4a4c-120">az webapp config ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="e4a4c-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="e4a4c-121">Bir özel etki alanı tooa web uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="e4a4c-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4a4c-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4a4c-122">Next steps</span></span>

<span data-ttu-id="e4a4c-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4a4c-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e4a4c-124">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e4a4c-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

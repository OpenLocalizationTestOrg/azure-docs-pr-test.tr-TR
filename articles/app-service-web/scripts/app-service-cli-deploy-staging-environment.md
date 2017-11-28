---
title: "aaaAzure CLI komut dosyası örneği - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="8ab7c-103">Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma</span><span class="sxs-lookup"><span data-stu-id="8ab7c-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="8ab7c-104">Bu örnek betik "Hazırlama" adlı bir ek dağıtım yuvası ile App Service'te bir web uygulaması oluşturur ve ardından "yuvası Hazırlama" örnek uygulama toohello dağıtır.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8ab7c-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8ab7c-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8ab7c-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ab7c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8ab7c-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8ab7c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8ab7c-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8ab7c-109">Script explanation</span></span>

<span data-ttu-id="8ab7c-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-110">This script uses hello following commands.</span></span> <span data-ttu-id="8ab7c-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8ab7c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="8ab7c-112">Command</span></span> | <span data-ttu-id="8ab7c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="8ab7c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ab7c-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ab7c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8ab7c-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8ab7c-116">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ab7c-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8ab7c-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8ab7c-118">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ab7c-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8ab7c-119">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8ab7c-120">az webapp dağıtım yuvası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ab7c-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="8ab7c-121">Bir dağıtım yuvası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="8ab7c-122">az webapp dağıtım kaynağı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="8ab7c-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="8ab7c-123">Azure web uygulaması Git veya Mercurial deposu ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="8ab7c-124">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="8ab7c-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="8ab7c-125">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="8ab7c-126">az webapp dağıtım yuvası takas</span><span class="sxs-lookup"><span data-stu-id="8ab7c-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="8ab7c-127">Belirtilen dağıtım yuvası üretime değiştirme.</span><span class="sxs-lookup"><span data-stu-id="8ab7c-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ab7c-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ab7c-128">Next steps</span></span>

<span data-ttu-id="8ab7c-129">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ab7c-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8ab7c-130">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8ab7c-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

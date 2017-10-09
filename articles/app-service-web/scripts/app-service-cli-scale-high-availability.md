---
title: "aaaAzure CLI komut dosyası örneği - bir web uygulaması dünya çapında yüksek availabilty mimarisi ile ölçeklendirin | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - ölçek yüksek availabilty mimarisiyle dünya çapında bir web uygulaması"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="452c2-103">Bir web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="452c2-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="452c2-104">Bu senaryoda, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="452c2-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="452c2-105">Merhaba alıştırma tamamlandıktan sonra bir yüksek kullanılabilir olacaktır sağlayan mimari hello en düşük ağ gecikmesine bağlı, web uygulamanızın genel kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="452c2-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="452c2-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="452c2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="452c2-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="452c2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="452c2-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="452c2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="452c2-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="452c2-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="452c2-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="452c2-110">Script explanation</span></span>

<span data-ttu-id="452c2-111">Bu komut dosyasını aşağıdaki komutları toocreate bir kaynak grubu, web uygulaması, trafik Yöneticisi profili hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="452c2-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="452c2-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="452c2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="452c2-113">Komut</span><span class="sxs-lookup"><span data-stu-id="452c2-113">Command</span></span> | <span data-ttu-id="452c2-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="452c2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="452c2-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="452c2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="452c2-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="452c2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="452c2-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="452c2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="452c2-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="452c2-118">Creates an App Service plan.</span></span> <span data-ttu-id="452c2-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="452c2-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="452c2-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="452c2-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="452c2-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="452c2-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="452c2-122">az ağ trafik Yöneticisi profili oluştur</span><span class="sxs-lookup"><span data-stu-id="452c2-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="452c2-123">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="452c2-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="452c2-124">az ağ trafik Yöneticisi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="452c2-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="452c2-125">Uç nokta tooan Azure trafik Yöneticisi profili ekler.</span><span class="sxs-lookup"><span data-stu-id="452c2-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="452c2-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="452c2-126">Next steps</span></span>

<span data-ttu-id="452c2-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="452c2-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="452c2-128">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="452c2-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

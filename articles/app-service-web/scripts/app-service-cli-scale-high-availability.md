---
title: "Azure CLI komut dosyası örneği - ölçek yüksek availabilty mimarisiyle dünya çapında bir web uygulaması | Microsoft Docs"
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
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="8464d-103">Bir web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="8464d-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="8464d-104">Bu senaryoda, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8464d-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="8464d-105">Alıştırma tamamlandıktan sonra bir yüksek kullanılabilir olacaktır sağlayan mimari web uygulamanızın üzerinde en düşük ağ gecikmesini genel kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="8464d-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8464d-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8464d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8464d-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8464d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="8464d-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8464d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="8464d-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8464d-109">Sample script</span></span>

<span data-ttu-id="8464d-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "coğrafi ölçek")]</span><span class="sxs-lookup"><span data-stu-id="8464d-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8464d-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8464d-111">Script explanation</span></span>

<span data-ttu-id="8464d-112">Bu komut, bir kaynak grubu, web uygulaması, trafik Yöneticisi profili ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8464d-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="8464d-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8464d-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8464d-114">Komut</span><span class="sxs-lookup"><span data-stu-id="8464d-114">Command</span></span> | <span data-ttu-id="8464d-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="8464d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8464d-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8464d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8464d-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8464d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8464d-118">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8464d-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8464d-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8464d-119">Creates an App Service plan.</span></span> <span data-ttu-id="8464d-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="8464d-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8464d-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="8464d-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8464d-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8464d-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8464d-123">az ağ trafik Yöneticisi profili oluştur</span><span class="sxs-lookup"><span data-stu-id="8464d-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="8464d-124">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8464d-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="8464d-125">az ağ trafik Yöneticisi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8464d-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="8464d-126">Bir uç noktası için bir Azure Traffic Manager profili ekler.</span><span class="sxs-lookup"><span data-stu-id="8464d-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8464d-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8464d-127">Next steps</span></span>

<span data-ttu-id="8464d-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8464d-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8464d-129">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8464d-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>

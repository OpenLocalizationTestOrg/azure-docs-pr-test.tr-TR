---
title: "aaaAzure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="5479f-103">Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="5479f-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="5479f-104">Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5479f-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="5479f-105">Merhaba uygulaması hello birincil bölgede kullanılamaz duruma geldiğinde traffic Manager trafik toohello uygulamada hello birincil bölge olarak tek bir bölge ve toohello ikincil bölge yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="5479f-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="5479f-106">Hello betiği yürütülürken önce hello mywebapp şeklindedir, MyWebAppL1 değiştirmeniz gerekir ve Azure arasında toounique değerleri MyWebAppL2 değerleri.</span><span class="sxs-lookup"><span data-stu-id="5479f-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="5479f-107">Hello komut dosyasını çalıştırdıktan sonra hello birincil bölge hello URL mywebapp.trafficmanager.net ile Merhaba uygulamasında erişebilir.</span><span class="sxs-lookup"><span data-stu-id="5479f-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5479f-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5479f-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="5479f-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="5479f-109">Clean up deployment</span></span> 

<span data-ttu-id="5479f-110">Merhaba komut dosyası örneği çalıştırdıktan sonra hello izleyin komutu kullanılan tooremove hello kaynak grubu, App Service uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="5479f-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5479f-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="5479f-111">Script explanation</span></span>

<span data-ttu-id="5479f-112">Bu komut dosyasını aşağıdaki komutları toocreate bir kaynak grubu, web uygulaması, trafik Yöneticisi profili hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5479f-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="5479f-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="5479f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5479f-114">Komut</span><span class="sxs-lookup"><span data-stu-id="5479f-114">Command</span></span> | <span data-ttu-id="5479f-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="5479f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5479f-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5479f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5479f-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5479f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5479f-118">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5479f-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5479f-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5479f-119">Creates an App Service plan.</span></span> <span data-ttu-id="5479f-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="5479f-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5479f-121">az appservice web oluşturma</span><span class="sxs-lookup"><span data-stu-id="5479f-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="5479f-122">Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5479f-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="5479f-123">az ağ trafik Yöneticisi profili oluştur</span><span class="sxs-lookup"><span data-stu-id="5479f-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="5479f-124">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5479f-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="5479f-125">az ağ trafik Yöneticisi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5479f-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="5479f-126">Uç nokta tooan Azure trafik Yöneticisi profili ekler.</span><span class="sxs-lookup"><span data-stu-id="5479f-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5479f-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5479f-127">Next steps</span></span>

<span data-ttu-id="5479f-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5479f-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5479f-129">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure ağ belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5479f-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>

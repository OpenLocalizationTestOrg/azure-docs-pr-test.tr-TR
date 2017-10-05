---
title: "Azure CLI komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme | Microsoft Docs"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="83011-103">Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="83011-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="83011-104">Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83011-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="83011-105">Birincil bölge uygulamada kullanılamadığında trafik Yöneticisi bir bölgede birincil bölge olarak uygulama ve ikincil bölge trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="83011-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="83011-106">Komut yürütülmeden önce Azure arasında benzersiz değerler mywebapp şeklindedir, MyWebAppL1 ve MyWebAppL2 değerleri değiştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="83011-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="83011-107">Betiği çalıştırdıktan sonra uygulama URL'si mywebapp.trafficmanager.net ile birincil bölgede erişebilir.</span><span class="sxs-lookup"><span data-stu-id="83011-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="83011-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="83011-108">Sample script</span></span>

<span data-ttu-id="83011-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "yüksek kullanılabilirlik için trafiği yönlendirmek")]</span><span class="sxs-lookup"><span data-stu-id="83011-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="83011-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="83011-110">Clean up deployment</span></span> 

<span data-ttu-id="83011-111">Komut dosyası örneği çalıştırdıktan sonra izleme komutu kaynak grubu, App Service uygulaması kaldırmak için kullanılabilir ve tüm kaynakları ilgili.</span><span class="sxs-lookup"><span data-stu-id="83011-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="83011-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="83011-112">Script explanation</span></span>

<span data-ttu-id="83011-113">Bu komut, bir kaynak grubu, web uygulaması, trafik Yöneticisi profili ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="83011-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="83011-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="83011-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="83011-115">Komut</span><span class="sxs-lookup"><span data-stu-id="83011-115">Command</span></span> | <span data-ttu-id="83011-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="83011-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="83011-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="83011-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="83011-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83011-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="83011-119">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="83011-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="83011-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83011-120">Creates an App Service plan.</span></span> <span data-ttu-id="83011-121">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="83011-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="83011-122">az appservice web oluşturma</span><span class="sxs-lookup"><span data-stu-id="83011-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="83011-123">Uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83011-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="83011-124">az ağ trafik Yöneticisi profili oluştur</span><span class="sxs-lookup"><span data-stu-id="83011-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="83011-125">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83011-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="83011-126">az ağ trafik Yöneticisi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="83011-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="83011-127">Bir uç noktası için bir Azure Traffic Manager profili ekler.</span><span class="sxs-lookup"><span data-stu-id="83011-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="83011-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83011-128">Next steps</span></span>

<span data-ttu-id="83011-129">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83011-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="83011-130">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure ağ belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="83011-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>

---
title: "Bir Azure Ağ İzleyicisi örneği oluşturma | Microsoft Docs"
description: "Bu sayfa portal ve Azure REST API'sini kullanarak Ağ İzleyicisi örneği oluşturmak için aşağıdaki adımları sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="5424a-103">Bir Azure Ağ İzleyicisi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="5424a-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="5424a-104">Ağ İzleyicisi İzleme ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure tanılama sağlayan bölgesel bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="5424a-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="5424a-105">Senaryo düzeyi izleme, bir uçtan uca ağ düzey görünümü adresindeki sorunlara tanı koymak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5424a-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="5424a-106">Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Azure ağınızdaki serisidir yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5424a-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5424a-107">Ağ İzleyicisi'ni şu anda yalnızca CLI 1.0 destekler gibi CLI 1.0 için yeni bir Ağ İzleyicisi örneği oluşturmak için yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5424a-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="5424a-108">Portalda bir Ağ İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5424a-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="5424a-109">Gidin **daha fazla hizmet** > **ağ** > **Ağ İzleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="5424a-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="5424a-110">Ağ İzleyicisi için etkinleştirmek istediğiniz tüm abonelikleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5424a-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="5424a-111">Bu eylem, kullanılabilir olan her bölgede bir Ağ İzleyicisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5424a-111">This action creates a Network Watcher in every region that is available.</span></span>

![Ağ İzleyicisi oluşturma][1]

<span data-ttu-id="5424a-113">Ağ İzleyicisi'ni Portalı'nı kullanarak etkinleştirdiğinizde, Ağ İzleyicisi örneğinin adını burada region_name örneği etkinleştirdiğiniz Azure bölgesine karşılık gelen NetworkWatcher_region_name otomatik olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5424a-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="5424a-114">Örneğin, Batı Orta ABD bölgesinde etkin bir Ağ İzleyicisi NetworkWatcher_westcentralus adlandırılır</span><span class="sxs-lookup"><span data-stu-id="5424a-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="5424a-115">Ayrıca, Ağ İzleyicisi örneği NetworkWatcherRG adlı bir kaynak grubuna otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="5424a-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="5424a-116">Bu kaynak grubu, zaten yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5424a-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="5424a-117">Bir Ağ İzleyicisi örneği ve kaynak grubu adını özelleştirmek istiyorsanız içine yerleştirildiğinde, aşağıda açıklanan Powershell, REST API veya ARMClient yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5424a-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="5424a-118">Ağ İzleyicisi'ni içine yerleştirmeden önce her seçenekte, kaynak grubu mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5424a-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="5424a-119">PowerShell ile bir Ağ İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5424a-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="5424a-120">Ağ İzleyicisi örneği oluşturmak için aşağıdaki örnekte çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5424a-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="5424a-121">Ağ İzleyicisi ile REST API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="5424a-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="5424a-122">ARMclient PowerShell kullanarak REST API'sini çağırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5424a-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="5424a-123">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="5424a-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="5424a-124">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="5424a-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="5424a-125">Ağ İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5424a-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="5424a-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5424a-126">Next steps</span></span>

<span data-ttu-id="5424a-127">Ağ İzleyicisi örneği sahip olduğunuza göre kullanılabilir özellikleri hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="5424a-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="5424a-128">Topoloji</span><span class="sxs-lookup"><span data-stu-id="5424a-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="5424a-129">Paket yakalama</span><span class="sxs-lookup"><span data-stu-id="5424a-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="5424a-130">IP akışı doğrulama</span><span class="sxs-lookup"><span data-stu-id="5424a-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="5424a-131">Sonraki atlama</span><span class="sxs-lookup"><span data-stu-id="5424a-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="5424a-132">Güvenlik grubu görünümü</span><span class="sxs-lookup"><span data-stu-id="5424a-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="5424a-133">NSG akış günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="5424a-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="5424a-134">Sanal ağ geçidi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="5424a-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="5424a-135">Ağ İzleyicisi örneği oluşturulduktan sonra paket yakalama makaleyi izleyerek yapılandırılabilir: [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="5424a-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png












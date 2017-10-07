---
title: "aaaCreate Azure Ağ İzleyicisi örneği | Microsoft Docs"
description: "Bu sayfa, hello portalı ve Azure REST API'sini kullanarak Ağ İzleyicisi örneği hello adımları toocreate sağlar"
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="57962-103">Bir Azure Ağ İzleyicisi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="57962-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="57962-104">Ağ İzleyicisi'ni ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure Tanılama, toomonitor sağlayan bölgesel bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="57962-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="57962-105">Senaryo düzeyi izleme bir bitiş tooend ağ düzey görünümü adresindeki toodiagnose sorunları sağlar.</span><span class="sxs-lookup"><span data-stu-id="57962-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="57962-106">Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="57962-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="57962-107">Ağ İzleyicisi'ni şu anda yalnızca CLI 1.0 destekler gibi hello yönergeleri toocreate CLI 1.0 için yeni bir Ağ İzleyicisi örnek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="57962-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="57962-108">Ağ İzleyicisi Merhaba Portalı'nda oluşturma</span><span class="sxs-lookup"><span data-stu-id="57962-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="57962-109">Çok gidin**daha Hizmetleri** > **ağ** > **Ağ İzleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="57962-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="57962-110">Ağ İzleyicisi tooenable istediğiniz tüm hello abonelikleri seçebilirsiniz için.</span><span class="sxs-lookup"><span data-stu-id="57962-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="57962-111">Bu eylem, kullanılabilir olan her bölgede bir Ağ İzleyicisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57962-111">This action creates a Network Watcher in every region that is available.</span></span>

![Ağ İzleyicisi oluşturma][1]

<span data-ttu-id="57962-113">Ağ İzleyicisi Merhaba Portal kullanarak etkinleştirdiğinizde hello hello Ağ İzleyicisi örneğinin adını otomatik olarak tooNetworkWatcher_region_name nerede region_name toohello Azure hello örneği etkinleştirdiğiniz bölge karşılık gelen ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="57962-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="57962-114">Örneğin, Batı Orta ABD bölgesinde etkin bir Ağ İzleyicisi NetworkWatcher_westcentralus adlandırılır</span><span class="sxs-lookup"><span data-stu-id="57962-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="57962-115">Ayrıca, hello Ağ İzleyicisi örneği NetworkWatcherRG adlı bir kaynak grubuna otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="57962-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="57962-116">Bu kaynak grubu, zaten yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57962-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="57962-117">Ağ İzleyicisi örneği ve hello toocustomize hello adı istiyorsanız içine yerleştirilen kaynak grubu, aşağıda açıklanan Powershell, hello REST API veya ARMClient yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57962-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="57962-118">Ağ İzleyicisi Merhaba içine yerleştirmeden önce her seçenekte, hello kaynak grubu mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57962-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="57962-119">PowerShell ile bir Ağ İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="57962-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="57962-120">toocreate Ağ İzleyicisi, aşağıdaki örneğine hello çalıştırmak örneği:</span><span class="sxs-lookup"><span data-stu-id="57962-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="57962-121">Ağ İzleyicisi Merhaba REST API ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="57962-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="57962-122">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="57962-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="57962-123">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="57962-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="57962-124">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="57962-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="57962-125">Merhaba Ağ İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="57962-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="57962-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57962-126">Next steps</span></span>

<span data-ttu-id="57962-127">Ağ İzleyicisi örneği sahip olduğunuza göre kullanılabilir hello özellikleri hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="57962-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="57962-128">Topoloji</span><span class="sxs-lookup"><span data-stu-id="57962-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="57962-129">Paket yakalama</span><span class="sxs-lookup"><span data-stu-id="57962-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="57962-130">IP akışı doğrulama</span><span class="sxs-lookup"><span data-stu-id="57962-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="57962-131">Sonraki atlama</span><span class="sxs-lookup"><span data-stu-id="57962-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="57962-132">Güvenlik grubu görünümü</span><span class="sxs-lookup"><span data-stu-id="57962-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="57962-133">NSG akış günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="57962-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="57962-134">Sanal ağ geçidi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="57962-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="57962-135">Paket yakalama Ağ İzleyicisi örneği oluşturulduktan sonra aşağıdaki hello makalesiyle yapılandırılabilir: [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="57962-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png












---
title: "Azure Ağ İzleyicisi topolojisi - PowerShell görüntülemek | Microsoft Docs"
description: "Bu makalede PowerShell ağ topolojinizi sorgulamak için nasıl kullanılacağını anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="0b6fd-103">PowerShell ile Ağ İzleyicisi topolojisini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="0b6fd-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0b6fd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b6fd-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="0b6fd-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b6fd-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="0b6fd-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b6fd-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="0b6fd-107">REST API</span><span class="sxs-lookup"><span data-stu-id="0b6fd-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="0b6fd-108">Ağ İzleyicisi'nin topoloji özelliği görsel bir abonelik ağ kaynaklarında sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="0b6fd-109">Portalda, bu görselleştirme için otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="0b6fd-110">Portal topoloji görünümünde ardındaki bilgiler PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="0b6fd-111">Bu özelliği olan topoloji bilgisi veri görselleştirmesi oluşturmak için diğer araçları tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="0b6fd-112">Bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="0b6fd-113">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="0b6fd-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="0b6fd-114">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="0b6fd-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="0b6fd-115">Topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="0b6fd-116">**ad** -kaynağın adı</span><span class="sxs-lookup"><span data-stu-id="0b6fd-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="0b6fd-117">**Kimliği** -kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="0b6fd-118">**Konum** -kaynağın bulunduğu konum.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="0b6fd-119">**ilişkileri** -başvurulan nesne ilişkilerini listesi.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="0b6fd-120">**ad** -başvurulan kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="0b6fd-121">**ResourceId** -ResourceId association'ında başvurulan kaynak URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="0b6fd-122">**associationType** -bu değer alt nesne ve üst arasındaki ilişkiyi başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="0b6fd-123">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0b6fd-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0b6fd-124">Before you begin</span></span>

<span data-ttu-id="0b6fd-125">Bu senaryoda, kullandığınız `Get-AzureRmNetworkWatcherTopology` topoloji bilgilerini almak üzere.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="0b6fd-126">Olduğundan ayrıca bir makale nasıl [ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="0b6fd-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="0b6fd-127">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="0b6fd-128">Senaryo</span><span class="sxs-lookup"><span data-stu-id="0b6fd-128">Scenario</span></span>

<span data-ttu-id="0b6fd-129">Bu makalede ele alınan senaryo belirtilen kaynak grubu için topoloji yanıtı alır.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="0b6fd-130">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="0b6fd-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="0b6fd-131">Ağ İzleyicisi örneği almak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="0b6fd-132">`$networkWatcher` Değişkeni iletilir `Get-AzureRmNetworkWatcherTopology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="0b6fd-133">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="0b6fd-133">Retrieve topology</span></span>

<span data-ttu-id="0b6fd-134">`Get-AzureRmNetworkWatcherTopology` Cmdlet'i, belirtilen kaynak grubu için topoloji alır.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="0b6fd-135">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="0b6fd-135">Results</span></span>

<span data-ttu-id="0b6fd-136">Döndürülen sonuçların bir özellik "json yanıt gövdesi için içeren adı" kaynaklarınız `Get-AzureRmNetworkWatcherTopology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="0b6fd-137">Yanıt ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="0b6fd-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="0b6fd-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b6fd-138">Next steps</span></span>

<span data-ttu-id="0b6fd-139">Ziyaret ederek NSG akış günlüklerinizi Power BI ile görselleştirme öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0b6fd-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



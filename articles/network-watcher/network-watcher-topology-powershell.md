---
title: "aaaView Azure Ağ İzleyicisi topolojisi - PowerShell | Microsoft Docs"
description: "Bu makalede anlatmaktadır nasıl toouse PowerShell tooquery ağ topolojinizi."
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
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="79968-103">PowerShell ile Ağ İzleyicisi topolojisini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="79968-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="79968-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79968-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="79968-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="79968-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="79968-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="79968-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="79968-107">REST API</span><span class="sxs-lookup"><span data-stu-id="79968-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="79968-108">Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="79968-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="79968-109">Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="79968-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="79968-110">Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="79968-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="79968-111">Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="79968-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="79968-112">Merhaba bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="79968-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="79968-113">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="79968-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="79968-114">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="79968-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="79968-115">Merhaba aşağıdaki hello topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="79968-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="79968-116">**ad** - hello hello kaynak adı</span><span class="sxs-lookup"><span data-stu-id="79968-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="79968-117">**Kimliği** -hello kaynak URI'si hello.</span><span class="sxs-lookup"><span data-stu-id="79968-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="79968-118">**Konum** -hello hello kaynak bulunduğu konumu.</span><span class="sxs-lookup"><span data-stu-id="79968-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="79968-119">**ilişkileri** -ilişkilendirmeleri toohello listesini başvurulan nesne.</span><span class="sxs-lookup"><span data-stu-id="79968-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="79968-120">**ad** -hello hello adını başvurulan kaynak.</span><span class="sxs-lookup"><span data-stu-id="79968-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="79968-121">**ResourceId** -hello ResourceId olduğu hello association'ında başvurulan hello kaynağının hello URI.</span><span class="sxs-lookup"><span data-stu-id="79968-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="79968-122">**associationType** -bu değer hello ilişkisi hello alt nesne hello üst başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="79968-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="79968-123">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="79968-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="79968-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="79968-124">Before you begin</span></span>

<span data-ttu-id="79968-125">Bu senaryoda, kullandığınız hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topoloji bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="79968-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="79968-126">Ayrıca bir makalesi vardır hakkında çok[ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="79968-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="79968-127">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="79968-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="79968-128">Senaryo</span><span class="sxs-lookup"><span data-stu-id="79968-128">Scenario</span></span>

<span data-ttu-id="79968-129">Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.</span><span class="sxs-lookup"><span data-stu-id="79968-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="79968-130">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="79968-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="79968-131">Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="79968-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="79968-132">Merhaba `$networkWatcher` değişkeni toohello geçirilen `Get-AzureRmNetworkWatcherTopology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="79968-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="79968-133">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="79968-133">Retrieve topology</span></span>

<span data-ttu-id="79968-134">Merhaba `Get-AzureRmNetworkWatcherTopology` cmdlet'i belirtilen kaynak grubu için hello topolojisini alır.</span><span class="sxs-lookup"><span data-stu-id="79968-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="79968-135">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="79968-135">Results</span></span>

<span data-ttu-id="79968-136">Merhaba döndürülen sonuçları bir özellik "Merhaba json yanıt gövdesine hello için içeren adı" kaynaklarınız `Get-AzureRmNetworkWatcherTopology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="79968-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="79968-137">Merhaba yanıt hello kaynaklarında hello ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) içerir.</span><span class="sxs-lookup"><span data-stu-id="79968-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="79968-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79968-138">Next steps</span></span>

<span data-ttu-id="79968-139">Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="79968-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



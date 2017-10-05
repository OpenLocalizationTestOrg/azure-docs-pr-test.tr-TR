---
title: "Azure Ağ İzleyicisi topolojisi - Azure CLI görüntülemek | Microsoft Docs"
description: "Bu makalede, Azure CLI ağ topolojinizi sorgulamak için nasıl kullanılacağını anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5be8e103f9a1f32117a4ed3be73bff021db1186d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="aaeba-103">Ağ İzleyicisi topolojisi Azure CLI ile görüntüleme</span><span class="sxs-lookup"><span data-stu-id="aaeba-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="aaeba-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaeba-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="aaeba-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aaeba-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="aaeba-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aaeba-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="aaeba-107">REST API</span><span class="sxs-lookup"><span data-stu-id="aaeba-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="aaeba-108">Ağ İzleyicisi'nin topoloji özelliği görsel bir abonelik ağ kaynaklarında sağlar.</span><span class="sxs-lookup"><span data-stu-id="aaeba-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="aaeba-109">Portalda, bu görselleştirme için otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="aaeba-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="aaeba-110">Portal topoloji görünümünde ardındaki bilgiler PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="aaeba-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="aaeba-111">Bu özelliği olan topoloji bilgisi veri görselleştirmesi oluşturmak için diğer araçları tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="aaeba-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="aaeba-112">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="aaeba-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="aaeba-113">Ağ İzleyicisi, CLI desteği şu anda Azure CLI 1.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="aaeba-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="aaeba-114">Bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="aaeba-114">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="aaeba-115">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="aaeba-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="aaeba-116">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="aaeba-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="aaeba-117">Topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="aaeba-117">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="aaeba-118">**ad** -kaynağın adı</span><span class="sxs-lookup"><span data-stu-id="aaeba-118">**name** - The name of the resource</span></span>
* <span data-ttu-id="aaeba-119">**Kimliği** -kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="aaeba-119">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="aaeba-120">**Konum** -kaynağın bulunduğu konum.</span><span class="sxs-lookup"><span data-stu-id="aaeba-120">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="aaeba-121">**ilişkileri** -başvurulan nesne ilişkilerini listesi.</span><span class="sxs-lookup"><span data-stu-id="aaeba-121">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="aaeba-122">**ad** -başvurulan kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="aaeba-122">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="aaeba-123">**ResourceId** -ResourceId association'ında başvurulan kaynak URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="aaeba-123">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="aaeba-124">**associationType** -bu değer alt nesne ve üst arasındaki ilişkiyi başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="aaeba-124">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="aaeba-125">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="aaeba-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aaeba-126">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="aaeba-126">Before you begin</span></span>

<span data-ttu-id="aaeba-127">Bu senaryoda, kullandığınız `network watcher topology` topoloji bilgilerini almak üzere.</span><span class="sxs-lookup"><span data-stu-id="aaeba-127">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="aaeba-128">Olduğundan ayrıca bir makale nasıl [ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="aaeba-128">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="aaeba-129">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="aaeba-129">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="aaeba-130">Senaryo</span><span class="sxs-lookup"><span data-stu-id="aaeba-130">Scenario</span></span>

<span data-ttu-id="aaeba-131">Bu makalede ele alınan senaryo belirtilen kaynak grubu için topoloji yanıtı alır.</span><span class="sxs-lookup"><span data-stu-id="aaeba-131">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="aaeba-132">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="aaeba-132">Retrieve topology</span></span>

<span data-ttu-id="aaeba-133">`network watcher topology` Cmdlet'i, belirtilen kaynak grubu için topoloji alır.</span><span class="sxs-lookup"><span data-stu-id="aaeba-133">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="aaeba-134">Bağımsız değişken Ekle "--json" json biçiminde oput görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="aaeba-134">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="aaeba-135">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="aaeba-135">Results</span></span>

<span data-ttu-id="aaeba-136">Döndürülen sonuçların bir özellik "json yanıt gövdesi için içeren adı" kaynaklarınız `network watcher topology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="aaeba-136">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="aaeba-137">Yanıt ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="aaeba-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="aaeba-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aaeba-138">Next steps</span></span>

<span data-ttu-id="aaeba-139">Ağ kaynaklarınıza ziyaret ederek uygulanan güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="aaeba-139">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>

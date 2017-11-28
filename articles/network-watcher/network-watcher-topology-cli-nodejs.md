---
title: "aaaView Azure Ağ İzleyicisi topolojisi - Azure CLI 1.0 | Microsoft Docs"
description: "Bu makalede anlatmaktadır nasıl toouse Azure CLI 1.0 tooquery ağ topolojinizi."
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
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="3ac08-103">Ağ İzleyicisi topolojisi Azure CLI 1.0 ile görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3ac08-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3ac08-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ac08-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="3ac08-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3ac08-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="3ac08-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3ac08-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="3ac08-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3ac08-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="3ac08-108">Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ac08-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="3ac08-109">Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="3ac08-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="3ac08-110">Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac08-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="3ac08-111">Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="3ac08-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="3ac08-112">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ac08-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="3ac08-113">Merhaba bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="3ac08-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="3ac08-114">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="3ac08-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="3ac08-115">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="3ac08-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="3ac08-116">Merhaba aşağıdaki hello topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ac08-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="3ac08-117">**ad** - hello hello kaynak adı</span><span class="sxs-lookup"><span data-stu-id="3ac08-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="3ac08-118">**Kimliği** -hello kaynak URI'si hello.</span><span class="sxs-lookup"><span data-stu-id="3ac08-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="3ac08-119">**Konum** -hello hello kaynak bulunduğu konumu.</span><span class="sxs-lookup"><span data-stu-id="3ac08-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="3ac08-120">**ilişkileri** -ilişkilendirmeleri toohello listesini başvurulan nesne.</span><span class="sxs-lookup"><span data-stu-id="3ac08-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="3ac08-121">**ad** -hello hello adını başvurulan kaynak.</span><span class="sxs-lookup"><span data-stu-id="3ac08-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="3ac08-122">**ResourceId** -hello ResourceId olduğu hello association'ında başvurulan hello kaynağının hello URI.</span><span class="sxs-lookup"><span data-stu-id="3ac08-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="3ac08-123">**associationType** -bu değer hello ilişkisi hello alt nesne hello üst başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="3ac08-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="3ac08-124">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="3ac08-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3ac08-125">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3ac08-125">Before you begin</span></span>

<span data-ttu-id="3ac08-126">Bu senaryoda, kullandığınız hello `network watcher topology` cmdlet tooretrieve hello topoloji bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="3ac08-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="3ac08-127">Ayrıca bir makalesi vardır hakkında çok[ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3ac08-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="3ac08-128">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="3ac08-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3ac08-129">Senaryo</span><span class="sxs-lookup"><span data-stu-id="3ac08-129">Scenario</span></span>

<span data-ttu-id="3ac08-130">Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.</span><span class="sxs-lookup"><span data-stu-id="3ac08-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="3ac08-131">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="3ac08-131">Retrieve topology</span></span>

<span data-ttu-id="3ac08-132">Merhaba `network watcher topology` cmdlet'i belirtilen kaynak grubu için hello topolojisini alır.</span><span class="sxs-lookup"><span data-stu-id="3ac08-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="3ac08-133">Merhaba bağımsız değişken Ekle "--json" json biçiminde tooview hello oput</span><span class="sxs-lookup"><span data-stu-id="3ac08-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="3ac08-134">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="3ac08-134">Results</span></span>

<span data-ttu-id="3ac08-135">Merhaba döndürülen sonuçları bir özellik "Merhaba json yanıt gövdesine hello için içeren adı" kaynaklarınız `network watcher topology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3ac08-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="3ac08-136">Merhaba yanıt hello kaynaklarında hello ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) içerir.</span><span class="sxs-lookup"><span data-stu-id="3ac08-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3ac08-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ac08-137">Next steps</span></span>

<span data-ttu-id="3ac08-138">Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3ac08-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>

---
title: "aaaView Azure Ağ İzleyicisi topolojisi - Azure CLI | Microsoft Docs"
description: "Bu makalede anlatmaktadır nasıl toouse Azure CLI tooquery ağ topolojinizi."
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
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="70539-103">Ağ İzleyicisi topolojisi Azure CLI ile görüntüleme</span><span class="sxs-lookup"><span data-stu-id="70539-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="70539-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70539-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="70539-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="70539-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="70539-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="70539-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="70539-107">REST API</span><span class="sxs-lookup"><span data-stu-id="70539-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="70539-108">Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="70539-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="70539-109">Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="70539-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="70539-110">Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="70539-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="70539-111">Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="70539-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="70539-112">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="70539-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="70539-113">Ağ İzleyicisi, CLI desteği şu anda Azure CLI 1.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="70539-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="70539-114">Merhaba bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="70539-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="70539-115">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="70539-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="70539-116">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="70539-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="70539-117">Merhaba aşağıdaki hello topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="70539-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="70539-118">**ad** - hello hello kaynak adı</span><span class="sxs-lookup"><span data-stu-id="70539-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="70539-119">**Kimliği** -hello kaynak URI'si hello.</span><span class="sxs-lookup"><span data-stu-id="70539-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="70539-120">**Konum** -hello hello kaynak bulunduğu konumu.</span><span class="sxs-lookup"><span data-stu-id="70539-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="70539-121">**ilişkileri** -ilişkilendirmeleri toohello listesini başvurulan nesne.</span><span class="sxs-lookup"><span data-stu-id="70539-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="70539-122">**ad** -hello hello adını başvurulan kaynak.</span><span class="sxs-lookup"><span data-stu-id="70539-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="70539-123">**ResourceId** -hello ResourceId olduğu hello association'ında başvurulan hello kaynağının hello URI.</span><span class="sxs-lookup"><span data-stu-id="70539-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="70539-124">**associationType** -bu değer hello ilişkisi hello alt nesne hello üst başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="70539-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="70539-125">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="70539-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="70539-126">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="70539-126">Before you begin</span></span>

<span data-ttu-id="70539-127">Bu senaryoda, kullandığınız hello `network watcher topology` cmdlet tooretrieve hello topoloji bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="70539-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="70539-128">Ayrıca bir makalesi vardır hakkında çok[ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="70539-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="70539-129">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="70539-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="70539-130">Senaryo</span><span class="sxs-lookup"><span data-stu-id="70539-130">Scenario</span></span>

<span data-ttu-id="70539-131">Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.</span><span class="sxs-lookup"><span data-stu-id="70539-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="70539-132">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="70539-132">Retrieve topology</span></span>

<span data-ttu-id="70539-133">Merhaba `network watcher topology` cmdlet'i belirtilen kaynak grubu için hello topolojisini alır.</span><span class="sxs-lookup"><span data-stu-id="70539-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="70539-134">Merhaba bağımsız değişken Ekle "--json" json biçiminde tooview hello oput</span><span class="sxs-lookup"><span data-stu-id="70539-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="70539-135">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="70539-135">Results</span></span>

<span data-ttu-id="70539-136">Merhaba döndürülen sonuçları bir özellik "Merhaba json yanıt gövdesine hello için içeren adı" kaynaklarınız `network watcher topology` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="70539-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="70539-137">Merhaba yanıt hello kaynaklarında hello ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) içerir.</span><span class="sxs-lookup"><span data-stu-id="70539-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="70539-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="70539-138">Next steps</span></span>

<span data-ttu-id="70539-139">Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="70539-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>

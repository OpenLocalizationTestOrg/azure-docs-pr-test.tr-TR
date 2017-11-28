---
title: "aaaView Azure Ağ İzleyicisi topolojisi - REST API | Microsoft Docs"
description: "Bu makalede, nasıl toouse REST API tooquery ağ topolojinizi anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="96689-103">Ağ İzleyicisi topolojisi REST API ile görüntüleme</span><span class="sxs-lookup"><span data-stu-id="96689-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="96689-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96689-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="96689-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="96689-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="96689-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="96689-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="96689-107">REST API</span><span class="sxs-lookup"><span data-stu-id="96689-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="96689-108">Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="96689-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="96689-109">Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="96689-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="96689-110">Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="96689-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="96689-111">Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="96689-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="96689-112">Merhaba bağlantısı altında iki ilişki modellenir.</span><span class="sxs-lookup"><span data-stu-id="96689-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="96689-113">**Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir</span><span class="sxs-lookup"><span data-stu-id="96689-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="96689-114">**İlişkili** -örnek: NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="96689-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="96689-115">Merhaba aşağıdaki hello topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="96689-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="96689-116">**ad** - hello hello kaynak adı</span><span class="sxs-lookup"><span data-stu-id="96689-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="96689-117">**Kimliği** -hello kaynak URI'si hello.</span><span class="sxs-lookup"><span data-stu-id="96689-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="96689-118">**Konum** -hello hello kaynak bulunduğu konumu.</span><span class="sxs-lookup"><span data-stu-id="96689-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="96689-119">**ilişkileri** -ilişkilendirmeleri toohello listesini başvurulan nesne.</span><span class="sxs-lookup"><span data-stu-id="96689-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="96689-120">**ad** -hello hello adını başvurulan kaynak.</span><span class="sxs-lookup"><span data-stu-id="96689-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="96689-121">**ResourceId** -hello ResourceId olduğu hello association'ında başvurulan hello kaynağının hello URI.</span><span class="sxs-lookup"><span data-stu-id="96689-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="96689-122">**associationType** -bu değer hello ilişkisi hello alt nesne hello üst başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="96689-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="96689-123">Geçerli değerler **içerir** veya **ilişkilendirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="96689-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96689-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="96689-124">Before you begin</span></span>

<span data-ttu-id="96689-125">Bu senaryoda, hello topoloji bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="96689-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="96689-126">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="96689-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="96689-127">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="96689-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="96689-128">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="96689-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="96689-129">Senaryo</span><span class="sxs-lookup"><span data-stu-id="96689-129">Scenario</span></span>

<span data-ttu-id="96689-130">Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.</span><span class="sxs-lookup"><span data-stu-id="96689-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="96689-131">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="96689-131">Log in with ARMClient</span></span>

<span data-ttu-id="96689-132">İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="96689-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="96689-133">Topoloji alma</span><span class="sxs-lookup"><span data-stu-id="96689-133">Retrieve topology</span></span>

<span data-ttu-id="96689-134">Aşağıdaki örneğine hello hello topoloji hello REST API ' ister.</span><span class="sxs-lookup"><span data-stu-id="96689-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="96689-135">Merhaba, örnek oluşturma esneklik için parametreli tooallow örnektir.</span><span class="sxs-lookup"><span data-stu-id="96689-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="96689-136">Tüm değerlerle değiştirin \< \> bunları çevreleyen.</span><span class="sxs-lookup"><span data-stu-id="96689-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="96689-137">yanıt aşağıdaki hello örneği olduğunda döndürülen kısaltılmış bir yanıt almak için bir kaynak grubu topolojisi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="96689-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="96689-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96689-138">Next steps</span></span>

<span data-ttu-id="96689-139">Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="96689-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


---
title: "aaaFind sonraki atlama Azure Ağ İzleyicisi sonraki atlama - REST ile | Microsoft Docs"
description: "Bu makalede nasıl hangi hello sonraki atlama türü olan ve sonraki atlama kullanarak IP adresi hello Azure REST API bulabilirsiniz açıklayın"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="7c390-103">Hangi hello sonraki atlama türü hello sonraki atlama yetenek Azure REST API'sini kullanarak işlemleri Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="7c390-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7c390-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7c390-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="7c390-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c390-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="7c390-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7c390-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="7c390-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7c390-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="7c390-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="7c390-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="7c390-109">Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir.</span><span class="sxs-lookup"><span data-stu-id="7c390-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="7c390-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7c390-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c390-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="7c390-111">Before you begin</span></span>

<span data-ttu-id="7c390-112">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="7c390-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7c390-113">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="7c390-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7c390-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="7c390-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7c390-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="7c390-115">Scenario</span></span>

<span data-ttu-id="7c390-116">Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır.</span><span class="sxs-lookup"><span data-stu-id="7c390-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="7c390-117">Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c390-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="7c390-118">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="7c390-118">In this scenario, you will:</span></span>

* <span data-ttu-id="7c390-119">Bir sanal makine için sonraki atlama Hello alın.</span><span class="sxs-lookup"><span data-stu-id="7c390-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7c390-120">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="7c390-120">Log in with ARMClient</span></span>

<span data-ttu-id="7c390-121">İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7c390-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="7c390-122">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="7c390-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="7c390-123">Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c390-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="7c390-124">Bu bilgiler sonraki atlama çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7c390-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="7c390-125">koddan hello Merhaba değişkenleri aşağıdaki değerleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c390-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="7c390-126">**Subscriptionıd** -abonelik kimliği toouse hello.</span><span class="sxs-lookup"><span data-stu-id="7c390-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="7c390-127">**resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="7c390-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="7c390-128">Çıktı hello aşağıdakiler arasından hello kimliği hello sanal makinenin örnek aşağıdaki hello kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7c390-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="7c390-129">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="7c390-129">Get Next Hop</span></span>

<span data-ttu-id="7c390-130">Merhaba authorization üstbilgisi oluşturulduktan sonra bir sanal makineden hello sonraki atlama alınabilir.</span><span class="sxs-lookup"><span data-stu-id="7c390-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="7c390-131">Merhaba aşağıdaki değerleri hello kod örnek toowork için değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c390-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="7c390-132">Ağ İzleyicisi REST API çağrıları hello tanılama eylemleri gerçekleştirdiğiniz hello kaynakları değil hello Ağ İzleyicisi'ni içeren hello kaynak grubunu URI'dir hello isteğindeki kaynak grubu adı hello.</span><span class="sxs-lookup"><span data-stu-id="7c390-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="7c390-133">Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7c390-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="7c390-134">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="7c390-134">Results</span></span>

<span data-ttu-id="7c390-135">Merhaba aşağıdaki kod parçacığında, alınan hello çıkış örneğidir.</span><span class="sxs-lookup"><span data-stu-id="7c390-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="7c390-136">Merhaba sonuçları değerleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="7c390-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="7c390-137">**nextHopType** -bu değer değerleri aşağıdaki hello biridir: Internet değerinin VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway veya yok.</span><span class="sxs-lookup"><span data-stu-id="7c390-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="7c390-138">**Nexthopıpaddress** -hello hello sonraki atlamanın IP adresi.</span><span class="sxs-lookup"><span data-stu-id="7c390-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="7c390-139">**routeTableId** - hello değerdir hello rota ile ilişkili hello yol tablosu için bir ya da bir URI veya kullanıcı tanımlı Hayır ise rota tanımlı hello değeri *sistem yolu* döndürülür.</span><span class="sxs-lookup"><span data-stu-id="7c390-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="7c390-140">Merhaba, json biçiminde hello sonuçları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7c390-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="7c390-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c390-141">Next steps</span></span>

<span data-ttu-id="7c390-142">Bir sanal makine için sonraki atlama hello çıkışı mümkün toofind işlendikten sonra ağ kaynaklarının hello güvenlik ziyaret ederek görüntüleyebilirsiniz [güvenlik görünümüne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7c390-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>















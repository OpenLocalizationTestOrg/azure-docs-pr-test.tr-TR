---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure CLI 2.0 ile aaaFind sonraki atlama | Microsoft Docs"
description: "Bu makale, hangi hello sonraki atlama türü olduğunu ve IP adresini kullanarak sonraki atlama Azure CLI kullanarak nasıl bulabilirsiniz anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="0251b-103">Hangi hello sonraki atlama türü hello sonraki atlama yetenek Azure CLI 2.0 kullanan Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="0251b-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0251b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0251b-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="0251b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0251b-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="0251b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0251b-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="0251b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0251b-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="0251b-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="0251b-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="0251b-109">Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir.</span><span class="sxs-lookup"><span data-stu-id="0251b-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="0251b-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="0251b-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="0251b-111">Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="0251b-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="0251b-112">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0251b-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0251b-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0251b-113">Before you begin</span></span>

<span data-ttu-id="0251b-114">Bu senaryoda, hello Azure CLI toofind hello sonraki atlama türü ve IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0251b-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="0251b-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="0251b-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="0251b-116">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0251b-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="0251b-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="0251b-117">Scenario</span></span>

<span data-ttu-id="0251b-118">Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır.</span><span class="sxs-lookup"><span data-stu-id="0251b-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="0251b-119">Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0251b-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="0251b-120">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="0251b-120">Get Next Hop</span></span>

<span data-ttu-id="0251b-121">Merhaba diyoruz tooget hello sonraki atlama `az network watcher show-next-hop` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0251b-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="0251b-122">Biz hello cmdlet hello Ağ İzleyicisi kaynak grubu, hello NetworkWatcher, sanal makine kimliği, kaynak IP adresi ve hedef IP adresi geçirin.</span><span class="sxs-lookup"><span data-stu-id="0251b-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="0251b-123">Bu örnekte, başka bir sanal ağda tooa VM hello hedef IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="0251b-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="0251b-124">Merhaba iki sanal ağ arasında bir sanal ağ geçidi yok.</span><span class="sxs-lookup"><span data-stu-id="0251b-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="0251b-125">Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0251b-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="0251b-126">Ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0251b-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="0251b-127">Merhaba VM varsa birden çok NIC ve IP iletimini hello NIC'ler hiçbirinde etkinse, NIC parametre hello (-ı NIC-ID) belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0251b-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="0251b-128">Aksi takdirde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0251b-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="0251b-129">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="0251b-129">Review results</span></span>

<span data-ttu-id="0251b-130">Tamamlandığında, hello sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0251b-130">When complete, hello results are provided.</span></span> <span data-ttu-id="0251b-131">Merhaba sonraki atlama IP adresi bu kaynak hello türü yanı sıra döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0251b-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="0251b-132">Merhaba aşağıdaki listede hello şu anda kullanılabilir NextHopType değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="0251b-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="0251b-133">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="0251b-133">**Next Hop Type**</span></span>

* <span data-ttu-id="0251b-134">Internet</span><span class="sxs-lookup"><span data-stu-id="0251b-134">Internet</span></span>
* <span data-ttu-id="0251b-135">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="0251b-135">VirtualAppliance</span></span>
* <span data-ttu-id="0251b-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="0251b-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="0251b-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="0251b-137">VnetLocal</span></span>
* <span data-ttu-id="0251b-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="0251b-138">HyperNetGateway</span></span>
* <span data-ttu-id="0251b-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="0251b-139">VnetPeering</span></span>
* <span data-ttu-id="0251b-140">None</span><span class="sxs-lookup"><span data-stu-id="0251b-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="0251b-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0251b-141">Next steps</span></span>

<span data-ttu-id="0251b-142">Bilgi nasıl tooreview ağ güvenlik grubu ayarlarınızı programlı olarak şu adresi ziyaret ederek [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0251b-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

---
title: "Azure Ağ İzleyicisi aaaIntroduction toonext atlama | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi'ne genel bakış sonraki atlama yeteneği sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="97f1e-103">Azure Ağ İzleyicisi giriş toonext atlama</span><span class="sxs-lookup"><span data-stu-id="97f1e-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="97f1e-104">Bir VM'ye gelen trafiği tooa hedef bir NIC ile ilişkili hello etkili rotalarını göre gönderilir</span><span class="sxs-lookup"><span data-stu-id="97f1e-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="97f1e-105">Sonraki atlama hello sonraki atlama türü ve IP adresi bir paket için bir belirli bir sanal makine ve NIC alır</span><span class="sxs-lookup"><span data-stu-id="97f1e-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="97f1e-106">Bu hello paket yönlendirilmiş toohello hedef yüklenmekte olan veya siyah olan hello trafiği holed toodetermine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="97f1e-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="97f1e-107">Rotaların trafik yönlendirilmiş tooan şirket içi konumu veya bir sanal gereç olduğu hello kullanıcı tarafından hatalı bir yapılandırma tooconnectivity sorunları yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="97f1e-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="97f1e-108">Sonraki atlama ayrıca hello sonraki atlama ile ilişkili hello yol tablosu döndürür.</span><span class="sxs-lookup"><span data-stu-id="97f1e-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="97f1e-109">Bu rota Hello rota kullanıcı tanımlı bir yol olarak tanımlanırsa, bir sonraki atlama sorgulanırken döndürülür.</span><span class="sxs-lookup"><span data-stu-id="97f1e-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="97f1e-110">Aksi takdirde sonraki atlama "Sistem yolu" döndürür.</span><span class="sxs-lookup"><span data-stu-id="97f1e-110">Otherwise Next hop returns "System Route".</span></span>

![sonraki atlama genel bakış][1]

<span data-ttu-id="97f1e-112">Merhaba, sonraki atlama sorgulanırken döndürülebilecek hello sonraki atlama türlerini listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="97f1e-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="97f1e-113">Internet</span><span class="sxs-lookup"><span data-stu-id="97f1e-113">Internet</span></span>
* <span data-ttu-id="97f1e-114">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="97f1e-114">VirtualAppliance</span></span>
* <span data-ttu-id="97f1e-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="97f1e-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="97f1e-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="97f1e-116">VnetLocal</span></span>
* <span data-ttu-id="97f1e-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="97f1e-117">HyperNetGateway</span></span>
* <span data-ttu-id="97f1e-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="97f1e-118">VnetPeering</span></span>
* <span data-ttu-id="97f1e-119">None</span><span class="sxs-lookup"><span data-stu-id="97f1e-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="97f1e-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97f1e-120">Next steps</span></span>

<span data-ttu-id="97f1e-121">Nasıl toouse sonraki atlama toofind ziyaret ederek ile ağ bağlantısı sorunları öğrenmek [bir VM'de onay hello sonraki atlama](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="97f1e-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png














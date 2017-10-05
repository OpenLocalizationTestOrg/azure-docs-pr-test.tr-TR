---
title: "Azure Ağ İzleyicisi sonraki atlama giriş | Microsoft Docs"
description: "Bu sayfa Ağ İzleyicisi'ne genel bakış sonraki atlama yeteneği sağlar."
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
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="3c5c3-103">Azure Ağ İzleyicisi sonraki atlama giriş</span><span class="sxs-lookup"><span data-stu-id="3c5c3-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="3c5c3-104">Bir VM'ye gelen trafiği bir NIC ile ilişkili etkili rotalarını dayalı bir hedefe gönderilir</span><span class="sxs-lookup"><span data-stu-id="3c5c3-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="3c5c3-105">Sonraki atlama IP adresini bir paket ve sonraki atlama türü bir belirli bir sanal makine ve NIC alır</span><span class="sxs-lookup"><span data-stu-id="3c5c3-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="3c5c3-106">Bu paketin hedef yönlendirilmiş veya siyah olan trafik holed belirlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="3c5c3-107">Burada trafik bir şirket içi konumu veya bir sanal gereç yönlendirilir, bir kullanıcı tarafından yolların hatalı bir yapılandırma bağlantısı sorunlarına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="3c5c3-108">Sonraki atlama ayrıca sonraki atlama ile ilişkili yol tablosu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="3c5c3-109">Varsa rota kullanıcı tanımlı bir yol olarak tanımlanan bir sonraki atlama sorgularken bu rota döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="3c5c3-110">Aksi takdirde sonraki atlama "Sistem yolu" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-110">Otherwise Next hop returns "System Route".</span></span>

![sonraki atlama genel bakış][1]

<span data-ttu-id="3c5c3-112">Sonraki atlama sorgulanırken döndürülen sonraki atlama türlerini listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3c5c3-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="3c5c3-113">Internet</span><span class="sxs-lookup"><span data-stu-id="3c5c3-113">Internet</span></span>
* <span data-ttu-id="3c5c3-114">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="3c5c3-114">VirtualAppliance</span></span>
* <span data-ttu-id="3c5c3-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="3c5c3-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="3c5c3-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="3c5c3-116">VnetLocal</span></span>
* <span data-ttu-id="3c5c3-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="3c5c3-117">HyperNetGateway</span></span>
* <span data-ttu-id="3c5c3-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="3c5c3-118">VnetPeering</span></span>
* <span data-ttu-id="3c5c3-119">None</span><span class="sxs-lookup"><span data-stu-id="3c5c3-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="3c5c3-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3c5c3-120">Next steps</span></span>

<span data-ttu-id="3c5c3-121">Sonraki atlama adresini ziyaret ederek ile ağ bağlantısı sorunları bulmak için nasıl kullanılacağını öğrenin [bir VM'de sonraki atlama denetleyin](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3c5c3-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png














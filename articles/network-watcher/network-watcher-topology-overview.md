---
title: "Azure Ağ İzleyicisi'ni de aaaIntroduction tootopology | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi topoloji özelliklerine genel bakış sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="24ca2-103">Azure Ağ İzleyicisi'ni de giriş tootopology</span><span class="sxs-lookup"><span data-stu-id="24ca2-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="24ca2-104">Topoloji, bir sanal ağ ağ kaynaklarının bir grafik döndürür.</span><span class="sxs-lookup"><span data-stu-id="24ca2-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="24ca2-105">Merhaba grafikte hello bağlantısı hello kaynakları toorepresent hello son tooend ağ bağlantısı arasında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="24ca2-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![Topoloji genel bakış][1]

<span data-ttu-id="24ca2-107">Merhaba Portalı'nda topoloji hello kaynak nesneleri döndürür bir sanal ağ temelinde.</span><span class="sxs-lookup"><span data-stu-id="24ca2-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="24ca2-108">Merhaba kaynak grubu görüntülenmeyecek olsa bile hello Ağ İzleyicisi bölgesi dışında hello kaynakları kaynakları arasındaki çizgilerle hello ilişkileri gösterilen.</span><span class="sxs-lookup"><span data-stu-id="24ca2-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="24ca2-109">Merhaba portal görünümünde döndürülen hello kaynakları grafiği çizilecek hello ağ bileşenleri bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="24ca2-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="24ca2-110">ağ kaynakları toosee hello tam listesini kullanabilir [PowerShell](network-watcher-topology-powershell.md) veya [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="24ca2-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="24ca2-111">Ağ İzleyicisi örneği toorun topoloji istediğiniz her bir bölge gereklidir.</span><span class="sxs-lookup"><span data-stu-id="24ca2-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="24ca2-112">Kaynakları hello bağlantı aralarında döndürülür gibi altında iki ilişki Modellenen.</span><span class="sxs-lookup"><span data-stu-id="24ca2-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="24ca2-113">**Kapsama** -örnek: sanal ağ, bir NIC içeren bir alt ağ içerir</span><span class="sxs-lookup"><span data-stu-id="24ca2-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="24ca2-114">**İlişkili** -örnek: bir NIC VM ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="24ca2-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="24ca2-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24ca2-115">Next steps</span></span>

<span data-ttu-id="24ca2-116">Nasıl toouse PowerShell tooretrieve hello topolojisini görüntülemek ziyaret ederek bilgi [PowerShell ile Ağ İzleyicisi topolojisi](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="24ca2-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png

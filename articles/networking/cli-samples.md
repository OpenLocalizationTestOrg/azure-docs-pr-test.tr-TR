---
title: "aaaAzure CLI örnekleri | Microsoft Docs"
description: "Azure CLI örnekleri"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="ef653-103">Ağ iletişimi için Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="ef653-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="ef653-104">Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure CLI kullanarak oluşturulan komut dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ef653-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="ef653-105">**Azure kaynakları arasında bağlantı**</span><span class="sxs-lookup"><span data-stu-id="ef653-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="ef653-106">Çok katmanlı uygulamalar için bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef653-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-107">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ef653-108">Trafik toohello ön uç alt sınırlı tooHTTP ve SSH, trafik toohello sırasında arka uç alt sınırlı tooMySQL, bağlantı noktası 3306.</span><span class="sxs-lookup"><span data-stu-id="ef653-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="ef653-109">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="ef653-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-110">Oluşturur ve iki sanal ağlarda hello bağlanır aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="ef653-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="ef653-111">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="ef653-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-112">Ön uç ve arka uç alt ağları ve mümkün tooroute trafiği hello iki alt ağlar arasında bir VM sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="ef653-113">Gelen ve giden VM ağ trafiği filtreleme</span><span class="sxs-lookup"><span data-stu-id="ef653-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-114">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ef653-115">Gelen ağ trafiğini toohello ön uç alt sınırlı tooHTTP, HTTPS ve SSH değil.</span><span class="sxs-lookup"><span data-stu-id="ef653-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="ef653-116">Merhaba arka uç alt ağından giden trafiği toohello Internet izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ef653-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="ef653-117">**Yük Dengeleme ve trafik yönü**</span><span class="sxs-lookup"><span data-stu-id="ef653-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="ef653-118">Bakiye trafiği tooVMs yüksek kullanılabilirlik için yük</span><span class="sxs-lookup"><span data-stu-id="ef653-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-119">Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="ef653-120">Yük Dengelemesi birden çok Web sitesi vm'lerinde</span><span class="sxs-lookup"><span data-stu-id="ef653-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="ef653-121">Birden çok IP yapılandırmaları, birleştirilmiş tooan Azure kullanılabilirlik kümesi, bir Azure yük dengeleyici erişilebilir olan iki VM'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="ef653-122">Uygulama yüksek kullanılabilirlik için birden çok bölgede doğrudan trafiği</span><span class="sxs-lookup"><span data-stu-id="ef653-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="ef653-123">İki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef653-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |

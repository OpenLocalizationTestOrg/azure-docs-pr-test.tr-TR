---
title: "Azure CLI örnekleri | Microsoft Docs"
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
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="48f0e-103">Ağ iletişimi için Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="48f0e-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="48f0e-104">Aşağıdaki tabloda Azure CLI kullanarak oluşturulan komut dosyalarını bash bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="48f0e-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="48f0e-105">**Azure kaynakları arasında bağlantı**</span><span class="sxs-lookup"><span data-stu-id="48f0e-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="48f0e-106">Çok katmanlı uygulamalar için bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="48f0e-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-107">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="48f0e-108">Arka uç alt ağ trafiği MySQL, bağlantı noktası 3306 sınırlı olsa ön uç alt ağ trafiği HTTP ve SSH, ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="48f0e-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="48f0e-109">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="48f0e-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-110">Oluşturur ve iki sanal ağ aynı bölgede bağlanır.</span><span class="sxs-lookup"><span data-stu-id="48f0e-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="48f0e-111">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="48f0e-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-112">Ön uç ve arka uç alt ağları ve iki alt ağlar arasında trafiği yönlendirmek için bir VM sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="48f0e-113">Gelen ve giden VM ağ trafiği filtreleme</span><span class="sxs-lookup"><span data-stu-id="48f0e-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-114">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="48f0e-115">Ön uç alt ağa gelen ağ trafiğini, HTTP, HTTPS ve SSH sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="48f0e-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="48f0e-116">Arka uç alt ağından internet giden trafiğe izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="48f0e-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="48f0e-117">**Yük Dengeleme ve trafik yönü**</span><span class="sxs-lookup"><span data-stu-id="48f0e-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="48f0e-118">Yük trafiği dengelemek için sanal makineleri yüksek oranda kullanılabilirlik için</span><span class="sxs-lookup"><span data-stu-id="48f0e-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-119">Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="48f0e-120">Yük Dengelemesi birden çok Web sitesi vm'lerinde</span><span class="sxs-lookup"><span data-stu-id="48f0e-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="48f0e-121">Bir Azure kullanılabilirlik kümesi, bir Azure yük dengeleyici erişilebilir katılmış birden fazla IP yapılandırması ile iki VM'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="48f0e-122">Uygulama yüksek kullanılabilirlik için birden çok bölgede doğrudan trafiği</span><span class="sxs-lookup"><span data-stu-id="48f0e-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="48f0e-123">İki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="48f0e-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |

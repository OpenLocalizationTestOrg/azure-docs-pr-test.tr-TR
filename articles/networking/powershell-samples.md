---
title: "Azure PowerShell örnekleri | Microsoft Docs"
description: "Azure PowerShell örnekleri"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="6b7dd-103">Ağ iletişimi için Azure PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="6b7dd-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="6b7dd-104">Aşağıdaki tabloda Azure PowerShell kullanılarak oluşturulan komut dosyalarını bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="6b7dd-105">**Azure kaynakları arasında bağlantı**</span><span class="sxs-lookup"><span data-stu-id="6b7dd-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="6b7dd-106">Çok katmanlı uygulamalar için bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b7dd-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-107">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6b7dd-108">Arka uç alt ağ trafiği SQL, bağlantı noktası 1433 sınırlı olsa da HTTP için ön uç alt ağ trafiği sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="6b7dd-109">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="6b7dd-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-110">Oluşturur ve iki sanal ağ aynı bölgede bağlanır.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="6b7dd-111">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="6b7dd-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-112">Ön uç ve arka uç alt ağları ve iki alt ağlar arasında trafiği yönlendirmek için bir VM sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="6b7dd-113">Gelen ve giden VM ağ trafiği filtreleme</span><span class="sxs-lookup"><span data-stu-id="6b7dd-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-114">Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6b7dd-115">Ön uç alt ağa gelen ağ trafiğini, HTTP ve HTTPS ile sınırlıdır...</span><span class="sxs-lookup"><span data-stu-id="6b7dd-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="6b7dd-116">Arka uç alt ağından internet giden trafiğe izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="6b7dd-117">**Yük Dengeleme ve trafik yönü**</span><span class="sxs-lookup"><span data-stu-id="6b7dd-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="6b7dd-118">Yük trafiği dengelemek için sanal makineleri yüksek oranda kullanılabilirlik için</span><span class="sxs-lookup"><span data-stu-id="6b7dd-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-119">Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="6b7dd-120">Yük Dengelemesi birden çok Web sitesi vm'lerinde</span><span class="sxs-lookup"><span data-stu-id="6b7dd-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6b7dd-121">Bir Azure kullanılabilirlik kümesi, bir Azure yük dengeleyici erişilebilir katılmış birden fazla IP yapılandırması ile iki VM'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="6b7dd-122">Uygulama yüksek kullanılabilirlik için birden çok bölgede doğrudan trafiği</span><span class="sxs-lookup"><span data-stu-id="6b7dd-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="6b7dd-123">İki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b7dd-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |

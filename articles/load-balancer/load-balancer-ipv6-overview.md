---
title: "IPv6 Azure yük dengeleyici için genel bakış | Microsoft Docs"
description: "IPv6 desteği Azure yük dengeleyici ve yük dengeli sanal makineleri anlama."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 8cca857314ecf37ef51700fd25aef228515ecd0a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="48693-104">IPv6 Azure yük dengeleyici için genel bakış</span><span class="sxs-lookup"><span data-stu-id="48693-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="48693-105">Internet'e yönelik Yük Dengeleyici, bir IPv6 adresi ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="48693-106">IPv4 bağlantısı ek olarak, bu aşağıdaki yetenekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="48693-106">In addition to IPv4 connectivity, this enables the following capabilities:</span></span>

* <span data-ttu-id="48693-107">Yerel uçtan uca IPv6 bağlantısı ortak Internet istemcileri ve Azure sanal makineleri (VM'ler) arasında yük dengeleyici üzerinden.</span><span class="sxs-lookup"><span data-stu-id="48693-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span></span>
* <span data-ttu-id="48693-108">Yerel uçtan uca IPv6 giden bağlantı VM'ler ve ortak Internet IPv6 özellikli istemciler arasında.</span><span class="sxs-lookup"><span data-stu-id="48693-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="48693-109">Aşağıdaki resimde, Azure yük dengeleyici için IPv6 işlevselliği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="48693-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span></span>

![IPv6 Azure yük dengeleyici](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="48693-111">Dağıtıldığında, bir IPv4 veya IPv6 özellikli Internet istemcisi ortak IPv4 veya IPv6 adresleri (veya ana bilgisayar adları) Azure Internet'e yönelik Yük Dengeleyici iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="48693-112">Yük Dengeleyici ağ adresi çevirisi (NAT) kullanarak sanal makineleri özel IPv6 adreslerini IPv6 paketlerini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="48693-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span></span> <span data-ttu-id="48693-113">IPv6 Internet istemcisi doğrudan IPv6 adresi VM'ler ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="48693-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span></span>

## <a name="features"></a><span data-ttu-id="48693-114">Özellikler</span><span class="sxs-lookup"><span data-stu-id="48693-114">Features</span></span>

<span data-ttu-id="48693-115">Azure Resource Manager aracılığıyla dağıtılan VM'ler için yerel IPv6 desteği sağlar:</span><span class="sxs-lookup"><span data-stu-id="48693-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="48693-116">IPv6 Internet üzerindeki istemciler için yük dengeli IPv6 Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="48693-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span></span>
2. <span data-ttu-id="48693-117">Yerel IPv6 ve IPv4 uç noktaları vm'lerde ("Yığılmış çift")</span><span class="sxs-lookup"><span data-stu-id="48693-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="48693-118">Gelen ve giden başlatılan yerel IPv6 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="48693-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="48693-119">TCP, UDP ve HTTP (S) gibi desteklenen protokoller eksiksiz bir hizmet mimarileri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="48693-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="48693-120">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="48693-120">Benefits</span></span>

<span data-ttu-id="48693-121">Bu işlevsellik, aşağıdaki faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="48693-121">This functionality enables the following key benefits:</span></span>

* <span data-ttu-id="48693-122">Yeni uygulamalar yalnızca IPv6 istemciler için erişilebilir olmasını gerektiren kamu düzenlemeleri karşılayan</span><span class="sxs-lookup"><span data-stu-id="48693-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span></span>
* <span data-ttu-id="48693-123">Etkinleştirme mobil ve nesnelerin interneti (IOT) geliştiriciler çift yığın (IPv4 + IPv6) Azure sanal makineler büyüyen mobil & IOT pazarlara yönelik olarak kullanmak için</span><span class="sxs-lookup"><span data-stu-id="48693-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="48693-124">Ayrıntılar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="48693-124">Details and limitations</span></span>

<span data-ttu-id="48693-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="48693-125">Details</span></span>

* <span data-ttu-id="48693-126">Azure DNS hizmeti, bir IPv4 ve IPv6 AAAA ad kayıtlarını içerir ve yük dengeleyici için her iki kayıt ile yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="48693-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span></span> <span data-ttu-id="48693-127">İstemci ile iletişim kurmak için adres (IPv4 veya IPv6) seçer.</span><span class="sxs-lookup"><span data-stu-id="48693-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span></span>
* <span data-ttu-id="48693-128">Bir VM ortak Internet IPv6 bağlı aygıtına bir bağlantı başlattığında, VM'nin IPv6 adresi çevrilmiş ağ adresine (NAT) yük dengeleyicinin genel IPv6 adresi kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="48693-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span></span>
* <span data-ttu-id="48693-129">Linux işletim sistemi çalıştıran VM'ler, DHCP aracılığıyla bir IPv6 IP adresi almak için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48693-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="48693-130">Çoğu Azure Galerisi'ndeki Linux görüntülerinin IPv6 değişiklik yapmadan desteklemek için zaten yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="48693-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span></span> <span data-ttu-id="48693-131">Daha fazla bilgi için bkz: [yapılandırma DHCPv6 Linux VM'ler](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="48693-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="48693-132">Yük Dengeleyici ile bir sistem durumu araştırması kullanmayı seçerseniz, bir IPv4 araştırması oluşturabilir ve hem IPv4 hem de IPv6 uç ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48693-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="48693-133">VM hizmette kullanılamaz hale gelirse IPv4 ve IPv6 uç noktalar dışında döndürme alınır.</span><span class="sxs-lookup"><span data-stu-id="48693-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="48693-134">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="48693-134">Limitations</span></span>

* <span data-ttu-id="48693-135">Azure portalında IPv6 Yük Dengeleme kuralları eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="48693-135">You cannot add IPv6 load balancing rules in the Azure portal.</span></span> <span data-ttu-id="48693-136">Kuralları yalnızca şablonu aracılığıyla, CLI, PowerShell oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-136">The rules can only be created through the template, CLI, PowerShell.</span></span>
* <span data-ttu-id="48693-137">IPv6 adresleri kullanmak için var olan VM'ler yükseltme değil.</span><span class="sxs-lookup"><span data-stu-id="48693-137">You may not upgrade existing VMs to use IPv6 addresses.</span></span> <span data-ttu-id="48693-138">Yeni VM'ler dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48693-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="48693-139">Tek bir IPv6 adresi her VM tek bir ağ arabiriminde atanabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-139">A single IPv6 address can be assigned to a single network interface in each VM.</span></span>
* <span data-ttu-id="48693-140">Genel IPv6 adresi için bir VM atanamaz.</span><span class="sxs-lookup"><span data-stu-id="48693-140">The public IPv6 addresses cannot be assigned to a VM.</span></span> <span data-ttu-id="48693-141">Bir yük dengeleyiciye yalnızca atanabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-141">They can only be assigned to a load balancer.</span></span>
* <span data-ttu-id="48693-142">Ters DNS araması, genel IPv6 adresleri için yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="48693-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="48693-143">IPv6 adresleri ile sanal makineleri bir Azure bulut hizmeti üyesi olamaz.</span><span class="sxs-lookup"><span data-stu-id="48693-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="48693-144">Bunlar, bir Azure sanal ağı (VNet) bağlanabilir ve IPv4 adresleri birbirleriyle iletişim.</span><span class="sxs-lookup"><span data-stu-id="48693-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="48693-145">Özel IPv6 adresleri, bir kaynak grubunda tek tek sanal makineleri üzerinde dağıtılabilir ancak ölçek kümeleri aracılığıyla bir kaynak grubuna dağıtılamıyor.</span><span class="sxs-lookup"><span data-stu-id="48693-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="48693-146">Azure VM'ler, diğer sanal makineleri, diğer Azure hizmetlerine veya şirket içi cihazlar için IPv6 üzerinden bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="48693-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="48693-147">Bunlar yalnızca Azure yük dengeleyici ile IPv6 üzerinden iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-147">They can only communicate with the Azure load balancer over IPv6.</span></span> <span data-ttu-id="48693-148">Ancak, IPv4 kullanarak bu diğer kaynaklarla iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="48693-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="48693-149">Ağ güvenlik grubu (NSG) koruma IPv4 için ikili yığını (IPv4 + IPv6) dağıtımlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="48693-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="48693-150">Nsg'ler IPv6 uç noktaları için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="48693-150">NSGs do not apply to the IPv6 endpoints.</span></span>
* <span data-ttu-id="48693-151">VM IPv6 uç noktada doğrudan Internet'e açık değil.</span><span class="sxs-lookup"><span data-stu-id="48693-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span></span> <span data-ttu-id="48693-152">Bir yük dengeleyicinin arkasına olur.</span><span class="sxs-lookup"><span data-stu-id="48693-152">It is behind a load balancer.</span></span> <span data-ttu-id="48693-153">Yalnızca Yük Dengeleyici kurallarında belirtilen bağlantı noktalarını IPv6 üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="48693-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="48693-154">IPv6 için IdleTimeout parametre değiştirme **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="48693-154">Changing the IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="48693-155">Varsayılan dört dakikadır.</span><span class="sxs-lookup"><span data-stu-id="48693-155">The default is four minutes.</span></span>
* <span data-ttu-id="48693-156">IPv6 için loadDistributionMethod parametre değiştirme **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="48693-156">Changing the loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="48693-157">Ayrılan IPv6 IP'leri (burada Ipallocationmethod statik =) olan **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="48693-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48693-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48693-158">Next steps</span></span>

<span data-ttu-id="48693-159">IPv6 olan yük dengeleyici dağıtmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="48693-159">Learn how to deploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="48693-160">Bölgeye göre IPv6 kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="48693-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="48693-161">Bir şablonu kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="48693-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="48693-162">Azure PowerShell kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="48693-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="48693-163">Azure CLI kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="48693-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)

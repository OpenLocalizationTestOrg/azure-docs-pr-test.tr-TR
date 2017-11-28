---
title: "Azure yük dengeleyici için IPv6 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="05a34-104">IPv6 Azure yük dengeleyici için genel bakış</span><span class="sxs-lookup"><span data-stu-id="05a34-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="05a34-105">Internet'e yönelik Yük Dengeleyici, bir IPv6 adresi ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="05a34-106">Ayrıca tooIPv4 bağlantısı, bu özellikler aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="05a34-106">In addition tooIPv4 connectivity, this enables hello following capabilities:</span></span>

* <span data-ttu-id="05a34-107">Yerel uçtan uca IPv6 bağlantısı ortak Internet istemcileri ve Azure sanal makineleri (VM'ler) arasında hello yük dengeleyici üzerinden.</span><span class="sxs-lookup"><span data-stu-id="05a34-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through hello load balancer.</span></span>
* <span data-ttu-id="05a34-108">Yerel uçtan uca IPv6 giden bağlantı VM'ler ve ortak Internet IPv6 özellikli istemciler arasında.</span><span class="sxs-lookup"><span data-stu-id="05a34-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="05a34-109">Resim aşağıdaki hello Azure yük dengeleyici için hello IPv6 işlevselliği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="05a34-109">hello following picture illustrates hello IPv6 functionality for Azure Load Balancer.</span></span>

![IPv6 Azure yük dengeleyici](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="05a34-111">Uygulama dağıtıldıktan sonra bir IPv4 veya IPv6 özellikli Internet istemcisi hello ortak IPv4 veya IPv6 adresleri (veya ana bilgisayar adları) hello Azure Internet'e yönelik Yük Dengeleyici ile iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with hello public IPv4 or IPv6 addresses (or hostnames) of hello Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="05a34-112">Merhaba yük dengeleyici yolların IPv6 paketlerini toohello özel IPv6 adreslerini ağ adresi çevirisi (NAT) kullanarak hello VM'ler hello.</span><span class="sxs-lookup"><span data-stu-id="05a34-112">hello load balancer routes hello IPv6 packets toohello private IPv6 addresses of hello VMs using network address translation (NAT).</span></span> <span data-ttu-id="05a34-113">Merhaba IPv6 Internet istemcisi doğrudan hello hello VM'ler IPv6 adresini'ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="05a34-113">hello IPv6 Internet client cannot communicate directly with hello IPv6 address of hello VMs.</span></span>

## <a name="features"></a><span data-ttu-id="05a34-114">Özellikler</span><span class="sxs-lookup"><span data-stu-id="05a34-114">Features</span></span>

<span data-ttu-id="05a34-115">Azure Resource Manager aracılığıyla dağıtılan VM'ler için yerel IPv6 desteği sağlar:</span><span class="sxs-lookup"><span data-stu-id="05a34-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="05a34-116">Yük dengeli IPv6 Hizmetleri hello Internet üzerindeki IPv6 istemciler için</span><span class="sxs-lookup"><span data-stu-id="05a34-116">Load-balanced IPv6 services for IPv6 clients on hello Internet</span></span>
2. <span data-ttu-id="05a34-117">Yerel IPv6 ve IPv4 uç noktaları vm'lerde ("Yığılmış çift")</span><span class="sxs-lookup"><span data-stu-id="05a34-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="05a34-118">Gelen ve giden başlatılan yerel IPv6 bağlantılar</span><span class="sxs-lookup"><span data-stu-id="05a34-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="05a34-119">TCP, UDP ve HTTP (S) gibi desteklenen protokoller eksiksiz bir hizmet mimarileri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="05a34-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="05a34-120">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="05a34-120">Benefits</span></span>

<span data-ttu-id="05a34-121">Bu işlev hello aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="05a34-121">This functionality enables hello following key benefits:</span></span>

* <span data-ttu-id="05a34-122">Yeni uygulamalar erişilebilir yalnızca tooIPv6 istemcileri olmasını gerektiren karşılayan kamu düzenlemeleri</span><span class="sxs-lookup"><span data-stu-id="05a34-122">Meet government regulations requiring that new applications be accessible tooIPv6-only clients</span></span>
* <span data-ttu-id="05a34-123">Büyüyen mobil & IOT pazarda etkinleştir mobil ve nesnelerin interneti (IOT) geliştiriciler toouse çift yığın (IPv4 + IPv6) Azure sanal makineleri tooaddress hello</span><span class="sxs-lookup"><span data-stu-id="05a34-123">Enable mobile and Internet of things (IOT) developers toouse dual-stacked (IPv4+IPv6) Azure Virtual Machines tooaddress hello growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="05a34-124">Ayrıntılar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="05a34-124">Details and limitations</span></span>

<span data-ttu-id="05a34-125">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="05a34-125">Details</span></span>

* <span data-ttu-id="05a34-126">Hello Azure DNS hizmeti, bir IPv4 ve IPv6 AAAA ad kayıtlarını içerir ve hello yük dengeleyici için her iki kayıt ile yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="05a34-126">hello Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for hello load balancer.</span></span> <span data-ttu-id="05a34-127">Merhaba istemci ile hangi adresi (IPv4 veya IPv6) toocommunicate seçer.</span><span class="sxs-lookup"><span data-stu-id="05a34-127">hello client chooses which address (IPv4 or IPv6) toocommunicate with.</span></span>
* <span data-ttu-id="05a34-128">VM bir bağlantı tooa ortak Internet IPv6 bağlı cihaz başlattığında hello VM'in IPv6 adresi ağ adresi hello yük dengeleyici (NAT) toohello genel IPv6 adresi çevrilen kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="05a34-128">When a VM initiates a connection tooa public Internet IPv6-connected device, hello VM's source IPv6 address is network address translated (NAT) toohello public IPv6 address of hello load balancer.</span></span>
* <span data-ttu-id="05a34-129">Merhaba Linux işletim sistemi çalıştıran VM'ler yapılandırılmış tooreceive DHCP aracılığıyla bir IPv6 IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="05a34-129">VMs running hello Linux operating system must be configured tooreceive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="05a34-130">Merhaba Linux Azure Galerisi olan zaten hello görüntülerinde çoğunu toosupport IPv6 değişiklik yapmadan yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="05a34-130">Many of hello Linux images in hello Azure Gallery are already configured toosupport IPv6 without modification.</span></span> <span data-ttu-id="05a34-131">Daha fazla bilgi için bkz: [yapılandırma DHCPv6 Linux VM'ler](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="05a34-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="05a34-132">Seçerseniz bir sistem durumu araştırma, yük dengeleyici ile toouse bir IPv4 araştırması oluşturup hello IPv4 ve IPv6 uç noktaları ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05a34-132">If you choose toouse a health probe with your load balancer, create an IPv4 probe and use it with both hello IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="05a34-133">VM Hello hizmette kullanılamaz hale gelirse hello IPv4 ve IPv6 uç noktalar dışında döndürme alınır.</span><span class="sxs-lookup"><span data-stu-id="05a34-133">If hello service on your VM goes down, both hello IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="05a34-134">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="05a34-134">Limitations</span></span>

* <span data-ttu-id="05a34-135">IPv6 Yük Dengeleme kuralları hello Azure portal ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="05a34-135">You cannot add IPv6 load balancing rules in hello Azure portal.</span></span> <span data-ttu-id="05a34-136">Merhaba kuralları yalnızca CLI, PowerShell gibi hello şablonu aracılığıyla oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-136">hello rules can only be created through hello template, CLI, PowerShell.</span></span>
* <span data-ttu-id="05a34-137">Var olan sanal makineleri toouse IPv6 adreslerini yükseltme değil.</span><span class="sxs-lookup"><span data-stu-id="05a34-137">You may not upgrade existing VMs toouse IPv6 addresses.</span></span> <span data-ttu-id="05a34-138">Yeni VM'ler dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05a34-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="05a34-139">Tek bir IPv6 adresi her VM tooa tek ağ arabirimine atanabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-139">A single IPv6 address can be assigned tooa single network interface in each VM.</span></span>
* <span data-ttu-id="05a34-140">Merhaba genel IPv6 adresi tooa VM atanamaz.</span><span class="sxs-lookup"><span data-stu-id="05a34-140">hello public IPv6 addresses cannot be assigned tooa VM.</span></span> <span data-ttu-id="05a34-141">Tooa yük dengeleyici yalnızca atanabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-141">They can only be assigned tooa load balancer.</span></span>
* <span data-ttu-id="05a34-142">Merhaba ters DNS araması, genel IPv6 adresleri için yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="05a34-142">You cannot configure hello reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="05a34-143">Merhaba VM'ler hello IPv6 adresleri ile bir Azure bulut hizmeti üyesi olamaz.</span><span class="sxs-lookup"><span data-stu-id="05a34-143">hello VMs with hello IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="05a34-144">Bağlı tooan Azure sanal ağ (VNet) olması ve IPv4 adresleri birbirleriyle iletişim.</span><span class="sxs-lookup"><span data-stu-id="05a34-144">They can be connected tooan Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="05a34-145">Özel IPv6 adresleri, bir kaynak grubunda tek tek sanal makineleri üzerinde dağıtılabilir ancak ölçek kümeleri aracılığıyla bir kaynak grubuna dağıtılamıyor.</span><span class="sxs-lookup"><span data-stu-id="05a34-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="05a34-146">Azure VM'ler, IPv6 tooother VM'ler, diğer Azure hizmetlerine veya şirket içi cihazlar bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="05a34-146">Azure VMs cannot connect over IPv6 tooother VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="05a34-147">Bunlar yalnızca hello Azure yük dengeleyici ile IPv6 üzerinden iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-147">They can only communicate with hello Azure load balancer over IPv6.</span></span> <span data-ttu-id="05a34-148">Ancak, IPv4 kullanarak bu diğer kaynaklarla iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="05a34-149">Ağ güvenlik grubu (NSG) koruma IPv4 için ikili yığını (IPv4 + IPv6) dağıtımlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="05a34-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="05a34-150">Nsg'ler toohello IPv6 uç noktaları geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="05a34-150">NSGs do not apply toohello IPv6 endpoints.</span></span>
* <span data-ttu-id="05a34-151">VM değil hello Hello IPv6 uç noktada kullanıma doğrudan toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="05a34-151">hello IPv6 endpoint on hello VM is not exposed directly toohello internet.</span></span> <span data-ttu-id="05a34-152">Bir yük dengeleyicinin arkasına olur.</span><span class="sxs-lookup"><span data-stu-id="05a34-152">It is behind a load balancer.</span></span> <span data-ttu-id="05a34-153">Yalnızca hello bağlantı noktalarını Hello yük dengeleyici kurallarında belirtilen IPv6 üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="05a34-153">Only hello ports specified in hello load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="05a34-154">Değiştirme hello IdleTimeout parametre IPv6 için **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="05a34-154">Changing hello IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="05a34-155">Merhaba, dört dakika varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="05a34-155">hello default is four minutes.</span></span>
* <span data-ttu-id="05a34-156">Değiştirme hello loadDistributionMethod parametresi IPv6 için **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="05a34-156">Changing hello loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="05a34-157">Ayrılan IPv6 IP'leri (burada Ipallocationmethod statik =) olan **şu anda desteklenmiyor**.</span><span class="sxs-lookup"><span data-stu-id="05a34-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05a34-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05a34-158">Next steps</span></span>

<span data-ttu-id="05a34-159">Bilgi nasıl toodeploy IPv6 olan yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="05a34-159">Learn how toodeploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="05a34-160">Bölgeye göre IPv6 kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="05a34-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="05a34-161">Bir şablonu kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="05a34-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="05a34-162">Azure PowerShell kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="05a34-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="05a34-163">Azure CLI kullanarak bir yük dengeleyici IPv6 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="05a34-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)

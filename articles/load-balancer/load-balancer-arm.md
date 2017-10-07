---
title: "Yük Dengeleyici Kaynak Yöneticisi desteği aaaAzure | Microsoft Docs"
description: "Azure Resource Manager ile yük dengeleyici için PowerShell kullanma. Yük Dengeleyici için şablonları kullanma"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="069db-104">Azure Kaynak Yöneticisi desteği Azure yük dengeleyici ile kullanma</span><span class="sxs-lookup"><span data-stu-id="069db-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="069db-105">Azure Resource Manager hello tercih edilen Yönetim Azure hizmetlerini çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="069db-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="069db-106">Azure yük dengeleyici, Azure Resource Manager tabanlı API'ler ve araçlar kullanılarak yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="069db-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="069db-107">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="069db-107">Concepts</span></span>

<span data-ttu-id="069db-108">Resource Manager ile Azure yük dengeleyici alt kaynakları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="069db-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="069db-109">Ön uç IP yapılandırmasını –, aksi halde sanal IP (VIP) bilinen bir veya daha fazla ön uç IP adresi bir yük dengeleyici içerebilir.</span><span class="sxs-lookup"><span data-stu-id="069db-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="069db-110">Bu IP adreslerine hello trafiği için giriş işlevini görür.</span><span class="sxs-lookup"><span data-stu-id="069db-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="069db-111">Arka uç adres havuzu – bunlar ağ arabirim kartı (NIC) toowhich yük dağıtılan hello sanal makineyle ilişkilendirilmiş IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="069db-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="069db-112">Yük Dengeleme kuralları – bir kural özellik eşlemeleri verilen ön uç IP bağlantı noktası bileşimi tooa arka uç IP adresleri kümesini ve bağlantı noktası bileşimi.</span><span class="sxs-lookup"><span data-stu-id="069db-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="069db-113">Tek bir yük dengeleyici birden çok dengeleme kuralına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="069db-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="069db-114">Her kural, bir ön uç IP’si ile bağlantı noktasının ve arka uç IP’si ile VM’lerle ilişkilendirilmiş bağlantı noktasının birleşiminden oluşur.</span><span class="sxs-lookup"><span data-stu-id="069db-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="069db-115">Araştırmalar – araştırmalar, VM örnekleri hello durumunu tookeep izlemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="069db-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="069db-116">Hello VM örneği bir sistem durumu araştırması başarısız olursa, döndürme dışında otomatik olarak gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="069db-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="069db-117">Gelen NAT kuralları – NAT kuralları tanımlama hello ön uç IP üzerinden akan gelen trafiğin hello ve geri dağıtılmış toohello bitiş IP.</span><span class="sxs-lookup"><span data-stu-id="069db-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="069db-118">Hızlı başlangıç şablonları</span><span class="sxs-lookup"><span data-stu-id="069db-118">Quickstart templates</span></span>

<span data-ttu-id="069db-119">Azure Resource Manager bildirim temelli bir şablon kullanarak uygulamalarınızı tooprovision sağlar.</span><span class="sxs-lookup"><span data-stu-id="069db-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="069db-120">Tek bir şablonda birden çok hizmeti bağımlılıklarıyla birlikte dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="069db-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="069db-121">Merhaba kullandığınız aynı şablon toorepeatedly hello uygulama yaşam döngüsünün her aşaması sırasında uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="069db-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="069db-122">Şablonları sanal makineler, sanal ağlar, kullanılabilirlik kümeleri, ağ arabirimlerine (NIC'ler), depolama hesapları, yük dengeleyici, ağ güvenlik grupları ve genel IP'ler için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="069db-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="069db-123">Şablonları ile karmaşık bir uygulama için gereksinim duyduğunuz her şeyi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="069db-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="069db-124">Merhaba şablon dosyası, sürüm denetimi ve işbirliği için içerik yönetim sistemi içine denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="069db-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="069db-125">Şablonlar hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="069db-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="069db-126">Ağ kaynakları hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="069db-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="069db-127">Azure yük dengeleyici kullanarak hızlı başlangıç şablonlarını bulunabilir bir [GitHub deposunu](https://github.com/Azure/azure-quickstart-templates) oluşturulan topluluk şablonları kümesi barındırma.</span><span class="sxs-lookup"><span data-stu-id="069db-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="069db-128">Şablonları örnekleri:</span><span class="sxs-lookup"><span data-stu-id="069db-128">Examples of templates:</span></span>

* [<span data-ttu-id="069db-129">Bir yük dengeleyici ve Yük Dengeleme kuralları içinde 2 VM</span><span class="sxs-lookup"><span data-stu-id="069db-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="069db-130">Bir iç yük dengeleyici ve yük dengeleyici kuralları sahip bir VNET içinde 2 VM</span><span class="sxs-lookup"><span data-stu-id="069db-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="069db-131">Bir yük dengeleyici içinde 2 VM LB hello üzerinde NAT kuralları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="069db-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="069db-132">PowerShell veya CLI ile Azure yük dengeleyici ayarlama</span><span class="sxs-lookup"><span data-stu-id="069db-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="069db-133">Azure Resource Manager cmdlet'leri, komut satırı araçları ve REST API'leri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="069db-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="069db-134">[Azure ağı cmdlet'lerini](https://msdn.microsoft.com/library/azure/mt163510.aspx) kullanılan toocreate bir yük dengeleyici olabilir.</span><span class="sxs-lookup"><span data-stu-id="069db-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="069db-135">Nasıl toocreate Azure Kaynak Yöneticisi'ni kullanarak bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="069db-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="069db-136">Azure kaynak yönetimi ile Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="069db-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="069db-137">Yük Dengeleyici REST API'leri</span><span class="sxs-lookup"><span data-stu-id="069db-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="069db-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="069db-138">Next steps</span></span>

<span data-ttu-id="069db-139">Ayrıca [Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md) ve ne tür yapılandırma [dağıtım modu](load-balancer-distribution-mode.md) belirli yük dengeleyici ağ trafiği davranışı için.</span><span class="sxs-lookup"><span data-stu-id="069db-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="069db-140">Bilgi nasıl toomanage [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="069db-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="069db-141">Bu, uygulamanızın tookeep bağlantıları canlı bir yük dengeleyicinin arkasındaki sunucular için gerektiğinde önemlidir.</span><span class="sxs-lookup"><span data-stu-id="069db-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>

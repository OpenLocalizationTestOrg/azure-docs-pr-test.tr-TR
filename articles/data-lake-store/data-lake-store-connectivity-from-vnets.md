---
title: Data Lake Deposu'ndan veri Vnet'ler aaaConnect tooAzure | Microsoft Docs
description: "Azure sanal ağlar tooAzure Data Lake Store Bağlan"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="7bc25-103">Erişim Azure Data Lake Store bir Azure sanal içinde vm'lerden</span><span class="sxs-lookup"><span data-stu-id="7bc25-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="7bc25-104">Azure Data Lake Store genel Internet IP adresleri üzerinde çalışan bir PaaS hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="7bc25-105">Toohello ortak Internet can genellikle bağlanabilir herhangi bir sunucu tooAzure Data Lake Store uç noktalarını da bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7bc25-105">Any server that can connect toohello public Internet can typically connect tooAzure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="7bc25-106">Varsayılan olarak, Azure Vnet'lerde olan tüm VM'ler hello Internet erişebilir ve bu nedenle Azure Data Lake Store erişebilir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-106">By default, all VMs that are in Azure VNETs can access hello Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="7bc25-107">Ancak, bir VNET toonot olası tooconfigure Vm'lerde olan erişim toohello Internet sahip.</span><span class="sxs-lookup"><span data-stu-id="7bc25-107">However, it is possible tooconfigure VMs in a VNET toonot have access toohello Internet.</span></span> <span data-ttu-id="7bc25-108">Bu tür VM'ler için erişim tooAzure Data Lake Store de sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="7bc25-108">For such VMs, access tooAzure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="7bc25-109">Azure sanal ağlar VM'ler için genel Internet erişimi engelleme yapılabilir yaklaşımı izleyerek hello birini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7bc25-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of hello following approach.</span></span>

* <span data-ttu-id="7bc25-110">Ağ güvenlik grupları (NSG) yapılandırarak</span><span class="sxs-lookup"><span data-stu-id="7bc25-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="7bc25-111">Kullanıcı tanımlı yolları (UDR) yapılandırarak</span><span class="sxs-lookup"><span data-stu-id="7bc25-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="7bc25-112">Yollar BGP (endüstri standardı dinamik yönlendirme protokolü) üzerinden değişimi tarafından bu blok ExpressRoute kullanıldığında toohello Internet erişimi</span><span class="sxs-lookup"><span data-stu-id="7bc25-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access toohello Internet</span></span>

<span data-ttu-id="7bc25-113">Bu makalede, nasıl tooenable erişim toohello Azure Data Lake Store hello üç yöntemden birini kullanarak kaynak yukarıda listelenen kısıtlı tooaccess silinmiş Azure vm'lerden öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7bc25-113">In this article, you will learn how tooenable access toohello Azure Data Lake Store from Azure VMs which have been restricted tooaccess resources using one of hello three methods listed above.</span></span>

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="7bc25-114">Bağlantı tooAzure vm'lerden Data Lake Store ile kısıtlı bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7bc25-114">Enabling connectivity tooAzure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="7bc25-115">tooaccess Azure Data Lake deposuna böyle Vm'lerden, hello Azure Data Lake Store hesabı kullanılabilir olduğu tooaccess başlangıç IP adresi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-115">tooaccess Azure Data Lake Store from such VMs, you must configure them tooaccess hello IP address where hello Azure Data Lake Store account is available.</span></span> <span data-ttu-id="7bc25-116">Hesaplarınız hello DNS adları çözme tarafından Data Lake Store hesapları için hello IP adreslerini tanımlayabilirsiniz (`<account>.azuredatalakestore.net`).</span><span class="sxs-lookup"><span data-stu-id="7bc25-116">You can identify hello IP addresses for your Data Lake Store accounts by resolving hello DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="7bc25-117">Bu araçları gibi kullanabileceğiniz **nslookup**.</span><span class="sxs-lookup"><span data-stu-id="7bc25-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="7bc25-118">Bilgisayarınızı bir komut istemi açın ve hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7bc25-118">Open a command prompt on your computer and run hello following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="7bc25-119">Merhaba çıktı hello aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="7bc25-119">hello output resembles hello following.</span></span> <span data-ttu-id="7bc25-120">Merhaba karşı değer **adresi** başlangıç IP adresi, Data Lake Store hesabınızla ilişkili bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-120">hello value against **Address** property is hello IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="7bc25-121">NSG kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7bc25-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="7bc25-122">Bir NSG kural kullanıldığında tooblock erişim toohello Internet, ardından erişim toohello Data Lake deposu IP adresi sağlayan başka bir NSG oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bc25-122">When a NSG rule is used tooblock access toohello Internet, then you can create another NSG that allows access toohello Data Lake Store IP Address.</span></span> <span data-ttu-id="7bc25-123">NSG kuralları hakkında daha fazla bilgi için bkz. [bir ağ güvenlik grubu nedir?](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="7bc25-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="7bc25-124">Yönergeler için nasıl toocreate Nsg'ler bkz [nasıl Azure portal kullanarak toomanage Nsg'ler hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7bc25-124">For instructions on how toocreate NSGs see [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="7bc25-125">UDR veya ExpressRoute kullanılarak kısıtlanmış VM'ler bağlantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7bc25-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="7bc25-126">Yollar, Udr'ler ya da BGP alınıp yolları, kullanılan tooblock erişim toohello Internet olduğunda, özel bir rota bu tür alt VM'ler Data Lake Store uç noktaları erişebilmesi için yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-126">When routes, either UDRs or BGP-exchanged routes, are used tooblock access toohello Internet, a special route needs toobe configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="7bc25-127">Daha fazla bilgi için bkz: [kullanıcı tanımlı yollar nelerdir?](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bc25-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="7bc25-128">Udr'ler oluşturma ile ilgili yönergeler için bkz: [oluşturma Udr'ler Kaynak Yöneticisi'nde](../virtual-network/virtual-network-create-udr-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7bc25-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="7bc25-129">ExpressRoute kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7bc25-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="7bc25-130">Bir expressroute bağlantı hattı yapılandırıldığında, hello şirket içi sunucular ortak eşleme aracılığıyla Data Lake Store erişebilir.</span><span class="sxs-lookup"><span data-stu-id="7bc25-130">When an ExpressRoute circuit is configured, hello on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="7bc25-131">Bunun için ortak eşleme adresinde Expressroute'u yapılandırma hakkında daha fazla ayrıntı [ExpressRoute SSS](../expressroute/expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="7bc25-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7bc25-132">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7bc25-132">See also</span></span>
* [<span data-ttu-id="7bc25-133">Azure Data Lake Store'a Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7bc25-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="7bc25-134">Azure Data Lake Store içinde depolanan verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="7bc25-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)


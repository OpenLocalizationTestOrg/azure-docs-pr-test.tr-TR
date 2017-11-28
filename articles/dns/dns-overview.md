---
title: Azure DNS aaaOverview | Microsoft Docs
description: "DNS barındırma hizmeti Microsoft Azure ile ilgili genel bakış. Microsoft Azure etki alanınızda barındırır."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="f66ca-104">Azure DNS'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="f66ca-104">Azure DNS overview</span></span>

<span data-ttu-id="f66ca-105">Merhaba etki alanı adı sistemi ya da DNS, çevirmek için sorumlu (veya çözme) bir Web sitesi veya hizmet name tooits IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f66ca-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="f66ca-106">Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="f66ca-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="f66ca-107">Azure etki alanlarınızı barındırarak DNS sunucunuzun yönetebilirsiniz kullanarak kayıtları, diğer Azure hizmetleriyle aynı kimlik bilgileri, API'leri, Araçlar ve faturalama hello.</span><span class="sxs-lookup"><span data-stu-id="f66ca-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS'ye genel bakış](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="f66ca-109">Özellikler</span><span class="sxs-lookup"><span data-stu-id="f66ca-109">Features</span></span>

* <span data-ttu-id="f66ca-110">**Güvenilirlik ve performans** -Azure DNS'de DNS etki alanı, Azure'nın genel DNS ad sunucuları ağda barındırılır.</span><span class="sxs-lookup"><span data-stu-id="f66ca-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="f66ca-111">Böylece her DNS sorgusu hello en yakın kullanılabilir DNS sunucusu tarafından yanıtlanan her noktaya yayın ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="f66ca-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="f66ca-112">Bu, etki alanınız için yüksek kullanılabilirlik ve hızlı performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="f66ca-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="f66ca-113">**Sorunsuz tümleştirme** -hello Azure DNS hizmeti kullanılan toomanage Azure hizmetlerinizi için DNS kayıtlarını olabilir ve kullanılan tooprovide DNS dış kaynaklar da olabilir.</span><span class="sxs-lookup"><span data-stu-id="f66ca-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="f66ca-114">Azure DNS hello Azure portal tümleştirilmiştir ve diğer Azure hizmetlerinizi kullandığı aynı kimlik bilgilerini, faturalama ve destek sözleşmesi hello.</span><span class="sxs-lookup"><span data-stu-id="f66ca-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="f66ca-115">**Güvenlik** -hello Azure DNS hizmeti, Azure Resource Manager dayanır.</span><span class="sxs-lookup"><span data-stu-id="f66ca-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="f66ca-116">Bu nedenle, rol tabanlı erişim denetimi, denetim günlüklerini ve kaynak kilitleme gibi Resource Manager özelliklerinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="f66ca-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="f66ca-117">Etki alanları ve kayıtları hello Azure portal, Azure PowerShell cmdlet'leri, yönetilebilir ve platformlar arası Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="f66ca-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="f66ca-118">Otomatik DNS Yönetimi gerektiren uygulamalar hello hizmetiyle hello üzerinden REST API ve SDK'ları tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f66ca-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="f66ca-119">Azure DNS, etki alanı adlarını satın alma şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f66ca-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="f66ca-120">Toopurchase etki alanları istiyorsanız, bir üçüncü taraf etki alanı adı kayıt toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="f66ca-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="f66ca-121">Merhaba Kaydedici genellikle küçük bir yıllık ücret ister.</span><span class="sxs-lookup"><span data-stu-id="f66ca-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="f66ca-122">Merhaba etki alanları için DNS kayıtlarını Yönetimi sonra Azure DNS'de barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f66ca-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="f66ca-123">Bkz: [bir etki alanı tooAzure DNS temsilci](dns-domain-delegation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="f66ca-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="f66ca-124">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="f66ca-124">Pricing</span></span>

<span data-ttu-id="f66ca-125">DNS faturalama Azure ve DNS sorgularının hello sayısı tarafından barındırılan DNS bölgeleri hello sayısını temel alır.</span><span class="sxs-lookup"><span data-stu-id="f66ca-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="f66ca-126">toolearn ziyaret fiyatlandırma hakkında daha fazla [Azure DNS fiyatlandırma](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="f66ca-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="f66ca-127">SSS</span><span class="sxs-lookup"><span data-stu-id="f66ca-127">FAQ</span></span>

<span data-ttu-id="f66ca-128">Azure DNS hakkında sık sorulan sorular için bkz: Merhaba [Azure DNS ile ilgili SSS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f66ca-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66ca-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f66ca-129">Next steps</span></span>

<span data-ttu-id="f66ca-130">Ziyaret ederek DNS bölgeleri ve kayıtlar hakkında bilgi edinin: [DNS bölgeleri ve genel bakış kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="f66ca-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="f66ca-131">Nasıl çok öğrenin[bir DNS bölgesi oluşturma](./dns-getstarted-create-dnszone-portal.md) Azure DNS'de.</span><span class="sxs-lookup"><span data-stu-id="f66ca-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="f66ca-132">Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.</span><span class="sxs-lookup"><span data-stu-id="f66ca-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>


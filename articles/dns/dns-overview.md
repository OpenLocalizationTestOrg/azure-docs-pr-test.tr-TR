---
title: "Azure DNS genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="35b92-104">Azure DNS'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="35b92-104">Azure DNS overview</span></span>

<span data-ttu-id="35b92-105">Etki alanı adı sistemi ya da DNS, çevirmek için sorumludur (veya çözme) bir Web sitesi ya da hizmet adı IP adresine.</span><span class="sxs-lookup"><span data-stu-id="35b92-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="35b92-106">Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="35b92-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="35b92-107">Etki alanlarınızı Azure'da barındırarak DNS kayıtlarınızı diğer Azure hizmetlerinde kullandığınız kimlik bilgileri, API’ler, araçlar ve faturalarla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35b92-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS'ye genel bakış](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="35b92-109">Özellikler</span><span class="sxs-lookup"><span data-stu-id="35b92-109">Features</span></span>

* <span data-ttu-id="35b92-110">**Güvenilirlik ve performans** -Azure DNS'de DNS etki alanı, Azure'nın genel DNS ad sunucuları ağda barındırılır.</span><span class="sxs-lookup"><span data-stu-id="35b92-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="35b92-111">Böylece her DNS sorgusu en yakın kullanılabilir DNS sunucusu tarafından yanıtlanan her noktaya yayın ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="35b92-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="35b92-112">Bu, etki alanınız için yüksek kullanılabilirlik ve hızlı performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="35b92-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="35b92-113">**Sorunsuz tümleştirme** -Azure DNS hizmeti, dış kaynaklarınız için DNS sağlamak için kullanılan ve Azure hizmetlerinizi için DNS kayıtlarını yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35b92-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="35b92-114">Azure DNS, Azure portalında tümleşiktir ve aynı kimlik bilgilerini, faturalama ve destek sözleşmesi, diğer Azure Hizmetleri olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="35b92-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="35b92-115">**Güvenlik** -Azure DNS hizmeti, Azure Resource Manager dayanır.</span><span class="sxs-lookup"><span data-stu-id="35b92-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="35b92-116">Bu nedenle, rol tabanlı erişim denetimi, denetim günlüklerini ve kaynak kilitleme gibi Resource Manager özelliklerinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="35b92-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="35b92-117">Etki alanları ve kayıtları Azure portalı, Azure PowerShell cmdlet'leri ve platformlar arası Azure CLI yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="35b92-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="35b92-118">Otomatik DNS Yönetimi gerektiren uygulamalar, REST API ve SDK aracılığıyla hizmeti ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35b92-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="35b92-119">Azure DNS, etki alanı adlarını satın alma şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="35b92-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="35b92-120">Etki alanı satın almak istiyorsanız, bir üçüncü taraf etki alanı adı kayıt kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35b92-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="35b92-121">Kayıt, genellikle küçük bir yıllık ücret ister.</span><span class="sxs-lookup"><span data-stu-id="35b92-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="35b92-122">Etki alanları için DNS kayıtlarını Yönetimi sonra Azure DNS'de barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="35b92-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="35b92-123">Bkz: [bir etki alanını Azure DNS'ye devretme](dns-domain-delegation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="35b92-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="35b92-124">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="35b92-124">Pricing</span></span>

<span data-ttu-id="35b92-125">DNS faturalama Azure ve DNS sorgularının sayısı tarafından barındırılan DNS bölgeleri sayısını temel alır.</span><span class="sxs-lookup"><span data-stu-id="35b92-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="35b92-126">Ziyaret fiyatlandırma hakkında daha fazla bilgi için [Azure DNS fiyatlandırma](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="35b92-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="35b92-127">SSS</span><span class="sxs-lookup"><span data-stu-id="35b92-127">FAQ</span></span>

<span data-ttu-id="35b92-128">Azure DNS hakkında sık sorulan sorular için bkz: [Azure DNS ile ilgili SSS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="35b92-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="35b92-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35b92-129">Next steps</span></span>

<span data-ttu-id="35b92-130">Ziyaret ederek DNS bölgeleri ve kayıtlar hakkında bilgi edinin: [DNS bölgeleri ve genel bakış kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="35b92-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="35b92-131">Bilgi edinmek için nasıl [bir DNS bölgesi oluşturma](./dns-getstarted-create-dnszone-portal.md) Azure DNS'de.</span><span class="sxs-lookup"><span data-stu-id="35b92-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="35b92-132">Azure'un diğer önemli [ağ özelliklerinden](../networking/networking-overview.md) bazıları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="35b92-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>


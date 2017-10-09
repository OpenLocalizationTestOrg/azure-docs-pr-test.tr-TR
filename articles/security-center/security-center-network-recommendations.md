---
title: "aaaProtecting Azure Güvenlik Merkezi, ağınızda | Microsoft Docs"
description: "Yardımcı olacak öneriler Azure Güvenlik Merkezi'nde Azure ağınızı korumak ve güvenlik ilkeleriyle uyumlu olmak bu belge adresleri."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="71333-103">Azure Güvenlik Merkezi, ağınızda koruma</span><span class="sxs-lookup"><span data-stu-id="71333-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="71333-104">Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler.</span><span class="sxs-lookup"><span data-stu-id="71333-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="71333-105">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71333-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="71333-106">Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve uygulamaları makineleri (VM'ler).</span><span class="sxs-lookup"><span data-stu-id="71333-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="71333-107">Bu makalede tooyour ağ uygulamak önerileri giderir.</span><span class="sxs-lookup"><span data-stu-id="71333-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="71333-108">Ağ önerileri merkezi İleri nesil güvenlik duvarları, ağ güvenlik grupları, yapılandırma gelen trafiği kuralları ve daha fazla etrafında.</span><span class="sxs-lookup"><span data-stu-id="71333-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="71333-109">Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir ağ önerileri ve onu uygularsanız her birini ne yaptığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="71333-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="71333-110">Kullanılabilir ağ önerileri</span><span class="sxs-lookup"><span data-stu-id="71333-110">Available network recommendations</span></span>
| <span data-ttu-id="71333-111">Öneri</span><span class="sxs-lookup"><span data-stu-id="71333-111">Recommendation</span></span> | <span data-ttu-id="71333-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="71333-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="71333-113">Yeni Nesil Güvenlik Duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="71333-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="71333-114">Güvenlik korumaları bir Microsoft iş ortağı tooincrease İleri nesil Güvenlik Duvarı (NGFW) eklemek önerir.</span><span class="sxs-lookup"><span data-stu-id="71333-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="71333-115">Trafiği yalnızca NGFW aracılığıyla yönlendirme</span><span class="sxs-lookup"><span data-stu-id="71333-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="71333-116">Gelen trafik tooyour, NGFW aracılığıyla VM zorla ağ güvenlik grubu (NSG) kurallarını yapılandırmak önerir.</span><span class="sxs-lookup"><span data-stu-id="71333-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="71333-117">Ağ güvenlik grupları alt ağları veya sanal makinelerde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="71333-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="71333-118">Nsg'ler alt ağları veya VM'ler etkinleştirmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="71333-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="71333-119">Uç nokta Internet'e aracılığıyla erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="71333-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="71333-120">İçin Nsg'ler gelen trafik kurallarını yapılandırmak önerir.</span><span class="sxs-lookup"><span data-stu-id="71333-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="71333-121">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="71333-121">See also</span></span>
<span data-ttu-id="71333-122">toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="71333-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="71333-123">Azure Güvenlik Merkezi'nde, sanal makineleri koruma</span><span class="sxs-lookup"><span data-stu-id="71333-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="71333-124">Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma</span><span class="sxs-lookup"><span data-stu-id="71333-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="71333-125">Azure SQL hizmetinizi Azure Güvenlik Merkezi'nde koruma</span><span class="sxs-lookup"><span data-stu-id="71333-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="71333-126">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="71333-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="71333-127">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="71333-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="71333-128">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="71333-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="71333-129">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71333-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>

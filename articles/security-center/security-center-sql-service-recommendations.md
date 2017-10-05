---
title: "Azure SQL Hizmeti ve Azure Güvenlik Merkezi'nde veri koruma | Microsoft Docs"
description: "Bu belge adresleri yardımcı olacak öneriler Azure Güvenlik Merkezi'nde veri ve Azure SQL Hizmeti korumak ve güvenlik ilkeleriyle uyumlu olmak."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="52256-103">Azure SQL Hizmeti ve Azure Güvenlik Merkezi'nde veri koruma</span><span class="sxs-lookup"><span data-stu-id="52256-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="52256-104">Azure Güvenlik Merkezi, ayrıca Azure kaynaklarınızın güvenlik durumunu çözümler.</span><span class="sxs-lookup"><span data-stu-id="52256-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="52256-105">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli denetimlerin yapılandırılması sürecinde size rehberlik öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="52256-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="52256-106">Önerileri Azure kaynak türleri için geçerlidir: sanal ağ, SQL ve veri ve uygulamaları makineleri (VM'ler).</span><span class="sxs-lookup"><span data-stu-id="52256-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="52256-107">Bu makalede, Azure SQL Hizmeti ve verilere uygulanır önerileri giderir.</span><span class="sxs-lookup"><span data-stu-id="52256-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="52256-108">Azure SQL sunucuları ve SQL veritabanları için şifreleme ve Azure depolama hesabınızın etkinleştirme şifreleme etkinleştirme veritabanları için denetimi etkinleştirme geçici önerileri Merkezi.</span><span class="sxs-lookup"><span data-stu-id="52256-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="52256-109">Aşağıdaki tabloda kullanılabilir SQL Hizmeti ve verileri önerileri ve onu uygularsanız ne her biri yaptığını anlamanıza yardımcı olması için bir başvuru olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="52256-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="52256-110">Kullanılabilir SQL Hizmeti ve verileri önerileri</span><span class="sxs-lookup"><span data-stu-id="52256-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="52256-111">Öneri</span><span class="sxs-lookup"><span data-stu-id="52256-111">Recommendation</span></span> | <span data-ttu-id="52256-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="52256-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="52256-113">SQL sunucularında denetim ve tehdit algılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52256-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="52256-114">Denetim ve tehdit algılama için (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL sunucuları Aç önerir.</span><span class="sxs-lookup"><span data-stu-id="52256-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="52256-115">SQL veritabanlarında denetim ve tehdit algılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52256-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="52256-116">Denetim ve tehdit algılama (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL veritabanları için Aç önerir.</span><span class="sxs-lookup"><span data-stu-id="52256-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="52256-117">SQL veritabanlarını saydam veri şifreleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="52256-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="52256-118">SQL veritabanları (yalnızca Azure SQL Hizmeti) için şifrelemeyi etkinleştirmek önerir.</span><span class="sxs-lookup"><span data-stu-id="52256-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="52256-119">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="52256-119">See also</span></span>
<span data-ttu-id="52256-120">Diğer Azure kaynak türleri için geçerli öneriler hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="52256-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="52256-121">Azure Güvenlik Merkezi'nde, sanal makineleri koruma</span><span class="sxs-lookup"><span data-stu-id="52256-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="52256-122">Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma</span><span class="sxs-lookup"><span data-stu-id="52256-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="52256-123">Azure Güvenlik Merkezi, ağınızda koruma</span><span class="sxs-lookup"><span data-stu-id="52256-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="52256-124">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="52256-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="52256-125">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="52256-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="52256-126">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="52256-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="52256-127">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52256-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>

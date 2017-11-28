---
title: "aaaProtecting Azure SQL Hizmeti ve verileri Azure Güvenlik Merkezi'nde | Microsoft Docs"
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
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="02ac7-103">Azure SQL Hizmeti ve Azure Güvenlik Merkezi'nde veri koruma</span><span class="sxs-lookup"><span data-stu-id="02ac7-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="02ac7-104">Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler.</span><span class="sxs-lookup"><span data-stu-id="02ac7-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="02ac7-105">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02ac7-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="02ac7-106">Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve veri ve uygulamaları makineleri (VM'ler).</span><span class="sxs-lookup"><span data-stu-id="02ac7-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="02ac7-107">Bu makalede tooAzure SQL Hizmeti ve verileri uygulamak önerileri giderir.</span><span class="sxs-lookup"><span data-stu-id="02ac7-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="02ac7-108">Azure SQL sunucuları ve SQL veritabanları için şifreleme ve Azure depolama hesabınızın etkinleştirme şifreleme etkinleştirme veritabanları için denetimi etkinleştirme geçici önerileri Merkezi.</span><span class="sxs-lookup"><span data-stu-id="02ac7-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="02ac7-109">Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir SQL Hizmeti ve verileri önerileri ve onu uygularsanız her birini ne yaptığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="02ac7-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="02ac7-110">Kullanılabilir SQL Hizmeti ve verileri önerileri</span><span class="sxs-lookup"><span data-stu-id="02ac7-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="02ac7-111">Öneri</span><span class="sxs-lookup"><span data-stu-id="02ac7-111">Recommendation</span></span> | <span data-ttu-id="02ac7-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="02ac7-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="02ac7-113">SQL sunucularında denetim ve tehdit algılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="02ac7-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="02ac7-114">Denetim ve tehdit algılama için (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL sunucuları Aç önerir.</span><span class="sxs-lookup"><span data-stu-id="02ac7-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="02ac7-115">SQL veritabanlarında denetim ve tehdit algılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="02ac7-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="02ac7-116">Denetim ve tehdit algılama (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL veritabanları için Aç önerir.</span><span class="sxs-lookup"><span data-stu-id="02ac7-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="02ac7-117">SQL veritabanlarını saydam veri şifreleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="02ac7-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="02ac7-118">SQL veritabanları (yalnızca Azure SQL Hizmeti) için şifrelemeyi etkinleştirmek önerir.</span><span class="sxs-lookup"><span data-stu-id="02ac7-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="02ac7-119">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="02ac7-119">See also</span></span>
<span data-ttu-id="02ac7-120">toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="02ac7-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="02ac7-121">Azure Güvenlik Merkezi'nde, sanal makineleri koruma</span><span class="sxs-lookup"><span data-stu-id="02ac7-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="02ac7-122">Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma</span><span class="sxs-lookup"><span data-stu-id="02ac7-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="02ac7-123">Azure Güvenlik Merkezi, ağınızda koruma</span><span class="sxs-lookup"><span data-stu-id="02ac7-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="02ac7-124">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="02ac7-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="02ac7-125">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="02ac7-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="02ac7-126">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="02ac7-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="02ac7-127">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02ac7-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>

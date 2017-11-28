---
title: "Azure Güvenlik Merkezi'nde SQL sunucularında aaaEnable denetim ve tehdit algılama | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** üzerinde SQL sunucuları ** denetimi etkinleştirme ve tehdit algılama."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="4bcef-103">Azure Güvenlik Merkezi'nde SQL sunucularında denetim ve tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4bcef-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="4bcef-104">Azure Güvenlik Merkezi Denetim açıldıktan ve tehdit algılama denetim varsa, Azure SQL sunucularınızda tüm veritabanları için etkinleştirilmediyse önerir.</span><span class="sxs-lookup"><span data-stu-id="4bcef-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="4bcef-105">Denetim ve tehdit algılama, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve anormallikleri, kavramanıza yardımcı olabilir iş endişeleri veya güvenlik ihlalleri şüpheli.</span><span class="sxs-lookup"><span data-stu-id="4bcef-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="4bcef-106">Denetim ayarladıktan sonra tehdit algılama ayarlarını ve e-postaları tooreceive güvenlik uyarılarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bcef-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="4bcef-107">Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="4bcef-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="4bcef-108">Bu toodetect sağlar ve bunlar ortaya çıktığında toopotential tehditlerine yanıt.</span><span class="sxs-lookup"><span data-stu-id="4bcef-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="4bcef-109">Bu öneri toohello yalnızca Azure SQL Hizmeti uygulanır; Azure altyapı Hizmetleri'nde (Azure Iaas), sanal makinelerde çalışan SQL Server içermez.</span><span class="sxs-lookup"><span data-stu-id="4bcef-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="4bcef-110">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="4bcef-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4bcef-111">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="4bcef-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4bcef-112">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="4bcef-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="4bcef-113">Merhaba, **önerileri** dikey penceresinde, select **SQL sunucularında denetimi etkinleştirme ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="4bcef-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="4bcef-114">Merhaba açılır **SQL sunucularında denetimi etkinleştirme ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4bcef-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![SQL sunucularında denetimi etkinleştirme][1]
2. <span data-ttu-id="4bcef-116">' Bir SQL server tooenable denetim ve tehdit Algılama'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4bcef-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="4bcef-117">Merhaba açılır **denetim ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4bcef-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="4bcef-118">Merhaba üzerinde **denetim ve tehdit algılama** dikey penceresinde, select **ON** altında **denetim**.</span><span class="sxs-lookup"><span data-stu-id="4bcef-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Denetim Ayarları'nı Aç][2]
4. <span data-ttu-id="4bcef-120">Merhaba adımları [hello Azure portal, SQL veritabanı denetimi](../sql-database/sql-database-auditing-portal.md) denetim günlüklerini depolanacağı tooconfigure depolama.</span><span class="sxs-lookup"><span data-stu-id="4bcef-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="4bcef-121">Merhaba aboneliğinin depolama hesabı için veri toplama hello varsayılan depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="4bcef-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="4bcef-122">Merhaba adımları [SQL veritabanı tehdit algılama ile çalışmaya başlama](../sql-database/sql-database-threat-detection.md) üzerinde tooturn ve tehdit algılama ve anormal etkinlikler algılandığında güvenlik uyarı alacak olan e-posta tooconfigure hello liste yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4bcef-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="4bcef-123">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="4bcef-123">See also</span></span>
<span data-ttu-id="4bcef-124">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Denetlemeyi etkinleştirme ve tehdit algılama SQL sunucularında." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="4bcef-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="4bcef-125">SQL veritabanınızın güvenliğini sağlama hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="4bcef-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="4bcef-126">SQL Veritabanınızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="4bcef-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="4bcef-127">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="4bcef-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4bcef-128">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="4bcef-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4bcef-129">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4bcef-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4bcef-130">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4bcef-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4bcef-131">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="4bcef-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4bcef-132">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4bcef-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4bcef-133">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bcef-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4bcef-134">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="4bcef-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png

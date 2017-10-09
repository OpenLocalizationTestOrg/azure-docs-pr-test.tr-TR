---
title: "aaaEnable denetim ve tehdit algılama özelliğini SQL veritabanları Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** Denetim ve tehdit algılama SQL veritabanları ** özelliğini etkinleştirin."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="e44f2-103">SQL veritabanları Azure Güvenlik Merkezi'nde denetim ve tehdit algılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e44f2-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="e44f2-104">Azure Güvenlik Merkezi, Denetim ve tehdit algılama tüm SQL veritabanları için denetimi, kapatmanız ve tehdit algılama zaten etkin önerir.</span><span class="sxs-lookup"><span data-stu-id="e44f2-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="e44f2-105">Denetim ve tehdit algılama, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve anormallikleri, kavramanıza yardımcı olabilir iş endişeleri veya güvenlik ihlalleri şüpheli.</span><span class="sxs-lookup"><span data-stu-id="e44f2-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="e44f2-106">Denetim ayarladıktan sonra tehdit algılama ayarlarını ve e-postaları tooreceive güvenlik uyarılarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e44f2-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="e44f2-107">Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="e44f2-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="e44f2-108">Bu toodetect sağlar ve bunlar ortaya çıktığında toopotential tehditlerine yanıt.</span><span class="sxs-lookup"><span data-stu-id="e44f2-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="e44f2-109">Bu öneri toohello yalnızca Azure SQL Hizmeti uygulanır; sanal makinelerde çalışan SQL içermez.</span><span class="sxs-lookup"><span data-stu-id="e44f2-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="e44f2-110">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="e44f2-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="e44f2-111">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="e44f2-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="e44f2-112">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="e44f2-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="e44f2-113">Merhaba, **önerileri** dikey penceresinde, select **SQL veritabanlarında denetimi etkinleştirme ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="e44f2-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="e44f2-114">Merhaba açılır **SQL veritabanlarında denetimi etkinleştirme ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e44f2-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![SQL veritabanlarında denetimi etkinleştirme][1]
2. <span data-ttu-id="e44f2-116">Bir SQL veritabanı tooenable üzerinde denetimi seçin.</span><span class="sxs-lookup"><span data-stu-id="e44f2-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="e44f2-117">Merhaba açılır **denetim ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e44f2-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="e44f2-118">Merhaba üzerinde **denetim ve tehdit algılama** dikey penceresinde, select **ON** altında **denetim**.</span><span class="sxs-lookup"><span data-stu-id="e44f2-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Denetim ve tehdit algılamayı etkinleştirme][2]
4. <span data-ttu-id="e44f2-120">Merhaba adımları [SQL veritabanı tehdit Algılama'hello Azure portal'ın](../sql-database/sql-database-threat-detection-portal.md) üzerinde tooturn ve tehdit algılama ve anormal etkinlikler algılandığında güvenlik uyarı alacak olan e-posta tooconfigure hello liste yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e44f2-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="e44f2-121">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e44f2-121">See also</span></span>
<span data-ttu-id="e44f2-122">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "etkinleştirme denetim ve tehdit algılama SQL veritabanlarında." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="e44f2-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="e44f2-123">SQL veritabanınızın güvenliğini sağlama hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="e44f2-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="e44f2-124">SQL Veritabanınızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="e44f2-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="e44f2-125">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="e44f2-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="e44f2-126">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="e44f2-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e44f2-127">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e44f2-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e44f2-128">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e44f2-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="e44f2-129">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="e44f2-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="e44f2-130">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e44f2-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="e44f2-131">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e44f2-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="e44f2-132">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="e44f2-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png

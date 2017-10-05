---
title: "SQL veritabanları Azure Güvenlik Merkezi'nde üzerinde denetim ve tehdit Algılama'yı etkinleştirmek | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** denetim ve tehdit algılama SQL veritabanları ** özelliğini etkinleştirin."
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
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="3c2cd-103">SQL veritabanları Azure Güvenlik Merkezi'nde denetim ve tehdit algılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3c2cd-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="3c2cd-104">Azure Güvenlik Merkezi, Denetim ve tehdit algılama tüm SQL veritabanları için denetimi, kapatmanız ve tehdit algılama zaten etkin önerir.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="3c2cd-105">Denetim ve tehdit algılama, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve anormallikleri, kavramanıza yardımcı olabilir iş endişeleri veya güvenlik ihlalleri şüpheli.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="3c2cd-106">Denetim ayarladıktan sonra tehdit algılama ayarlarını ve e-postaları güvenlik uyarıları almak üzere yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="3c2cd-107">Tehdit algılama veritabanına olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="3c2cd-108">Bu, algılamak ve bunlar ortaya çıktığında, olası risklere yanıt olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="3c2cd-109">Bu öneri, yalnızca Azure SQL Hizmeti için geçerlidir; sanal makinelerde çalışan SQL içermez.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2cd-110">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="3c2cd-111">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="3c2cd-112">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="3c2cd-112">Implement the recommendation</span></span>
1. <span data-ttu-id="3c2cd-113">İçinde **önerileri** dikey penceresinde, select **SQL veritabanlarında denetimi etkinleştirme ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="3c2cd-114">Bu açılır **SQL veritabanlarında denetimi etkinleştirme ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![SQL veritabanlarında denetimi etkinleştirme][1]
2. <span data-ttu-id="3c2cd-116">Denetimi etkinleştirmek için bir SQL veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="3c2cd-117">Bu açılır **denetim ve tehdit algılama** dikey.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="3c2cd-118">Üzerinde **denetim ve tehdit algılama** dikey penceresinde, select **ON** altında **denetim**.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Denetim ve tehdit algılamayı etkinleştirme][2]
4. <span data-ttu-id="3c2cd-120">Adımları [SQL veritabanı tehdit algılama Azure portalında](../sql-database/sql-database-threat-detection-portal.md) etkinleştirmek ve tehdit algılama yapılandırmak ve anormal etkinlikler algılandığında güvenlik uyarı alacak olan e-postaları listesini yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="3c2cd-121">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-121">See also</span></span>
<span data-ttu-id="3c2cd-122">Bu makalede "etkinleştirme denetim ve tehdit algılama SQL veritabanlarında." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="3c2cd-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="3c2cd-123">SQL veritabanınızın güvenliğini sağlama hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="3c2cd-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="3c2cd-124">SQL Veritabanınızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="3c2cd-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="3c2cd-125">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="3c2cd-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="3c2cd-126">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3c2cd-127">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3c2cd-128">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="3c2cd-129">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="3c2cd-130">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="3c2cd-131">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3c2cd-132">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --en son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="3c2cd-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png

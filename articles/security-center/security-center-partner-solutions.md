---
title: "Azure Güvenlik Merkezi'nde aaaManaging iş ortağı çözümleri | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi, Azure aboneliğinizle tümleşik iş ortağı Çözümlerinizin bir bakışta hello sistem durumunu izleyiciyi nasıl sağlar açıklanmaktadır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="9240c-103">Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme</span><span class="sxs-lookup"><span data-stu-id="9240c-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="9240c-104">Bu belge nasıl toomonitor hello Azure Güvenlik Merkezi'nde iş ortağı çözümlerinizin sistem durumunu size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="9240c-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="9240c-105">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="9240c-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="9240c-106">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="9240c-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="9240c-107">İş ortağı çözümlerini izleme</span><span class="sxs-lookup"><span data-stu-id="9240c-107">Monitoring partner solutions</span></span>
<span data-ttu-id="9240c-108">Merhaba **iş ortağı çözümleri** döşeme hello üzerinde **Güvenlik Merkezi** adresindeki Azure aboneliğinizle tümleşik iş ortağı Çözümlerinizin bir bakışta hello sistem durumunu izleme dikey sağlar.</span><span class="sxs-lookup"><span data-stu-id="9240c-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![İş ortağı çözümleri kutucuğu][1]

<span data-ttu-id="9240c-110">Merhaba **iş ortağı çözümleri** kutucuğu aboneliğinizle tümleşik iş ortağı çözümleri hello sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9240c-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="9240c-111">Tümleşik çözüm yoksa, hello döşeme hello sıfır görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9240c-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="9240c-112">tooview hello iş ortağı çözümlerinizin sistem durumu:</span><span class="sxs-lookup"><span data-stu-id="9240c-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="9240c-113">Select hello **iş ortağı çözümleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="9240c-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="9240c-114">Merhaba **iş ortağı çözümleri** tooSecurity Center bağlı iş ortağı çözümlerinizin listesini görüntüleyen dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="9240c-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![İş ortağı çözümleri][3]

   <span data-ttu-id="9240c-116">iş ortağı çözümü Hello durumu aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="9240c-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="9240c-117">Korumalı (yeşil) - sistem durumuyla ilgili bir sorun yok.</span><span class="sxs-lookup"><span data-stu-id="9240c-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="9240c-118">Sağlıksız (kırmızı) - sistem durumunda hemen ilgilenilmesi gereken bir sorun var.</span><span class="sxs-lookup"><span data-stu-id="9240c-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="9240c-119">Durdurulan Raporlama (turuncu) - hello çözüm, sistem durumunu raporlamayı durdurdu.</span><span class="sxs-lookup"><span data-stu-id="9240c-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="9240c-120">Bilinmeyen koruma durumu (turuncu) - hello çözüm hello durumunu yeni bir kaynak toohello varolan çözüm ekleme işlemi başarısız tooa nedeniyle şu anda bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="9240c-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="9240c-121">(Gri) - bildirmemiş hello çözüm değil bildirdi herhangi bir şey henüz yakın zamanda bağlanmış ve hala çözümün durumu bildirilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="9240c-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="9240c-122">İş ortağı çözümü seçin.</span><span class="sxs-lookup"><span data-stu-id="9240c-122">Select a partner solution.</span></span> <span data-ttu-id="9240c-123">Bu örnekte, select hello sağlar **Qualys** çözümü.</span><span class="sxs-lookup"><span data-stu-id="9240c-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="9240c-124">Merhaba durumunu hello iş ortağı çözümü ve hello çözümün ilişkili kaynakları gösteren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="9240c-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="9240c-125">Seçin **çözüm konsolunu** tooopen hello iş ortağı Yönetimi deneyimini Bu çözüm için.</span><span class="sxs-lookup"><span data-stu-id="9240c-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![İş ortağı çözümü ayrıntısı][4]
3. <span data-ttu-id="9240c-127">Toohello dönün **Qualys** dikey penceresinde ve select **bağlantı VM**.</span><span class="sxs-lookup"><span data-stu-id="9240c-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="9240c-128">Merhaba **bağlantı uygulamaları** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="9240c-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="9240c-129">Burada kaynakları toohello iş ortağı çözümüne bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9240c-129">Here you can connect resources toohello partner solution.</span></span>

   ![Bağlantı kaynakları toopartner çözümü][5]

## <a name="next-steps"></a><span data-ttu-id="9240c-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9240c-131">Next steps</span></span>
<span data-ttu-id="9240c-132">Bu belgede, sunulan toohello olan **iş ortağı çözümleri** döşeme Güvenlik Merkezi'nde.</span><span class="sxs-lookup"><span data-stu-id="9240c-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="9240c-133">Güvenlik Merkezi hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9240c-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="9240c-134">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="9240c-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9240c-135">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9240c-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9240c-136">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9240c-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="9240c-137">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="9240c-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="9240c-138">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9240c-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="9240c-139">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="9240c-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png

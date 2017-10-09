---
title: "Azure Güvenlik Merkezi'nde aaaApply sistem güncelleştirmelerini | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** Sistem güncelleştirmeleri ** uygulamak ve ** sistem güncelleştirmeleri ** sonra yeniden başlatın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="d2e19-103">Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulama</span><span class="sxs-lookup"><span data-stu-id="d2e19-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="d2e19-104">Azure Güvenlik Merkezi, Windows ve Linux işletim sistemi güncelleştirmeleri eksik makineleri (VM'ler) günlük izler.</span><span class="sxs-lookup"><span data-stu-id="d2e19-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="d2e19-105">Güvenlik Merkezi hizmeti bağlı olarak bir Windows VM üzerinde yapılandırıldığı Windows Update veya Windows Server Update Services (WSUS) kullanılabilir güvenlik ve kritik güncelleştirmeler listesini alır.</span><span class="sxs-lookup"><span data-stu-id="d2e19-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="d2e19-106">Güvenlik Merkezi, ayrıca Linux sistemlerinde hello en son güncelleştirmeleri denetler.</span><span class="sxs-lookup"><span data-stu-id="d2e19-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="d2e19-107">VM'yi bir sistem güncelleştirmesi eksikse, Güvenlik Merkezi sistem güncelleştirmeleri uygulamanızı önerir</span><span class="sxs-lookup"><span data-stu-id="d2e19-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="d2e19-108">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="d2e19-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="d2e19-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="d2e19-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d2e19-110">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="d2e19-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="d2e19-111">Merhaba, **önerileri** dikey penceresinde, select **sistem güncelleştirmelerini**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Sistem güncelleştirmelerini uygulayın][1]
2. <span data-ttu-id="d2e19-113">Merhaba **sistem güncelleştirmelerini** eksik sistem güncelleştirmeleri VM'ler listesini görüntüleyen dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d2e19-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="d2e19-114">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-114">Select a VM.</span></span>

   ![Bir VM seçin][2]
3. <span data-ttu-id="d2e19-116">Bu VM için eksik güncelleştirmelerin listesini görüntüleyen bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d2e19-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="d2e19-117">Bir Sistem Güncelleştirmesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-117">Select a system update.</span></span> <span data-ttu-id="d2e19-118">Bu örnekte, şimdi KB3156016 seçin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-118">In this example, let’s select KB3156016.</span></span>

   ![Eksik güvenlik güncelleştirmelerini][3]

4. <span data-ttu-id="d2e19-120">Merhaba Hello adımları **güvenlik güncelleştirmesi** dikey tooapply hello eksik güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="d2e19-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Güvenlik güncelleştirmesi][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="d2e19-122">Sistem güncelleştirmelerinden sonra yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="d2e19-122">Reboot after system updates</span></span>
1. <span data-ttu-id="d2e19-123">Toohello iade **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2e19-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="d2e19-124">Adlı Sistem güncelleştirmeleri uygulandıktan sonra yeni bir giriş oluşturulan **sonra sistem güncelleştirmelerini yeniden**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="d2e19-125">Bu giriş, sistemi güncelleştirmelerini uygulama tooreboot hello VM toocomplete hello işlemi gereksinim bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2e19-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Sistem güncelleştirmelerinden sonra yeniden başlatın][5]
2. <span data-ttu-id="d2e19-127">Seçin **sonra sistem güncelleştirmelerini yeniden**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="d2e19-128">Bu açılır **bir yeniden başlatma beklemede toocomplete sistem güncelleştirmelerini var** toorestart toocomplete hello gereken sanal makineleri listesini görüntüleyen dikey sistem güncelleştirmeleri işlemi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d2e19-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Beklemedeki yeniden başlatma][6]

<span data-ttu-id="d2e19-130">Azure toocomplete hello işleminden Hello VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d2e19-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2e19-131">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d2e19-131">See also</span></span>
<span data-ttu-id="d2e19-132">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="d2e19-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d2e19-133">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="d2e19-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d2e19-134">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d2e19-135">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d2e19-136">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="d2e19-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d2e19-137">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d2e19-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d2e19-138">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e19-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d2e19-139">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e19-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png

---
title: "Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulamak | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi önerileri uygulamak gösterilmiştir ** sistem güncelleştirmeleri ** uygulamak ve ** sistem güncelleştirmeleri ** sonra yeniden başlatın."
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="32df4-103">Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulama</span><span class="sxs-lookup"><span data-stu-id="32df4-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="32df4-104">Azure Güvenlik Merkezi, Windows ve Linux işletim sistemi güncelleştirmeleri eksik makineleri (VM'ler) günlük izler.</span><span class="sxs-lookup"><span data-stu-id="32df4-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="32df4-105">Güvenlik Merkezi hizmeti bağlı olarak bir Windows VM üzerinde yapılandırıldığı Windows Update veya Windows Server Update Services (WSUS) kullanılabilir güvenlik ve kritik güncelleştirmeler listesini alır.</span><span class="sxs-lookup"><span data-stu-id="32df4-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="32df4-106">Güvenlik Merkezi, ayrıca Linux sistemleri için en son güncelleştirmeleri denetler.</span><span class="sxs-lookup"><span data-stu-id="32df4-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="32df4-107">VM'yi bir sistem güncelleştirmesi eksikse, Güvenlik Merkezi sistem güncelleştirmeleri uygulamanızı önerir</span><span class="sxs-lookup"><span data-stu-id="32df4-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="32df4-108">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="32df4-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="32df4-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="32df4-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="32df4-110">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="32df4-110">Implement the recommendation</span></span>
1. <span data-ttu-id="32df4-111">İçinde **önerileri** dikey penceresinde, select **sistem güncelleştirmelerini**.</span><span class="sxs-lookup"><span data-stu-id="32df4-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Sistem güncelleştirmelerini uygulayın][1]
2. <span data-ttu-id="32df4-113">**Sistem güncelleştirmelerini** eksik sistem güncelleştirmeleri VM'ler listesini görüntüleyen dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="32df4-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="32df4-114">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="32df4-114">Select a VM.</span></span>

   ![Bir VM seçin][2]
3. <span data-ttu-id="32df4-116">Bu VM için eksik güncelleştirmelerin listesini görüntüleyen bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="32df4-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="32df4-117">Bir Sistem Güncelleştirmesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="32df4-117">Select a system update.</span></span> <span data-ttu-id="32df4-118">Bu örnekte, şimdi KB3156016 seçin.</span><span class="sxs-lookup"><span data-stu-id="32df4-118">In this example, let’s select KB3156016.</span></span>

   ![Eksik güvenlik güncelleştirmelerini][3]

4. <span data-ttu-id="32df4-120">Adımları **güvenlik güncelleştirmesi** eksik güncelleştirmeyi uygulamak için dikey.</span><span class="sxs-lookup"><span data-stu-id="32df4-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Güvenlik güncelleştirmesi][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="32df4-122">Sistem güncelleştirmelerinden sonra yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="32df4-122">Reboot after system updates</span></span>
1. <span data-ttu-id="32df4-123">Geri dönüp **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="32df4-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="32df4-124">Adlı Sistem güncelleştirmeleri uygulandıktan sonra yeni bir giriş oluşturulan **sonra sistem güncelleştirmelerini yeniden**.</span><span class="sxs-lookup"><span data-stu-id="32df4-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="32df4-125">Bu giriş, VM sistemi güncelleştirmelerini uygulama işlemini tamamlamak için bilgisayarınızı yeniden başlatmanız gerektiğini bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="32df4-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Sistem güncelleştirmelerinden sonra yeniden başlatın][5]
2. <span data-ttu-id="32df4-127">Seçin **sonra sistem güncelleştirmelerini yeniden**.</span><span class="sxs-lookup"><span data-stu-id="32df4-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="32df4-128">Bu açılır **sistem güncelleştirmelerini tamamlamak için yeniden başlatma bekleniyor** Uygula sistem tamamlamak için yeniden başlatmanız gerekir VM'ler listesini görüntüleyen dikey işlem güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="32df4-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Beklemedeki yeniden başlatma][6]

<span data-ttu-id="32df4-130">İşlemi tamamlamak için Azure VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="32df4-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="32df4-131">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="32df4-131">See also</span></span>
<span data-ttu-id="32df4-132">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="32df4-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="32df4-133">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="32df4-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="32df4-134">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="32df4-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="32df4-135">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="32df4-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="32df4-136">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="32df4-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="32df4-137">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="32df4-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="32df4-138">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32df4-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="32df4-139">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32df4-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png

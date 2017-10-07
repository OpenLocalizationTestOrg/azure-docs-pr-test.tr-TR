---
title: "aaaUpdate Azure Azure Automation modülleri | Microsoft Docs"
description: "Bu makalede, Azure automation'da varsayılan olarak sağlanan ortak Azure PowerShell modülleri nasıl şimdi güncelleştirebilirsiniz açıklanmaktadır."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="f9ac9-103">Nasıl tooupdate Azure PowerShell modülleri Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f9ac9-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="f9ac9-104">Merhaba en yaygın Azure PowerShell modülleri, varsayılan olarak her Automation hesabı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="f9ac9-105">Yeni sürümler hello portalından kullanılabilir olduğunda hello Otomasyon hesabı şekilde sizin için tooupdate hello modülleri hello hesabındaki sağladığımız şekilde hello Azure ekibi güncelleştirmeleri düzenli olarak Azure modülleri hello.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="f9ac9-106">Modülleri hello ürün grubu tarafından düzenli olarak güncelleştirilen çünkü değişiklikler değişimin parametre yeniden adlandırma veya tamamen bir cmdlet onaysız kılınmadan gibi hello türüne bağlı olarak, runbook'ları olumsuz yönde etkileyebilir dahil hello cmdlet'leri oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="f9ac9-107">runbook'larınızı ve hello etkileyen tooavoid bunlar süreçlerini otomatikleştirmek, test ve doğrulama devam etmeden önce kesinlikle önerilir.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="f9ac9-108">Hedeflenen bu amaç için adanmış bir Otomasyon hesabı yoksa, böylece hello güncelleştirme gibi ek tooiterative değişiklikleri, runbook'ların hello geliştirme sırasında birçok farklı senaryolar ve permütasyon sınayabilirsiniz bir oluşturmayı düşünün PowerShell modülleri.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="f9ac9-109">Merhaba sonuçları doğrulanır ve gereken değişiklikleri uyguladığınız sonra değiştirilmesi gereken runbook'ları hello geçişini Eşgüdümleme ile devam etmek ve üretimde aşağıda açıklandığı gibi hello güncelleştirme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="f9ac9-110">Azure modülleri güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="f9ac9-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="f9ac9-111">Merhaba modülleri Automation hesabınız var. dikey olarak adlandırılan bir seçenektir **Update Azure modülleri**.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="f9ac9-112">Her zaman etkindir.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-112">It is always enabled.</span></span><br><br> <span data-ttu-id="f9ac9-113">![Azure modülleri seçeneği modülleri dikey penceresinde Güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="f9ac9-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="f9ac9-114">Tıklatın **Update Azure modülleri** ve toocontinue isteyip istemediğinizi soran bir onay bildirimi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="f9ac9-115">![Azure modülleri bildirim güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="f9ac9-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="f9ac9-116">Tıklatın **Evet** ve hello modülü güncelleştirme işlemi başlayacak.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="f9ac9-117">Merhaba güncelleştirme işlemini modülleri aşağıdaki 15-20 dakika tooupdate hello hakkında alır:</span><span class="sxs-lookup"><span data-stu-id="f9ac9-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="f9ac9-118">Azure</span><span class="sxs-lookup"><span data-stu-id="f9ac9-118">Azure</span></span>
  * <span data-ttu-id="f9ac9-119">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="f9ac9-119">Azure.Storage</span></span>
  * <span data-ttu-id="f9ac9-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="f9ac9-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="f9ac9-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="f9ac9-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="f9ac9-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="f9ac9-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="f9ac9-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="f9ac9-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="f9ac9-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="f9ac9-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="f9ac9-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="f9ac9-125">AzureRm.Storage</span></span>

    <span data-ttu-id="f9ac9-126">Merhaba modülleri toodate zaten varsa, hello işlemini birkaç saniye içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="f9ac9-127">Merhaba güncelleştirme işlemi tamamlandığında size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-127">When hello update process completes you will be notified.</span></span><br><br> ![Azure modülleri güncelleştirme durumunu güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="f9ac9-129">Yeni bir zamanlanan iş çalıştırdığınızda azure Automation Otomasyon hesabınızda hello son modülleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="f9ac9-130">Cmdlet'leri kullanıyorsanız, runbook'ları toomanage Azure içinde bu Azure PowerShell modüllerden kaynakları, sonra tooperform Bu güncelleştirme işlemi her ay veya isteyecektir böylece elinizde tooassure hello son modüller.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9ac9-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9ac9-131">Next steps</span></span>

* <span data-ttu-id="f9ac9-132">Tümleştirme modülleri ve nasıl toocreate özel modüller toofurther tümleştirmek Otomasyon diğer sistemler, hizmetleri veya çözümleri hakkında daha fazla toolearn bkz [tümleştirme modülleri](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="f9ac9-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="f9ac9-133">Kaynak denetimi tümleştirmesi kullanmayı [GitHub Kurumsal](automation-scenario-source-control-integration-with-github-ent.md) veya [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally yönetmek ve denetlemek Otomasyon runbook ve yapılandırma Portföy sürümleri.</span><span class="sxs-lookup"><span data-stu-id="f9ac9-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  

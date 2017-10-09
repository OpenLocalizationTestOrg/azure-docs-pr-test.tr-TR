---
title: "Azure Otomasyon hesabı günlük analizi aaaUnlink | Microsoft Docs"
description: "Bu makalede nasıl toounlink Azure Automation'ınızı hesap bir OMS çalışma alanından genel bir bakış sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="99c63-103">Nasıl toounlink, Otomasyon hesabı günlük analizi çalışma alanından</span><span class="sxs-lookup"><span data-stu-id="99c63-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="99c63-104">Azure Otomasyonu günlük analizi toonot yalnızca öngörülü, runbook işleri tüm Automation hesapları arasında izleme desteği ile tümleştirilir, ancak günlük analizi bağımlı çözümleri aşağıdaki hello içeri aktardığınızda de gereklidir:</span><span class="sxs-lookup"><span data-stu-id="99c63-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="99c63-105">Güncelleştirme yönetimi</span><span class="sxs-lookup"><span data-stu-id="99c63-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="99c63-106">Değişiklik İzleme</span><span class="sxs-lookup"><span data-stu-id="99c63-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="99c63-107">Yoğun olmayan saatlerde sırasında Başlat/Durdur VM'ler</span><span class="sxs-lookup"><span data-stu-id="99c63-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="99c63-108">Günlük analizi ile Automation hesabınız artık toointegrate istediğiniz karar verirseniz, hesabınızdan doğrudan hello Azure portal bağlantısını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c63-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="99c63-109">Devam etmeden önce bu işlemin devam etmesini Aksi takdirde engellenir, daha önce bahsedilen tooremove hello çözümleri ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="99c63-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="99c63-110">Gözden geçirme hello konu hello belirli çözüm için gereken toounderstand hello adımları aktardığınız tooremove onu.</span><span class="sxs-lookup"><span data-stu-id="99c63-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="99c63-111">Bu çözümlerin kaldırdıktan sonra aşağıdaki adımları toounlink hello Automation hesabınız gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c63-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="99c63-112">Çalışma alanı bağlantısını Kaldır</span><span class="sxs-lookup"><span data-stu-id="99c63-112">Unlink workspace</span></span>

1. <span data-ttu-id="99c63-113">Hello Azure portal, Automation hesabınızı açın ve hello Otomasyon hesabı dikey penceresinde hello hesabı dikey penceresinde, seçin **çalışma bağlantısını**.</span><span class="sxs-lookup"><span data-stu-id="99c63-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="99c63-114">![Çalışma alanı seçeneği bağlantısını Kaldır](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="99c63-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="99c63-115">Merhaba Bağlantıyı Kes'i çalışma dikey penceresinde **worksapce bağlantısını**.</span><span class="sxs-lookup"><span data-stu-id="99c63-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="99c63-116">![Çalışma alanı dikey bağlantısını](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="99c63-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="99c63-117">Tooproceed istediğiniz doğrulayan bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="99c63-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="99c63-118">Azure Otomasyonu toounlink hello hesabı günlük analizi çalışma alanınız çalışır, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="99c63-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="99c63-119">İsteğe bağlı olarak hello güncelleştirme yönetimi çözümü kullandıysanız, hello çözüm kaldırdıktan sonra artık gerekli olmayan öğeleri aşağıdaki tooremove hello isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c63-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="99c63-120">Zamanlamaları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="99c63-120">Update schedules.</span></span>  <span data-ttu-id="99c63-121">Her oluşturduğunuz hello güncelleştirme dağıtımları eşleşen adlara sahip olacaktır)</span><span class="sxs-lookup"><span data-stu-id="99c63-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="99c63-122">Karma çalışan grupları Hello çözüm için oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="99c63-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="99c63-123">Her benzer şekilde çok adlandırılacağını machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="99c63-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="99c63-124">İsteğe bağlı olarak sırasında yoğun olmayan saatlerde çözüm hello Başlat/Durdur VM'ler kullandıysanız, hello çözüm kaldırdıktan sonra artık gerekli olmayan öğeleri aşağıdaki tooremove hello isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99c63-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="99c63-125">Başlatma ve durdurma VM runbook zamanlama</span><span class="sxs-lookup"><span data-stu-id="99c63-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="99c63-126">Başlatma ve VM runbook'ları durdurun</span><span class="sxs-lookup"><span data-stu-id="99c63-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="99c63-127">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="99c63-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="99c63-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99c63-128">Next steps</span></span>

<span data-ttu-id="99c63-129">OMS günlük analizi ile Otomasyon hesabı toointegrate tooreconfigure bkz [Otomasyon tooLog analizi (OMS) iş durumu ve iş akışları iletmek](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="99c63-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 

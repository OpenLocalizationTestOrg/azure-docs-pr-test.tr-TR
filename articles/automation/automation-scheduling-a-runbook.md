---
title: Azure Otomasyon runbook'u zamanlama | Microsoft Docs
description: "Belirli bir zamanda veya yinelenen bir zamanlamaya göre otomatik olarak bir runbook başlatabilirsiniz Azure Otomasyonu'nda bir zamanlama oluşturmak üzere açıklar."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="84e16-103">Azure Otomasyonu’nda runbook zamanlama</span><span class="sxs-lookup"><span data-stu-id="84e16-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="84e16-104">Belirli bir zamanda başlatmak için Azure automation'da bir runbook'u zamanlamak için bir veya daha fazla zamanlamaya bağlayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="84e16-105">Klasik Azure portalı runbook'larda ve runbook'ları Azure portalında bir kez veya bir yinelenmeye saatlik çalıştırma ya da günlük zamanlama için bir zamanlama yapılandırılabilir, ayrıca bunları için haftalık, aylık, haftanın belirli gün veya ayın günleri veya ayın belirli zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e16-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="84e16-106">Bir runbook için birden çok zamanlama bağlanabilir ve bir zamanlama birden çok runbook bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="84e16-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="84e16-107">Bir zamanlama oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e16-107">Creating a schedule</span></span>
<span data-ttu-id="84e16-108">Azure portalında Klasik portalında veya Windows PowerShell ile runbook'lar için yeni bir zamanlama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e16-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="84e16-109">Ayrıca bir runbook'u Azure Klasik veya Azure portalını kullanarak bir zamanlamaya bağladığınızda, yeni bir zamanlama oluşturma seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="84e16-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="84e16-110">Zamanlama runbook ile ilişkilendirdiğinizde, Automation hesabınızı modülleri geçerli sürümleri depolar ve bu zamanlama için bağlar.</span><span class="sxs-lookup"><span data-stu-id="84e16-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="84e16-111">Başka bir deyişle, bir zamanlama oluşturuldu ve ardından modülü sürüm 2.0 güncelleştirme hesabınızda sürüm 1.0 sahip bir modül olsaydı, zamanlama 1.0 kullanmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="84e16-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="84e16-112">Güncelleştirilmiş Modül sürümü kullanmak için yeni bir zamanlama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e16-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="84e16-113">Klasik Azure portalında yeni bir zamanlama oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="84e16-114">Azure Klasik portalında Otomasyon seçin ve ardından bir Otomasyon hesabının adını seçin.</span><span class="sxs-lookup"><span data-stu-id="84e16-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="84e16-115">Seçin **varlıklar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="84e16-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="84e16-116">Pencerenin alt kısmındaki tıklatın **ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="84e16-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="84e16-117">Tıklatın **zamanlama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="84e16-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="84e16-118">Tür a **adı** ve isteğe bağlı olarak bir **açıklama** için yeni schedule.your zamanlamanın çalışacağı **bir kez**, **saatlik**, **günlük**, **haftalık**, veya **aylık**.</span><span class="sxs-lookup"><span data-stu-id="84e16-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="84e16-119">Belirtin bir **başlangıç saati** ve seçtiğiniz zamanlamanın türüne bağlı olarak diğer seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="84e16-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="84e16-120">Azure portalında yeni bir zamanlama oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="84e16-121">Azure portalından automation hesabınız tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e16-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="84e16-122">Tıklatın **zamanlamaları** açmak için kutucuğa **zamanlamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e16-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="84e16-123">Tıklatın **bir zamanlama Ekle** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="84e16-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="84e16-124">Üzerinde **yeni zamanlama** dikey penceresinde bir **adı** ve isteğe bağlı olarak bir **açıklama** yeni zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="84e16-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="84e16-125">Bir kez zamanlamanın çalışacağı olup olmadığını veya bir yeniden zamanlamada seçerek **kez** veya **yineleme**.</span><span class="sxs-lookup"><span data-stu-id="84e16-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="84e16-126">Seçerseniz **kez** belirtin bir **başlangıç zamanı** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="84e16-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="84e16-127">Seçerseniz **yineleme**, belirtin bir **başlangıç zamanı** ve ne sıklıkta runbook - göre yinelemek istediğiniz sıklığını **saat**, **gün**, **hafta**, ya da **ay**.</span><span class="sxs-lookup"><span data-stu-id="84e16-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="84e16-128">Seçerseniz **hafta** veya **ay** aşağı açılan listeden **yineleme seçeneği** dikey penceresinde ve seçime bağlı görünür **yineleme seçeneği** dikey sunulabilir ve seçtiyseniz, haftanın günü seçebilirsiniz **hafta**.</span><span class="sxs-lookup"><span data-stu-id="84e16-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="84e16-129">Seçtiyseniz **ay**, tarafından seçebilirsiniz **haftanın günleri** veya takvim ayın belirli günlerine ve son olarak, çalıştırmak ayın son gününde veya ve ardından istiyorsunuz **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="84e16-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="84e16-130">Windows PowerShell ile yeni bir zamanlama oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="84e16-131">Kullanabileceğiniz [yeni AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) Azure Otomasyonu'nda Klasik runbook'lar için yeni bir zamanlama oluşturmak için cmdlet'i veya [yeni AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet'i Azure portalında runbook'lar için.</span><span class="sxs-lookup"><span data-stu-id="84e16-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="84e16-132">Zamanlama ve çalışmalı sıklığı için başlangıç saatini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e16-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="84e16-133">Aşağıdaki örnek komutlar her gün 3:30 Şöyle bir Azure Hizmet Yönetimi cmdlet'iyle 20 Ocak 2015 tarihinde başlatma sırasında çalışan yeni bir zamanlama oluşturmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="84e16-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="84e16-134">Aşağıdaki örnek komutlar bir Azure Resource Manager cmdlet'i kullanılarak her ayın 30 ve 15'inden için bir zamanlama oluşturmak nasıl gösterilir.</span><span class="sxs-lookup"><span data-stu-id="84e16-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="84e16-135">Bir runbook'a bir zamanlama bağlama</span><span class="sxs-lookup"><span data-stu-id="84e16-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="84e16-136">Bir runbook için birden çok zamanlama bağlanabilir ve bir zamanlama birden çok runbook bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="84e16-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="84e16-137">Bir runbook'un parametreleri varsa, daha sonra değerleri kendileri için sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e16-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="84e16-138">Zorunlu parametreler için değer sağlamalısınız ve isteğe bağlı parametreler için değerler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="84e16-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="84e16-139">Bu zamanlama tarafından runbook her başlatıldığında bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84e16-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="84e16-140">Aynı runbook başka bir plana bağlayın ve farklı parametre değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="84e16-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="84e16-141">Klasik Azure portalı ile runbook için bir zamanlama bağlamak için</span><span class="sxs-lookup"><span data-stu-id="84e16-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="84e16-142">Klasik Azure portalında seçin **Otomasyon** ve ardından bir Otomasyon hesabı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="84e16-143">Seçin **Runbook'lar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="84e16-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="84e16-144">Zamanlamak için runbook'un adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="84e16-145">Tıklatın **zamanlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="84e16-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="84e16-146">Runbook şu anda bir zamanlamaya bağlı olmayan sonra seçeneğine verilen **yeni bir zamanlama Bağla** veya **varolan bir zamanlama Bağla**.</span><span class="sxs-lookup"><span data-stu-id="84e16-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="84e16-147">Runbook şu anda bir zamanlamaya bağlıysa, tıklatın **bağlantı** bu seçeneklerine erişmek için pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="84e16-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="84e16-148">Runbook'un parametreleri varsa, bunların değerleri istenir.</span><span class="sxs-lookup"><span data-stu-id="84e16-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="84e16-149">Azure portal ile bir runbook için bir zamanlama bağlamak için</span><span class="sxs-lookup"><span data-stu-id="84e16-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="84e16-150">Azure portalından automation hesabınız tıklatın **Runbook'lar** açmak için kutucuğa **Runbook'lar** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e16-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="84e16-151">Zamanlamak için runbook'un adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="84e16-152">Runbook şu anda bir zamanlamaya bağlı değilse yeni bir zamanlama ya da mevcut bir zamanlamayı bağlantısını oluşturma seçeneğini verilen.</span><span class="sxs-lookup"><span data-stu-id="84e16-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="84e16-153">Runbook parametrelere sahipse, seçeneğini seçebilmenize **çalıştırma ayarlarını (varsayılan: Azure) Değiştir** ve **parametreleri** dikey bilgileri buna göre girebilecekleri sunulur.</span><span class="sxs-lookup"><span data-stu-id="84e16-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="84e16-154">Windows PowerShell ile bir runbook için bir zamanlama bağlamak için</span><span class="sxs-lookup"><span data-stu-id="84e16-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="84e16-155">Kullanabileceğiniz [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) klasik bir runbook'a bir zamanlama bağlamak için veya [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet'i Azure portalında runbook'lar için.</span><span class="sxs-lookup"><span data-stu-id="84e16-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="84e16-156">Parametreleri parametresiyle runbook'un parametreleri için değerler belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e16-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="84e16-157">Bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) parametre değerleri belirtme hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="84e16-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="84e16-158">Aşağıdaki örnek komutlar parametrelere sahip bir Azure Hizmet Yönetimi cmdlet'i kullanılarak bir zamanlama Bağla gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84e16-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="84e16-159">Aşağıdaki örnek komutlar parametrelere sahip bir Azure Resource Manager cmdlet'i kullanılarak bir runbook'a bir zamanlama Bağla gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84e16-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="84e16-160">Bir zamanlama devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="84e16-160">Disabling a schedule</span></span>
<span data-ttu-id="84e16-161">Bir zamanlama devre dışı bıraktığınızda, bağlı tüm runbook artık bu zamanlamaya göre çalıştır.</span><span class="sxs-lookup"><span data-stu-id="84e16-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="84e16-162">El ile bir zamanlama devre dışı bırakmak veya bunları oluşturduğunuzda bir sıklığı ile zamanlama için sona erme süresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="84e16-163">Sona erme zamanı geldiğinde, zamanlama devre dışı bırakılacak.</span><span class="sxs-lookup"><span data-stu-id="84e16-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="84e16-164">Azure Klasik portalından bir zamanlama devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="84e16-165">Zamanlama için Zamanlama Ayrıntıları sayfası, Klasik Azure portalından bir zamanlama devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e16-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="84e16-166">Azure Klasik portalında Otomasyon seçin ve ardından bir Otomasyon hesabı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="84e16-167">Varlıklar sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="84e16-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="84e16-168">Kendi ayrıntı sayfası açmak için bir zamanlama adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="84e16-169">Değişiklik **etkin** için **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="84e16-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="84e16-170">Azure portalından bir zamanlama devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="84e16-171">Azure portalından automation hesabınız tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e16-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="84e16-172">Tıklatın **zamanlamaları** açmak için kutucuğa **zamanlamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e16-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="84e16-173">Ayrıntılar dikey penceresini açmak için bir zamanlama adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e16-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="84e16-174">Değişiklik **etkin** için **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="84e16-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="84e16-175">Windows PowerShell ile bir zamanlama devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="84e16-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="84e16-176">Kullanabileceğiniz [kümesi AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) klasik bir runbook için varolan bir zamanlamanın özelliklerini değiştirmek için cmdlet veya [kümesi AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet'i Azure portalında runbook'lar için.</span><span class="sxs-lookup"><span data-stu-id="84e16-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="84e16-177">Zamanlama devre dışı bırakmak için belirtmek **false** için **IsEnabled** parametresi.</span><span class="sxs-lookup"><span data-stu-id="84e16-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="84e16-178">Aşağıdaki örnek komutlar Azure Hizmet Yönetimi cmdlet'ini kullanarak bir zamanlama devre dışı bırakma göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="84e16-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="84e16-179">Aşağıdaki örnek komutlar bir Azure Resource Manager cmdlet'i kullanılarak bir runbook için bir zamanlama devre dışı bırakma göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="84e16-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="84e16-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84e16-180">Next steps</span></span>
* <span data-ttu-id="84e16-181">Zamanlama ile çalışma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu zamanlama varlıkları](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="84e16-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="84e16-182">Azure Otomasyonu runbook'ları kullanmaya başlamak için bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="84e16-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 


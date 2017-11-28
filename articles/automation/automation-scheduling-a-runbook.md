---
title: Azure Automation runbook aaaScheduling | Microsoft Docs
description: "Açıklar nasıl toocreate bir Azure Otomasyonu zamanlama belirli bir zamanda veya yinelenen bir zamanlamaya göre otomatik olarak bir runbook başlatabilirsiniz."
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
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="d910d-103">Azure Otomasyonu’nda runbook zamanlama</span><span class="sxs-lookup"><span data-stu-id="d910d-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="d910d-104">tooschedule bir runbook belirtilen bir zamanda Azure Otomasyonu toostart içinde tooone ya da daha fazla zamanlama Bağla.</span><span class="sxs-lookup"><span data-stu-id="d910d-104">tooschedule a runbook in Azure Automation toostart at a specified time, you link it tooone or more schedules.</span></span> <span data-ttu-id="d910d-105">Bir zamanlama bir kez çalıştır yapılandırılmış tooeither olabilir veya bir yeniden saatlik veya günlük zamanlamayla hello Klasik Azure portalı runbook'ları ve hello Azure portalı runbook'ları, ayrıca bunları hello haftada haftalık, aylık, belirli gün veya gün için zamanlayabilirsiniz Merhaba ay veya hello ayın belirli bir günü.</span><span class="sxs-lookup"><span data-stu-id="d910d-105">A schedule can be configured tooeither run once or on a reoccurring hourly or daily schedule for runbooks in hello Azure classic portal and for runbooks in hello Azure portal,  you can additionally schedule them for weekly, monthly, specific days of hello week or days of hello month, or a particular day of hello month.</span></span>  <span data-ttu-id="d910d-106">Bir runbook bağlantılı toomultiple zamanlamaları olabilir ve birden çok runbook bağlı tooit bir zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="d910d-106">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="d910d-107">Bir zamanlama oluşturma</span><span class="sxs-lookup"><span data-stu-id="d910d-107">Creating a schedule</span></span>
<span data-ttu-id="d910d-108">Merhaba Klasik portalında veya Windows PowerShell ile hello Azure portal, runbook'lar için yeni bir zamanlama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d910d-108">You can create a new schedule for runbooks in hello Azure portal, in hello classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="d910d-109">Hello Azure Klasik kullanarak bir runbook tooa zamanlamaya bağladığınızda, yeni bir zamanlama ya da Azure portal oluşturma hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="d910d-109">You also have hello option of creating a new schedule when you link a runbook tooa schedule using hello Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d910d-110">Zamanlama runbook ile ilişkilendirdiğinizde, Automation hesabınızı hello geçerli hello modülleri sürümleri depolar ve toothat zamanlama bağlar.</span><span class="sxs-lookup"><span data-stu-id="d910d-110">When you associate a schedule with a runbook, Automation stores hello current versions of hello modules in your account and links them toothat schedule.</span></span>  <span data-ttu-id="d910d-111">Başka bir deyişle, bir zamanlama oluşturduğunuzda hesabınızda sürüm 1.0 sahip bir modül var ve bu nedenle hello modülü tooversion 2.0 güncelleştirmek, hello zamanlama toouse 1.0 devam eder.</span><span class="sxs-lookup"><span data-stu-id="d910d-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update hello module tooversion 2.0, hello schedule will continue toouse 1.0.</span></span>  <span data-ttu-id="d910d-112">Sipariş toouse hello güncelleştirilmiş modülü sürümünde, yeni bir zamanlama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d910d-112">In order toouse hello updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a><span data-ttu-id="d910d-113">toocreate hello Klasik Azure portalında yeni bir zamanlama</span><span class="sxs-lookup"><span data-stu-id="d910d-113">toocreate a new schedule in hello Azure classic portal</span></span>
1. <span data-ttu-id="d910d-114">Hello Klasik Azure portalı, Otomasyon seçin ve ardından bir Otomasyon hesabı hello adını seçin.</span><span class="sxs-lookup"><span data-stu-id="d910d-114">In hello Azure classic portal, select Automation and then then select hello name of an automation account.</span></span>
2. <span data-ttu-id="d910d-115">Select hello **varlıklar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d910d-115">Select hello **Assets** tab.</span></span>
3. <span data-ttu-id="d910d-116">Merhaba penceresinin Hello altında tıklatın **ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d910d-116">At hello bottom of hello window, click **Add Setting**.</span></span>
4. <span data-ttu-id="d910d-117">Tıklatın **zamanlama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d910d-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="d910d-118">Tür a **adı** ve isteğe bağlı olarak bir **açıklama** hello yeni schedule.your için zamanlamanın çalışacağı **bir kez**, **saatlik**, **Günlük**, **haftalık**, veya **aylık**.</span><span class="sxs-lookup"><span data-stu-id="d910d-118">Type a **Name** and optionally a **Description** for hello new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="d910d-119">Belirtin bir **başlangıç saati** ve diğer seçenekler, seçtiğiniz zamanlamanın hello türüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="d910d-119">Specify a **Start Time** and other options depending on hello type of schedule that you selected.</span></span>

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a><span data-ttu-id="d910d-120">toocreate hello Azure portal'ın yeni bir zamanlama</span><span class="sxs-lookup"><span data-stu-id="d910d-120">toocreate a new schedule in hello Azure portal</span></span>
1. <span data-ttu-id="d910d-121">Hello Azure portalından, automation hesabınızı hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="d910d-121">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="d910d-122">Merhaba tıklatın **zamanlamaları** döşeme tooopen hello **zamanlamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d910d-122">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="d910d-123">Tıklatın **bir zamanlama Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="d910d-123">Click **Add a schedule** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d910d-124">Merhaba üzerinde **yeni zamanlama** dikey penceresinde bir **adı** ve isteğe bağlı olarak bir **açıklama** hello yeni zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="d910d-124">On hello **New schedule** blade, type a **Name** and optionally a **Description** for hello new schedule.</span></span>
5. <span data-ttu-id="d910d-125">Bir kez Hello zamanlamanın çalışacağı olup olmadığını veya yeniden zamanlamada seçerek **kez** veya **yineleme**.</span><span class="sxs-lookup"><span data-stu-id="d910d-125">Select whether hello schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="d910d-126">Seçerseniz **kez** belirtin bir **başlangıç zamanı** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d910d-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="d910d-127">Seçerseniz **yineleme**, belirtin bir **başlangıç zamanı** ve ne sıklıkta hello runbook toorepeat - göre istediğiniz hello sıklığı **saat**, **gün**, **hafta**, ya da **ay**.</span><span class="sxs-lookup"><span data-stu-id="d910d-127">If you select **Recurrence**, specify a **Start time** and hello frequency for how often you want hello runbook toorepeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="d910d-128">Seçerseniz **hafta** veya **ay** hello aşağı açılan listeden hello **yineleme seçeneği** hello dikey penceresinde ve seçime bağlı hello görünür **yineleme seçenek** dikey sunulabilir ve seçtiyseniz, haftanın başlangıç günü seçebilirsiniz **hafta**.</span><span class="sxs-lookup"><span data-stu-id="d910d-128">If you select **week** or **month** from hello drop-down list, hello **Recurrence option** will appear in hello blade and upon selection, hello **Recurrence option** blade will be presented and you can select hello day of week if you selected **week**.</span></span>  <span data-ttu-id="d910d-129">Seçtiyseniz **ay**, tarafından seçebilirsiniz **haftanın günleri** veya üzerinde hello ayın belirli günlerine hello takvim ve toorun son olarak, istediğiniz üzerinde veya hello ayın son günü hello ve ardından **Tamam** .</span><span class="sxs-lookup"><span data-stu-id="d910d-129">If you selected **month**, you can choose by **week days** or specific days of hello month on hello calendar and finally, do you want toorun it on hello last day of hello month or not and then click **OK**.</span></span>   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="d910d-130">toocreate Windows PowerShell ile yeni bir zamanlama</span><span class="sxs-lookup"><span data-stu-id="d910d-130">toocreate a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="d910d-131">Merhaba kullanabilirsiniz [yeni AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate yeni bir Azure Otomasyonu zamanlama Klasik runbook'lar için veya [yeni AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) hello Azure runbook'lar için cmdlet Portal.</span><span class="sxs-lookup"><span data-stu-id="d910d-131">You can use hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="d910d-132">Merhaba zamanlama ve hello frekans çalışmalı hello başlangıç zamanını belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d910d-132">You must specify hello start time for hello schedule and hello frequency it should run.</span></span>

<span data-ttu-id="d910d-133">Aşağıdaki örnek komutlar hello Göster nasıl toocreate yeni bir zamanlama her çalıştıran 3:30 Şöyle bir Azure Hizmet Yönetimi cmdlet'iyle 20 Ocak 2015 tarihinde başlayan adresindeki gün.</span><span class="sxs-lookup"><span data-stu-id="d910d-133">hello following sample commands show how toocreate a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="d910d-134">Merhaba aşağıdaki örnek gösterir nasıl komutları toocreate hello için bir zamanlama 15 ve bir Azure Resource Manager cmdlet'i kullanılarak her ayın 30.</span><span class="sxs-lookup"><span data-stu-id="d910d-134">hello following sample commands shows how toocreate a schedule for hello 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a><span data-ttu-id="d910d-135">Bir zamanlama tooa runbook bağlama</span><span class="sxs-lookup"><span data-stu-id="d910d-135">Linking a schedule tooa runbook</span></span>
<span data-ttu-id="d910d-136">Bir runbook bağlantılı toomultiple zamanlamaları olabilir ve birden çok runbook bağlı tooit bir zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="d910d-136">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span> <span data-ttu-id="d910d-137">Bir runbook'un parametreleri varsa, daha sonra değerleri kendileri için sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d910d-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="d910d-138">Zorunlu parametreler için değer sağlamalısınız ve isteğe bağlı parametreler için değerler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d910d-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="d910d-139">Bu zamanlama tarafından hello runbook her başlatıldığında bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d910d-139">These values will be used each time hello runbook is started by this schedule.</span></span>  <span data-ttu-id="d910d-140">Ekleyebilir miyim hello aynı runbook tooanother zamanlaması ve farklı parametre değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d910d-140">You can attach hello same runbook tooanother schedule and specify different parameter values.</span></span>

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="d910d-141">toolink zamanlama tooa runbook hello Klasik Azure portalı ile</span><span class="sxs-lookup"><span data-stu-id="d910d-141">toolink a schedule tooa runbook with hello Azure classic portal</span></span>
1. <span data-ttu-id="d910d-142">Hello Klasik Azure portalı, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d910d-142">In hello Azure classic portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="d910d-143">Select hello **Runbook'lar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d910d-143">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="d910d-144">Merhaba runbook tooschedule Hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d910d-144">Click on hello name of hello runbook tooschedule.</span></span>
4. <span data-ttu-id="d910d-145">Merhaba tıklatın **zamanlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d910d-145">Click hello **Schedule** tab.</span></span>
5. <span data-ttu-id="d910d-146">Merhaba runbook şu anda bağlı tooa zamanlama değil sonra çok hello seçeneği sunulur**tooa yeni zamanlama bağlantı** veya **tooan varolan zamanlama bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="d910d-146">If hello runbook is not currently linked tooa schedule, then you will be given hello option too**Link tooa New Schedule** or **Link tooan Existing Schedule**.</span></span>  <span data-ttu-id="d910d-147">Merhaba runbook şu anda bağlı tooa zamanlama ise, tıklatın **bağlantı** , bu seçenekleri hello penceresi tooaccess alt hello.</span><span class="sxs-lookup"><span data-stu-id="d910d-147">If hello runbook is currently linked tooa schedule, click **Link** at hello bottom of hello window tooaccess these options.</span></span>
6. <span data-ttu-id="d910d-148">Merhaba runbook'un parametreleri varsa, bunların değerleri istenir.</span><span class="sxs-lookup"><span data-stu-id="d910d-148">If hello runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a><span data-ttu-id="d910d-149">toolink zamanlama tooa runbook hello Azure portal ile</span><span class="sxs-lookup"><span data-stu-id="d910d-149">toolink a schedule tooa runbook with hello Azure portal</span></span>
1. <span data-ttu-id="d910d-150">Hello Azure portalından, automation hesabınızı hello tıklatın **Runbook'lar** döşeme tooopen hello **Runbook'lar** dikey.</span><span class="sxs-lookup"><span data-stu-id="d910d-150">In hello Azure portal, from your automation account, click hello **Runbooks** tile tooopen hello **Runbooks** blade.</span></span>
2. <span data-ttu-id="d910d-151">Merhaba runbook tooschedule Hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d910d-151">Click on hello name of hello runbook tooschedule.</span></span>
3. <span data-ttu-id="d910d-152">Sonra Hello runbook şu anda bağlı tooa zamanlama değilse yeni bir zamanlama verilen hello seçeneği toocreate olması veya zamanlama varolan tooan bağlantısını.</span><span class="sxs-lookup"><span data-stu-id="d910d-152">If hello runbook is not currently linked tooa schedule, then you will be given hello option toocreate a new schedule or link tooan existing schedule.</span></span>  
4. <span data-ttu-id="d910d-153">Merhaba runbook'un parametreleri varsa hello seçeneği seçebilirsiniz **çalıştırma ayarlarını (varsayılan: Azure) Değiştir** ve hello **parametreleri** dikey penceresinde hello bilgileri buna göre girebilecekleri sunulur.</span><span class="sxs-lookup"><span data-stu-id="d910d-153">If hello runbook has parameters, you can select hello option **Modify run settings (Default:Azure)** and hello **Parameters** blade is presented where you can enter hello information accordingly.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a><span data-ttu-id="d910d-154">Windows PowerShell ile bir zamanlama tooa runbook toolink</span><span class="sxs-lookup"><span data-stu-id="d910d-154">toolink a schedule tooa runbook with Windows PowerShell</span></span>
<span data-ttu-id="d910d-155">Merhaba kullanabilirsiniz [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink bir zamanlama tooa Klasik runbook veya [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet'i hello Azure portalı runbook'ları için.</span><span class="sxs-lookup"><span data-stu-id="d910d-155">You can use hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink a schedule tooa classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in hello Azure portal.</span></span>  <span data-ttu-id="d910d-156">Merhaba parametreleri parametresiyle hello runbook'un parametreleri için değerler belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d910d-156">You can specify values for hello runbook’s parameters with hello Parameters parameter.</span></span> <span data-ttu-id="d910d-157">Bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) parametre değerleri belirtme hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d910d-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="d910d-158">Merhaba aşağıdaki örnek komutlar Göster nasıl toolink parametrelere sahip bir Azure Hizmet Yönetimi cmdlet'i kullanılarak bir zamanlama.</span><span class="sxs-lookup"><span data-stu-id="d910d-158">hello following sample commands show how toolink a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="d910d-159">Merhaba aşağıdaki örnek komutlar Göster nasıl toolink parametrelere sahip bir Azure Resource Manager cmdlet'i kullanılarak bir zamanlama tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="d910d-159">hello following sample commands show how toolink a schedule tooa runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="d910d-160">Bir zamanlama devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="d910d-160">Disabling a schedule</span></span>
<span data-ttu-id="d910d-161">Bir zamanlama devre dışı bıraktığınızda, tüm bağlı olan runbook'lardan tooit artık bu zamanlamaya göre çalıştır.</span><span class="sxs-lookup"><span data-stu-id="d910d-161">When you disable a schedule, any runbooks linked tooit will no longer run on that schedule.</span></span> <span data-ttu-id="d910d-162">El ile bir zamanlama devre dışı bırakmak veya bunları oluşturduğunuzda bir sıklığı ile zamanlama için sona erme süresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d910d-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="d910d-163">Merhaba sona erme süresine ulaşıldığında hello zamanlama devre dışı bırakılacak.</span><span class="sxs-lookup"><span data-stu-id="d910d-163">When hello expiration time is reached, hello schedule will be disabled.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a><span data-ttu-id="d910d-164">toodisable hello Klasik Azure portalı zamanlamadan</span><span class="sxs-lookup"><span data-stu-id="d910d-164">toodisable a schedule from hello Azure classic portal</span></span>
<span data-ttu-id="d910d-165">Merhaba hello Zamanlama Ayrıntıları sayfası hello zamanlama için Klasik Azure portalından bir zamanlama devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d910d-165">You can disable a schedule in hello Azure classic portal from hello Schedule Details page for hello schedule.</span></span>

1. <span data-ttu-id="d910d-166">Hello Klasik Azure portalı, Otomasyon seçin ve ardından bir Otomasyon hesabı hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d910d-166">In hello Azure classic portal, select Automation and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="d910d-167">Merhaba varlıklar sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d910d-167">Select hello Assets tab.</span></span>
3. <span data-ttu-id="d910d-168">Kendi ayrıntı sayfası zamanlama tooopen Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d910d-168">Click hello name of a schedule tooopen its detail page.</span></span>
4. <span data-ttu-id="d910d-169">Değişiklik **etkin** çok**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="d910d-169">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a><span data-ttu-id="d910d-170">toodisable hello Azure portal zamanlamadan</span><span class="sxs-lookup"><span data-stu-id="d910d-170">toodisable a schedule from hello Azure portal</span></span>
1. <span data-ttu-id="d910d-171">Hello Azure portalından, automation hesabınızı hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="d910d-171">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="d910d-172">Merhaba tıklatın **zamanlamaları** döşeme tooopen hello **zamanlamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d910d-172">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="d910d-173">Bir zamanlama tooopen hello ayrıntıları dikey penceresinde Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d910d-173">Click hello name of a schedule tooopen hello details blade.</span></span>
4. <span data-ttu-id="d910d-174">Değişiklik **etkin** çok**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="d910d-174">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-with-windows-powershell"></a><span data-ttu-id="d910d-175">toodisable Windows PowerShell ile bir zamanlama</span><span class="sxs-lookup"><span data-stu-id="d910d-175">toodisable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="d910d-176">Merhaba kullanabilirsiniz [kümesi AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello klasik bir runbook için varolan bir zamanlamanın özelliklerini veya [kümesi AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) hello Azure runbook'lar için cmdlet Portal.</span><span class="sxs-lookup"><span data-stu-id="d910d-176">You can use hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="d910d-177">toodisable hello zamanlama, belirtin **false** hello için **IsEnabled** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d910d-177">toodisable hello schedule, specify **false** for hello **IsEnabled** parameter.</span></span>

<span data-ttu-id="d910d-178">Aşağıdaki örnek komutlar hello nasıl kullanarak bir zamanlama toodisable hello Azure Hizmet Yönetimi cmdlet'ini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d910d-178">hello following sample commands show how toodisable a schedule using hello Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="d910d-179">Merhaba aşağıdaki örnek komutlar Göster nasıl toodisable bir Azure Resource Manager cmdlet'i kullanılarak bir runbook için bir zamanlama.</span><span class="sxs-lookup"><span data-stu-id="d910d-179">hello following sample commands show how toodisable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="d910d-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d910d-180">Next steps</span></span>
* <span data-ttu-id="d910d-181">zamanlama ile çalışma hakkında daha fazla toolearn bakın [Azure Otomasyonu zamanlama varlıkları](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="d910d-181">toolearn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="d910d-182">Azure Otomasyonu runbook'ları kullanmaya tooget bakın [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="d910d-182">tooget started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 


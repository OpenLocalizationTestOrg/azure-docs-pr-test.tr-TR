---
title: "Azure Otomasyonu runbook başlatma | Microsoft Docs"
description: "Azure portalı ve Windows PowerShell kullanma hakkında ayrıntılar verilmiştir ve Azure Otomasyon runbook'u başlatmak için kullanılır farklı yöntemleri özetler."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="45e99-103">Azure Otomasyonu runbook başlatma</span><span class="sxs-lookup"><span data-stu-id="45e99-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="45e99-104">Aşağıdaki tabloda, Azure automation'da belirli senaryonuza en uygun bir runbook'u başlatmak için bu yöntem belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="45e99-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="45e99-105">Bu makalede Azure portal ile ve Windows PowerShell ile bir runbook'u başlatma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="45e99-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="45e99-106">Aşağıdaki bağlantılardan erişebilirsiniz diğer belgelerinde diğer yöntemler hakkında ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45e99-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="45e99-107">**YÖNTEMİ**</span><span class="sxs-lookup"><span data-stu-id="45e99-107">**METHOD**</span></span> | <span data-ttu-id="45e99-108">**ÖZELLİKLERİ**</span><span class="sxs-lookup"><span data-stu-id="45e99-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="45e99-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="45e99-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="45e99-110">En basit yöntem etkileşimli kullanıcı arabirimi ile.</span><span class="sxs-lookup"><span data-stu-id="45e99-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="45e99-111">Basit parametre değerlerini sağlamak için form.</span><span class="sxs-lookup"><span data-stu-id="45e99-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="45e99-112">İş durumu kolayca izleyin.</span><span class="sxs-lookup"><span data-stu-id="45e99-112">Easily track job state.</span></span><br> <li><span data-ttu-id="45e99-113">İle Azure oturum açma kimliği doğrulanmış erişim.</span><span class="sxs-lookup"><span data-stu-id="45e99-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="45e99-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="45e99-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="45e99-115">Komut satırından Windows PowerShell cmdlet'leri ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="45e99-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="45e99-116">Birden çok adımı otomatik Çözümle eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="45e99-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="45e99-117">Sertifika veya OAuth kullanıcı asıl / hizmet isteği kimliği doğrulanır asıl.</span><span class="sxs-lookup"><span data-stu-id="45e99-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="45e99-118">Basit ve karmaşık parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="45e99-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="45e99-119">İş durumu izleyin.</span><span class="sxs-lookup"><span data-stu-id="45e99-119">Track job state.</span></span><br> <li><span data-ttu-id="45e99-120">PowerShell cmdlet'leri desteklemek için gereken istemci.</span><span class="sxs-lookup"><span data-stu-id="45e99-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="45e99-121">Azure Otomasyonu API</span><span class="sxs-lookup"><span data-stu-id="45e99-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="45e99-122">En esnek yöntem, ancak ayrıca en karmaşık.</span><span class="sxs-lookup"><span data-stu-id="45e99-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="45e99-123">HTTP isteği yapabilen dilediğiniz özel kodu çağırın.</span><span class="sxs-lookup"><span data-stu-id="45e99-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="45e99-124">İstek sertifika ya da Oauth kullanıcı asıl / hizmet kimliği doğrulanmış sorumlu.</span><span class="sxs-lookup"><span data-stu-id="45e99-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="45e99-125">Basit ve karmaşık parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="45e99-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="45e99-126">İş durumu izleyin.</span><span class="sxs-lookup"><span data-stu-id="45e99-126">Track job state.</span></span> |
| [<span data-ttu-id="45e99-127">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="45e99-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="45e99-128">Runbook tek HTTP isteğinden başlatın.</span><span class="sxs-lookup"><span data-stu-id="45e99-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="45e99-129">Güvenlik belirteci URL ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="45e99-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="45e99-130">İstemci Web kancası oluşturduğunuzda belirtilen parametre değerleri geçersiz kılamaz.</span><span class="sxs-lookup"><span data-stu-id="45e99-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="45e99-131">Runbook ile HTTP istek ayrıntıları doldurulmuş tek bir parametre tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45e99-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="45e99-132">Web kancası URL'si aracılığıyla iş durumu izleme yeteneği yok.</span><span class="sxs-lookup"><span data-stu-id="45e99-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="45e99-133">Azure uyarısına yanıt</span><span class="sxs-lookup"><span data-stu-id="45e99-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="45e99-134">Azure uyarı yanıtta bir runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="45e99-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="45e99-135">Web kancası runbook ve uyarı için bağlantı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45e99-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="45e99-136">Güvenlik belirteci URL ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="45e99-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="45e99-137">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="45e99-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="45e99-138">Saatlik, günlük, haftalık veya aylık zamanlamaya göre otomatik olarak runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="45e99-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="45e99-139">Azure portal, PowerShell cmdlet'leri veya Azure API aracılığıyla zamanlama yönetme.</span><span class="sxs-lookup"><span data-stu-id="45e99-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="45e99-140">Zamanlama ile kullanılacak parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="45e99-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="45e99-141">Başka bir Runbook'tan</span><span class="sxs-lookup"><span data-stu-id="45e99-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="45e99-142">Bir runbook başka bir runbook'taki bir etkinlik olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="45e99-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="45e99-143">Birden çok runbook tarafından kullanılan işlevselliği için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="45e99-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="45e99-144">Alt runbook parametre değerlerini sağlayın ve çıktı üst runbook'ta kullanın.</span><span class="sxs-lookup"><span data-stu-id="45e99-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="45e99-145">Aşağıdaki resimde bir runbook yaşam döngüsünü ayrıntılı adım adım işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="45e99-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="45e99-146">Bir runbook Azure Otomasyon karma Runbook çalışanı için gerekli bileşenleri Azure Otomasyon çalışma kitabı ve farklı bileşenler arasındaki etkileşimler yürütmek için başlatılan farklı yolları içerir.</span><span class="sxs-lookup"><span data-stu-id="45e99-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="45e99-147">Otomasyon runbook'ları, veri merkezinizde çalıştırma hakkında bilgi edinmek için bkz [karma runbook çalışanları](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="45e99-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook mimarisi](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="45e99-149">Azure portalıyla bir runbook'u başlatma</span><span class="sxs-lookup"><span data-stu-id="45e99-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="45e99-150">Azure portalında seçin **Otomasyon** ve ardından bir Otomasyon hesabı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45e99-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="45e99-151">Hub menüsünde seçin **Runbook'lar**.</span><span class="sxs-lookup"><span data-stu-id="45e99-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="45e99-152">Üzerinde **Runbook'lar** dikey penceresinde, bir runbook seçin ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="45e99-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="45e99-153">Runbook'un parametreleri varsa her parametre için bir metin kutusu değerlerini sağlamak için istenir.</span><span class="sxs-lookup"><span data-stu-id="45e99-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="45e99-154">Bkz: [Runbook parametreleri](#Runbook-parameters) altında daha fazla ayrıntı için parametreleri.</span><span class="sxs-lookup"><span data-stu-id="45e99-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="45e99-155">Üzerinde **iş** dikey penceresinde, runbook işinin durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45e99-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="45e99-156">Windows PowerShell ile bir runbook başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="45e99-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="45e99-157">Kullanabileceğiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) Windows PowerShell ile bir runbook'u başlatın.</span><span class="sxs-lookup"><span data-stu-id="45e99-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="45e99-158">Aşağıdaki örnek kod, Test-Runbook adlı bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="45e99-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="45e99-159">Başlangıç AzureRmAutomationRunbook runbook başlatıldıktan sonra durumunu izlemek için kullanabileceğiniz bir iş nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="45e99-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="45e99-160">Bu iş nesnesi ile sonra kullanabileceğiniz [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) işin durumunu belirlemek için ve [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) çıktısını almak için.</span><span class="sxs-lookup"><span data-stu-id="45e99-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="45e99-161">Aşağıdaki örnek kod, Test-Runbook, tamamlandı ve ardından çıktısını görüntüler tamamlanmasını bekler adlı bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="45e99-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="45e99-162">Runbook'un parametreler gerektirmesi durumunda bunları sağlamanız gereken bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) burada karma tablosu anahtarının parametre adıyla eşleştiği ve değerin parametre değeridir.</span><span class="sxs-lookup"><span data-stu-id="45e99-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="45e99-163">Aşağıdaki örnek, FirstName ve LastName, RepeatCount adlı bir tamsayı ve Show adlı bir boolean parametresiyle adlı iki dize parametresi ile bir runbook başlatın gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="45e99-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="45e99-164">Parametreleri hakkında ek bilgi için bkz: [Runbook parametreleri](#Runbook-parameters) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="45e99-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="45e99-165">Runbook parametreleri</span><span class="sxs-lookup"><span data-stu-id="45e99-165">Runbook parameters</span></span>
<span data-ttu-id="45e99-166">Azure Portal ya da Windows PowerShell bir runbook'u başlattığınızda talimat Azure Otomasyonu web hizmeti aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="45e99-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="45e99-167">Bu hizmet, karmaşık veri türleriyle parametreleri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="45e99-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="45e99-168">Karmaşık bir parametre için bir değer sağlanması gerekiyor durumunda, satır içi başka bir runbook'tan açıklandığı gibi çağırmalısınız [alt runbook'ları Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="45e99-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="45e99-169">Azure Otomasyonu web hizmeti aşağıdaki bölümlerde açıklandığı gibi belirli veri türlerini kullanarak parametreler için özel işlevler sağlar.</span><span class="sxs-lookup"><span data-stu-id="45e99-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="45e99-170">Adlandırılmış değerler</span><span class="sxs-lookup"><span data-stu-id="45e99-170">Named values</span></span>
<span data-ttu-id="45e99-171">Veri türü [object] parametredir sonra adlandırılmış değerler listesini göndermek için şu JSON biçimini kullanabilirsiniz: *{Ad1: 'Değer1', ad2: 'Değer2', AD3: 'Değer3'}*.</span><span class="sxs-lookup"><span data-stu-id="45e99-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="45e99-172">Bu değerler basit türler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="45e99-172">These values must be simple types.</span></span> <span data-ttu-id="45e99-173">Runbook parametre olarak alıp almayacağını bir [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) her adlandırılmış değerine karşılık gelen özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="45e99-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="45e99-174">Kullanıcı adında bir parametre kabul eden aşağıdaki sınama runbook'unu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="45e99-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="45e99-175">Aşağıdaki metin kullanıcı parametresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="45e99-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="45e99-176">Bu durum şunlara sebep olur.</span><span class="sxs-lookup"><span data-stu-id="45e99-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="45e99-177">Diziler</span><span class="sxs-lookup"><span data-stu-id="45e99-177">Arrays</span></span>
<span data-ttu-id="45e99-178">Parametresi [array] gibi bir dizi olup olmadığını veya [string []] değerlerinin listesini göndermek için şu JSON biçimini kullanabilirsiniz: *[Value1, Value2, Value3]*.</span><span class="sxs-lookup"><span data-stu-id="45e99-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="45e99-179">Bu değerler basit türler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="45e99-179">These values must be simple types.</span></span>

<span data-ttu-id="45e99-180">Adlı bir parametre kabul eden aşağıdaki sınama runbook'unu göz önünde bulundurun *kullanıcı*.</span><span class="sxs-lookup"><span data-stu-id="45e99-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="45e99-181">Aşağıdaki metin kullanıcı parametresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="45e99-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="45e99-182">Bu durum şunlara sebep olur.</span><span class="sxs-lookup"><span data-stu-id="45e99-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="45e99-183">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="45e99-183">Credentials</span></span>
<span data-ttu-id="45e99-184">Parametre veri türü ise **PSCredential**, bir Azure Otomasyonu adını sağlayın ve sonra [kimlik bilgisi varlığı](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="45e99-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="45e99-185">Runbook Belirttiğiniz ada sahip kimlik bilgisi alır.</span><span class="sxs-lookup"><span data-stu-id="45e99-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="45e99-186">Kimlik bilgisi adlı bir parametre kabul eden aşağıdaki sınama runbook'unu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="45e99-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="45e99-187">Aşağıdaki metin kullanıcı parametresi adlı bir kimlik bilgisi varlığı olduğunu varsayarak için kullanılabilecek *My kimlik bilgisi*.</span><span class="sxs-lookup"><span data-stu-id="45e99-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="45e99-188">Kullanıcı kimlik bilgisi olduğu kabul *jsmith*, bu durum şunlara sebep olur.</span><span class="sxs-lookup"><span data-stu-id="45e99-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="45e99-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45e99-189">Next steps</span></span>
* <span data-ttu-id="45e99-190">Geçerli makale runbook mimarisinde kaynakları yöneten runbook Azure ve şirket içi karma Runbook çalışanı ile üst düzey bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="45e99-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="45e99-191">Otomasyon runbook'ları, veri merkezinizde çalıştırma hakkında bilgi edinmek için bkz [karma Runbook çalışanları](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="45e99-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="45e99-192">Özel veya ortak işlevleri için diğer runbook'lar tarafından kullanılacak oluşturma modüler runbook'lar hakkında daha fazla bilgi için bkz [alt runbook'ları](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="45e99-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>


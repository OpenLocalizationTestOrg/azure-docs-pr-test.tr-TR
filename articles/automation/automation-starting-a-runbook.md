---
title: Azure Automation runbook aaaStarting | Microsoft Docs
description: "Kullanılan toostart Azure Automation runbook olabilir ve her ikisi de kullanımıyla ilgili ayrıntılar Azure portalı ve Windows PowerShell hello sağlayan hello farklı yöntemler özetler."
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="69dec-103">Azure Otomasyonu runbook başlatma</span><span class="sxs-lookup"><span data-stu-id="69dec-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="69dec-104">Aşağıdaki tablonun hello hello yöntemi toostart en uygun tooyour belirli senaryo Azure Automation runbook belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="69dec-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="69dec-105">Bu makalede Windows PowerShell ile hello Azure portal ile bir runbook'u başlatma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="69dec-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="69dec-106">Ayrıntılar üzerinde hello bağlantılar hello aşağıdaki erişebilirsiniz diğer belgelerinde diğer yöntemleri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="69dec-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="69dec-107">**YÖNTEMİ**</span><span class="sxs-lookup"><span data-stu-id="69dec-107">**METHOD**</span></span> | <span data-ttu-id="69dec-108">**ÖZELLİKLERİ**</span><span class="sxs-lookup"><span data-stu-id="69dec-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="69dec-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="69dec-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="69dec-110">En basit yöntem etkileşimli kullanıcı arabirimi ile.</span><span class="sxs-lookup"><span data-stu-id="69dec-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="69dec-111">Form tooprovide basit parametre değerleri.</span><span class="sxs-lookup"><span data-stu-id="69dec-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="69dec-112">İş durumu kolayca izleyin.</span><span class="sxs-lookup"><span data-stu-id="69dec-112">Easily track job state.</span></span><br> <li><span data-ttu-id="69dec-113">İle Azure oturum açma kimliği doğrulanmış erişim.</span><span class="sxs-lookup"><span data-stu-id="69dec-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="69dec-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="69dec-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="69dec-115">Komut satırından Windows PowerShell cmdlet'leri ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="69dec-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="69dec-116">Birden çok adımı otomatik Çözümle eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="69dec-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="69dec-117">Sertifika veya OAuth kullanıcı asıl / hizmet isteği kimliği doğrulanır asıl.</span><span class="sxs-lookup"><span data-stu-id="69dec-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="69dec-118">Basit ve karmaşık parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69dec-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="69dec-119">İş durumu izleyin.</span><span class="sxs-lookup"><span data-stu-id="69dec-119">Track job state.</span></span><br> <li><span data-ttu-id="69dec-120">İstemci toosupport PowerShell cmdlet'leri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="69dec-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="69dec-121">Azure Otomasyonu API</span><span class="sxs-lookup"><span data-stu-id="69dec-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="69dec-122">En esnek yöntem, ancak ayrıca en karmaşık.</span><span class="sxs-lookup"><span data-stu-id="69dec-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="69dec-123">HTTP isteği yapabilen dilediğiniz özel kodu çağırın.</span><span class="sxs-lookup"><span data-stu-id="69dec-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="69dec-124">İstek sertifika ya da Oauth kullanıcı asıl / hizmet kimliği doğrulanmış sorumlu.</span><span class="sxs-lookup"><span data-stu-id="69dec-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="69dec-125">Basit ve karmaşık parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69dec-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="69dec-126">İş durumu izleyin.</span><span class="sxs-lookup"><span data-stu-id="69dec-126">Track job state.</span></span> |
| [<span data-ttu-id="69dec-127">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="69dec-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="69dec-128">Runbook tek HTTP isteğinden başlatın.</span><span class="sxs-lookup"><span data-stu-id="69dec-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="69dec-129">Güvenlik belirteci URL ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="69dec-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="69dec-130">İstemci Web kancası oluşturduğunuzda belirtilen parametre değerleri geçersiz kılamaz.</span><span class="sxs-lookup"><span data-stu-id="69dec-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="69dec-131">Runbook hello HTTP istek ayrıntıları ile doldurulur tek bir parametre tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69dec-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="69dec-132">Web kancası URL'si aracılığıyla özelliği hiçbir tootrack iş durumu.</span><span class="sxs-lookup"><span data-stu-id="69dec-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="69dec-133">Yanıt tooAzure uyarı</span><span class="sxs-lookup"><span data-stu-id="69dec-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="69dec-134">Bir runbook yanıt tooAzure uyarıda başlatın.</span><span class="sxs-lookup"><span data-stu-id="69dec-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="69dec-135">Web kancası runbook için yapılandırmak ve tooalert bağlayın.</span><span class="sxs-lookup"><span data-stu-id="69dec-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="69dec-136">Güvenlik belirteci URL ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="69dec-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="69dec-137">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="69dec-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="69dec-138">Saatlik, günlük, haftalık veya aylık zamanlamaya göre otomatik olarak runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="69dec-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="69dec-139">Azure portal, PowerShell cmdlet'leri veya Azure API aracılığıyla zamanlama yönetme.</span><span class="sxs-lookup"><span data-stu-id="69dec-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="69dec-140">Zamanlama ile kullanılan parametre değerleri toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="69dec-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="69dec-141">Başka bir Runbook'tan</span><span class="sxs-lookup"><span data-stu-id="69dec-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="69dec-142">Bir runbook başka bir runbook'taki bir etkinlik olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="69dec-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="69dec-143">Birden çok runbook tarafından kullanılan işlevselliği için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="69dec-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="69dec-144">Parametre değerleri toochild runbook sağlayın ve çıktı üst runbook'ta kullanın.</span><span class="sxs-lookup"><span data-stu-id="69dec-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="69dec-145">Merhaba aşağıdaki görüntüde ayrıntılı adım adım işlemi bir runbook'un hello yaşam döngüsü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="69dec-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="69dec-146">Azure Automation'da bir runbook'u başlatan farklı yollar karma Runbook çalışanı tooexecute Azure Otomasyonu runbook'ları ve farklı bileşenler arasındaki etkileşimler için gerekli bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="69dec-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="69dec-147">Otomasyon runbook'ları, veri merkezinizde, yürütülen toolearn başvurmak çok[karma runbook çalışanları](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="69dec-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook mimarisi](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="69dec-149">Hello Azure portal ile bir runbook başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="69dec-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="69dec-150">Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="69dec-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="69dec-151">Merhaba Hub menüsünde seçin **Runbook'lar**.</span><span class="sxs-lookup"><span data-stu-id="69dec-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="69dec-152">Merhaba üzerinde **Runbook'lar** dikey penceresinde, bir runbook seçin ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="69dec-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="69dec-153">Merhaba runbook'un parametreleri varsa, istendiğinde tooprovide değerler her parametre için bir metin kutusu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="69dec-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="69dec-154">Bkz: [Runbook parametreleri](#Runbook-parameters) altında daha fazla ayrıntı için parametreleri.</span><span class="sxs-lookup"><span data-stu-id="69dec-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="69dec-155">Merhaba üzerinde **iş** dikey penceresinde hello hello runbook işinin durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69dec-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="69dec-156">Windows PowerShell ile bir runbook başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="69dec-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="69dec-157">Merhaba kullanabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart bir runbook'u Windows PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="69dec-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="69dec-158">Merhaba aşağıdaki örnek kod Test-Runbook adlı bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="69dec-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="69dec-159">İşi Başlat AzureRmAutomationRunbook döndürür hello runbook başlatıldıktan sonra tootrack durumunu kullanabileceğiniz nesne.</span><span class="sxs-lookup"><span data-stu-id="69dec-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="69dec-160">Bu iş nesnesi ile sonra kullanabileceğiniz [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello hello işinin durumunu ve [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget çıktısını.</span><span class="sxs-lookup"><span data-stu-id="69dec-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="69dec-161">Aşağıdaki örnek kod hello Test-Runbook, tamamlandı ve ardından çıktısını görüntüler tamamlanmasını bekler adlı bir runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="69dec-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="69dec-162">Merhaba runbook parametreleri gerektirir sonra bunları olarak sağlamalısınız bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello hashtable hello anahtarı hello parametre ve hello değerle eşleştiği hello parametre değeridir.</span><span class="sxs-lookup"><span data-stu-id="69dec-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="69dec-163">Merhaba aşağıdaki örnek FirstName ve LastName, RepeatCount adlı bir tamsayı ve Show adlı bir boolean parametresiyle toostart iki dize parametresi ile bir runbook nasıl adlı gösterir.</span><span class="sxs-lookup"><span data-stu-id="69dec-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="69dec-164">Parametreleri hakkında ek bilgi için bkz: [Runbook parametreleri](#Runbook-parameters) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="69dec-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="69dec-165">Runbook parametreleri</span><span class="sxs-lookup"><span data-stu-id="69dec-165">Runbook parameters</span></span>
<span data-ttu-id="69dec-166">Hello Azure Portal ya da Windows PowerShell bir runbook'u başlattığınızda hello yönerge hello Azure Otomasyonu web hizmeti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="69dec-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="69dec-167">Bu hizmet, karmaşık veri türleriyle parametreleri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="69dec-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="69dec-168">Karmaşık bir parametre için bir değer tooprovide ihtiyacınız varsa, satır içi başka bir runbook'tan açıklandığı gibi çağırmanız gerekir [alt runbook'ları Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="69dec-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="69dec-169">Hello Azure Otomasyonu web hizmeti hello aşağıdaki bölümlerde açıklandığı gibi belirli veri türlerini kullanarak parametreler için özel işlevler sağlar.</span><span class="sxs-lookup"><span data-stu-id="69dec-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="69dec-170">Adlandırılmış değerler</span><span class="sxs-lookup"><span data-stu-id="69dec-170">Named values</span></span>
<span data-ttu-id="69dec-171">Merhaba parametredir [object] veri türünü sonra onu listesini adlı değerleri JSON biçimi toosend aşağıdaki hello kullanabilirsiniz: *{Ad1: 'Değer1', ad2: 'Değer2', AD3: 'Değer3'}*.</span><span class="sxs-lookup"><span data-stu-id="69dec-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="69dec-172">Bu değerler basit türler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="69dec-172">These values must be simple types.</span></span> <span data-ttu-id="69dec-173">Merhaba runbook hello parametre olarak alacağı bir [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) adlı değer tooeach karşılık gelen özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="69dec-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="69dec-174">Kullanıcı adında bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="69dec-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="69dec-175">Merhaba aşağıdaki metni hello kullanıcı parametresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="69dec-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="69dec-176">Çıktı aşağıdaki hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="69dec-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="69dec-177">Diziler</span><span class="sxs-lookup"><span data-stu-id="69dec-177">Arrays</span></span>
<span data-ttu-id="69dec-178">Merhaba parametresi [array] gibi bir dizi olup olmadığını veya [string []] kullanabileceğiniz sonra hello JSON biçimi toosend bu değerleri listesi: *[Value1, Value2, Value3]*.</span><span class="sxs-lookup"><span data-stu-id="69dec-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="69dec-179">Bu değerler basit türler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="69dec-179">These values must be simple types.</span></span>

<span data-ttu-id="69dec-180">Adlı bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun *kullanıcı*.</span><span class="sxs-lookup"><span data-stu-id="69dec-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="69dec-181">Merhaba aşağıdaki metni hello kullanıcı parametresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="69dec-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="69dec-182">Çıktı aşağıdaki hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="69dec-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="69dec-183">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="69dec-183">Credentials</span></span>
<span data-ttu-id="69dec-184">Merhaba parametre veri türü ise **PSCredential**, bir Azure Otomasyonu hello adını sağlayın ve sonra [kimlik bilgisi varlığı](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="69dec-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="69dec-185">Merhaba runbook belirttiğiniz hello ada sahip hello kimlik bilgisi alır.</span><span class="sxs-lookup"><span data-stu-id="69dec-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="69dec-186">Kimlik bilgisi adlı bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="69dec-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="69dec-187">Merhaba aşağıdaki metni adlı bir kimlik bilgisi varlığı olduğunu varsayarak hello kullanıcı parametresi için kullanılabilecek *My kimlik bilgisi*.</span><span class="sxs-lookup"><span data-stu-id="69dec-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="69dec-188">Merhaba kimlik bilgisi Hello kullanıcı olduğu varsayılarak *jsmith*, bu çıkış aşağıdaki hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="69dec-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="69dec-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69dec-189">Next steps</span></span>
* <span data-ttu-id="69dec-190">Merhaba runbook mimari geçerli makalede kaynakları yöneten runbook Azure ve şirket içi hello karma Runbook çalışanı ile üst düzey bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="69dec-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="69dec-191">Otomasyon runbook'ları, veri merkezinizde, yürütülen toolearn başvurmak çok[karma Runbook çalışanları](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="69dec-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="69dec-192">hakkında daha fazla özel veya ortak işlevleri için diğer runbook'lar tarafından kullanılan modüler runbook'lar toobe oluşturma hello toolearn başvurmak çok[alt runbook'ları](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="69dec-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>


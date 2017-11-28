---
title: "Azure Otomasyonu - PowerShell iş akışı aaaStarting ve durdurma sanal makinelerle | Microsoft Docs"
description: "Runbook'ları toostart ve durdurma Klasik sanal makineler de dahil olmak üzere Azure otomasyonu senaryosu grafik sürümü."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="e0e42-103">Başlatma ve durdurma sanal makineler, azure otomasyonu senaryosu-</span><span class="sxs-lookup"><span data-stu-id="e0e42-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="e0e42-104">Bu Azure otomasyonu senaryosu runbook'lar toostart ve durdurma Klasik sanal makineleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="e0e42-105">Bu senaryo hello aşağıdakilerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e0e42-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="e0e42-106">Değişiklik yapmadan Hello runbook'ları, kendi ortamınızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0e42-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="e0e42-107">Merhaba runbook'lar özelleştirilmiş tooperform işlevlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e0e42-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="e0e42-108">Merhaba runbook çözümü genelinin bir parçası olarak başka bir runbook'tan çağırın.</span><span class="sxs-lookup"><span data-stu-id="e0e42-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="e0e42-109">Merhaba runbook'lar öğreticileri toolearn runbook kavramları yazma kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0e42-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0e42-110">Grafik</span><span class="sxs-lookup"><span data-stu-id="e0e42-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="e0e42-111">PowerShell İş Akışı</span><span class="sxs-lookup"><span data-stu-id="e0e42-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="e0e42-112">Merhaba PowerShell iş akışı runbook sürümü bu senaryonun budur.</span><span class="sxs-lookup"><span data-stu-id="e0e42-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="e0e42-113">Ayrıca kullanılabilir kullanarak olan [grafik runbook'lar](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="e0e42-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="e0e42-114">Merhaba senaryo alma</span><span class="sxs-lookup"><span data-stu-id="e0e42-114">Getting hello scenario</span></span>
<span data-ttu-id="e0e42-115">Bu senaryo bağlantılar aşağıdaki hello indirebilirsiniz iki PowerShell iş akışı runbook oluşur.</span><span class="sxs-lookup"><span data-stu-id="e0e42-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="e0e42-116">Merhaba bkz [grafik sürümünü](automation-solution-startstopvm-graphical.md) Bağlantılar toohello grafik runbook'lar için bu senaryonun.</span><span class="sxs-lookup"><span data-stu-id="e0e42-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="e0e42-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="e0e42-117">Runbook</span></span> | <span data-ttu-id="e0e42-118">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="e0e42-118">Link</span></span> | <span data-ttu-id="e0e42-119">Tür</span><span class="sxs-lookup"><span data-stu-id="e0e42-119">Type</span></span> | <span data-ttu-id="e0e42-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0e42-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e0e42-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-121">Start-AzureVMs</span></span> |[<span data-ttu-id="e0e42-122">Azure Klasik sanal makineleri Başlat</span><span class="sxs-lookup"><span data-stu-id="e0e42-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="e0e42-123">PowerShell iş akışı</span><span class="sxs-lookup"><span data-stu-id="e0e42-123">PowerShell Workflow</span></span> |<span data-ttu-id="e0e42-124">Tüm Klasik sanal makineleri bir Azure subscriptionor içinde tüm sanal makinelerin belirli bir hizmet adı ile başlar.</span><span class="sxs-lookup"><span data-stu-id="e0e42-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="e0e42-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="e0e42-126">Azure Klasik Vm'leri Durdur</span><span class="sxs-lookup"><span data-stu-id="e0e42-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="e0e42-127">PowerShell iş akışı</span><span class="sxs-lookup"><span data-stu-id="e0e42-127">PowerShell Workflow</span></span> |<span data-ttu-id="e0e42-128">Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur.</span><span class="sxs-lookup"><span data-stu-id="e0e42-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="e0e42-129">Yükleme ve yapılandırma hello senaryosu</span><span class="sxs-lookup"><span data-stu-id="e0e42-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="e0e42-130">1. Merhaba runbook'ları yükleyin</span><span class="sxs-lookup"><span data-stu-id="e0e42-130">1. Install hello runbooks</span></span>
<span data-ttu-id="e0e42-131">Merhaba runbook'ları indirdikten sonra bunları aktarabilirsiniz hello yordamda kullanarak [bir Runbook'u içeri aktarma](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="e0e42-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="e0e42-132">2. Gözden geçirme hello açıklama ve gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="e0e42-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="e0e42-133">Merhaba runbook'ları bir açıklama ve gerekli varlıkları içerir açıklamalı Yardım metni içerir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="e0e42-134">Ayrıca alabilirsiniz hello Bu makale aynı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e0e42-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="e0e42-135">3. Varlıklar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e0e42-135">3. Configure assets</span></span>
<span data-ttu-id="e0e42-136">Merhaba runbook'lar oluşturmak ve uygun değerlerle doldurmak varlıklar aşağıdaki hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="e0e42-137">Varlık türü</span><span class="sxs-lookup"><span data-stu-id="e0e42-137">Asset Type</span></span> | <span data-ttu-id="e0e42-138">Varlık adı</span><span class="sxs-lookup"><span data-stu-id="e0e42-138">Asset Name</span></span> | <span data-ttu-id="e0e42-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0e42-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e0e42-140">Kimlik Bilgisi</span><span class="sxs-lookup"><span data-stu-id="e0e42-140">Credential</span></span> |<span data-ttu-id="e0e42-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="e0e42-141">AzureCredential</span></span> |<span data-ttu-id="e0e42-142">Yetkilisi toostart ve durdurma sanal makineler hello Azure aboneliğine sahip bir hesabın kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="e0e42-143">Alternatif olarak, başka bir kimlik bilgisi varlığı hello belirtebilirsiniz **kimlik bilgisi** hello parametresinin **Add-AzureAccount** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="e0e42-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="e0e42-144">Değişken</span><span class="sxs-lookup"><span data-stu-id="e0e42-144">Variable</span></span> |<span data-ttu-id="e0e42-145">Azuresubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="e0e42-145">AzureSubscriptionId</span></span> |<span data-ttu-id="e0e42-146">Merhaba abonelik kimliği, Azure aboneliğinizin yer alır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="e0e42-147">Merhaba senaryo kullanma</span><span class="sxs-lookup"><span data-stu-id="e0e42-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="e0e42-148">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e0e42-148">Parameters</span></span>
<span data-ttu-id="e0e42-149">Merhaba runbook'lar şu parametreler hello vardır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="e0e42-150">Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="e0e42-151">Parametre</span><span class="sxs-lookup"><span data-stu-id="e0e42-151">Parameter</span></span> | <span data-ttu-id="e0e42-152">Tür</span><span class="sxs-lookup"><span data-stu-id="e0e42-152">Type</span></span> | <span data-ttu-id="e0e42-153">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="e0e42-153">Mandatory</span></span> | <span data-ttu-id="e0e42-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0e42-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e0e42-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="e0e42-155">ServiceName</span></span> |<span data-ttu-id="e0e42-156">Dize</span><span class="sxs-lookup"><span data-stu-id="e0e42-156">string</span></span> |<span data-ttu-id="e0e42-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="e0e42-157">No</span></span> |<span data-ttu-id="e0e42-158">Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.</span><span class="sxs-lookup"><span data-stu-id="e0e42-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="e0e42-159">Herhangi bir değer sağlanmazsa, ardından hello Azure aboneliği tüm Klasik sanal makinelerin başlatıldığı veya durdurulduğu.</span><span class="sxs-lookup"><span data-stu-id="e0e42-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="e0e42-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="e0e42-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="e0e42-161">Dize</span><span class="sxs-lookup"><span data-stu-id="e0e42-161">string</span></span> |<span data-ttu-id="e0e42-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="e0e42-162">No</span></span> |<span data-ttu-id="e0e42-163">Merhaba Hello adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) hello abonelik kimliği, Azure aboneliğinizin içerir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="e0e42-164">Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="e0e42-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="e0e42-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="e0e42-166">Dize</span><span class="sxs-lookup"><span data-stu-id="e0e42-166">string</span></span> |<span data-ttu-id="e0e42-167">Hayır</span><span class="sxs-lookup"><span data-stu-id="e0e42-167">No</span></span> |<span data-ttu-id="e0e42-168">Merhaba Hello adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) hello runbook toouse hello kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="e0e42-169">Bir değer belirtmezseniz *AzureCredential* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="e0e42-170">Başlangıç hello runbook'ları</span><span class="sxs-lookup"><span data-stu-id="e0e42-170">Starting hello runbooks</span></span>
<span data-ttu-id="e0e42-171">Merhaba yöntemlerden herhangi birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) toostart ya da bu senaryoda hello runbook'lar.</span><span class="sxs-lookup"><span data-stu-id="e0e42-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="e0e42-172">Aşağıdaki örnek komutlar hello kullanan Windows PowerShell toorun **StartAzureVMs** toostart hello hizmet adı ile tüm sanal makineleri *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="e0e42-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="e0e42-173">Çıktı</span><span class="sxs-lookup"><span data-stu-id="e0e42-173">Output</span></span>
<span data-ttu-id="e0e42-174">Merhaba runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) her sanal makine belirten desteklemediğini hello Başlat veya Durdur yönerge başarıyla gönderildiği.</span><span class="sxs-lookup"><span data-stu-id="e0e42-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="e0e42-175">Merhaba çıktı toodetermine hello sonuç her runbook için belirli bir dizeyi arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0e42-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="e0e42-176">Merhaba olası çıktı dizeleri aşağıdaki tablonun hello listelenir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="e0e42-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="e0e42-177">Runbook</span></span> | <span data-ttu-id="e0e42-178">Koşul</span><span class="sxs-lookup"><span data-stu-id="e0e42-178">Condition</span></span> | <span data-ttu-id="e0e42-179">İleti</span><span class="sxs-lookup"><span data-stu-id="e0e42-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e0e42-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-180">Start-AzureVMs</span></span> |<span data-ttu-id="e0e42-181">Sanal makine zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="e0e42-181">Virtual machine is already running</span></span> |<span data-ttu-id="e0e42-182">MyVM zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="e0e42-182">MyVM is already running</span></span> |
| <span data-ttu-id="e0e42-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-183">Start-AzureVMs</span></span> |<span data-ttu-id="e0e42-184">Başlatma isteği başarıyla gönderildi bir sanal makine için</span><span class="sxs-lookup"><span data-stu-id="e0e42-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="e0e42-185">MyVM başlatıldı</span><span class="sxs-lookup"><span data-stu-id="e0e42-185">MyVM has been started</span></span> |
| <span data-ttu-id="e0e42-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-186">Start-AzureVMs</span></span> |<span data-ttu-id="e0e42-187">Sanal makine başlatma isteği başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="e0e42-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="e0e42-188">MyVM toostart başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="e0e42-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="e0e42-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-189">Stop-AzureVMs</span></span> |<span data-ttu-id="e0e42-190">Sanal makine zaten durdurulmuş</span><span class="sxs-lookup"><span data-stu-id="e0e42-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="e0e42-191">MyVM zaten durdurulmuş</span><span class="sxs-lookup"><span data-stu-id="e0e42-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="e0e42-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-192">Stop-AzureVMs</span></span> |<span data-ttu-id="e0e42-193">Durdurma isteği başarıyla gönderildi bir sanal makine için</span><span class="sxs-lookup"><span data-stu-id="e0e42-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="e0e42-194">MyVM durduruldu</span><span class="sxs-lookup"><span data-stu-id="e0e42-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="e0e42-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="e0e42-195">Stop-AzureVMs</span></span> |<span data-ttu-id="e0e42-196">Sanal makine durdurma isteği başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="e0e42-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="e0e42-197">MyVM toostop başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="e0e42-197">MyVM failed toostop</span></span> |

<span data-ttu-id="e0e42-198">Örneğin, bir runbook'tan kod parçacığını aşağıdaki hello toostart hello hizmet adı ile tüm sanal makineler çalışır *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="e0e42-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="e0e42-199">Merhaba hiçbirini istekleri başarısız başlatırsanız, hata eylemleri alınabilir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="e0e42-200">Ayrıntılı dökümü</span><span class="sxs-lookup"><span data-stu-id="e0e42-200">Detailed breakdown</span></span>
<span data-ttu-id="e0e42-201">Bu senaryoda hello runbook'lar ayrıntılı bir dökümünü aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="e0e42-202">Bu bilgileri kullanabilir tooeither özelleştirme hello runbook'ları veya bunlardan yalnızca toolearn kendi Otomasyon senaryoları yazma.</span><span class="sxs-lookup"><span data-stu-id="e0e42-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="e0e42-203">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e0e42-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="e0e42-204">Merhaba iş akışı için hello başlangıç değerleri alma başlatır [giriş parametreleri](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="e0e42-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="e0e42-205">Merhaba varlık adları sağlanmadığında varsayılan adları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="e0e42-206">Çıktı</span><span class="sxs-lookup"><span data-stu-id="e0e42-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="e0e42-207">Bu satır hello runbook hello çıkışını bir dize olacağını bildirir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="e0e42-208">Bu gerekli değildir ancak hello runbook olarak kullanıldığında için en iyi uygulamadır bir [alt runbook](automation-child-runbooks.md) üst runbook hello çıkış bilmesini tooexpect yazın.</span><span class="sxs-lookup"><span data-stu-id="e0e42-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="e0e42-209">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e0e42-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="e0e42-210">Merhaba sonraki satırları ayarlamak hello [kimlik bilgileri](automation-credentials.md) ve hello runbook hello kalanı için kullanılacak Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e0e42-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="e0e42-211">İlk kullanırız **Get-AutomationPSCredential** hello kimlik bilgileriyle erişim toostart ve durdurma sanal makineleri hello Azure aboneliği tutan tooget hello varlık.</span><span class="sxs-lookup"><span data-stu-id="e0e42-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="e0e42-212">**Add-AzureAccount** bu varlık tooset hello kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="e0e42-213">Böylece hello runbook çıktısında dahil edilmemiştir hello çıktı tooa kukla değişkeni atanır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="e0e42-214">Merhaba değişken varlığı kimliği ile alınan sonra hello aboneliğiyle **Get-AutomationVariable** ve kümesiyle hello abonelik **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="e0e42-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="e0e42-215">VM Al</span><span class="sxs-lookup"><span data-stu-id="e0e42-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="e0e42-216">**Get-AzureVM** kullanılan tooretrieve olan hello sanal makineleri hello runbook ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="e0e42-217">Bir değer hello sağladıysanız **ServiceName** giriş değişken sonra yalnızca hello sanal makinelerle hizmet adının alınır.</span><span class="sxs-lookup"><span data-stu-id="e0e42-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="e0e42-218">Varsa **ServiceName** tüm sanal makineleri aldıktan sonra boştur.</span><span class="sxs-lookup"><span data-stu-id="e0e42-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="e0e42-219">Sanal makineleri Başlat/Durdur ve çıktı gönderin</span><span class="sxs-lookup"><span data-stu-id="e0e42-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="e0e42-220">Merhaba sonraki satırları adım her bir sanal makine aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="e0e42-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="e0e42-221">İlk hello **PowerState** çalışıyor veya durdurulmuştur hello runbook'a bağlı zaten Merhaba sanal makine checked toosee ise.</span><span class="sxs-lookup"><span data-stu-id="e0e42-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="e0e42-222">Zaten bir hello hedef durumda ise, bir ileti toooutput ve hello runbook sona erer gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="e0e42-223">Aksi durumda, ardından **Start-AzureVM** veya **Stop-AzureVM** hello isteği saklı tooa değişkeni hello sonucu ile kullanılan tooattempt toostart veya stop hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="e0e42-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="e0e42-224">Merhaba isteği toostart veya stop başarıyla gönderildi olup olmadığını toooutput belirten bir ileti sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e0e42-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0e42-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0e42-225">Next steps</span></span>
* <span data-ttu-id="e0e42-226">alt runbook'ları ile çalışma hakkında daha fazla toolearn bakın [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="e0e42-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="e0e42-227">hakkında daha fazla bilgi toolearn çıkış runbook yürütme ve günlüğe kaydetme toohelp sırasında iletilerinde sorun gidermek için bkz: [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e0e42-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>


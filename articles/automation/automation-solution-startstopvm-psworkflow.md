---
title: "Başlatma ve durdurma Azure Otomasyonu - PowerShell iş akışı sanal makinelerle | Microsoft Docs"
description: "Klasik sanal makineleri durdurmak ve başlatmak için runbook'ları da dahil olmak üzere Azure otomasyonu senaryosu grafik sürümü."
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
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="51b56-103">Başlatma ve durdurma sanal makineler, azure otomasyonu senaryosu-</span><span class="sxs-lookup"><span data-stu-id="51b56-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="51b56-104">Bu Azure otomasyonu senaryosu Klasik sanal makineleri durdurmak ve başlatmak için runbook'ları içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="51b56-105">Bu senaryo herhangi birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51b56-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="51b56-106">Değişiklik yapmadan runbook'ları, kendi ortamınızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="51b56-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="51b56-107">Özelleştirilmiş işlevleri gerçekleştirmek için runbook'ları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="51b56-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="51b56-108">Runbook'ları çözümü genelinin bir parçası olarak başka bir runbook'tan çağırın.</span><span class="sxs-lookup"><span data-stu-id="51b56-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="51b56-109">Runbook'ları öğreticileri runbook kavramları yazma öğrenmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="51b56-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="51b56-110">Grafik</span><span class="sxs-lookup"><span data-stu-id="51b56-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="51b56-111">PowerShell İş Akışı</span><span class="sxs-lookup"><span data-stu-id="51b56-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="51b56-112">Bu PowerShell iş akışı runbook bu senaryo sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="51b56-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="51b56-113">Ayrıca kullanılabilir kullanarak olan [grafik runbook'lar](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="51b56-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="51b56-114">Senaryoyu alma</span><span class="sxs-lookup"><span data-stu-id="51b56-114">Getting the scenario</span></span>
<span data-ttu-id="51b56-115">Bu senaryo, aşağıdaki bağlantılardan birini yükleyebilirsiniz iki PowerShell iş akışı runbook oluşur.</span><span class="sxs-lookup"><span data-stu-id="51b56-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="51b56-116">Bkz: [grafik sürümünü](automation-solution-startstopvm-graphical.md) bağlantıları grafik runbook'lar için bu senaryonun.</span><span class="sxs-lookup"><span data-stu-id="51b56-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="51b56-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="51b56-117">Runbook</span></span> | <span data-ttu-id="51b56-118">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="51b56-118">Link</span></span> | <span data-ttu-id="51b56-119">Tür</span><span class="sxs-lookup"><span data-stu-id="51b56-119">Type</span></span> | <span data-ttu-id="51b56-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51b56-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51b56-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-121">Start-AzureVMs</span></span> |[<span data-ttu-id="51b56-122">Azure Klasik sanal makineleri Başlat</span><span class="sxs-lookup"><span data-stu-id="51b56-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="51b56-123">PowerShell iş akışı</span><span class="sxs-lookup"><span data-stu-id="51b56-123">PowerShell Workflow</span></span> |<span data-ttu-id="51b56-124">Tüm Klasik sanal makineleri bir Azure subscriptionor içinde tüm sanal makinelerin belirli bir hizmet adı ile başlar.</span><span class="sxs-lookup"><span data-stu-id="51b56-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="51b56-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="51b56-126">Azure Klasik Vm'leri Durdur</span><span class="sxs-lookup"><span data-stu-id="51b56-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="51b56-127">PowerShell iş akışı</span><span class="sxs-lookup"><span data-stu-id="51b56-127">PowerShell Workflow</span></span> |<span data-ttu-id="51b56-128">Tüm sanal makinelerin bir Otomasyon hesabı veya belirli bir hizmet adı ile tüm sanal makineleri durdurur.</span><span class="sxs-lookup"><span data-stu-id="51b56-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="51b56-129">Yükleme ve yapılandırma senaryosu</span><span class="sxs-lookup"><span data-stu-id="51b56-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="51b56-130">1. Runbook'ları yükleyin</span><span class="sxs-lookup"><span data-stu-id="51b56-130">1. Install the runbooks</span></span>
<span data-ttu-id="51b56-131">Runbook'ları indirdikten sonra bunları yordamı kullanarak aktarabilirsiniz [bir Runbook'u içeri aktarma](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="51b56-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="51b56-132">2. Açıklama ve gereksinimleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="51b56-132">2. Review the description and requirements</span></span>
<span data-ttu-id="51b56-133">Runbook'ları bir açıklama ve gerekli varlıkları içerir açıklamalı Yardım metni içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="51b56-134">Bu makalede aynı bilgiler de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51b56-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="51b56-135">3. Varlıklar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="51b56-135">3. Configure assets</span></span>
<span data-ttu-id="51b56-136">Runbook'ları oluşturma ve uygun değerlerle doldurmak şu varlıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="51b56-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="51b56-137">Varlık türü</span><span class="sxs-lookup"><span data-stu-id="51b56-137">Asset Type</span></span> | <span data-ttu-id="51b56-138">Varlık adı</span><span class="sxs-lookup"><span data-stu-id="51b56-138">Asset Name</span></span> | <span data-ttu-id="51b56-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51b56-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51b56-140">Kimlik Bilgisi</span><span class="sxs-lookup"><span data-stu-id="51b56-140">Credential</span></span> |<span data-ttu-id="51b56-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="51b56-141">AzureCredential</span></span> |<span data-ttu-id="51b56-142">Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için yetkili olan bir hesabın kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="51b56-143">Alternatif olarak, başka bir kimlik bilgisi varlığı belirtebilirsiniz **kimlik bilgisi** parametresinin **Add-AzureAccount** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="51b56-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="51b56-144">Değişken</span><span class="sxs-lookup"><span data-stu-id="51b56-144">Variable</span></span> |<span data-ttu-id="51b56-145">Azuresubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="51b56-145">AzureSubscriptionId</span></span> |<span data-ttu-id="51b56-146">Azure aboneliğiniz abonelik Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="51b56-147">Senaryo kullanma</span><span class="sxs-lookup"><span data-stu-id="51b56-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="51b56-148">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51b56-148">Parameters</span></span>
<span data-ttu-id="51b56-149">Her runbook aşağıdaki parametreleri var.</span><span class="sxs-lookup"><span data-stu-id="51b56-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="51b56-150">Zorunlu parametreler için değer sağlamalısınız ve değerleri gereksinimlerinize bağlı olarak diğer parametreleri için isteğe bağlı olarak sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="51b56-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="51b56-151">Parametre</span><span class="sxs-lookup"><span data-stu-id="51b56-151">Parameter</span></span> | <span data-ttu-id="51b56-152">Tür</span><span class="sxs-lookup"><span data-stu-id="51b56-152">Type</span></span> | <span data-ttu-id="51b56-153">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="51b56-153">Mandatory</span></span> | <span data-ttu-id="51b56-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51b56-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51b56-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="51b56-155">ServiceName</span></span> |<span data-ttu-id="51b56-156">Dize</span><span class="sxs-lookup"><span data-stu-id="51b56-156">string</span></span> |<span data-ttu-id="51b56-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="51b56-157">No</span></span> |<span data-ttu-id="51b56-158">Bir değer belirtilirse, hizmet adının tüm sanal makinelerle başlatıldığı veya durdurulduğu sonra.</span><span class="sxs-lookup"><span data-stu-id="51b56-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="51b56-159">Herhangi bir değer sağlanmazsa, ardından Azure Abonelikteki tüm Klasik sanal makineleri başlatıldığı veya durdurulduğu.</span><span class="sxs-lookup"><span data-stu-id="51b56-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="51b56-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="51b56-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="51b56-161">Dize</span><span class="sxs-lookup"><span data-stu-id="51b56-161">string</span></span> |<span data-ttu-id="51b56-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="51b56-162">No</span></span> |<span data-ttu-id="51b56-163">Adını içeren [değişken varlığı](#installing-and-configuring-the-scenario) , Azure aboneliğinizin abonelik Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="51b56-164">Bir değer belirtmezseniz *Azuresubscriptionıd* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51b56-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="51b56-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="51b56-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="51b56-166">Dize</span><span class="sxs-lookup"><span data-stu-id="51b56-166">string</span></span> |<span data-ttu-id="51b56-167">Hayır</span><span class="sxs-lookup"><span data-stu-id="51b56-167">No</span></span> |<span data-ttu-id="51b56-168">Adını içeren [kimlik bilgisi varlığı](#installing-and-configuring-the-scenario) runbook'un kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="51b56-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="51b56-169">Bir değer belirtmezseniz *AzureCredential* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51b56-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="51b56-170">Runbook'ları başlatma</span><span class="sxs-lookup"><span data-stu-id="51b56-170">Starting the runbooks</span></span>
<span data-ttu-id="51b56-171">Yöntemlerden birini kullanabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) runbook'ları ya da bu senaryoda başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="51b56-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="51b56-172">Aşağıdaki örnek komutlar çalıştırmak için Windows PowerShell kullanan **StartAzureVMs** tüm sanal makinelerin hizmet adı ile başlatmak için *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="51b56-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="51b56-173">Çıktı</span><span class="sxs-lookup"><span data-stu-id="51b56-173">Output</span></span>
<span data-ttu-id="51b56-174">Runbook'ları olacak [bir çıktı mesajı](automation-runbook-output-and-messages.md) Başlat veya Durdur yönerge başarıyla gönderildi olup olmadığını belirten her sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="51b56-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="51b56-175">Her runbook için sonucu belirlemek için çıktı belirli bir dizeyi arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51b56-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="51b56-176">Olası çıktı dizeler aşağıdaki tabloda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="51b56-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="51b56-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="51b56-177">Runbook</span></span> | <span data-ttu-id="51b56-178">Koşul</span><span class="sxs-lookup"><span data-stu-id="51b56-178">Condition</span></span> | <span data-ttu-id="51b56-179">İleti</span><span class="sxs-lookup"><span data-stu-id="51b56-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="51b56-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-180">Start-AzureVMs</span></span> |<span data-ttu-id="51b56-181">Sanal makine zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="51b56-181">Virtual machine is already running</span></span> |<span data-ttu-id="51b56-182">MyVM zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="51b56-182">MyVM is already running</span></span> |
| <span data-ttu-id="51b56-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-183">Start-AzureVMs</span></span> |<span data-ttu-id="51b56-184">Başlatma isteği başarıyla gönderildi bir sanal makine için</span><span class="sxs-lookup"><span data-stu-id="51b56-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="51b56-185">MyVM başlatıldı</span><span class="sxs-lookup"><span data-stu-id="51b56-185">MyVM has been started</span></span> |
| <span data-ttu-id="51b56-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-186">Start-AzureVMs</span></span> |<span data-ttu-id="51b56-187">Sanal makine başlatma isteği başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="51b56-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="51b56-188">MyVM başlatılamadı</span><span class="sxs-lookup"><span data-stu-id="51b56-188">MyVM failed to start</span></span> |
| <span data-ttu-id="51b56-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-189">Stop-AzureVMs</span></span> |<span data-ttu-id="51b56-190">Sanal makine zaten durdurulmuş</span><span class="sxs-lookup"><span data-stu-id="51b56-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="51b56-191">MyVM zaten durdurulmuş</span><span class="sxs-lookup"><span data-stu-id="51b56-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="51b56-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-192">Stop-AzureVMs</span></span> |<span data-ttu-id="51b56-193">Durdurma isteği başarıyla gönderildi bir sanal makine için</span><span class="sxs-lookup"><span data-stu-id="51b56-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="51b56-194">MyVM durduruldu</span><span class="sxs-lookup"><span data-stu-id="51b56-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="51b56-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51b56-195">Stop-AzureVMs</span></span> |<span data-ttu-id="51b56-196">Sanal makine durdurma isteği başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="51b56-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="51b56-197">MyVM durdurulamadı</span><span class="sxs-lookup"><span data-stu-id="51b56-197">MyVM failed to stop</span></span> |

<span data-ttu-id="51b56-198">Örneğin, tüm sanal makinelerin hizmet adı ile başlatmak aşağıdaki kod parçacığını bir runbook'tan çalışır *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="51b56-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="51b56-199">Varsa Başlangıç istekleri başarısız hata eylemleri alınabilir.</span><span class="sxs-lookup"><span data-stu-id="51b56-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="51b56-200">Ayrıntılı dökümü</span><span class="sxs-lookup"><span data-stu-id="51b56-200">Detailed breakdown</span></span>
<span data-ttu-id="51b56-201">Bu senaryoda runbook'ları ayrıntılı bir dökümünü aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="51b56-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="51b56-202">Runbook'ları özelleştirme veya sadece kendi Otomasyon senaryoları yazmak için bunlardan öğrenmek için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="51b56-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="51b56-203">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51b56-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="51b56-204">İş akışı için değerleri alarak başlatır [giriş parametreleri](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="51b56-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="51b56-205">Varlık adları sağlanmadığında varsayılan adları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51b56-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="51b56-206">Çıktı</span><span class="sxs-lookup"><span data-stu-id="51b56-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="51b56-207">Bu satır, runbook çıkışını bir dize olacağını bildirir.</span><span class="sxs-lookup"><span data-stu-id="51b56-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="51b56-208">Bu gerekli değildir, ancak runbook olarak kullanıldığında için en iyi uygulamadır bir [alt runbook](automation-child-runbooks.md) üst runbook beklenecek çıktı türü bilmesini.</span><span class="sxs-lookup"><span data-stu-id="51b56-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="51b56-209">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="51b56-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="51b56-210">Sonraki satırları kümesi [kimlik bilgileri](automation-credentials.md) ve runbook geri kalanı için kullanılacak Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="51b56-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="51b56-211">İlk kullanırız **Get-AutomationPSCredential** Azure Abonelikteki sanal makineleri durdurmak ve başlatmak için erişim kimlik bilgilerini tutan varlık almak için.</span><span class="sxs-lookup"><span data-stu-id="51b56-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="51b56-212">**Add-AzureAccount** kimlik bilgilerini ayarlamak için bu varlık kullanır.</span><span class="sxs-lookup"><span data-stu-id="51b56-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="51b56-213">Runbook çıktısında dahil edilmemiştir böylece çıkış kukla bir değişkene atanır.</span><span class="sxs-lookup"><span data-stu-id="51b56-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="51b56-214">Değişken varlığı kimliği ile alınan sonra abonelik ile **Get-AutomationVariable** ve kümesiyle abonelik **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="51b56-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="51b56-215">VM Al</span><span class="sxs-lookup"><span data-stu-id="51b56-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="51b56-216">**Get-AzureVM** runbook ile çalışır sanal makineleri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51b56-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="51b56-217">İçinde bir değer sağlanmazsa **ServiceName** giriş değişken, yalnızca sanal makineler, hizmet adı ile alınan sonra.</span><span class="sxs-lookup"><span data-stu-id="51b56-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="51b56-218">Varsa **ServiceName** tüm sanal makineleri aldıktan sonra boştur.</span><span class="sxs-lookup"><span data-stu-id="51b56-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="51b56-219">Sanal makineleri Başlat/Durdur ve çıktı gönderin</span><span class="sxs-lookup"><span data-stu-id="51b56-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="51b56-220">Sonraki satırların her sanal makineye üzerinden adım.</span><span class="sxs-lookup"><span data-stu-id="51b56-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="51b56-221">İlk **PowerState** sanal makinesini, zaten çalışıyor veya durdurulmuştur runbook'a bağlı olup olmadığını görmek için denetlenir.</span><span class="sxs-lookup"><span data-stu-id="51b56-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="51b56-222">Bunu zaten hedef durumdaysa, bir ileti çıkış ve runbook sona erer gönderilir.</span><span class="sxs-lookup"><span data-stu-id="51b56-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="51b56-223">Aksi durumda, ardından **Start-AzureVM** veya **Stop-AzureVM** başlatmak veya durdurmak için bir değişken depolanan isteğinin sonucunu sanal makineyle girişimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51b56-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="51b56-224">Bir ileti başlatma veya durdurma isteği başarıyla gönderildi belirtme çıktı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="51b56-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51b56-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51b56-225">Next steps</span></span>
* <span data-ttu-id="51b56-226">Alt runbook'larla çalışma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="51b56-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="51b56-227">Runbook yürütme ve gidermenize yardımcı olması için günlüğe kaydetme sırasında çıkış iletileri hakkında daha fazla bilgi için bkz: [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="51b56-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>


---
title: "aaaMonitor ve akış analizi işleri PowerShell ile yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Azure PowerShell ve cmdlet'leri toomonitor ve akış analizi işleri yönetin."
keywords: "Azure powershell, azure powershell cmdlet'leri, powershell komutu, powershell komut dosyası"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="35136-104">İzleme ve akış analizi işleri Azure PowerShell cmdlet'leri ile yönetme</span><span class="sxs-lookup"><span data-stu-id="35136-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="35136-105">Bilgi nasıl toomonitor ve Azure PowerShell cmdlet'leri ve powershell komut dosyası ile temel akış analizi görevleri yürütün akış analizi kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="35136-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="35136-106">Akış analizi için Azure PowerShell cmdlet'lerini çalıştırmak için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="35136-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="35136-107">Aboneliğinizde Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35136-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="35136-108">Merhaba, örnek bir Azure PowerShell komut dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="35136-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="35136-109">Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="35136-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="35136-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="35136-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="35136-112">Program aracılığıyla oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35136-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="35136-113">Hello Azure Portal'ı toohello işin izleme sayfası gezinme tarafından izleme el ile etkinleştirebilir ve hello Etkinleştir düğmesini veya tıklatarak yapabilirsiniz konumunda bulunan hello adımları izleyerek program aracılığıyla [Azure akış analizi - İzleyici akış Analytics işleri programlı şekilde](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="35136-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="35136-114">Akış analizi için Azure PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="35136-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="35136-115">Azure PowerShell cmdlet'lerini aşağıdaki hello kullanılan toomonitor olması ve Azure akış analizi işleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="35136-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="35136-116">Azure PowerShell farklı sürümlerini olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="35136-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="35136-117">**Listelenen hello ilk Azure PowerShell 0.9.8 komuttur hello örneklerde hello ikinci için Azure PowerShell 1.0 komuttur.**</span><span class="sxs-lookup"><span data-stu-id="35136-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="35136-118">Hello Azure PowerShell 1.0 komutları, her zaman "AzureRM" Merhaba komutta olacaktır.</span><span class="sxs-lookup"><span data-stu-id="35136-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="35136-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="35136-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="35136-120">Hello Azure aboneliği veya belirtilen kaynak grubunda tanımlanan tüm Stream Analytics işlerini listeler veya bir kaynak grubu içindeki belirli bir iş iş bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="35136-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="35136-121">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-121">**Example 1**</span></span>

<span data-ttu-id="35136-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="35136-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="35136-124">Bu PowerShell komutunu hello Azure aboneliği tüm hello Stream Analytics işleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="35136-125">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-125">**Example 2**</span></span>

<span data-ttu-id="35136-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="35136-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="35136-128">Bu PowerShell komutunu hello kaynak grubunda varsayılan orta ABD StreamAnalytics tüm hello Stream Analytics işleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="35136-129">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="35136-129">**Example 3**</span></span>

<span data-ttu-id="35136-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="35136-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="35136-132">Bu PowerShell komutunu hello kaynak grubunda varsayılan orta ABD StreamAnalytics hello Stream Analytics işi StreamingJob hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="35136-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="35136-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="35136-134">Tüm belirtilen Stream Analytics işinde tanımlanan hello girdi listeler veya belirli bir giriş bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="35136-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="35136-135">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-135">**Example 1**</span></span>

<span data-ttu-id="35136-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="35136-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="35136-138">Bu PowerShell komutunu hello iş StreamingJob tanımlanan tüm hello girişleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="35136-139">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-139">**Example 2**</span></span>

<span data-ttu-id="35136-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="35136-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="35136-142">Bu PowerShell komutunu hello iş StreamingJob tanımlanan EntryStream adlı hello giriş hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="35136-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="35136-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="35136-144">Tüm belirtilen Stream Analytics işinde tanımlanan hello çıkışları listeler veya belirli bir çıkış hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="35136-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="35136-145">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-145">**Example 1**</span></span>

<span data-ttu-id="35136-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="35136-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="35136-148">Bu PowerShell komutunu hello iş StreamingJob tanımlanan hello çıkışları hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="35136-149">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-149">**Example 2**</span></span>

<span data-ttu-id="35136-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="35136-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="35136-152">Bu PowerShell komutunu hello iş StreamingJob tanımlanan çıkış adlı hello çıktı hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="35136-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="35136-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="35136-154">Belirtilen bir bölgede birimleri akış hello kota hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="35136-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="35136-155">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-155">**Example 1**</span></span>

<span data-ttu-id="35136-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="35136-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="35136-158">Bu PowerShell komutunu hello Orta ABD bölgesinde hello kota ve akış birimleri kullanımı hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="35136-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="35136-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="35136-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="35136-160">Stream Analytics işinde tanımlanan belirli bir dönüşüm hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="35136-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="35136-161">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-161">**Example 1**</span></span>

<span data-ttu-id="35136-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="35136-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="35136-164">Bu PowerShell komutunu hello iş StreamingJob StreamingJob adlı hello dönüştürme hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="35136-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="35136-165">AzureStreamAnalyticsInput yeni | AzureRMStreamAnalyticsInput yeni</span><span class="sxs-lookup"><span data-stu-id="35136-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="35136-166">Akış analizi işi içinde yeni bir giriş oluşturur veya mevcut bir belirtilen giriş güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="35136-167">Merhaba hello giriş adını hello .json dosyası veya hello komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="35136-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="35136-168">Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.</span><span class="sxs-lookup"><span data-stu-id="35136-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="35136-169">Zaten bir girdi belirtin ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan giriş hello olup olmadığını sorar.</span><span class="sxs-lookup"><span data-stu-id="35136-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="35136-170">Belirtirseniz hello – Force parametresini ve var olan giriş adı, hello giriş onaysız değiştirilecek belirtin.</span><span class="sxs-lookup"><span data-stu-id="35136-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="35136-171">Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [girişi oluşturun (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-input] hello bölümünü [Stream Analytics Yönetimi REST API'si Başvuru Kitaplığı][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="35136-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="35136-172">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-172">**Example 1**</span></span>

<span data-ttu-id="35136-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="35136-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="35136-175">Bu PowerShell komutunu Input.json hello dosyasından yeni bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35136-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="35136-176">Var olan bir giriş hello giriş tanım dosyasında belirtilen hello adıyla zaten tanımlı olup olmadığını, hello cmdlet ister olsun veya olmasın tooreplace onu.</span><span class="sxs-lookup"><span data-stu-id="35136-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="35136-177">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-177">**Example 2**</span></span>

<span data-ttu-id="35136-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="35136-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="35136-180">Bu PowerShell komutunu hello işe EntryStream adlı yeni bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35136-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="35136-181">Bu ada sahip mevcut bir giriş zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.</span><span class="sxs-lookup"><span data-stu-id="35136-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="35136-182">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="35136-182">**Example 3**</span></span>

<span data-ttu-id="35136-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="35136-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="35136-185">Bu PowerShell komutunu hello varolan giriş kaynağı hello dosyasından hello tanımıyla EntryStream adlı hello tanımının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="35136-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="35136-186">AzureStreamAnalyticsJob yeni | AzureRMStreamAnalyticsJob yeni</span><span class="sxs-lookup"><span data-stu-id="35136-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="35136-187">Microsoft Azure'da yeni bir akış analizi işi oluşturur veya mevcut bir belirtilen proje hello tanımını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="35136-188">Merhaba .json dosyası veya hello komut satırında hello işinin Hello adı belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="35136-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="35136-189">Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.</span><span class="sxs-lookup"><span data-stu-id="35136-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="35136-190">Zaten bir iş adı belirtin ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace mevcut iş hello olup olmadığını sorar.</span><span class="sxs-lookup"><span data-stu-id="35136-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="35136-191">Var olan bir iş adı belirtin ve hello – Force parametresini belirtirseniz, hello iş tanımı onaysız değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="35136-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="35136-192">Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [Stream Analytics işi oluşturmak] [ msdn-rest-api-create-stream-analytics-job] hello bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplık][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="35136-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="35136-193">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-193">**Example 1**</span></span>

<span data-ttu-id="35136-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="35136-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="35136-196">Bu PowerShell komutunu JobDefinition.json hello tanımında yeni bir proje oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35136-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="35136-197">Merhaba iş tanımı dosyasında belirtilen hello ada sahip mevcut bir iş zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.</span><span class="sxs-lookup"><span data-stu-id="35136-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="35136-198">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-198">**Example 2**</span></span>

<span data-ttu-id="35136-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="35136-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="35136-201">Bu PowerShell komutunu hello iş tanımı için StreamingJob yerini alır.</span><span class="sxs-lookup"><span data-stu-id="35136-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="35136-202">AzureStreamAnalyticsOutput yeni | AzureRMStreamAnalyticsOutput yeni</span><span class="sxs-lookup"><span data-stu-id="35136-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="35136-203">Akış analizi işi yeni çıktısı oluşturur veya mevcut bir çıktı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="35136-204">Merhaba Çıktı Hello adını hello .json dosyası veya hello komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="35136-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="35136-205">Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.</span><span class="sxs-lookup"><span data-stu-id="35136-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="35136-206">Zaten bir çıktı belirtirseniz ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan çıktı hello olup olmadığını sorar.</span><span class="sxs-lookup"><span data-stu-id="35136-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="35136-207">Belirtirseniz hello – Force parametresini ve mevcut bir çıktı adı, hello çıkış onaysız değiştirilecek belirtin.</span><span class="sxs-lookup"><span data-stu-id="35136-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="35136-208">Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma çıkış (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-output] hello bölümünü [Stream Analytics Yönetimi REST API'si Başvuru Kitaplığı][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="35136-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="35136-209">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-209">**Example 1**</span></span>

<span data-ttu-id="35136-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="35136-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="35136-212">Bu PowerShell komutunu hello iş StreamingJob "çıktı" adlı yeni bir çıkış oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35136-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="35136-213">Bu ada sahip mevcut bir çıktı zaten tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.</span><span class="sxs-lookup"><span data-stu-id="35136-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="35136-214">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-214">**Example 2**</span></span>

<span data-ttu-id="35136-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="35136-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="35136-217">Bu PowerShell komutunu StreamingJob hello işteki "çıktı" Merhaba tanımı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="35136-218">AzureStreamAnalyticsTransformation yeni | AzureRMStreamAnalyticsTransformation yeni</span><span class="sxs-lookup"><span data-stu-id="35136-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="35136-219">Akış analizi işi içinde yeni bir dönüştürme oluşturur veya hello varolan dönüştürme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="35136-220">Merhaba dönüştürme Hello adını hello .json dosyası veya hello komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="35136-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="35136-221">Her ikisi de belirtilirse hello adı hello komut satırında gerekir olması hello hello dosyasındaki hello ile aynı.</span><span class="sxs-lookup"><span data-stu-id="35136-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="35136-222">Zaten bir dönüşüm belirtirseniz ve belirtmeyin hello – Force parametresini hello cmdlet tooreplace varolan dönüştürme hello olup olmadığını sorar.</span><span class="sxs-lookup"><span data-stu-id="35136-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="35136-223">Merhaba – Force parametresini ve varolan bir dönüşüm adı belirtirseniz belirtirseniz hello dönüştürme onaysız değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="35136-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="35136-224">Toohello hello JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma dönüştürme (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-transformation] hello bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplığı][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="35136-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="35136-225">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-225">**Example 1**</span></span>

<span data-ttu-id="35136-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="35136-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="35136-228">Bu PowerShell komutunu hello iş StreamingJob StreamingJobTransform adlı yeni bir dönüştürme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35136-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="35136-229">Varolan bir dönüşüm zaten bu ada sahip tanımlı olup olmadığını, hello cmdlet ister desteklemediğini tooreplace onu.</span><span class="sxs-lookup"><span data-stu-id="35136-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="35136-230">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="35136-230">**Example 2**</span></span>

<span data-ttu-id="35136-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="35136-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="35136-233">Bu PowerShell komutunu hello tanımında StreamingJobTransform hello iş StreamingJob değiştirir.</span><span class="sxs-lookup"><span data-stu-id="35136-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="35136-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="35136-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="35136-235">Zaman uyumsuz olarak belirli bir giriş Microsoft Azure Stream Analytics işinde siler.</span><span class="sxs-lookup"><span data-stu-id="35136-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="35136-236">Belirtirseniz hello – Force parametresini, giriş hello onay silinir.</span><span class="sxs-lookup"><span data-stu-id="35136-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="35136-237">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-237">**Example 1**</span></span>

<span data-ttu-id="35136-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="35136-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="35136-240">Giriş EventStream StreamingJob hello işteki kaldırır hello bu PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="35136-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="35136-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="35136-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="35136-242">Zaman uyumsuz olarak bir belirli Microsoft Azure akış analizi işi siler.</span><span class="sxs-lookup"><span data-stu-id="35136-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="35136-243">Belirtirseniz hello – Force parametresini hello iş olacaktır onay silinir.</span><span class="sxs-lookup"><span data-stu-id="35136-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="35136-244">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-244">**Example 1**</span></span>

<span data-ttu-id="35136-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="35136-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="35136-247">Bu PowerShell komutunu hello iş StreamingJob kaldırır.</span><span class="sxs-lookup"><span data-stu-id="35136-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="35136-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="35136-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="35136-249">Zaman uyumsuz olarak belirli bir çıkış Microsoft Azure Stream Analytics işinde siler.</span><span class="sxs-lookup"><span data-stu-id="35136-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="35136-250">Belirtirseniz hello – Force parametresini hello çıkış olacaktır onay silinir.</span><span class="sxs-lookup"><span data-stu-id="35136-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="35136-251">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-251">**Example 1**</span></span>

<span data-ttu-id="35136-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="35136-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="35136-254">Bu PowerShell komutunu kaldırır hello hello iş StreamingJob çıkış çıktı.</span><span class="sxs-lookup"><span data-stu-id="35136-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="35136-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="35136-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="35136-256">Zaman uyumsuz olarak dağıtır ve Microsoft Azure Stream Analytics işini başlatır.</span><span class="sxs-lookup"><span data-stu-id="35136-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="35136-257">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-257">**Example 1**</span></span>

<span data-ttu-id="35136-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="35136-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="35136-260">Bu PowerShell komutunu başlatır hello özel çıkış başlangıç saatine sahip StreamingJob ayarlamak tooDecember 12, 2012, 12:12:12 iş UTC.</span><span class="sxs-lookup"><span data-stu-id="35136-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="35136-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="35136-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="35136-262">Zaman uyumsuz olarak Microsoft Azure üzerinde çalışan bir Stream Analytics işini durdurur ve kullanılmakta olan kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="35136-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="35136-263">Merhaba iş düzenlenen yeniden ve gibi hello iş tanımı ve meta veri aboneliğinizi hello Azure portalı ve yönetim API'si aracılığıyla içinde kullanılabilir kalır.</span><span class="sxs-lookup"><span data-stu-id="35136-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="35136-264">Hello durduruldu durumunda bir iş için ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="35136-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="35136-265">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-265">**Example 1**</span></span>

<span data-ttu-id="35136-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="35136-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="35136-268">Bu PowerShell komutunu hello işini StreamingJob durdurur.</span><span class="sxs-lookup"><span data-stu-id="35136-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="35136-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="35136-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="35136-270">Stream Analytics tooconnect tooa testleri hello yeteneğini giriş belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="35136-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="35136-271">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-271">**Example 1**</span></span>

<span data-ttu-id="35136-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="35136-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="35136-274">Bu PowerShell komutunu testleri hello bağlantı durumunu hello giriş StreamingJob EntryStream.</span><span class="sxs-lookup"><span data-stu-id="35136-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="35136-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="35136-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="35136-276">Stream Analytics tooconnect tooa testleri hello yeteneğini çıkış belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="35136-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="35136-277">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="35136-277">**Example 1**</span></span>

<span data-ttu-id="35136-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="35136-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="35136-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="35136-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="35136-280">Bu PowerShell komutunu testleri hello bağlantı durumunu hello StreamingJob çıktısında çıktı.</span><span class="sxs-lookup"><span data-stu-id="35136-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="35136-281">Destek alın</span><span class="sxs-lookup"><span data-stu-id="35136-281">Get support</span></span>
<span data-ttu-id="35136-282">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="35136-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="35136-283">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35136-283">Next steps</span></span>
* [<span data-ttu-id="35136-284">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="35136-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="35136-285">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="35136-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="35136-286">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="35136-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="35136-287">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="35136-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="35136-288">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="35136-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301


---
title: "İzleme ve akış analizi işleri PowerShell ile yönetme | Microsoft Docs"
description: "Akış analizi işleri yönetmek ve izlemek için Azure PowerShell ve cmdlet'lerini kullanmayı öğrenin."
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
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="4f81b-104">İzleme ve akış analizi işleri Azure PowerShell cmdlet'leri ile yönetme</span><span class="sxs-lookup"><span data-stu-id="4f81b-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="4f81b-105">İzleme ve Azure PowerShell cmdlet'leri ve powershell komut dosyası ile temel akış analizi görevleri yürütün akış analizi kaynaklarını yönetme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4f81b-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="4f81b-106">Akış analizi için Azure PowerShell cmdlet'lerini çalıştırmak için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4f81b-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="4f81b-107">Aboneliğinizde Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f81b-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="4f81b-108">Örnek bir Azure PowerShell komut dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="4f81b-109">Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="4f81b-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="4f81b-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="4f81b-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="4f81b-112">Program aracılığıyla oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4f81b-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="4f81b-113">Azure Portalı'nda izleme iş İzleyici sayfasına giderek ve etkinleştir düğmesine tıklayarak el ile etkinleştirebilirsiniz veya bu program aracılığıyla konumunda bulunan adımları izleyerek yapabilirsiniz [Azure akış analizi - Stream Analytics işleri izleme Programlı şekilde](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="4f81b-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="4f81b-114">Akış analizi için Azure PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="4f81b-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="4f81b-115">Azure Stream Analytics işlerini yönetmek ve izlemek için aşağıdaki Azure PowerShell cmdlet'leri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="4f81b-116">Azure PowerShell farklı sürümlerini olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4f81b-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="4f81b-117">**Azure PowerShell 0.9.8, ilk komut listelenen örneklerde olduğu için Azure PowerShell 1.0 ikinci komuttur.**</span><span class="sxs-lookup"><span data-stu-id="4f81b-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="4f81b-118">Azure PowerShell 1.0 komutları komutta her zaman "AzureRM" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="4f81b-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="4f81b-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="4f81b-120">Azure aboneliği veya belirtilen kaynak grubunda tanımlanan tüm Stream Analytics işlerini listeler veya bir kaynak grubu içindeki belirli bir iş iş bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="4f81b-121">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-121">**Example 1**</span></span>

<span data-ttu-id="4f81b-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="4f81b-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="4f81b-124">Bu PowerShell komutunu Azure aboneliğindeki tüm Stream Analytics işleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="4f81b-125">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-125">**Example 2**</span></span>

<span data-ttu-id="4f81b-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="4f81b-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="4f81b-128">Bu PowerShell komutunu kaynak grubunda varsayılan orta ABD StreamAnalytics tüm Stream Analytics işleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="4f81b-129">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="4f81b-129">**Example 3**</span></span>

<span data-ttu-id="4f81b-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="4f81b-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="4f81b-132">Bu PowerShell komutunu kaynak grubunda varsayılan orta ABD StreamAnalytics StreamingJob Stream Analytics işi hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="4f81b-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="4f81b-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="4f81b-134">Tüm belirtilen Stream Analytics işinde tanımlı girdi listeler veya belirli bir giriş bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="4f81b-135">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-135">**Example 1**</span></span>

<span data-ttu-id="4f81b-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="4f81b-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="4f81b-138">Bu PowerShell komutunu iş StreamingJob tanımlanan tüm girişleri hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="4f81b-139">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-139">**Example 2**</span></span>

<span data-ttu-id="4f81b-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="4f81b-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="4f81b-142">Bu PowerShell komutunu iş StreamingJob tanımlanan EntryStream adlı giriş hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="4f81b-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="4f81b-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="4f81b-144">Tüm belirtilen Stream Analytics işinde tanımlanan çıkışları listeler veya belirli bir çıkış hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="4f81b-145">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-145">**Example 1**</span></span>

<span data-ttu-id="4f81b-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="4f81b-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="4f81b-148">Bu PowerShell komutunu iş StreamingJob tanımlanan çıkışları hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="4f81b-149">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-149">**Example 2**</span></span>

<span data-ttu-id="4f81b-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-152">Bu PowerShell komutunu iş StreamingJob tanımlanan çıkış adlı çıktı hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="4f81b-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="4f81b-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="4f81b-154">Akış birimleri belirtilen bir bölgede, kota hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="4f81b-155">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-155">**Example 1**</span></span>

<span data-ttu-id="4f81b-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="4f81b-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="4f81b-158">Bu PowerShell komutunu Orta ABD bölgesinde kota ve akış birimleri kullanımı hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="4f81b-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="4f81b-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="4f81b-160">Stream Analytics işinde tanımlanan belirli bir dönüşüm hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="4f81b-161">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-161">**Example 1**</span></span>

<span data-ttu-id="4f81b-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="4f81b-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="4f81b-164">Bu PowerShell komutunu iş StreamingJob StreamingJob adlı dönüştürme hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4f81b-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="4f81b-165">AzureStreamAnalyticsInput yeni | AzureRMStreamAnalyticsInput yeni</span><span class="sxs-lookup"><span data-stu-id="4f81b-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="4f81b-166">Akış analizi işi içinde yeni bir giriş oluşturur veya mevcut bir belirtilen giriş güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="4f81b-167">Giriş adı .json dosyası veya komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="4f81b-168">Her ikisi de belirtilirse, komut satırında adı bir dosya ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="4f81b-169">Zaten bir girdi belirtin ve belirtmeyin Force parametresini cmdlet varolan giriş değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="4f81b-170">Belirtirseniz – Force parametresi ve var olan giriş adı, giriş onaysız değiştirilecek belirtin.</span><span class="sxs-lookup"><span data-stu-id="4f81b-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="4f81b-171">JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [girişi oluşturun (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-input] bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplık][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="4f81b-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="4f81b-172">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-172">**Example 1**</span></span>

<span data-ttu-id="4f81b-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="4f81b-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="4f81b-175">Bu PowerShell komutunu Input.json dosyasından yeni bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="4f81b-176">Giriş tanım dosyasında belirtilen ada sahip mevcut bir giriş zaten tanımlanmış ise, cmdlet değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="4f81b-177">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-177">**Example 2**</span></span>

<span data-ttu-id="4f81b-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="4f81b-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="4f81b-180">Bu PowerShell komutunu İşte EntryStream adlı yeni bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="4f81b-181">Bu ada sahip mevcut bir giriş zaten tanımlanmış ise, cmdlet değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="4f81b-182">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="4f81b-182">**Example 3**</span></span>

<span data-ttu-id="4f81b-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="4f81b-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="4f81b-185">Bu PowerShell komut dosyasından tanımıyla EntryStream adlı varolan giriş kaynağı tanımını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="4f81b-186">AzureStreamAnalyticsJob yeni | AzureRMStreamAnalyticsJob yeni</span><span class="sxs-lookup"><span data-stu-id="4f81b-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="4f81b-187">Microsoft Azure'da yeni bir akış analizi işi oluşturur veya mevcut bir belirtilen iş tanımı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="4f81b-188">İş adı .json dosyası veya komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="4f81b-189">Her ikisi de belirtilirse, komut satırında adı bir dosya ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="4f81b-190">Zaten bir iş adı belirtin ve belirtmeyin Force parametresini cmdlet mevcut iş değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="4f81b-191">Belirtirseniz, Force parametresi ve var olan bir iş adı belirtin iş tanımı onaysız değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="4f81b-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="4f81b-192">JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [Stream Analytics işi oluşturmak] [ msdn-rest-api-create-stream-analytics-job] bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplığı] [stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="4f81b-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="4f81b-193">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-193">**Example 1**</span></span>

<span data-ttu-id="4f81b-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="4f81b-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="4f81b-196">Bu PowerShell komutunu JobDefinition.json tanımında yeni bir proje oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="4f81b-197">İş tanımı dosyasında belirtilen ada sahip mevcut bir iş zaten tanımlanmış ise, cmdlet değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="4f81b-198">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-198">**Example 2**</span></span>

<span data-ttu-id="4f81b-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="4f81b-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="4f81b-201">Bu PowerShell komutunu iş tanımı için StreamingJob yerini alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="4f81b-202">AzureStreamAnalyticsOutput yeni | AzureRMStreamAnalyticsOutput yeni</span><span class="sxs-lookup"><span data-stu-id="4f81b-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="4f81b-203">Akış analizi işi yeni çıktısı oluşturur veya mevcut bir çıktı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="4f81b-204">Çıktı adı .json dosyası veya komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="4f81b-205">Her ikisi de belirtilirse, komut satırında adı bir dosya ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="4f81b-206">Zaten bir çıktı belirtin ve belirtmeyin Force parametresini cmdlet varolan çıkış değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="4f81b-207">Belirtirseniz – Force parametresi ve mevcut bir çıktı adı, çıktı onaysız değiştirilecek belirtin.</span><span class="sxs-lookup"><span data-stu-id="4f81b-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="4f81b-208">JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma çıkış (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-output] bölümünü [Stream Analytics Yönetimi REST API Başvurusu Kitaplık][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="4f81b-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="4f81b-209">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-209">**Example 1**</span></span>

<span data-ttu-id="4f81b-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="4f81b-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="4f81b-212">Bu PowerShell komutunu iş StreamingJob "çıktı" adlı yeni bir çıkış oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="4f81b-213">Bu ada sahip mevcut bir çıktı zaten tanımlanmış ise, cmdlet değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="4f81b-214">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-214">**Example 2**</span></span>

<span data-ttu-id="4f81b-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="4f81b-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="4f81b-217">Bu PowerShell komutunu "çıktı" tanımı iş StreamingJob yerini alır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="4f81b-218">AzureStreamAnalyticsTransformation yeni | AzureRMStreamAnalyticsTransformation yeni</span><span class="sxs-lookup"><span data-stu-id="4f81b-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="4f81b-219">Akış analizi işi içinde yeni bir dönüştürme oluşturur veya mevcut dönüştürme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="4f81b-220">Dönüştürme adını .json dosyası veya komut satırında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="4f81b-221">Her ikisi de belirtilirse, komut satırında adı bir dosya ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="4f81b-222">Zaten bir dönüşüm belirtin ve belirtmeyin Force parametresini cmdlet varolan dönüştürme değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="4f81b-223">Belirtirseniz, Force parametresi ve varolan bir dönüşüm adını belirtin dönüştürme onaysız değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="4f81b-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="4f81b-224">JSON dosya yapısı ve içeriği hakkında ayrıntılı bilgi için bkz [oluşturma dönüştürme (Azure akış analizi)] [ msdn-rest-api-create-stream-analytics-transformation] bölümünü [Stream Analytics Yönetimi REST API'si Başvuru Kitaplığı][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="4f81b-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="4f81b-225">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-225">**Example 1**</span></span>

<span data-ttu-id="4f81b-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="4f81b-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="4f81b-228">Bu PowerShell komutunu iş StreamingJob StreamingJobTransform adlı yeni bir dönüştürme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="4f81b-229">Varolan bir dönüşüm zaten bu ada sahip tanımlanmışsa, cmdlet değiştirmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="4f81b-230">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="4f81b-230">**Example 2**</span></span>

<span data-ttu-id="4f81b-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="4f81b-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="4f81b-233">Bu PowerShell komutunu StreamingJob iş StreamingJobTransform tanımında değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="4f81b-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="4f81b-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="4f81b-235">Zaman uyumsuz olarak belirli bir giriş Microsoft Azure Stream Analytics işinde siler.</span><span class="sxs-lookup"><span data-stu-id="4f81b-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="4f81b-236">Belirtirseniz – Force parametresini giriş onay silinir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="4f81b-237">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-237">**Example 1**</span></span>

<span data-ttu-id="4f81b-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="4f81b-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="4f81b-240">Bu PowerShell komutunu giriş EventStream iş StreamingJob kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="4f81b-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="4f81b-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="4f81b-242">Zaman uyumsuz olarak bir belirli Microsoft Azure akış analizi işi siler.</span><span class="sxs-lookup"><span data-stu-id="4f81b-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="4f81b-243">Belirtirseniz – Force parametresini iş onay silinir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="4f81b-244">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-244">**Example 1**</span></span>

<span data-ttu-id="4f81b-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="4f81b-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="4f81b-247">Bu PowerShell komutunu StreamingJob iş kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="4f81b-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="4f81b-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="4f81b-249">Zaman uyumsuz olarak belirli bir çıkış Microsoft Azure Stream Analytics işinde siler.</span><span class="sxs-lookup"><span data-stu-id="4f81b-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="4f81b-250">Belirtirseniz – Force parametresini çıkış onay silinir.</span><span class="sxs-lookup"><span data-stu-id="4f81b-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="4f81b-251">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-251">**Example 1**</span></span>

<span data-ttu-id="4f81b-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-254">Çıktıyı iş StreamingJob çıkış bu PowerShell komutunu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="4f81b-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="4f81b-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="4f81b-256">Zaman uyumsuz olarak dağıtır ve Microsoft Azure Stream Analytics işini başlatır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="4f81b-257">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-257">**Example 1**</span></span>

<span data-ttu-id="4f81b-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="4f81b-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="4f81b-260">Bu PowerShell komutunu StreamingJob özel çıkış başlangıç saati ile 12:12:12 12 Kasım 2012 için ayarlanmış işini başlatır UTC.</span><span class="sxs-lookup"><span data-stu-id="4f81b-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="4f81b-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="4f81b-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="4f81b-262">Zaman uyumsuz olarak Microsoft Azure üzerinde çalışan bir Stream Analytics işini durdurur ve kullanılmakta olan kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="4f81b-263">İş düzenlenmesi ve yeniden gibi meta verileri ve iş tanımı aboneliğinizi Azure portalı ve yönetim API'si aracılığıyla içinde kullanılabilir kalır.</span><span class="sxs-lookup"><span data-stu-id="4f81b-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="4f81b-264">Durdurulmuş durumdaki bir iş için ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="4f81b-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="4f81b-265">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-265">**Example 1**</span></span>

<span data-ttu-id="4f81b-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="4f81b-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="4f81b-268">Bu PowerShell komutunu StreamingJob işini durdurur.</span><span class="sxs-lookup"><span data-stu-id="4f81b-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="4f81b-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="4f81b-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="4f81b-270">Akış analizi için belirtilen giriş bağlantı olanağı sınar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="4f81b-271">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-271">**Example 1**</span></span>

<span data-ttu-id="4f81b-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="4f81b-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="4f81b-274">Bu PowerShell komutunu StreamingJob içinde giriş EntryStream bağlantı durumunu sınar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="4f81b-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="4f81b-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="4f81b-276">Stream Analytics belirli bir çıktıya bağlanma yeteneğini sınar.</span><span class="sxs-lookup"><span data-stu-id="4f81b-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="4f81b-277">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="4f81b-277">**Example 1**</span></span>

<span data-ttu-id="4f81b-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="4f81b-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="4f81b-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="4f81b-280">Bu PowerShell komut testleri StreamingJob çıkış bağlantı durumunu çıktı.</span><span class="sxs-lookup"><span data-stu-id="4f81b-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="4f81b-281">Destek alın</span><span class="sxs-lookup"><span data-stu-id="4f81b-281">Get support</span></span>
<span data-ttu-id="4f81b-282">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="4f81b-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4f81b-283">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f81b-283">Next steps</span></span>
* [<span data-ttu-id="4f81b-284">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="4f81b-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4f81b-285">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4f81b-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4f81b-286">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="4f81b-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4f81b-287">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="4f81b-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4f81b-288">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="4f81b-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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


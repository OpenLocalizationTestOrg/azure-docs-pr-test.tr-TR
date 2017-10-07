---
title: Azure PowerShell kullanarak Azure Data Lake Analytics aaaManage | Microsoft Docs
description: "Nasıl toomanage Data Lake Analytics hesaplarını, veri kaynaklarının işleri, öğrenin ve Katalog öğeleri. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="b56a8-103">Azure Data Lake Analytics'i Azure PowerShell'i kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="b56a8-104">Toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, işlerin nasıl ve Azure PowerShell'i kullanarak katalog öğeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b56a8-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b56a8-105">Prerequisites</span></span>

<span data-ttu-id="b56a8-106">Bir Data Lake Analytics hesabı oluştururken tooknow gerekir:</span><span class="sxs-lookup"><span data-stu-id="b56a8-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="b56a8-107">**Abonelik kimliği**: Azure abonelik kimliği, Data Lake Analytics hesabınızı bulunduğu hello.</span><span class="sxs-lookup"><span data-stu-id="b56a8-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="b56a8-108">**Kaynak grubu**: Data Lake Analytics hesabınızı içeren hello Azure kaynak grubu hello adı.</span><span class="sxs-lookup"><span data-stu-id="b56a8-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="b56a8-109">**Data Lake Analytics hesap adı**: Merhaba hesap adı küçük harf ve sayı yalnızca içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="b56a8-110">**Varsayılan Data Lake Store hesabı**: Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="b56a8-111">Bu hesapları hello olmalıdır aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="b56a8-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="b56a8-112">**Konum**: "Doğu ABD 2" veya diğer gibi Data Lake Analytics hesabınızı hello konumunu desteklenen konumlar.</span><span class="sxs-lookup"><span data-stu-id="b56a8-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="b56a8-113">Desteklenen konumlar üzerinde görülme bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="b56a8-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="b56a8-114">Bu öğreticide Hello PowerShell parçacıkları bu değişkenleri toostore bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="b56a8-115">Oturum açma</span><span class="sxs-lookup"><span data-stu-id="b56a8-115">Log in</span></span>

<span data-ttu-id="b56a8-116">Bir abonelik kimliği kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="b56a8-117">Abonelik adı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="b56a8-118">Merhaba `Login-AzureRmAccount` cmdlet her zaman için kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="b56a8-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="b56a8-119">Cmdlet aşağıdaki hello kullanarak sorulmasını önlemek:</span><span class="sxs-lookup"><span data-stu-id="b56a8-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="b56a8-120">Hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="b56a8-121">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b56a8-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="b56a8-122">Henüz yoksa bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b56a8-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="b56a8-123">Her Data Lake Analytics hesabı, günlükleri depolamak için kullandığı varsayılan bir Data Lake Store hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="b56a8-124">Hesabınız yeniden ya da bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b56a8-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="b56a8-125">Bir Kaynak Grubu ve Data Lake Store hesabı oluşturulduktan sonra Data Lake Analytics hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b56a8-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="b56a8-126">Bir hesap hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b56a8-126">Get information about an account</span></span>

<span data-ttu-id="b56a8-127">Bir hesap ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="b56a8-128">Belirli bir Data Lake Analytics hesabı Hello var olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="b56a8-129">Merhaba cmdlet'i döndürür ya da `True` veya `False`.</span><span class="sxs-lookup"><span data-stu-id="b56a8-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="b56a8-130">Belirli bir Data Lake Store hesabı Hello var olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="b56a8-131">Merhaba cmdlet'i döndürür ya da `True` veya `False`.</span><span class="sxs-lookup"><span data-stu-id="b56a8-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="b56a8-132">Hesapları listeleme</span><span class="sxs-lookup"><span data-stu-id="b56a8-132">Listing accounts</span></span>

<span data-ttu-id="b56a8-133">Merhaba geçerli abonelik içindeki listesi Data Lake Analytics hesapları.</span><span class="sxs-lookup"><span data-stu-id="b56a8-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="b56a8-134">Belirli bir kaynak grubunun içinde listesi Data Lake Analytics hesapları.</span><span class="sxs-lookup"><span data-stu-id="b56a8-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="b56a8-135">Güvenlik duvarı kurallarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-135">Managing firewall rules</span></span>

<span data-ttu-id="b56a8-136">Güvenlik duvarı kuralları listesi.</span><span class="sxs-lookup"><span data-stu-id="b56a8-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="b56a8-137">Bir güvenlik duvarı kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="b56a8-138">Bir güvenlik duvarı kuralı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="b56a8-139">Bir güvenlik duvarı kuralı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="b56a8-140">Azure IP adreslerini verin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="b56a8-141">Veri kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-141">Managing data sources</span></span>
<span data-ttu-id="b56a8-142">Azure Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:</span><span class="sxs-lookup"><span data-stu-id="b56a8-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="b56a8-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b56a8-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="b56a8-144">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="b56a8-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="b56a8-145">Analytics hesabı oluşturduğunuzda, bir Data Lake Store hesabı toobe hello varsayılan veri kaynağı tanımlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="b56a8-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="b56a8-146">Merhaba varsayılan Data Lake Store hesabı kullanılan toostore işi meta verileri ve iş denetim günlükleri.</span><span class="sxs-lookup"><span data-stu-id="b56a8-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="b56a8-147">Bir Data Lake Analytics hesabı oluşturduktan sonra ek Data Lake Store hesapları ve/veya depolama hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b56a8-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="b56a8-148">Merhaba varsayılan Data Lake Store hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b56a8-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="b56a8-149">Veri kaynakları listesi hello hello tarafından filtre uygulayarak hello varsayılan Data Lake Store hesabı bulabilirsiniz `IsDefault` özelliği:</span><span class="sxs-lookup"><span data-stu-id="b56a8-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="b56a8-150">Veri kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="b56a8-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="b56a8-151">Veri kaynaklarını listele</span><span class="sxs-lookup"><span data-stu-id="b56a8-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="b56a8-152">U-SQL işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="b56a8-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="b56a8-153">U-SQL komut dosyası olarak bir dize gönderme</span><span class="sxs-lookup"><span data-stu-id="b56a8-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="b56a8-154">U-SQL komut dosyası olarak bir dosya gönderin</span><span class="sxs-lookup"><span data-stu-id="b56a8-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="b56a8-155">Bir hesap listesi işleri</span><span class="sxs-lookup"><span data-stu-id="b56a8-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="b56a8-156">Merhaba hesaptaki tüm hello işlerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="b56a8-157">Merhaba çıktı işler ve son tamamladınız bu işleri çalışmakta hello içerir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="b56a8-158">İşlerini belirli sayıda listesi</span><span class="sxs-lookup"><span data-stu-id="b56a8-158">List a specific number of jobs</span></span>

<span data-ttu-id="b56a8-159">Varsayılan olarak hello işlerin listesini sıralanır gönderme sırasında zaman.</span><span class="sxs-lookup"><span data-stu-id="b56a8-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="b56a8-160">İşlerini ilk görünecek Hello en son gönderildi.</span><span class="sxs-lookup"><span data-stu-id="b56a8-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="b56a8-161">Varsayılan olarak, 180 gün için işleri hello ADLA hesap hatırlıyor ancak hello Ge AdlJob cmdlet varsayılan döndürür tarafından yalnızca ilk 500 hello.</span><span class="sxs-lookup"><span data-stu-id="b56a8-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="b56a8-162">Kullanın - üst parametre toolist işleri belirli bir sayısı.</span><span class="sxs-lookup"><span data-stu-id="b56a8-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="b56a8-163">Merhaba değerine göre işi özellik listesi işleri</span><span class="sxs-lookup"><span data-stu-id="b56a8-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="b56a8-164">Hello kullanarak `-State` parametresi.</span><span class="sxs-lookup"><span data-stu-id="b56a8-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="b56a8-165">Bu değerleri birleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b56a8-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="b56a8-166">Kullanım hello `-Result` parametresi toodetect sona erdi işler başarıyla tamamlandığında olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="b56a8-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="b56a8-167">Bu değer vardır:</span><span class="sxs-lookup"><span data-stu-id="b56a8-167">It has these values:</span></span>

* <span data-ttu-id="b56a8-168">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="b56a8-168">Cancelled</span></span>
* <span data-ttu-id="b56a8-169">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="b56a8-169">Failed</span></span>
* <span data-ttu-id="b56a8-170">None</span><span class="sxs-lookup"><span data-stu-id="b56a8-170">None</span></span>
* <span data-ttu-id="b56a8-171">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="b56a8-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="b56a8-172">Merhaba `-Submitter` parametre kullanan bir işin gönderildiği belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b56a8-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="b56a8-173">Merhaba `-SubmittedAfter` tooa zaman aralığı filtreleme yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b56a8-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="b56a8-174">İşlerini listeleme için genel senaryolar</span><span class="sxs-lookup"><span data-stu-id="b56a8-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="b56a8-175">İşlerin listesini filtreleme</span><span class="sxs-lookup"><span data-stu-id="b56a8-175">Filtering a list of jobs</span></span>

<span data-ttu-id="b56a8-176">Bir kez işlerin bir listesini geçerli PowerShell oturumunda sahip.</span><span class="sxs-lookup"><span data-stu-id="b56a8-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="b56a8-177">Normal PowerShell cmdlet'leri toofilter hello listesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b56a8-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="b56a8-178">Son 24 saat hello filtre işleri toohello işlerin bir listesini gönderildi</span><span class="sxs-lookup"><span data-stu-id="b56a8-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="b56a8-179">Son 24 saat hello sona işleri toohello işlerin bir listesini filtreleme</span><span class="sxs-lookup"><span data-stu-id="b56a8-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="b56a8-180">Çalışmaya başladığı işleri toohello işlerin bir listesini filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="b56a8-181">Bir işi derleme zamanında - başarısız olabilir ve bu nedenle hiçbir zaman başlatır.</span><span class="sxs-lookup"><span data-stu-id="b56a8-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="b56a8-182">Gerçekten çalışmaya başladığı ve ardından başarısız hello başarısız işleri bakalım.</span><span class="sxs-lookup"><span data-stu-id="b56a8-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="b56a8-183">İşlerin listesini analiz etme</span><span class="sxs-lookup"><span data-stu-id="b56a8-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="b56a8-184">Kullanım hello `Group-Object` cmdlet tooanalyze işlerin bir listesini.</span><span class="sxs-lookup"><span data-stu-id="b56a8-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="b56a8-185">Bir analiz gerçekleştirirken, filtreleme ve daha basit gruplandırma yararlı tooadd özellikleri toohello iş nesneleri toomake olabilir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="b56a8-186">Aşağıdaki kod parçacığında hello ile iş tanımı bir tooannotate özellikleri nasıl hesaplandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b56a8-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="b56a8-187">Ardışık Düzen ve tekrarları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b56a8-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="b56a8-188">Kullanım hello `Get-AdlJobPipeline` cmdlet toosee hello ardışık düzen bilgileri daha önce gönderilen işler.</span><span class="sxs-lookup"><span data-stu-id="b56a8-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="b56a8-189">Kullanım hello `Get-AdlJobRecurrence` cmdlet toosee hello yineleme bilgilerini daha önce gönderilen işler.</span><span class="sxs-lookup"><span data-stu-id="b56a8-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="b56a8-190">Bir iş hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b56a8-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="b56a8-191">İş durumunu Al</span><span class="sxs-lookup"><span data-stu-id="b56a8-191">Get job status</span></span>

<span data-ttu-id="b56a8-192">Belirli bir iş Hello durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="b56a8-193">Merhaba iş çıkışları inceleyin</span><span class="sxs-lookup"><span data-stu-id="b56a8-193">Examine hello job outputs</span></span>

<span data-ttu-id="b56a8-194">Merhaba işi sona erdikten sonra hello çıktı dosyası hello dosyaları bir klasör içinde listeleyerek olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="b56a8-195">Çalışan işleri Yönet</span><span class="sxs-lookup"><span data-stu-id="b56a8-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="b56a8-196">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="b56a8-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="b56a8-197">Bir iş toofinish bekle</span><span class="sxs-lookup"><span data-stu-id="b56a8-197">Wait for a job toofinish</span></span>

<span data-ttu-id="b56a8-198">Yinelenen yerine `Get-AdlAnalyticsJob` bir işi tamamlanana kadar hello kullanabilirsiniz `Wait-AdlJob` hello iş tooend için cmdlet toowait.</span><span class="sxs-lookup"><span data-stu-id="b56a8-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="b56a8-199">İşlem ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="b56a8-200">Var olan bilgi işlem ilkeleri listesi</span><span class="sxs-lookup"><span data-stu-id="b56a8-200">List existing compute policies</span></span>

<span data-ttu-id="b56a8-201">Merhaba `Get-AdlAnalyticsComputePolicy` cmdlet'i bir Data Lake Analytics hesabı için bilgi işlem ilkeleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="b56a8-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="b56a8-202">Bir işlem ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b56a8-202">Create a compute policy</span></span>

<span data-ttu-id="b56a8-203">Merhaba `New-AdlAnalyticsComputePolicy` cmdlet'i, bir Data Lake Analytics hesabı için yeni bir işlem ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b56a8-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="b56a8-204">Kümeleri en fazla Avustralya kullanılabilir toohello hello Bu örnekte, kullanıcı too50 ve hello en düşük iş önceliği too250 belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="b56a8-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="b56a8-205">Bir dosyanın hello varlığını denetle.</span><span class="sxs-lookup"><span data-stu-id="b56a8-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="b56a8-206">Karşıya yükleme ve indirme</span><span class="sxs-lookup"><span data-stu-id="b56a8-206">Uploading and downloading</span></span>

<span data-ttu-id="b56a8-207">Bir dosyayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="b56a8-208">Tüm klasörü yinelemeli olarak karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="b56a8-209">Dosya indirme.</span><span class="sxs-lookup"><span data-stu-id="b56a8-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="b56a8-210">Tüm klasörü yinelemeli olarak indirin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="b56a8-211">Merhaba, karşıya yükleme veya indirme işlemi kesildiği, yeniden hello birlikte çalışan hello cmdlet'i tooresume hello işlem deneyebilirsiniz ``-Resume`` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="b56a8-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="b56a8-212">Katalog öğelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="b56a8-212">Manage catalog items</span></span>

<span data-ttu-id="b56a8-213">U-SQL komut dosyaları tarafından paylaşılabilmesi hello U-SQL kullanılan toostructure veri ve kod kataloğudur.</span><span class="sxs-lookup"><span data-stu-id="b56a8-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="b56a8-214">başlangıç kataloğu hello Azure Data Lake verilerle olası en yüksek performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b56a8-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="b56a8-215">Daha fazla bilgi için bkz. [U-SQL kataloğunu kullanma](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="b56a8-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="b56a8-216">Merhaba U-SQL kataloğunda liste öğeleri</span><span class="sxs-lookup"><span data-stu-id="b56a8-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="b56a8-217">Bir ADLA hesaptaki tüm hello veritabanlarındaki tüm hello derlemeler listeleyin.</span><span class="sxs-lookup"><span data-stu-id="b56a8-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="b56a8-218">Bir katalog öğesi hakkında bilgi almak</span><span class="sxs-lookup"><span data-stu-id="b56a8-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="b56a8-219">Kimlik bilgileri bir katalogda oluşturun</span><span class="sxs-lookup"><span data-stu-id="b56a8-219">Create credentials in a catalog</span></span>

<span data-ttu-id="b56a8-220">U-SQL veritabanı içinde Azure üzerinde barındırılan bir veritabanı için bir kimlik bilgisi nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b56a8-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="b56a8-221">Şu anda, U-SQL kimlik hello yalnızca PowerShell aracılığıyla oluşturabilirsiniz katalog öğesi türüdür.</span><span class="sxs-lookup"><span data-stu-id="b56a8-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="b56a8-222">Bir ADLA hesap hakkında temel bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b56a8-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="b56a8-223">Bir hesap adı hello hesabıyla ilgili temel bilgileri koddan hello arar</span><span class="sxs-lookup"><span data-stu-id="b56a8-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="b56a8-224">Azure ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b56a8-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="b56a8-225">AzureRm hataların ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="b56a8-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="b56a8-226">Yönetici olarak çalıştırıyorsanız doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b56a8-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="b56a8-227">Bir Tenantıd Bul</span><span class="sxs-lookup"><span data-stu-id="b56a8-227">Find a TenantID</span></span>

<span data-ttu-id="b56a8-228">Abonelik adı:</span><span class="sxs-lookup"><span data-stu-id="b56a8-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="b56a8-229">Bir abonelik kimliği:</span><span class="sxs-lookup"><span data-stu-id="b56a8-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="b56a8-230">"Contoso.com" gibi bir etki alanı adresi</span><span class="sxs-lookup"><span data-stu-id="b56a8-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="b56a8-231">Tüm aboneliklerinizi listelemek ve kimlikler Kiracı</span><span class="sxs-lookup"><span data-stu-id="b56a8-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="b56a8-232">Bir şablon kullanarak Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b56a8-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="b56a8-233">PowerShell Betiği aşağıdaki hello kullanarak bir Azure kaynak grubu şablonu de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b56a8-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="b56a8-234">Daha fazla bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](../azure-resource-manager/resource-group-template-deploy.md) ve [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b56a8-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b56a8-235">**Örnek şablon**</span><span class="sxs-lookup"><span data-stu-id="b56a8-235">**Example template**</span></span>

<span data-ttu-id="b56a8-236">Metin olarak aşağıdaki hello kaydetmek bir `.json` dosya ve PowerShell komut dosyası toouse hello şablon önceki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b56a8-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="b56a8-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b56a8-237">Next steps</span></span>
* [<span data-ttu-id="b56a8-238">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="b56a8-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="b56a8-239">Kullanarak Data Lake Analytics ile çalışmaya başlama [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="b56a8-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="b56a8-240">Kullanarak Azure Data Lake Analytics yönetmek [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b56a8-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 

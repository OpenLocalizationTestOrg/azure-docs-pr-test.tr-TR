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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Azure Data Lake Analytics'i Azure PowerShell'i kullanarak yönetme
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, işlerin nasıl ve Azure PowerShell'i kullanarak katalog öğeleri öğrenin. 

## <a name="prerequisites"></a>Ön koşullar

Bir Data Lake Analytics hesabı oluştururken tooknow gerekir:

* **Abonelik kimliği**: Azure abonelik kimliği, Data Lake Analytics hesabınızı bulunduğu hello.
* **Kaynak grubu**: Data Lake Analytics hesabınızı içeren hello Azure kaynak grubu hello adı.
* **Data Lake Analytics hesap adı**: Merhaba hesap adı küçük harf ve sayı yalnızca içermelidir.
* **Varsayılan Data Lake Store hesabı**: Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabına sahiptir. Bu hesapları hello olmalıdır aynı konumu.
* **Konum**: "Doğu ABD 2" veya diğer gibi Data Lake Analytics hesabınızı hello konumunu desteklenen konumlar. Desteklenen konumlar üzerinde görülme bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

Bu öğreticide Hello PowerShell parçacıkları bu değişkenleri toostore bu bilgileri kullanın.

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Oturum açma

Bir abonelik kimliği kullanarak oturum açın.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Abonelik adı kullanarak oturum açın.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Merhaba `Login-AzureRmAccount` cmdlet her zaman için kimlik bilgilerini ister. Cmdlet aşağıdaki hello kullanarak sorulmasını önlemek:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Hesaplarını yönetme

### <a name="create-a-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma

Henüz yoksa bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, bir tane oluşturun. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Her Data Lake Analytics hesabı, günlükleri depolamak için kullandığı varsayılan bir Data Lake Store hesabı gerektirir. Hesabınız yeniden ya da bir hesap oluşturun. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Bir Kaynak Grubu ve Data Lake Store hesabı oluşturulduktan sonra Data Lake Analytics hesabı oluşturun.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Bir hesap hakkında bilgi edinin

Bir hesap ayrıntılarını alın.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Belirli bir Data Lake Analytics hesabı Hello var olup olmadığını denetleyin. Merhaba cmdlet'i döndürür ya da `True` veya `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Belirli bir Data Lake Store hesabı Hello var olup olmadığını denetleyin. Merhaba cmdlet'i döndürür ya da `True` veya `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Hesapları listeleme

Merhaba geçerli abonelik içindeki listesi Data Lake Analytics hesapları.

```powershell
Get-AdlAnalyticsAccount
```

Belirli bir kaynak grubunun içinde listesi Data Lake Analytics hesapları.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Güvenlik duvarı kurallarını yönetme

Güvenlik duvarı kuralları listesi.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Bir güvenlik duvarı kuralı ekleyin.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Bir güvenlik duvarı kuralı değiştirin.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Bir güvenlik duvarı kuralı kaldırın.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Azure IP adreslerini verin.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Veri kaynaklarını yönetme
Azure Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Depolama](../storage/common/storage-introduction.md)

Analytics hesabı oluşturduğunuzda, bir Data Lake Store hesabı toobe hello varsayılan veri kaynağı tanımlamalısınız. Merhaba varsayılan Data Lake Store hesabı kullanılan toostore işi meta verileri ve iş denetim günlükleri. Bir Data Lake Analytics hesabı oluşturduktan sonra ek Data Lake Store hesapları ve/veya depolama hesapları ekleyebilirsiniz. 

### <a name="find-hello-default-data-lake-store-account"></a>Merhaba varsayılan Data Lake Store hesabı bulunamadı

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Veri kaynakları listesi hello hello tarafından filtre uygulayarak hello varsayılan Data Lake Store hesabı bulabilirsiniz `IsDefault` özelliği:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Veri kaynağı ekleme

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Veri kaynaklarını listele

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>U-SQL işlerini gönderme

### <a name="submit-a-string-as-a-u-sql-script"></a>U-SQL komut dosyası olarak bir dize gönderme

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


### <a name="submit-a-file-as-a-u-sql-script"></a>U-SQL komut dosyası olarak bir dosya gönderin

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Bir hesap listesi işleri

### <a name="list-all-hello-jobs-in-hello-account"></a>Merhaba hesaptaki tüm hello işlerini listeleyin. 

Merhaba çıktı işler ve son tamamladınız bu işleri çalışmakta hello içerir.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>İşlerini belirli sayıda listesi

Varsayılan olarak hello işlerin listesini sıralanır gönderme sırasında zaman. İşlerini ilk görünecek Hello en son gönderildi. Varsayılan olarak, 180 gün için işleri hello ADLA hesap hatırlıyor ancak hello Ge AdlJob cmdlet varsayılan döndürür tarafından yalnızca ilk 500 hello. Kullanın - üst parametre toolist işleri belirli bir sayısı.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Merhaba değerine göre işi özellik listesi işleri

Hello kullanarak `-State` parametresi. Bu değerleri birleştirebilirsiniz:

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

Kullanım hello `-Result` parametresi toodetect sona erdi işler başarıyla tamamlandığında olup olmadığını. Bu değer vardır:

* İptal edildi
* Başarısız oldu
* None
* Başarılı oldu

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Merhaba `-Submitter` parametre kullanan bir işin gönderildiği belirlemenize yardımcı olur.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Merhaba `-SubmittedAfter` tooa zaman aralığı filtreleme yararlıdır.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>İşlerini listeleme için genel senaryolar


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

## <a name="filtering-a-list-of-jobs"></a>İşlerin listesini filtreleme

Bir kez işlerin bir listesini geçerli PowerShell oturumunda sahip. Normal PowerShell cmdlet'leri toofilter hello listesini kullanabilirsiniz.

Son 24 saat hello filtre işleri toohello işlerin bir listesini gönderildi

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Son 24 saat hello sona işleri toohello işlerin bir listesini filtreleme

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Çalışmaya başladığı işleri toohello işlerin bir listesini filtreleyin. Bir işi derleme zamanında - başarısız olabilir ve bu nedenle hiçbir zaman başlatır. Gerçekten çalışmaya başladığı ve ardından başarısız hello başarısız işleri bakalım.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>İşlerin listesini analiz etme

Kullanım hello `Group-Object` cmdlet tooanalyze işlerin bir listesini.

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
Bir analiz gerçekleştirirken, filtreleme ve daha basit gruplandırma yararlı tooadd özellikleri toohello iş nesneleri toomake olabilir. Aşağıdaki kod parçacığında hello ile iş tanımı bir tooannotate özellikleri nasıl hesaplandığını gösterir.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Ardışık Düzen ve tekrarları hakkında bilgi edinin

Kullanım hello `Get-AdlJobPipeline` cmdlet toosee hello ardışık düzen bilgileri daha önce gönderilen işler.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Kullanım hello `Get-AdlJobRecurrence` cmdlet toosee hello yineleme bilgilerini daha önce gönderilen işler.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Bir iş hakkında bilgi edinin

### <a name="get-job-status"></a>İş durumunu Al

Belirli bir iş Hello durumunu alın.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Merhaba iş çıkışları inceleyin

Merhaba işi sona erdikten sonra hello çıktı dosyası hello dosyaları bir klasör içinde listeleyerek olup olmadığını kontrol edin.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Çalışan işleri Yönet

### <a name="cancel-a-job"></a>Bir işi iptal etme

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Bir iş toofinish bekle

Yinelenen yerine `Get-AdlAnalyticsJob` bir işi tamamlanana kadar hello kullanabilirsiniz `Wait-AdlJob` hello iş tooend için cmdlet toowait.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>İşlem ilkelerini yönetme

### <a name="list-existing-compute-policies"></a>Var olan bilgi işlem ilkeleri listesi

Merhaba `Get-AdlAnalyticsComputePolicy` cmdlet'i bir Data Lake Analytics hesabı için bilgi işlem ilkeleri hakkında bilgi alır.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Bir işlem ilkesi oluşturma

Merhaba `New-AdlAnalyticsComputePolicy` cmdlet'i, bir Data Lake Analytics hesabı için yeni bir işlem ilkesi oluşturur. Kümeleri en fazla Avustralya kullanılabilir toohello hello Bu örnekte, kullanıcı too50 ve hello en düşük iş önceliği too250 belirtilmiş.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Bir dosyanın hello varlığını denetle.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Karşıya yükleme ve indirme

Bir dosyayı karşıya yükleyin.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Tüm klasörü yinelemeli olarak karşıya yükleyin.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Dosya indirme.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Tüm klasörü yinelemeli olarak indirin.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Merhaba, karşıya yükleme veya indirme işlemi kesildiği, yeniden hello birlikte çalışan hello cmdlet'i tooresume hello işlem deneyebilirsiniz ``-Resume`` bayrağı.

## <a name="manage-catalog-items"></a>Katalog öğelerini yönetme

U-SQL komut dosyaları tarafından paylaşılabilmesi hello U-SQL kullanılan toostructure veri ve kod kataloğudur. başlangıç kataloğu hello Azure Data Lake verilerle olası en yüksek performansı sağlar. Daha fazla bilgi için bkz. [U-SQL kataloğunu kullanma](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Merhaba U-SQL kataloğunda liste öğeleri

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Bir ADLA hesaptaki tüm hello veritabanlarındaki tüm hello derlemeler listeleyin.

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

### <a name="get-details-about-a-catalog-item"></a>Bir katalog öğesi hakkında bilgi almak

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Kimlik bilgileri bir katalogda oluşturun

U-SQL veritabanı içinde Azure üzerinde barındırılan bir veritabanı için bir kimlik bilgisi nesnesi oluşturun. Şu anda, U-SQL kimlik hello yalnızca PowerShell aracılığıyla oluşturabilirsiniz katalog öğesi türüdür.

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

### <a name="get-basic-information-about-an-adla-account"></a>Bir ADLA hesap hakkında temel bilgi edinin

Bir hesap adı hello hesabıyla ilgili temel bilgileri koddan hello arar

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

## <a name="working-with-azure"></a>Azure ile çalışma

### <a name="get-details-of-azurerm-errors"></a>AzureRm hataların ayrıntılarını alma

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Yönetici olarak çalıştırıyorsanız doğrulayın

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Bir Tenantıd Bul

Abonelik adı:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

Bir abonelik kimliği:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

"Contoso.com" gibi bir etki alanı adresi


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Tüm aboneliklerinizi listelemek ve kimlikler Kiracı

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Bir şablon kullanarak Data Lake Analytics hesabı oluşturma

PowerShell Betiği aşağıdaki hello kullanarak bir Azure kaynak grubu şablonu de kullanabilirsiniz:

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

Daha fazla bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](../azure-resource-manager/resource-group-template-deploy.md) ve [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

**Örnek şablon**

Metin olarak aşağıdaki hello kaydetmek bir `.json` dosya ve PowerShell komut dosyası toouse hello şablon önceki hello kullanın. 

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

## <a name="next-steps"></a>Sonraki adımlar
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* Kullanarak Data Lake Analytics ile çalışmaya başlama [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Kullanarak Azure Data Lake Analytics yönetmek [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 

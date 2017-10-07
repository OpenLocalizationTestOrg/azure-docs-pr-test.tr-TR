---
title: Azure .NET SDK kullanarak Azure Data Lake Analytics aaaManage | Microsoft Docs
description: "Nasıl toomanage Data Lake Analytics, veri kaynakları, kullanıcıların işlerini öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Azure .NET SDK kullanarak Azure Data Lake Analytics yönetme
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Azure .NET SDK'sı toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, kullanıcılar ve işleri kullanarak nasıl hello öğrenin. 

## <a name="prerequisites"></a>Ön koşullar

* **Visual Studio 2015, Visual Studio 2013 Güncelleştirme 4 veya Visual C++ Yüklü Visual Studio 2012**.
* **.NET sürüm 2.5 veya üzeri için Microsoft Azure SDK**.  Hello kullanarak yükleyin [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).
* **Gerekli NuGet paketleri**

### <a name="install-nuget-packages"></a>NuGet paketlerini yükleme

|Paket|Sürüm|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0-Preview|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0-Preview|

Bu paketleri hello NuGet komut satırı aracılığıyla komutları aşağıdaki hello ile yükleyebilirsiniz:

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>Genel değişkenler

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>Kimlik Doğrulaması

Data Lake Analytics tooAzure üzerinde günlüğe kaydetme için birçok seçeneğiniz vardır. Merhaba aşağıdaki kod parçacığında bir açılır pencere ile etkileşimli kullanıcı kimlik doğrulaması ile kimlik doğrulaması örneği gösterir.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

Merhaba için kaynak kodunu **GetCreds_User_Popup** ve kimlik doğrulama için diğer seçenekleri ele alınmaktadır için kod hello [Data Lake Analytics .NET kimlik doğrulama seçenekleri](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-hello-client-management-objects"></a>Merhaba istemci yönetimi nesneleri oluşturma

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>Hesapları yönetme

### <a name="create-an-azure-resource-group"></a>Azure Kaynak Grubu oluşturma

Zaten bir oluşturmadıysanız, Data Lake Analytics bileşenlerinizi bir Azure kaynak grubu toocreate olması gerekir. Kimlik doğrulama kimlik bilgilerinizi, abonelik kimliği ve bir konum gerekir. kodun gösterdiği nasıl aşağıdaki hello toocreate bir kaynak grubu:

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
Daha fazla bilgi için bkz: [Azure kaynak grupları ve Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).

### <a name="create-a-data-lake-store-account"></a>Data Lake Store hesabı oluşturma

Şimdiye kadar ADLA hesap ADLS hesabına gerektirir. Bir toouse zaten sahip değilseniz, koddan hello biriyle oluşturabilirsiniz:

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma

koddan hello ADLS hesabına oluşturur

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Liste Data Lake Store hesapları

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>Liste Data Lake Analytics hesapları

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>Bir hesap var olup olmadığını denetleme

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>Bir hesap hakkında bilgi edinin

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>Hesap silme

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a>Merhaba varsayılan Data Lake Store hesabı edinin

Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabı gerektirir. Bu kod toodetermine hello varsayılan depolama hesabını Analytics hesabı için kullanın.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>Veri kaynaklarını yönet

Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure depolama hesabı](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a>Bağlantı tooan Azure depolama hesabı

Bağlantılar tooAzure depolama hesapları oluşturabilirsiniz.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Azure depolama veri kaynakları listesi

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Liste Data Lake Store veri kaynakları

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>Karşıya yükleme ve klasörleri ve dosyaları indirme
Merhaba Data Lake Store dosya sistemi istemci Yönetim nesnesi tooupload kullanın ve tek tek dosyalar veya klasörler yöntemler aşağıdaki hello kullanarak Azure tooyour yerel bilgisayardan karşıdan yükleyin:

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

Bu yöntemlere ait Hello ilk parametre hello kaynak yolu ve hello hedef yolu parametrelerini arkasından hello Data Lake Store hesabı hello adıdır.

Aşağıdaki örnek hello nasıl toodownload klasöründe bir hello Data Lake Store gösterir.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Bir Data Lake Store hesabı oluşturma

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Azure depolama hesabı yolları doğrulayın
Merhaba aşağıdaki kod bir Data Lake Analytics hesabı (analyticsAccountName) bir Azure Storage hesabı (storageAccntName) olup olmadığını ve hello Azure depolama hesabında bir kapsayıcı (containerName) olup olmadığını denetler.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>Katalog ve işleri Yönet
Merhaba DataLakeAnalyticsCatalogManagementClient nesne her Azure Data Lake Analytics hesabı için sağlanan hello SQL veritabanını yönetme için yöntemleri sağlar. Merhaba DataLakeAnalyticsJobManagementClient yöntemleri toosubmit sağlar ve U-SQL betikleri hello veritabanıyla çalışan işleri yönetin.

### <a name="list-databases-and-schemas"></a>Liste veritabanları ve şemaları
Merhaba arasında listeleyebilir, birkaç hello en yaygın veritabanları ve bunların şema noktalardır. Merhaba aşağıdaki kodu veritabanları koleksiyonunu alır ve her veritabanı için hello şema numaralandırır.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>Liste tablo sütunları
Merhaba aşağıdaki kod tooaccess belirtilen bir tablodaki bir Data Lake Analytics Kataloğu yönetim istemci toolist hello sütun veritabanıyla nasıl hello gösterir.

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>Başarısız olan işler listesi
Merhaba aşağıdaki kod başarısız işlemler hakkında bilgi listeler.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>Liste komut zincirleri
Merhaba aşağıdaki kod işleri gönderilen toohello hesabının her ardışık düzeni hakkında bilgi listeler.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>Liste tekrarları
Merhaba aşağıdaki kodu işleri gönderilen toohello hesabının her yineleme hakkında bilgileri listeler.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>Grafik senaryoları

### <a name="look-up-user-in-hello-aad-directory"></a>Merhaba AAD dizininde kullanıcı arayın

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a>Merhaba AAD dizini Hello bir kullanıcının objectID alın

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>İşlem ilkelerini yönetme
bir Data Lake Analytics hesabı için ilkeler hello yönetme için yöntemleri işlem Hello DataLakeAnalyticsAccountManagementClient nesnesi sağlar.

### <a name="list-compute-policies"></a>Liste işlem ilkeleri
koddan hello Data Lake Analytics hesabı için işlem ilkelerinin bir listesini alır.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>Yeni bir işlem ilke oluşturun
bir Data Lake Analytics hesabı için yeni bir işlem İlkesi koddan hello oluşturur, ayarı hello maksimum Avustralya kullanılabilir toohello belirtilen kullanıcı too50 ve hello en düşük iş önceliği too250.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>Sonraki adımlar
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Azure Data Lake Analytics'i Azure portalını kullanarak yönetme](data-lake-analytics-manage-use-portal.md)
* [Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

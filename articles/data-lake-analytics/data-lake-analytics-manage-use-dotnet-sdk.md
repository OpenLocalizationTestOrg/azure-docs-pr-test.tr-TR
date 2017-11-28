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
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="438ae-103">Azure .NET SDK kullanarak Azure Data Lake Analytics yönetme</span><span class="sxs-lookup"><span data-stu-id="438ae-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="438ae-104">Azure .NET SDK'sı toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, kullanıcılar ve işleri kullanarak nasıl hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="438ae-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="438ae-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="438ae-105">Prerequisites</span></span>

* <span data-ttu-id="438ae-106">**Visual Studio 2015, Visual Studio 2013 Güncelleştirme 4 veya Visual C++ Yüklü Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="438ae-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="438ae-107">**.NET sürüm 2.5 veya üzeri için Microsoft Azure SDK**.</span><span class="sxs-lookup"><span data-stu-id="438ae-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="438ae-108">Hello kullanarak yükleyin [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="438ae-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="438ae-109">**Gerekli NuGet paketleri**</span><span class="sxs-lookup"><span data-stu-id="438ae-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="438ae-110">NuGet paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="438ae-110">Install NuGet packages</span></span>

|<span data-ttu-id="438ae-111">Paket</span><span class="sxs-lookup"><span data-stu-id="438ae-111">Package</span></span>|<span data-ttu-id="438ae-112">Sürüm</span><span class="sxs-lookup"><span data-stu-id="438ae-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="438ae-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="438ae-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="438ae-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="438ae-114">2.3.1</span></span>|
|[<span data-ttu-id="438ae-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="438ae-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="438ae-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="438ae-116">3.0.0</span></span>|
|[<span data-ttu-id="438ae-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="438ae-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="438ae-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="438ae-118">2.2.0</span></span>|
|[<span data-ttu-id="438ae-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="438ae-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="438ae-120">1.6.0-Preview</span><span class="sxs-lookup"><span data-stu-id="438ae-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="438ae-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="438ae-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="438ae-122">3.4.0-Preview</span><span class="sxs-lookup"><span data-stu-id="438ae-122">3.4.0-preview</span></span>|

<span data-ttu-id="438ae-123">Bu paketleri hello NuGet komut satırı aracılığıyla komutları aşağıdaki hello ile yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="438ae-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="438ae-124">Genel değişkenler</span><span class="sxs-lookup"><span data-stu-id="438ae-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="438ae-125">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="438ae-125">Authentication</span></span>

<span data-ttu-id="438ae-126">Data Lake Analytics tooAzure üzerinde günlüğe kaydetme için birçok seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="438ae-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="438ae-127">Merhaba aşağıdaki kod parçacığında bir açılır pencere ile etkileşimli kullanıcı kimlik doğrulaması ile kimlik doğrulaması örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="438ae-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="438ae-128">Merhaba için kaynak kodunu **GetCreds_User_Popup** ve kimlik doğrulama için diğer seçenekleri ele alınmaktadır için kod hello [Data Lake Analytics .NET kimlik doğrulama seçenekleri](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="438ae-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="438ae-129">Merhaba istemci yönetimi nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="438ae-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="438ae-130">Hesapları yönetme</span><span class="sxs-lookup"><span data-stu-id="438ae-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="438ae-131">Azure Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="438ae-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="438ae-132">Zaten bir oluşturmadıysanız, Data Lake Analytics bileşenlerinizi bir Azure kaynak grubu toocreate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="438ae-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="438ae-133">Kimlik doğrulama kimlik bilgilerinizi, abonelik kimliği ve bir konum gerekir.</span><span class="sxs-lookup"><span data-stu-id="438ae-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="438ae-134">kodun gösterdiği nasıl aşağıdaki hello toocreate bir kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="438ae-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="438ae-135">Daha fazla bilgi için bkz: [Azure kaynak grupları ve Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="438ae-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="438ae-136">Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="438ae-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="438ae-137">Şimdiye kadar ADLA hesap ADLS hesabına gerektirir.</span><span class="sxs-lookup"><span data-stu-id="438ae-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="438ae-138">Bir toouse zaten sahip değilseniz, koddan hello biriyle oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="438ae-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="438ae-139">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="438ae-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="438ae-140">koddan hello ADLS hesabına oluşturur</span><span class="sxs-lookup"><span data-stu-id="438ae-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="438ae-141">Liste Data Lake Store hesapları</span><span class="sxs-lookup"><span data-stu-id="438ae-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="438ae-142">Liste Data Lake Analytics hesapları</span><span class="sxs-lookup"><span data-stu-id="438ae-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="438ae-143">Bir hesap var olup olmadığını denetleme</span><span class="sxs-lookup"><span data-stu-id="438ae-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="438ae-144">Bir hesap hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="438ae-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="438ae-145">Hesap silme</span><span class="sxs-lookup"><span data-stu-id="438ae-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="438ae-146">Merhaba varsayılan Data Lake Store hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="438ae-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="438ae-147">Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="438ae-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="438ae-148">Bu kod toodetermine hello varsayılan depolama hesabını Analytics hesabı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="438ae-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="438ae-149">Veri kaynaklarını yönet</span><span class="sxs-lookup"><span data-stu-id="438ae-149">Manage data sources</span></span>

<span data-ttu-id="438ae-150">Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:</span><span class="sxs-lookup"><span data-stu-id="438ae-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="438ae-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="438ae-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="438ae-152">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="438ae-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="438ae-153">Bağlantı tooan Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="438ae-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="438ae-154">Bağlantılar tooAzure depolama hesapları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="438ae-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="438ae-155">Azure depolama veri kaynakları listesi</span><span class="sxs-lookup"><span data-stu-id="438ae-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="438ae-156">Liste Data Lake Store veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="438ae-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="438ae-157">Karşıya yükleme ve klasörleri ve dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="438ae-157">Upload and download folders and files</span></span>
<span data-ttu-id="438ae-158">Merhaba Data Lake Store dosya sistemi istemci Yönetim nesnesi tooupload kullanın ve tek tek dosyalar veya klasörler yöntemler aşağıdaki hello kullanarak Azure tooyour yerel bilgisayardan karşıdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="438ae-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="438ae-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="438ae-159">UploadFolder</span></span>
- <span data-ttu-id="438ae-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="438ae-160">UploadFile</span></span>
- <span data-ttu-id="438ae-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="438ae-161">DownloadFolder</span></span>
- <span data-ttu-id="438ae-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="438ae-162">DownloadFile</span></span>

<span data-ttu-id="438ae-163">Bu yöntemlere ait Hello ilk parametre hello kaynak yolu ve hello hedef yolu parametrelerini arkasından hello Data Lake Store hesabı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="438ae-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="438ae-164">Aşağıdaki örnek hello nasıl toodownload klasöründe bir hello Data Lake Store gösterir.</span><span class="sxs-lookup"><span data-stu-id="438ae-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="438ae-165">Bir Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="438ae-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="438ae-166">Azure depolama hesabı yolları doğrulayın</span><span class="sxs-lookup"><span data-stu-id="438ae-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="438ae-167">Merhaba aşağıdaki kod bir Data Lake Analytics hesabı (analyticsAccountName) bir Azure Storage hesabı (storageAccntName) olup olmadığını ve hello Azure depolama hesabında bir kapsayıcı (containerName) olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="438ae-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="438ae-168">Katalog ve işleri Yönet</span><span class="sxs-lookup"><span data-stu-id="438ae-168">Manage catalog and jobs</span></span>
<span data-ttu-id="438ae-169">Merhaba DataLakeAnalyticsCatalogManagementClient nesne her Azure Data Lake Analytics hesabı için sağlanan hello SQL veritabanını yönetme için yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="438ae-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="438ae-170">Merhaba DataLakeAnalyticsJobManagementClient yöntemleri toosubmit sağlar ve U-SQL betikleri hello veritabanıyla çalışan işleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="438ae-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="438ae-171">Liste veritabanları ve şemaları</span><span class="sxs-lookup"><span data-stu-id="438ae-171">List databases and schemas</span></span>
<span data-ttu-id="438ae-172">Merhaba arasında listeleyebilir, birkaç hello en yaygın veritabanları ve bunların şema noktalardır.</span><span class="sxs-lookup"><span data-stu-id="438ae-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="438ae-173">Merhaba aşağıdaki kodu veritabanları koleksiyonunu alır ve her veritabanı için hello şema numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="438ae-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="438ae-174">Liste tablo sütunları</span><span class="sxs-lookup"><span data-stu-id="438ae-174">List table columns</span></span>
<span data-ttu-id="438ae-175">Merhaba aşağıdaki kod tooaccess belirtilen bir tablodaki bir Data Lake Analytics Kataloğu yönetim istemci toolist hello sütun veritabanıyla nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="438ae-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="438ae-176">Başarısız olan işler listesi</span><span class="sxs-lookup"><span data-stu-id="438ae-176">List failed jobs</span></span>
<span data-ttu-id="438ae-177">Merhaba aşağıdaki kod başarısız işlemler hakkında bilgi listeler.</span><span class="sxs-lookup"><span data-stu-id="438ae-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="438ae-178">Liste komut zincirleri</span><span class="sxs-lookup"><span data-stu-id="438ae-178">List pipelines</span></span>
<span data-ttu-id="438ae-179">Merhaba aşağıdaki kod işleri gönderilen toohello hesabının her ardışık düzeni hakkında bilgi listeler.</span><span class="sxs-lookup"><span data-stu-id="438ae-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="438ae-180">Liste tekrarları</span><span class="sxs-lookup"><span data-stu-id="438ae-180">List recurrences</span></span>
<span data-ttu-id="438ae-181">Merhaba aşağıdaki kodu işleri gönderilen toohello hesabının her yineleme hakkında bilgileri listeler.</span><span class="sxs-lookup"><span data-stu-id="438ae-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="438ae-182">Grafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="438ae-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="438ae-183">Merhaba AAD dizininde kullanıcı arayın</span><span class="sxs-lookup"><span data-stu-id="438ae-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="438ae-184">Merhaba AAD dizini Hello bir kullanıcının objectID alın</span><span class="sxs-lookup"><span data-stu-id="438ae-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="438ae-185">İşlem ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="438ae-185">Manage compute policies</span></span>
<span data-ttu-id="438ae-186">bir Data Lake Analytics hesabı için ilkeler hello yönetme için yöntemleri işlem Hello DataLakeAnalyticsAccountManagementClient nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="438ae-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="438ae-187">Liste işlem ilkeleri</span><span class="sxs-lookup"><span data-stu-id="438ae-187">List compute policies</span></span>
<span data-ttu-id="438ae-188">koddan hello Data Lake Analytics hesabı için işlem ilkelerinin bir listesini alır.</span><span class="sxs-lookup"><span data-stu-id="438ae-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="438ae-189">Yeni bir işlem ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="438ae-189">Create a new compute policy</span></span>
<span data-ttu-id="438ae-190">bir Data Lake Analytics hesabı için yeni bir işlem İlkesi koddan hello oluşturur, ayarı hello maksimum Avustralya kullanılabilir toohello belirtilen kullanıcı too50 ve hello en düşük iş önceliği too250.</span><span class="sxs-lookup"><span data-stu-id="438ae-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="438ae-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="438ae-191">Next steps</span></span>
* [<span data-ttu-id="438ae-192">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="438ae-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="438ae-193">Azure Data Lake Analytics'i Azure portalını kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="438ae-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="438ae-194">Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="438ae-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

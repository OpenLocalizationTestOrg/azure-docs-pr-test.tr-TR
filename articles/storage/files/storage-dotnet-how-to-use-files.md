---
title: ".NET ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop .NET uygulamalarını ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="fc26e-103">.NET ile Azure Dosya depolama için geliştirme</span><span class="sxs-lookup"><span data-stu-id="fc26e-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="fc26e-104">Bu makalede gösterilmektedir nasıl toomanage Azure File storage ile .NET kodu.</span><span class="sxs-lookup"><span data-stu-id="fc26e-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="fc26e-105">Azure File storage hakkında daha fazla toolearn hello bakın [giriş tooAzure dosya depolama](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc26e-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="fc26e-106">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="fc26e-106">About this tutorial</span></span>
<span data-ttu-id="fc26e-107">Bu öğretici .NET toodevelop uygulamaları ya da Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="fc26e-108">Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl .NET ve Azure File storage ile tooperform temel eylemleri:</span><span class="sxs-lookup"><span data-stu-id="fc26e-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="fc26e-109">Merhaba bir dosyanın içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="fc26e-109">Get hello contents of a file</span></span>
* <span data-ttu-id="fc26e-110">Merhaba dosya paylaşımı için Hello kota (en fazla boyut) ayarlama.</span><span class="sxs-lookup"><span data-stu-id="fc26e-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="fc26e-111">Merhaba paylaşımında tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc26e-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="fc26e-112">Hello tooanother dosyası kopyalamak aynı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="fc26e-113">Bir dosya tooa blob hello kopyalama aynı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="fc26e-114">Sorun giderme için Azure Storage Ölçümleri’ni kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="fc26e-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="fc26e-115">SMB üzerinden Azure File storage erişilebileceği için dosya g/ç için hello standart System.IO sınıflarını kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var.</span><span class="sxs-lookup"><span data-stu-id="fc26e-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="fc26e-116">Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama .NET SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.</span><span class="sxs-lookup"><span data-stu-id="fc26e-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="fc26e-117">Merhaba konsol uygulaması oluşturun ve hello derleme alma</span><span class="sxs-lookup"><span data-stu-id="fc26e-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="fc26e-118">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc26e-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="fc26e-119">Aşağıdaki adımları hello nasıl toocreate bir konsol uygulaması Visual Studio 2017, ancak başlangıç adımları benzerdir diğer Visual Studio sürümlerinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="fc26e-120">**Dosya** > **Yeni** > **Proje**’yi seçin</span><span class="sxs-lookup"><span data-stu-id="fc26e-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="fc26e-121">**Yüklü** > **Şablonlar** > **Visual C#** > **Windows Klasik Masaüstü** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="fc26e-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="fc26e-122">**Konsol Uygulaması (.NET Framework)** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="fc26e-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="fc26e-123">Hello uygulamanız için bir ad girin **Name:** alanı</span><span class="sxs-lookup"><span data-stu-id="fc26e-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="fc26e-124">**Tamam**’ı seçin</span><span class="sxs-lookup"><span data-stu-id="fc26e-124">Select **OK**</span></span>

<span data-ttu-id="fc26e-125">Bu öğreticideki tüm kod örnekleri toohello eklenebilir `Main()` konsol uygulamanızın yöntemi `Program.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="fc26e-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="fc26e-126">Herhangi bir Azure bulut hizmeti veya web uygulaması dahil olmak üzere, .NET uygulaması ve Masaüstü ve mobil uygulamaları türünde hello Azure Storage istemci kitaplığı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="fc26e-127">Bu kılavuzda, sadeleştirmek için konsol uygulaması kullanmaktayız.</span><span class="sxs-lookup"><span data-stu-id="fc26e-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="fc26e-128">NuGet tooinstall gerekli hello paketlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="fc26e-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="fc26e-129">Bu öğretici, proje toocomplete tooreference gereken iki paket vardır:</span><span class="sxs-lookup"><span data-stu-id="fc26e-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="fc26e-130">[.NET için Microsoft Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/): Bu paket depolama hesabınızdaki toodata kaynaklara programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc26e-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="fc26e-131">[.NET için Microsoft Azure Configuration Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): Bu paket, uygulamanızın nerede çalıştığına bakmaksızın yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc26e-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="fc26e-132">Her iki paket NuGet tooobtain kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="fc26e-133">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="fc26e-133">Follow these steps:</span></span>

1. <span data-ttu-id="fc26e-134">**Çözüm Gezgini**'nde projenize sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="fc26e-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="fc26e-135">Çevrimiçi olarak "WindowsAzure.Storage" ifadesini arayın ve'ı tıklatın **yükleme** tooinstall hello depolama istemci kitaplığı ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="fc26e-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="fc26e-136">Çevrimiçi "WindowsAzure.ConfigurationManager" için arama ve tıklayın **yükleme** tooinstall hello Azure Yapılandırma Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="fc26e-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="fc26e-137">Depolama hesabı kimlik bilgileri toohello app.config dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="fc26e-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="fc26e-138">Sonraki adımda, kimlik bilgilerinizi projenizin app.config dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fc26e-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="fc26e-139">Aşağıdaki örnek, değiştirme benzer toohello göründüğü şekilde hello app.config dosyasını düzenlemeniz `myaccount` , depolama hesabı adı ile ve `mykey` değerini depolama hesabınızın anahtarıyla.</span><span class="sxs-lookup"><span data-stu-id="fc26e-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> Azure File storage Hello hello Azure storage öykünücüsü en son sürümünü desteklemiyor. <span data-ttu-id="fc26e-141">Bağlantı dizenizi Azure File storage ile Merhaba bulut toowork içinde Azure Storage hesabını hedeflemelidir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="fc26e-142">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fc26e-142">Add using directives</span></span>
<span data-ttu-id="fc26e-143">Açık hello `Program.cs` dosya Çözüm Gezgini'nden ve hello aşağıdakileri ekleyin yönergeleri toohello dosyasının üst kısmında hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fc26e-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="fc26e-144">Erişim hello dosya paylaşımı program aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="fc26e-144">Access hello file share programmatically</span></span>
<span data-ttu-id="fc26e-145">Ardından, kod toohello aşağıdaki hello eklemek `Main()` yöntemi (sonra hello kodu yukarıda gösterilen) tooretrieve hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="fc26e-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="fc26e-146">Bu kod, daha önce oluşturduğumuz başvuru toohello dosya alır ve içeriği toohello konsol penceresine çıkarır.</span><span class="sxs-lookup"><span data-stu-id="fc26e-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="fc26e-147">Merhaba konsol uygulaması toosee hello çıkışı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fc26e-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="fc26e-148">Bir dosya paylaşımı için Hello maksimum boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc26e-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="fc26e-149">Sürümünden başlayarak hello Azure Storage istemci kitaplığı 5.x, ayarlayabileceğiniz kümesi hello kota (veya en büyük boyutu) bir dosya paylaşımı için gigabayt cinsinden.</span><span class="sxs-lookup"><span data-stu-id="fc26e-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="fc26e-150">Ayrıca, ne kadar veri şu anda hello paylaşımında depolanan toosee kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="fc26e-151">Ayarı hello tarafından paylaşımı için kota bir, hello paylaşımında depolanan hello dosyaların toplam boyutu hello sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="fc26e-152">Hello hello paylaşımdaki dosyaların toplam boyutu aşarsa hello kota hello paylaşımında ayarlayın, sonra istemcileri oluşturulamıyor tooincrease hello mevcut dosyaların boyutunu olabilir veya bu dosyaları boş olmadığı sürece, yeni dosyalar oluşturma.</span><span class="sxs-lookup"><span data-stu-id="fc26e-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="fc26e-153">Aşağıdaki örnek Hello nasıl toocheck hello bir paylaşım için geçerli kullanım ve nasıl tooset hello hello paylaşımı için kota gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="fc26e-154">Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc26e-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="fc26e-155">Sürümünden başlayarak 5.x Merhaba Azure Storage istemci kitaplığı, paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="fc26e-156">Ayrıca, bir dosya paylaşımı toomanage paylaşılan erişim imzaları bir paylaşılan erişim ilkesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="fc26e-157">Tehlikeye girdiği durumlarda hello SAS iptal etme yolu sağladığı gibi bir paylaşılan erişim ilkesi oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="fc26e-158">Aşağıdaki örneğine hello bir paylaşılan erişim ilkesi oluşturulur ve Itanium tabanlı sistemler için ilke tooprovide hello kısıtlamaları SAS için hello bir dosyada paylaşıma kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc26e-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="fc26e-159">Paylaşılan erişim imzaları oluşturma ve kullanma hakkında daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) ve [Azure Blobları ile SAS oluşturma ve kullanma](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="fc26e-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="fc26e-160">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="fc26e-160">Copy files</span></span>
<span data-ttu-id="fc26e-161">Sürümünden başlayarak 5.x Merhaba Azure Storage istemci kitaplığı, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="fc26e-162">Merhaba sonraki bölümlerde, biz nasıl tooperform bu kopyalama göstermek işlemleri programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="fc26e-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="fc26e-163">AzCopy toocopy bir dosya tooanother veya toocopy blob tooa dosya ya da tam tersini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="fc26e-164">Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc26e-164">See [Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="fc26e-165">Bir blob tooa dosyası veya dosya tooa blob kopyalıyorsanız aynı hello içinde kopyalama yapıyor olsanız bir paylaşılan erişim imzası (SAS) tooauthenticate hello kaynak nesnesi kullanmalısınız depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="fc26e-166">**Bir dosya tooanother dosyasından kopyalama** hello aşağıdaki örnek tooanother dosyası hello kopyalar aynı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="fc26e-167">Bu kopyalama işlemi arasında kopyaladığından dosyalarında Merhaba aynı depolama hesabı, paylaşılan anahtar kimlik doğrulaması tooperform hello kopya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="fc26e-168">**Bir dosya tooa blob kopyalama** hello aşağıdaki örnekte bir dosya oluşturur ve hello içinde tooa blob kopyalar aynı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="fc26e-169">hangi hello hizmet hello kopyalama işlemi sırasında tooauthenticate erişim toohello kaynak dosyasını kullanır hello kaynak dosya için bir SAS Merhaba örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc26e-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="fc26e-170">Hello bir blob tooa dosyaya kopyalayabilirsiniz aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="fc26e-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="fc26e-171">Merhaba kaynak nesnesi bir blob ise, SAS tooauthenticate erişim toothat blob hello kopyalama işlemi sırasında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc26e-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="fc26e-172">Ölçümleri kullanarak Azure Dosya depolama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fc26e-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="fc26e-173">Artık Azure Depolama Analizi, Azure Dosya depolama için ölçümleri destekliyor.</span><span class="sxs-lookup"><span data-stu-id="fc26e-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="fc26e-174">Ölçüm verilerini kullanarak istekleri ve tanılama sorunlarını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="fc26e-175">Merhaba dan Azure File storage için ölçümleri etkinleştirebilirsiniz [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc26e-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="fc26e-176">Program aracılığıyla arama hello hello REST API aracılığıyla dosya hizmeti özelliklerini ayarla işlemi ya da hello depolama istemci Kitaplığı'nda analoglarından biri tarafından ölçümleri etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc26e-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="fc26e-177">Aşağıdaki kod örneğine hello nasıl toouse hello depolama istemci kitaplığı Azure File storage için .NET tooenable ölçümleri için gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc26e-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="fc26e-178">İlk olarak, hello aşağıdakileri ekleyin `using` yönergeleri tooyour `Program.cs` dosyası, ayrıca, eklediğiniz yukarıdaki toothose:</span><span class="sxs-lookup"><span data-stu-id="fc26e-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="fc26e-179">Kullanan Azure BLOB'ları, Azure Table ve Azure kuyrukları sırasında paylaşılan hello Not `ServiceProperties` hello türü `Microsoft.WindowsAzure.Storage.Shared.Protocol` ad alanı, Azure File storage kendi türünü kullandığını, hello `FileServiceProperties` hello türü `Microsoft.WindowsAzure.Storage.File.Protocol` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="fc26e-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="fc26e-180">Her iki ad alanı kodunuzdan, Bununla birlikte, kod toocompile aşağıdaki Merhaba başvurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fc26e-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="fc26e-181">Ayrıca, çok başvuruda bulunabilir[Azure File storage sorun giderme makalesi](storage-troubleshoot-windows-file-connection-problems.md) uçtan uca sorun giderme kılavuzu için.</span><span class="sxs-lookup"><span data-stu-id="fc26e-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc26e-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc26e-182">Next steps</span></span>
<span data-ttu-id="fc26e-183">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="fc26e-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="fc26e-184">Kavramsal makaleler ve videolar</span><span class="sxs-lookup"><span data-stu-id="fc26e-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="fc26e-185">Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="fc26e-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="fc26e-186">Nasıl toouse Linux Azure File storage</span><span class="sxs-lookup"><span data-stu-id="fc26e-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="fc26e-187">File Storage için araç desteği</span><span class="sxs-lookup"><span data-stu-id="fc26e-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="fc26e-188">Nasıl toouse Microsoft Azure Storage ile AzCopy</span><span class="sxs-lookup"><span data-stu-id="fc26e-188">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="fc26e-189">Azure Storage ile Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="fc26e-189">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="fc26e-190">Azure Dosya depolama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fc26e-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="fc26e-191">Başvuru</span><span class="sxs-lookup"><span data-stu-id="fc26e-191">Reference</span></span>
* [<span data-ttu-id="fc26e-192">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="fc26e-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="fc26e-193">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="fc26e-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="fc26e-194">Blog yazıları</span><span class="sxs-lookup"><span data-stu-id="fc26e-194">Blog posts</span></span>
* [<span data-ttu-id="fc26e-195">Azure Dosya Depolama genel kullanıma sunulmuştur</span><span class="sxs-lookup"><span data-stu-id="fc26e-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="fc26e-196">Azure Dosya depolama incelemesi</span><span class="sxs-lookup"><span data-stu-id="fc26e-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="fc26e-197">Microsoft Azure Dosya Hizmeti’ne Giriş</span><span class="sxs-lookup"><span data-stu-id="fc26e-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="fc26e-198">Kalıcı bağlantılar tooMicrosoft Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="fc26e-198">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)

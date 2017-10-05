---
title: ".NET ile Azure Dosya depolama için geliştirme | Microsoft Docs"
description: "Dosya verilerini depolamak için Azure Dosya depolama kullanan .NET uygulamaları ve hizmetlerini geliştirmeyi öğrenin."
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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="7ba7b-103">.NET ile Azure Dosya depolama için geliştirme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="7ba7b-104">Bu makalede Azure Dosya depolamanın .NET koduyla nasıl yönetileceği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="7ba7b-105">Azure Dosya depolama hakkında daha fazla bilgi için lütfen [Azure Dosya depolamaya giriş](storage-files-introduction.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="7ba7b-106">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="7ba7b-106">About this tutorial</span></span>
<span data-ttu-id="7ba7b-107">Bu öğretici, dosya verilerini depolamak için Azure Dosya depolama kullanan .NET uygulamaları ve hizmetleri geliştirmenin temellerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="7ba7b-108">Bu öğreticide basit bir konsol uygulaması oluşturacağız ve .NET ve Azure Dosya depolama ile nasıl temel eylemler gerçekleştirileceğini göstereceğiz:</span><span class="sxs-lookup"><span data-stu-id="7ba7b-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="7ba7b-109">Dosyanın içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-109">Get the contents of a file</span></span>
* <span data-ttu-id="7ba7b-110">Dosya paylaşımı için kota (en fazla boyut) ayarlama.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="7ba7b-111">Paylaşımda tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="7ba7b-112">Bir dosyayı aynı depolama hesabındaki başka bir dosyaya kopyalama.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="7ba7b-113">Bir dosyayı aynı depolama hesabındaki bir bloba kopyalama.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="7ba7b-114">Sorun giderme için Azure Storage Ölçümleri’ni kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="7ba7b-115">Azure Dosya depolamaya SMB üzerinden erişilebildiğinden, Dosya G/Ç için standart System.IO sınıflarını kullanarak Azure Dosya paylaşımına erişen basit uygulamalar yazmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="7ba7b-116">Bu makalede, [Azure Dosya depolama REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) kullanarak Azure Dosya depolamayla iletişim kuran Azure Depolama .NET SDK’sının kullanıldığı uygulamaların nasıl yazılacağı anlatılır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="7ba7b-117">Konsol uygulaması oluşturma ve derleme alma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="7ba7b-118">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="7ba7b-119">Aşağıdaki adımlar Visual Studio 2017’de konsol uygulaması oluşturmayı gösterir, ancak adımlar, diğer Visual Studio sürümlerindekilerle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="7ba7b-120">**Dosya** > **Yeni** > **Proje**’yi seçin</span><span class="sxs-lookup"><span data-stu-id="7ba7b-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="7ba7b-121">**Yüklü** > **Şablonlar** > **Visual C#** > **Windows Klasik Masaüstü** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="7ba7b-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="7ba7b-122">**Konsol Uygulaması (.NET Framework)** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="7ba7b-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="7ba7b-123">**Ad:** alanına uygulamanız için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="7ba7b-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="7ba7b-124">**Tamam**’ı seçin</span><span class="sxs-lookup"><span data-stu-id="7ba7b-124">Select **OK**</span></span>

<span data-ttu-id="7ba7b-125">Bu öğreticideki tüm kod örnekleri konsol uygulamanızın `Program.cs` dosyasındaki `Main()` yöntemine eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="7ba7b-126">Azure bulut hizmeti veya web uygulaması ile masaüstü ve mobil uygulamaları dahil olmak üzere herhangi bir .NET uygulaması türünde Azure Depolama İstemcisi Kitaplığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="7ba7b-127">Bu kılavuzda, sadeleştirmek için konsol uygulaması kullanmaktayız.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="7ba7b-128">Gereken paketleri yüklemek için NuGet kullanma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="7ba7b-129">Bu öğreticiyi tamamlamak için projenizde başvurmanız gereken iki paket vardır:</span><span class="sxs-lookup"><span data-stu-id="7ba7b-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="7ba7b-130">[.NET için Microsoft Azure Storage İstemcisi Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/): Bu paket depolama hesabınızdaki veri kaynaklarına programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="7ba7b-131">[.NET için Microsoft Azure Configuration Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): Bu paket, uygulamanızın nerede çalıştığına bakmaksızın yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="7ba7b-132">Her iki paketi de almak için NuGet kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="7ba7b-133">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="7ba7b-133">Follow these steps:</span></span>

1. <span data-ttu-id="7ba7b-134">**Çözüm Gezgini**'nde projenize sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="7ba7b-135">Çevrimiçi olarak "WindowsAzure.Storage" ifadesini arayın ve Depolama İstemci Kitaplığı’nı ve bağımlılıklarını yüklemek için **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="7ba7b-136">Çevrimiçi olarak "WindowsAzure.ConfigurationManager" ifadesini arayın ve Azure Yapılandırma Yöneticisi’ni yüklemek için **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="7ba7b-137">Depolama hesabı kimlik bilgilerinizi app.config dosyasına kaydetme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="7ba7b-138">Sonraki adımda, kimlik bilgilerinizi projenizin app.config dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="7ba7b-139">app.config dosyasını aşağıdaki örneğe benzeyecek şekilde düzenleyin. `myaccount` değerini depolama hesabınızın adıyla ve `mykey` değerini depolama hesabınızın anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> Azure depolama öykünücüsünün en son sürümü Azure Dosya depolamayı desteklemez. <span data-ttu-id="7ba7b-141">Bağlantı dizeniz, Azure Dosya depolama ile çalışmak için buluttaki bir Azure Depolama hesabını hedeflemelidir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="7ba7b-142">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-142">Add using directives</span></span>
<span data-ttu-id="7ba7b-143">Çözüm Gezgini’nde `Program.cs` dosyasını açın ve aşağıdaki using yönergelerini dosyanın üst tarafına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="7ba7b-144">Dosya paylaşımına programlamayla erişme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-144">Access the file share programmatically</span></span>
<span data-ttu-id="7ba7b-145">Şimdi, bağlantı dizesini almak için aşağıdaki kodu `Main()` yöntemine (yukarıda gösterilen koddan sonra) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="7ba7b-146">Bu kod, daha önce oluşturduğumuz dosyaya başvuru alır ve bu dosyanın içeriğini konsol penceresine çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="7ba7b-147">Çıkışı görmek konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="7ba7b-148">Dosya paylaşımı için boyut üst sınırını ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ba7b-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="7ba7b-149">Azure Storage İstemci Kitaplığı’nın 5.x sürümünden başlayarak, dosya paylaşımı için gigabayt cinsinden kota (veya boyut üst sınırı) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="7ba7b-150">Paylaşımda halihazırda ne kadar verinin depolandığını da kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="7ba7b-151">Paylaşım için kota ayarlayarak paylaşımda depolanan toplam dosya boyutunu kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="7ba7b-152">Paylaşımdaki toplam dosya boyutu belirlediğiniz kotayı aşarsa, istemciler mevcut dosyaların boyutunu artıramaz veya boş olmamaları halinde yeni dosyalar oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="7ba7b-153">Aşağıdaki örnekte, paylaşımdaki mevcut kullanımını nasıl kontrol edileceği veya paylaşım için nasıl kota ayarlanacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="7ba7b-154">Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="7ba7b-155">Azure Storage İstemci Kitaplığı’nın 5.x sürümünden başlayarak, bir dosya paylaşımı veya yalnızca dosya için paylaşılan erişim imzası (SAS) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="7ba7b-156">Ayrıca, paylaşılan erişim imzalarını yönetmek için dosya paylaşımında bir paylaşılan erişim ilkesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="7ba7b-157">Gizliliğinin tehlikeye girdiği durumlarda SAS’yi iptal etme aracı olarak kullanılabilmesi nedeniyle bir paylaşılan erişim ilkesi oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="7ba7b-158">Aşağıdaki örnekte, paylaşım için bir paylaşılan erişim ilkesi oluşturulur, daha sonra bu ilke paylaşımdaki bir dosyada bulunan SAS için sınırlamalar sağlamak amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="7ba7b-159">Paylaşılan erişim imzaları oluşturma ve kullanma hakkında daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md) ve [Azure Blobları ile SAS oluşturma ve kullanma](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="7ba7b-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="7ba7b-160">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="7ba7b-160">Copy files</span></span>
<span data-ttu-id="7ba7b-161">Azure Storage İstemci Kitaplığı’nın 5.x sürümünden başlayarak, bir dosyayı başka bir dosyaya, bir dosyayı başka bir bloba veya bir blobu bir dosyaya kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="7ba7b-162">Sonraki bölümlerde, bu kopyalama işlemlerini programlamayla nasıl gerçekleştirebileceğinizi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="7ba7b-163">Bir dosyayı diğer bir dosyaya veya bir blobu bir dosyaya ya da tam tersini yapmak için AzCopy’i de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="7ba7b-164">Bkz. [AzCopy Komut Satırı Yardımcı Programı ile veri aktarımı](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="7ba7b-164">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7ba7b-165">Bir blobu dosyaya veya bir dosyayı bloba kopyalamak için aynı depolama hesabında kopyalama yapıyor olsanız da kaynak nesnesinin kimliğini doğrulamak amacıyla bir paylaşılan erişim imzası (SAS) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="7ba7b-166">**Dosyayı başka bir dosyaya kopyalama** Aşağıdaki örnekte, bir dosya aynı paylaşımdaki başka bir dosyaya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="7ba7b-167">Bu kopyalama işlemi aynı depolama hesabındaki dosyaları kopyaladığı için, kopyalama işlemini gerçekleştirmek üzere Paylaşılan Anahtar kimlik doğrulaması kullanabilirsiniz. </span><span class="sxs-lookup"><span data-stu-id="7ba7b-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="7ba7b-168">**Dosyayı bir bloba kopyalama** Aşağıdaki örnekte, bir dosya oluşturulur ve aynı depolama hesabındaki bir bloba kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="7ba7b-169">Örnekte, kaynak dosya için hizmetin kopyalama sırasında kaynak dosyaya erişimin kimlik doğrulamasını yapmak üzere kullandığı bir SAS oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="7ba7b-170">Aynı şekilde, bir blobu bir dosyaya kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="7ba7b-171">Kaynak dosya bir blob ise, kopyalama sırasında bu bloba erişimin kimlik doğrulamasını yapması için bir SAS oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="7ba7b-172">Ölçümleri kullanarak Azure Dosya depolama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="7ba7b-173">Artık Azure Depolama Analizi, Azure Dosya depolama için ölçümleri destekliyor.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="7ba7b-174">Ölçüm verilerini kullanarak istekleri ve tanılama sorunlarını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="7ba7b-175">Azure Dosya depolama ölçümlerini [Azure Portal](https://portal.azure.com)’dan etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="7ba7b-176">Ayrıca, REST API veya Depolama İstemci Kitaplığı’ndaki analoglarından biri aracılığıyla Dosya Hizmeti Özelliklerini Ayarla işlemine çağrı yaparak ölçümleri programlamayla etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="7ba7b-177">Aşağıdaki kodda, Azure Dosya depolama için ölçümleri etkinleştirmek üzere .NET için Depolama İstemcisi Kitaplığı’nı nasıl kullanacağınız gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="7ba7b-178">İlk olarak, yukarıda eklediğiniz yönergelere ek olarak aşağıdaki `using` yönergelerini `Program.cs` dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ba7b-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="7ba7b-179">Azure Blobları, Azure Tablosu ve Azure Kuyruklarının `Microsoft.WindowsAzure.Storage.Shared.Protocol` ad alanındaki paylaşılan `ServiceProperties` türünü kullanmasına rağmen, Azure Dosya depolamanın `Microsoft.WindowsAzure.Storage.File.Protocol` ad alanında bulunan kendi `FileServiceProperties` türünü kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="7ba7b-180">Aşağıdaki kodların derlenebilmesi için her iki ad alanına da kodunuzdan başvurulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

<span data-ttu-id="7ba7b-181">Uçtan uca sorun giderme rehberi için [Azure Dosya depolama Sorun Giderme Makalesine](storage-troubleshoot-file-connection-problems.md) de başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba7b-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ba7b-182">Next steps</span></span>
<span data-ttu-id="7ba7b-183">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="7ba7b-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="7ba7b-184">Kavramsal makaleler ve videolar</span><span class="sxs-lookup"><span data-stu-id="7ba7b-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="7ba7b-185">Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="7ba7b-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="7ba7b-186">Azure Dosya depolamayı Linux ile kullanma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="7ba7b-187">File Storage için araç desteği</span><span class="sxs-lookup"><span data-stu-id="7ba7b-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="7ba7b-188">Azure Depolama ile Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="7ba7b-189">Microsoft Azure Depolama ile AzCopy kullanma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-189">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="7ba7b-190">Azure Depolama ile Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="7ba7b-190">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="7ba7b-191">Azure Dosya depolama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="7ba7b-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="7ba7b-192">Başvuru</span><span class="sxs-lookup"><span data-stu-id="7ba7b-192">Reference</span></span>
* [<span data-ttu-id="7ba7b-193">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="7ba7b-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="7ba7b-194">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="7ba7b-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="7ba7b-195">Blog yazıları</span><span class="sxs-lookup"><span data-stu-id="7ba7b-195">Blog posts</span></span>
* [<span data-ttu-id="7ba7b-196">Azure Dosya Depolama genel kullanıma sunulmuştur</span><span class="sxs-lookup"><span data-stu-id="7ba7b-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="7ba7b-197">Azure Dosya depolama incelemesi</span><span class="sxs-lookup"><span data-stu-id="7ba7b-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="7ba7b-198">Microsoft Azure Dosya Hizmeti’ne Giriş</span><span class="sxs-lookup"><span data-stu-id="7ba7b-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="7ba7b-199">Microsoft Azure Dosya depolamaya kalıcı bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7ba7b-199">Persisting connections to Microsoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
---
title: "BLOB storage (nesne depolama) C++ içinden kullanma | Microsoft Docs"
description: "Azure Blob Storage (nesne depolama) ile bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="6bd5d-103">C++ içinden BLOB Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6bd5d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6bd5d-104">Overview</span></span>
<span data-ttu-id="6bd5d-105">Azure Blob Storage, bulutta nesne/blob olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="6bd5d-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="6bd5d-107">Blob Storage aynı zamanda nesne depolama olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="6bd5d-108">Bu kılavuz Azure Blob Depolama hizmeti kullanılarak yaygın senaryolar gerçekleştirme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="6bd5d-109">C++ ve kullanım örnekleri yazılır [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6bd5d-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="6bd5d-110">Kapsamdaki senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="6bd5d-111">Bu kılavuz, c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hedefler.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="6bd5d-112">Aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, önerilen sürümüdür [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="6bd5d-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="6bd5d-113">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-113">Create a C++ application</span></span>
<span data-ttu-id="6bd5d-114">Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="6bd5d-115">Bunu yapmak için Azure Storage istemci kitaplığı C++ için yükleme ve Azure aboneliğinizde bir Azure depolama hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="6bd5d-116">C++ için Azure Storage istemci kitaplığı yüklemek için aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="6bd5d-117">**Linux:** verilen yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="6bd5d-118">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="6bd5d-119">Aşağıdaki komutu yazın [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="6bd5d-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="6bd5d-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="6bd5d-121">BLOB depolama alanına erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6bd5d-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="6bd5d-122">Azure depolama API'leri BLOB'lar erişmek için kullanmasını istediğiniz C++ dosyanın en üstüne deyimlerini şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="6bd5d-123">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6bd5d-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="6bd5d-124">Bir Azure storage istemci uç noktaları ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgilerini depolamak için bir depolama bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="6bd5d-125">Bir istemci uygulamasında çalıştırırken, depolama hesabı altında listelenen için adını depolama hesabınız ve depolama erişim tuşunu kullanarak depolama bağlantı dizesi şu biçimde sağlamalısınız [Azure Portal](https://portal.azure.com) için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="6bd5d-126">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6bd5d-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="6bd5d-127">Bu örnek, bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="6bd5d-128">Yerel Windows bilgisayarınızda uygulamanızı test etmek için Microsoft Azure kullanabilirsiniz [depolama öykünücüsü](../storage-use-emulator.md) ile yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6bd5d-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="6bd5d-129">Depolama öykünücüsü Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="6bd5d-130">Aşağıdaki örnek, yerel depolama öykünücüsü için bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="6bd5d-131">Azure storage öykünücüsü başlatmak için **Başlat** düğmesini veya tuşuna **Windows** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="6bd5d-132">Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamalar listesinden.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="6bd5d-133">Aşağıdaki örnekler, bu iki yöntemden birini depolama bağlantı dizesini almak için kullanılan olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="6bd5d-134">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-134">Retrieve your connection string</span></span>
<span data-ttu-id="6bd5d-135">Kullanabileceğiniz **cloud_storage_account** depolama hesabı bilgileri temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="6bd5d-136">Depolama bağlantı dizesi, depolama hesabı bilgilerini almak için kullanabileceğiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="6bd5d-137">Ardından, bir başvuru almak bir **cloud_blob_client** sınıfı gibi kapsayıcılar ve bloblar Blob Depolama hizmet içinde depolanan temsil eden nesneler almanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="6bd5d-138">Aşağıdaki kod oluşturur bir **cloud_blob_client** biz alınan yukarıda depolama hesabı nesnesini kullanarak nesnesi:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="6bd5d-139">Nasıl yapılır: bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="6bd5d-140">Bu örnek, zaten yoksa, nasıl bir kapsayıcı oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="6bd5d-141">Varsayılan olarak yeni kapsayıcı özeldir ve Bu kapsayıcıdan BLOB indirmek için depolama erişim anahtarınızı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="6bd5d-142">Dosyaları (BLOB) kapsayıcı içinde herkes tarafından kullanılabilmesini sağlamak istiyorsanız, aşağıdaki kodu kullanarak genel kapsayıcıya ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="6bd5d-143">Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca uygun erişim anahtarı varsa, bunları silin.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="6bd5d-144">Nasıl yapılır: bir kapsayıcıya bir blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="6bd5d-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="6bd5d-145">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="6bd5d-146">Çoğu durumda kullanılması önerilen blob türü blok blobudur.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="6bd5d-147">Bir dosyayı bir blok blobuna yüklemek için bir kapsayıcı başvurusu alın ve blok blob başvurusu almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="6bd5d-148">Bir blob başvurusu edindiğinizde veri kendisine çağırarak yükleyebilirsiniz **upload_from_stream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="6bd5d-149">Bu işlemle, eğer önceden oluşturulmadıysa bir blob oluşturulacaktır, aksi takdirde üzerine yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="6bd5d-150">Aşağıdaki örnek kapsayıcının önceden oluşturulduğunu varsayarak bir blobun bir kapsayıcıya nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="6bd5d-151">Alternatif olarak, kullanabileceğiniz **upload_from_file** bir dosyayı bir blok blobuna yüklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="6bd5d-152">Nasıl yapılır: bir kapsayıcıda BLOB'ları Listele</span><span class="sxs-lookup"><span data-stu-id="6bd5d-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="6bd5d-153">Blob’ları bir kapsayıcıda listelemek için ilk olarak bir kapsayıcı başvurusu edinin.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="6bd5d-154">Kapsayıcının sonra kullanabileceğiniz **list_blobs** blobları ve/veya dizinleri içindeki alma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="6bd5d-155">Zengin özellik ve yöntem erişmek için **list_blob_item**, çağırmalısınız **list_blob_item.as_blob** almak için yöntemi bir **cloud_blob** nesnesi veya **list_blob.as_directory** cloud_blob_directory nesnesini almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="6bd5d-156">Aşağıdaki kodda almak ve her öğe URI'sini çıkış gösterilmiştir **örnek kapsayıcı my** kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="6bd5d-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="6bd5d-157">İşlem listeleme konusunda daha fazla ayrıntı için bkz: [listesi Azure depolama kaynaklarını c++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="6bd5d-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="6bd5d-158">Nasıl yapılır: BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="6bd5d-158">How to: Download blobs</span></span>
<span data-ttu-id="6bd5d-159">BLOB'ları indirmek için önce bir blob başvurusu alın ve ardından çağırın **download_to_stream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="6bd5d-160">Aşağıdaki örnek kullanır **download_to_stream** blob içeriklerini sonra yerel bir dosyaya kalıcı bir akış nesnesine aktarmak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="6bd5d-161">Alternatif olarak, kullanabileceğiniz **download_to_file** bir dosyaya bir blob içeriğini indirmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="6bd5d-162">Ayrıca, ayrıca kullanabileceğiniz **download_text** yöntemi bir blob'u bir metin dizesi olarak içeriğini indirmek için.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="6bd5d-163">Nasıl yapılır: BLOB'ları silme</span><span class="sxs-lookup"><span data-stu-id="6bd5d-163">How to: Delete blobs</span></span>
<span data-ttu-id="6bd5d-164">Bir blobu silmek için önce bir blob başvurusu alın ve ardından çağıran **delete_blob** yöntemini.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="6bd5d-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bd5d-165">Next steps</span></span>
<span data-ttu-id="6bd5d-166">Blob storage'nın öğrendiğinize göre Azure Storage hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6bd5d-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="6bd5d-167">C++ içinden kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="6bd5d-168">Tablo depolama C++ içinden kullanma</span><span class="sxs-lookup"><span data-stu-id="6bd5d-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="6bd5d-169">C++'ta listesi Azure Storage kaynakları</span><span class="sxs-lookup"><span data-stu-id="6bd5d-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="6bd5d-170">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="6bd5d-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="6bd5d-171">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="6bd5d-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="6bd5d-172">AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="6bd5d-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)


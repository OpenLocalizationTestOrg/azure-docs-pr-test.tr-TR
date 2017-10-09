---
title: "C++ içinden aaaHow toouse blob storage (nesne depolama) | Microsoft Docs"
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="959f3-103">Nasıl toouse Blob depolama alanından C++</span><span class="sxs-lookup"><span data-stu-id="959f3-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="959f3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="959f3-104">Overview</span></span>
<span data-ttu-id="959f3-105">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="959f3-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="959f3-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="959f3-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="959f3-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="959f3-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="959f3-108">Bu kılavuzu kullanarak tooperform genel senaryolar Azure Blob Depolama hizmetinin nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="959f3-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="959f3-109">Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="959f3-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="959f3-110">Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="959f3-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="959f3-111">Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello.</span><span class="sxs-lookup"><span data-stu-id="959f3-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="959f3-112">Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="959f3-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="959f3-113">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="959f3-113">Create a C++ application</span></span>
<span data-ttu-id="959f3-114">Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="959f3-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="959f3-115">toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="959f3-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="959f3-116">tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="959f3-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="959f3-117">**Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="959f3-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="959f3-118">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="959f3-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="959f3-119">Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="959f3-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="959f3-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="959f3-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="959f3-121">Uygulama tooaccess Blob Storage yapılandırın</span><span class="sxs-lookup"><span data-stu-id="959f3-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="959f3-122">Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess BLOB'lar istediğiniz hello C++ Hello şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="959f3-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="959f3-123">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="959f3-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="959f3-124">Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="959f3-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="959f3-125">Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello listelenen hello depolama hesabı için depolama hesabı ve hello depolama erişim anahtarınızı hello adını kullanarak hello olarak sağlamalısınız [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="959f3-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="959f3-126">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="959f3-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="959f3-127">Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="959f3-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="959f3-128">tootest uygulamanızı yerel Windows bilgisayarınızda, Microsoft Azure hello kullanabilirsiniz [depolama öykünücüsü](../storage-use-emulator.md) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="959f3-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="959f3-129">Merhaba depolama öykünücüsü hello Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="959f3-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="959f3-130">Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="959f3-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="959f3-131">toostart hello Azure storage öykünücüsü, Select hello **Başlat** düğmesini veya tuşuna hello **Windows** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="959f3-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="959f3-132">Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="959f3-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="959f3-133">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="959f3-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="959f3-134">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="959f3-134">Retrieve your connection string</span></span>
<span data-ttu-id="959f3-135">Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="959f3-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="959f3-136">tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="959f3-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="959f3-137">Ardından, bir başvuru tooa almak **cloud_blob_client** kapsayıcılar ve bloblar Blob Depolama hizmetinin hello içinde depolanan temsil eden tooretrieve nesnelerini izin verdiği ölçüde sınıfı.</span><span class="sxs-lookup"><span data-stu-id="959f3-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="959f3-138">Merhaba aşağıdaki kod oluşturur bir **cloud_blob_client** biz alınan yukarıda hello depolama hesabı nesnesini kullanarak nesnesi:</span><span class="sxs-lookup"><span data-stu-id="959f3-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="959f3-139">Nasıl yapılır: bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="959f3-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="959f3-140">Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="959f3-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="959f3-141">Varsayılan olarak, hello yeni kapsayıcı özeldir ve bu kapsayıcı, depolama erişim anahtarı toodownload bloblarından belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="959f3-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="959f3-142">Merhaba kapsayıcı kullanılabilir tooeveryone içinde toomake hello dosyaları (BLOB) istiyorsanız hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="959f3-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="959f3-143">Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca hello uygun erişim anahtarı varsa, bunları silin.</span><span class="sxs-lookup"><span data-stu-id="959f3-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="959f3-144">Nasıl yapılır: bir kapsayıcıya bir blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="959f3-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="959f3-145">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="959f3-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="959f3-146">Merhaba çoğu durumda, blok blob türü toouse önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="959f3-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="959f3-147">tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın.</span><span class="sxs-lookup"><span data-stu-id="959f3-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="959f3-148">Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **upload_from_stream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="959f3-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="959f3-149">Bu işlem daha önce mevcut alamadık veya mevcut değilse üzerine hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="959f3-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="959f3-150">örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="959f3-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="959f3-151">Alternatif olarak, hello kullanabilirsiniz **upload_from_file** yöntemi tooupload dosya tooa blok blobu.</span><span class="sxs-lookup"><span data-stu-id="959f3-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="959f3-152">Nasıl yapılır: hello BLOB'ları bir kapsayıcıda listelemek</span><span class="sxs-lookup"><span data-stu-id="959f3-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="959f3-153">toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="959f3-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="959f3-154">Merhaba kapsayıcının sonra kullanabileceğiniz **list_blobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki.</span><span class="sxs-lookup"><span data-stu-id="959f3-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="959f3-155">tooaccess hello zengin özellik ve yöntem **list_blob_item**, hello çağırmalısınız **list_blob_item.as_blob** yöntemi tooget bir **cloud_blob** nesnesi veya hello **list_blob.as_directory** yöntemi tooget cloud_blob_directory nesnesi.</span><span class="sxs-lookup"><span data-stu-id="959f3-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="959f3-156">Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir **örnek kapsayıcı my** kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="959f3-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
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

<span data-ttu-id="959f3-157">İşlem listeleme konusunda daha fazla ayrıntı için bkz: [listesi Azure depolama kaynaklarını c++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="959f3-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="959f3-158">Nasıl yapılır: BLOB'ları indirme</span><span class="sxs-lookup"><span data-stu-id="959f3-158">How to: Download blobs</span></span>
<span data-ttu-id="959f3-159">toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **download_to_stream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="959f3-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="959f3-160">Merhaba aşağıdaki örnek kullanır hello **download_to_stream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="959f3-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="959f3-161">Alternatif olarak, hello kullanabilirsiniz **download_to_file** yöntemi toodownload hello blob tooa dosyasının içeriğini.</span><span class="sxs-lookup"><span data-stu-id="959f3-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="959f3-162">Ayrıca, aynı zamanda hello kullanabilirsiniz **download_text** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.</span><span class="sxs-lookup"><span data-stu-id="959f3-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="959f3-163">Nasıl yapılır: BLOB'ları silme</span><span class="sxs-lookup"><span data-stu-id="959f3-163">How to: Delete blobs</span></span>
<span data-ttu-id="959f3-164">bir blob toodelete önce bir blob başvurusu alın ve ardından hello çağırın **delete_blob** yöntemini.</span><span class="sxs-lookup"><span data-stu-id="959f3-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="959f3-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="959f3-165">Next steps</span></span>
<span data-ttu-id="959f3-166">Blob storage'nın hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="959f3-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="959f3-167">Nasıl toouse C++ içinden kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="959f3-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="959f3-168">Nasıl toouse C++ tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="959f3-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="959f3-169">C++'ta listesi Azure Storage kaynakları</span><span class="sxs-lookup"><span data-stu-id="959f3-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="959f3-170">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="959f3-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="959f3-171">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="959f3-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="959f3-172">Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="959f3-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)


---
title: "C++ ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop C++ uygulamaları ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="44e7e-103">C++ ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="44e7e-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="44e7e-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="44e7e-104">About this tutorial</span></span>

<span data-ttu-id="44e7e-105">Bu öğreticide şunları öğreneceksiniz nasıl tooperform Azure File storage üzerinde temel işlemler.</span><span class="sxs-lookup"><span data-stu-id="44e7e-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="44e7e-106">Aracılığıyla örnekleri, C++ ile yazılmış nasıl toocreate paylaşır öğreneceksiniz ve dizinleri, karşıya yükleme, liste ve dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="44e7e-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="44e7e-107">Yeni tooAzure dosya depolama varsa, hello kavramları izleyin hello bölümlerde aracılığıyla hello örnekleri anlaşılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="44e7e-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="44e7e-108">Oluşturma ve Azure dosya paylaşımları silme</span><span class="sxs-lookup"><span data-stu-id="44e7e-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="44e7e-109">Oluşturma ve dizinleri silme</span><span class="sxs-lookup"><span data-stu-id="44e7e-109">Create and delete directories</span></span>
* <span data-ttu-id="44e7e-110">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="44e7e-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="44e7e-111">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="44e7e-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="44e7e-112">Bir Azure dosya paylaşımı için Hello kota (en fazla boyut) ayarlama</span><span class="sxs-lookup"><span data-stu-id="44e7e-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="44e7e-113">Merhaba paylaşımında tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44e7e-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="44e7e-114">SMB üzerinden Azure File storage erişilebileceği için hello standart C++ g/ç sınıfları ve işlevleri kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var.</span><span class="sxs-lookup"><span data-stu-id="44e7e-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="44e7e-115">Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama C++ SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.</span><span class="sxs-lookup"><span data-stu-id="44e7e-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="44e7e-116">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44e7e-116">Create a C++ application</span></span>
<span data-ttu-id="44e7e-117">toobuild hello örnekleri, C++ için tooinstall hello Azure Storage istemci kitaplığı 2.4.0 gerekir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="44e7e-118">Ayrıca bir Azure depolama hesabı oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="44e7e-119">tooinstall hello Azure Storage istemcisi 2.4.0 C++ için yöntemler aşağıdaki hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44e7e-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="44e7e-120">**Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="44e7e-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="44e7e-121">**Windows:** Visual Studio'da sırasıyla **Araçları &gt; NuGet Paket Yöneticisi &gt; Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="44e7e-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="44e7e-122">Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="44e7e-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="44e7e-123">Uygulama toouse Azure File storage ayarlayın</span><span class="sxs-lookup"><span data-stu-id="44e7e-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="44e7e-124">Deyimleri toohello üst toomanipulate Azure File storage istediğiniz hello C++ kaynak dosyasının Hello şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44e7e-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="44e7e-125">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="44e7e-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="44e7e-126">Dosya depolama toouse tooconnect tooyour Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="44e7e-127">Merhaba ilk adımı tooconfigure kullanacağız bir bağlantı dizesi olacaktır tooconnect tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="44e7e-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="44e7e-128">Şimdi bir statik değişken toodo tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="44e7e-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="44e7e-129">Tooan Azure depolama hesabı bağlanma</span><span class="sxs-lookup"><span data-stu-id="44e7e-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="44e7e-130">Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="44e7e-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="44e7e-131">tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="44e7e-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="44e7e-132">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44e7e-132">Create an Azure File share</span></span>
<span data-ttu-id="44e7e-133">Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="44e7e-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="44e7e-134">Depolama hesabınız hesap kapasitenizi verdiğinden sayıda paylaşımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="44e7e-135">tooobtain erişim tooa paylaşımı ve içeriklerini, toouse Azure dosya depolama istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="44e7e-136">Hello Azure File storage İstemcisi'ni kullanarak bir başvuru tooa paylaşımı edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="44e7e-137">toocreate hello paylaşımı, kullanım hello **create_if_not_exists** hello yöntemi **cloud_file_share** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="44e7e-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="44e7e-138">Bu noktada, **paylaşmak** adlı bir başvuru tooa paylaşımı tutan **örnek paylaşımı my**.</span><span class="sxs-lookup"><span data-stu-id="44e7e-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="44e7e-139">Bir Azure Dosya Paylaşımı Sil</span><span class="sxs-lookup"><span data-stu-id="44e7e-139">Delete an Azure File share</span></span>
<span data-ttu-id="44e7e-140">Bir paylaşım silme arama hello tarafından yapılır **delete_if_exists** cloud_file_share nesnesi üzerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="44e7e-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="44e7e-141">Yapan örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="44e7e-142">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="44e7e-142">Create a directory</span></span>
<span data-ttu-id="44e7e-143">Bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="44e7e-144">Azure File storage hesabı olacak olarak birden çok dizini izin toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="44e7e-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="44e7e-145">Aşağıdaki Hello kodu adlı bir dizin oluşturur **örnek dizin my** adlı bir alt yanı sıra hello kök dizini altında **örnek alt my**.</span><span class="sxs-lookup"><span data-stu-id="44e7e-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="44e7e-146">Bir dizini silme</span><span class="sxs-lookup"><span data-stu-id="44e7e-146">Delete a directory</span></span>
<span data-ttu-id="44e7e-147">Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizin silinmesi basit bir görev olduğundan.</span><span class="sxs-lookup"><span data-stu-id="44e7e-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="44e7e-148">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="44e7e-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="44e7e-149">Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **list_files_and_directories** üzerinde bir **cloud_file_directory** başvuru.</span><span class="sxs-lookup"><span data-stu-id="44e7e-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="44e7e-150">tooaccess hello zengin özellik ve yöntem **list_file_and_directory_item**, hello çağırmalısınız **list_file_and_directory_item.as_file** yöntemi tooget bir **cloud_ Dosya** nesne veya hello **list_file_and_directory_item.as_directory** yöntemi tooget bir **cloud_file_directory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="44e7e-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="44e7e-151">koddan hello tooretrieve ve çıkış URI hello paylaşımının hello kök dizininde her öğesinin nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="44e7e-152">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="44e7e-152">Upload a file</span></span>
<span data-ttu-id="44e7e-153">Merhaba çok, bir Azure dosya paylaşımı dosyalarının bulunduğu bir kök dizin içeriyor.</span><span class="sxs-lookup"><span data-stu-id="44e7e-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="44e7e-154">Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="44e7e-155">bir dosyayı karşıya yüklemeyi hello ilk adımı tooobtain bulunduğu bir başvuru toohello dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="44e7e-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="44e7e-156">Arama hello tarafından bunu **get_root_directory_reference** hello Paylaşım nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="44e7e-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="44e7e-157">Bir başvuru toohello kök dizin hello paylaşımının sahip olduğunuza göre üzerine bir dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="44e7e-158">Bu örnek, bir dosya, metin ve bir akış yükler.</span><span class="sxs-lookup"><span data-stu-id="44e7e-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="44e7e-159">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="44e7e-159">Download a file</span></span>
<span data-ttu-id="44e7e-160">toodownload dosyaları, önce dosya başvurusu alın ve ardından hello çağırın **download_to_stream** sonra sürdürebilirsiniz yöntemi tootransfer hello dosya içeriği tooa akış nesne tooa yerel dosya.</span><span class="sxs-lookup"><span data-stu-id="44e7e-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="44e7e-161">Alternatif olarak, hello kullanabilirsiniz **download_to_file** yöntemi toodownload hello bir dosya tooa yerel dosyanın içeriğini.</span><span class="sxs-lookup"><span data-stu-id="44e7e-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="44e7e-162">Merhaba kullanabilirsiniz **download_text** yöntemi toodownload hello bir metin dizesi olarak bir dosyanın içeriğini.</span><span class="sxs-lookup"><span data-stu-id="44e7e-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="44e7e-163">Merhaba aşağıdaki örnek kullanır hello **download_to_stream** ve **download_text** yöntemleri toodemonstrate önceki kısımlarında oluşturulan hello dosyaları indirme.</span><span class="sxs-lookup"><span data-stu-id="44e7e-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="44e7e-164">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="44e7e-164">Delete a file</span></span>
<span data-ttu-id="44e7e-165">Başka bir ortak Azure File storage dosya silme işlemdir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="44e7e-166">Merhaba aşağıdaki kod my-örnek-dosya-hello kök dizini altında depolanan 3 adlı bir dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="44e7e-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="44e7e-167">Bir Azure dosya paylaşımı için Hello kota (en fazla boyut) ayarlama</span><span class="sxs-lookup"><span data-stu-id="44e7e-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="44e7e-168">Gigabayt cinsinden bir dosya paylaşımı için hello kota (veya üst sınırı) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="44e7e-169">Ayrıca, ne kadar veri şu anda hello paylaşımında depolanan toosee kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="44e7e-170">Ayarı hello tarafından paylaşımı için kota bir, hello paylaşımında depolanan hello dosyaların toplam boyutu hello sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="44e7e-171">Hello hello paylaşımdaki dosyaların toplam boyutu aşarsa hello kota hello paylaşımında ayarlayın, sonra istemcileri oluşturulamıyor tooincrease hello mevcut dosyaların boyutunu olabilir veya bu dosyaları boş olmadığı sürece, yeni dosyalar oluşturma.</span><span class="sxs-lookup"><span data-stu-id="44e7e-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="44e7e-172">Aşağıdaki örnek Hello nasıl toocheck hello bir paylaşım için geçerli kullanım ve nasıl tooset hello hello paylaşımı için kota gösterir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="44e7e-173">Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="44e7e-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="44e7e-174">Paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="44e7e-175">Ayrıca, bir dosya paylaşımı toomanage paylaşılan erişim imzaları bir paylaşılan erişim ilkesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44e7e-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="44e7e-176">Tehlikeye girdiği durumlarda hello SAS iptal etme yolu sağladığı gibi bir paylaşılan erişim ilkesi oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="44e7e-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="44e7e-177">Aşağıdaki örneğine hello bir paylaşılan erişim ilkesi oluşturulur ve Itanium tabanlı sistemler için ilke tooprovide hello kısıtlamaları SAS için hello bir dosyada paylaşıma kullanır.</span><span class="sxs-lookup"><span data-stu-id="44e7e-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="44e7e-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44e7e-178">Next steps</span></span>
<span data-ttu-id="44e7e-179">Azure Storage hakkında daha fazla toolearn bu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="44e7e-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="44e7e-180">C++ için Depolama İstemcisi Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="44e7e-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="44e7e-181">[Azure depolama dosya hizmeti örnekleri c++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="44e7e-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="44e7e-182">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="44e7e-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="44e7e-183">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="44e7e-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
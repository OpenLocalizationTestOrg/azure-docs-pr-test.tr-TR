---
title: "C++ ile Azure File storage için geliştirme | Microsoft Docs"
description: "C++ uygulamaları ve dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmeyi öğrenin."
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
ms.openlocfilehash: fc0d8451442f1337db4a36718c3fc746f8eb5125
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="05909-103">C++ ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="05909-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="05909-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="05909-104">About this tutorial</span></span>

<span data-ttu-id="05909-105">Bu öğreticide, Azure File storage temel işlemleri gerçekleştirmek öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-105">In this tutorial, you'll learn how to perform basic operations on Azure File storage.</span></span> <span data-ttu-id="05909-106">C++'da yazılmış örnekleri sayesinde, paylaşımları ve dizinler oluşturma, karşıya yükleme, liste ve dosyaları silin öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="05909-107">Azure dosya depolama alanına yeniyseniz, aşağıdaki bölümlerde açıklanan kavramlar aracılığıyla örnekleri anlaşılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="05909-107">If you are new to Azure File storage , going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>


* <span data-ttu-id="05909-108">Oluşturma ve Azure dosya paylaşımları silme</span><span class="sxs-lookup"><span data-stu-id="05909-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="05909-109">Oluşturma ve dizinleri silme</span><span class="sxs-lookup"><span data-stu-id="05909-109">Create and delete directories</span></span>
* <span data-ttu-id="05909-110">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="05909-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="05909-111">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="05909-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="05909-112">Bir Azure dosya paylaşımı için kota (en fazla boyut) ayarlama</span><span class="sxs-lookup"><span data-stu-id="05909-112">Set the quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="05909-113">Paylaşımda tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturma.</span><span class="sxs-lookup"><span data-stu-id="05909-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>

> [!Note]  
> <span data-ttu-id="05909-114">SMB üzerinden Azure File storage erişilebileceği için standart C++ g/ç sınıfları ve işlevleri kullanarak Azure dosya paylaşımına erişmek basit uygulamaları yazmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="05909-114">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard C++ I/O classes and functions.</span></span> <span data-ttu-id="05909-115">Bu makalede Azure depolama C++ kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosya depolama alanına anlaşmak için.</span><span class="sxs-lookup"><span data-stu-id="05909-115">This article will describe how to write applications that use the Azure Storage C++ SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="05909-116">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="05909-116">Create a C++ application</span></span>
<span data-ttu-id="05909-117">Örnekleri oluşturmak için Azure Storage istemci Kitaplığı'nı 2.4.0 C++ için yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05909-117">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="05909-118">Ayrıca bir Azure depolama hesabı oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="05909-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="05909-119">C++ için Azure Storage istemcisi 2.4.0 yüklemek için aşağıdaki yöntemlerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05909-119">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="05909-120">**Linux:** verilen yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="05909-120">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="05909-121">**Windows:** Visual Studio'da sırasıyla **Araçları &gt; NuGet Paket Yöneticisi &gt; Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="05909-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="05909-122">Aşağıdaki komutu yazın [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="05909-122">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="05909-123">Uygulamanızı Azure File storage kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="05909-123">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="05909-124">Azure File storage yönetmek istediğiniz C++ kaynak dosyanın en üstüne deyimleri şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="05909-124">Add the following include statements to the top of the C++ source file where you want to manipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="05909-125">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="05909-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="05909-126">Dosya depolama kullanmak için Azure depolama hesabınıza bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05909-126">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="05909-127">İlk adım, depolama hesabınıza bağlanmak için kullanacağız bir bağlantı dizesini yapılandırmak için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="05909-127">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="05909-128">Şimdi bunun için statik bir değişken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="05909-128">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="05909-129">Bir Azure depolama hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="05909-129">Connecting to an Azure storage account</span></span>
<span data-ttu-id="05909-130">Kullanabileceğiniz **cloud_storage_account** depolama hesabı bilgileri temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="05909-130">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="05909-131">Depolama bağlantı dizesi, depolama hesabı bilgilerini almak için kullanabileceğiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05909-131">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="05909-132">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="05909-132">Create an Azure File share</span></span>
<span data-ttu-id="05909-133">Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="05909-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="05909-134">Depolama hesabınız hesap kapasitenizi verdiğinden sayıda paylaşımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="05909-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="05909-135">Bir paylaşımı ve içeriklerini erişim sağlamak için Azure dosya depolama istemcisi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05909-135">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```cpp
// Create the Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="05909-136">Azure File storage İstemcisi'ni kullanarak bir paylaşım için bir başvuru edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-136">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="05909-137">Paylaşımı oluşturmak için kullanın **create_if_not_exists** yöntemi **cloud_file_share** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="05909-137">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="05909-138">Bu noktada, **paylaşmak** adlı bir paylaşım için bir başvuru tutan **örnek paylaşımı my**.</span><span class="sxs-lookup"><span data-stu-id="05909-138">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="05909-139">Bir Azure Dosya Paylaşımı Sil</span><span class="sxs-lookup"><span data-stu-id="05909-139">Delete an Azure File share</span></span>
<span data-ttu-id="05909-140">Bir paylaşım silme yapılır çağırarak **delete_if_exists** cloud_file_share nesnesi üzerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05909-140">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="05909-141">Yapan örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="05909-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="05909-142">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="05909-142">Create a directory</span></span>
<span data-ttu-id="05909-143">Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları koyarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-143">You can organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="05909-144">Azure File storage hesabınıza izin verdiği sayıda dizinleri oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="05909-144">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="05909-145">Aşağıdaki kodu adlı bir dizin oluşturacak **örnek dizin my** adlı bir alt yanı sıra kök dizini altında **örnek alt my**.</span><span class="sxs-lookup"><span data-stu-id="05909-145">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="05909-146">Bir dizini silme</span><span class="sxs-lookup"><span data-stu-id="05909-146">Delete a directory</span></span>
<span data-ttu-id="05909-147">Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizin silinmesi basit bir görev olduğundan.</span><span class="sxs-lookup"><span data-stu-id="05909-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="05909-148">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="05909-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="05909-149">Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **list_files_and_directories** üzerinde bir **cloud_file_directory** başvuru.</span><span class="sxs-lookup"><span data-stu-id="05909-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="05909-150">Zengin özellik ve yöntem erişmek için **list_file_and_directory_item**, çağırmalısınız **list_file_and_directory_item.as_file** almak için yöntemi bir **cloud_file**  nesnesi veya **list_file_and_directory_item.as_directory** almak için yöntemi bir **cloud_file_directory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="05909-150">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="05909-151">Aşağıdaki kod, almak ve paylaşımın kök dizininde bulunan her öğesinin URI çıkış gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="05909-151">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
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

## <a name="upload-a-file"></a><span data-ttu-id="05909-152">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="05909-152">Upload a file</span></span>
<span data-ttu-id="05909-153">En azından bir Azure dosya paylaşımı dosyalarının bulunduğu kök dizini içerir.</span><span class="sxs-lookup"><span data-stu-id="05909-153">At the very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="05909-154">Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-154">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="05909-155">Bir dosyayı karşıya yüklemeyi ilk adımı bulunduğu dizin başvuru elde edilir.</span><span class="sxs-lookup"><span data-stu-id="05909-155">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="05909-156">Çağırarak bunu **get_root_directory_reference** Paylaşım nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05909-156">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="05909-157">Bir başvuru paylaşımının kök dizinine sahip olduğunuza göre üzerine bir dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-157">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="05909-158">Bu örnek, bir dosya, metin ve bir akış yükler.</span><span class="sxs-lookup"><span data-stu-id="05909-158">This example uploads from a file, from text, and from a stream.</span></span>

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

## <a name="download-a-file"></a><span data-ttu-id="05909-159">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="05909-159">Download a file</span></span>
<span data-ttu-id="05909-160">Dosyalarını indirmek için önce bir dosya başvurusu alın ve ardından arama **download_to_stream** dosya içeriğini sonra yerel bir dosyaya kalıcı bir akış nesnesine aktarmak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="05909-160">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="05909-161">Alternatif olarak, kullanabileceğiniz **download_to_file** yerel bir dosyaya bir dosyanın içeriğini indirmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="05909-161">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="05909-162">Kullanabileceğiniz **download_text** bir metin dizesi olarak bir dosyanın içeriğini indirmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="05909-162">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="05909-163">Aşağıdaki örnek kullanır **download_to_stream** ve **download_text** önceki kısımlarında oluşturulan dosyaları indirme göstermek için yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="05909-163">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="05909-164">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="05909-164">Delete a file</span></span>
<span data-ttu-id="05909-165">Başka bir ortak Azure File storage dosya silme işlemdir.</span><span class="sxs-lookup"><span data-stu-id="05909-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="05909-166">Aşağıdaki kod, my-örnek-dosya-kök dizini altında depolanan 3 adlı bir dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="05909-166">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="05909-167">Bir Azure dosya paylaşımı için kota (en fazla boyut) ayarlama</span><span class="sxs-lookup"><span data-stu-id="05909-167">Set the quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="05909-168">Gigabayt cinsinden bir dosya paylaşımı için kota (veya üst sınırı) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-168">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="05909-169">Paylaşımda halihazırda ne kadar verinin depolandığını da kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-169">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="05909-170">Paylaşım için kota ayarlayarak paylaşımda depolanan toplam dosya boyutunu kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-170">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="05909-171">Paylaşımdaki toplam dosya boyutu belirlediğiniz kotayı aşarsa, istemciler mevcut dosyaların boyutunu artıramaz veya boş olmamaları halinde yeni dosyalar oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="05909-171">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="05909-172">Aşağıdaki örnekte, paylaşımdaki mevcut kullanımını nasıl kontrol edileceği veya paylaşım için nasıl kota ayarlanacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="05909-172">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="05909-173">Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="05909-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="05909-174">Paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="05909-175">Ayrıca, paylaşılan erişim imzalarını yönetmek için dosya paylaşımında bir paylaşılan erişim ilkesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05909-175">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="05909-176">Gizliliğinin tehlikeye girdiği durumlarda SAS’yi iptal etme aracı olarak kullanılabilmesi nedeniyle bir paylaşılan erişim ilkesi oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="05909-176">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="05909-177">Aşağıdaki örnekte, paylaşım için bir paylaşılan erişim ilkesi oluşturulur, daha sonra bu ilke paylaşımdaki bir dosyada bulunan SAS için sınırlamalar sağlamak amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="05909-177">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
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

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="05909-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05909-178">Next steps</span></span>
<span data-ttu-id="05909-179">Azure Storage hakkında daha fazla bilgi için şu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="05909-179">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="05909-180">C++ için Depolama İstemcisi Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="05909-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="05909-181">[Azure depolama dosya hizmeti örnekleri c++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="05909-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="05909-182">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="05909-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="05909-183">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="05909-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
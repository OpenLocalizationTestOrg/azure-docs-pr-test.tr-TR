---
title: Ruby'den BLOB storage (nesne depolama) kullanma | Microsoft Docs
description: "Azure Blob Storage (nesne depolama) ile bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="92c1b-103">Ruby’den Blob Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="92c1b-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="92c1b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="92c1b-104">Overview</span></span>
<span data-ttu-id="92c1b-105">Azure Blob Storage, bulutta nesne/blob olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="92c1b-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="92c1b-107">Blob Storage aynı zamanda nesne depolama olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="92c1b-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="92c1b-108">Bu kılavuz yaygın senaryolar Blob storage kullanarak gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="92c1b-109">Örnekler, Ruby API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="92c1b-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="92c1b-110">Kapsamdaki senaryolar dahil **karşıya yükleme, listeleme, indirme,** ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="92c1b-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="92c1b-111">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c1b-111">Create a Ruby application</span></span>
<span data-ttu-id="92c1b-112">Bir Ruby uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="92c1b-112">Create a Ruby application.</span></span> <span data-ttu-id="92c1b-113">Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="92c1b-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="92c1b-114">Depolama alanına erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="92c1b-114">Configure your application to access Storage</span></span>
<span data-ttu-id="92c1b-115">Azure Storage kullanmak için indirme ve storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Söyleniş azure paketini kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="92c1b-116">Paket elde etmek için RubyGems kullanın</span><span class="sxs-lookup"><span data-stu-id="92c1b-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="92c1b-117">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="92c1b-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="92c1b-118">Gem ve bağımlılıklarını yüklemek için komut penceresinde "gem yükleme azure" yazın.</span><span class="sxs-lookup"><span data-stu-id="92c1b-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="92c1b-119">Paket alma</span><span class="sxs-lookup"><span data-stu-id="92c1b-119">Import the package</span></span>
<span data-ttu-id="92c1b-120">Sık kullandığınız metin Düzenleyicisi'ni kullanarak aşağıdaki depolama kullanmak istediğiniz yere Söyleniş dosyasının üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="92c1b-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="92c1b-121">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="92c1b-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="92c1b-122">Azure modülü ortam değişkenleri okur **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** Azure depolama hesabınıza bağlanmak için gerekli bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="92c1b-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="92c1b-123">Bu ortam değişkenleri ayarlanmamışsa, hesap bilgilerini kullanmadan önce belirtmelisiniz **Azure::Blob::BlobService** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="92c1b-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="92c1b-124">Klasik veya Resource Manager depolama hesabı Azure portalında bu değerleri almak için:</span><span class="sxs-lookup"><span data-stu-id="92c1b-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="92c1b-125">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="92c1b-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="92c1b-126">Kullanmak istediğiniz depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="92c1b-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="92c1b-127">Sağ taraftaki ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="92c1b-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="92c1b-128">Görüntülenen erişim anahtarları dikey penceresinde, erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="92c1b-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="92c1b-129">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c1b-129">You can use either of these.</span></span>
5. <span data-ttu-id="92c1b-130">Anahtarı panoya kopyalamak için Kopyala simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c1b-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="92c1b-131">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c1b-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="92c1b-132">**Azure::Blob::BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="92c1b-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="92c1b-133">Bir kapsayıcı oluşturmak için kullanmak **oluşturma\_container()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92c1b-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="92c1b-134">Aşağıdaki kod örneği, bir kapsayıcı oluşturur veya hata varsa yazdırır.</span><span class="sxs-lookup"><span data-stu-id="92c1b-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="92c1b-135">Dosya kapsayıcıda genel hale getirmek istiyorsanız, kapsayıcının izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c1b-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="92c1b-136">Yalnızca değiştirebileceğiniz <strong>oluşturma\_container()</strong> geçirmek için çağrı **: ortak\_erişim\_düzeyi** seçeneği:</span><span class="sxs-lookup"><span data-stu-id="92c1b-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="92c1b-137">İçin geçerli değerler **: ortak\_erişim\_düzeyi** seçeneği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92c1b-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="92c1b-138">**BLOB:** BLOB'lar için herkese okuma erişimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="92c1b-139">Bu kapsayıcı içindeki BLOB verilerini anonim istek okunabilir ancak kapsayıcı verileri mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="92c1b-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="92c1b-140">İstemcilerin anonim istek aracılığıyla kapsayıcıdaki blobları numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="92c1b-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="92c1b-141">**kapsayıcı:** tam ortak okuma erişimi için kapsayıcı ve blob verilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="92c1b-142">İstemcilerin anonim istek aracılığıyla kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="92c1b-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="92c1b-143">Alternatif olarak, bir kapsayıcı genel erişim düzeyini kullanarak değiştirebileceğiniz **ayarlamak\_kapsayıcı\_acl()** yöntemi ortak erişim düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="92c1b-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="92c1b-144">Aşağıdaki kod örneğinde genel erişim düzeyini değiştirir **kapsayıcı**:</span><span class="sxs-lookup"><span data-stu-id="92c1b-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="92c1b-145">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="92c1b-145">Upload a blob into a container</span></span>
<span data-ttu-id="92c1b-146">Bir blobu içerik yüklemek için kullanmak **oluşturma\_blok\_blob()** blob oluşturmak için yöntemi, blob içeriği olarak bir dosya veya dize kullanın.</span><span class="sxs-lookup"><span data-stu-id="92c1b-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="92c1b-147">Aşağıdaki kod dosya yüklemeleri **test.png** "görüntü-blob'u" kapsayıcısında adlı yeni bir blob olarak.</span><span class="sxs-lookup"><span data-stu-id="92c1b-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="92c1b-148">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="92c1b-148">List the blobs in a container</span></span>
<span data-ttu-id="92c1b-149">Kapsayıcılar listelemek için kullanın **list_containers()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92c1b-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="92c1b-150">Bir kapsayıcıdaki blobları listelemek için kullanın **listesi\_blobs()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92c1b-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="92c1b-151">Bu hesap için tüm kapsayıcılarında tüm BLOB'lar URL'lerini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="92c1b-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="92c1b-152">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="92c1b-152">Download blobs</span></span>
<span data-ttu-id="92c1b-153">BLOB'ları indirmek için kullanacağınız **almak\_blob()** içeriği alma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92c1b-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="92c1b-154">Aşağıdaki kod örneğinde kullanımı gösterilir **almak\_blob()** "görüntü blob'u" içeriğini indirmek ve yerel bir dosyaya yazmak için.</span><span class="sxs-lookup"><span data-stu-id="92c1b-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="92c1b-155">Bir Blob Sil</span><span class="sxs-lookup"><span data-stu-id="92c1b-155">Delete a Blob</span></span>
<span data-ttu-id="92c1b-156">Son olarak, bir blobu silmek için kullanın **silmek\_blob()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92c1b-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="92c1b-157">Aşağıdaki kod örneği, bir blobu silmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="92c1b-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="92c1b-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92c1b-158">Next steps</span></span>
<span data-ttu-id="92c1b-159">Daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="92c1b-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="92c1b-160">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="92c1b-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="92c1b-161">[Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="92c1b-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="92c1b-162">AzCopy Komut Satırı Yardımcı Programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="92c1b-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)


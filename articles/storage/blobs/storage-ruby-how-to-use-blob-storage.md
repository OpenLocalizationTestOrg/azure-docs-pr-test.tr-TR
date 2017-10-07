---
title: aaaHow toouse ruby'den Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
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
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="42291-103">Nasıl toouse ruby'den Blob storage</span><span class="sxs-lookup"><span data-stu-id="42291-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="42291-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="42291-104">Overview</span></span>
<span data-ttu-id="42291-105">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="42291-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="42291-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="42291-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="42291-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="42291-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="42291-108">Bu kılavuz size nasıl gösterir Blob storage kullanarak tooperform senaryoları.</span><span class="sxs-lookup"><span data-stu-id="42291-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="42291-109">Merhaba örnekleri hello Ruby API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="42291-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="42291-110">Merhaba kapsanan senaryolar dahil **karşıya yükleme, listeleme, indirme,** ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="42291-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="42291-111">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="42291-111">Create a Ruby application</span></span>
<span data-ttu-id="42291-112">Bir Ruby uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42291-112">Create a Ruby application.</span></span> <span data-ttu-id="42291-113">Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="42291-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="42291-114">Uygulama tooaccess depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="42291-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="42291-115">Azure Storage toouse, toodownload ve kullanım hello hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="42291-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="42291-116">RubyGems tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="42291-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="42291-117">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="42291-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="42291-118">"Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.</span><span class="sxs-lookup"><span data-stu-id="42291-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="42291-119">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="42291-119">Import hello package</span></span>
<span data-ttu-id="42291-120">Sık kullandığınız metin Düzenleyicisi'ni kullanarak hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="42291-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="42291-121">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="42291-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="42291-122">Hello azure modülü hello ortam değişkenleri okuma **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** için bilgi tooconnect tooyour Azure depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="42291-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="42291-123">Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::Blob::BlobService** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="42291-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="42291-124">tooobtain hello Azure portal bu değerleri Klasik veya Resource Manager depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="42291-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="42291-125">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42291-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="42291-126">Toouse istediğiniz toohello depolama hesabının gidin.</span><span class="sxs-lookup"><span data-stu-id="42291-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="42291-127">Merhaba sağ üzerinde Hello ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="42291-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="42291-128">Görüntülenen hello erişim anahtarları dikey penceresinde hello erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="42291-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="42291-129">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42291-129">You can use either of these.</span></span>
5. <span data-ttu-id="42291-130">Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="42291-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="42291-131">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="42291-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="42291-132">Merhaba **Azure::Blob::BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="42291-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="42291-133">toocreate bir kapsayıcı kullanmak hello **oluşturma\_container()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="42291-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="42291-134">Merhaba aşağıdaki kod örneğinde bir kapsayıcı oluşturur veya varsa hello hata yazdırır.</span><span class="sxs-lookup"><span data-stu-id="42291-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="42291-135">Toomake hello hello kapsayıcı dosyalarında ortak istiyorsanız hello kapsayıcının izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42291-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="42291-136">Merhaba yalnızca değiştirebileceğiniz <strong>oluşturma\_container()</strong> çağrısı toopass hello **: ortak\_erişim\_düzeyi** seçeneği:</span><span class="sxs-lookup"><span data-stu-id="42291-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="42291-137">Hello için geçerli değerler **: ortak\_erişim\_düzeyi** seçeneği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="42291-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="42291-138">**BLOB:** BLOB'lar için herkese okuma erişimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="42291-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="42291-139">Bu kapsayıcı içindeki BLOB verilerini anonim istek okunabilir ancak kapsayıcı verileri mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="42291-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="42291-140">İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="42291-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="42291-141">**kapsayıcı:** tam ortak okuma erişimi için kapsayıcı ve blob verilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="42291-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="42291-142">İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="42291-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="42291-143">Alternatif olarak, bir kapsayıcı hello genel erişim düzeyini kullanarak değiştirebileceğiniz **ayarlamak\_kapsayıcı\_acl()** yöntemi toospecify hello genel erişim düzeyi.</span><span class="sxs-lookup"><span data-stu-id="42291-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="42291-144">Aşağıdaki kod örneğine değişiklikleri hello genel erişim düzeyi çok hello**kapsayıcı**:</span><span class="sxs-lookup"><span data-stu-id="42291-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="42291-145">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="42291-145">Upload a blob into a container</span></span>
<span data-ttu-id="42291-146">tooupload içerik tooa blob, kullanım hello **oluşturma\_blok\_blob()** yöntemi toocreate hello blob, bir dosya kullanın veya dize hello BLOB Merhaba içeriğine.</span><span class="sxs-lookup"><span data-stu-id="42291-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="42291-147">Merhaba aşağıdaki kodu hello dosya yüklemeleri **test.png** "görüntü-blob'u" Merhaba kapsayıcısında adlı yeni bir blob olarak.</span><span class="sxs-lookup"><span data-stu-id="42291-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="42291-148">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="42291-148">List hello blobs in a container</span></span>
<span data-ttu-id="42291-149">toolist hello kapsayıcılar kullanma **list_containers()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="42291-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="42291-150">bir kapsayıcıdaki toolist hello BLOB'ları kullanmak **listesi\_blobs()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="42291-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="42291-151">Bu, tüm Merhaba kapsayıcılara hello hesabı için tüm hello blobları hello URL'lerini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="42291-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="42291-152">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="42291-152">Download blobs</span></span>
<span data-ttu-id="42291-153">toodownload BLOB'ları kullanmak hello **almak\_blob()** yöntemi tooretrieve hello içeriği.</span><span class="sxs-lookup"><span data-stu-id="42291-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="42291-154">Merhaba aşağıdaki kod örneğinde kullanarak gösterilmektedir **almak\_blob()** toodownload hello "görüntü blob'u" içeriğini ve tooa yerel dosya yazma.</span><span class="sxs-lookup"><span data-stu-id="42291-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="42291-155">Bir Blob Sil</span><span class="sxs-lookup"><span data-stu-id="42291-155">Delete a Blob</span></span>
<span data-ttu-id="42291-156">Son olarak, bir blob toodelete kullanmak hello **silmek\_blob()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="42291-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="42291-157">Merhaba aşağıdaki kod örneğinde gösterilmektedir nasıl toodelete blob.</span><span class="sxs-lookup"><span data-stu-id="42291-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="42291-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42291-158">Next steps</span></span>
<span data-ttu-id="42291-159">daha karmaşık depolama görevleri hakkında toolearn bu bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="42291-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="42291-160">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="42291-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="42291-161">[Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="42291-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="42291-162">Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="42291-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)


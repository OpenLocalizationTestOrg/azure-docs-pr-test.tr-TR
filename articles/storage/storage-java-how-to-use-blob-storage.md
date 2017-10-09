---
title: aaaHow toouse Java'dan Azure Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="d6bbb-103">Nasıl toouse Java'dan Blob storage</span><span class="sxs-lookup"><span data-stu-id="d6bbb-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="d6bbb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d6bbb-104">Overview</span></span>
<span data-ttu-id="d6bbb-105">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="d6bbb-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="d6bbb-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="d6bbb-108">Bu makale nasıl Microsoft Azure Blob storage kullanarak tooperform genel senaryolar hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="d6bbb-109">Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d6bbb-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="d6bbb-110">Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="d6bbb-111">BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#Next-Steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="d6bbb-112">Bir SDK'sı, Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="d6bbb-113">Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="d6bbb-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="d6bbb-114">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bbb-114">Create a Java application</span></span>
<span data-ttu-id="d6bbb-115">Bu makalede, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="d6bbb-116">toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="d6bbb-117">Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="d6bbb-118">Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="d6bbb-119">Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="d6bbb-120">Uygulama tooaccess Blob storage'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6bbb-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="d6bbb-121">İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess BLOB'lar istediğiniz hello Java aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d6bbb-122">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="d6bbb-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="d6bbb-123">Bir Azure Storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d6bbb-124">Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d6bbb-125">Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="d6bbb-126">Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="d6bbb-127">Merhaba aşağıdaki örnek alır hello bağlantı dizesinden bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="d6bbb-128">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d6bbb-129">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bbb-129">Create a container</span></span>
<span data-ttu-id="d6bbb-130">A **CloudBlobClient** nesne kapsayıcılar ve bloblar için başvuru nesneleri alma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="d6bbb-131">Merhaba aşağıdaki kod oluşturur bir **CloudBlobClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="d6bbb-132">Başka bir yolu toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].</span><span class="sxs-lookup"><span data-stu-id="d6bbb-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d6bbb-133">Kullanım hello **CloudBlobClient** tooget toouse istediğiniz bir başvuru toohello kapsayıcı nesne.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="d6bbb-134">Merhaba ile yoksa hello kapsayıcı oluşturabilirsiniz **createIfNotExists** aksi hello var olan bir kapsayıcı döndürür yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="d6bbb-135">(Daha önce yaptığınız gibi), depolama erişim anahtarınızı belirtmeniz gerekir böylece varsayılan olarak, hello yeni kapsayıcı özel, bu kapsayıcı toodownload bloblarından.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="d6bbb-136">İsteğe bağlı: genel erişim için bir kapsayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d6bbb-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="d6bbb-137">Bir kapsayıcının izinleri varsayılan olarak özel erişim için yapılandırılmış, ancak hello Internet üzerinde bir kapsayıcının izinleri tooallow genel, salt okunur erişim tüm kullanıcılar için kolayca yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d6bbb-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d6bbb-138">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="d6bbb-138">Upload a blob into a container</span></span>
<span data-ttu-id="d6bbb-139">tooupload dosya tooa blob bir kapsayıcı başvurusu alın ve tooget bir blob başvurusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="d6bbb-140">Bir blob başvurusu edindiğinizde hello blob başvurusu üzerinde karşıya yükleme çağırarak tüm akış karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="d6bbb-141">Mevcut veya varsa üzerine değildir, bu işlem hello blob oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="d6bbb-142">Aşağıdaki kod örneği hello bu gösterir ve bu hello kapsayıcısı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="d6bbb-143">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="d6bbb-143">List hello blobs in a container</span></span>
<span data-ttu-id="d6bbb-144">toolist hello BLOB'ları bir kapsayıcıda ilk alın bir kapsayıcı başvurusu blob tooupload yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="d6bbb-145">Merhaba kapsayıcının kullanabilirsiniz **listBlobs** yöntemi ile bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="d6bbb-146">Merhaba aşağıdaki kodu hello her blob bir kapsayıcı toohello konsolunda URI'sini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="d6bbb-147">Blobları adlarında yol bilgileriyle adlandırabilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="d6bbb-148">Bu, geleneksel bir dosya sisteminde olduğu gibi düzenleme ve geçiş yapabileceğiniz sanal bir dizin yapısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="d6bbb-149">Merhaba dizin yapısını yalnızca sanal - hello yalnızca Blob depolama alanına kullanılabilir kapsayıcılar ve bloblar kaynaklardır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="d6bbb-150">Ancak, hello istemci kitaplığı sunar bir **CloudBlobDirectory** nesne toorefer tooa sanal dizini ve bu şekilde düzenlenen BLOB'ları ile çalışmanın hello işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="d6bbb-151">Örneğin, "" rootphoto1"," 2010/photo1"," 2010/photo2"adlı BLOB'ları ve" 2011/photo1"karşıya neden fotoğrafları" adlı bir kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="d6bbb-152">Bu hello "2010" ve "2011" hello "fotoğrafları" kapsayıcı içindeki sanal dizinler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="d6bbb-153">Çağırdığınızda **listBlobs** hello "fotoğrafları" kapsayıcısı üzerinde döndürülen hello koleksiyonu içerir **CloudBlobDirectory** ve **CloudBlob** hello temsil eden nesneleri dizinleri ve blobları hello en üst düzeyde yer alan.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="d6bbb-154">Bu durumda, fotoğraf "rootphoto1" yanı sıra, dizinler "2010" ve "2011" döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="d6bbb-155">Merhaba kullanabilirsiniz **instanceof** işleci toodistinguish bu nesneler.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="d6bbb-156">İsteğe bağlı olarak, parametreleri toohello geçirebilirsiniz **listBlobs** hello yöntemiyle **Listblobs** parametresini tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="d6bbb-157">Bu bağımsız olarak dizin döndürülen her blob neden olur.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="d6bbb-158">Daha fazla bilgi için bkz: **CloudBlobContainer.listBlobs** hello içinde [Azure Storage istemci SDK'sı başvurusu].</span><span class="sxs-lookup"><span data-stu-id="d6bbb-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="d6bbb-159">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="d6bbb-159">Download a blob</span></span>
<span data-ttu-id="d6bbb-160">toodownload BLOB'ları hello sipariş tooget bir blob başvurusu bir blob'a yüklemek için yaptığınız gibi aynı adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="d6bbb-161">Örnek karşıya hello hello blob nesnesi üzerinde karşıya yükleme çağrılır.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="d6bbb-162">Aşağıdaki örneğine hello çağrı indirme tootransfer hello blob içeriği tooa stream nesnesi gibi bir **FileOutputStream** toopersist hello blob tooa yerel dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="d6bbb-163">Blob silme</span><span class="sxs-lookup"><span data-stu-id="d6bbb-163">Delete a blob</span></span>
<span data-ttu-id="d6bbb-164">toodelete bir blob alma bir blob başvurusu ve arama **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="d6bbb-165">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="d6bbb-165">Delete a blob container</span></span>
<span data-ttu-id="d6bbb-166">Son olarak, toodelete bir blob kapsayıcısını Al blob kapsayıcı başvurusu ve çağrı **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="d6bbb-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6bbb-167">Next steps</span></span>
<span data-ttu-id="d6bbb-168">Blob storage'nın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bbb-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="d6bbb-169">[Azure depolama için Java SDK'sı][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="d6bbb-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="d6bbb-170">[Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]</span><span class="sxs-lookup"><span data-stu-id="d6bbb-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="d6bbb-171">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="d6bbb-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="d6bbb-172">[Azure depolama ekibi blogu][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="d6bbb-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="d6bbb-173">Daha fazla bilgi için hello Ayrıca bkz. [Java Geliştirici Merkezi](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="d6bbb-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/

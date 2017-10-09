---
title: "aaaEnable ortak okuma erişiminin kapsayıcılar ve bloblar Azure Blob depolamada için | Microsoft Docs"
description: "Bilgi nasıl toomake kapsayıcılar ve bloblar anonim erişim için kullanılabilir ve nasıl tooaccess bunları programlı olarak."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="51071-103">Anonim okuma erişimini toocontainers ve BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="51071-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="51071-104">Anonim, ortak okuma erişimi tooa kapsayıcı ve bloblarını Azure Blob depolamada etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="51071-105">Bunu yaparak, hesap anahtarınızı paylaşımı ve paylaşılan erişim imzası (SAS) gerek olmadan toothese kaynaklarına salt okunur erişim verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="51071-106">Ortak okuma erişimi BLOB'lar tooalways anonim okuma erişimi için kullanılabilir belirli istediğiniz senaryolar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="51071-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="51071-107">Daha ayrıntılı denetim için bir paylaşılan erişim imzası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="51071-108">Paylaşılan erişim imzaları tooprovide sınırlı erişimi belirli bir süre için farklı izinleri kullanarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="51071-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="51071-109">Paylaşılan oluşturma hakkında daha fazla bilgi için erişim imzalar, bkz: [kullanarak paylaşılan erişim imzaları (SAS) Azure storage'da](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51071-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="51071-110">Anonim kullanıcılar izinleri toocontainers ve blobları verin</span><span class="sxs-lookup"><span data-stu-id="51071-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="51071-111">Varsayılan olarak, bir kapsayıcı ve içindeki tüm BLOB'ları yalnızca hello hello depolama hesabının sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="51071-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="51071-112">toogive anonim kullanıcıların Okuma izinleri tooa kapsayıcı ve bloblarını, hello kapsayıcı izinleri tooallow genel erişim ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="51071-113">Anonim kullanıcılar genel olarak erişilebilir bir kapsayıcıdaki blobları hello isteği doğrulanmadan okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="51071-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="51071-114">Bir kapsayıcı aşağıdaki izinleri hello ile yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51071-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="51071-115">**Hiçbir public okuma erişimi:** hello kapsayıcı ve bloblarını yalnızca hello depolama hesabı sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="51071-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="51071-116">Bu, tüm yeni kapsayıcıları için hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="51071-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="51071-117">**Genel erişim için BLOB'ları yalnızca okuma:** hello kapsayıcıdaki Blobları anonim istek tarafından okunabilir ancak kapsayıcı verileri kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="51071-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="51071-118">Anonim istemcileri hello BLOB'lar hello kapsayıcıdaki numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="51071-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="51071-119">**Tam herkese okuma erişimi:** tüm kapsayıcı ve blob verilerini anonim istek tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="51071-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="51071-120">İstemcileri hello kapsayıcıdaki blobları anonim istek göre sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="51071-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="51071-121">Aşağıdaki tooset kapsayıcı izinleri hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51071-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="51071-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="51071-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="51071-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51071-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="51071-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51071-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="51071-125">Program aracılığıyla, bir hello depolama istemcisi kitaplıklarını veya hello REST API kullanarak</span><span class="sxs-lookup"><span data-stu-id="51071-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="51071-126">Hello Azure portal'ın kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="51071-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="51071-127">Merhaba tooset kapsayıcı izinleri [Azure portal](https://portal.azure.com), şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="51071-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="51071-128">Açık, **depolama hesabı** dikey penceresinde hello portal.</span><span class="sxs-lookup"><span data-stu-id="51071-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="51071-129">Depolama hesabınızı seçerek bulabileceğiniz **depolama hesapları** hello ana portal menü dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="51071-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="51071-130">Altında **BLOB hizmeti** hello menü dikey penceresinde, seçin **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="51071-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="51071-131">Merhaba kapsayıcı satır veya select hello üç nokta tooopen hello kapsayıcının sağ **bağlam menüsü**.</span><span class="sxs-lookup"><span data-stu-id="51071-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="51071-132">Seçin **erişim ilkesi** hello bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="51071-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="51071-133">Seçin bir **erişim türüne** hello açılan menüsünde.</span><span class="sxs-lookup"><span data-stu-id="51071-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Kapsayıcı meta verileri iletişim Düzenle](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="51071-135">.NET ile kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="51071-135">Set container permissions with .NET</span></span>
<span data-ttu-id="51071-136">.NET için C# ve hello depolama istemci kitaplığı kullanarak bir kapsayıcı tooset izinlerini tarafından arama hello ilk hello kapsayıcının var olan izinleri almak **GetPermissions** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="51071-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="51071-137">Ardından kümesi hello **PublicAccess** özelliği hello için **BlobContainerPermissions** hello tarafından döndürülen nesne **GetPermissions** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="51071-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="51071-138">Son olarak, hello çağrısı **izinleri ayarla** hello yöntemiyle izinleri güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="51071-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="51071-139">Aşağıdaki örnek hello toofull herkese okuma erişimi hello kapsayıcının izinleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="51071-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="51071-140">BLOB'ları yalnızca hello ayarlamak için tooset izinleri toopublic okuma erişiminin **PublicAccess** özelliği çok**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="51071-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="51071-141">Anonim kullanıcılar için tüm izinleri tooremove ayarlama özelliği çok hello**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="51071-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="51071-142">Kapsayıcılar ve bloblar anonim erişim</span><span class="sxs-lookup"><span data-stu-id="51071-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="51071-143">Kapsayıcılar ve bloblar anonim olarak erişen istemci kimlik bilgileri gerektirmeyecek oluşturucular kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="51071-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="51071-144">Örnek hello birkaç farklı şekilde tooreference Blob hizmeti kaynakları anonim olarak göster.</span><span class="sxs-lookup"><span data-stu-id="51071-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="51071-145">Anonim istemci nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="51071-145">Create an anonymous client object</span></span>
<span data-ttu-id="51071-146">Merhaba hesabı için hello Blob Hizmeti uç noktası sağlayarak anonim erişim için yeni bir hizmet istemci nesnesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="51071-147">Ancak, bu hesaptaki anonim erişim için kullanılabilir bir kapsayıcı hello adını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51071-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="51071-148">Anonim olarak bir kapsayıcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="51071-148">Reference a container anonymously</span></span>
<span data-ttu-id="51071-149">Anonim olarak kullanılabilir hello URL tooa kapsayıcı varsa tooreference hello kapsayıcı doğrudan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51071-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="51071-150">Anonim olarak bir blob başvurusu</span><span class="sxs-lookup"><span data-stu-id="51071-150">Reference a blob anonymously</span></span>
<span data-ttu-id="51071-151">Anonim erişim için kullanılabilir hello URL tooa blob varsa, bu URL'yi kullanarak doğrudan hello blob başvurusu yapabilir:</span><span class="sxs-lookup"><span data-stu-id="51071-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="51071-152">Özellikler kullanılabilir tooanonymous kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="51071-152">Features available tooanonymous users</span></span>
<span data-ttu-id="51071-153">Aşağıdaki tablonun hello bir kapsayıcının ACL tooallow genel erişim ayarladığınızda, anonim kullanıcılar tarafından hangi işlemleri çağrılabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="51071-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="51071-154">REST işlemi</span><span class="sxs-lookup"><span data-stu-id="51071-154">REST Operation</span></span> | <span data-ttu-id="51071-155">Tam ortak okuma erişimi izni</span><span class="sxs-lookup"><span data-stu-id="51071-155">Permission with full public read access</span></span> | <span data-ttu-id="51071-156">Yalnızca BLOB'lar için herkese okuma erişimi izniyle</span><span class="sxs-lookup"><span data-stu-id="51071-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51071-157">Liste kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="51071-157">List Containers</span></span> |<span data-ttu-id="51071-158">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-158">Owner only</span></span> |<span data-ttu-id="51071-159">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-159">Owner only</span></span> |
| <span data-ttu-id="51071-160">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51071-160">Create Container</span></span> |<span data-ttu-id="51071-161">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-161">Owner only</span></span> |<span data-ttu-id="51071-162">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-162">Owner only</span></span> |
| <span data-ttu-id="51071-163">Kapsayıcı özellikleri Al</span><span class="sxs-lookup"><span data-stu-id="51071-163">Get Container Properties</span></span> |<span data-ttu-id="51071-164">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-164">All</span></span> |<span data-ttu-id="51071-165">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-165">Owner only</span></span> |
| <span data-ttu-id="51071-166">Kapsayıcı meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="51071-166">Get Container Metadata</span></span> |<span data-ttu-id="51071-167">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-167">All</span></span> |<span data-ttu-id="51071-168">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-168">Owner only</span></span> |
| <span data-ttu-id="51071-169">Kapsayıcı meta verileri ayarlama</span><span class="sxs-lookup"><span data-stu-id="51071-169">Set Container Metadata</span></span> |<span data-ttu-id="51071-170">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-170">Owner only</span></span> |<span data-ttu-id="51071-171">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-171">Owner only</span></span> |
| <span data-ttu-id="51071-172">Kapsayıcı ACL Al</span><span class="sxs-lookup"><span data-stu-id="51071-172">Get Container ACL</span></span> |<span data-ttu-id="51071-173">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-173">Owner only</span></span> |<span data-ttu-id="51071-174">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-174">Owner only</span></span> |
| <span data-ttu-id="51071-175">Kapsayıcı ACL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="51071-175">Set Container ACL</span></span> |<span data-ttu-id="51071-176">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-176">Owner only</span></span> |<span data-ttu-id="51071-177">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-177">Owner only</span></span> |
| <span data-ttu-id="51071-178">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="51071-178">Delete Container</span></span> |<span data-ttu-id="51071-179">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-179">Owner only</span></span> |<span data-ttu-id="51071-180">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-180">Owner only</span></span> |
| <span data-ttu-id="51071-181">Liste BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="51071-181">List Blobs</span></span> |<span data-ttu-id="51071-182">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-182">All</span></span> |<span data-ttu-id="51071-183">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-183">Owner only</span></span> |
| <span data-ttu-id="51071-184">BLOB yerleştirme</span><span class="sxs-lookup"><span data-stu-id="51071-184">Put Blob</span></span> |<span data-ttu-id="51071-185">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-185">Owner only</span></span> |<span data-ttu-id="51071-186">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-186">Owner only</span></span> |
| <span data-ttu-id="51071-187">BLOB alma</span><span class="sxs-lookup"><span data-stu-id="51071-187">Get Blob</span></span> |<span data-ttu-id="51071-188">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-188">All</span></span> |<span data-ttu-id="51071-189">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-189">All</span></span> |
| <span data-ttu-id="51071-190">BLOB özelliklerini alma</span><span class="sxs-lookup"><span data-stu-id="51071-190">Get Blob Properties</span></span> |<span data-ttu-id="51071-191">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-191">All</span></span> |<span data-ttu-id="51071-192">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-192">All</span></span> |
| <span data-ttu-id="51071-193">Blob özelliklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="51071-193">Set Blob Properties</span></span> |<span data-ttu-id="51071-194">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-194">Owner only</span></span> |<span data-ttu-id="51071-195">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-195">Owner only</span></span> |
| <span data-ttu-id="51071-196">BLOB meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="51071-196">Get Blob Metadata</span></span> |<span data-ttu-id="51071-197">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-197">All</span></span> |<span data-ttu-id="51071-198">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-198">All</span></span> |
| <span data-ttu-id="51071-199">BLOB meta verileri ayarlama</span><span class="sxs-lookup"><span data-stu-id="51071-199">Set Blob Metadata</span></span> |<span data-ttu-id="51071-200">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-200">Owner only</span></span> |<span data-ttu-id="51071-201">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-201">Owner only</span></span> |
| <span data-ttu-id="51071-202">Blok yerleştirme</span><span class="sxs-lookup"><span data-stu-id="51071-202">Put Block</span></span> |<span data-ttu-id="51071-203">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-203">Owner only</span></span> |<span data-ttu-id="51071-204">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-204">Owner only</span></span> |
| <span data-ttu-id="51071-205">Engelleme listesi (yalnızca kaydedilmiş engeller) Al</span><span class="sxs-lookup"><span data-stu-id="51071-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="51071-206">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-206">All</span></span> |<span data-ttu-id="51071-207">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-207">All</span></span> |
| <span data-ttu-id="51071-208">Engelleme listesi (yalnızca kaydedilmemiş blokları veya tüm blokları) Al</span><span class="sxs-lookup"><span data-stu-id="51071-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="51071-209">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-209">Owner only</span></span> |<span data-ttu-id="51071-210">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-210">Owner only</span></span> |
| <span data-ttu-id="51071-211">Engelleme listesi yerleştirme</span><span class="sxs-lookup"><span data-stu-id="51071-211">Put Block List</span></span> |<span data-ttu-id="51071-212">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-212">Owner only</span></span> |<span data-ttu-id="51071-213">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-213">Owner only</span></span> |
| <span data-ttu-id="51071-214">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="51071-214">Delete Blob</span></span> |<span data-ttu-id="51071-215">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-215">Owner only</span></span> |<span data-ttu-id="51071-216">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-216">Owner only</span></span> |
| <span data-ttu-id="51071-217">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="51071-217">Copy Blob</span></span> |<span data-ttu-id="51071-218">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-218">Owner only</span></span> |<span data-ttu-id="51071-219">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-219">Owner only</span></span> |
| <span data-ttu-id="51071-220">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="51071-220">Snapshot Blob</span></span> |<span data-ttu-id="51071-221">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-221">Owner only</span></span> |<span data-ttu-id="51071-222">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-222">Owner only</span></span> |
| <span data-ttu-id="51071-223">Kira blob'u</span><span class="sxs-lookup"><span data-stu-id="51071-223">Lease Blob</span></span> |<span data-ttu-id="51071-224">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-224">Owner only</span></span> |<span data-ttu-id="51071-225">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-225">Owner only</span></span> |
| <span data-ttu-id="51071-226">Sayfa yerleştirin</span><span class="sxs-lookup"><span data-stu-id="51071-226">Put Page</span></span> |<span data-ttu-id="51071-227">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-227">Owner only</span></span> |<span data-ttu-id="51071-228">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-228">Owner only</span></span> |
| <span data-ttu-id="51071-229">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="51071-229">Get Page Ranges</span></span> |<span data-ttu-id="51071-230">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-230">All</span></span> |<span data-ttu-id="51071-231">Tümü</span><span class="sxs-lookup"><span data-stu-id="51071-231">All</span></span> |
| <span data-ttu-id="51071-232">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="51071-232">Append Blob</span></span> |<span data-ttu-id="51071-233">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-233">Owner only</span></span> |<span data-ttu-id="51071-234">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="51071-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51071-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51071-235">Next steps</span></span>

* [<span data-ttu-id="51071-236">Hello Azure Storage Hizmetleri için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="51071-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="51071-237">Paylaşılan erişim imzaları (SAS) kullanma</span><span class="sxs-lookup"><span data-stu-id="51071-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="51071-238">Paylaşılan Erişim İmzası ile Erişim için Temsilci Seçme</span><span class="sxs-lookup"><span data-stu-id="51071-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)

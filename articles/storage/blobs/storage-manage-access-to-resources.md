---
title: "Kapsayıcılar ve Azure Blob depolamada BLOB'lar için herkese okuma erişimi etkinleştir | Microsoft Docs"
description: "Kapsayıcılar ve bloblar anonim erişim için nasıl oluşturulacağı ve programlı olarak erişmek nasıl öğrenin."
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
ms.openlocfilehash: 8d4f4c7c208baf0db6155eb78a53e37c4ec1e023
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="070ee-103">Kapsayıcılara ve blob’lara anonim okuma erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="070ee-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="070ee-104">Bir kapsayıcı ve bloblarını Azure Blob depolamada anonim, ortak okuma erişimi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="070ee-105">Bunu yaparak, hesap anahtarınızı paylaşımı ve paylaşılan erişim imzası (SAS) gerek olmadan bu kaynaklara salt okunur erişim verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="070ee-106">Ortak okuma erişimi belirli BLOB'ları her zaman anonim okuma erişimi için kullanılabilir olmasını istediğiniz senaryolar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="070ee-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="070ee-107">Daha ayrıntılı denetim için bir paylaşılan erişim imzası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="070ee-108">Paylaşılan erişim imzalar, belirli bir süre için farklı izinleri kullanarak kısıtlı erişim sağlamak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="070ee-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="070ee-109">Paylaşılan oluşturma hakkında daha fazla bilgi için erişim imzalar, bkz: [kullanarak paylaşılan erişim imzaları (SAS) Azure storage'da](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="070ee-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="070ee-110">Kapsayıcılar ve bloblar için anonim kullanıcı izinleri</span><span class="sxs-lookup"><span data-stu-id="070ee-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="070ee-111">Varsayılan olarak, bir kapsayıcı ve içindeki tüm BLOB'ları yalnızca depolama hesabı sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="070ee-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="070ee-112">Anonim kullanıcılar bir kapsayıcı ve bloblarını için Okuma izinleri vermek için genel erişime izin vermek için kapsayıcı izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="070ee-113">Anonim kullanıcılar istek doğrulanmadan genel olarak erişilebilir bir kapsayıcıdaki blobları okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="070ee-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="070ee-114">Şu izinlere sahip bir kapsayıcı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="070ee-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="070ee-115">**Hiçbir public okuma erişimi:** kapsayıcı ve bloblarını yalnızca depolama hesabı sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="070ee-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="070ee-116">Bu, tüm yeni kapsayıcıları için varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="070ee-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="070ee-117">**Genel erişim için BLOB'ları yalnızca okuma:** kapsayıcıdaki Blobları anonim istek tarafından okunabilir ancak kapsayıcı verileri kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="070ee-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="070ee-118">Anonim istemcileri kapsayıcısı içinde BLOB'ları numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="070ee-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="070ee-119">**Tam herkese okuma erişimi:** tüm kapsayıcı ve blob verilerini anonim istek tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="070ee-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="070ee-120">İstemcileri kapsayıcıdaki blobları anonim istek göre sıralayabilirsiniz, ancak depolama hesabı kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="070ee-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="070ee-121">Kapsayıcı izinlerini ayarlamak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="070ee-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="070ee-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="070ee-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="070ee-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="070ee-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="070ee-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="070ee-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="070ee-125">Program aracılığıyla, depolama istemcisi kitaplıklarını veya REST API'yi birini kullanarak</span><span class="sxs-lookup"><span data-stu-id="070ee-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="070ee-126">Azure portalında kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="070ee-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="070ee-127">Kapsayıcı izinleri ayarlamak için [Azure portal](https://portal.azure.com), şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="070ee-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="070ee-128">Açık, **depolama hesabı** portaldaki dikey pencere.</span><span class="sxs-lookup"><span data-stu-id="070ee-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="070ee-129">Depolama hesabınızı seçerek bulabileceğiniz **depolama hesapları** ana portal menü dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="070ee-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="070ee-130">Altında **BLOB hizmeti** menü dikey penceresinde, seçin **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="070ee-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="070ee-131">Kapsayıcının açmak için üç nokta seçin veya kapsayıcı satırındaki sağ **bağlam menüsü**.</span><span class="sxs-lookup"><span data-stu-id="070ee-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="070ee-132">Seçin **erişim ilkesi** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="070ee-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="070ee-133">Seçin bir **erişim türüne** açılan menüden.</span><span class="sxs-lookup"><span data-stu-id="070ee-133">Select an **Access type** from the drop down menu.</span></span>

    ![Kapsayıcı meta verileri iletişim Düzenle](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="070ee-135">.NET ile kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="070ee-135">Set container permissions with .NET</span></span>
<span data-ttu-id="070ee-136">C# ve depolama istemci kitaplığı için .NET kullanarak bir kapsayıcı izinlerini ayarlamak için ilk kapsayıcının varolan izinlerini çağırarak almaya **GetPermissions** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="070ee-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="070ee-137">Ardından **PublicAccess** özelliği için **BlobContainerPermissions** tarafından döndürülen nesne **GetPermissions** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="070ee-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="070ee-138">Son olarak, arama **izinleri ayarla** güncelleştirilmiş izinlerle yöntemi.</span><span class="sxs-lookup"><span data-stu-id="070ee-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="070ee-139">Aşağıdaki örnek kapsayıcının izinleri için tam ortak okuma erişimi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="070ee-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="070ee-140">Yalnızca BLOB'lar için herkese okuma erişimi izinlerini ayarlamak için ayarlanmış **PublicAccess** özelliğine **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="070ee-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="070ee-141">Özelliğin anonim kullanıcılar için tüm izinleri kaldırmak için kümesine **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="070ee-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="070ee-142">Kapsayıcılar ve bloblar anonim erişim</span><span class="sxs-lookup"><span data-stu-id="070ee-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="070ee-143">Kapsayıcılar ve bloblar anonim olarak erişen istemci kimlik bilgileri gerektirmeyecek oluşturucular kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="070ee-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="070ee-144">Aşağıdaki örnekler Blob hizmeti kaynaklarını anonim olarak başvurmak için birkaç farklı yolu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="070ee-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="070ee-145">Anonim istemci nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="070ee-145">Create an anonymous client object</span></span>
<span data-ttu-id="070ee-146">Hesap için Blob Hizmeti uç noktası sağlayarak anonim erişim için yeni bir hizmet istemci nesnesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="070ee-147">Ancak, bu hesaptaki anonim erişim için kullanılabilir bir kapsayıcının adını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="070ee-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="070ee-148">Anonim olarak bir kapsayıcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="070ee-148">Reference a container anonymously</span></span>
<span data-ttu-id="070ee-149">Anonim olarak kullanılabilir bir kapsayıcı URL'si varsa, kapsayıcı doğrudan başvurmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ee-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="070ee-150">Anonim olarak bir blob başvurusu</span><span class="sxs-lookup"><span data-stu-id="070ee-150">Reference a blob anonymously</span></span>
<span data-ttu-id="070ee-151">Anonim erişim için kullanılabilir bir blob URL'si varsa, bu URL'yi kullanarak doğrudan blob başvurusu yapabilir:</span><span class="sxs-lookup"><span data-stu-id="070ee-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="070ee-152">Anonim kullanıcılar için kullanılabilir özellikler</span><span class="sxs-lookup"><span data-stu-id="070ee-152">Features available to anonymous users</span></span>
<span data-ttu-id="070ee-153">Bir kapsayıcının ACL genel erişime izin verecek şekilde ayarladığınızda, anonim kullanıcılar tarafından hangi işlemleri çağrılabilir aşağıdaki tabloda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="070ee-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="070ee-154">REST işlemi</span><span class="sxs-lookup"><span data-stu-id="070ee-154">REST Operation</span></span> | <span data-ttu-id="070ee-155">Tam ortak okuma erişimi izni</span><span class="sxs-lookup"><span data-stu-id="070ee-155">Permission with full public read access</span></span> | <span data-ttu-id="070ee-156">Yalnızca BLOB'lar için herkese okuma erişimi izniyle</span><span class="sxs-lookup"><span data-stu-id="070ee-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="070ee-157">Liste kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="070ee-157">List Containers</span></span> |<span data-ttu-id="070ee-158">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-158">Owner only</span></span> |<span data-ttu-id="070ee-159">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-159">Owner only</span></span> |
| <span data-ttu-id="070ee-160">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="070ee-160">Create Container</span></span> |<span data-ttu-id="070ee-161">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-161">Owner only</span></span> |<span data-ttu-id="070ee-162">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-162">Owner only</span></span> |
| <span data-ttu-id="070ee-163">Kapsayıcı özellikleri Al</span><span class="sxs-lookup"><span data-stu-id="070ee-163">Get Container Properties</span></span> |<span data-ttu-id="070ee-164">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-164">All</span></span> |<span data-ttu-id="070ee-165">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-165">Owner only</span></span> |
| <span data-ttu-id="070ee-166">Kapsayıcı meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="070ee-166">Get Container Metadata</span></span> |<span data-ttu-id="070ee-167">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-167">All</span></span> |<span data-ttu-id="070ee-168">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-168">Owner only</span></span> |
| <span data-ttu-id="070ee-169">Kapsayıcı meta verileri ayarlama</span><span class="sxs-lookup"><span data-stu-id="070ee-169">Set Container Metadata</span></span> |<span data-ttu-id="070ee-170">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-170">Owner only</span></span> |<span data-ttu-id="070ee-171">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-171">Owner only</span></span> |
| <span data-ttu-id="070ee-172">Kapsayıcı ACL Al</span><span class="sxs-lookup"><span data-stu-id="070ee-172">Get Container ACL</span></span> |<span data-ttu-id="070ee-173">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-173">Owner only</span></span> |<span data-ttu-id="070ee-174">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-174">Owner only</span></span> |
| <span data-ttu-id="070ee-175">Kapsayıcı ACL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="070ee-175">Set Container ACL</span></span> |<span data-ttu-id="070ee-176">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-176">Owner only</span></span> |<span data-ttu-id="070ee-177">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-177">Owner only</span></span> |
| <span data-ttu-id="070ee-178">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="070ee-178">Delete Container</span></span> |<span data-ttu-id="070ee-179">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-179">Owner only</span></span> |<span data-ttu-id="070ee-180">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-180">Owner only</span></span> |
| <span data-ttu-id="070ee-181">Liste BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="070ee-181">List Blobs</span></span> |<span data-ttu-id="070ee-182">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-182">All</span></span> |<span data-ttu-id="070ee-183">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-183">Owner only</span></span> |
| <span data-ttu-id="070ee-184">BLOB yerleştirme</span><span class="sxs-lookup"><span data-stu-id="070ee-184">Put Blob</span></span> |<span data-ttu-id="070ee-185">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-185">Owner only</span></span> |<span data-ttu-id="070ee-186">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-186">Owner only</span></span> |
| <span data-ttu-id="070ee-187">BLOB alma</span><span class="sxs-lookup"><span data-stu-id="070ee-187">Get Blob</span></span> |<span data-ttu-id="070ee-188">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-188">All</span></span> |<span data-ttu-id="070ee-189">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-189">All</span></span> |
| <span data-ttu-id="070ee-190">BLOB özelliklerini alma</span><span class="sxs-lookup"><span data-stu-id="070ee-190">Get Blob Properties</span></span> |<span data-ttu-id="070ee-191">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-191">All</span></span> |<span data-ttu-id="070ee-192">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-192">All</span></span> |
| <span data-ttu-id="070ee-193">Blob özelliklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="070ee-193">Set Blob Properties</span></span> |<span data-ttu-id="070ee-194">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-194">Owner only</span></span> |<span data-ttu-id="070ee-195">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-195">Owner only</span></span> |
| <span data-ttu-id="070ee-196">BLOB meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="070ee-196">Get Blob Metadata</span></span> |<span data-ttu-id="070ee-197">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-197">All</span></span> |<span data-ttu-id="070ee-198">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-198">All</span></span> |
| <span data-ttu-id="070ee-199">BLOB meta verileri ayarlama</span><span class="sxs-lookup"><span data-stu-id="070ee-199">Set Blob Metadata</span></span> |<span data-ttu-id="070ee-200">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-200">Owner only</span></span> |<span data-ttu-id="070ee-201">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-201">Owner only</span></span> |
| <span data-ttu-id="070ee-202">Blok yerleştirme</span><span class="sxs-lookup"><span data-stu-id="070ee-202">Put Block</span></span> |<span data-ttu-id="070ee-203">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-203">Owner only</span></span> |<span data-ttu-id="070ee-204">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-204">Owner only</span></span> |
| <span data-ttu-id="070ee-205">Engelleme listesi (yalnızca kaydedilmiş engeller) Al</span><span class="sxs-lookup"><span data-stu-id="070ee-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="070ee-206">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-206">All</span></span> |<span data-ttu-id="070ee-207">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-207">All</span></span> |
| <span data-ttu-id="070ee-208">Engelleme listesi (yalnızca kaydedilmemiş blokları veya tüm blokları) Al</span><span class="sxs-lookup"><span data-stu-id="070ee-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="070ee-209">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-209">Owner only</span></span> |<span data-ttu-id="070ee-210">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-210">Owner only</span></span> |
| <span data-ttu-id="070ee-211">Engelleme listesi yerleştirme</span><span class="sxs-lookup"><span data-stu-id="070ee-211">Put Block List</span></span> |<span data-ttu-id="070ee-212">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-212">Owner only</span></span> |<span data-ttu-id="070ee-213">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-213">Owner only</span></span> |
| <span data-ttu-id="070ee-214">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="070ee-214">Delete Blob</span></span> |<span data-ttu-id="070ee-215">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-215">Owner only</span></span> |<span data-ttu-id="070ee-216">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-216">Owner only</span></span> |
| <span data-ttu-id="070ee-217">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="070ee-217">Copy Blob</span></span> |<span data-ttu-id="070ee-218">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-218">Owner only</span></span> |<span data-ttu-id="070ee-219">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-219">Owner only</span></span> |
| <span data-ttu-id="070ee-220">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="070ee-220">Snapshot Blob</span></span> |<span data-ttu-id="070ee-221">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-221">Owner only</span></span> |<span data-ttu-id="070ee-222">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-222">Owner only</span></span> |
| <span data-ttu-id="070ee-223">Kira blob'u</span><span class="sxs-lookup"><span data-stu-id="070ee-223">Lease Blob</span></span> |<span data-ttu-id="070ee-224">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-224">Owner only</span></span> |<span data-ttu-id="070ee-225">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-225">Owner only</span></span> |
| <span data-ttu-id="070ee-226">Sayfa yerleştirin</span><span class="sxs-lookup"><span data-stu-id="070ee-226">Put Page</span></span> |<span data-ttu-id="070ee-227">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-227">Owner only</span></span> |<span data-ttu-id="070ee-228">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-228">Owner only</span></span> |
| <span data-ttu-id="070ee-229">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="070ee-229">Get Page Ranges</span></span> |<span data-ttu-id="070ee-230">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-230">All</span></span> |<span data-ttu-id="070ee-231">Tümü</span><span class="sxs-lookup"><span data-stu-id="070ee-231">All</span></span> |
| <span data-ttu-id="070ee-232">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="070ee-232">Append Blob</span></span> |<span data-ttu-id="070ee-233">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-233">Owner only</span></span> |<span data-ttu-id="070ee-234">Yalnızca sahibi</span><span class="sxs-lookup"><span data-stu-id="070ee-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="070ee-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="070ee-235">Next steps</span></span>

* [<span data-ttu-id="070ee-236">Azure Storage Hizmetleri için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="070ee-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="070ee-237">Paylaşılan erişim imzaları (SAS) kullanma</span><span class="sxs-lookup"><span data-stu-id="070ee-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="070ee-238">Paylaşılan Erişim İmzası ile Erişim için Temsilci Seçme</span><span class="sxs-lookup"><span data-stu-id="070ee-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)

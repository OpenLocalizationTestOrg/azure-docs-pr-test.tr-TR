---
title: "Azure Storage'da bir BLOB salt okunur anlık görüntü oluşturma | Microsoft Docs"
description: "Zaman içinde belirli bir anda blob verileri yedeklemek için bir blobun bir anlık görüntü oluşturmayı öğrenin. Anlık görüntüler nasıl faturalandırılır ve bunların kapasite ücretleri en aza indirmek için nasıl kullanılacağını anlayın."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 6ebb77f4ec5f1887e5c55bf1c8c64224a9233654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="28dc4-104">Blob anlık görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="28dc4-104">Create a blob snapshot</span></span>

<span data-ttu-id="28dc4-105">Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="28dc4-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="28dc4-106">Anlık görüntüler, BLOB'ları yedekleme için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="28dc4-107">Bir anlık görüntü oluşturduktan sonra okuma, kopyalama veya silin, ancak değişiklik yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="28dc4-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="28dc4-108">Blob URI'si olan bir anlık görüntü bir BLOB kendi temel blob için aynıdır bir **DateTime** anlık görüntünün alındığı zaman belirtmek için URI blob eklenmiş değeri.</span><span class="sxs-lookup"><span data-stu-id="28dc4-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="28dc4-109">Örneğin, URI bir sayfa blob ise `http://storagesample.core.blob.windows.net/mydrives/myvhd`, URI benzer anlık görüntü `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="28dc4-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="28dc4-110">Tüm anlık görüntüleri temel blob'un URI paylaşır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="28dc4-111">Temel blob ve anlık görüntü arasındaki tek fark eklenmiş olan **DateTime** değeri.</span><span class="sxs-lookup"><span data-stu-id="28dc4-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="28dc4-112">Bir blob herhangi bir sayıda anlık görüntü olabilir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="28dc4-113">Açıkça silinene kadar anlık görüntüleri kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="28dc4-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="28dc4-114">Bir anlık görüntü, temel blob outlive olamaz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="28dc4-115">Geçerli anlık izlemek için temel blob ile ilişkili anlık görüntüleri sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="28dc4-116">Bir blob görüntüsünü oluşturduğunuzda, blob'un Sistem özellikleri aynı değerleri anlık görüntü kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="28dc4-117">Oluşturduğunuzda anlık görüntü için ayrı meta verileri belirtmediğiniz sürece temel blob'un meta veriler ayrıca anlık görüntüye kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="28dc4-118">Temel blob ile ilişkili kiraları anlık görüntü etkilemez.</span><span class="sxs-lookup"><span data-stu-id="28dc4-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="28dc4-119">Bir anlık görüntü üzerinde bir kira edinemez.</span><span class="sxs-lookup"><span data-stu-id="28dc4-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="28dc4-120">Bir VHD dosyasının VM diskinin durumu ve geçerli bilgi depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="28dc4-121">VM dahilinde bir diski kullanımdan çıkarın veya VM kapatma ve sonra VHD dosyasını bir anlık görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="28dc4-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="28dc4-122">Daha sonra zamandaki o noktada VHD dosyasını alın ve VM yeniden oluşturmak için bu anlık görüntü dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="28dc4-123">Depolama hizmeti şifreleme (SSE) blob bulunduğu için depolama hesabına etkinleştirilmişse bu blob geçen tüm anlık görüntüleri bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="28dc4-124">Bir anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="28dc4-124">Create a snapshot</span></span>
<span data-ttu-id="28dc4-125">Aşağıdaki kod örneği kullanarak bir anlık görüntü oluşturmak gösterilmiştir [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="28dc4-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="28dc4-126">Oluşturulduğunda bu örnek anlık görüntü için ek meta veri belirtir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="28dc4-127">Anlık görüntü kopyalama</span><span class="sxs-lookup"><span data-stu-id="28dc4-127">Copy snapshots</span></span>
<span data-ttu-id="28dc4-128">BLOB'ları ve anlık görüntüleri içeren kopyalama işlemleri bu kurallar izleyin:</span><span class="sxs-lookup"><span data-stu-id="28dc4-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="28dc4-129">Bir anlık görüntü, temel blob kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="28dc4-130">Anlık görüntü temel blob konumuna yükselterek bir blob önceki bir sürümünü geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="28dc4-131">Anlık görüntü kalır, ancak temel blob üzerine yazılabilir bir anlık görüntü kopyası ile yazılır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="28dc4-132">Hedef blob farklı ada sahip bir anlık görüntü kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="28dc4-133">Sonuçta elde edilen hedef blob yazılabilir bir blob ve anlık görüntü olmayan ' dir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="28dc4-134">Kaynak blob kopyalandığında, tüm anlık görüntüleri kaynak BLOB hedefe kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="28dc4-135">Hedef blob bir kopya ile yazılır, özgün hedef blob ile ilişkili tüm anlık görüntüleri değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="28dc4-136">Bir blok blobu görüntüsünü oluşturduğunuzda, blob'un taahhüt engelleme listesi da anlık görüntüye kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="28dc4-137">Herhangi bir kaydedilmeyen bloğu kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="28dc4-138">Bir erişim koşulu belirtin</span><span class="sxs-lookup"><span data-stu-id="28dc4-138">Specify an access condition</span></span>
<span data-ttu-id="28dc4-139">Çağırdığınızda [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], böylece yalnızca bir koşul karşılandığında anlık görüntü oluşturulduğunda bir erişim koşulu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="28dc4-140">Bir erişim koşulu belirtmek için kullanın [AccessCondition] [ dotnet_AccessCondition] parametresi.</span><span class="sxs-lookup"><span data-stu-id="28dc4-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="28dc4-141">Belirtilen koşulu karşılanmadı, anlık görüntü oluşturulmadı ve Blob hizmeti durum kodunu döndüren [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="28dc4-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="28dc4-142">Anlık görüntüleri silin</span><span class="sxs-lookup"><span data-stu-id="28dc4-142">Delete snapshots</span></span>
<span data-ttu-id="28dc4-143">Anlık görüntüler aynı zamanda silinene kadar anlık görüntüleri içeren bir blobu silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="28dc4-144">Tek tek bir anlık görüntüyü silmek ya da kaynak blob silindiğinde tüm anlık görüntülerin silinmesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="28dc4-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="28dc4-145">Hala anlık görüntülere sahip bir blobu silmek çalışırsanız, bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="28dc4-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="28dc4-146">Aşağıdaki kod örneği, bir blob ve .NET, kendi anlık görüntüleri silmek gösterilmiştir nerede `blockBlob` türünde bir nesne [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="28dc4-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="28dc4-147">Azure Premium Storage ile anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="28dc4-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="28dc4-148">Anlık görüntü Premium Storage ile kullanırken, aşağıdaki kurallar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="28dc4-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="28dc4-149">Maksimum sayıda anlık görüntü premium depolama hesabındaki bir sayfa blobu başına 100'dür.</span><span class="sxs-lookup"><span data-stu-id="28dc4-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="28dc4-150">Bu sınır aşılırsa, anlık görüntü Blob işlem hata kodu 409 döndürür (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="28dc4-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="28dc4-151">Premium depolama hesabı her 10 dakikada bir sayfa blob'u görüntüsünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="28dc4-152">Hızı aşılırsa, anlık görüntü Blob işlem hata kodu 409 döndürür (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="28dc4-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="28dc4-153">Bir anlık görüntü okumak için başka bir sayfa blobu hesabındaki bir anlık görüntü kopyalamak için Kopyala Blob işlemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="28dc4-154">Kopyalama işleminin hedef blob mevcut tüm anlık görüntüleri olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="28dc4-155">Hedef blob anlık görüntüleri sahip sonra Blob kopyalama işlemi hata kodunu 409 döndürür (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="28dc4-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="28dc4-156">Bir anlık görüntü mutlak URI dön</span><span class="sxs-lookup"><span data-stu-id="28dc4-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="28dc4-157">Bu C# kod örneği, bir anlık görüntü oluşturur ve birincil konumu için mutlak URI çıkışı yazar.</span><span class="sxs-lookup"><span data-stu-id="28dc4-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="28dc4-158">Nasıl anlık görüntüleri ücretler tahakkuk anlama</span><span class="sxs-lookup"><span data-stu-id="28dc4-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="28dc4-159">Bir blob salt okunur bir kopyası olan, bir anlık görüntü oluşturma hesabınıza ek veri depolama ücretlere neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="28dc4-160">Uygulamanızı tasarlarken, böylece maliyetleri en aza indirebilirsiniz nasıl bu ücretler tahakkuk haberdar olmanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="28dc4-161">Fatura ile ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="28dc4-161">Important billing considerations</span></span>
<span data-ttu-id="28dc4-162">Aşağıdaki listede, bir anlık görüntü oluştururken dikkate alınması gereken önemli noktaları içerir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="28dc4-163">Blob veya anlık görüntü olup depolama hesabınızın benzersiz blokları veya sayfalar için ücret doğurur.</span><span class="sxs-lookup"><span data-stu-id="28dc4-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="28dc4-164">Hesabınız, bunlar temel alır blob güncelleştirilene kadar blob ile ilişkili anlık görüntüler için ek ücretler uygulanır değil.</span><span class="sxs-lookup"><span data-stu-id="28dc4-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="28dc4-165">Temel blob güncelleştirdikten sonra anlık görüntülerden kareninkinden.</span><span class="sxs-lookup"><span data-stu-id="28dc4-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="28dc4-166">Bu gerçekleştiğinde, benzersiz blokları veya her bir blob veya anlık görüntü sayfalarında için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="28dc4-167">Bir blok blobu blokta değiştirdiğinizde, bu blok sonradan benzersiz bloğu olarak ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="28dc4-168">Anlık görüntüdeki olduğu gibi blok aynı blok Kimliğini ve aynı verilere sahip olsa bile bu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="28dc4-169">Blok kaydedildikten sonra yine, kendisine karşılık gelen hiçbir anlık görüntüdeki gelen kareninkinden ve verileri için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="28dc4-170">Aynı aynı verilerle güncelleştirilir bir sayfa blob'u içinde bir sayfa için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="28dc4-171">Bir blok blobu çağırarak değiştirme [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] yöntemi blob tüm bloklarında değiştirir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="28dc4-172">Bu blob ile ilişkili bir anlık görüntü varsa, tüm blokların anlık görüntü ve temel blob şimdi ayırmak ve hem BLOB'ları tüm bloklarında için ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="28dc4-173">Temel blob ve anlık görüntü verileri aynı kalır olsa bile bu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="28dc4-174">Azure Blob hizmetine iki blokları özdeş veriler içeren olup olmadığını belirlemek için bir yol yok.</span><span class="sxs-lookup"><span data-stu-id="28dc4-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="28dc4-175">Aynı veri ve aynı blok kimliğe sahip olsa bile karşıya ve kaydedilen her bloğu benzersiz olarak kabul edilir</span><span class="sxs-lookup"><span data-stu-id="28dc4-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="28dc4-176">Benzersiz blokları için Ücret tahakkuk olduğundan, ek benzersiz blokları ve ek ücretlere anlık görüntü sonuçlarında sahip bir blob güncelleştirme dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="28dc4-177">Anlık Görüntü Yönetimi ile maliyeti en aza indir</span><span class="sxs-lookup"><span data-stu-id="28dc4-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="28dc4-178">Dikkatli bir şekilde ek ücretlerden kaçınmak için anlık görüntüleri yönetme öneririz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="28dc4-179">Anlık görüntü Depolama tarafından maliyetleri en aza indirmek için bu en iyi uygulamaları takip edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="28dc4-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="28dc4-180">Silin ve blob güncelleştirdiğinizde Uygulama tasarımınız anlık görüntüleri tutmak gerektirmedikçe aynı verilerle güncelleştirdiğiniz olsa bile bir blob ile ilişkili anlık görüntüleri yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="28dc4-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="28dc4-181">Silme ve blob'un anlık görüntü yeniden oluşturma, anlık görüntüler ve blob değil ayırmak emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28dc4-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="28dc4-182">Bir blob için anlık görüntü bakımı, arama kaçının. [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] blob güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="28dc4-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="28dc4-183">Bu yöntemler tüm temel blob ve önemli ölçüde ayırmak için anlık görüntüleri neden blob bloklarında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="28dc4-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="28dc4-184">Bunun yerine, bloğu en az olası sayısı kullanarak güncelleştirme [PutBlock] [ dotnet_PutBlock] ve [PutBlockList] [ dotnet_PutBlockList] yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="28dc4-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="28dc4-185">Anlık görüntü senaryoları faturalama</span><span class="sxs-lookup"><span data-stu-id="28dc4-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="28dc4-186">Bir blok blobu ve onun anlık görüntüleri için nasıl ücretler tahakkuk aşağıdaki senaryolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="28dc4-187">**Senaryo 1**</span><span class="sxs-lookup"><span data-stu-id="28dc4-187">**Scenario 1**</span></span>

<span data-ttu-id="28dc4-188">Anlık görüntü alındıktan sonra yalnızca benzersiz blokları için 1, 2 ve 3 ücretler tahakkuk eden şekilde Senaryo 1'de, temel blob güncelleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="28dc4-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="28dc4-190">**Senaryo 2**</span><span class="sxs-lookup"><span data-stu-id="28dc4-190">**Scenario 2**</span></span>

<span data-ttu-id="28dc4-191">2. senaryo, temel blob güncelleştirildi ancak anlık görüntüye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="28dc4-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="28dc4-192">Blok 3 güncelleştirildi ve aynı veri ve aynı kimliği içeriyor olsa bile, onu anlık görüntüdeki 3 engelleme aynı değil.</span><span class="sxs-lookup"><span data-stu-id="28dc4-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="28dc4-193">Sonuç olarak, hesap için dört blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="28dc4-193">As a result, the account is charged for four blocks.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="28dc4-195">**Senaryo 3**</span><span class="sxs-lookup"><span data-stu-id="28dc4-195">**Scenario 3**</span></span>

<span data-ttu-id="28dc4-196">Senaryo 3, temel blob güncelleştirildi ancak anlık görüntüye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="28dc4-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="28dc4-197">Blok 3 temel blob 4 bloğunda ile değiştirildi, ancak anlık görüntü hala Blok 3 yansıtır.</span><span class="sxs-lookup"><span data-stu-id="28dc4-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="28dc4-198">Sonuç olarak, hesap için dört blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="28dc4-198">As a result, the account is charged for four blocks.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="28dc4-200">**Senaryo 4**</span><span class="sxs-lookup"><span data-stu-id="28dc4-200">**Scenario 4**</span></span>

<span data-ttu-id="28dc4-201">Senaryo 4, temel blob tamamen güncelleştirildi ve kendi özgün blokları hiçbiri içerir.</span><span class="sxs-lookup"><span data-stu-id="28dc4-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="28dc4-202">Sonuç olarak, hesap için tüm sekiz benzersiz blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="28dc4-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="28dc4-203">Bir güncelleştirme yöntemi gibi kullanıyorsanız, bu senaryo ortaya çıkabilir [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray][dotnet_UploadFromByteArray], bu yöntemler tüm blob içeriğinin değiştirin.</span><span class="sxs-lookup"><span data-stu-id="28dc4-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="28dc4-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="28dc4-205">Next steps</span></span>

* <span data-ttu-id="28dc4-206">Sanal makine (VM) disk anlık görüntüleri ile çalışma hakkında daha fazla bilgi bulabilirsiniz [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="28dc4-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="28dc4-207">BLOB storage kullanarak ek kod örnekleri için bkz: [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="28dc4-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="28dc4-208">Örnek uygulamayı indirin ve çalıştırın veya github'daki kod göz atın.</span><span class="sxs-lookup"><span data-stu-id="28dc4-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx
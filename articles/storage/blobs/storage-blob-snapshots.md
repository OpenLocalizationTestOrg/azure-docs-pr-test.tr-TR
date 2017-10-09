---
title: "aaaCreate salt okunur anlık görüntüyü Azure storage'da bir BLOB | Microsoft Docs"
description: "Bilgi nasıl toocreate anlık görüntüsünü blob verilerini zaman içinde belirli bir anda bir blob tooback. Anlık görüntüler faturalandırılır nasıl ve ne anlama toouse bunları toominimize kapasite giderler."
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
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="0d372-104">Blob anlık görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d372-104">Create a blob snapshot</span></span>

<span data-ttu-id="0d372-105">Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="0d372-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="0d372-106">Anlık görüntüler, BLOB'ları yedekleme için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="0d372-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="0d372-107">Bir anlık görüntü oluşturduktan sonra okuma, kopyalama veya silin, ancak değişiklik yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0d372-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="0d372-108">Aynı tooits temel blobu blob anlık görüntüsüdür, o hello blob dışında bir URI'ya sahip bir **DateTime** değeri toohello blob URI'si tooindicate hello zaman hangi Merhaba anlık görüntü alındığı eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="0d372-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="0d372-109">Örneğin, URI bir sayfa blob ise `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello anlık görüntü URI benzer çok`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="0d372-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="0d372-110">Tüm anlık görüntüleri hello temel blob'un URI paylaşır.</span><span class="sxs-lookup"><span data-stu-id="0d372-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="0d372-111">Merhaba temel blob ve hello anlık görüntü arasında ayrım eklenmiş hello yalnızca hello **DateTime** değeri.</span><span class="sxs-lookup"><span data-stu-id="0d372-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="0d372-112">Bir blob herhangi bir sayıda anlık görüntü olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d372-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="0d372-113">Açıkça silinene kadar anlık görüntüleri kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d372-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="0d372-114">Bir anlık görüntü, temel blob outlive olamaz.</span><span class="sxs-lookup"><span data-stu-id="0d372-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="0d372-115">Merhaba temel blob tootrack ile ilişkili hello anlık görüntüleri listeleme, geçerli anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0d372-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="0d372-116">Bir blob görüntüsünü oluşturduğunuzda, blob'un Sistem özellikleri hello hello kopyalanan toohello anlık görüntü aynı değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="0d372-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="0d372-117">Merhaba oluşturduğunuzda anlık görüntü için ayrı meta verileri belirtmediğiniz sürece hello temel blob'un meta verileri de anlık görüntü, kopyalanan toohello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0d372-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="0d372-118">Merhaba temel blob ile ilişkili kiraları hello anlık görüntü etkilemez.</span><span class="sxs-lookup"><span data-stu-id="0d372-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="0d372-119">Bir anlık görüntü üzerinde bir kira edinemez.</span><span class="sxs-lookup"><span data-stu-id="0d372-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="0d372-120">Bir VHD kullanılan toostore hello geçerli bilgilerini ve VM diskinin durumu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="0d372-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="0d372-121">Merhaba VM bir diski kullanımdan çıkarın veya VM hello kapatın ve sonra VHD dosyasını bir anlık görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="0d372-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="0d372-122">Bu anlık görüntü dosyasını kullanabilirsiniz sonraki tooretrieve hello VHD dosya zamandaki o noktada ve hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d372-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="0d372-123">Merhaba depolama hesabı için depolama hizmeti şifreleme (SSE) etkinse, hangi hello blob bulunduğu, ardından o blob gerçekleştirilecek tüm anlık görüntüleri bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="0d372-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="0d372-124">Bir anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d372-124">Create a snapshot</span></span>
<span data-ttu-id="0d372-125">Merhaba aşağıdaki kod örneğinde nasıl toocreate kullanarak bir anlık görüntü hello gösterilmektedir [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="0d372-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="0d372-126">Bu örnek, oluşturulduğunda hello anlık görüntü için ek meta veri belirtir.</span><span class="sxs-lookup"><span data-stu-id="0d372-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="0d372-127">Anlık görüntü kopyalama</span><span class="sxs-lookup"><span data-stu-id="0d372-127">Copy snapshots</span></span>
<span data-ttu-id="0d372-128">BLOB'ları ve anlık görüntüleri içeren kopyalama işlemleri bu kurallar izleyin:</span><span class="sxs-lookup"><span data-stu-id="0d372-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="0d372-129">Bir anlık görüntü, temel blob kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="0d372-130">Anlık görüntü toohello konumunu hello temel blob yükselterek bir blob önceki bir sürümünü geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="0d372-131">Merhaba anlık görüntü olarak kalır, ancak hello temel blob hello anlık görüntü yazılabilir bir kopyasını üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="0d372-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="0d372-132">Bir anlık görüntü tooa hedef blob farklı bir adla kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="0d372-133">Merhaba elde edilen hedef blob yazılabilir bir blob ve anlık görüntü değil ' dir.</span><span class="sxs-lookup"><span data-stu-id="0d372-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="0d372-134">Kaynak blob kopyalandığında, tüm anlık görüntüleri hello kaynak BLOB kopyalanan toohello hedef olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="0d372-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="0d372-135">Hedef blob bir kopya ile yazılır, hello özgün hedef blob ile ilişkili tüm anlık görüntüleri değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="0d372-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="0d372-136">Bir blok blobu görüntüsünü oluşturduğunuzda, hello blob'un taahhüt engelleme listesine de kopyalanan toohello anlık görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="0d372-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="0d372-137">Herhangi bir kaydedilmeyen bloğu kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="0d372-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="0d372-138">Bir erişim koşulu belirtin</span><span class="sxs-lookup"><span data-stu-id="0d372-138">Specify an access condition</span></span>
<span data-ttu-id="0d372-139">Çağırdığınızda [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], böylece yalnızca bir koşul karşılandığında hello anlık görüntü oluşturulduğunda bir erişim koşulu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="0d372-140">toospecify erişim koşulu kullanmak hello [AccessCondition] [ dotnet_AccessCondition] parametresi.</span><span class="sxs-lookup"><span data-stu-id="0d372-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="0d372-141">Merhaba koşulu karşılanmadı, hello anlık görüntü oluşturulmadı ve hello Blob hizmeti durum kodu döndürdüğünde belirtilmişse [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="0d372-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="0d372-142">Anlık görüntüleri silin</span><span class="sxs-lookup"><span data-stu-id="0d372-142">Delete snapshots</span></span>
<span data-ttu-id="0d372-143">Merhaba anlık görüntüleri de silinene kadar anlık görüntüleri içeren bir blobu silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="0d372-144">Tek tek bir anlık görüntüyü silmek veya hello kaynak blob silindiğinde tüm anlık görüntülerin silinmesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="0d372-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="0d372-145">Toodelete hala anlık görüntülere sahip bir blob denediğinizde bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="0d372-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="0d372-146">Kod örnekteki nasıl aşağıdaki hello toodelete bir blob ve .NET, kendi anlık görüntülerini nerede `blockBlob` türünde bir nesne [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="0d372-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="0d372-147">Azure Premium Storage ile anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="0d372-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="0d372-148">Premium depolama ile anlık görüntülerini kullanarak kurallar aşağıdaki hello uygulayın:</span><span class="sxs-lookup"><span data-stu-id="0d372-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="0d372-149">Merhaba Maksimum sayıda anlık görüntü premium depolama hesabındaki bir sayfa blobu başına 100'dür.</span><span class="sxs-lookup"><span data-stu-id="0d372-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="0d372-150">Bu sınır aşılırsa, hata kodu 409 hello anlık görüntü Blob işlemi döndürür (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="0d372-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="0d372-151">Premium depolama hesabı her 10 dakikada bir sayfa blob'u görüntüsünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="0d372-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="0d372-152">Hızı aşılırsa, hata kodu 409 hello anlık görüntü Blob işlemi döndürür (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="0d372-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="0d372-153">bir anlık görüntü tooread, hello hesabında hello kopyalama Blob işlemi toocopy bir anlık görüntü tooanother sayfa blobu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="0d372-154">Merhaba hedef blob hello kopyalama işlemi için var olan tüm anlık görüntüleri olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d372-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="0d372-155">Merhaba hedef blob anlık görüntüleri sahip sonra hello Blob kopyalama işlemi hata kodu 409 döndürür (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="0d372-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="0d372-156">Dönüş hello mutlak URI tooa anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="0d372-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="0d372-157">Bu C# kod örneği bir anlık görüntü oluşturur ve hello Yazar hello birincil konumu için mutlak URI.</span><span class="sxs-lookup"><span data-stu-id="0d372-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="0d372-158">Nasıl anlık görüntüleri ücretler tahakkuk anlama</span><span class="sxs-lookup"><span data-stu-id="0d372-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="0d372-159">Bir blob salt okunur bir kopyası olan, bir anlık görüntü oluşturma ek veri depolama ücretleri tooyour hesabında neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d372-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="0d372-160">Uygulamanızı tasarlarken, böylece maliyetleri en aza indirebilirsiniz nasıl bu ücretler tahakkuk farkında önemli toobe olur.</span><span class="sxs-lookup"><span data-stu-id="0d372-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="0d372-161">Fatura ile ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="0d372-161">Important billing considerations</span></span>
<span data-ttu-id="0d372-162">liste aşağıdaki hello bir anlık görüntü oluşturulurken önemli noktaları tooconsider içerir.</span><span class="sxs-lookup"><span data-stu-id="0d372-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="0d372-163">Merhaba blob veya hello anlık görüntü olup depolama hesabınızın benzersiz blokları veya sayfalar için ücret doğurur.</span><span class="sxs-lookup"><span data-stu-id="0d372-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="0d372-164">Hesabınızı hello Kabarcık bunlar temel alır güncelleştirilene kadar blob ile ilişkili anlık görüntüler için ek ücretler uygulanır değil.</span><span class="sxs-lookup"><span data-stu-id="0d372-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="0d372-165">Merhaba temel blob güncelleştirdikten sonra anlık görüntülerden kareninkinden.</span><span class="sxs-lookup"><span data-stu-id="0d372-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="0d372-166">Bu gerçekleştiğinde, hello benzersiz blokları veya her bir blob veya anlık görüntü sayfalarında için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="0d372-167">Bir blok blobu blokta değiştirdiğinizde, bu blok sonradan benzersiz bloğu olarak ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="0d372-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="0d372-168">Merhaba blok aynı kimliği engelleme ve aynı hello hello olsa bile bu geçerlidir veriler hello anlık sahip.</span><span class="sxs-lookup"><span data-stu-id="0d372-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="0d372-169">Merhaba blok kaydedildikten sonra yine, kendisine karşılık gelen hiçbir anlık görüntüdeki gelen kareninkinden ve verileri için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="0d372-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="0d372-170">Merhaba aynı aynı verilerle güncelleştirilir bir sayfa blob'u içinde bir sayfa için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0d372-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="0d372-171">Bir blok blobu tarafından arama hello değiştirme [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] yöntemi hello blob tüm bloklarında değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0d372-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="0d372-172">Bu blob ile ilişkili bir anlık görüntü varsa, tüm bloklarında hello temel blob ve anlık görüntü şimdi ayırmak ve hem BLOB'ları tüm hello bloklarında için ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="0d372-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="0d372-173">Merhaba temel blob ve hello anlık görüntü Hello verileri aynı kalır olsa bile bu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0d372-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="0d372-174">iki özdeş veriler içeren olup olmadığını hello Azure Blob hizmeti anlamına gelir toodetermine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="0d372-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="0d372-175">Karşıya yüklenen ve kaydedilen her bloğu benzersiz olarak kabul edilir, sahip hello olsa bile aynı veri ve hello aynı kimliği engelle</span><span class="sxs-lookup"><span data-stu-id="0d372-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="0d372-176">Benzersiz blokları için Ücret tahakkuk, bir anlık görüntüsü bir blob güncelleştirme ek benzersiz blokları ve ek ücretlere sonuçları önemli tooconsider demektir.</span><span class="sxs-lookup"><span data-stu-id="0d372-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="0d372-177">Anlık Görüntü Yönetimi ile maliyeti en aza indir</span><span class="sxs-lookup"><span data-stu-id="0d372-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="0d372-178">Anlık görüntüleri dikkatle yönetme öneririz tooavoid ek giderleri.</span><span class="sxs-lookup"><span data-stu-id="0d372-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="0d372-179">Toohelp tarafından hello depolama, anlık görüntü hello maliyetleri en aza bu en iyi uygulamaları takip edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0d372-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="0d372-180">Silin ve hello blob güncelleştirdiğinizde Uygulama tasarımınız anlık görüntüleri tutmak gerektirmedikçe aynı verilerle güncelleştirdiğiniz olsa bile bir blob ile ilişkili anlık görüntüleri yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d372-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="0d372-181">Silme ve hello blob'un anlık yeniden oluşturmayı hello blob ve anlık görüntüleri değil ayırmak emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d372-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="0d372-182">Bir blob için anlık görüntü bakımı, arama kaçının. [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob.</span><span class="sxs-lookup"><span data-stu-id="0d372-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="0d372-183">Bu yöntemler tüm temel blob ve anlık görüntüleri toodiverge önemli ölçüde neden hello blob hello bloklarında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0d372-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="0d372-184">Bunun yerine, güncelleştirme hello blokları olası en az sayıda hello kullanarak [PutBlock] [ dotnet_PutBlock] ve [PutBlockList] [ dotnet_PutBlockList] yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="0d372-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="0d372-185">Anlık görüntü senaryoları faturalama</span><span class="sxs-lookup"><span data-stu-id="0d372-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="0d372-186">Aşağıdaki senaryolar hello nasıl bir blok blobu ve onun anlık görüntüleri için Ücret tahakkuk göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="0d372-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="0d372-187">**Senaryo 1**</span><span class="sxs-lookup"><span data-stu-id="0d372-187">**Scenario 1**</span></span>

<span data-ttu-id="0d372-188">Başlangıç anlık görüntü alındıktan sonra yalnızca benzersiz blokları için 1, 2 ve 3 ücretler tahakkuk eden şekilde Senaryo 1'de, hello temel blob güncelleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="0d372-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="0d372-190">**Senaryo 2**</span><span class="sxs-lookup"><span data-stu-id="0d372-190">**Scenario 2**</span></span>

<span data-ttu-id="0d372-191">Senaryo 2, hello temel blob güncelleştirildi ancak hello anlık görüntü sahip değil.</span><span class="sxs-lookup"><span data-stu-id="0d372-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="0d372-192">Blok 3 güncelleştirildi ve içerdiği olsa bile aynı veri hello ve aynı kimliği Merhaba, 3 hello anlık görüntüdeki engelleme aynı hello değil.</span><span class="sxs-lookup"><span data-stu-id="0d372-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="0d372-193">Sonuç olarak, hello hesap için dört blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="0d372-193">As a result, hello account is charged for four blocks.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="0d372-195">**Senaryo 3**</span><span class="sxs-lookup"><span data-stu-id="0d372-195">**Scenario 3**</span></span>

<span data-ttu-id="0d372-196">Senaryo 3, hello temel blob güncelleştirildi ancak hello anlık görüntü sahip değil.</span><span class="sxs-lookup"><span data-stu-id="0d372-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="0d372-197">Blok 3 hello temel blob 4 bloğunda ile değiştirildi, ancak hello anlık görüntü hala Blok 3 yansıtır.</span><span class="sxs-lookup"><span data-stu-id="0d372-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="0d372-198">Sonuç olarak, hello hesap için dört blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="0d372-198">As a result, hello account is charged for four blocks.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="0d372-200">**Senaryo 4**</span><span class="sxs-lookup"><span data-stu-id="0d372-200">**Scenario 4**</span></span>

<span data-ttu-id="0d372-201">Senaryo 4, hello temel blob tamamen güncelleştirildi ve kendi özgün blokları hiçbiri içerir.</span><span class="sxs-lookup"><span data-stu-id="0d372-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="0d372-202">Sonuç olarak, hello hesabı için tüm sekiz benzersiz blokları doludur.</span><span class="sxs-lookup"><span data-stu-id="0d372-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="0d372-203">Bir güncelleştirme yöntemi gibi kullanıyorsanız, bu senaryo ortaya çıkabilir [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray][dotnet_UploadFromByteArray], bu yöntemler tüm blob Merhaba içeriğine değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="0d372-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="0d372-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d372-205">Next steps</span></span>

* <span data-ttu-id="0d372-206">Sanal makine (VM) disk anlık görüntüleri ile çalışma hakkında daha fazla bilgi bulabilirsiniz [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](../../virtual-machines/windows/incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="0d372-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="0d372-207">BLOB storage kullanarak ek kod örnekleri için bkz: [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="0d372-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="0d372-208">Örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.</span><span class="sxs-lookup"><span data-stu-id="0d372-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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
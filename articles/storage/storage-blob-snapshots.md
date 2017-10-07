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
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Blob anlık görüntüsü oluşturma

Bir anlık görüntüsü, bir noktada geçen süre içinde bir blob, salt okunur bir sürümüdür. Anlık görüntüler, BLOB'ları yedekleme için kullanışlıdır. Bir anlık görüntü oluşturduktan sonra okuma, kopyalama veya silin, ancak değişiklik yapamazsınız.

Aynı tooits temel blobu blob anlık görüntüsüdür, o hello blob dışında bir URI'ya sahip bir **DateTime** değeri toohello blob URI'si tooindicate hello zaman hangi Merhaba anlık görüntü alındığı eklenmiş. Örneğin, URI bir sayfa blob ise `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello anlık görüntü URI benzer çok`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Tüm anlık görüntüleri hello temel blob'un URI paylaşır. Merhaba temel blob ve hello anlık görüntü arasında ayrım eklenmiş hello yalnızca hello **DateTime** değeri.
>

Bir blob herhangi bir sayıda anlık görüntü olabilir. Açıkça silinene kadar anlık görüntüleri kalıcı olmasını sağlar. Bir anlık görüntü, temel blob outlive olamaz. Merhaba temel blob tootrack ile ilişkili hello anlık görüntüleri listeleme, geçerli anlık görüntüler.

Bir blob görüntüsünü oluşturduğunuzda, blob'un Sistem özellikleri hello hello kopyalanan toohello anlık görüntü aynı değerlerdir. Merhaba oluşturduğunuzda anlık görüntü için ayrı meta verileri belirtmediğiniz sürece hello temel blob'un meta verileri de anlık görüntü, kopyalanan toohello oluşturur.

Merhaba temel blob ile ilişkili kiraları hello anlık görüntü etkilemez. Bir anlık görüntü üzerinde bir kira edinemez.

Bir VHD kullanılan toostore hello geçerli bilgilerini ve VM diskinin durumu dosyasıdır. Merhaba VM bir diski kullanımdan çıkarın veya VM hello kapatın ve sonra VHD dosyasını bir anlık görüntüsünü. Bu anlık görüntü dosyasını kullanabilirsiniz sonraki tooretrieve hello VHD dosya zamandaki o noktada ve hello VM oluşturun.

Merhaba depolama hesabı için depolama hizmeti şifreleme (SSE) etkinse, hangi hello blob bulunduğu, ardından o blob gerçekleştirilecek tüm anlık görüntüleri bekleyen şifrelenir.

## <a name="create-a-snapshot"></a>Bir anlık görüntü oluşturma
Merhaba aşağıdaki kod örneğinde nasıl toocreate kullanarak bir anlık görüntü hello gösterilmektedir [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/). Bu örnek, oluşturulduğunda hello anlık görüntü için ek meta veri belirtir.

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

## <a name="copy-snapshots"></a>Anlık görüntü kopyalama
BLOB'ları ve anlık görüntüleri içeren kopyalama işlemleri bu kurallar izleyin:

* Bir anlık görüntü, temel blob kopyalayabilirsiniz. Anlık görüntü toohello konumunu hello temel blob yükselterek bir blob önceki bir sürümünü geri yükleyebilirsiniz. Merhaba anlık görüntü olarak kalır, ancak hello temel blob hello anlık görüntü yazılabilir bir kopyasını üzerine yazılır.
* Bir anlık görüntü tooa hedef blob farklı bir adla kopyalayabilirsiniz. Merhaba elde edilen hedef blob yazılabilir bir blob ve anlık görüntü değil ' dir.
* Kaynak blob kopyalandığında, tüm anlık görüntüleri hello kaynak BLOB kopyalanan toohello hedef olup olmadığı. Hedef blob bir kopya ile yazılır, hello özgün hedef blob ile ilişkili tüm anlık görüntüleri değişmeden kalır.
* Bir blok blobu görüntüsünü oluşturduğunuzda, hello blob'un taahhüt engelleme listesine de kopyalanan toohello anlık görüntüsüdür. Herhangi bir kaydedilmeyen bloğu kopyalanmaz.

## <a name="specify-an-access-condition"></a>Bir erişim koşulu belirtin
Çağırdığınızda [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], böylece yalnızca bir koşul karşılandığında hello anlık görüntü oluşturulduğunda bir erişim koşulu belirtebilirsiniz. toospecify erişim koşulu kullanmak hello [AccessCondition] [ dotnet_AccessCondition] parametresi. Merhaba koşulu karşılanmadı, hello anlık görüntü oluşturulmadı ve hello Blob hizmeti durum kodu döndürdüğünde belirtilmişse [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Anlık görüntüleri silin
Merhaba anlık görüntüleri de silinene kadar anlık görüntüleri içeren bir blobu silemezsiniz. Tek tek bir anlık görüntüyü silmek veya hello kaynak blob silindiğinde tüm anlık görüntülerin silinmesi belirtin. Toodelete hala anlık görüntülere sahip bir blob denediğinizde bir hatayla sonuçlanır.

Kod örnekteki nasıl aşağıdaki hello toodelete bir blob ve .NET, kendi anlık görüntülerini nerede `blockBlob` türünde bir nesne [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Azure Premium Storage ile anlık görüntüler
Premium depolama ile anlık görüntülerini kullanarak kurallar aşağıdaki hello uygulayın:

* Merhaba Maksimum sayıda anlık görüntü premium depolama hesabındaki bir sayfa blobu başına 100'dür. Bu sınır aşılırsa, hata kodu 409 hello anlık görüntü Blob işlemi döndürür (`SnapshotCountExceeded`).
* Premium depolama hesabı her 10 dakikada bir sayfa blob'u görüntüsünü alabilir. Hızı aşılırsa, hata kodu 409 hello anlık görüntü Blob işlemi döndürür (`SnapshotOperationRateExceeded`).
* bir anlık görüntü tooread, hello hesabında hello kopyalama Blob işlemi toocopy bir anlık görüntü tooanother sayfa blobu kullanabilirsiniz. Merhaba hedef blob hello kopyalama işlemi için var olan tüm anlık görüntüleri olmaması gerekir. Merhaba hedef blob anlık görüntüleri sahip sonra hello Blob kopyalama işlemi hata kodu 409 döndürür (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Dönüş hello mutlak URI tooa anlık görüntü
Bu C# kod örneği bir anlık görüntü oluşturur ve hello Yazar hello birincil konumu için mutlak URI.

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

## <a name="understand-how-snapshots-accrue-charges"></a>Nasıl anlık görüntüleri ücretler tahakkuk anlama
Bir blob salt okunur bir kopyası olan, bir anlık görüntü oluşturma ek veri depolama ücretleri tooyour hesabında neden olabilir. Uygulamanızı tasarlarken, böylece maliyetleri en aza indirebilirsiniz nasıl bu ücretler tahakkuk farkında önemli toobe olur.

### <a name="important-billing-considerations"></a>Fatura ile ilgili önemli noktalar
liste aşağıdaki hello bir anlık görüntü oluşturulurken önemli noktaları tooconsider içerir.

* Merhaba blob veya hello anlık görüntü olup depolama hesabınızın benzersiz blokları veya sayfalar için ücret doğurur. Hesabınızı hello Kabarcık bunlar temel alır güncelleştirilene kadar blob ile ilişkili anlık görüntüler için ek ücretler uygulanır değil. Merhaba temel blob güncelleştirdikten sonra anlık görüntülerden kareninkinden. Bu gerçekleştiğinde, hello benzersiz blokları veya her bir blob veya anlık görüntü sayfalarında için ücretlendirilirsiniz.
* Bir blok blobu blokta değiştirdiğinizde, bu blok sonradan benzersiz bloğu olarak ücretlendirilir. Merhaba blok aynı kimliği engelleme ve aynı hello hello olsa bile bu geçerlidir veriler hello anlık sahip. Merhaba blok kaydedildikten sonra yine, kendisine karşılık gelen hiçbir anlık görüntüdeki gelen kareninkinden ve verileri için sizden ücret alınır. Merhaba aynı aynı verilerle güncelleştirilir bir sayfa blob'u içinde bir sayfa için geçerlidir.
* Bir blok blobu tarafından arama hello değiştirme [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] yöntemi hello blob tüm bloklarında değiştirir. Bu blob ile ilişkili bir anlık görüntü varsa, tüm bloklarında hello temel blob ve anlık görüntü şimdi ayırmak ve hem BLOB'ları tüm hello bloklarında için ücretlendirilir. Merhaba temel blob ve hello anlık görüntü Hello verileri aynı kalır olsa bile bu geçerlidir.
* iki özdeş veriler içeren olup olmadığını hello Azure Blob hizmeti anlamına gelir toodetermine sahip değil. Karşıya yüklenen ve kaydedilen her bloğu benzersiz olarak kabul edilir, sahip hello olsa bile aynı veri ve hello aynı kimliği engelle Benzersiz blokları için Ücret tahakkuk, bir anlık görüntüsü bir blob güncelleştirme ek benzersiz blokları ve ek ücretlere sonuçları önemli tooconsider demektir.

### <a name="minimize-cost-with-snapshot-management"></a>Anlık Görüntü Yönetimi ile maliyeti en aza indir

Anlık görüntüleri dikkatle yönetme öneririz tooavoid ek giderleri. Toohelp tarafından hello depolama, anlık görüntü hello maliyetleri en aza bu en iyi uygulamaları takip edebilirsiniz:

* Silin ve hello blob güncelleştirdiğinizde Uygulama tasarımınız anlık görüntüleri tutmak gerektirmedikçe aynı verilerle güncelleştirdiğiniz olsa bile bir blob ile ilişkili anlık görüntüleri yeniden oluşturun. Silme ve hello blob'un anlık yeniden oluşturmayı hello blob ve anlık görüntüleri değil ayırmak emin olabilirsiniz.
* Bir blob için anlık görüntü bakımı, arama kaçının. [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob. Bu yöntemler tüm temel blob ve anlık görüntüleri toodiverge önemli ölçüde neden hello blob hello bloklarında değiştirin. Bunun yerine, güncelleştirme hello blokları olası en az sayıda hello kullanarak [PutBlock] [ dotnet_PutBlock] ve [PutBlockList] [ dotnet_PutBlockList] yöntemleri.

### <a name="snapshot-billing-scenarios"></a>Anlık görüntü senaryoları faturalama
Aşağıdaki senaryolar hello nasıl bir blok blobu ve onun anlık görüntüleri için Ücret tahakkuk göstermektedir.

**Senaryo 1**

Başlangıç anlık görüntü alındıktan sonra yalnızca benzersiz blokları için 1, 2 ve 3 ücretler tahakkuk eden şekilde Senaryo 1'de, hello temel blob güncelleştirilmemiş.

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Senaryo 2**

Senaryo 2, hello temel blob güncelleştirildi ancak hello anlık görüntü sahip değil. Blok 3 güncelleştirildi ve içerdiği olsa bile aynı veri hello ve aynı kimliği Merhaba, 3 hello anlık görüntüdeki engelleme aynı hello değil. Sonuç olarak, hello hesap için dört blokları doludur.

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Senaryo 3**

Senaryo 3, hello temel blob güncelleştirildi ancak hello anlık görüntü sahip değil. Blok 3 hello temel blob 4 bloğunda ile değiştirildi, ancak hello anlık görüntü hala Blok 3 yansıtır. Sonuç olarak, hello hesap için dört blokları doludur.

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Senaryo 4**

Senaryo 4, hello temel blob tamamen güncelleştirildi ve kendi özgün blokları hiçbiri içerir. Sonuç olarak, hello hesabı için tüm sekiz benzersiz blokları doludur. Bir güncelleştirme yöntemi gibi kullanıyorsanız, bu senaryo ortaya çıkabilir [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], veya [UploadFromByteArray][dotnet_UploadFromByteArray], bu yöntemler tüm blob Merhaba içeriğine değiştirmek.

![Azure Storage kaynakları](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Sonraki adımlar

* Sanal makine (VM) disk anlık görüntüleri ile çalışma hakkında daha fazla bilgi bulabilirsiniz [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](storage-incremental-snapshots.md)

* BLOB storage kullanarak ek kod örnekleri için bkz: [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.

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
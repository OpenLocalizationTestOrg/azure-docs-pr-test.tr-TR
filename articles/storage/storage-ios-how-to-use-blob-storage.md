---
title: "aaaHow toouse Azure Blob depolama alanından iOS | Microsoft Docs"
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Nasıl toouse Blob depolama alanından iOS
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Bu makale size nasıl gösterir tooperform yaygın senaryolar Microsoft Azure Blob storage kullanarak. Merhaba örnekler Objective-C yazılmıştır ve hello kullan [iOS için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-ios). Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar. BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü. Merhaba de indirebilirsiniz [örnek uygulaması](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly bkz hello bir iOS uygulamasına Azure depolama alanı kullanımda.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Hello Azure depolama iOS kitaplığı uygulamanıza alma
Hello Azure depolama iOS kitaplığı uygulamanıza hello kullanarak alabileceğiniz [Azure depolama CocoaPod](https://cocoapods.org/pods/AZSClient) veya hello alarak **Framework** dosya. CocoaPod tümleştirme hello kitaplığı, ancak hello framework dosyasından içe aktarımı varolan projeniz için daha az müdahale kolaylaştırır gibi şekilde önerilen hello ' dir.

toouse bu kitaplığı aşağıdaki hello gerekir:
- iOS 8 +
- Xcode 7 +

## <a name="cocoapod"></a>CocoaPod
1. Henüz yapmadıysanız [yükleme CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) bir terminal penceresi açarak ve çalışan komut aşağıdaki hello bilgisayarınızda
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Ardından, hello proje dizininde (Merhaba dizin .xcodeproj dosyanızı içeren) adlı yeni bir dosya oluşturun _Podfile_(dosya uzantısı yok). Too_Podfile_ aşağıdaki hello ekleyin ve kaydedin.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Merhaba terminal penceresinde toohello proje dizini ve aşağıdaki komutu çalıştırın hello gidin

    ```shell    
    pod install
    ```

4. Xcode'da, .xcodeproj açıksa, kapatın. Proje dizini yeni oluşturulan açık hello proje dosyasında hangi hello .xcworkspace uzantısına sahip olacaktır. Bu gelen için şimdi çalıştığınız hello dosyasıdır.

## <a name="framework"></a>Framework
Merhaba toouse hello toobuild hello framework el ile kitaplığıdır başka bir şekilde:

1. İlk, indirme veya kopya hello [azure depolama ios depodaki](https://github.com/azure/azure-storage-ios).
2. Na *azure depolama ios* -> *Lib* -> *Azure Storage istemci Kitaplığı*, açarak `AZSClient.xcodeproj` xcode'da.
3. Xcode, değişiklik hello etkin sol üst hello çok "Azure Storage istemci kitaplığı" Düzen "Framework".
4. Merhaba projeyi (⌘ + B) oluşturun. Bu oluşturacak bir `AZSClient.framework` masaüstünüzde dosya.

Merhaba aşağıdakileri yaparak uygulamanıza sonra hello framework dosyasını içe aktarabilirsiniz:

1. Yeni bir proje oluşturun veya varolan Xcode projenizde açın.
2. Sürükle ve bırak hello `AZSClient.framework` Xcode Proje Gezgini içine.
3. Seçin *gerekirse öğeleri Kopyala*ve tıklayın *son*.
4. Merhaba sol gezinti projenizde tıklayın ve hello tıklatın *genel* hello projesini düzenleyen hello üstündeki sekmesi.
5. Merhaba altında *bağlantılı çerçeveler ve kitaplıklar* bölümünde, hello Ekle düğmesine (+) tıklayın.
6. Merhaba listesinde zaten sağlanan kitaplıkları, arama `libxml2.2.tbd` ve tooyour proje ekleyin.

## <a name="import-hello-library"></a>İçeri aktarma hello kitaplığı 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Swift kullanıyorsanız, toocreate köprü oluşturma üst bilgi gerekir ve < AZSClient/AZSClient.h > var. içeri aktarın:

1. Bir üst bilgi dosyası oluştur `Bridging-Header.h`ve içeri aktarma deyimini yukarıda hello ekleyin.
2. Toohello Git *Build Settings* arayın ve sekmesinde *Objective-C köprü oluşturma üst bilgisi*.
3. Merhaba alanında bulunan çift *Objective-C köprü oluşturma üst bilgisi* ve hello yolu tooyour üstbilgi dosyası ekleyin:`ProjectName/Bridging-Header.h`
4. Köprü oluşturma üst bilgisi hello yapı hello proje (⌘ + B) tooverify Xcode tarafından çekilmiş.
5. Merhaba kitaplığı doğrudan SWIFT herhangi dosyasında kullanmaya başlamak, içeri aktarma deyimlerini için gerek yoktur.

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Zaman uyumsuz işlemler
> [!NOTE]
> Merhaba Hizmeti'ne yönelik bir istek gerçekleştiren tüm yöntemleri zaman uyumsuz işlemleridir. Merhaba kod örnekleri, bu yöntemleri tamamlama işleyici olduğunu bulabilirsiniz. Merhaba tamamlama işleyici içinde kod çalışacağı **sonra** hello isteği tamamlandı. Merhaba tamamlama işleyici çalıştırdıktan sonra kod **sırada** hello istek yapıldığında.
> 
> 

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
Azure storage'daki her blob bir kapsayıcıda yer almalıdır. Merhaba aşağıdaki örnekte nasıl bir kapsayıcı toocreate adlı gösterir *newcontainer*, zaten yoksa, depolama hesabınızdaki. Kapsayıcı için bir ad seçerken, yukarıda belirtilen kural adlandırma Merhaba, dikkatli olun.

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

Bu durum hello bakarak çalıştığını doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve olmadığını doğrulayarak *newcontainer* depolama hesabınız için kapsayıcıları hello listesi bulunmaktadır.

## <a name="set-container-permissions"></a>Kapsayıcı izinleri ayarlama
Bir kapsayıcının izinler için yapılandırılmış olan **özel** varsayılan erişim. Ancak, kapsayıcılar kapsayıcı erişim için birkaç farklı seçenekleri sağlar:

* **Özel**: kapsayıcı ve blob verilerini yalnızca hello hesap sahibi tarafından okunabilir.
* **BLOB**: Bu kapsayıcı içindeki Blob verilerini anonim istek okunabilir ancak kapsayıcı verileri kullanılabilir değil. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları numaralandırılamıyor.
* **Kapsayıcı**: kapsayıcı ve blob verilerini anonim istek okunabilir. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.

Merhaba aşağıdaki örnekte, nasıl gösterir içeren kapsayıcı bir toocreate **kapsayıcı** erişim hello Internet üzerindeki tüm kullanıcılar için genel, salt okunur erişime izin verip izinlerini:

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
Hello belirtildiği gibi [Blob hizmeti kavramları](#blob-service-concepts) bölümü, Blob Storage üç farklı türde BLOB sunar: blok blobları, ekleme blobları ve sayfa blobları. Hello Azure depolama iOS kitaplığı üç türde BLOB destekler. Çoğu durumda, blok blob türü toouse önerilen hello ' dir.

Aşağıdaki örnek hello nasıl tooupload bir blok blob bir NSString gösterir. Bir blob, aynı adı zaten var. Bu kapsayıcıda hello ile bu blob Merhaba içeriğine üzerine yazılır.

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

Bu durum hello bakarak çalıştığını doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve o hello kapsayıcı doğrulama *containerpublic*, hello blob içeriyor *sampleblob*. Bu örnekte, bu uygulama giderek toohello göre BLOB URI'si çalışılan doğrulayabilmeniz için ortak bir kapsayıcı kullandık:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Ayrıca bir NSString blok blobundan toouploading, NSData, NSInputStream veya yerel bir dosya için benzer yöntemler mevcut.

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
Merhaba aşağıdaki örnekte nasıl toolist tüm bir kapsayıcıda BLOB'ların gösterilmektedir. Bu işlemi gerçekleştirirken şu parametreler Merhaba dikkatli olun:     

* **continuationToken** -hello işlemi listeleme hello burada başlamalıdır devamlılık belirteci temsil eder. Herhangi bir belirteci sağlanırsa, hello başından BLOB'ları listeler. Maksimum Küme tooa yukarı sıfırdan herhangi bir sayıda BLOB listelenebilir. Bu yöntem, sıfır sonuçları döndürür olsa bile `results.continuationToken` nil, olmayan değil listelenen başka BLOB hello hizmeti üzerinde olabilir.
* **önek** -hello önek toouse blob liste belirtebilirsiniz. Bu önek ile başlayan BLOB'lar listelenir.
* **Listblobs** - hello belirtildiği gibi [adlandırma ve kapsayıcılar ve bloblar başvuran](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) bölümünde, bir düz depolama düzeni hello Blob hizmeti olmasına rağmen oluşturabilirsiniz sanal bir hiyerarşi BLOB'lar yolu ile adlandırılmasıyla bilgi. Ancak, düz olmayan listeleme şu anda desteklenmiyor. Bu özellik yakında çıkıyor. Şimdilik, bu değer olmalıdır **Evet**.

* **blobListingDetails** -, BLOB'ları listelerken hangi öğeleri tooinclude belirtebilirsiniz
  * _AZSBlobListingDetailsNone_: kaydedilmiş BLOB'ları yalnızca listelemek ve blob verilerini döndürmenizi değil.
  * _AZSBlobListingDetailsSnapshots_: kaydedilmiş BLOB'ları listeler ve blob anlık görüntüler.
  * _AZSBlobListingDetailsMetadata_: döndürülen hello listesindeki her bir blob için blob meta veri alınamadı.
  * _AZSBlobListingDetailsUncommittedBlobs_: kaydedilmiş ve kaydedilmemiş BLOB'ları listeler.
  * _AZSBlobListingDetailsCopy_: kopyalama dahil hello listesindeki özellikleri.
  * _AZSBlobListingDetailsAll_: tüm kullanılabilir kaydedilmiş BLOB'ları, kaydedilmemiş BLOB'ları ve anlık görüntüleri listesi ve bu BLOB'lar için tüm meta veri ve kopyalama durumu döndürür.
* **maxResults** -hello sonuçları tooreturn bu işlem için maksimum sayısı. Kullanımı -1 toonot bir sınır belirleyin.
* **completionHandler** -kod tooexecute hello blok işlemi listeleme hello hello sonuçlarını ile.

Devamlılık belirteci döndürülen her zaman bu örnekte, bir yardımcı yöntemi kullanılan toorecursively çağrısı hello listesi BLOB'lar yöntemidir.

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a>Blob indirme
örnekte gösterildiği nasıl aşağıdaki hello toodownload bir blob tooa NSString nesnesi.

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a>Blob silme
örnekte gösterildiği nasıl aşağıdaki hello toodelete blob.

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a>Bir blob kapsayıcısından silin
örnekte gösterildiği nasıl aşağıdaki hello toodelete bir kapsayıcı.

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a>Sonraki adımlar
Artık, öğrendiğinize göre nasıl toouse Blob depolama alanından iOS, bu bağlantıları toolearn hello iOS Kitaplığı hakkında daha fazla izleyin ve depolama hizmeti hello.

* [İOS için Azure Storage istemci kitaplığı](https://github.com/azure/azure-storage-ios)
* [Azure depolama iOS başvuru belgeleri](http://azure.github.io/azure-storage-ios/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage)

Bu kitaplığı ile ilgili sorularınız varsa, ücretsiz toopost tooour eşitleyerek [MSDN Azure Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) veya [yığın taşması](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Lütfen Azure depolama için özellik önerileri varsa, çok sonrası[Azure depolama geri bildirim](https://feedback.azure.com/forums/217298-storage/).


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
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="6a263-103">Nasıl toouse Blob depolama alanından iOS</span><span class="sxs-lookup"><span data-stu-id="6a263-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6a263-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6a263-104">Overview</span></span>
<span data-ttu-id="6a263-105">Bu makale size nasıl gösterir tooperform yaygın senaryolar Microsoft Azure Blob storage kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6a263-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="6a263-106">Merhaba örnekler Objective-C yazılmıştır ve hello kullan [iOS için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="6a263-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="6a263-107">Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="6a263-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="6a263-108">BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="6a263-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="6a263-109">Merhaba de indirebilirsiniz [örnek uygulaması](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly bkz hello bir iOS uygulamasına Azure depolama alanı kullanımda.</span><span class="sxs-lookup"><span data-stu-id="6a263-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="6a263-110">Hello Azure depolama iOS kitaplığı uygulamanıza alma</span><span class="sxs-lookup"><span data-stu-id="6a263-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="6a263-111">Hello Azure depolama iOS kitaplığı uygulamanıza hello kullanarak alabileceğiniz [Azure depolama CocoaPod](https://cocoapods.org/pods/AZSClient) veya hello alarak **Framework** dosya.</span><span class="sxs-lookup"><span data-stu-id="6a263-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="6a263-112">CocoaPod tümleştirme hello kitaplığı, ancak hello framework dosyasından içe aktarımı varolan projeniz için daha az müdahale kolaylaştırır gibi şekilde önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a263-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="6a263-113">toouse bu kitaplığı aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a263-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="6a263-114">iOS 8 +</span><span class="sxs-lookup"><span data-stu-id="6a263-114">iOS 8+</span></span>
- <span data-ttu-id="6a263-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="6a263-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="6a263-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="6a263-116">CocoaPod</span></span>
1. <span data-ttu-id="6a263-117">Henüz yapmadıysanız [yükleme CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) bir terminal penceresi açarak ve çalışan komut aşağıdaki hello bilgisayarınızda</span><span class="sxs-lookup"><span data-stu-id="6a263-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="6a263-118">Ardından, hello proje dizininde (Merhaba dizin .xcodeproj dosyanızı içeren) adlı yeni bir dosya oluşturun _Podfile_(dosya uzantısı yok).</span><span class="sxs-lookup"><span data-stu-id="6a263-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="6a263-119">Too_Podfile_ aşağıdaki hello ekleyin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a263-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="6a263-120">Merhaba terminal penceresinde toohello proje dizini ve aşağıdaki komutu çalıştırın hello gidin</span><span class="sxs-lookup"><span data-stu-id="6a263-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="6a263-121">Xcode'da, .xcodeproj açıksa, kapatın.</span><span class="sxs-lookup"><span data-stu-id="6a263-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="6a263-122">Proje dizini yeni oluşturulan açık hello proje dosyasında hangi hello .xcworkspace uzantısına sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6a263-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="6a263-123">Bu gelen için şimdi çalıştığınız hello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6a263-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="6a263-124">Framework</span><span class="sxs-lookup"><span data-stu-id="6a263-124">Framework</span></span>
<span data-ttu-id="6a263-125">Merhaba toouse hello toobuild hello framework el ile kitaplığıdır başka bir şekilde:</span><span class="sxs-lookup"><span data-stu-id="6a263-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="6a263-126">İlk, indirme veya kopya hello [azure depolama ios depodaki](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="6a263-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="6a263-127">Na *azure depolama ios* -> *Lib* -> *Azure Storage istemci Kitaplığı*, açarak `AZSClient.xcodeproj` xcode'da.</span><span class="sxs-lookup"><span data-stu-id="6a263-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="6a263-128">Xcode, değişiklik hello etkin sol üst hello çok "Azure Storage istemci kitaplığı" Düzen "Framework".</span><span class="sxs-lookup"><span data-stu-id="6a263-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="6a263-129">Merhaba projeyi (⌘ + B) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a263-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="6a263-130">Bu oluşturacak bir `AZSClient.framework` masaüstünüzde dosya.</span><span class="sxs-lookup"><span data-stu-id="6a263-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="6a263-131">Merhaba aşağıdakileri yaparak uygulamanıza sonra hello framework dosyasını içe aktarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6a263-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="6a263-132">Yeni bir proje oluşturun veya varolan Xcode projenizde açın.</span><span class="sxs-lookup"><span data-stu-id="6a263-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="6a263-133">Sürükle ve bırak hello `AZSClient.framework` Xcode Proje Gezgini içine.</span><span class="sxs-lookup"><span data-stu-id="6a263-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="6a263-134">Seçin *gerekirse öğeleri Kopyala*ve tıklayın *son*.</span><span class="sxs-lookup"><span data-stu-id="6a263-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="6a263-135">Merhaba sol gezinti projenizde tıklayın ve hello tıklatın *genel* hello projesini düzenleyen hello üstündeki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6a263-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="6a263-136">Merhaba altında *bağlantılı çerçeveler ve kitaplıklar* bölümünde, hello Ekle düğmesine (+) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a263-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="6a263-137">Merhaba listesinde zaten sağlanan kitaplıkları, arama `libxml2.2.tbd` ve tooyour proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6a263-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="6a263-138">İçeri aktarma hello kitaplığı</span><span class="sxs-lookup"><span data-stu-id="6a263-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="6a263-139">Swift kullanıyorsanız, toocreate köprü oluşturma üst bilgi gerekir ve < AZSClient/AZSClient.h > var. içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="6a263-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="6a263-140">Bir üst bilgi dosyası oluştur `Bridging-Header.h`ve içeri aktarma deyimini yukarıda hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6a263-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="6a263-141">Toohello Git *Build Settings* arayın ve sekmesinde *Objective-C köprü oluşturma üst bilgisi*.</span><span class="sxs-lookup"><span data-stu-id="6a263-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="6a263-142">Merhaba alanında bulunan çift *Objective-C köprü oluşturma üst bilgisi* ve hello yolu tooyour üstbilgi dosyası ekleyin:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="6a263-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="6a263-143">Köprü oluşturma üst bilgisi hello yapı hello proje (⌘ + B) tooverify Xcode tarafından çekilmiş.</span><span class="sxs-lookup"><span data-stu-id="6a263-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="6a263-144">Merhaba kitaplığı doğrudan SWIFT herhangi dosyasında kullanmaya başlamak, içeri aktarma deyimlerini için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="6a263-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="6a263-145">Zaman uyumsuz işlemler</span><span class="sxs-lookup"><span data-stu-id="6a263-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="6a263-146">Merhaba Hizmeti'ne yönelik bir istek gerçekleştiren tüm yöntemleri zaman uyumsuz işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="6a263-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="6a263-147">Merhaba kod örnekleri, bu yöntemleri tamamlama işleyici olduğunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a263-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="6a263-148">Merhaba tamamlama işleyici içinde kod çalışacağı **sonra** hello isteği tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6a263-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="6a263-149">Merhaba tamamlama işleyici çalıştırdıktan sonra kod **sırada** hello istek yapıldığında.</span><span class="sxs-lookup"><span data-stu-id="6a263-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="6a263-150">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a263-150">Create a container</span></span>
<span data-ttu-id="6a263-151">Azure storage'daki her blob bir kapsayıcıda yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="6a263-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="6a263-152">Merhaba aşağıdaki örnekte nasıl bir kapsayıcı toocreate adlı gösterir *newcontainer*, zaten yoksa, depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="6a263-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="6a263-153">Kapsayıcı için bir ad seçerken, yukarıda belirtilen kural adlandırma Merhaba, dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="6a263-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

<span data-ttu-id="6a263-154">Bu durum hello bakarak çalıştığını doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve olmadığını doğrulayarak *newcontainer* depolama hesabınız için kapsayıcıları hello listesi bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6a263-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="6a263-155">Kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="6a263-155">Set Container Permissions</span></span>
<span data-ttu-id="6a263-156">Bir kapsayıcının izinler için yapılandırılmış olan **özel** varsayılan erişim.</span><span class="sxs-lookup"><span data-stu-id="6a263-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="6a263-157">Ancak, kapsayıcılar kapsayıcı erişim için birkaç farklı seçenekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="6a263-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="6a263-158">**Özel**: kapsayıcı ve blob verilerini yalnızca hello hesap sahibi tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="6a263-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="6a263-159">**BLOB**: Bu kapsayıcı içindeki Blob verilerini anonim istek okunabilir ancak kapsayıcı verileri kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="6a263-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="6a263-160">İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="6a263-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="6a263-161">**Kapsayıcı**: kapsayıcı ve blob verilerini anonim istek okunabilir.</span><span class="sxs-lookup"><span data-stu-id="6a263-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="6a263-162">İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="6a263-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="6a263-163">Merhaba aşağıdaki örnekte, nasıl gösterir içeren kapsayıcı bir toocreate **kapsayıcı** erişim hello Internet üzerindeki tüm kullanıcılar için genel, salt okunur erişime izin verip izinlerini:</span><span class="sxs-lookup"><span data-stu-id="6a263-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6a263-164">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="6a263-164">Upload a blob into a container</span></span>
<span data-ttu-id="6a263-165">Hello belirtildiği gibi [Blob hizmeti kavramları](#blob-service-concepts) bölümü, Blob Storage üç farklı türde BLOB sunar: blok blobları, ekleme blobları ve sayfa blobları.</span><span class="sxs-lookup"><span data-stu-id="6a263-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="6a263-166">Hello Azure depolama iOS kitaplığı üç türde BLOB destekler.</span><span class="sxs-lookup"><span data-stu-id="6a263-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="6a263-167">Çoğu durumda, blok blob türü toouse önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a263-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="6a263-168">Aşağıdaki örnek hello nasıl tooupload bir blok blob bir NSString gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a263-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="6a263-169">Bir blob, aynı adı zaten var. Bu kapsayıcıda hello ile bu blob Merhaba içeriğine üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="6a263-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="6a263-170">Bu durum hello bakarak çalıştığını doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve o hello kapsayıcı doğrulama *containerpublic*, hello blob içeriyor *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="6a263-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="6a263-171">Bu örnekte, bu uygulama giderek toohello göre BLOB URI'si çalışılan doğrulayabilmeniz için ortak bir kapsayıcı kullandık:</span><span class="sxs-lookup"><span data-stu-id="6a263-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="6a263-172">Ayrıca bir NSString blok blobundan toouploading, NSData, NSInputStream veya yerel bir dosya için benzer yöntemler mevcut.</span><span class="sxs-lookup"><span data-stu-id="6a263-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="6a263-173">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="6a263-173">List hello blobs in a container</span></span>
<span data-ttu-id="6a263-174">Merhaba aşağıdaki örnekte nasıl toolist tüm bir kapsayıcıda BLOB'ların gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6a263-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="6a263-175">Bu işlemi gerçekleştirirken şu parametreler Merhaba dikkatli olun:</span><span class="sxs-lookup"><span data-stu-id="6a263-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="6a263-176">**continuationToken** -hello işlemi listeleme hello burada başlamalıdır devamlılık belirteci temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6a263-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="6a263-177">Herhangi bir belirteci sağlanırsa, hello başından BLOB'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="6a263-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="6a263-178">Maksimum Küme tooa yukarı sıfırdan herhangi bir sayıda BLOB listelenebilir.</span><span class="sxs-lookup"><span data-stu-id="6a263-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="6a263-179">Bu yöntem, sıfır sonuçları döndürür olsa bile `results.continuationToken` nil, olmayan değil listelenen başka BLOB hello hizmeti üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a263-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="6a263-180">**önek** -hello önek toouse blob liste belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a263-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="6a263-181">Bu önek ile başlayan BLOB'lar listelenir.</span><span class="sxs-lookup"><span data-stu-id="6a263-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="6a263-182">**Listblobs** - hello belirtildiği gibi [adlandırma ve kapsayıcılar ve bloblar başvuran](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) bölümünde, bir düz depolama düzeni hello Blob hizmeti olmasına rağmen oluşturabilirsiniz sanal bir hiyerarşi BLOB'lar yolu ile adlandırılmasıyla bilgi.</span><span class="sxs-lookup"><span data-stu-id="6a263-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="6a263-183">Ancak, düz olmayan listeleme şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6a263-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="6a263-184">Bu özellik yakında çıkıyor.</span><span class="sxs-lookup"><span data-stu-id="6a263-184">This feature is coming soon.</span></span> <span data-ttu-id="6a263-185">Şimdilik, bu değer olmalıdır **Evet**.</span><span class="sxs-lookup"><span data-stu-id="6a263-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="6a263-186">**blobListingDetails** -, BLOB'ları listelerken hangi öğeleri tooinclude belirtebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6a263-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="6a263-187">_AZSBlobListingDetailsNone_: kaydedilmiş BLOB'ları yalnızca listelemek ve blob verilerini döndürmenizi değil.</span><span class="sxs-lookup"><span data-stu-id="6a263-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="6a263-188">_AZSBlobListingDetailsSnapshots_: kaydedilmiş BLOB'ları listeler ve blob anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6a263-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="6a263-189">_AZSBlobListingDetailsMetadata_: döndürülen hello listesindeki her bir blob için blob meta veri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="6a263-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="6a263-190">_AZSBlobListingDetailsUncommittedBlobs_: kaydedilmiş ve kaydedilmemiş BLOB'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="6a263-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="6a263-191">_AZSBlobListingDetailsCopy_: kopyalama dahil hello listesindeki özellikleri.</span><span class="sxs-lookup"><span data-stu-id="6a263-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="6a263-192">_AZSBlobListingDetailsAll_: tüm kullanılabilir kaydedilmiş BLOB'ları, kaydedilmemiş BLOB'ları ve anlık görüntüleri listesi ve bu BLOB'lar için tüm meta veri ve kopyalama durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a263-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="6a263-193">**maxResults** -hello sonuçları tooreturn bu işlem için maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="6a263-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="6a263-194">Kullanımı -1 toonot bir sınır belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6a263-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="6a263-195">**completionHandler** -kod tooexecute hello blok işlemi listeleme hello hello sonuçlarını ile.</span><span class="sxs-lookup"><span data-stu-id="6a263-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="6a263-196">Devamlılık belirteci döndürülen her zaman bu örnekte, bir yardımcı yöntemi kullanılan toorecursively çağrısı hello listesi BLOB'lar yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="6a263-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="6a263-197">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="6a263-197">Download a blob</span></span>
<span data-ttu-id="6a263-198">örnekte gösterildiği nasıl aşağıdaki hello toodownload bir blob tooa NSString nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6a263-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="6a263-199">Blob silme</span><span class="sxs-lookup"><span data-stu-id="6a263-199">Delete a blob</span></span>
<span data-ttu-id="6a263-200">örnekte gösterildiği nasıl aşağıdaki hello toodelete blob.</span><span class="sxs-lookup"><span data-stu-id="6a263-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="6a263-201">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="6a263-201">Delete a blob container</span></span>
<span data-ttu-id="6a263-202">örnekte gösterildiği nasıl aşağıdaki hello toodelete bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="6a263-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6a263-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a263-203">Next steps</span></span>
<span data-ttu-id="6a263-204">Artık, öğrendiğinize göre nasıl toouse Blob depolama alanından iOS, bu bağlantıları toolearn hello iOS Kitaplığı hakkında daha fazla izleyin ve depolama hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="6a263-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="6a263-205">İOS için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="6a263-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="6a263-206">Azure depolama iOS başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="6a263-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="6a263-207">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="6a263-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="6a263-208">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="6a263-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="6a263-209">Bu kitaplığı ile ilgili sorularınız varsa, ücretsiz toopost tooour eşitleyerek [MSDN Azure Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) veya [yığın taşması](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="6a263-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="6a263-210">Lütfen Azure depolama için özellik önerileri varsa, çok sonrası[Azure depolama geri bildirim](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="6a263-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>


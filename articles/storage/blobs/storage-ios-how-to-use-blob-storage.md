---
title: "Azure Blob depolama alanından iOS kullanma | Microsoft Docs"
description: "Azure Blob Storage (nesne depolama) ile bulutta yapılandırılmamış veri depolayın."
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
ms.openlocfilehash: b5f43156d46b1ab9dd10ff5a93427270c1b839ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="49395-103">BLOB depolama alanından iOS kullanma</span><span class="sxs-lookup"><span data-stu-id="49395-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="49395-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="49395-104">Overview</span></span>
<span data-ttu-id="49395-105">Bu makalede Microsoft Azure Blob storage kullanarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="49395-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="49395-106">Objective-C ve kullanım örnekleri yazılır [iOS için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="49395-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="49395-107">Kapsamdaki senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="49395-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="49395-108">BLOB'ları hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="49395-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="49395-109">Ayrıca indirebilirsiniz [örnek uygulaması](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) hızlı bir şekilde bir iOS uygulamasına Azure Storage kullanımda görmek için.</span><span class="sxs-lookup"><span data-stu-id="49395-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="49395-110">Azure depolama iOS kitaplığı uygulamanıza alma</span><span class="sxs-lookup"><span data-stu-id="49395-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="49395-111">Azure depolama iOS kitaplığı uygulamanıza kullanarak alabileceğiniz [Azure depolama CocoaPod](https://cocoapods.org/pods/AZSClient) veya alarak **Framework** dosya.</span><span class="sxs-lookup"><span data-stu-id="49395-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="49395-112">Kolay varolan projeniz için daha az müdahale ancak framework dosyasından içeri aktarma kitaplığı tümleştirme getirir CocoaPod önerilen yoludur.</span><span class="sxs-lookup"><span data-stu-id="49395-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="49395-113">Bu kitaplığı kullanmak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="49395-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="49395-114">iOS 8 +</span><span class="sxs-lookup"><span data-stu-id="49395-114">iOS 8+</span></span>
- <span data-ttu-id="49395-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="49395-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="49395-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="49395-116">CocoaPod</span></span>
1. <span data-ttu-id="49395-117">Henüz yapmadıysanız [yükleme CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) bir terminal penceresi açıp aşağıdaki komutu çalıştırarak, bilgisayarınızdaki</span><span class="sxs-lookup"><span data-stu-id="49395-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="49395-118">Ardından, proje dizininde (.xcodeproj dosyanızı içeren dizini) adlı yeni bir dosya oluşturun _Podfile_(dosya uzantısı yok).</span><span class="sxs-lookup"><span data-stu-id="49395-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="49395-119">Aşağıdakileri ekleyin _Podfile_ ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="49395-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="49395-120">Terminal penceresi, proje dizinine gidin ve aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="49395-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="49395-121">Xcode'da, .xcodeproj açıksa, kapatın.</span><span class="sxs-lookup"><span data-stu-id="49395-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="49395-122">Proje dizininde .xcworkspace uzantısına sahip olacak yeni oluşturulan proje dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="49395-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="49395-123">Bu gelen için şimdi çalıştığınız dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="49395-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="49395-124">Framework</span><span class="sxs-lookup"><span data-stu-id="49395-124">Framework</span></span>
<span data-ttu-id="49395-125">Kitaplığı kullanarak diğer bir yol framework el ile oluşturmaktır:</span><span class="sxs-lookup"><span data-stu-id="49395-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="49395-126">İlk olarak, indirme ya da kopyalama [azure depolama ios depodaki](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="49395-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="49395-127">Na *azure depolama ios* -> *Lib* -> *Azure Storage istemci Kitaplığı*, açarak `AZSClient.xcodeproj` xcode'da.</span><span class="sxs-lookup"><span data-stu-id="49395-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="49395-128">Sol üst, Xcode, "Azure Storage istemci kitaplığı" "Framework" etkin düzenine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="49395-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="49395-129">Projeyi (⌘ + B) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49395-129">Build the project (⌘+B).</span></span> <span data-ttu-id="49395-130">Bu oluşturacak bir `AZSClient.framework` masaüstünüzde dosya.</span><span class="sxs-lookup"><span data-stu-id="49395-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="49395-131">Aşağıdakileri yaparak uygulamanıza sonra framework dosyasını içe aktarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49395-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="49395-132">Yeni bir proje oluşturun veya varolan Xcode projenizde açın.</span><span class="sxs-lookup"><span data-stu-id="49395-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="49395-133">Sürükleme ve bırakma `AZSClient.framework` Xcode Proje Gezgini içine.</span><span class="sxs-lookup"><span data-stu-id="49395-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="49395-134">Seçin *gerekirse öğeleri Kopyala*ve tıklayın *son*.</span><span class="sxs-lookup"><span data-stu-id="49395-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="49395-135">Sol taraftaki gezinti projenizde tıklayın ve tıklayın *genel* proje Düzenleyicisi'ni üstündeki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="49395-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="49395-136">Altında *bağlantılı çerçeveler ve kitaplıklar* bölümünde, (+) Ekle düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="49395-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="49395-137">İçin zaten sağlanan Kitaplıklar listesinde arama `libxml2.2.tbd` ve projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="49395-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="49395-138">İçeri aktarma kitaplığı</span><span class="sxs-lookup"><span data-stu-id="49395-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="49395-139">SWIFT kullanıyorsanız, bir köprü oluşturma üst bilgisi oluşturun ve < AZSClient/AZSClient.h > var. alma gerekir:</span><span class="sxs-lookup"><span data-stu-id="49395-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="49395-140">Bir üst bilgi dosyası oluştur `Bridging-Header.h`ve yukarıdaki içeri aktarma deyimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="49395-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="49395-141">Git *Build Settings* arayın ve sekmesinde *Objective-C köprü oluşturma üst bilgisi*.</span><span class="sxs-lookup"><span data-stu-id="49395-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="49395-142">Alanın üzerinde çift *Objective-C köprü oluşturma üst bilgisi* ve yolun üstbilgi dosyanıza ekleyin:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="49395-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="49395-143">Köprü oluşturma üst bilgisi tarafından Xcode çekilmiş olduğunu doğrulamak için projeyi (⌘ + B) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49395-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="49395-144">Kitaplık doğrudan SWIFT herhangi dosyasında kullanmaya başlamak, içeri aktarma deyimlerini için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="49395-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="49395-145">Zaman uyumsuz işlemler</span><span class="sxs-lookup"><span data-stu-id="49395-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="49395-146">Bir hizmet isteği gerçekleştiren tüm yöntemleri zaman uyumsuz işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="49395-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="49395-147">Kod örnekleri, bu yöntemleri tamamlama işleyici olduğunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49395-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="49395-148">Kod tamamlama işleyici içinde çalışacak **sonra** isteğini tamamladı.</span><span class="sxs-lookup"><span data-stu-id="49395-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="49395-149">Tamamlama işleyici çalıştırdıktan sonra kod **sırada** istek yapılır.</span><span class="sxs-lookup"><span data-stu-id="49395-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="49395-150">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="49395-150">Create a container</span></span>
<span data-ttu-id="49395-151">Azure storage'daki her blob bir kapsayıcıda yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="49395-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="49395-152">Aşağıdaki örnek adlı bir kapsayıcı oluşturulacağını gösterir *newcontainer*, zaten yoksa, depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="49395-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="49395-153">Kapsayıcı için bir ad seçerken, yukarıda belirtilen adlandırma kuralları dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="49395-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="49395-154">Bu bakarak çalıştığını onaylayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve olmadığını doğrulayarak *newcontainer* depolama hesabınız için kapsayıcılar listesi bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="49395-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="49395-155">Kapsayıcı izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="49395-155">Set Container Permissions</span></span>
<span data-ttu-id="49395-156">Bir kapsayıcının izinler için yapılandırılmış olan **özel** varsayılan erişim.</span><span class="sxs-lookup"><span data-stu-id="49395-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="49395-157">Ancak, kapsayıcılar kapsayıcı erişim için birkaç farklı seçenekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="49395-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="49395-158">**Özel**: kapsayıcı ve blob verileri yalnızca hesap sahibi tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="49395-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="49395-159">**BLOB**: Bu kapsayıcı içindeki Blob verilerini anonim istek okunabilir ancak kapsayıcı verileri kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="49395-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="49395-160">İstemcilerin anonim istek aracılığıyla kapsayıcıdaki blobları numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="49395-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="49395-161">**Kapsayıcı**: kapsayıcı ve blob verilerini anonim istek okunabilir.</span><span class="sxs-lookup"><span data-stu-id="49395-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="49395-162">İstemcilerin anonim istek aracılığıyla kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı kapsayıcılara numaralandırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="49395-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="49395-163">Aşağıdaki örnekte nasıl ile bir kapsayıcı oluşturulacağını gösterir **kapsayıcı** erişim Internet üzerindeki tüm kullanıcılar için genel, salt okunur erişime izin verip izinlerini:</span><span class="sxs-lookup"><span data-stu-id="49395-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="49395-164">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="49395-164">Upload a blob into a container</span></span>
<span data-ttu-id="49395-165">Bölümünde belirtildiği gibi [Blob hizmeti kavramları](#blob-service-concepts) bölümü, Blob Storage üç farklı türde BLOB sunar: blok blobları, ekleme blobları ve sayfa blobları.</span><span class="sxs-lookup"><span data-stu-id="49395-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="49395-166">Azure depolama iOS kitaplığı üç türde BLOB destekler.</span><span class="sxs-lookup"><span data-stu-id="49395-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="49395-167">Çoğu durumda, kullanılması önerilen blob türü blok blobudur.</span><span class="sxs-lookup"><span data-stu-id="49395-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="49395-168">Aşağıdaki örnek, bir NSString blok blobundan karşıya nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="49395-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="49395-169">Aynı ada sahip bir blob bu kapsayıcıda zaten varsa, bu blob içeriğinin üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="49395-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

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

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="49395-170">Bu bakarak çalıştığını onaylayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com) ve olmadığını doğrulayarak kapsayıcı *containerpublic*, blob'un bulunduğu *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="49395-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="49395-171">Bu örnekte, bu uygulama BLOB URI'si giderek çalışılan doğrulayabilmeniz için ortak bir kapsayıcı kullandık:</span><span class="sxs-lookup"><span data-stu-id="49395-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="49395-172">Bir NSString blok blobundan karşıya yanı sıra, NSData, NSInputStream veya yerel bir dosya için benzer yöntemler mevcut.</span><span class="sxs-lookup"><span data-stu-id="49395-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="49395-173">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="49395-173">List the blobs in a container</span></span>
<span data-ttu-id="49395-174">Aşağıdaki örnek, bir kapsayıcıdaki tüm blob'lara listesinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="49395-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="49395-175">Bu işlemi gerçekleştirirken, aşağıdaki parametreleri dikkatli olun:</span><span class="sxs-lookup"><span data-stu-id="49395-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="49395-176">**continuationToken** -listeleme işlemi burada başlamalıdır devamlılık belirteci temsil eder.</span><span class="sxs-lookup"><span data-stu-id="49395-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="49395-177">Herhangi bir belirteci sağlanırsa, başlangıçtan itibaren BLOB'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="49395-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="49395-178">En fazla kümesi kadar sıfırdan herhangi bir sayıda BLOB listelenebilir.</span><span class="sxs-lookup"><span data-stu-id="49395-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="49395-179">Bu yöntem, sıfır sonuçları döndürür olsa bile `results.continuationToken` nil, olmayan değil listelenen başka BLOB hizmeti üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="49395-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="49395-180">**önek** -blob listesi için kullanılacak öneki belirtin.</span><span class="sxs-lookup"><span data-stu-id="49395-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="49395-181">Bu önek ile başlayan BLOB'lar listelenir.</span><span class="sxs-lookup"><span data-stu-id="49395-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="49395-182">**Listblobs** - bölümünde belirtildiği gibi [adlandırma ve kapsayıcılar ve bloblar başvuran](#naming-and-referencing-containers-and-blobs) bölümünde, bir düz depolama düzeni Blob hizmeti olmasına rağmen oluşturabilirsiniz sanal bir hiyerarşi BLOB'lar yolu ile adlandırılmasıyla bilgi.</span><span class="sxs-lookup"><span data-stu-id="49395-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="49395-183">Ancak, düz olmayan listeleme şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="49395-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="49395-184">Bu özellik yakında çıkıyor.</span><span class="sxs-lookup"><span data-stu-id="49395-184">This feature is coming soon.</span></span> <span data-ttu-id="49395-185">Şimdilik, bu değer olmalıdır **Evet**.</span><span class="sxs-lookup"><span data-stu-id="49395-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="49395-186">**blobListingDetails** -BLOB'lar listelerken dahil edilecek maddeleri belirtebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="49395-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="49395-187">_AZSBlobListingDetailsNone_: kaydedilmiş BLOB'ları yalnızca listelemek ve blob verilerini döndürmenizi değil.</span><span class="sxs-lookup"><span data-stu-id="49395-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="49395-188">_AZSBlobListingDetailsSnapshots_: kaydedilmiş BLOB'ları listeler ve blob anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="49395-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="49395-189">_AZSBlobListingDetailsMetadata_: döndürülen listesindeki her bir blob için blob meta veri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="49395-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="49395-190">_AZSBlobListingDetailsUncommittedBlobs_: kaydedilmiş ve kaydedilmemiş BLOB'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="49395-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="49395-191">_AZSBlobListingDetailsCopy_: kopyalama dahil listenin özelliklerinde.</span><span class="sxs-lookup"><span data-stu-id="49395-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="49395-192">_AZSBlobListingDetailsAll_: tüm kullanılabilir kaydedilmiş BLOB'ları, kaydedilmemiş BLOB'ları ve anlık görüntüleri listesi ve bu BLOB'lar için tüm meta veri ve kopyalama durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="49395-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="49395-193">**maxResults** -bu işlem için döndürülecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="49395-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="49395-194">Bir sınır ayarlamamayı -1 kullanın.</span><span class="sxs-lookup"><span data-stu-id="49395-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="49395-195">**completionHandler** - listeleme işlemi sonuçlarıyla yürütülecek kod bloğu.</span><span class="sxs-lookup"><span data-stu-id="49395-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="49395-196">Bu örnekte, bir yardımcı yöntemi için kullanılan yinelemeli olarak çağrı listesi BLOB'devamlılık belirteci döndürülen her zaman yöntemi.</span><span class="sxs-lookup"><span data-stu-id="49395-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="49395-197">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="49395-197">Download a blob</span></span>
<span data-ttu-id="49395-198">Aşağıdaki örnek, bir NSString nesnesine bir blob indirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="49395-198">The following example shows how to download a blob to a NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="49395-199">Blob silme</span><span class="sxs-lookup"><span data-stu-id="49395-199">Delete a blob</span></span>
<span data-ttu-id="49395-200">Aşağıdaki örnek, bir blobu silmek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="49395-200">The following example shows how to delete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="49395-201">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="49395-201">Delete a blob container</span></span>
<span data-ttu-id="49395-202">Aşağıdaki örnek, bir kapsayıcı silmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="49395-202">The following example shows how to delete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49395-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49395-203">Next steps</span></span>
<span data-ttu-id="49395-204">Artık iOS Blob Storage kullanma öğrendiğinize göre iOS kitaplığı ve depolama hizmeti hakkında daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="49395-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="49395-205">İOS için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="49395-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="49395-206">Azure depolama iOS başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="49395-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="49395-207">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="49395-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="49395-208">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="49395-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="49395-209">Bu kitaplığı ile ilgili sorularınız varsa, gönderilecek çekinmeyin bizim [MSDN Azure Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) veya [yığın taşması](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="49395-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="49395-210">Azure Storage için özellik önerileri varsa, lütfen deftere [Azure depolama geri bildirim](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="49395-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>


---
title: "Windows mağazası uygulamalarında Azure depolama aaaUse | Microsoft Docs"
description: "Nasıl toocreate bir Windows mağazası öğrenin Azure Blob, kuyruk, tablo veya dosya depolama kullanan uygulama."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="ae4e4-103">Nasıl Windows mağazası uygulamalarında toouse Azure depolama</span><span class="sxs-lookup"><span data-stu-id="ae4e4-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="ae4e4-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ae4e4-104">Overview</span></span>
<span data-ttu-id="ae4e4-105">Bu kılavuz Azure Storage kullanır bir Windows mağazası uygulaması geliştirme ile tooget nasıl başlatılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="ae4e4-106">Gerekli araçları yükleyin</span><span class="sxs-lookup"><span data-stu-id="ae4e4-106">Download required tools</span></span>
* <span data-ttu-id="ae4e4-107">[Visual Studio](https://www.visualstudio.com/downloads/) kolay toobuild kolaylaştırır hata ayıklama, yerelleştirme, paketini ve Windows mağazası uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="ae4e4-108">Visual Studio 2012 veya üzeri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="ae4e4-109">Merhaba [Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) Azure Storage ile çalışmak için bir Windows çalışma zamanı sınıf kitaplığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="ae4e4-110">[Windows mağazası uygulamaları için WCF Veri Hizmetleri Araçları](http://www.microsoft.com/download/details.aspx?id=30714) hello hizmet Başvurusu Ekle deneyimi Visual Studio'daki Windows mağazası uygulamaları için istemci tarafı OData desteği ile genişletir.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="ae4e4-111">Uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="ae4e4-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="ae4e4-112">Hazırlanma</span><span class="sxs-lookup"><span data-stu-id="ae4e4-112">Getting ready</span></span>
<span data-ttu-id="ae4e4-113">Yeni bir Windows mağazası uygulama projesi Visual Studio 2012 veya sonraki sürümlerde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![Depolama-apps-depolama-vs-proje][store-apps-storage-vs-project]

<span data-ttu-id="ae4e4-115">Ardından sağ tıklayarak bir başvuru toohello Azure Storage istemci kitaplığı ekleyin **başvuruları**a **Başvuru Ekle**ve Windows Runtime için depolama istemci kitaplığı toohello göz atma, yüklenen:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![Depolama-uygulamalar-storage--kitaplığını seçin][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="ae4e4-117">Merhaba Blob ile Merhaba kitaplığını ve kuyruk Hizmetleri kullanma</span><span class="sxs-lookup"><span data-stu-id="ae4e4-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="ae4e4-118">Bu noktada, uygulamanız hazır toocall hello Azure Blob ve kuyruk Hizmetleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="ae4e4-119">Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri böylece Azure depolama türlerini doğrudan başvurulabilir:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="ae4e4-120">Ardından, bir düğme tooyour sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="ae4e4-121">Kod tooits aşağıdaki hello eklemek **tıklatın** olay ve hello kullanarak, olay işleyicisi yöntemi değiştirme [async anahtar sözcüğü](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="ae4e4-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="ae4e4-122">Bu kod iki dize değişkenleri olduğunu varsayar *accountName* ve *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="ae4e4-123">Bunlar, bu hesapla ilişkili depolama hesabı ve hello hesap anahtarınızı hello adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="ae4e4-124">Derleme ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-124">Build and run hello application.</span></span> <span data-ttu-id="ae4e4-125">Merhaba düğmesi tıklatıldığında, bir kapsayıcı adlı olup olmadığını denetleyin *container1* hesabınızda var ve ardından değilse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="ae4e4-126">Merhaba tablo hizmeti ile Merhaba kitaplığı kullanma</span><span class="sxs-lookup"><span data-stu-id="ae4e4-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="ae4e4-127">WCF Veri Hizmetleri hello Windows mağazası uygulama kitaplığı için kullanılan toocommunicate hello Azure Table hizmetiyle olan türlerini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="ae4e4-128">Ardından, Paket Yöneticisi konsolu kullanılarak WCF kitaplıkları hello başvuru toohello gerekli ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![Mağaza-apps-depolama-Paket-Yöneticisi][store-apps-storage-package-manager]

<span data-ttu-id="ae4e4-130">Komut toopoint Paket Yöneticisi toohello konumu makinenizde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="ae4e4-131">Bu komut tüm gerekli başvuruları tooyour proje otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="ae4e4-132">Toouse istemiyorsanız, Paket Yöneticisi konsolu Merhaba, paket kaynaklarını, LocalMachine toohello listenizde hello WCF Veri Hizmetleri NuGet klasör ekleyin ve ardından açıklandığı gibi hello kullanıcı Arabirimi aracılığıyla hello başvurusu ekleyin [yönetme NuGet paketlerini kullanma Merhaba iletişim](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="ae4e4-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="ae4e4-133">Merhaba WCF Veri Hizmetleri NuGet paketi başvurduğunda, düğmenin hello kodda değişiklik **tıklatın** olay:</span><span class="sxs-lookup"><span data-stu-id="ae4e4-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="ae4e4-134">Bu kod adlı bir tablo olup olmadığını denetler *tablo1* hesabınızda var ve yoksa oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="ae4e4-135">Aynı yüklediğiniz paketini hello kullanılabilir olduğu bir başvuru tooMicrosoft.WindowsAzure.Storage.Table.dll de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="ae4e4-136">Bu kitaplık yansıma tabanlı seri hale getirme ve genel sorgular gibi ek işlevler içerir.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="ae4e4-137">Bu kitaplık JavaScript'i desteklemiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ae4e4-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

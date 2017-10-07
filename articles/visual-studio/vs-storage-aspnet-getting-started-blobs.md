---
title: "aaaGet başlatılan Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak tooa depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure blob storage kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="ff5b1-103">Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff5b1-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ff5b1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ff5b1-104">Overview</span></span>

<span data-ttu-id="ff5b1-105">Azure blob depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ff5b1-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ff5b1-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ff5b1-108">Bu öğretici, Azure blob storage kullanarak bazı genel senaryolar için toowrite ASP.NET kodu nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="ff5b1-109">Bir blob kapsayıcısını oluşturma ve karşıya yükleme, listeleme, indirme ve BLOB'ları silme senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="ff5b1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff5b1-110">Prerequisites</span></span>

* [<span data-ttu-id="ff5b1-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff5b1-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="ff5b1-112">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="ff5b1-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="ff5b1-113">Bir MVC denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="ff5b1-114">Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="ff5b1-116">Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="ff5b1-118">Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *BlobsController*seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="ff5b1-120">Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `BlobsController.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="ff5b1-121">Bir blob kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ff5b1-121">Create a blob container</span></span>

<span data-ttu-id="ff5b1-122">Bir blob kapsayıcı, BLOB'ları ve klasörleri iç içe geçmiş bir hiyerarşisidir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="ff5b1-123">Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ff5b1-124">Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ff5b1-125">Açık hello `BlobsController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="ff5b1-126">Adlı bir yöntem ekleyin **CreateBlobContainer** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ff5b1-127">Merhaba içinde **CreateBlobContainer** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ff5b1-128">Kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="ff5b1-129">(Değişiklik  *&lt;depolama hesabı adı >* hello erişme Azure depolama hesabı adını toohello.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ff5b1-130">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="ff5b1-131">Alma bir **CloudBlobContainer** bir başvuru toohello istenen blob kapsayıcı adı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="ff5b1-132">Merhaba **CloudBlobClient.GetContainerReference** yöntemi blob Storage'a karşı istek yapmaz.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="ff5b1-133">Merhaba blob kapsayıcısı mevcut olup olmadığına bakılmaksızın hello başvuru döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="ff5b1-134">Merhaba çağrısı **CloudBlobContainer.CreateIfNotExists** henüz yoksa, yöntem toocreate hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="ff5b1-135">Merhaba **CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **true** hello kapsayıcısı yok ve başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="ff5b1-136">Aksi takdirde, **false** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="ff5b1-137">Güncelleştirme hello **ViewBag** hello blob kapsayıcısının hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="ff5b1-138">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ff5b1-139">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateBlobContainer** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ff5b1-140">Açık `CreateBlobContainer.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="ff5b1-141">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ff5b1-142">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="ff5b1-143">Merhaba uygulamayı çalıştırın ve seçin **Blob kapsayıcısı oluşturmak** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![BLOB kapsayıcı oluşturun](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="ff5b1-145">Daha önce belirtildiği gibi hello **CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello kapsayıcısı yok ve oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="ff5b1-146">Bu nedenle, hello kapsayıcı mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="ff5b1-147">toorun hello uygulama birden çok kez, hello kapsayıcı hello uygulama yeniden çalıştırmadan önce silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="ff5b1-148">Silme hello kapsayıcı hello yapılabilir **CloudBlobContainer.Delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="ff5b1-149">Merhaba kapsayıcı hello kullanarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="ff5b1-150">Bir blob kapsayıcıya bir blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="ff5b1-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="ff5b1-151">Seçtiğiniz sonra [bir blob kapsayıcısını oluşturulan](#create-a-blob-container), bu kapsayıcıya dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="ff5b1-152">Bu bölümde, bir yerel dosya tooa blob kapsayıcısı karşıya aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="ff5b1-153">Merhaba adımlar varsayar adlı bir blob kapsayıcı oluşturduğunuz *test blob kapsayıcısı*.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="ff5b1-154">Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ff5b1-155">Açık hello `BlobsController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="ff5b1-156">Adlı bir yöntem ekleyin **UploadBlob** döndüren bir **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="ff5b1-157">Merhaba içinde **UploadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ff5b1-158">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ff5b1-159">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="ff5b1-160">Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="ff5b1-161">Daha önce açıklandığı gibi Azure depolama farklı blob türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="ff5b1-162">tooretrieve bir başvuru tooa sayfa blob'u çağrısı hello **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="ff5b1-163">tooretrieve bir başvuru tooa blok blobu çağrısı hello **CloudBlobContainer.GetBlockBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="ff5b1-164">Genellikle, blok blob türü toouse önerilen hello olur.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="ff5b1-165">(Değiştir < blob-adı > * kez karşıya toogive hello blob istediğiniz toohello ad.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="ff5b1-166">Bir blob başvurusu edindiğinizde hello blob başvurusu nesnenin çağırarak tüm veri akışı tooit yükleyebilirsiniz **UploadFromStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="ff5b1-167">Merhaba **UploadFromStream** yöntemi, mevcut değil veya mevcut değilse bu raporun üzerine hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="ff5b1-168">(Değişiklik  *&lt;dosya karşıya yükleme >* tooa tooupload istediğiniz yolun toohello dosyasını tam.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="ff5b1-169">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ff5b1-170">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ff5b1-171">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="ff5b1-172">Merhaba uygulamayı çalıştırın ve seçin **karşıya yükleme blob**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="ff5b1-173">Merhaba bölüm - [listesinde bir blob kapsayıcısında hello BLOB'lar](#list-the-blobs-in-a-blob-container) -toolist hello bir blob kapsayıcısında nasıl BLOB'gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="ff5b1-174">Bir blob kapsayıcısında listesi hello BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="ff5b1-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="ff5b1-175">Bu bölümde, nasıl bir blob kapsayıcısında toolist hello BLOB gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="ff5b1-176">Merhaba örnek kod başvuran hello *test blob kapsayıcısı* hello bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ff5b1-177">Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ff5b1-178">Açık hello `BlobsController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="ff5b1-179">Adlı bir yöntem ekleyin **ListBlobs** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ff5b1-180">Merhaba içinde **ListBlobs** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ff5b1-181">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ff5b1-182">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="ff5b1-183">Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="ff5b1-184">bir blob kapsayıcısında toolist hello BLOB'ları kullanmak hello **CloudBlobContainer.ListBlobs** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="ff5b1-185">Merhaba **CloudBlobContainer.ListBlobs** yöntemi döndürür bir **Ilistblobıtem** tooa cast nesne **CloudBlockBlob**, **CloudPageBlob**, veya **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="ff5b1-186">Merhaba aşağıdaki kod parçacığını bir blob kapsayıcısında tüm hello BLOB'lar numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="ff5b1-187">Cast toohello uygun nesne türünü ve onun adına göre her bir blob olduğunu (veya URI hello durumda bir **CloudBlobDirectory**) tooa listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="ff5b1-188">Toplama tooblobs içinde blob kapsayıcıları dizinleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="ff5b1-189">Şimdi adlı bir blob kapsayıcıya sahip varsayalım *test blob kapsayıcısı* hiyerarşi aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="ff5b1-190">Önceki kod örneğinde hello kullanarak hello **BLOB'lar** dize liste değerleri benzer toohello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="ff5b1-191">Gördüğünüz gibi hello listesi yalnızca hello en üst düzey varlıkları içerir; değil hello olanları iç içe (*bar.png* ve *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="ff5b1-192">toolist tüm varlıkları bir blob kapsayıcı içindeki Merhaba, hello çağırmalısınız **CloudBlobContainer.ListBlobs** yöntemi ve geçişi **true** hello için **Listblobs** parametre.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="ff5b1-193">Ayar hello **Listblobs** parametresi çok**true** hello blob kapsayıcısında tüm varlıkların düz bir liste döndürür ve sonuçları aşağıdaki hello verir:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="ff5b1-194">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ff5b1-195">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ListBlobs** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ff5b1-196">Açık `ListBlobs.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="ff5b1-197">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ff5b1-198">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="ff5b1-199">Merhaba uygulamayı çalıştırın ve seçin **listesinde BLOB'lar** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![BLOB listeleme](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="ff5b1-201">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="ff5b1-201">Download blobs</span></span>

<span data-ttu-id="ff5b1-202">Bu bölümde, nasıl toodownload blob ve ya da onu toolocal depolama veya okuma hello içeriği bir dizeye kalıcı olmasını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="ff5b1-203">Merhaba örnek kod başvuran hello *test blob kapsayıcısı* hello bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="ff5b1-204">Açık hello `BlobsController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="ff5b1-205">Adlı bir yöntem ekleyin **DownloadBlob** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="ff5b1-206">Merhaba içinde **DownloadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ff5b1-207">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ff5b1-208">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="ff5b1-209">Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="ff5b1-210">Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="ff5b1-211">(Değişiklik  *&lt;blob adı >* indirme hello blob adını toohello.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="ff5b1-212">toodownload bir blob kullanmak hello **CloudBlockBlob.DownloadToStream** veya **CloudPageBlob.DownloadToStream** hello blob türüne bağlı olarak yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="ff5b1-213">Merhaba aşağıdaki kod parçacığını kullanan hello **CloudBlockBlob.DownloadToStream** yöntemi tootransfer bir blob'un içeriği tooa akış nesnesi başka bir deyişle, ardından tooa yerel dosya kalıcı: (değişiklik  *&lt;yerel dosya adı >* toohello tam indirilen hello blob istediğiniz dosya adını temsil eden.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="ff5b1-214">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ff5b1-215">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="ff5b1-216">Merhaba uygulamayı çalıştırın ve seçin **indirme blob** toodownload hello blob.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="ff5b1-217">Hello belirtilen hello blob **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı indirmeleri hello belirttiğiniz toohello konumu **File.OpenWrite** yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="ff5b1-218">Blob’ları silme</span><span class="sxs-lookup"><span data-stu-id="ff5b1-218">Delete blobs</span></span>

<span data-ttu-id="ff5b1-219">Merhaba aşağıdaki adımları göstermek nasıl toodelete blob:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ff5b1-220">Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ff5b1-221">Açık hello `BlobsController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="ff5b1-222">Adlı bir yöntem ekleyin **DeleteBlob** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="ff5b1-223">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ff5b1-224">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ff5b1-225">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="ff5b1-226">Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="ff5b1-227">Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="ff5b1-228">(Değişiklik  *&lt;blob adı >* silmekte hello blob adını toohello.)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="ff5b1-229">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ff5b1-230">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="ff5b1-231">Merhaba uygulamayı çalıştırın ve seçin **Delete blob** toodelete hello blob hello belirtilen **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ff5b1-232">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff5b1-232">Next steps</span></span>
<span data-ttu-id="ff5b1-233">Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="ff5b1-234">Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff5b1-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="ff5b1-235">Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff5b1-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)

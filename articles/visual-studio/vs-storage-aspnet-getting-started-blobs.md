---
title: "Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak bir depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure blob storage kullanarak nereden başlayacaksınız"
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
ms.openlocfilehash: e953c7978705379a28581213e8f1c665473ddd60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="d28f0-103">Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d28f0-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d28f0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d28f0-104">Overview</span></span>

<span data-ttu-id="d28f0-105">Azure blob depolama bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="d28f0-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="d28f0-107">Blob Storage aynı zamanda nesne depolama olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d28f0-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="d28f0-108">Bu öğretici, Azure blob storage kullanarak bazı genel senaryolar için ASP.NET kodunun nasıl yazılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="d28f0-109">Bir blob kapsayıcısını oluşturma ve karşıya yükleme, listeleme, indirme ve BLOB'ları silme senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="d28f0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d28f0-110">Prerequisites</span></span>

* [<span data-ttu-id="d28f0-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d28f0-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="d28f0-112">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="d28f0-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="d28f0-113">Bir MVC denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d28f0-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="d28f0-114">İçinde **Çözüm Gezgini**, sağ **denetleyicileri**ve bağlam menüsünden seçin **Ekle -> denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Bir ASP.NET MVC uygulamasına denetleyici ekleme](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="d28f0-116">Üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="d28f0-118">Üzerinde **denetleyici Ekle** iletişim kutusunda, denetleyici adı *BlobsController*seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![MVC Denetleyici adı](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="d28f0-120">Aşağıdakileri ekleyin *kullanarak* yönergeleri `BlobsController.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d28f0-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="d28f0-121">Bir blob kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d28f0-121">Create a blob container</span></span>

<span data-ttu-id="d28f0-122">Bir blob kapsayıcı, BLOB'ları ve klasörleri iç içe geçmiş bir hiyerarşisidir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="d28f0-123">Aşağıdaki adımları bir blob kapsayıcı oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d28f0-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="d28f0-124">Bu bölümdeki kod bölümündeki adımları tamamladınız varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="d28f0-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="d28f0-125">`BlobsController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="d28f0-126">Adlı bir yöntem ekleyin **CreateBlobContainer** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="d28f0-127">İçinde **CreateBlobContainer** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d28f0-128">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="d28f0-129">(Değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="d28f0-130">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d28f0-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="d28f0-131">Alma bir **CloudBlobContainer** istenen blob kapsayıcı adı için başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="d28f0-132">**CloudBlobClient.GetContainerReference** yöntemi blob Storage'a karşı istek yapmaz.</span><span class="sxs-lookup"><span data-stu-id="d28f0-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="d28f0-133">Blob kapsayıcısı mevcut olup olmadığına bakılmaksızın başvuru döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d28f0-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="d28f0-134">Çağrı **CloudBlobContainer.CreateIfNotExists** yöntemi henüz yoksa kapsayıcıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d28f0-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="d28f0-135">**CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **true** kapsayıcı yok ve başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d28f0-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="d28f0-136">Aksi takdirde, **false** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d28f0-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="d28f0-137">Güncelleştirme **ViewBag** blob kapsayıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d28f0-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="d28f0-138">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="d28f0-139">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateBlobContainer** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="d28f0-140">Açık `CreateBlobContainer.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d28f0-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="d28f0-141">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d28f0-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="d28f0-142">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="d28f0-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="d28f0-143">Uygulamayı çalıştırmak ve seçmek **Blob kapsayıcısı oluşturmak** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="d28f0-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![BLOB kapsayıcı oluşturun](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="d28f0-145">Daha önce belirtildiği gibi **CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca kapsayıcı yok ve oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d28f0-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="d28f0-146">Bu nedenle, kapsayıcı mevcut olduğunda uygulama çalıştırırsanız, yöntem **false**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="d28f0-147">Birden çok kez uygulamayı çalıştırmak için uygulamayı yeniden çalıştırmadan önce kapsayıcı silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="d28f0-148">Aracılığıyla kapsayıcı silme yapılabilir **CloudBlobContainer.Delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="d28f0-149">Bir kapsayıcı kullanılarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="d28f0-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="d28f0-150">Bir blob kapsayıcıya bir blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d28f0-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="d28f0-151">Seçtiğiniz sonra [bir blob kapsayıcısını oluşturulan](#create-a-blob-container), bu kapsayıcıya dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="d28f0-152">Bu bölümde, bir blob kapsayıcısına bir yerel dosya karşıya yükleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d28f0-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="d28f0-153">Adlı bir blob kapsayıcı oluşturduğunuz adımlarda varsayılır *test blob kapsayıcısı*.</span><span class="sxs-lookup"><span data-stu-id="d28f0-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="d28f0-154">Bu bölümdeki kod bölümündeki adımları tamamladınız varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="d28f0-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="d28f0-155">`BlobsController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="d28f0-156">Adlı bir yöntem ekleyin **UploadBlob** döndüren bir **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="d28f0-157">İçinde **UploadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d28f0-158">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="d28f0-159">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d28f0-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="d28f0-160">Alma bir **CloudBlobContainer** blob kapsayıcı adı için başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="d28f0-161">Daha önce açıklandığı gibi Azure depolama farklı blob türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d28f0-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="d28f0-162">Bir sayfa blob'u için bir başvuru almak için arama **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="d28f0-163">Bir blok blob başvurusu almak için arama **CloudBlobContainer.GetBlockBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="d28f0-164">Genellikle, blok blobu kullanmak için önerilen türüdür.</span><span class="sxs-lookup"><span data-stu-id="d28f0-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="d28f0-165">(Değiştir < blob-adı > * kez karşıya blob vermek istediğiniz ad.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="d28f0-166">Bir blob başvurusu edindiğinizde, tüm veri akışı için blob başvurusu nesnenin çağırarak karşıya yükleyebilirsiniz **UploadFromStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="d28f0-167">**UploadFromStream** yöntemi, mevcut değil veya mevcut değilse bu raporun üzerine blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d28f0-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="d28f0-168">(Değişiklik  *&lt;dosya karşıya yükleme >* karşıya yüklemek istediğiniz dosyasının tam yolunu için.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="d28f0-169">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="d28f0-170">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d28f0-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="d28f0-171">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="d28f0-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="d28f0-172">Uygulamayı çalıştırmak ve seçmek **karşıya yükleme blob**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="d28f0-173">Bölüm - [blob kapsayıcısı içinde BLOB'ları listesi](#list-the-blobs-in-a-blob-container) -blob kapsayıcısı içinde BLOB'ları listesi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="d28f0-174">Blob kapsayıcısı içinde BLOB'ları Listele</span><span class="sxs-lookup"><span data-stu-id="d28f0-174">List the blobs in a blob container</span></span>

<span data-ttu-id="d28f0-175">Bu bölümde, bir blob kapsayıcısı içinde BLOB'ları listesi göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="d28f0-176">Örnek kod başvurularını *test blob kapsayıcısı* bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="d28f0-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="d28f0-177">Bu bölümdeki kod bölümündeki adımları tamamladınız varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="d28f0-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="d28f0-178">`BlobsController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="d28f0-179">Adlı bir yöntem ekleyin **ListBlobs** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="d28f0-180">İçinde **ListBlobs** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d28f0-181">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="d28f0-182">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d28f0-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="d28f0-183">Alma bir **CloudBlobContainer** blob kapsayıcı adı için başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="d28f0-184">Blob kapsayıcısı içinde BLOB'ları listelemek için kullanın **CloudBlobContainer.ListBlobs** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="d28f0-185">**CloudBlobContainer.ListBlobs** yöntemi döndürür bir **Ilistblobıtem** için cast nesnesi bir **CloudBlockBlob**, **CloudPageBlob**, veya **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="d28f0-186">Aşağıdaki kod parçacığını bir blob kapsayıcıdaki tüm blob'lara numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="d28f0-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="d28f0-187">Her bir blob türü ve onun adına göre uygun nesnesine cast (veya URI durumunda bir **CloudBlobDirectory**) bir listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

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

    <span data-ttu-id="d28f0-188">BLOB'ları yanı sıra blob kapsayıcıları dizinleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d28f0-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="d28f0-189">Şimdi adlı bir blob kapsayıcıya sahip varsayalım *test blob kapsayıcısı* aşağıdaki hiyerarşi ile:</span><span class="sxs-lookup"><span data-stu-id="d28f0-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="d28f0-190">Önceki kod örneğinde kullanarak **BLOB'lar** dize listesi aşağıdakine benzer değerleri içerir:</span><span class="sxs-lookup"><span data-stu-id="d28f0-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="d28f0-191">Gördüğünüz gibi yalnızca üst düzey varlıklar listesi içerir; iç içe geçmiş olanlar (*bar.png* ve *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="d28f0-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="d28f0-192">Bir blob kapsayıcı içindeki tüm varlıkları listelemek için çağırmalısınız **CloudBlobContainer.ListBlobs** yöntemi ve geçişi **true** için **Listblobs** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="d28f0-193">Ayarı **Listblobs** parametresi **true** blob kapsayıcısında tüm varlıkların düz bir liste döndürür ve aşağıdaki sonuçları verir:</span><span class="sxs-lookup"><span data-stu-id="d28f0-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="d28f0-194">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="d28f0-195">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ListBlobs** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="d28f0-196">Açık `ListBlobs.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d28f0-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="d28f0-197">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d28f0-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="d28f0-198">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="d28f0-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="d28f0-199">Uygulamayı çalıştırmak ve seçmek **listesinde BLOB'lar** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="d28f0-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![BLOB listeleme](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="d28f0-201">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="d28f0-201">Download blobs</span></span>

<span data-ttu-id="d28f0-202">Bu bölümde bir blob indirmek nasıl gösterir ve yerel depolama alanına ya da kalıcı olması veya bir dizeye içeriği okuyun.</span><span class="sxs-lookup"><span data-stu-id="d28f0-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="d28f0-203">Örnek kod başvurularını *test blob kapsayıcısı* bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="d28f0-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="d28f0-204">`BlobsController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="d28f0-205">Adlı bir yöntem ekleyin **DownloadBlob** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="d28f0-206">İçinde **DownloadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d28f0-207">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="d28f0-208">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d28f0-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="d28f0-209">Alma bir **CloudBlobContainer** blob kapsayıcı adı için başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="d28f0-210">Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="d28f0-211">(Değişiklik  *&lt;blob adı >* blob adını karşıdan yükleniyor.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="d28f0-212">Bir blob indirmek için kullanacağınız **CloudBlockBlob.DownloadToStream** veya **CloudPageBlob.DownloadToStream** blob türüne bağlı olarak yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="d28f0-213">Aşağıdaki kod parçacığını kullanır **CloudBlockBlob.DownloadToStream** yöntemi bir blob'un içeriği sonra yerel bir dosyaya kalıcı bir akış nesnesine aktarmak için: (değişiklik  *&lt;yerel dosya adı >* tam dosya adı blob istediğiniz temsil eden indirilen.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="d28f0-214">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d28f0-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="d28f0-215">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="d28f0-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="d28f0-216">Uygulamayı çalıştırmak ve seçmek **indirme blob** blob indirmek için.</span><span class="sxs-lookup"><span data-stu-id="d28f0-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="d28f0-217">Belirtilen blob **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı indirir, belirttiğiniz konuma **File.OpenWrite** yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="d28f0-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="d28f0-218">Blob’ları silme</span><span class="sxs-lookup"><span data-stu-id="d28f0-218">Delete blobs</span></span>

<span data-ttu-id="d28f0-219">Aşağıdaki adımlar bir blobu silmek nasıl gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d28f0-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="d28f0-220">Bu bölümdeki kod bölümündeki adımları tamamladınız varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="d28f0-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="d28f0-221">`BlobsController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d28f0-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="d28f0-222">Adlı bir yöntem ekleyin **DeleteBlob** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="d28f0-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="d28f0-223">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d28f0-224">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="d28f0-225">Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d28f0-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="d28f0-226">Alma bir **CloudBlobContainer** blob kapsayıcı adı için başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d28f0-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="d28f0-227">Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d28f0-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="d28f0-228">(Değişiklik  *&lt;blob adı >* blob adını silmekte olduğunuz.)</span><span class="sxs-lookup"><span data-stu-id="d28f0-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="d28f0-229">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d28f0-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="d28f0-230">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="d28f0-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="d28f0-231">Uygulamayı çalıştırmak ve seçmek **Delete blob** belirtilen blobu silmek için **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="d28f0-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d28f0-232">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d28f0-232">Next steps</span></span>
<span data-ttu-id="d28f0-233">Azure’da veri depolama ile ilgili ek seçenekler hakkında daha fazla bilgi edinmek için daha fazla özellik kılavuzu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d28f0-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="d28f0-234">Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d28f0-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="d28f0-235">Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d28f0-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)

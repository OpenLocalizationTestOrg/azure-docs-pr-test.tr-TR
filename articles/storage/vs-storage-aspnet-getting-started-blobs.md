---
title: "aaaGet başlatılan Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak tooa depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure blob storage kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış

Azure blob depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu öğretici, Azure blob storage kullanarak bazı genel senaryolar için toowrite ASP.NET kodu nasıl gösterir. Bir blob kapsayıcısını oluşturma ve karşıya yükleme, listeleme, indirme ve BLOB'ları silme senaryolar içerir.

##<a name="prerequisites"></a>Ön koşullar

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure depolama hesabı](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Bir MVC denetleyicisi oluşturun. 

1. Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *BlobsController*seçip **Ekle**.

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `BlobsController.cs` dosyası:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Bir blob kapsayıcı oluşturun

Bir blob kapsayıcı, BLOB'ları ve klasörleri iç içe geçmiş bir hiyerarşisidir. Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcı:

> [!NOTE]
> 
> Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `BlobsController.cs` dosya.

1. Adlı bir yöntem ekleyin **CreateBlobContainer** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **CreateBlobContainer** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından aşağıdaki hello kullanın. (Değişiklik  *&lt;depolama hesabı adı >* hello erişme Azure depolama hesabı adını toohello.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Alma bir **CloudBlobContainer** bir başvuru toohello istenen blob kapsayıcı adı temsil eden nesne. Merhaba **CloudBlobClient.GetContainerReference** yöntemi blob Storage'a karşı istek yapmaz. Merhaba blob kapsayıcısı mevcut olup olmadığına bakılmaksızın hello başvuru döndürülür. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Merhaba çağrısı **CloudBlobContainer.CreateIfNotExists** henüz yoksa, yöntem toocreate hello kapsayıcı. Merhaba **CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **true** hello kapsayıcısı yok ve başarıyla oluşturuldu. Aksi takdirde, **false** döndürülür.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Güncelleştirme hello **ViewBag** hello blob kapsayıcısının hello ada sahip.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateBlobContainer** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `CreateBlobContainer.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **Blob kapsayıcısı oluşturmak** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![BLOB kapsayıcı oluşturun](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Daha önce belirtildiği gibi hello **CloudBlobContainer.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello kapsayıcısı yok ve oluşturulur. Bu nedenle, hello kapsayıcı mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**. toorun hello uygulama birden çok kez, hello kapsayıcı hello uygulama yeniden çalıştırmadan önce silmeniz gerekir. Silme hello kapsayıcı hello yapılabilir **CloudBlobContainer.Delete** yöntemi. Merhaba kapsayıcı hello kullanarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Bir blob kapsayıcıya bir blob karşıya yükleme

Seçtiğiniz sonra [bir blob kapsayıcısını oluşturulan](#create-a-blob-container), bu kapsayıcıya dosyaları karşıya yükleyebilir. Bu bölümde, bir yerel dosya tooa blob kapsayıcısı karşıya aracılığıyla açıklanmaktadır. Merhaba adımlar varsayar adlı bir blob kapsayıcı oluşturduğunuz *test blob kapsayıcısı*. 

> [!NOTE]
> 
> Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `BlobsController.cs` dosya.

1. Adlı bir yöntem ekleyin **UploadBlob** döndüren bir **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Merhaba içinde **UploadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Daha önce açıklandığı gibi Azure depolama farklı blob türlerini destekler. tooretrieve bir başvuru tooa sayfa blob'u çağrısı hello **CloudBlobContainer.GetPageBlobReference** yöntemi. tooretrieve bir başvuru tooa blok blobu çağrısı hello **CloudBlobContainer.GetBlockBlobReference** yöntemi. Genellikle, blok blob türü toouse önerilen hello olur. (Değiştir < blob-adı > * kez karşıya toogive hello blob istediğiniz toohello ad.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Bir blob başvurusu edindiğinizde hello blob başvurusu nesnenin çağırarak tüm veri akışı tooit yükleyebilirsiniz **UploadFromStream** yöntemi. Merhaba **UploadFromStream** yöntemi, mevcut değil veya mevcut değilse bu raporun üzerine hello blob oluşturur. (Değişiklik  *&lt;dosya karşıya yükleme >* tooa tooupload istediğiniz yolun toohello dosyasını tam.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **karşıya yükleme blob**.  
  
Merhaba bölüm - [listesinde bir blob kapsayıcısında hello BLOB'lar](#list-the-blobs-in-a-blob-container) -toolist hello bir blob kapsayıcısında nasıl BLOB'gösterilmektedir.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Bir blob kapsayıcısında listesi hello BLOB'ları

Bu bölümde, nasıl bir blob kapsayıcısında toolist hello BLOB gösterilmektedir. Merhaba örnek kod başvuran hello *test blob kapsayıcısı* hello bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).

> [!NOTE]
> 
> Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `BlobsController.cs` dosya.

1. Adlı bir yöntem ekleyin **ListBlobs** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **ListBlobs** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. bir blob kapsayıcısında toolist hello BLOB'ları kullanmak hello **CloudBlobContainer.ListBlobs** yöntemi. Merhaba **CloudBlobContainer.ListBlobs** yöntemi döndürür bir **Ilistblobıtem** tooa cast nesne **CloudBlockBlob**, **CloudPageBlob**, veya **CloudBlobDirectory** nesnesi. Merhaba aşağıdaki kod parçacığını bir blob kapsayıcısında tüm hello BLOB'lar numaralandırır. Cast toohello uygun nesne türünü ve onun adına göre her bir blob olduğunu (veya URI hello durumda bir **CloudBlobDirectory**) tooa listesine eklenir.

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

    Toplama tooblobs içinde blob kapsayıcıları dizinleri içerebilir. Şimdi adlı bir blob kapsayıcıya sahip varsayalım *test blob kapsayıcısı* hiyerarşi aşağıdaki hello ile:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Önceki kod örneğinde hello kullanarak hello **BLOB'lar** dize liste değerleri benzer toohello aşağıdakileri içerir:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Gördüğünüz gibi hello listesi yalnızca hello en üst düzey varlıkları içerir; değil hello olanları iç içe (*bar.png* ve *baz.png*). toolist tüm varlıkları bir blob kapsayıcı içindeki Merhaba, hello çağırmalısınız **CloudBlobContainer.ListBlobs** yöntemi ve geçişi **true** hello için **Listblobs** parametre.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Ayar hello **Listblobs** parametresi çok**true** hello blob kapsayıcısında tüm varlıkların düz bir liste döndürür ve sonuçları aşağıdaki hello verir:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **BLOB'lar**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ListBlobs** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `ListBlobs.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **listesinde BLOB'lar** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![BLOB listeleme](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Blob’ları indirme

Bu bölümde, nasıl toodownload blob ve ya da onu toolocal depolama veya okuma hello içeriği bir dizeye kalıcı olmasını gösterilmektedir. Merhaba örnek kod başvuran hello *test blob kapsayıcısı* hello bölümünde oluşturduğunuz [bir blob kapsayıcı oluşturun](#create-a-blob-container).

1. Açık hello `BlobsController.cs` dosya.

1. Adlı bir yöntem ekleyin **DownloadBlob** döndüren bir **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Merhaba içinde **DownloadBlob** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi. (Değişiklik  *&lt;blob adı >* indirme hello blob adını toohello.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload bir blob kullanmak hello **CloudBlockBlob.DownloadToStream** veya **CloudPageBlob.DownloadToStream** hello blob türüne bağlı olarak yöntemi. Merhaba aşağıdaki kod parçacığını kullanan hello **CloudBlockBlob.DownloadToStream** yöntemi tootransfer bir blob'un içeriği tooa akış nesnesi başka bir deyişle, ardından tooa yerel dosya kalıcı: (değişiklik  *&lt;yerel dosya adı >* toohello tam indirilen hello blob istediğiniz dosya adını temsil eden.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **indirme blob** toodownload hello blob. Hello belirtilen hello blob **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı indirmeleri hello belirttiğiniz toohello konumu **File.OpenWrite** yöntem çağrısı. 

## <a name="delete-blobs"></a>Blob’ları silme

Merhaba aşağıdaki adımları göstermek nasıl toodelete blob:

> [!NOTE]
> 
> Merhaba kod bu bölümdeki hello bölümdeki hello adımları tamamladınız varsayar [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `BlobsController.cs` dosya.

1. Adlı bir yöntem ekleyin **DeleteBlob** döndüren bir **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudBlobClient** nesnesi, bir blob hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Alma bir **CloudBlobContainer** bir başvuru toohello blob kapsayıcı adı temsil eden nesne. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Bir blob başvurusu nesnesi çağırarak alma **CloudBlobContainer.GetBlockBlobReference** veya **CloudBlobContainer.GetPageBlobReference** yöntemi. (Değişiklik  *&lt;blob adı >* silmekte hello blob adını toohello.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **Delete blob** toodelete hello blob hello belirtilen **CloudBlobContainer.GetBlockBlobReference** yöntem çağrısı. 

## <a name="next-steps"></a>Sonraki adımlar
Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.

  * [Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](./vs-storage-aspnet-getting-started-tables.md)
  * [Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](./vs-storage-aspnet-getting-started-queues.md)

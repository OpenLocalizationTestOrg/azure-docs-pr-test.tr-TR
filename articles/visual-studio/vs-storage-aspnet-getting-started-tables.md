---
title: "aaaGet başlatılan Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak tooa depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure tablo depolaması kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="6b4a4-103">Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6b4a4-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="6b4a4-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6b4a4-104">Overview</span></span>

<span data-ttu-id="6b4a4-105">Azure Table storage yapılandırılmış veri büyük miktarlarda toostore sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="6b4a4-106">Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="6b4a4-107">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="6b4a4-108">Bu öğretici, nasıl Azure tablo depolama varlıkları kullanarak bazı genel senaryolar için toowrite ASP.NET kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="6b4a4-109">Bu senaryolar, tablo oluşturma ve ekleme, sorgulama ve tablo varlıkları silme içerir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="6b4a4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6b4a4-110">Prerequisites</span></span>

* [<span data-ttu-id="6b4a4-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b4a4-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="6b4a4-112">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="6b4a4-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="6b4a4-113">Bir MVC denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="6b4a4-114">Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="6b4a4-116">Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="6b4a4-118">Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *TablesController*seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="6b4a4-120">Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `TablesController.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="6b4a4-121">Bir model sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b4a4-121">Create a model class</span></span>

<span data-ttu-id="6b4a4-122">Birçok hello örnekleri bu makaleyi kullanın bir **TableEntity**-türetilmiş sınıf adlı **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="6b4a4-123">Aşağıdaki adımları hello bir model sınıfı olarak bu sınıf bildirme aracılığıyla Kılavuzu:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="6b4a4-124">Merhaba, **Çözüm Gezgini**, sağ **modelleri**ve hello bağlam menüsünden seçin **Ekle -> sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="6b4a4-125">Merhaba üzerinde **Yeni Öğe Ekle** iletişim, ad hello sınıfını **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="6b4a4-126">Açık hello `CustomerEntity.cs` dosya ve hello aşağıdakileri ekleyin **kullanarak** yönergesi:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="6b4a4-127">Tamamlandığında, hello sınıfı koddan hello olduğu gibi bildirilmiş böylece hello sınıfı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="6b4a4-128">Merhaba sınıfı bildirir adlı bir varlık sınıfı **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını hello.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="6b4a4-129">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b4a4-129">Create a table</span></span>

<span data-ttu-id="6b4a4-130">Merhaba aşağıdaki adımları göstermek nasıl toocreate tablosu:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-131">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6b4a4-132">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-133">Adlı bir yöntem ekleyin **CreateTable** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-134">Merhaba içinde **CreateTable** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-135">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-136">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-137">Alma bir **CloudTable** başvuru toohello istenilen tablo adını temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="6b4a4-138">Merhaba **CloudTableClient.GetTableReference** yöntemi tablo depolama doğrulamasını yapmaz.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="6b4a4-139">Merhaba tablo var olup olmadığına bakılmaksızın hello başvuru döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-140">Merhaba çağrısı **CloudTable.CreateIfNotExists** henüz yoksa, yöntem toocreate hello tablo.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="6b4a4-141">Merhaba **CloudTable.CreateIfNotExists** yöntemi döndürür **true** hello tablo mevcut değil ve başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="6b4a4-142">Aksi takdirde, **false** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="6b4a4-143">Güncelleştirme hello **ViewBag** Merhaba tablonun hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="6b4a4-144">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-145">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateTable** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-146">Açık `CreateTable.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="6b4a4-147">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-148">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-149">Merhaba uygulamayı çalıştırın ve seçin **Create table** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Tablo oluşturma](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="6b4a4-151">Daha önce belirtildiği gibi hello **CloudTable.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello tablo mevcut değil ve oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="6b4a4-152">Bu nedenle, hello tablo mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="6b4a4-153">toorun hello uygulama birden çok kez, hello tablo hello uygulama yeniden çalıştırmadan önce silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="6b4a4-154">Silme hello tablo hello yapılabilir **CloudTable.Delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="6b4a4-155">Hello kullanarak hello tablosu silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="6b4a4-156">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="6b4a4-156">Add an entity tooa table</span></span>

<span data-ttu-id="6b4a4-157">*Varlıkları* tooC eşleme\# özel bir sınıf kullanarak nesneleri türetilen **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="6b4a4-158">bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="6b4a4-159">Bu bölümde, nasıl toodefine kullanan bir varlık sınıfı hello hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="6b4a4-160">Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="6b4a4-161">Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlı varlıklara göre daha hızlı sorgulanabilir ancak farklı bölüm anahtarlarının kullanılması paralel işlemler için daha büyük ölçeklendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="6b4a4-162">Merhaba tablo hizmetinde depolanması gereken tüm özellikler için hello özelliğini ayarlarken ve değerlerini alma kullanıma sunan desteklenen bir tür genel özelliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="6b4a4-163">Merhaba varlık sınıfı *gerekir* genel bir parametresiz oluşturucuya bildirin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-164">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="6b4a4-165">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-166">Merhaba kodda hello şekilde yönergesi aşağıdaki hello eklemek `TablesController.cs` dosya hello erişebilir **CustomerEntity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="6b4a4-167">Adlı bir yöntem ekleyin **AddEntity** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-168">Merhaba içinde **AddEntity** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-169">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-170">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-171">Alma bir **CloudTable** tooadd hello yeni varlık bulacağınızı başvuru toohello tablo toowhich temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-172">Örneği ve hello başlatma **CustomerEntity** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="6b4a4-173">Oluşturma bir **TableOperation** hello müşteri varlığı ekler nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="6b4a4-174">Merhaba ekleme işlemi tarafından arama hello yürütme **CloudTable.Execute** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="6b4a4-175">Merhaba inceleyerek hello işleminin hello sonucu doğrulayabilirsiniz **TableResult.HttpStatusCode** özelliği.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="6b4a4-176">Merhaba eylemin hello istemci tarafından istenilen başarıyla işlendi 2xx durum kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="6b4a4-177">Örneğin, yeni varlıkların başarılı eklemeler, bir HTTP durum kodunu hello işlemi başarıyla işlendi ve hello sunucu herhangi bir içerik döndürmedi anlamına 204 sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="6b4a4-178">Güncelleştirme hello **ViewBag** hello tablo adı ve hello ekleme işlemi hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="6b4a4-179">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-180">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddEntity** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-181">Açık `AddEntity.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="6b4a4-182">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-183">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-184">Merhaba uygulamayı çalıştırın ve seçin **varlık ekleme** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Varlık ekleme](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="6b4a4-186">Merhaba varlık hello bölümdeki hello adımları izleyerek eklendiğini doğrulayabilirsiniz [tek bir varlık alma](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="6b4a4-187">Merhaba de kullanabilirsiniz [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tüm, tablolar için varlıklar hello.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="6b4a4-188">Varlıkları tooa tablo toplu ekleme</span><span class="sxs-lookup"><span data-stu-id="6b4a4-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="6b4a4-189">Toplama toobeing mümkün içinde çok[bir varlık tooa tablo biri aynı anda eklemek](#add-an-entity-to-a-table), varlıkları toplu işlemde de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="6b4a4-190">Toplu işlemde varlıklar ekleme kodu ve hello Azure tablo hizmeti arasındaki gidiş dönüş hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="6b4a4-191">Aşağıdaki adımları hello nasıl tooadd birden çok varlık tooa tablo ile tek ekleme işlemi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-192">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="6b4a4-193">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-194">Adlı bir yöntem ekleyin **AddEntities** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-195">Merhaba içinde **AddEntities** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-196">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-197">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-198">Alma bir **CloudTable** giderek tooadd hello yeni varlıklar olduğunuz bir başvuru toohello tablo toowhich temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-199">Bazı müşteri nesneler üzerinde Hello örneği **CustomerEntity** model hello bölümde sunulan sınıfı [bir varlık tooa tablo eklemek](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="6b4a4-200">Alma bir **TableBatchOperation** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="6b4a4-201">Varlıkları toohello toplu ekleme işlemi nesnesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="6b4a4-202">Merhaba toplu ekleme işlemi tarafından arama hello yürütme **CloudTable.ExecuteBatch** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="6b4a4-203">Merhaba **CloudTable.ExecuteBatch** yöntemi listesini döndürür **TableResult** nesneleri burada her **TableResult** nesne incelenmesi toodetermine hello başarılı veya başarısız olabilir tek tek her işlemi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="6b4a4-204">Bu örnek için hello liste tooa görünümü geçirmek ve her işlemin hello sonuçları görüntüleme hello görünüm izin verin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="6b4a4-205">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-206">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddEntities** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-207">Açık `AddEntities.cshtml`ve hello şuna benzeyen şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="6b4a4-208">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-209">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-210">Merhaba uygulamayı çalıştırın ve seçin **varlıkları ekleyin** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Varlık ekleme](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="6b4a4-212">Merhaba varlık hello bölümdeki hello adımları izleyerek eklendiğini doğrulayabilirsiniz [tek bir varlık alma](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="6b4a4-213">Merhaba de kullanabilirsiniz [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tüm, tablolar için varlıklar hello.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="6b4a4-214">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="6b4a4-214">Get a single entity</span></span>

<span data-ttu-id="6b4a4-215">Bu bölümde, nasıl tooget tablo kullanarak tek bir varlık hello varlığın satır anahtarı ve bölüm anahtarı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-216">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6b4a4-217">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-218">Adlı bir yöntem ekleyin **GetSingle** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-219">Merhaba içinde **GetSingle** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-220">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-221">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-222">Alma bir **CloudTable** içinden, alma hello varlık başvurusu toohello tablo temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-223">Türetilen bir varlık nesnesini alır bir alma işlemi nesnesi oluşturmak **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="6b4a4-224">Merhaba ilk parametredir hello *partitionKey*, ve hello ikinci parametre hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="6b4a4-225">Hello kullanarak **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table), hello aşağıdaki kod parçacığını sorguları hello tablo için bir **CustomerEntity** varlıkla bir *partitionKey* "Smith" değerini ve *rowKey* "Ben" değeri:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="6b4a4-226">Merhaba alma işlemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="6b4a4-227">Merhaba sonuç toohello görünümünü görüntülemek için geçirin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="6b4a4-228">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-229">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetSingle** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-230">Açık `GetSingle.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="6b4a4-231">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-232">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-233">Merhaba uygulamayı çalıştırın ve seçin **alma tek** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Tek Al](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="6b4a4-235">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="6b4a4-235">Get all entities in a partition</span></span>

<span data-ttu-id="6b4a4-236">Merhaba bölümünde belirtildiği gibi [bir varlık tooa tablo eklemek](#add-an-entity-to-a-table), bir bölüm ve satır anahtarını hello birleşimi benzersiz şekilde tanımlamak bir tablodaki bir varlık.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="6b4a4-237">Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlarının varlıklar daha hızlı sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="6b4a4-238">Bu bölümde anlatılacaktır nasıl tooquery belirtilen bölümünden tüm hello varlıklar için bir tablo.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-239">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6b4a4-240">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-241">Adlı bir yöntem ekleyin **GetPartition** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-242">Merhaba içinde **GetPartition** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-243">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-244">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-245">Alma bir **CloudTable** içinden, alma hello varlıklar bir başvuru toohello tablosu temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-246">Örneği bir **TableQuery** hello hello sorgu belirten nesnesini **burada** yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="6b4a4-247">Hello kullanarak **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table), hello aşağıdaki kod parçacığını sorguları hello tablosu tüm varlıklar için hello burada  **PartitionKey** (müşterinin soyadı) "Smith" değerine sahip:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="6b4a4-248">Bir döngü içinde hello çağrısı **CloudTable.ExecuteQuerySegmented** hello önceki adımda, örneği hello sorgu nesnesi geçirme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="6b4a4-249">Merhaba **CloudTable.ExecuteQuerySegmented** yöntemi döndürür bir **TableContinuationToken** - nesnesinin zaman **null** -daha fazla varlık yok gösterir tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="6b4a4-250">Merhaba döngü içinde başka bir döngü tooiterate varlıklar döndürülen hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="6b4a4-251">Aşağıdaki kod örneğine hello her döndürülen varlığı tooa listesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="6b4a4-252">Bir kez döngü sona erer Merhaba, hello listesi görüntü tooa görünümünü geçirilir:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="6b4a4-253">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-254">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetPartition** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-255">Açık `GetPartition.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="6b4a4-256">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-257">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-258">Merhaba uygulamayı çalıştırın ve seçin **alma bölüm** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Bölüm alma](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="6b4a4-260">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="6b4a4-260">Delete an entity</span></span>

<span data-ttu-id="6b4a4-261">Bu bölümde anlatılacaktır nasıl toodelete bir tablodan bir varlık.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6b4a4-262">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6b4a4-263">Açık hello `TablesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6b4a4-264">Adlı bir yöntem ekleyin **DeleteEntity** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6b4a4-265">Merhaba içinde **DeleteEntity** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6b4a4-266">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="6b4a4-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6b4a4-267">Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6b4a4-268">Alma bir **CloudTable** içinden silmekte hello varlık başvurusu toohello tablo temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6b4a4-269">Türetilen bir varlık nesnesini alır bir silme işlemi nesnesi oluşturmak **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="6b4a4-270">Bu durumda, hello kullanırız **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6b4a4-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="6b4a4-271">Merhaba varlığın **ETag** tooa geçerli bir değer ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="6b4a4-272">Merhaba silme işlemini yürütün.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="6b4a4-273">Merhaba sonuç toohello görünümünü görüntülemek için geçirin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="6b4a4-274">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6b4a4-275">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **DeleteEntity** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6b4a4-276">Açık `DeleteEntity.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="6b4a4-277">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6b4a4-278">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="6b4a4-279">Merhaba uygulamayı çalıştırın ve seçin **silmek varlık** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="6b4a4-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Tek Al](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="6b4a4-281">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b4a4-281">Next steps</span></span>
<span data-ttu-id="6b4a4-282">Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6b4a4-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="6b4a4-283">Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6b4a4-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="6b4a4-284">Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6b4a4-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)

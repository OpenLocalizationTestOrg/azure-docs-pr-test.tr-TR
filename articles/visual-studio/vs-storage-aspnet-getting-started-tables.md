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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Genel Bakış

Azure Table storage yapılandırılmış veri büyük miktarlarda toostore sağlar. Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.

Bu öğretici, nasıl Azure tablo depolama varlıkları kullanarak bazı genel senaryolar için toowrite ASP.NET kodu gösterir. Bu senaryolar, tablo oluşturma ve ekleme, sorgulama ve tablo varlıkları silme içerir. 

##<a name="prerequisites"></a>Ön koşullar

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Bir MVC denetleyicisi oluşturun. 

1. Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *TablesController*seçip **Ekle**.

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `TablesController.cs` dosyası:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Bir model sınıfı oluşturma

Birçok hello örnekleri bu makaleyi kullanın bir **TableEntity**-türetilmiş sınıf adlı **CustomerEntity**. Aşağıdaki adımları hello bir model sınıfı olarak bu sınıf bildirme aracılığıyla Kılavuzu:

1. Merhaba, **Çözüm Gezgini**, sağ **modelleri**ve hello bağlam menüsünden seçin **Ekle -> sınıfı**.

1. Merhaba üzerinde **Yeni Öğe Ekle** iletişim, ad hello sınıfını **CustomerEntity**.

1. Açık hello `CustomerEntity.cs` dosya ve hello aşağıdakileri ekleyin **kullanarak** yönergesi:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Tamamlandığında, hello sınıfı koddan hello olduğu gibi bildirilmiş böylece hello sınıfı değiştirin. Merhaba sınıfı bildirir adlı bir varlık sınıfı **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını hello.

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

## <a name="create-a-table"></a>Bir tablo oluşturma

Merhaba aşağıdaki adımları göstermek nasıl toocreate tablosu:

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `TablesController.cs` dosya.

1. Adlı bir yöntem ekleyin **CreateTable** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **CreateTable** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** başvuru toohello istenilen tablo adını temsil eden nesne. Merhaba **CloudTableClient.GetTableReference** yöntemi tablo depolama doğrulamasını yapmaz. Merhaba tablo var olup olmadığına bakılmaksızın hello başvuru döndürülür. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Merhaba çağrısı **CloudTable.CreateIfNotExists** henüz yoksa, yöntem toocreate hello tablo. Merhaba **CloudTable.CreateIfNotExists** yöntemi döndürür **true** hello tablo mevcut değil ve başarıyla oluşturuldu. Aksi takdirde, **false** döndürülür.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Güncelleştirme hello **ViewBag** Merhaba tablonun hello ada sahip.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateTable** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `CreateTable.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **Create table** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Tablo oluşturma](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Daha önce belirtildiği gibi hello **CloudTable.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello tablo mevcut değil ve oluşturulur. Bu nedenle, hello tablo mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**. toorun hello uygulama birden çok kez, hello tablo hello uygulama yeniden çalıştırmadan önce silmeniz gerekir. Silme hello tablo hello yapılabilir **CloudTable.Delete** yöntemi. Hello kullanarak hello tablosu silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme

*Varlıkları* tooC eşleme\# özel bir sınıf kullanarak nesneleri türetilen **TableEntity**. bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun. Bu bölümde, nasıl toodefine kullanan bir varlık sınıfı hello hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını görürsünüz. Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar. Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlı varlıklara göre daha hızlı sorgulanabilir ancak farklı bölüm anahtarlarının kullanılması paralel işlemler için daha büyük ölçeklendirme sağlar. Merhaba tablo hizmetinde depolanması gereken tüm özellikler için hello özelliğini ayarlarken ve değerlerini alma kullanıma sunan desteklenen bir tür genel özelliği olmalıdır.
Merhaba varlık sınıfı *gerekir* genel bir parametresiz oluşturucuya bildirin.

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).

1. Açık hello `TablesController.cs` dosya.

1. Merhaba kodda hello şekilde yönergesi aşağıdaki hello eklemek `TablesController.cs` dosya hello erişebilir **CustomerEntity** sınıfı:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Adlı bir yöntem ekleyin **AddEntity** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **AddEntity** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** tooadd hello yeni varlık bulacağınızı başvuru toohello tablo toowhich temsil eden nesne. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Örneği ve hello başlatma **CustomerEntity** sınıfı.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Oluşturma bir **TableOperation** hello müşteri varlığı ekler nesne.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Merhaba ekleme işlemi tarafından arama hello yürütme **CloudTable.Execute** yöntemi. Merhaba inceleyerek hello işleminin hello sonucu doğrulayabilirsiniz **TableResult.HttpStatusCode** özelliği. Merhaba eylemin hello istemci tarafından istenilen başarıyla işlendi 2xx durum kodu gösterir. Örneğin, yeni varlıkların başarılı eklemeler, bir HTTP durum kodunu hello işlemi başarıyla işlendi ve hello sunucu herhangi bir içerik döndürmedi anlamına 204 sonuçlanır.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Güncelleştirme hello **ViewBag** hello tablo adı ve hello ekleme işlemi hello sonuçları.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddEntity** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `AddEntity.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **varlık ekleme** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Varlık ekleme](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Merhaba varlık hello bölümdeki hello adımları izleyerek eklendiğini doğrulayabilirsiniz [tek bir varlık alma](#get-a-single-entity). Merhaba de kullanabilirsiniz [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tüm, tablolar için varlıklar hello.

## <a name="add-a-batch-of-entities-tooa-table"></a>Varlıkları tooa tablo toplu ekleme

Toplama toobeing mümkün içinde çok[bir varlık tooa tablo biri aynı anda eklemek](#add-an-entity-to-a-table), varlıkları toplu işlemde de ekleyebilirsiniz. Toplu işlemde varlıklar ekleme kodu ve hello Azure tablo hizmeti arasındaki gidiş dönüş hello sayısını azaltır. Aşağıdaki adımları hello nasıl tooadd birden çok varlık tooa tablo ile tek ekleme işlemi gösterilmektedir:

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).

1. Açık hello `TablesController.cs` dosya.

1. Adlı bir yöntem ekleyin **AddEntities** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **AddEntities** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** giderek tooadd hello yeni varlıklar olduğunuz bir başvuru toohello tablo toowhich temsil eden nesne. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Bazı müşteri nesneler üzerinde Hello örneği **CustomerEntity** model hello bölümde sunulan sınıfı [bir varlık tooa tablo eklemek](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Alma bir **TableBatchOperation** nesnesi.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Varlıkları toohello toplu ekleme işlemi nesnesi ekleyin.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Merhaba toplu ekleme işlemi tarafından arama hello yürütme **CloudTable.ExecuteBatch** yöntemi.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Merhaba **CloudTable.ExecuteBatch** yöntemi listesini döndürür **TableResult** nesneleri burada her **TableResult** nesne incelenmesi toodetermine hello başarılı veya başarısız olabilir tek tek her işlemi. Bu örnek için hello liste tooa görünümü geçirmek ve her işlemin hello sonuçları görüntüleme hello görünüm izin verin. 
 
    ```csharp
    return View(results);
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddEntities** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `AddEntities.cshtml`ve hello şuna benzeyen şekilde değiştirin.

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **varlıkları ekleyin** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Varlık ekleme](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Merhaba varlık hello bölümdeki hello adımları izleyerek eklendiğini doğrulayabilirsiniz [tek bir varlık alma](#get-a-single-entity). Merhaba de kullanabilirsiniz [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tüm, tablolar için varlıklar hello.

## <a name="get-a-single-entity"></a>Tek bir varlık alma

Bu bölümde, nasıl tooget tablo kullanarak tek bir varlık hello varlığın satır anahtarı ve bölüm anahtarı gösterilmektedir. 

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table). 

1. Açık hello `TablesController.cs` dosya.

1. Adlı bir yöntem ekleyin **GetSingle** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **GetSingle** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** içinden, alma hello varlık başvurusu toohello tablo temsil eden nesne. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Türetilen bir varlık nesnesini alır bir alma işlemi nesnesi oluşturmak **TableEntity**. Merhaba ilk parametredir hello *partitionKey*, ve hello ikinci parametre hello *rowKey*. Hello kullanarak **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table), hello aşağıdaki kod parçacığını sorguları hello tablo için bir **CustomerEntity** varlıkla bir *partitionKey* "Smith" değerini ve *rowKey* "Ben" değeri:

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Merhaba alma işlemi yürütün.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Merhaba sonuç toohello görünümünü görüntülemek için geçirin.

    ```csharp
    return View(result);
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetSingle** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `GetSingle.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **alma tek** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Tek Al](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Tüm varlıkları bir bölüme alma

Merhaba bölümünde belirtildiği gibi [bir varlık tooa tablo eklemek](#add-an-entity-to-a-table), bir bölüm ve satır anahtarını hello birleşimi benzersiz şekilde tanımlamak bir tablodaki bir varlık. Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlarının varlıklar daha hızlı sorgulanabilir. Bu bölümde anlatılacaktır nasıl tooquery belirtilen bölümünden tüm hello varlıklar için bir tablo.  

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table). 

1. Açık hello `TablesController.cs` dosya.

1. Adlı bir yöntem ekleyin **GetPartition** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **GetPartition** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** içinden, alma hello varlıklar bir başvuru toohello tablosu temsil eden nesne. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Örneği bir **TableQuery** hello hello sorgu belirten nesnesini **burada** yan tümcesi. Hello kullanarak **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table), hello aşağıdaki kod parçacığını sorguları hello tablosu tüm varlıklar için hello burada  **PartitionKey** (müşterinin soyadı) "Smith" değerine sahip:

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Bir döngü içinde hello çağrısı **CloudTable.ExecuteQuerySegmented** hello önceki adımda, örneği hello sorgu nesnesi geçirme yöntemi.  Merhaba **CloudTable.ExecuteQuerySegmented** yöntemi döndürür bir **TableContinuationToken** - nesnesinin zaman **null** -daha fazla varlık yok gösterir tooretrieve. Merhaba döngü içinde başka bir döngü tooiterate varlıklar döndürülen hello kullanın. Aşağıdaki kod örneğine hello her döndürülen varlığı tooa listesi eklenir. Bir kez döngü sona erer Merhaba, hello listesi görüntü tooa görünümünü geçirilir: 

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetPartition** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `GetPartition.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **alma bölüm** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Bölüm alma](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Bir varlığı silme

Bu bölümde anlatılacaktır nasıl toodelete bir tablodan bir varlık.

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment)ve verileri kullanan [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table). 

1. Açık hello `TablesController.cs` dosya.

1. Adlı bir yöntem ekleyin **DeleteEntity** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **DeleteEntity** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudTableClient** nesnesi bir tablo hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Alma bir **CloudTable** içinden silmekte hello varlık başvurusu toohello tablo temsil eden nesne. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Türetilen bir varlık nesnesini alır bir silme işlemi nesnesi oluşturmak **TableEntity**. Bu durumda, hello kullanırız **CustomerEntity** sınıf ve hello bölümde sunulan veri [varlıklar tooa tablo toplu ekleme](#add-a-batch-of-entities-to-a-table). Merhaba varlığın **ETag** tooa geçerli bir değer ayarlamanız gerekir.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Merhaba silme işlemini yürütün.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Merhaba sonuç toohello görünümünü görüntülemek için geçirin.

    ```csharp
    return View(result);
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **tabloları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **DeleteEntity** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `DeleteEntity.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **silmek varlık** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Tek Al](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Sonraki adımlar
Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.

  * [Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](../storage/vs-storage-aspnet-getting-started-queues.md)

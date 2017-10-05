---
title: "Sanal makinede çalışan MongoDB’ye bağlanan Azure web uygulaması oluşturma"
description: "Git bir ASP.NET uygulamasını Azure App Service'e dağıtmak için nasıl kullanılacağını öğretilmektedir öğretici MongoDB üzerinde bir Azure sanal makinesine bağlı."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a>Sanal makinede çalışan MongoDB’ye bağlanan Azure web uygulaması oluşturma
Git kullanarak Azure App Service Web Apps için bir ASP.NET uygulamasını dağıtabilirsiniz. Bu öğreticide, basit bir ön uç ASP.NET MVC azure'da sanal makine üzerinde çalışan bir MongoDB veritabanına bağlayan görev listesi uygulaması oluşturacaksınız.  [MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanı. Çalıştıran ve ASP.NET uygulama geliştirme bilgisayarınızda testi sonra App Service Web Apps Git kullanarak uygulamaya karşıya yükler.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="background-knowledge"></a>Arka plan bilgisi
Aşağıdaki bilgisi gerekli değildir ancak bu öğretici için yararlıdır:

* C# sürücüsü MongoDB için. MongoDB MongoDB karşı C# uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [CSharp dil Merkezi][MongoC#LangCenter]. 
* ASP .NET web uygulama çerçevesidir. Tüm adresinden hakkında bilgi alabilirsiniz [ASP.net Web sitesi][ASP.NET].
* ASP .NET MVC web uygulama çerçevesidir. Tüm adresinden hakkında bilgi alabilirsiniz [ASP.NET MVC Web][MVCWebSite].
* kullanıyoruz. Bilgi başlayabiliriz [Azure][WindowsAzure].

## <a name="prerequisites"></a>Ön koşullar
* [Web için Visual Studio Express 2013] [ VSEWeb] veya [Visual Studio 2013][VSUlt]
* [.NET için Azure SDK](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Etkin bir Microsoft Azure aboneliği

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Bir sanal makine oluşturun ve MongoDB yükleme
Bu öğretici, Azure'da bir sanal makine oluşturduğunuz varsayar. Sanal makineyi oluşturduktan sonra sanal makinede MongoDB yüklemeniz gerekir:

* Bir Windows sanal makine oluşturun ve MongoDB yüklemek için bkz: [Azure'da Windows Server çalıştıran bir sanal makinede yüklemek MongoDB][InstallMongoOnWindowsVM].

Azure'da sanal makine oluşturup MongoDB yüklü sonra uç belirtilen MongoDB için sanal makine ("testlinuxvm.cloudapp.net", örneğin) ve dış bağlantı noktasını DNS adını anımsamak emin olun.  Bu bilgiler daha sonra öğreticide gerekecektir.

<a id="createapp"></a>

## <a name="create-the-application"></a>Uygulama oluşturma
Bu bölümde Visual Studio kullanarak "My görev listesi" adlı bir ASP.NET uygulaması oluşturun ve Azure App Service Web Apps için ilk bir dağıtım gerçekleştirin. Uygulamayı yerel olarak çalışır, ancak bunu Azure sanal makinenizde bağlanmak ve oluşturduğunuz MongoDB örneği burada kullanabilirsiniz.

1. Visual Studio'da sırasıyla **yeni proje**.
   
    ![Sayfa yeni bir proje başlatın][StartPageNewProject]
2. İçinde **yeni proje** penceresinde sol bölmesinde, **Visual C#**ve ardından **Web**. Orta bölmede seçin **ASP.NET Web uygulaması**. Projeniz "MyTaskListApp" alt kısmındaki adlandırın ve ardından **Tamam**.
   
    ![Yeni Proje İletişim Kutusu][NewProjectMyTaskListApp]
3. İçinde **yeni ASP.NET projesi** iletişim kutusunda **MVC**ve ardından **Tamam**.
   
    ![MVC şablonunu seçin][VS2013SelectMVCTemplate]
4. Microsoft Azure'da zaten oturumunuz açık değil, oturum açmak için istenir. Azure'da oturum için istemleri izleyin.
5. Oturum açtıktan sonra App Service web uygulamanızı yapılandırmaya başlayabilirsiniz. Belirtin **Web uygulaması adı**, **uygulama hizmeti planı**, **kaynak grubu**, ve **bölge**, ardından **oluşturma**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Azure App Service'te de belirtildiği gibi oluşturulması için web uygulaması projesi oluşturma tamamlandıktan sonra bekleyin **Azure App Service etkinliği** penceresi. Ardından **şimdi bu Web uygulaması yayımlama MyTaskListApp**.
7. **Yayımla**’ta tıklayın.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Varsayılan ASP.NET uygulamanızı Azure App Service Web Apps için yayımlandığında, tarayıcıda başlatılacak.

## <a name="install-the-mongodb-c-driver"></a>MongoDB C# sürücüsünü yükleyin
MongoDB yerel geliştirme bilgisayarınıza yüklemek için gereken bir sürücüyle C# uygulamaları için istemci tarafı desteği sağlar. C# sürücü NuGet kullanılabilir.

MongoDB C# sürücüyü yüklemek için:

1. İçinde **Çözüm Gezgini**, sağ **MyTaskListApp** proje ve seçin **yönetmek NuGetPackages**.
   
    ![NuGet paketlerini yönetme][VS2013ManageNuGetPackages]
2. İçinde **NuGet paketlerini Yönet** pencerede, sol bölmede, tıklayın **çevrimiçi**. İçinde **arama çevrimiçi** kutusuna sağ tarafta, "mongodb.driver" yazın.  Tıklatın **yükleme** sürücüyü yüklemek için.
   
    ![MongoDB C# sürücü arayın][SearchforMongoDBCSharpDriver]
3. Tıklatın **kabul ediyorum** 10gen, Inc. lisans koşullarını kabul etmek için.
4. Tıklatın **Kapat** sürücü yüklendikten sonra.
    ![MongoDB C# sürücüsünün yüklü][MongoDBCsharpDriverInstalled]

MongoDB C# sürücü artık yüklüdür.  Başvurular **MongoDB.Bson**, **MongoDB.Driver**, ve **MongoDB.Driver.Core** kitaplıkları projeye eklendi.

![MongoDB C# sürücü başvuruları][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Model ekleme
İçinde **Çözüm Gezgini**, sağ *modelleri* klasör ve **Ekle** yeni bir **sınıfı** ve adlandırın *TaskModel.cs*.  İçinde *TaskModel.cs*, var olan kodu aşağıdaki kodla değiştirin:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-the-data-access-layer"></a>Veri erişim katmanı ekleme
İçinde **Çözüm Gezgini**, sağ *MyTaskListApp* proje ve **Ekle** bir **yeni klasör** adlı *DAL*.  Sağ *DAL* klasör ve **Ekle** yeni bir **sınıfı**. Sınıf dosya adı *Dal.cs*.  İçinde *Dal.cs*, var olan kodu aşağıdaki kodla değiştirin:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into the collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>Denetleyici ekleme
Açık *Controllers\HomeController.cs* dosyasını **Çözüm Gezgini** ve var olan kodu aşağıdakilerle değiştirin:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-the-styles"></a>Stilleri ayarlama
Sayfanın üstündeki başlığını değiştirmek için açık *görünümler/paylaşılan\\_Layout.cshtml* dosyasını **Çözüm Gezgini** ve "Uygulama adı" navbar üstbilgisinde "My görev listesi ile değiştirin. Böyle uygulama"şekilde görünür:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Görev listesi menüsü Ayarla için açık *\Views\Home\Index.cshtml* dosya ve var olan kodu aşağıdaki kodla değiştirin:

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


Yeni bir görev oluşturma olanağı eklemek için sağ tıklatın *görünümler\\*  klasör ve **Ekle** bir **Görünüm**.  Görünüm adı *oluşturma*. Kod aşağıdakiyle değiştirin:

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Çözüm Gezgini** aşağıdaki gibi görünmelidir:

![Çözüm Gezgini][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a>MongoDB bağlantı dizesini ayarlayın
İçinde **Çözüm Gezgini**, açık *DAL/Dal.cs* dosya. Aşağıdaki kod satırını bulun:

    private string connectionString = "mongodb://<vm-dns-name>";

Değiştir `<vm-dns-name>` oluşturduğunuz MongoDB çalışan sanal makinenin DNS adı ile [bir sanal makine oluşturun ve MongoDB yükleme] [ Create a virtual machine and install MongoDB] Bu öğreticinin adımı.  Sanal makineniz DNS adını bulmak için select Azure Portalı'na Git **sanal makineleri**ve Bul **DNS adı**.

Sanal makinenin DNS adı "testlinuxvm.cloudapp.net" ise ve MongoDB 27017 varsayılan bağlantı noktasında dinleme bağlantı dizesi kod satırı ile gibi görünür:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Sanal makine uç noktası MongoDB için farklı bir dış bağlantı belirtiyorsa, bağlantı dizesindeki bağlantı noktası belirtin yapabilirsiniz:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

MongoDB bağlantı dizeleri hakkında daha fazla bilgi için bkz: [bağlantıları][MongoConnectionStrings].

## <a name="test-the-local-deployment"></a>Yerel dağıtımı test etme
Geliştirme bilgisayarınızda uygulamanızı çalıştırmak için seçin **hata ayıklamayı Başlat** gelen **hata ayıklama** menüsü veya isabet **F5**. IIS Express başlar ve bir tarayıcı açar ve uygulamanın giriş sayfasını açar.  Sanal makineniz azure'da çalışan MongoDB veritabanına eklenen yeni bir görev ekleyebilirsiniz.

![Görev listesi Uygulamam][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a>Azure App Service Web Apps için yayımlama
Bu bölümde Azure App Service Web Apps için yaptığınız değişiklikleri yayımlar.

1. Çözüm Gezgini'nde sağ **MyTaskListApp** yeniden tıklatıp **Yayımla**.
2. **Yayımla**’ta tıklayın.
   
    Web uygulamanızı Azure App Service içinde çalışan ve Azure Virtual Machines'de MongoDB veritabanı erişme görmelisiniz.

## <a name="summary"></a>Özet
ASP.NET uygulamanızı Azure App Service Web Apps için şimdi başarıyla dağıtmış. Web uygulaması görüntülemek için:

1. Azure portalı günlüğüne.
2. Tıklatın **Web uygulamaları**. 
3. Web uygulamanızı seçin **Web Apps** listesi.

C# MongoDB karşı uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [CSharp dil Merkezi][MongoC#LangCenter]. 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp

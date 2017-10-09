---
title: "bir sanal makinede çalışan tooMongoDB bağlanan Azure web uygulamasında aaaCreate"
description: "Bir ASP.NET uygulaması tooAzure uygulama hizmeti toouse Git toodeploy nasıl bağlanacağını öğretilmektedir öğretici tooMongoDB üzerinde bir Azure sanal makine."
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
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Azure'da bir sanal makinede çalışan tooMongoDB bağlanan bir web uygulaması oluşturma
Git kullanarak bir ASP.NET uygulaması tooAzure App Service Web Apps dağıtabilirsiniz. Bu öğreticide, basit bir ön uç ASP.NET MVC, azure'da bir sanal makinede çalışan tooa MongoDB veritabanına bağlayan görev listesi uygulaması oluşturacaksınız.  [MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanı. Çalıştıran ve hello ASP.NET uygulama geliştirme bilgisayarınızda testi sonra hello uygulama tooApp Service Web Apps karşıya yükleyecek Git kullanarak.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="background-knowledge"></a>Arka plan bilgisi
Bilgi Bankası hello aşağıdaki gerekli değildir ancak bu öğretici için yararlıdır:

* MongoDB için Hello C# sürücüsü. C# MongoDB karşı uygulamaları geliştirme hakkında daha fazla bilgi için bkz: Merhaba MongoDB [CSharp dil Merkezi][MongoC#LangCenter]. 
* Merhaba ASP .NET web uygulama çerçevesidir. Tüm hello adresinden hakkında bilgi alabilirsiniz [ASP.net Web sitesi][ASP.NET].
* Merhaba ASP .NET MVC web uygulama çerçevesidir. Tüm hello adresinden hakkında bilgi alabilirsiniz [ASP.NET MVC Web][MVCWebSite].
* kullanıyoruz. Bilgi başlayabiliriz [Azure][WindowsAzure].

## <a name="prerequisites"></a>Ön koşullar
* [Web için Visual Studio Express 2013] [ VSEWeb] veya [Visual Studio 2013][VSUlt]
* [.NET için Azure SDK](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Etkin bir Microsoft Azure aboneliği

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Bir sanal makine oluşturun ve MongoDB yükleme
Bu öğretici, Azure'da bir sanal makine oluşturduğunuz varsayar. Merhaba sanal makine oluşturduktan sonra tooinstall MongoDB hello sanal makineye gerekir:

* bkz: toocreate Windows sanal makine ve yükleme MongoDB, [Azure'da Windows Server çalıştıran bir sanal makinede yüklemek MongoDB][InstallMongoOnWindowsVM].

Azure'da hello sanal makine oluşturup MongoDB yüklü sonra emin tooremember hello DNS adı hello sanal makine ("testlinuxvm.cloudapp.net", örneğin) ve hello dış bağlantı noktası hello bitiş noktası içinde belirtilen MongoDB için olması.  Merhaba öğreticide daha sonra bu bilgileri gerekir.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Bu bölümde Visual Studio kullanarak "My görev listesi" adlı bir ASP.NET uygulaması oluşturun ve ilk dağıtım tooAzure App Service Web Apps gerçekleştirin. Merhaba uygulama yerel olarak çalışacak, ancak bu Azure tooyour sanal makineye bağlanmak ve oluşturduğunuz hello MongoDB örneği burada kullanabilirsiniz.

1. Visual Studio'da sırasıyla **yeni proje**.
   
    ![Sayfa yeni bir proje başlatın][StartPageNewProject]
2. Merhaba, **yeni proje** penceresinde hello sol bölmesinde, **Visual C#**ve ardından **Web**. Merhaba orta bölmesinde seçin **ASP.NET Web uygulaması**. Merhaba altındaki "MyTaskListApp" projenizi adlandırın ve ardından **Tamam**.
   
    ![Yeni Proje İletişim Kutusu][NewProjectMyTaskListApp]
3. Merhaba, **yeni ASP.NET projesi** iletişim kutusunda **MVC**ve ardından **Tamam**.
   
    ![MVC şablonunu seçin][VS2013SelectMVCTemplate]
4. Microsoft Azure'da zaten imzalanmadığını içinde istendiğinde toosign olacaktır. Azure'da Hello istemleri toosign izleyin.
5. Oturum açtıktan sonra App Service web uygulamanızı yapılandırmaya başlayabilirsiniz. Merhaba belirtin **Web uygulaması adı**, **uygulama hizmeti planı**, **kaynak grubu**, ve **bölge**, ardından **Oluştur**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Başlangıç projesi oluşturma tamamlandıktan sonra Azure App Service'te hello belirtildiği şekilde oluşturulan hello web uygulama toobe bekleyin **Azure App Service etkinliği** penceresi. Ardından **yayımlama MyTaskListApp toothis Web uygulaması şimdi**.
7. **Yayımla**’ta tıklayın.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Varsayılan ASP.NET uygulamanızı yayımlanan tooAzure App Service Web Apps eklendiğinde, hello tarayıcıda başlatılacak.

## <a name="install-hello-mongodb-c-driver"></a>Merhaba MongoDB C# sürücü yükleme
MongoDB gereksinim duyduğunuz bir sürücüyle C# uygulamaları için istemci tarafı destek sunar, yerel geliştirme bilgisayarınızda tooinstall. Merhaba C# sürücü NuGet kullanılabilir.

tooinstall hello MongoDB C# sürücüsü:

1. İçinde **Çözüm Gezgini**, sağ hello **MyTaskListApp** proje ve seçin **yönetmek NuGetPackages**.
   
    ![NuGet paketlerini yönetme][VS2013ManageNuGetPackages]
2. Merhaba, **NuGet paketlerini Yönet** penceresinde hello sol bölmede, tıklatın **çevrimiçi**. Merhaba, **arama çevrimiçi** kutusuna sağ Merhaba, "mongodb.driver" yazın.  Tıklatın **yükleme** tooinstall hello sürücü.
   
    ![MongoDB C# sürücü arayın][SearchforMongoDBCSharpDriver]
3. Tıklatın **kabul ediyorum** tooaccept hello 10gen, Inc. lisans koşulları.
4. Tıklatın **Kapat** hello sürücü yüklendikten sonra.
    ![MongoDB C# sürücüsünün yüklü][MongoDBCsharpDriverInstalled]

Merhaba MongoDB C# sürücü artık yüklüdür.  Başvuruları toohello **MongoDB.Bson**, **MongoDB.Driver**, ve **MongoDB.Driver.Core** kitaplıkları toohello proje eklenmiştir.

![MongoDB C# sürücü başvuruları][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Model ekleme
İçinde **Çözüm Gezgini**, sağ hello *modelleri* klasör ve **Ekle** yeni bir **sınıfı** ve adlandırın *TaskModel.cs* .  İçinde *TaskModel.cs*, hello varolan kod koddan hello ile değiştirin:

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

## <a name="add-hello-data-access-layer"></a>Merhaba veri erişim katmanı ekleme
İçinde **Çözüm Gezgini**, sağ hello *MyTaskListApp* proje ve **Ekle** bir **yeni klasör** adlı *DAL*.  Sağ hello *DAL* klasör ve **Ekle** yeni bir **sınıfı**. Ad hello sınıf dosyası *Dal.cs*.  İçinde *Dal.cs*, hello varolan kod koddan hello ile değiştirin:

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

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
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

            // Creates a Task and inserts it into hello collection in MongoDB.
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
Açık hello *Controllers\HomeController.cs* dosyasını **Çözüm Gezgini** ve hello var olan kodu hello şununla değiştirin:

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

## <a name="set-up-hello-styles"></a>Hello stilleri ayarlama
Merhaba sayfanın üst kısmındaki Merhaba, açık hello toochange hello başlık *görünümler/paylaşılan\\_Layout.cshtml* dosyasını **Çözüm Gezgini** ve "Uygulama adı" Merhaba navbar üstbilgisinde "My görev ile değiştirin. Uygulama listesi"böylece şöyle görünür:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Merhaba hello görev listesi menü yukarı sipariş tooset içinde açmak *\Views\Home\Index.cshtml* dosya ve hello varolan kod koddan hello ile değiştirin:

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


tooadd hello özelliği toocreate yeni bir görev sağ hello *görünümler\\*  klasör ve **Ekle** bir **Görünüm**.  Ad hello Görünüm *oluşturma*. Merhaba kod hello şununla değiştirin:

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

## <a name="set-hello-mongodb-connection-string"></a>Merhaba MongoDB bağlantı dizesini ayarlayın
İçinde **Çözüm Gezgini**açın hello *DAL/Dal.cs* dosya. Aşağıdaki kod hello bulur:

    private string connectionString = "mongodb://<vm-dns-name>";

Değiştir `<vm-dns-name>` hello oluşturduğunuz MongoDB çalışan hello sanal makine hello DNS adı ile [bir sanal makine oluşturun ve MongoDB yükleme] [ Create a virtual machine and install MongoDB] Bu öğreticinin adımı.  sanal makinenizin toofind hello DNS adı Git toohello Azure Portal, select **sanal makineleri**ve bulma **DNS adı**.

Merhaba sanal makinenin Hello DNS adı "testlinuxvm.cloudapp.net" ise ve MongoDB 27017 hello varsayılan bağlantı noktasında dinleme hello bağlantı dizesi satır kod gibi görünür:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Merhaba sanal makine uç noktası MongoDB için farklı bir dış bağlantı belirtiyorsa, kısa hello bağlantı noktası başlangıç bağlantı dizesinde yapabilirsiniz:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

MongoDB bağlantı dizeleri hakkında daha fazla bilgi için bkz: [bağlantıları][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Merhaba yerel dağıtımı test etme
geliştirme bilgisayarınızda uygulamanızı toorun seçin **hata ayıklamayı Başlat** hello gelen **hata ayıklama** menüsü veya isabet **F5**. IIS Express başlar ve bir tarayıcı açar ve hello uygulamanın giriş sayfasını açar.  Sanal makineniz azure'da çalışan toohello MongoDB veritabanı eklenecek yeni bir görev ekleyebilirsiniz.

![Görev listesi Uygulamam][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>TooAzure App Service Web Apps yayımlama
Bu bölümde, değişiklikleri tooAzure App Service Web Apps yayımlar.

1. Çözüm Gezgini'nde sağ **MyTaskListApp** yeniden tıklatıp **Yayımla**.
2. **Yayımla**’ta tıklayın.
   
    Web uygulamanızı Azure App Service içinde çalışan ve hello MongoDB veritabanı Azure Virtual Machines'de erişme görmelisiniz.

## <a name="summary"></a>Özet
ASP.NET uygulama tooAzure App Service Web Apps şimdi başarıyla dağıtmış. tooview hello web uygulaması:

1. Azure Portal Hello oturum açın.
2. Tıklatın **Web uygulamaları**. 
3. Web uygulamanızı hello seçin **Web Apps** listesi.

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
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp

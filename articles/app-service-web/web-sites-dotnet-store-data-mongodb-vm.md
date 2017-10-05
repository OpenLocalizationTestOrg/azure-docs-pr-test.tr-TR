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
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="b82d9-103">Sanal makinede çalışan MongoDB’ye bağlanan Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b82d9-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="b82d9-104">Git kullanarak Azure App Service Web Apps için bir ASP.NET uygulamasını dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="b82d9-105">Bu öğreticide, basit bir ön uç ASP.NET MVC azure'da sanal makine üzerinde çalışan bir MongoDB veritabanına bağlayan görev listesi uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b82d9-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="b82d9-106">[MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b82d9-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="b82d9-107">Çalıştıran ve ASP.NET uygulama geliştirme bilgisayarınızda testi sonra App Service Web Apps Git kullanarak uygulamaya karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="b82d9-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="b82d9-108">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="b82d9-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b82d9-109">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b82d9-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="b82d9-110">Arka plan bilgisi</span><span class="sxs-lookup"><span data-stu-id="b82d9-110">Background knowledge</span></span>
<span data-ttu-id="b82d9-111">Aşağıdaki bilgisi gerekli değildir ancak bu öğretici için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="b82d9-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="b82d9-112">C# sürücüsü MongoDB için.</span><span class="sxs-lookup"><span data-stu-id="b82d9-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="b82d9-113">MongoDB MongoDB karşı C# uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [CSharp dil Merkezi][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="b82d9-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="b82d9-114">ASP .NET web uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="b82d9-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="b82d9-115">Tüm adresinden hakkında bilgi alabilirsiniz [ASP.net Web sitesi][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="b82d9-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="b82d9-116">ASP .NET MVC web uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="b82d9-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="b82d9-117">Tüm adresinden hakkında bilgi alabilirsiniz [ASP.NET MVC Web][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="b82d9-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="b82d9-118">kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-118">Azure.</span></span> <span data-ttu-id="b82d9-119">Bilgi başlayabiliriz [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="b82d9-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b82d9-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b82d9-120">Prerequisites</span></span>
* <span data-ttu-id="b82d9-121">[Web için Visual Studio Express 2013] [ VSEWeb] veya [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="b82d9-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="b82d9-122">.NET için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="b82d9-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="b82d9-123">Etkin bir Microsoft Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="b82d9-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="b82d9-124">Bir sanal makine oluşturun ve MongoDB yükleme</span><span class="sxs-lookup"><span data-stu-id="b82d9-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="b82d9-125">Bu öğretici, Azure'da bir sanal makine oluşturduğunuz varsayar.</span><span class="sxs-lookup"><span data-stu-id="b82d9-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="b82d9-126">Sanal makineyi oluşturduktan sonra sanal makinede MongoDB yüklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b82d9-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="b82d9-127">Bir Windows sanal makine oluşturun ve MongoDB yüklemek için bkz: [Azure'da Windows Server çalıştıran bir sanal makinede yüklemek MongoDB][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="b82d9-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="b82d9-128">Azure'da sanal makine oluşturup MongoDB yüklü sonra uç belirtilen MongoDB için sanal makine ("testlinuxvm.cloudapp.net", örneğin) ve dış bağlantı noktasını DNS adını anımsamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="b82d9-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="b82d9-129">Bu bilgiler daha sonra öğreticide gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="b82d9-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="b82d9-130">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="b82d9-130">Create the application</span></span>
<span data-ttu-id="b82d9-131">Bu bölümde Visual Studio kullanarak "My görev listesi" adlı bir ASP.NET uygulaması oluşturun ve Azure App Service Web Apps için ilk bir dağıtım gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b82d9-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="b82d9-132">Uygulamayı yerel olarak çalışır, ancak bunu Azure sanal makinenizde bağlanmak ve oluşturduğunuz MongoDB örneği burada kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="b82d9-133">Visual Studio'da sırasıyla **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Sayfa yeni bir proje başlatın][StartPageNewProject]
2. <span data-ttu-id="b82d9-135">İçinde **yeni proje** penceresinde sol bölmesinde, **Visual C#**ve ardından **Web**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="b82d9-136">Orta bölmede seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="b82d9-137">Projeniz "MyTaskListApp" alt kısmındaki adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Yeni Proje İletişim Kutusu][NewProjectMyTaskListApp]
3. <span data-ttu-id="b82d9-139">İçinde **yeni ASP.NET projesi** iletişim kutusunda **MVC**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![MVC şablonunu seçin][VS2013SelectMVCTemplate]
4. <span data-ttu-id="b82d9-141">Microsoft Azure'da zaten oturumunuz açık değil, oturum açmak için istenir.</span><span class="sxs-lookup"><span data-stu-id="b82d9-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="b82d9-142">Azure'da oturum için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b82d9-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="b82d9-143">Oturum açtıktan sonra App Service web uygulamanızı yapılandırmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="b82d9-144">Belirtin **Web uygulaması adı**, **uygulama hizmeti planı**, **kaynak grubu**, ve **bölge**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="b82d9-145">Azure App Service'te de belirtildiği gibi oluşturulması için web uygulaması projesi oluşturma tamamlandıktan sonra bekleyin **Azure App Service etkinliği** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b82d9-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="b82d9-146">Ardından **şimdi bu Web uygulaması yayımlama MyTaskListApp**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="b82d9-147">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b82d9-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="b82d9-148">Varsayılan ASP.NET uygulamanızı Azure App Service Web Apps için yayımlandığında, tarayıcıda başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="b82d9-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="b82d9-149">MongoDB C# sürücüsünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="b82d9-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="b82d9-150">MongoDB yerel geliştirme bilgisayarınıza yüklemek için gereken bir sürücüyle C# uygulamaları için istemci tarafı desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="b82d9-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="b82d9-151">C# sürücü NuGet kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b82d9-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="b82d9-152">MongoDB C# sürücüyü yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="b82d9-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="b82d9-153">İçinde **Çözüm Gezgini**, sağ **MyTaskListApp** proje ve seçin **yönetmek NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![NuGet paketlerini yönetme][VS2013ManageNuGetPackages]
2. <span data-ttu-id="b82d9-155">İçinde **NuGet paketlerini Yönet** pencerede, sol bölmede, tıklayın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="b82d9-156">İçinde **arama çevrimiçi** kutusuna sağ tarafta, "mongodb.driver" yazın.</span><span class="sxs-lookup"><span data-stu-id="b82d9-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="b82d9-157">Tıklatın **yükleme** sürücüyü yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="b82d9-157">Click **Install** to install the driver.</span></span>
   
    ![MongoDB C# sürücü arayın][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="b82d9-159">Tıklatın **kabul ediyorum** 10gen, Inc. lisans koşullarını kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="b82d9-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="b82d9-160">Tıklatın **Kapat** sürücü yüklendikten sonra.</span><span class="sxs-lookup"><span data-stu-id="b82d9-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="b82d9-161">![MongoDB C# sürücüsünün yüklü][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="b82d9-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="b82d9-162">MongoDB C# sürücü artık yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="b82d9-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="b82d9-163">Başvurular **MongoDB.Bson**, **MongoDB.Driver**, ve **MongoDB.Driver.Core** kitaplıkları projeye eklendi.</span><span class="sxs-lookup"><span data-stu-id="b82d9-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![MongoDB C# sürücü başvuruları][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="b82d9-165">Model ekleme</span><span class="sxs-lookup"><span data-stu-id="b82d9-165">Add a model</span></span>
<span data-ttu-id="b82d9-166">İçinde **Çözüm Gezgini**, sağ *modelleri* klasör ve **Ekle** yeni bir **sınıfı** ve adlandırın *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="b82d9-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="b82d9-167">İçinde *TaskModel.cs*, var olan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b82d9-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="b82d9-168">Veri erişim katmanı ekleme</span><span class="sxs-lookup"><span data-stu-id="b82d9-168">Add the data access layer</span></span>
<span data-ttu-id="b82d9-169">İçinde **Çözüm Gezgini**, sağ *MyTaskListApp* proje ve **Ekle** bir **yeni klasör** adlı *DAL*.</span><span class="sxs-lookup"><span data-stu-id="b82d9-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="b82d9-170">Sağ *DAL* klasör ve **Ekle** yeni bir **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="b82d9-171">Sınıf dosya adı *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="b82d9-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="b82d9-172">İçinde *Dal.cs*, var olan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b82d9-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="b82d9-173">Denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="b82d9-173">Add a controller</span></span>
<span data-ttu-id="b82d9-174">Açık *Controllers\HomeController.cs* dosyasını **Çözüm Gezgini** ve var olan kodu aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b82d9-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="b82d9-175">Stilleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="b82d9-175">Set up the styles</span></span>
<span data-ttu-id="b82d9-176">Sayfanın üstündeki başlığını değiştirmek için açık *görünümler/paylaşılan\\_Layout.cshtml* dosyasını **Çözüm Gezgini** ve "Uygulama adı" navbar üstbilgisinde "My görev listesi ile değiştirin. Böyle uygulama"şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="b82d9-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="b82d9-177">Görev listesi menüsü Ayarla için açık *\Views\Home\Index.cshtml* dosya ve var olan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b82d9-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="b82d9-178">Yeni bir görev oluşturma olanağı eklemek için sağ tıklatın *görünümler\\*  klasör ve **Ekle** bir **Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="b82d9-179">Görünüm adı *oluşturma*.</span><span class="sxs-lookup"><span data-stu-id="b82d9-179">Name the view *Create*.</span></span> <span data-ttu-id="b82d9-180">Kod aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b82d9-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="b82d9-181">**Çözüm Gezgini** aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b82d9-181">**Solution Explorer** should look like this:</span></span>

![Çözüm Gezgini][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="b82d9-183">MongoDB bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b82d9-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="b82d9-184">İçinde **Çözüm Gezgini**, açık *DAL/Dal.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="b82d9-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="b82d9-185">Aşağıdaki kod satırını bulun:</span><span class="sxs-lookup"><span data-stu-id="b82d9-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="b82d9-186">Değiştir `<vm-dns-name>` oluşturduğunuz MongoDB çalışan sanal makinenin DNS adı ile [bir sanal makine oluşturun ve MongoDB yükleme] [ Create a virtual machine and install MongoDB] Bu öğreticinin adımı.</span><span class="sxs-lookup"><span data-stu-id="b82d9-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="b82d9-187">Sanal makineniz DNS adını bulmak için select Azure Portalı'na Git **sanal makineleri**ve Bul **DNS adı**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="b82d9-188">Sanal makinenin DNS adı "testlinuxvm.cloudapp.net" ise ve MongoDB 27017 varsayılan bağlantı noktasında dinleme bağlantı dizesi kod satırı ile gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b82d9-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="b82d9-189">Sanal makine uç noktası MongoDB için farklı bir dış bağlantı belirtiyorsa, bağlantı dizesindeki bağlantı noktası belirtin yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b82d9-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="b82d9-190">MongoDB bağlantı dizeleri hakkında daha fazla bilgi için bkz: [bağlantıları][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="b82d9-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="b82d9-191">Yerel dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="b82d9-191">Test the local deployment</span></span>
<span data-ttu-id="b82d9-192">Geliştirme bilgisayarınızda uygulamanızı çalıştırmak için seçin **hata ayıklamayı Başlat** gelen **hata ayıklama** menüsü veya isabet **F5**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="b82d9-193">IIS Express başlar ve bir tarayıcı açar ve uygulamanın giriş sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="b82d9-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="b82d9-194">Sanal makineniz azure'da çalışan MongoDB veritabanına eklenen yeni bir görev ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Görev listesi Uygulamam][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="b82d9-196">Azure App Service Web Apps için yayımlama</span><span class="sxs-lookup"><span data-stu-id="b82d9-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="b82d9-197">Bu bölümde Azure App Service Web Apps için yaptığınız değişiklikleri yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b82d9-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="b82d9-198">Çözüm Gezgini'nde sağ **MyTaskListApp** yeniden tıklatıp **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="b82d9-199">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b82d9-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="b82d9-200">Web uygulamanızı Azure App Service içinde çalışan ve Azure Virtual Machines'de MongoDB veritabanı erişme görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b82d9-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="b82d9-201">Özet</span><span class="sxs-lookup"><span data-stu-id="b82d9-201">Summary</span></span>
<span data-ttu-id="b82d9-202">ASP.NET uygulamanızı Azure App Service Web Apps için şimdi başarıyla dağıtmış.</span><span class="sxs-lookup"><span data-stu-id="b82d9-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="b82d9-203">Web uygulaması görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="b82d9-203">To view the web app:</span></span>

1. <span data-ttu-id="b82d9-204">Azure portalı günlüğüne.</span><span class="sxs-lookup"><span data-stu-id="b82d9-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="b82d9-205">Tıklatın **Web uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b82d9-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="b82d9-206">Web uygulamanızı seçin **Web Apps** listesi.</span><span class="sxs-lookup"><span data-stu-id="b82d9-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="b82d9-207">C# MongoDB karşı uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [CSharp dil Merkezi][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="b82d9-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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

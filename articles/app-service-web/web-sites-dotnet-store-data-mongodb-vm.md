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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="4d1f5-103">Azure'da bir sanal makinede çalışan tooMongoDB bağlanan bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d1f5-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="4d1f5-104">Git kullanarak bir ASP.NET uygulaması tooAzure App Service Web Apps dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4d1f5-105">Bu öğreticide, basit bir ön uç ASP.NET MVC, azure'da bir sanal makinede çalışan tooa MongoDB veritabanına bağlayan görev listesi uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="4d1f5-106">[MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="4d1f5-107">Çalıştıran ve hello ASP.NET uygulama geliştirme bilgisayarınızda testi sonra hello uygulama tooApp Service Web Apps karşıya yükleyecek Git kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="4d1f5-108">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4d1f5-109">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="4d1f5-110">Arka plan bilgisi</span><span class="sxs-lookup"><span data-stu-id="4d1f5-110">Background knowledge</span></span>
<span data-ttu-id="4d1f5-111">Bilgi Bankası hello aşağıdaki gerekli değildir ancak bu öğretici için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="4d1f5-112">MongoDB için Hello C# sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="4d1f5-113">C# MongoDB karşı uygulamaları geliştirme hakkında daha fazla bilgi için bkz: Merhaba MongoDB [CSharp dil Merkezi][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="4d1f5-114">Merhaba ASP .NET web uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="4d1f5-115">Tüm hello adresinden hakkında bilgi alabilirsiniz [ASP.net Web sitesi][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="4d1f5-116">Merhaba ASP .NET MVC web uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="4d1f5-117">Tüm hello adresinden hakkında bilgi alabilirsiniz [ASP.NET MVC Web][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="4d1f5-118">kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-118">Azure.</span></span> <span data-ttu-id="4d1f5-119">Bilgi başlayabiliriz [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d1f5-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4d1f5-120">Prerequisites</span></span>
* <span data-ttu-id="4d1f5-121">[Web için Visual Studio Express 2013] [ VSEWeb] veya [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="4d1f5-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="4d1f5-122">.NET için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="4d1f5-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="4d1f5-123">Etkin bir Microsoft Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="4d1f5-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="4d1f5-124">Bir sanal makine oluşturun ve MongoDB yükleme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="4d1f5-125">Bu öğretici, Azure'da bir sanal makine oluşturduğunuz varsayar.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="4d1f5-126">Merhaba sanal makine oluşturduktan sonra tooinstall MongoDB hello sanal makineye gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="4d1f5-127">bkz: toocreate Windows sanal makine ve yükleme MongoDB, [Azure'da Windows Server çalıştıran bir sanal makinede yüklemek MongoDB][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="4d1f5-128">Azure'da hello sanal makine oluşturup MongoDB yüklü sonra emin tooremember hello DNS adı hello sanal makine ("testlinuxvm.cloudapp.net", örneğin) ve hello dış bağlantı noktası hello bitiş noktası içinde belirtilen MongoDB için olması.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="4d1f5-129">Merhaba öğreticide daha sonra bu bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="4d1f5-130">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d1f5-130">Create hello application</span></span>
<span data-ttu-id="4d1f5-131">Bu bölümde Visual Studio kullanarak "My görev listesi" adlı bir ASP.NET uygulaması oluşturun ve ilk dağıtım tooAzure App Service Web Apps gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4d1f5-132">Merhaba uygulama yerel olarak çalışacak, ancak bu Azure tooyour sanal makineye bağlanmak ve oluşturduğunuz hello MongoDB örneği burada kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="4d1f5-133">Visual Studio'da sırasıyla **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Sayfa yeni bir proje başlatın][StartPageNewProject]
2. <span data-ttu-id="4d1f5-135">Merhaba, **yeni proje** penceresinde hello sol bölmesinde, **Visual C#**ve ardından **Web**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="4d1f5-136">Merhaba orta bölmesinde seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="4d1f5-137">Merhaba altındaki "MyTaskListApp" projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Yeni Proje İletişim Kutusu][NewProjectMyTaskListApp]
3. <span data-ttu-id="4d1f5-139">Merhaba, **yeni ASP.NET projesi** iletişim kutusunda **MVC**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![MVC şablonunu seçin][VS2013SelectMVCTemplate]
4. <span data-ttu-id="4d1f5-141">Microsoft Azure'da zaten imzalanmadığını içinde istendiğinde toosign olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="4d1f5-142">Azure'da Hello istemleri toosign izleyin.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="4d1f5-143">Oturum açtıktan sonra App Service web uygulamanızı yapılandırmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="4d1f5-144">Merhaba belirtin **Web uygulaması adı**, **uygulama hizmeti planı**, **kaynak grubu**, ve **bölge**, ardından **Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="4d1f5-145">Başlangıç projesi oluşturma tamamlandıktan sonra Azure App Service'te hello belirtildiği şekilde oluşturulan hello web uygulama toobe bekleyin **Azure App Service etkinliği** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="4d1f5-146">Ardından **yayımlama MyTaskListApp toothis Web uygulaması şimdi**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="4d1f5-147">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="4d1f5-148">Varsayılan ASP.NET uygulamanızı yayımlanan tooAzure App Service Web Apps eklendiğinde, hello tarayıcıda başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="4d1f5-149">Merhaba MongoDB C# sürücü yükleme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="4d1f5-150">MongoDB gereksinim duyduğunuz bir sürücüyle C# uygulamaları için istemci tarafı destek sunar, yerel geliştirme bilgisayarınızda tooinstall.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="4d1f5-151">Merhaba C# sürücü NuGet kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="4d1f5-152">tooinstall hello MongoDB C# sürücüsü:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="4d1f5-153">İçinde **Çözüm Gezgini**, sağ hello **MyTaskListApp** proje ve seçin **yönetmek NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![NuGet paketlerini yönetme][VS2013ManageNuGetPackages]
2. <span data-ttu-id="4d1f5-155">Merhaba, **NuGet paketlerini Yönet** penceresinde hello sol bölmede, tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="4d1f5-156">Merhaba, **arama çevrimiçi** kutusuna sağ Merhaba, "mongodb.driver" yazın.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="4d1f5-157">Tıklatın **yükleme** tooinstall hello sürücü.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![MongoDB C# sürücü arayın][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="4d1f5-159">Tıklatın **kabul ediyorum** tooaccept hello 10gen, Inc. lisans koşulları.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="4d1f5-160">Tıklatın **Kapat** hello sürücü yüklendikten sonra.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="4d1f5-161">![MongoDB C# sürücüsünün yüklü][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="4d1f5-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="4d1f5-162">Merhaba MongoDB C# sürücü artık yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="4d1f5-163">Başvuruları toohello **MongoDB.Bson**, **MongoDB.Driver**, ve **MongoDB.Driver.Core** kitaplıkları toohello proje eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![MongoDB C# sürücü başvuruları][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="4d1f5-165">Model ekleme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-165">Add a model</span></span>
<span data-ttu-id="4d1f5-166">İçinde **Çözüm Gezgini**, sağ hello *modelleri* klasör ve **Ekle** yeni bir **sınıfı** ve adlandırın *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="4d1f5-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="4d1f5-167">İçinde *TaskModel.cs*, hello varolan kod koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="4d1f5-168">Merhaba veri erişim katmanı ekleme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-168">Add hello data access layer</span></span>
<span data-ttu-id="4d1f5-169">İçinde **Çözüm Gezgini**, sağ hello *MyTaskListApp* proje ve **Ekle** bir **yeni klasör** adlı *DAL*.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="4d1f5-170">Sağ hello *DAL* klasör ve **Ekle** yeni bir **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="4d1f5-171">Ad hello sınıf dosyası *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="4d1f5-172">İçinde *Dal.cs*, hello varolan kod koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="4d1f5-173">Denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-173">Add a controller</span></span>
<span data-ttu-id="4d1f5-174">Açık hello *Controllers\HomeController.cs* dosyasını **Çözüm Gezgini** ve hello var olan kodu hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="4d1f5-175">Hello stilleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d1f5-175">Set up hello styles</span></span>
<span data-ttu-id="4d1f5-176">Merhaba sayfanın üst kısmındaki Merhaba, açık hello toochange hello başlık *görünümler/paylaşılan\\_Layout.cshtml* dosyasını **Çözüm Gezgini** ve "Uygulama adı" Merhaba navbar üstbilgisinde "My görev ile değiştirin. Uygulama listesi"böylece şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="4d1f5-177">Merhaba hello görev listesi menü yukarı sipariş tooset içinde açmak *\Views\Home\Index.cshtml* dosya ve hello varolan kod koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="4d1f5-178">tooadd hello özelliği toocreate yeni bir görev sağ hello *görünümler\\*  klasör ve **Ekle** bir **Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="4d1f5-179">Ad hello Görünüm *oluşturma*.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-179">Name hello view *Create*.</span></span> <span data-ttu-id="4d1f5-180">Merhaba kod hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="4d1f5-181">**Çözüm Gezgini** aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-181">**Solution Explorer** should look like this:</span></span>

![Çözüm Gezgini][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="4d1f5-183">Merhaba MongoDB bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d1f5-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="4d1f5-184">İçinde **Çözüm Gezgini**açın hello *DAL/Dal.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="4d1f5-185">Aşağıdaki kod hello bulur:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="4d1f5-186">Değiştir `<vm-dns-name>` hello oluşturduğunuz MongoDB çalışan hello sanal makine hello DNS adı ile [bir sanal makine oluşturun ve MongoDB yükleme] [ Create a virtual machine and install MongoDB] Bu öğreticinin adımı.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="4d1f5-187">sanal makinenizin toofind hello DNS adı Git toohello Azure Portal, select **sanal makineleri**ve bulma **DNS adı**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="4d1f5-188">Merhaba sanal makinenin Hello DNS adı "testlinuxvm.cloudapp.net" ise ve MongoDB 27017 hello varsayılan bağlantı noktasında dinleme hello bağlantı dizesi satır kod gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="4d1f5-189">Merhaba sanal makine uç noktası MongoDB için farklı bir dış bağlantı belirtiyorsa, kısa hello bağlantı noktası başlangıç bağlantı dizesinde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="4d1f5-190">MongoDB bağlantı dizeleri hakkında daha fazla bilgi için bkz: [bağlantıları][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="4d1f5-191">Merhaba yerel dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="4d1f5-191">Test hello local deployment</span></span>
<span data-ttu-id="4d1f5-192">geliştirme bilgisayarınızda uygulamanızı toorun seçin **hata ayıklamayı Başlat** hello gelen **hata ayıklama** menüsü veya isabet **F5**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="4d1f5-193">IIS Express başlar ve bir tarayıcı açar ve hello uygulamanın giriş sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="4d1f5-194">Sanal makineniz azure'da çalışan toohello MongoDB veritabanı eklenecek yeni bir görev ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Görev listesi Uygulamam][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="4d1f5-196">TooAzure App Service Web Apps yayımlama</span><span class="sxs-lookup"><span data-stu-id="4d1f5-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="4d1f5-197">Bu bölümde, değişiklikleri tooAzure App Service Web Apps yayımlar.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="4d1f5-198">Çözüm Gezgini'nde sağ **MyTaskListApp** yeniden tıklatıp **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="4d1f5-199">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="4d1f5-200">Web uygulamanızı Azure App Service içinde çalışan ve hello MongoDB veritabanı Azure Virtual Machines'de erişme görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="4d1f5-201">Özet</span><span class="sxs-lookup"><span data-stu-id="4d1f5-201">Summary</span></span>
<span data-ttu-id="4d1f5-202">ASP.NET uygulama tooAzure App Service Web Apps şimdi başarıyla dağıtmış.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4d1f5-203">tooview hello web uygulaması:</span><span class="sxs-lookup"><span data-stu-id="4d1f5-203">tooview hello web app:</span></span>

1. <span data-ttu-id="4d1f5-204">Azure Portal Hello oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="4d1f5-205">Tıklatın **Web uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="4d1f5-206">Web uygulamanızı hello seçin **Web Apps** listesi.</span><span class="sxs-lookup"><span data-stu-id="4d1f5-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="4d1f5-207">C# MongoDB karşı uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [CSharp dil Merkezi][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="4d1f5-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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

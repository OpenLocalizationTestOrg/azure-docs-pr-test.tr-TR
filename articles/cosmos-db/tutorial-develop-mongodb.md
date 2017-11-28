---
title: "aaaUse Azure Cosmos veritabanı API MongoDB toobuild bir web uygulaması için | Microsoft Docs"
description: "Merhaba API MongoDB için kullanarak bir çevrimiçi veritabanı web uygulaması oluşturan bir Azure Cosmos DB Öğreticisi."
keywords: "mongodb örnekleri"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="ffc40-104">Azure Cosmos DB: Tooa MongoDB uygulamaya .NET kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="ffc40-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="ffc40-105">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ffc40-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ffc40-106">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffc40-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ffc40-107">Bu öğretici nasıl hesabı kullanarak bir Azure Cosmos DB toocreate hello Azure portal ve toocreate bir veritabanı ve koleksiyonu toostore verileri kullanarak nasıl hello gösterir [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ffc40-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="ffc40-108">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="ffc40-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ffc40-109">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffc40-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="ffc40-110">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ffc40-110">Update your connection string</span></span>
> * <span data-ttu-id="ffc40-111">Bir sanal makinede bir MongoDB uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffc40-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="ffc40-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffc40-112">Create a database account</span></span>

<span data-ttu-id="ffc40-113">Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="ffc40-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="ffc40-114">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="ffc40-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="ffc40-115">Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="ffc40-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="ffc40-116">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="ffc40-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="ffc40-117">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ffc40-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="ffc40-118">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ffc40-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="ffc40-119">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ffc40-119">Update your connection string</span></span>

1. <span data-ttu-id="ffc40-120">Hello Azure portalında, hello içinde **Azure Cosmos DB** sayfasında, hello API MongoDB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="ffc40-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="ffc40-121">Merhaba sol hello hesabı dikey çubuğunda, **Hızlı Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="ffc40-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="ffc40-122">Platformunuzu seçin (*.NET sürücü*, *Node.js sürücü*, *MongoDB Kabuk*, *Java sürücü*, *Python sürücü*).</span><span class="sxs-lookup"><span data-stu-id="ffc40-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="ffc40-123">Sürücü veya listelenen aracı görmüyorsanız, endişelenmeyin, biz sürekli olarak daha fazla bağlantı kod parçacıkları belge.</span><span class="sxs-lookup"><span data-stu-id="ffc40-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="ffc40-124">MongoDB uygulamanıza hello kod parçacığını yapıştırın ve hazır toogo demektir.</span><span class="sxs-lookup"><span data-stu-id="ffc40-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="ffc40-125">MongoDB uygulamanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ffc40-125">Set up your MongoDB app</span></span>

<span data-ttu-id="ffc40-126">Merhaba kullanabilirsiniz [azure'da bir sanal makinede çalışan tooMongoDB bağlanan bir web uygulaması oluşturma](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) eğitmen, en az değişiklik, tooquickly Kurulum MongoDB uygulama (yerel olarak ya da veya yayımlanan tooan Azure web uygulaması), tooan API MongoDB hesabının bağlanır.</span><span class="sxs-lookup"><span data-stu-id="ffc40-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="ffc40-127">Bir değişiklik ile Merhaba öğreticisini izleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc40-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="ffc40-128">Merhaba Dal.cs kod bu ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffc40-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
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
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
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
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="ffc40-129">Hesap ayarlarınızı başına hello Dal.cs dosyasındaki değişkenleri hello Azure Portalı'nda hello anahtarları sayfasından aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffc40-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="ffc40-130">Merhaba uygulama kullanın!</span><span class="sxs-lookup"><span data-stu-id="ffc40-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ffc40-131">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="ffc40-131">Clean up resources</span></span>

<span data-ttu-id="ffc40-132">Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffc40-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="ffc40-133">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ffc40-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="ffc40-134">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ffc40-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc40-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ffc40-135">Next steps</span></span>

<span data-ttu-id="ffc40-136">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="ffc40-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ffc40-137">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffc40-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="ffc40-138">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ffc40-138">Update your connection string</span></span>
> * <span data-ttu-id="ffc40-139">Bir sanal makinede bir MongoDB uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffc40-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="ffc40-140">Toohello sonraki öğretici devam ve MongoDB veri tooAzure Cosmos DB içe aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffc40-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffc40-141">Azure Cosmos DB’ye MongoDB verileri aktarma</span><span class="sxs-lookup"><span data-stu-id="ffc40-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


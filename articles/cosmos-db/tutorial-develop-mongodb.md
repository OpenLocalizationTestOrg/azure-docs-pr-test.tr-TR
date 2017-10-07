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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure Cosmos DB: Tooa MongoDB uygulamaya .NET kullanarak bağlan

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu öğretici nasıl hesabı kullanarak bir Azure Cosmos DB toocreate hello Azure portal ve toocreate bir veritabanı ve koleksiyonu toostore verileri kullanarak nasıl hello gösterir [MongoDB API](mongodb-introduction.md). 

Bu öğretici hello aşağıdaki görevleri içerir:

> [!div class="checklist"]
> * Azure Cosmos DB hesabı oluşturma 
> * Bağlantı dizenizi güncelleştirme
> * Bir sanal makinede bir MongoDB uygulaması oluşturma 


## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.  

> [!TIP]
> * Zaten Azure Cosmos DB hesabınız var mı? Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)
> * Bir Azure DocumentDB hesabına sahip miydiniz? Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).  
> * Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

1. Hello Azure portalında, hello içinde **Azure Cosmos DB** sayfasında, hello API MongoDB hesabı seçin. 
2. Merhaba sol hello hesabı dikey çubuğunda, **Hızlı Başlangıç**. 
3. Platformunuzu seçin (*.NET sürücü*, *Node.js sürücü*, *MongoDB Kabuk*, *Java sürücü*, *Python sürücü*). Sürücü veya listelenen aracı görmüyorsanız, endişelenmeyin, biz sürekli olarak daha fazla bağlantı kod parçacıkları belge. 
4. MongoDB uygulamanıza hello kod parçacığını yapıştırın ve hazır toogo demektir.

## <a name="set-up-your-mongodb-app"></a>MongoDB uygulamanızı ayarlayın

Merhaba kullanabilirsiniz [azure'da bir sanal makinede çalışan tooMongoDB bağlanan bir web uygulaması oluşturma](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) eğitmen, en az değişiklik, tooquickly Kurulum MongoDB uygulama (yerel olarak ya da veya yayımlanan tooan Azure web uygulaması), tooan API MongoDB hesabının bağlanır.  

1. Bir değişiklik ile Merhaba öğreticisini izleyin.  Merhaba Dal.cs kod bu ile değiştirin:

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

2. Hesap ayarlarınızı başına hello Dal.cs dosyasındaki değişkenleri hello Azure Portalı'nda hello anahtarları sayfasından aşağıdaki hello değiştirin:

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Merhaba uygulama kullanın!

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın. 

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Azure Cosmos DB hesabı oluşturma 
> * Bağlantı dizenizi güncelleştirme
> * Bir sanal makinede bir MongoDB uygulaması oluşturma

Toohello sonraki öğretici devam ve MongoDB veri tooAzure Cosmos DB içe aktarabilirsiniz.  

> [!div class="nextstepaction"]
> [Azure Cosmos DB’ye MongoDB verileri aktarma](mongodb-migrate.md)


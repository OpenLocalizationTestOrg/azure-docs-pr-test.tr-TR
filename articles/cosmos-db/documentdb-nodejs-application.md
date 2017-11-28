---
title: "aaaBuild bir Node.js web uygulaması için Azure Cosmos DB | Microsoft Docs"
description: "Bu Node.js Öğreticisi nasıl toouse Microsoft Azure Cosmos DB toostore ve erişim verilerini bir Node.js Express web uygulamasından Azure Web Siteleri'nde barındırılan araştırır."
keywords: "Uygulama geliştirme, veritabanı Öğreticisi, node.js, node.js Öğreticisi öğrenin"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="57de8-104"><a name="_Toc395783175"></a>Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="57de8-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57de8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="57de8-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="57de8-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="57de8-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="57de8-107">Java</span><span class="sxs-lookup"><span data-stu-id="57de8-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="57de8-108">Python</span><span class="sxs-lookup"><span data-stu-id="57de8-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="57de8-109">Bu Node.js Öğreticisi nasıl toouse Azure Cosmos DB ve hello bir Node.js Express uygulamasında DocumentDB API toostore ve erişim verileri Azure Web Siteleri'nde barındırılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="57de8-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="57de8-110">Görevlerin oluşturulmasını, alınmasını ve tamamlanmasını sağlayan basit bir web tabanlı görev yönetimi uygulaması, yani yapılacak işler uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="57de8-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="57de8-111">Merhaba görevleri Azure Cosmos DB JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="57de8-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="57de8-112">Bu öğretici hello oluşturulmasını ve dağıtımını hello uygulama anlatılmaktadır ve her parçasında neler olduğunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="57de8-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Merhaba bu Node.js öğreticisinde oluşturulan Yapılacaklar listem uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="57de8-114">Yoksa zaman toocomplete hello öğretici ve yalnızca tooget hello eksiksiz çözüm istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="57de8-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="57de8-115">Bir sorun hello tam örnek çözümü alabilirsiniz [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="57de8-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="57de8-116">Merhaba okunan [Benioku](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) dosyası nasıl toorun hello uygulama hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="57de8-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="57de8-117"><a name="_Toc395783176"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="57de8-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="57de8-118">Bu Node.js öğreticisi, Node.js ve Azure Web Siteleri'ni kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="57de8-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="57de8-119">Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="57de8-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="57de8-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="57de8-120">An active Azure account.</span></span> <span data-ttu-id="57de8-121">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57de8-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="57de8-122">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57de8-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="57de8-123">OR</span><span class="sxs-lookup"><span data-stu-id="57de8-123">OR</span></span>

   <span data-ttu-id="57de8-124">Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md) (yalnızca Windows).</span><span class="sxs-lookup"><span data-stu-id="57de8-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="57de8-125">[Node.js][Node.js] sürüm v0.10.29 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="57de8-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="57de8-126">[Express oluşturucu](http://www.expressjs.com/starter/generator.html) (bunu `npm install express-generator -g` aracılığıyla yükleyebilirsiniz)</span><span class="sxs-lookup"><span data-stu-id="57de8-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="57de8-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="57de8-127">[Git][Git].</span></span>

## <span data-ttu-id="57de8-128"><a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57de8-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="57de8-129">İlk olarak bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="57de8-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="57de8-130">Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: yeni bir Node.js uygulaması oluşturma](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="57de8-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="57de8-131"><a name="_Toc395783178"></a>2. adım: yeni bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="57de8-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="57de8-132">Şimdi toocreate hello kullanarak temel bir Hello World Node.js projesi öğrenelim [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="57de8-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="57de8-133">Merhaba Node.js komut istemi gibi sık kullandığınız Terminali açın.</span><span class="sxs-lookup"><span data-stu-id="57de8-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="57de8-134">Toostore hello yeni uygulama istediğiniz toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="57de8-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="57de8-135">Yeni bir uygulama olarak adlandırılan hello express oluşturucuyu toogenerate kullanmak **Yapılacaklar**.</span><span class="sxs-lookup"><span data-stu-id="57de8-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="57de8-136">Yeni **todo** dizininizi açın ve bağımlılıkları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="57de8-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="57de8-137">Yeni uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57de8-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="57de8-138">Tarayıcınız çok giderek yeni uygulamanızı görüntüleyebilirsiniz[http://localhost: 3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="57de8-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Node.js - hello bir tarayıcı penceresinde Hello World uygulamasının ekran görüntüsü öğrenin](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="57de8-140">Ardından, uygulama Merhaba, terminal penceresinde hello CTRL + C tuşlarına basın ve ardından toostop **y** tooterminate hello toplu iş.</span><span class="sxs-lookup"><span data-stu-id="57de8-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="57de8-141"><a name="_Toc395783179"></a>3. Adım: Ek modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="57de8-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="57de8-142">Merhaba **package.json** dosya hello hello proje kökünde oluşturulan hello dosyaları biridir.</span><span class="sxs-lookup"><span data-stu-id="57de8-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="57de8-143">Bu dosya, Node.js uygulamanız için gerekli olan ek modüllerin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="57de8-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="57de8-144">Daha sonra bu uygulama tooAzure Web siteleri dağıttığınızda, bu dosya üzerinde Azure toosupport uygulamanızın hangi modülleri gerek toobe yüklü kullanılan toodetermine ' dir.</span><span class="sxs-lookup"><span data-stu-id="57de8-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="57de8-145">Hala tooinstall iki daha fazla paket Bu öğretici için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="57de8-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="57de8-146">Merhaba geri hello terminal, yükleme **zaman uyumsuz** npm aracılığıyla modülü.</span><span class="sxs-lookup"><span data-stu-id="57de8-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="57de8-147">Merhaba yüklemek **documentdb** npm aracılığıyla modülü.</span><span class="sxs-lookup"><span data-stu-id="57de8-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="57de8-148">Bu tüm hello Azure Cosmos DB Sihirli nerede olacağını hello modülüdür.</span><span class="sxs-lookup"><span data-stu-id="57de8-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="57de8-149">Merhaba Hızlı Kontrol **package.json** hello uygulama dosyasının ek modüller hello göster.</span><span class="sxs-lookup"><span data-stu-id="57de8-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="57de8-150">Bu dosyayı Azure hangi paketlerin toodownload söyleyin ve uygulamanızı çalıştırırken yükleyin.</span><span class="sxs-lookup"><span data-stu-id="57de8-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="57de8-151">Merhaba aşağıdaki örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="57de8-151">It should resemble hello example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="57de8-152">Bu düğüm, Düğüme (ve daha sonra Azure’a) uygulamanızın bu ek modüllere bağlı olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="57de8-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="57de8-153"><a name="_Toc395783180"></a>4. adım: hello Azure Cosmos DB hizmeti bir düğüm uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="57de8-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="57de8-154">Tüm hello ilk kurulumu ve yapılandırması, şimdi şimdi get mvc'deki toowhy burada çalışıyoruz ve Azure Cosmos DB kullanarak bazı kod toowrite olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="57de8-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="57de8-155">Merhaba modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="57de8-155">Create hello model</span></span>
1. <span data-ttu-id="57de8-156">Merhaba proje dizininde adlı yeni bir dizin oluşturun **modelleri** hello içinde hello package.json dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="57de8-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="57de8-157">Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="57de8-158">Bu dosya, uygulamamız tarafından oluşturulan hello görevler için hello modeli içerecektir.</span><span class="sxs-lookup"><span data-stu-id="57de8-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="57de8-159">İçinde aynı hello **modelleri** dizin adlı başka bir yeni dosya oluşturun **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="57de8-160">Bu dosya, uygulama genelinde kullanacağımız bazı yararlı ve yeniden kullanılabilir kodları içerir.</span><span class="sxs-lookup"><span data-stu-id="57de8-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="57de8-161">Kopya hello aşağıdaki kod içinde çok**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="57de8-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="57de8-162">Kaydet ve Kapat hello **docdbUtils.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="57de8-163">Merhaba hello başında **taskDao.js** dosya, aşağıdaki kod tooreference hello hello eklemek **DocumentDBClient** ve hello **docdbUtils.js** yukarıda oluşturduğumuz:</span><span class="sxs-lookup"><span data-stu-id="57de8-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="57de8-164">Ardından, kodu toodefine ekleyin ve hello görev nesneyi verin.</span><span class="sxs-lookup"><span data-stu-id="57de8-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="57de8-165">Bu kod Task nesnemizin başlatılmasından ve veritabanı ve belge kullanacağız koleksiyonunu hello ayarlama sorumludur.</span><span class="sxs-lookup"><span data-stu-id="57de8-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="57de8-166">Ardından, kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello Azure Cosmos DB içinde depolanan verileri ile etkileşim sağlayan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="57de8-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="57de8-167">Kaydet ve Kapat hello **taskDao.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="57de8-168">Merhaba denetleyicisi oluşturun</span><span class="sxs-lookup"><span data-stu-id="57de8-168">Create hello controller</span></span>
1. <span data-ttu-id="57de8-169">Merhaba, **yollar** , projenizin dizin adlı yeni bir dosya oluşturun **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="57de8-170">Kod çok aşağıdaki hello eklemek**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="57de8-171">Bu tarafından kullanılan hello DocumentDBClient ve async modüllerini yükler **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="57de8-172">Bu ayrıca hello tanımlanan **TaskList** hello örneği geçirilen işlevi **görev** daha önce tanımladığımız:</span><span class="sxs-lookup"><span data-stu-id="57de8-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="57de8-173">Toohello eklemeye devam **tasklist.js** çok kullanılan hello yöntemleri ekleyerek dosya**showTasks, addTask**, ve **tasklist.js**:</span><span class="sxs-lookup"><span data-stu-id="57de8-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="57de8-174">Kaydet ve Kapat hello **tasklist.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="57de8-175">Config.js ekleme</span><span class="sxs-lookup"><span data-stu-id="57de8-175">Add config.js</span></span>
1. <span data-ttu-id="57de8-176">Proje dizininizde **config.js** adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="57de8-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="57de8-177">Çok Hello ekleyin**config.js**.</span><span class="sxs-lookup"><span data-stu-id="57de8-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="57de8-178">Bu, uygulamamız için gereken yapılandırma ayarlarını ve değerlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57de8-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="57de8-179">Merhaba, **config.js** dosya, güncelleştirme hello değerleri HOST ve auth_key değerlerini hello Azure Cosmos DB hesabınızdaki hello anahtarlar dikey penceresinde bulunan hello değerleri kullanarak [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="57de8-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="57de8-180">Kaydet ve Kapat hello **config.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="57de8-181">App.js'yi değiştirme</span><span class="sxs-lookup"><span data-stu-id="57de8-181">Modify app.js</span></span>
1. <span data-ttu-id="57de8-182">Merhaba Hello proje dizininde açın **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="57de8-183">Merhaba Express web uygulaması oluşturduğunuzda bu dosya daha önce oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="57de8-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="57de8-184">Aşağıdaki kod toohello üstündeki hello eklemek **app.js**</span><span class="sxs-lookup"><span data-stu-id="57de8-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="57de8-185">Bu kod kullanılan hello yapılandırma dosyası toobe tanımlar ve tooread değerleri bu dosyadan yakında kullanacağımız bazı değişkenlere devam eder.</span><span class="sxs-lookup"><span data-stu-id="57de8-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="57de8-186">Aşağıdaki iki satırı hello yerine **app.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="57de8-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="57de8-187">Aşağıdaki kod parçacığında hello ile:</span><span class="sxs-lookup"><span data-stu-id="57de8-187">with hello following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="57de8-188">Bu satırlar yeni bir örneğini tanımlar bizim **Config.js** nesnesiyle yeni bir bağlantı tooAzure Cosmos DB (okunan hello hello değerleri kullanarak **config.js**), hello görev nesnesini başlatır ve ardından form eylemlerini bağlama üzerinde toomethods bizim **TaskList** denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="57de8-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="57de8-189">Son olarak, Kaydet ve Kapat hello **app.js** dosya, biz işimiz neredeyse bitti.</span><span class="sxs-lookup"><span data-stu-id="57de8-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="57de8-190"><a name="_Toc395783181"></a>5. Adım: Kullanıcı arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="57de8-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="57de8-191">Şimdi uygulamamız ile bir kullanıcı gerçekte etkileşim kurabilmesi bizim dikkat toobuilding hello kullanıcı arabirimi dönelim.</span><span class="sxs-lookup"><span data-stu-id="57de8-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="57de8-192">kullandığı oluşturduğumuz Express uygulaması hello **Jade** hello görüntüleme altyapısı olarak.</span><span class="sxs-lookup"><span data-stu-id="57de8-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="57de8-193">Jade hakkında daha fazla bilgi için lütfen çok başvurun[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="57de8-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="57de8-194">Merhaba **layout.jade** hello dosyasında **görünümleri** dizin kullanılan genel bir şablon olarak diğer **.jade** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="57de8-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="57de8-195">Bu adımda, toouse değiştirecek [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir Web sitesi kolaylaştıran bir araç olan.</span><span class="sxs-lookup"><span data-stu-id="57de8-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="57de8-196">Açık hello **layout.jade** dosyası bulundu hello **görünümleri** hello aşağıdaki klasörü ve Değiştir hello içeriğiyle:</span><span class="sxs-lookup"><span data-stu-id="57de8-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="57de8-197">Bu hello etkili bir şekilde söyler **Jade** toorender uygulamamız için bazı HTML altyapısı ve oluşturur bir **blok** adlı **içerik** burada biz tedarik hello düzeni bizim içerik için sayfaları.</span><span class="sxs-lookup"><span data-stu-id="57de8-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="57de8-198">Bu **layout.jade** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="57de8-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="57de8-199">Şimdi hello açmak **index.jade** dosya, uygulamamız tarafından kullanılacak olan ve hello dosyanın Merhaba içeriğine hello şununla değiştirin hello görünümü:</span><span class="sxs-lookup"><span data-stu-id="57de8-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="57de8-200">Bu, düzeni genişletir ve içerik Merhaba sağlayan **içerik** hello gördüğümüz yer tutucu **layout.jade** önceki dosya.</span><span class="sxs-lookup"><span data-stu-id="57de8-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="57de8-201">Bu düzende iki HTML formu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="57de8-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="57de8-202">Merhaba ilk formu içeren bir tablo için verilerimizi ve bize çok göndererek tooupdate öğeleri sağlayan bir düğmeyi**/completetask** denetleyicimizin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="57de8-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="57de8-203">Merhaba ikinci formu içeren bize çok göndererek toocreate yeni bir öğe sağlayan bir düğmeyi ve iki giriş alanını**/addtask** denetleyicimizin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="57de8-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="57de8-204">Bu bizim uygulama toowork için ihtiyacımız tüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57de8-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="57de8-205"><a name="_Toc395783181"></a>6. Adım: Uygulamanızı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="57de8-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="57de8-206">tootest hello uygulamayı yerel makinenizde çalıştırma `npm start` terminal toostart uygulamanızı hello ve ardından yenileme, [http://localhost: 3000](http://localhost:3000) tarayıcı sayfası.</span><span class="sxs-lookup"><span data-stu-id="57de8-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="57de8-207">Başlangıç sayfasında, aşağıdaki hello görüntü gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="57de8-207">hello page should now look like hello image below:</span></span>
   
    ![Merhaba bir tarayıcı penceresinde Yapılacaklar listem uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="57de8-209">Merhaba layout.jade dosyasında veya hello index.jade dosyasında hello girinti hakkında bir hata alırsanız, her iki dosya hello ilk iki satır sola hizalı olduğunu, boşluk emin olun.</span><span class="sxs-lookup"><span data-stu-id="57de8-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="57de8-210">Merhaba ilk iki satır önce boşluklar varsa, bunları kaldırmanız, her iki dosya kaydedin, sonra tarayıcı pencerenizi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="57de8-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="57de8-211">Merhaba öğesi, öğe adı ve kategori alanlarını tooenter yeni bir görev kullanın ve ardından **Öğe Ekle**.</span><span class="sxs-lookup"><span data-stu-id="57de8-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="57de8-212">Bu işlemden sonra Azure Cosmos DB içinde bu özelliklere sahip bir belge oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57de8-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="57de8-213">Merhaba sayfa öğesi hello Yapılacaklar listesinde yeni oluşturulan toodisplay hello güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57de8-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Merhaba Yapılacaklar listesinde yeni bir öğesiyle hello uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="57de8-215">toocomplete bir görev yalnızca hello tam sütununda hello onay kutusunu işaretleyin ve ardından **güncelleştirme görevleri**.</span><span class="sxs-lookup"><span data-stu-id="57de8-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="57de8-216">Bu, önceden oluşturulmuş hello belge güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="57de8-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="57de8-217">toostop Merhaba uygulaması hello terminal penceresinde CTRL + C tuşlarına basın ve ardından **Y** tooterminate hello toplu iş.</span><span class="sxs-lookup"><span data-stu-id="57de8-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="57de8-218"><a name="_Toc395783182"></a>7. adım: uygulama geliştirme projesi tooAzure Web siteleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="57de8-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="57de8-219">Daha önce yapmadıysanız Azure Web Siteniz için bir git deposunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="57de8-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="57de8-220">Hakkında yönergeler bulabilirsiniz toodo bu hello [yerel Git dağıtımı tooAzure uygulama hizmeti](../app-service-web/app-service-deploy-local-git.md) konu.</span><span class="sxs-lookup"><span data-stu-id="57de8-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="57de8-221">Azure Web Sitenizi bir git uzak öğesi olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="57de8-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="57de8-222">Toohello uzak ileterek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="57de8-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="57de8-223">Birkaç saniye içinde git web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!</span><span class="sxs-lookup"><span data-stu-id="57de8-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="57de8-224">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="57de8-224">Congratulations!</span></span> <span data-ttu-id="57de8-225">Yalnızca ilk Node.js Express Web Azure Cosmos DB kullanarak uygulamanızı oluşturdunuz ve bunu tooAzure Web siteleri yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="57de8-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="57de8-226">Toodownload istediğiniz veya toohello eksiksiz başvuru uygulaması Bu öğretici için bkz, onu yüklenebilir [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="57de8-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="57de8-227"><a name="_Toc395637775"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57de8-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="57de8-228">Tooperform ölçek ve performans ile Azure Cosmos DB istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="57de8-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="57de8-229">Bkz. [Azure Cosmos DB ile Performans ve Ölçek Testi](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="57de8-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="57de8-230">Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="57de8-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="57de8-231">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="57de8-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="57de8-232">Merhaba keşfedin [Azure Cosmos DB belgeleri](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="57de8-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app


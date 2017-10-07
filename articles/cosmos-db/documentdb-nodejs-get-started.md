---
title: "hello Azure Cosmos DB için DocumentDB API için aaaNode.js Öğreticisi | Microsoft Docs"
description: "Cosmos DB hello DocumentDB API ile oluşturan bir Node.js Öğreticisi."
keywords: "node.js öğreticisi, düğüm veritabanı"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="ea0e2-104">Node.js Öğreticisi: DocumentDB API kullanımı hello Azure Cosmos DB toocreate bir Node.js konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="ea0e2-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea0e2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ea0e2-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="ea0e2-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ea0e2-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="ea0e2-107">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="ea0e2-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="ea0e2-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="ea0e2-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="ea0e2-109">Java</span><span class="sxs-lookup"><span data-stu-id="ea0e2-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="ea0e2-110">C++</span><span class="sxs-lookup"><span data-stu-id="ea0e2-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="ea0e2-111">Hello Azure Cosmos DB Node.js SDK'sı için toohello Node.js Öğreticisi Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="ea0e2-112">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="ea0e2-113">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-113">We'll cover:</span></span>

* <span data-ttu-id="ea0e2-114">Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="ea0e2-115">Uygulamanızı kurma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-115">Setting up your application</span></span>
* <span data-ttu-id="ea0e2-116">Düğüm veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-116">Creating a node database</span></span>
* <span data-ttu-id="ea0e2-117">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-117">Creating a collection</span></span>
* <span data-ttu-id="ea0e2-118">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-118">Creating JSON documents</span></span>
* <span data-ttu-id="ea0e2-119">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="ea0e2-119">Querying hello collection</span></span>
* <span data-ttu-id="ea0e2-120">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-120">Replacing a document</span></span>
* <span data-ttu-id="ea0e2-121">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-121">Deleting a document</span></span>
* <span data-ttu-id="ea0e2-122">Merhaba node veritabanı silme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-122">Deleting hello node database</span></span>

<span data-ttu-id="ea0e2-123">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="ea0e2-123">Don't have time?</span></span> <span data-ttu-id="ea0e2-124">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-124">Don't worry!</span></span> <span data-ttu-id="ea0e2-125">Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="ea0e2-126">Bkz: [alma hello eksiksiz bir çözüm](#GetSolution) hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="ea0e2-127">Merhaba Node.js öğreticisini tamamladıktan sonra lütfen hello kullan oylama hello üst ve alt bu sayfa toogive bize geri bildirim düğmeler.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="ea0e2-128">Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="ea0e2-129">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="ea0e2-130">Merhaba Node.js öğreticisi için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ea0e2-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="ea0e2-131">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="ea0e2-132">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-132">An active Azure account.</span></span> <span data-ttu-id="ea0e2-133">Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="ea0e2-134">Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="ea0e2-135">[Node.js](https://nodejs.org/) v0.10.29 sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="ea0e2-136">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="ea0e2-137">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="ea0e2-138">Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[Node.js uygulamanızı ayarlama](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="ea0e2-139">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[Node.js uygulamanızı ayarlama](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="ea0e2-140"><a id="SetupNode"></a>2. adım: Node.js uygulamanızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ea0e2-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="ea0e2-141">Sık kullandığınız terminali açın.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="ea0e2-142">Merhaba klasör veya toosave oluşturulacağı yeri dizin Node.js uygulamanızı bulun.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="ea0e2-143">Aşağıdaki komutları hello ile iki boş JavaScript dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="ea0e2-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="ea0e2-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="ea0e2-146">Merhaba npm aracılığıyla documentdb modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="ea0e2-147">Merhaba aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="ea0e2-148">Harika!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-148">Great!</span></span> <span data-ttu-id="ea0e2-149">Kurulumu tamamladığınıza göre, biraz kod yazmaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="ea0e2-150"><a id="Config"></a>3. Adım: Uygulamanızın yapılandırmalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="ea0e2-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="ea0e2-151">Sık kullandığınız metin düzenleyicisinde ```config.js``` öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="ea0e2-152">Ardından, kopyalama ve yapıştırma hello aşağıdaki kod parçacığında ve özelliklerini ayarlama ```config.endpoint``` ve ```config.primaryKey``` tooyour Azure Cosmos DB uç noktası URI ve birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="ea0e2-153">Her iki Bu yapılandırmalar hello bulunabilir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Node.js Öğreticisi - hello hello etkin hub ile bir Azure Cosmos DB hesabını gösteren Azure portal ekran görüntüsü vurgulanmış, üzerinde hello vurgulanmış hello Azure Cosmos DB hesabı dikey ve hello URI, birincil anahtar ve ikincil anahtar değerleri vurgulanmış hello ANAHTARLAR düğmesi Anahtarlar dikey penceresi - Node veritabanı][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="ea0e2-155">Kopyalama ve yapıştırma hello ```database id```, ```collection id```, ve ```JSON documents``` tooyour ```config``` ayarladığınız alttaki nesne, ```config.endpoint``` ve ```config.authKey``` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="ea0e2-156">İstediğiniz toostore veritabanınızda veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md) hello belge tanımları eklemek yerine.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="ea0e2-157">Merhaba veritabanı, koleksiyon ve belge tanımları, Azure Cosmos DB hareket edecek ```database id```, ```collection id```ve belgelerin verileri.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="ea0e2-158">Son olarak, dışarı aktarma, ```config``` nesne hello içinde başvurabilmek ```app.js``` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="ea0e2-159"><a id="Connect"></a>4. adım: tooan Azure Cosmos DB hesap bağlanma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="ea0e2-160">Boş açmak ```app.js``` hello metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="ea0e2-161">Tooimport hello aşağıda hello kodu kopyalayıp yapıştırın ```documentdb``` modülü ve yeni oluşturduğunuz ```config``` modülü.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="ea0e2-162">Daha önce kaydettiğiniz hello kod toouse hello kopyalayıp ```config.endpoint``` ve ```config.primaryKey``` toocreate yeni bir DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="ea0e2-163">Merhaba kod tooinitialize hello Azure Cosmos DB istemci sahip olduğunuza göre Azure Cosmos DB kaynaklarla çalışmak bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="ea0e2-164">5. Adım: Düğüm veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="ea0e2-165">Merhaba kodu kopyalayıp tooset hello HTTP durumu aşağıda bulunamadı, hello veritabanı url ve hello koleksiyonu URL'si yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="ea0e2-166">Bu URL'leri hello Azure Cosmos DB istemci hello doğru veritabanı ve koleksiyonu nasıl bulacaksınız ' dir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="ea0e2-167">A [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="ea0e2-168">Veritabanı hello mantıksal koleksiyonlar genelinde bölümlenmiş belge depolama alanının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="ea0e2-169">Kopyalama ve yapıştırma hello **getDatabase** hello ile Merhaba app.js dosyasında yeni veritabanınızı oluşturmak için işlevi ```id``` hello belirtilen ```config``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="ea0e2-170">Merhaba hello ile aynı veritabanı hello işlevi denetler ```FamilyRegistry``` kimliği zaten mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="ea0e2-171">Varsa yeni bir veritabanı oluşturmak yerine var olan veritabanını getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="ea0e2-172">Merhaba ayarladığınız hello aşağıdaki kodu yapıştırın **getDatabase** işlev tooadd hello yardımcı işlevini **çıkmak** yazdıracak hello çıkış iletisini ve hello çağrı çok**getDatabase** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-173">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-174">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-174">Congratulations!</span></span> <span data-ttu-id="ea0e2-175">Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="ea0e2-176"><a id="CreateColl"></a>6. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="ea0e2-177">**CreateDocumentCollectionAsync**, fiyatlandırmaya yönelik etkilere sahip yeni bir koleksiyon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="ea0e2-178">Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="ea0e2-179">A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="ea0e2-180">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="ea0e2-181">Kopyalama ve yapıştırma hello **Getfamilydocument** hello altında işlevi **getDatabase** hello ile yeni koleksiyonunuzu hello app.js dosya toocreate işlev ```id``` hello belirtilen```config```nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="ea0e2-182">Biz toomake yeniden kontrol edeceğiz emin ile bir koleksiyon hello aynı ```FamilyCollection``` kimliği zaten mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="ea0e2-183">Varsa yeni bir koleksiyon oluşturmak yerine var olan koleksiyonu getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="ea0e2-184">Merhaba çağrısı hello kodu çok kopyalayıp**getDatabase** tooexecute hello **Getfamilydocument** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-185">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-186">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-186">Congratulations!</span></span> <span data-ttu-id="ea0e2-187">Bir Azure Cosmos DB koleksiyonunu başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="ea0e2-188"><a id="CreateDoc"></a>7. Adım: Belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea0e2-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="ea0e2-189">A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="ea0e2-190">Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="ea0e2-191">Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="ea0e2-192">Kopyalama ve yapıştırma hello **getFamilyDocument** hello altında işlevi **Getfamilydocument** hello kaydedilmiş hello JSON verilerini içeren hello belgeleri oluşturmak için işlevi ```config``` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="ea0e2-193">Yeniden, biz toomake emin kontrol edeceğiz bir belgeyle hello aynı kimliği zaten mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="ea0e2-194">Merhaba çağrısı hello kodu çok kopyalayıp**Getfamilydocument** tooexecute hello **getFamilyDocument** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-195">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-196">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-196">Congratulations!</span></span> <span data-ttu-id="ea0e2-197">Bir Azure Cosmos DB belgesini başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js Öğreticisi - hello hello hesabı, hello veritabanı, hello koleksiyonu ve hello belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram - Node veritabanı](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="ea0e2-199"><a id="Query"></a>8. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="ea0e2-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="ea0e2-200">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="ea0e2-201">Merhaba aşağıdaki örnek kod koleksiyonunuzda hello belgeleri karşı çalıştırabileceğiniz bir sorguyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="ea0e2-202">Kopyalama ve yapıştırma hello **queryCollection** hello altında işlevi **getFamilyDocument** hello app.js dosyasında işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="ea0e2-203">Azure Cosmos DB, aşağıda gösterildiği gibi SQL benzeri sorguları destekler.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="ea0e2-204">Karmaşık sorgular derleme hakkında daha fazla bilgi için hello denetleyin [Query Playground](https://www.documentdb.com/sql/demo) ve hello [sorgu belgelerini](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="ea0e2-205">Aşağıdaki diyagramda hello nasıl hello Azure Cosmos DB SQL sorgusu söz dizimi karşı hello koleksiyonu olarak adlandırılır, oluşturduğunuz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Node.js Öğreticisi - hello kapsamını ve hello sorgunun anlamını diyagram - Node veritabanı](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="ea0e2-207">Merhaba [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları kapsamlı tooa tek koleksiyon zaten olduğu için anahtar sözcüğü hello sorguda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="ea0e2-208">Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="ea0e2-209">Azure Cosmos DB aileleri, kök veya hello değişken adı, seçtiğiniz, başvuru hello geçerli koleksiyonu varsayılan olarak Infer.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="ea0e2-210">Merhaba çağrısı hello kodu çok kopyalayıp**getFamilyDocument** tooexecute hello **queryCollection** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-211">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-212">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-212">Congratulations!</span></span> <span data-ttu-id="ea0e2-213">Başarılı bir şekilde Azure Cosmos DB belgelerini sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="ea0e2-214"><a id="ReplaceDocument"></a>9. Adım: Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="ea0e2-215">Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="ea0e2-216">Kopyalama ve yapıştırma hello **replaceFamilyDocument** hello altında işlevi **queryCollection** hello app.js dosyasında işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="ea0e2-217">Merhaba çağrısı hello kodu çok kopyalayıp**queryCollection** tooexecute hello **replaceDocument** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="ea0e2-218">Ayrıca, hello kod toocall ekleme **queryCollection** yeniden tooverify hello Belge başarıyla değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-219">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-220">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-220">Congratulations!</span></span> <span data-ttu-id="ea0e2-221">Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ea0e2-222"><a id="DeleteDocument"></a>10. Adım: Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="ea0e2-223">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="ea0e2-224">Kopyalama ve yapıştırma hello **deleteFamilyDocument** hello altında işlevi **replaceFamilyDocument** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="ea0e2-225">Merhaba çağrısı toohello hello kodu ikinci kopyalayıp **queryCollection** tooexecute hello **deleteDocument** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-226">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-227">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-227">Congratulations!</span></span> <span data-ttu-id="ea0e2-228">Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ea0e2-229"><a id="DeleteDatabase"></a>11. adım: hello Node veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="ea0e2-230">Veritabanı oluşturulan silme hello hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="ea0e2-231">Kopyalama ve yapıştırma hello **Temizleme** hello altında işlevi **deleteFamilyDocument** tooremove hello veritabanı ve tüm hello alt kaynaklarını işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="ea0e2-232">Merhaba çağrısı hello kodu çok kopyalayıp**deleteFamilyDocument** tooexecute hello **Temizleme** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="ea0e2-233"><a id="Run"></a>12. Adım: Node.js uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="ea0e2-234">Tamamen işlevlerinizi çağırma hello dizisi aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="ea0e2-235">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="ea0e2-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="ea0e2-236">Merhaba Başlarken uygulamanızın çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="ea0e2-237">Merhaba çıktı hello örnek metinle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-237">hello output should match hello example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

<span data-ttu-id="ea0e2-238">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-238">Congratulations!</span></span> <span data-ttu-id="ea0e2-239">Oluşturduğunuz hello Node.js öğreticisini tamamladınız ve İlk Azure Cosmos DB konsol uygulamanız sahip!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="ea0e2-240"><a id="GetSolution"></a>Merhaba eksiksiz Node.js Öğreticisi çözümünü edinme</span><span class="sxs-lookup"><span data-stu-id="ea0e2-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="ea0e2-241">Bu öğreticide adımları hello ya da yalnızca toodownload hello kod istediğiniz zaman toocomplete varsa alamadık, buradan edinebilirsiniz [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="ea0e2-242">Bu makaledeki tüm hello örnekleri içeren toorun hello GetStarted çözümünü hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="ea0e2-243">[Azure Cosmos DB hesabı][create-account].</span><span class="sxs-lookup"><span data-stu-id="ea0e2-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="ea0e2-244">Merhaba [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) çözüm Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="ea0e2-245">Merhaba yüklemek **documentdb** npm aracılığıyla modülü.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="ea0e2-246">Merhaba aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ea0e2-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="ea0e2-247">Merhaba sonraki ```config.js``` dosya, güncelleştirme hello config.endpoint ve config.authKey değerlerini açıklandığı gibi [3. adım: uygulamanızın yapılandırmalarını ayarlama](#Config).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="ea0e2-248">Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="ea0e2-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="ea0e2-249">Hepsi bu kadar, derleyin ve devam edin!</span><span class="sxs-lookup"><span data-stu-id="ea0e2-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ea0e2-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea0e2-250">Next steps</span></span>
* <span data-ttu-id="ea0e2-251">Daha karmaşık bir Node.js örneği ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="ea0e2-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="ea0e2-252">Bkz. [Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="ea0e2-253">Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="ea0e2-254">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="ea0e2-255">Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="ea0e2-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png

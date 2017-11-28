---
title: "Hello Azure tablo hizmeti kullanarak aaaNode.js web uygulaması"
description: "Bu öğretici nasıl toouse hello Azure Table hizmet Azure App Service Web Apps içinde barındırılan bir Node.js uygulamasında toostore verileri öğretir."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="5b658-103">Hello Azure tablo hizmeti kullanarak Node.js web uygulaması</span><span class="sxs-lookup"><span data-stu-id="5b658-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="5b658-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5b658-104">Overview</span></span>
<span data-ttu-id="5b658-105">Bu öğreticide, Azure veri yönetimi toostore ve erişim verilerini nasıl toouse tablo hizmeti sağladığı gösterilmiştir bir [düğümü] uygulama barındırılan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="5b658-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="5b658-106">Bu öğretici, düğüm kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar ve [Git].</span><span class="sxs-lookup"><span data-stu-id="5b658-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="5b658-107">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="5b658-107">You will learn:</span></span>

* <span data-ttu-id="5b658-108">Nasıl toouse npm (düğüm paketi Yöneticisi) tooinstall hello düğümü modülleri</span><span class="sxs-lookup"><span data-stu-id="5b658-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="5b658-109">Nasıl toowork ile hello Azure tablo hizmeti</span><span class="sxs-lookup"><span data-stu-id="5b658-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="5b658-110">Nasıl toouse hello Azure CLI toocreate bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5b658-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="5b658-111">Bu öğreticiyi izleyerek, basit bir web tabanlı oluşturacaksınız oluşturulmasını, alınmasını ve görevleri tamamlama sağlayan "Yapılacaklar listesi" uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5b658-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="5b658-112">Merhaba görevleri hello tablo hizmetinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="5b658-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="5b658-113">Tamamlanan Merhaba uygulaması şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5b658-113">Here is hello completed application:</span></span>

![Boş bir tasklist görüntüleyen bir web sayfası][node-table-finished]

> [!NOTE]
> <span data-ttu-id="5b658-115">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b658-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5b658-116">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5b658-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5b658-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5b658-117">Prerequisites</span></span>
<span data-ttu-id="5b658-118">Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="5b658-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="5b658-119">[düğümü] sürüm 0.10.24 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="5b658-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="5b658-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="5b658-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="5b658-121">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-121">Create a storage account</span></span>
<span data-ttu-id="5b658-122">Bir Azure Storage hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b658-122">Create an Azure storage account.</span></span> <span data-ttu-id="5b658-123">Merhaba uygulama bu hesabı toostore hello Yapılacaklar öğelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5b658-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="5b658-124">Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b658-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b658-125">Merhaba tıklatın **yeni** hello alt simgesine sol hello portallarına, ardından **veri + depolama** > **depolama**.</span><span class="sxs-lookup"><span data-stu-id="5b658-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="5b658-126">Merhaba depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.</span><span class="sxs-lookup"><span data-stu-id="5b658-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Yeni düğmesi](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="5b658-128">Merhaba depolama hesabı oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve hello depolama hesabının dikey penceresi açık toohello yeni kaynak ait tooshow grubunu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5b658-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="5b658-129">Merhaba depolama hesabı dikey penceresinde tıklayın **ayarları** > **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="5b658-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="5b658-130">Merhaba birincil erişim anahtarı toohello panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b658-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Erişim anahtarı][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="5b658-132">Modüllerini yükleyin ve yapı iskelesi oluştur</span><span class="sxs-lookup"><span data-stu-id="5b658-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="5b658-133">Bu bölümde yeni bir düğüm uygulama oluşturma ve npm tooadd modülü paketleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="5b658-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="5b658-134">Bu uygulama için hello kullanacağı [Express] ve [Azure] modüller.</span><span class="sxs-lookup"><span data-stu-id="5b658-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="5b658-135">Hello Express modülü düğümü için bir Model View Controller çerçeve sağlar, başlangıç sırasında Azure modülleri bağlantı toohello tablo hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b658-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="5b658-136">Hızlı yükleme ve yapı iskelesi oluştur</span><span class="sxs-lookup"><span data-stu-id="5b658-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="5b658-137">Merhaba komut satırından adlı yeni bir dizin oluşturma **tasklist** ve anahtar toothat dizin.</span><span class="sxs-lookup"><span data-stu-id="5b658-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="5b658-138">Komut tooinstall hello Express Modülü aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="5b658-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="5b658-139">Merhaba işletim sistemine bağlı olarak tooput 'sudo' hello komutundan önce gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="5b658-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="5b658-140">Aşağıdaki örneğine benzer toohello Hello çıktı görünür:</span><span class="sxs-lookup"><span data-stu-id="5b658-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="5b658-141">Merhaba '-g' parametresi hello modülü genel olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="5b658-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="5b658-142">Bu şekilde kullanırız **express** ek yol bilgileri tootype kalmadan toogenerate web uygulama iskele.</span><span class="sxs-lookup"><span data-stu-id="5b658-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="5b658-143">Merhaba uygulaması için toocreate hello askılamayı girin hello **express** komutu:</span><span class="sxs-lookup"><span data-stu-id="5b658-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="5b658-144">Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="5b658-144">hello output of this command appears similar toohello following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="5b658-145">Şimdi birkaç yeni dizin ve dosyaların hello sahip **tasklist** dizin.</span><span class="sxs-lookup"><span data-stu-id="5b658-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="5b658-146">Ek modüller yükleme</span><span class="sxs-lookup"><span data-stu-id="5b658-146">Install additional modules</span></span>
<span data-ttu-id="5b658-147">Merhaba birini dosyaları **express** oluşturur olan **package.json**.</span><span class="sxs-lookup"><span data-stu-id="5b658-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="5b658-148">Bu dosya modülü bağımlılıkları listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="5b658-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="5b658-149">Daha sonra hello uygulama tooApp Service Web Apps dağıttığınızda, bu dosyayı Azure üzerinde yüklü toobe modüllerine gereksinim belirler.</span><span class="sxs-lookup"><span data-stu-id="5b658-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="5b658-150">Komut satırı Hello, komut tooinstall hello modülleri hello açıklanan aşağıdaki hello girin **package.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="5b658-151">Toouse 'sudo' gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5b658-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="5b658-152">Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="5b658-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="5b658-153">Ardından, komut tooinstall hello aşağıdaki hello girin [azure], [düğümü UUID], [nconf] ve [zaman uyumsuz] modülleri:</span><span class="sxs-lookup"><span data-stu-id="5b658-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="5b658-154">Merhaba **--Kaydet** bayrağı ekler bu modülleri toohello girişlerinde **package.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="5b658-155">Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="5b658-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="5b658-156">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-156">Create hello application</span></span>
<span data-ttu-id="5b658-157">Şimdi hazır toobuild Merhaba uygulaması demektir.</span><span class="sxs-lookup"><span data-stu-id="5b658-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="5b658-158">Bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-158">Create a model</span></span>
<span data-ttu-id="5b658-159">A *modeli* uygulamanızdaki hello verileri temsil eden bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="5b658-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="5b658-160">Merhaba uygulaması için hello yalnızca hello Yapılacaklar listesi bir öğeyi temsil eden bir görev nesnesi modelidir.</span><span class="sxs-lookup"><span data-stu-id="5b658-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="5b658-161">Görev alanları izleyen hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="5b658-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="5b658-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="5b658-162">PartitionKey</span></span>
* <span data-ttu-id="5b658-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="5b658-163">RowKey</span></span>
* <span data-ttu-id="5b658-164">adı (dize)</span><span class="sxs-lookup"><span data-stu-id="5b658-164">name (string)</span></span>
* <span data-ttu-id="5b658-165">Kategori (dize)</span><span class="sxs-lookup"><span data-stu-id="5b658-165">category (string)</span></span>
* <span data-ttu-id="5b658-166">Tamamlanan (Boole)</span><span class="sxs-lookup"><span data-stu-id="5b658-166">completed (Boolean)</span></span>

<span data-ttu-id="5b658-167">**PartitionKey** ve **RowKey** hello tablo hizmeti tarafından tablo anahtarlar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b658-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="5b658-168">Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b658-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="5b658-169">Merhaba, **tasklist** dizin adlı yeni bir dizin oluşturun **modelleri**.</span><span class="sxs-lookup"><span data-stu-id="5b658-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="5b658-170">Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**.</span><span class="sxs-lookup"><span data-stu-id="5b658-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="5b658-171">Bu dosya, uygulamanız tarafından oluşturulan hello görevler için hello modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="5b658-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="5b658-172">Merhaba hello başında **task.js** dosya, aşağıdaki kodu tooreference gerekli kitaplıkları hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5b658-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="5b658-173">Merhaba aşağıdaki toodefine kod ve hello görev nesne dışarı aktarma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b658-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="5b658-174">Bu nesne, toohello tablo bağlamak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="5b658-174">This object is responsible for connecting toohello table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="5b658-175">Kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello hello tablosunda depolanan veriler ile etkileşim sağlayan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5b658-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="5b658-176">Kaydet ve Kapat hello **task.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="5b658-177">Bir denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-177">Create a controller</span></span>
<span data-ttu-id="5b658-178">A *denetleyicisi* HTTP isteklerini işler ve hello HTML yanıt işler.</span><span class="sxs-lookup"><span data-stu-id="5b658-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="5b658-179">Merhaba, **tasklist/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="5b658-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="5b658-180">Kod çok aşağıdaki hello eklemek**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5b658-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="5b658-181">Bu tarafından kullanılan hello azure ve async modüllerini yükler **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5b658-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="5b658-182">Bu ayrıca hello tanımlar **TaskList** hello örneği geçirilen işlevi **görev** daha önce tanımladığımız:</span><span class="sxs-lookup"><span data-stu-id="5b658-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="5b658-183">Tanımlayan bir **TaskList** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5b658-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="5b658-184">Yöntemleri çok aşağıdaki hello eklemek**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="5b658-184">Add hello following methods too**TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="5b658-185">App.js'yi değiştirme</span><span class="sxs-lookup"><span data-stu-id="5b658-185">Modify app.js</span></span>
1. <span data-ttu-id="5b658-186">Merhaba gelen **tasklist** dizin, açık hello **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="5b658-187">Merhaba çalıştırarak bu dosya daha önce oluşturulmuş **express** komutu.</span><span class="sxs-lookup"><span data-stu-id="5b658-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="5b658-188">Merhaba dosya Hello başında tooload hello azure modülü, kümesi hello tablo adı, bölüm anahtarı ve kümesi hello depolama Bu örnek tarafından kullanılan kimlik bilgileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5b658-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="5b658-189">ortam değişkenleri veya hello nconf hello yapılandırma değerlerini yükler **config.json** daha sonra oluşturacağız dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="5b658-190">Merhaba app.js dosyasında gördüğünüz toowhere kaydırarak hello satırı:</span><span class="sxs-lookup"><span data-stu-id="5b658-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="5b658-191">Satırları yukarıda Hello aşağıda gösterilen hello kod ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5b658-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="5b658-192">Bu örneği başlatılamıyor <strong>görev</strong> bağlantı tooyour depolama hesabına sahip.</span><span class="sxs-lookup"><span data-stu-id="5b658-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="5b658-193">Bu toohello geçirilen <strong>TaskList</strong>, hangi kullanır, toocommunicate hello tablo hizmeti ile:</span><span class="sxs-lookup"><span data-stu-id="5b658-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="5b658-194">Merhaba Kaydet **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="5b658-195">Merhaba dizini görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="5b658-195">Modify hello index view</span></span>
1. <span data-ttu-id="5b658-196">Açık hello **tasklist/views/index.jade** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="5b658-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="5b658-197">Merhaba dosyanın tüm içeriğini Hello koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5b658-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="5b658-198">Bu, var olan görevleri görüntüler ve yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form içeren bir görünüm tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5b658-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
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
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="5b658-199">Kaydet ve Kapat **index.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="5b658-200">Merhaba genel düzenini değiştirme</span><span class="sxs-lookup"><span data-stu-id="5b658-200">Modify hello global layout</span></span>
<span data-ttu-id="5b658-201">Merhaba **layout.jade** hello dosyasında **görünümleri** dizindir diğer genel bir şablon **.jade** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="5b658-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="5b658-202">Bu adımda, toouse değiştirecek [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir web uygulaması kolaylaştıran bir araç olan.</span><span class="sxs-lookup"><span data-stu-id="5b658-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="5b658-203">Karşıdan yükleyip hello dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="5b658-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="5b658-204">Kopya hello **bootstrap.min.css** hello önyükleme dosyasından **css** hello klasörüne **ortak/stil sayfaları** uygulamanızın dizin.</span><span class="sxs-lookup"><span data-stu-id="5b658-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="5b658-205">Merhaba gelen **görünümleri** klasörü, açık **layout.jade** ve hello tüm içeriği hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="5b658-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="5b658-206">Bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-206">Create a config file</span></span>
<span data-ttu-id="5b658-207">yerel olarak toorun hello uygulama için biz bir yapılandırma dosyasına Azure depolama kimlik put.</span><span class="sxs-lookup"><span data-stu-id="5b658-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="5b658-208">Adlı bir dosya oluşturun **config.json* * JSON aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="5b658-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="5b658-209">Değiştir **depolama hesabı adı** hello depolama hello adla daha önce oluşturduğunuz hesap ve değiştirme **depolama erişim tuşu** hello depolama hesabınız için birincil erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="5b658-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="5b658-210">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5b658-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="5b658-211">Bu dosyayı kaydetmek *daha yüksek bir dizin düzeyinde* hello daha **tasklist** dizin şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="5b658-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="5b658-212">Bunu yapmak için hello hello config dosya kaynak denetimine denetimi tooavoid Burada, genel hale gelebilir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="5b658-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="5b658-213">Biz hello uygulama tooAzure dağıttığınızda, bir yapılandırma dosyası yerine ortam değişkenleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="5b658-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="5b658-214">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5b658-214">Run hello application locally</span></span>
<span data-ttu-id="5b658-215">yerel makinenizde tootest Merhaba uygulaması hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b658-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="5b658-216">Komut satırı Hello, dizinleri toohello değiştirme **tasklist** dizin.</span><span class="sxs-lookup"><span data-stu-id="5b658-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="5b658-217">Komut toolaunch hello uygulama yerel olarak aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5b658-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="5b658-218">Bir web tarayıcısı açın ve toohttp://127.0.0.1:3000 gidin.</span><span class="sxs-lookup"><span data-stu-id="5b658-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="5b658-219">Aşağıdaki örnek bir web sayfası benzer toohello görünür.</span><span class="sxs-lookup"><span data-stu-id="5b658-219">A web page similar toohello following example appears.</span></span>
   
    ![Bir Web sayfası boş tasklist görüntüleme][node-table-finished]
4. <span data-ttu-id="5b658-221">toocreate yeni bir Yapılacaklar öğesi bir adı ve kategori girin ve tıklayın **Öğe Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5b658-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="5b658-222">bir görevi tamamlandı, onay olarak toomark **tam** tıklatıp **güncelleştirme görevleri**.</span><span class="sxs-lookup"><span data-stu-id="5b658-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Merhaba görevlerin hello listesinde yeni öğe görüntüsü][node-table-list-items]

<span data-ttu-id="5b658-224">Hello uygulama yerel olarak çalışıyor olsa bile hello Azure tablo hizmeti hello veri depolama.</span><span class="sxs-lookup"><span data-stu-id="5b658-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="5b658-225">Uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="5b658-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="5b658-226">Bu bölümdeki Hello adımları hello Azure komut satırı araçları toocreate yeni bir web uygulaması App Service'te ve ardından Git toodeploy uygulamanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b658-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="5b658-227">tooperform adımları bir Azure aboneliğine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b658-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5b658-228">Bu adımları hello kullanılarak da gerçekleştirilebilir [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b658-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="5b658-229">Bkz: [derleme ve Azure App Service'te Node.js web uygulamasına dağıtma].</span><span class="sxs-lookup"><span data-stu-id="5b658-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="5b658-230">Merhaba, oluşturduğunuz ilk web uygulamanız varsa, bu uygulama hello Azure Portal toodeploy kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b658-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="5b658-231">başlatıldı, tooget yükleme hello [Azure CLI] komutu hello komut satırından aşağıdaki hello girerek:</span><span class="sxs-lookup"><span data-stu-id="5b658-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="5b658-232">Yayımlama ayarlarını içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="5b658-232">Import publishing settings</span></span>
<span data-ttu-id="5b658-233">Bu adımda, aboneliğinizle ilgili bilgiler içeren bir dosya yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5b658-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="5b658-234">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="5b658-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="5b658-235">Bu komut, bir tarayıcı başlatılır ve toohello indirme sayfasına gider.</span><span class="sxs-lookup"><span data-stu-id="5b658-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="5b658-236">İstenirse, Azure aboneliğinizle ilişkili hello hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5b658-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="5b658-237">Merhaba dosya indirme otomatik olarak başlatır; yoksa, hello sayfa toomanually indirme hello dosyasının hello başında hello bağlantıyı tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b658-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="5b658-238">Merhaba dosya ve Not hello dosya yolu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b658-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="5b658-239">Komut tooimport hello ayarlarını aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="5b658-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="5b658-240">Merhaba önceki adımda ayarları dosyasını indirdiğiniz yayımlama hello Hello yolu ve dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5b658-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="5b658-241">Hello ayarları alındıktan sonra hello silme yayımlama ayarları dosyası.</span><span class="sxs-lookup"><span data-stu-id="5b658-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="5b658-242">Artık gerekli değildir ve Azure aboneliğinize ilişkin hassas bilgi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5b658-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="5b658-243">Bir App Service web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b658-243">Create an App Service web app</span></span>
1. <span data-ttu-id="5b658-244">Komut satırı Hello, dizinleri toohello değiştirme **tasklist** dizin.</span><span class="sxs-lookup"><span data-stu-id="5b658-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="5b658-245">Komut toocreate yeni bir web uygulaması aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b658-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="5b658-246">Merhaba web uygulaması adı ve konumu için istenir.</span><span class="sxs-lookup"><span data-stu-id="5b658-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="5b658-247">Benzersiz bir ad ve select hello Azure Storage hesabınızı aynı coğrafi konumda sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5b658-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="5b658-248">Merhaba `--git` parametresi bu web uygulaması için Azure üzerinde bir Git deposu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b658-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="5b658-249">Hiçbiri varsa ve ekler, ayrıca bir Git deposu hello geçerli dizinde başlatır bir [Git uzaktan] 'azure' olarak adlandırılan olduğu kullanılan toopublish hello uygulama tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b658-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="5b658-250">Son olarak, oluşturduğu bir **web.config** Azure toohost düğümü uygulamaları tarafından kullanılan ayarları içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="5b658-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="5b658-251">Merhaba atlarsanız `--git` parametre ancak hello dizini içeren bir Git deposu, hello komutu hala 'azure' hello uzaktan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b658-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="5b658-252">Bu komut tamamlandığında, çıkış benzer toohello aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5b658-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="5b658-253">Bu hello satır başlayarak Not **Web sitesi oluşturduğu adresindeki** hello hello web uygulaması URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="5b658-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="5b658-254">Merhaba ilk App Service web uygulaması için aboneliğiniz varsa belirtildiği toouse hello Azure Portal toocreate hello web uygulaması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5b658-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="5b658-255">Daha fazla bilgi için bkz: [derleme ve Azure App Service'te Node.js web uygulamasına dağıtma].</span><span class="sxs-lookup"><span data-stu-id="5b658-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="5b658-256">Ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="5b658-256">Set environment variables</span></span>
<span data-ttu-id="5b658-257">Bu adımda, Azure üzerinde ortam değişkenleri tooyour web uygulama yapılandırması ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5b658-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="5b658-258">Merhaba komut satırından hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="5b658-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="5b658-259">Değiştir  **<storage account name>**  hello depolama hello adla daha önce oluşturduğunuz hesap ve değiştirme  **<storage access key>**  hello depolama hesabınız için birincil erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="5b658-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="5b658-260">(Değerlerini aynı hello daha önce oluşturduğunuz hello config.json dosyası olarak kullanın.)</span><span class="sxs-lookup"><span data-stu-id="5b658-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="5b658-261">Alternatif olarak, hello ortam değişkenlerini ayarlayabilirsiniz [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="5b658-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="5b658-262">Hello web uygulamanızın dikey tıklatarak **Gözat** > **Web uygulamaları** >, web uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="5b658-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="5b658-263">Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları** > **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5b658-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="5b658-264">Toohello aşağı **uygulama ayarları** bölümünde ve hello anahtar/değer çiftleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b658-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Uygulama ayarları](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="5b658-266">**KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b658-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="5b658-267">Merhaba uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="5b658-267">Publish hello application</span></span>
<span data-ttu-id="5b658-268">toopublish hello uygulama hello kod dosyaları tooGit kaydetmek ve tooazure/ana gönderme.</span><span class="sxs-lookup"><span data-stu-id="5b658-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="5b658-269">Dağıtım kimlik bilgilerinizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5b658-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="5b658-270">Ekleme ve uygulama dosyalarınızı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5b658-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="5b658-271">Merhaba yürütme toohello App Service web uygulaması gönderin:</span><span class="sxs-lookup"><span data-stu-id="5b658-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="5b658-272">Kullanım **ana** hello hedef dala olarak.</span><span class="sxs-lookup"><span data-stu-id="5b658-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="5b658-273">Merhaba dağıtım Hello sonunda, örneğin aşağıdaki deyim benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="5b658-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="5b658-274">Merhaba gönderme işlemi tamamlandıktan sonra daha önce hello tarafından döndürülen toohello web uygulaması URL'si Gözat `azure create site` uygulamanız tooview komutu.</span><span class="sxs-lookup"><span data-stu-id="5b658-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b658-275">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b658-275">Next steps</span></span>
<span data-ttu-id="5b658-276">Hello tablo hizmeti toostore bilgileri kullanarak bu makaledeki Hello adımları açıklayan olsa da kullanabilirsiniz [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="5b658-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b658-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5b658-277">Additional resources</span></span>
<span data-ttu-id="5b658-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="5b658-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5b658-279">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5b658-279">What's changed</span></span>
* <span data-ttu-id="5b658-280">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5b658-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[derleme ve Azure App Service'te Node.js web uygulamasına dağıtma]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[düğümü]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git uzaktan]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[düğümü UUID]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[zaman uyumsuz]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png

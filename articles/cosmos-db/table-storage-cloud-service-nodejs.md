---
title: Tablo depolama (Node.js) aaaWeb uygulamayla | Microsoft Docs
description: "Azure depolama hizmetleri ve hello Azure modülü ekleyerek hello Web uygulaması hızlı öğretici ile derlemeler Öğreticisi."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="82fb3-103">Depolama kullanarak node.js Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="82fb3-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="82fb3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="82fb3-104">Overview</span></span>
<span data-ttu-id="82fb3-105">Bu öğreticide oluşturduğunuz uygulama hello [Express kullanarak Node.js Web uygulaması] Öğreticisi, Node.js toowork veri Yönetim Hizmetleri ile Merhaba Microsoft Azure istemci kitaplıkları kullanarak genişletilir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="82fb3-106">Uygulamanızı tooAzure dağıtabileceğiniz bir web tabanlı görev listesi uygulama oluşturarak genişletir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="82fb3-107">Merhaba görev listesi, kullanıcının görevleri almak, yeni görevler ekleyin ve Görevler tamamlandı olarak işaretle izin verir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="82fb3-108">Merhaba görev öğeleri Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="82fb3-109">Azure depolama hataya dayanıklı ve yüksek oranda kullanılabilir yapılandırılmamış veri depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="82fb3-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="82fb3-110">Azure depolama burada depolamak ve verilere birkaç veri yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="82fb3-111">Hello depolama Hizmetleri'ndeki hello Node.js için veya REST API'leri aracılığıyla hello Azure SDK'sını dahil API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fb3-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="82fb3-112">Daha fazla bilgi için bkz: [depolama ve veri erişim].</span><span class="sxs-lookup"><span data-stu-id="82fb3-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="82fb3-113">Bu öğretici hello tamamladığınızı varsaymaktadır [Node.js Web uygulaması] ve [Node.js Express ile][Express kullanarak Node.js Web uygulaması] öğreticileri.</span><span class="sxs-lookup"><span data-stu-id="82fb3-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="82fb3-114">Aşağıdaki bilgilerle hello içerir:</span><span class="sxs-lookup"><span data-stu-id="82fb3-114">It contains hello following information:</span></span>

* <span data-ttu-id="82fb3-115">Nasıl toowork ile Merhaba Jade şablon motoru</span><span class="sxs-lookup"><span data-stu-id="82fb3-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="82fb3-116">Nasıl toowork Azure veri Yönetim Hizmetleri ile</span><span class="sxs-lookup"><span data-stu-id="82fb3-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="82fb3-117">Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:</span><span class="sxs-lookup"><span data-stu-id="82fb3-117">hello following screenshot shows hello completed application:</span></span>

![Internet Explorer'da web sayfası Hello tamamlandı](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="82fb3-119">Web.Config dosyasında depolama kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="82fb3-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="82fb3-120">Depolama kimlik bilgileri tooaccess Azure Storage geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="82fb3-121">Bu, hello web.config uygulama ayarları yararlanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="82fb3-122">Merhaba web.config ayarları sonra hello Azure SDK'sı tarafından okuma ortam değişkenleri tooNode geçirilir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="82fb3-123">Merhaba uygulaması dağıtılan tooAzure olduğunda depolama kimlik bilgileri yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="82fb3-124">Merhaba öykünücüsünde çalıştırırken hello uygulama hello depolama öykünücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="82fb3-125">Adımları tooretrieve hello depolama hesabının kimlik bilgilerini aşağıdaki hello gerçekleştirmek ve bunları toohello web.config ayarları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82fb3-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="82fb3-126">Zaten açık değilse, hello hello Azure PowerShell Başlat **Başlat** genişleterek menü **tüm programları, Azure**, sağ tıklatın **Azure PowerShell**ve ardından seçin **Yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="82fb3-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="82fb3-127">Uygulamanızı içeren dizinleri toohello klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="82fb3-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="82fb3-128">Örneğin, C:\\düğümü\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="82fb3-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="82fb3-129">Hello Azure Powershell penceresinden cmdlet tooretrieve hello depolama hesabı bilgilerini aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="82fb3-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="82fb3-130">Merhaba Önceki cmdlet hello depolama hesapları ve barındırılan hizmetiniz ile ilişkili hesap anahtarları listesini alır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82fb3-131">Bir hizmeti dağıtırken hello Azure SDK'yı bir depolama hesabı oluşturduğundan, bir depolama hesabı zaten hello önceki kılavuzları uygulamanızda dağıtma var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="82fb3-132">Açık hello **ServiceDefinition.csdef** Merhaba uygulaması dağıtılan tooAzure olduğunda kullanılan hello ortam ayarlarını içeren dosyayı:</span><span class="sxs-lookup"><span data-stu-id="82fb3-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="82fb3-133">INSERT hello aşağıdaki engelle altında **ortam** {depolama hesabı} değiştirerek öğesi ve {depolama erişim tuşu} hello hesap adını ve dağıtım için kullanmak istediğiniz toouse hello depolama hesabının birincil anahtarı hello:</span><span class="sxs-lookup"><span data-stu-id="82fb3-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Merhaba web.cloud.config dosya içerikleri](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="82fb3-135">Merhaba dosyayı kaydedin ve Not Defteri'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="82fb3-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="82fb3-136">Ek modüller yükleme</span><span class="sxs-lookup"><span data-stu-id="82fb3-136">Install additional modules</span></span>
1. <span data-ttu-id="82fb3-137">Komut tooinstall hello [azure] aşağıdaki kullanım hello, [düğüm-UUID], [nconf] ve yerel olarak toosave bir giriş için bunları toohello yanı sıra [async] modülleri **package.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="82fb3-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="82fb3-138">Bu komutun çıktısı Hello benzer toohello aşağıdaki görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="82fb3-138">hello output of this command should appear similar toohello following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="82fb3-139">Merhaba tablo hizmetini bir düğüm uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="82fb3-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="82fb3-140">Bu bölümde, temel uygulama hello tarafından oluşturulan hello **express** komutu ekleyerek genişletilir bir **task.js** görevleriniz için hello modeli içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="82fb3-141">Merhaba varolan değiştirme **app.js** dosya ve yeni bir **tasklist.js** hello modelini kullanan dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="82fb3-142">Merhaba modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="82fb3-142">Create hello model</span></span>
1. <span data-ttu-id="82fb3-143">Merhaba, **WebRole1** dizin adlı yeni bir dizin oluşturun **modelleri**.</span><span class="sxs-lookup"><span data-stu-id="82fb3-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="82fb3-144">Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**.</span><span class="sxs-lookup"><span data-stu-id="82fb3-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="82fb3-145">Bu dosya, uygulamanız tarafından oluşturulan hello görevler için hello modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="82fb3-146">Merhaba hello başında **task.js** dosya, aşağıdaki kodu tooreference gerekli kitaplıkları hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82fb3-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="82fb3-147">Ardından, kod toodefine ekleyin ve hello görev nesneyi verin.</span><span class="sxs-lookup"><span data-stu-id="82fb3-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="82fb3-148">Merhaba görev nesnesi toohello tablo bağlamak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="82fb3-148">hello Task object is responsible for connecting toohello table.</span></span>

    ```nodejs
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
    ```

5. <span data-ttu-id="82fb3-149">Ardından, kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello hello tablosunda depolanan veriler ile etkileşim sağlayan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82fb3-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. <span data-ttu-id="82fb3-150">Kaydet ve Kapat hello **task.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="82fb3-151">Merhaba denetleyicisi oluşturun</span><span class="sxs-lookup"><span data-stu-id="82fb3-151">Create hello controller</span></span>
1. <span data-ttu-id="82fb3-152">Merhaba, **WebRole1/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="82fb3-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="82fb3-153">Kod çok aşağıdaki hello eklemek**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="82fb3-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="82fb3-154">Bu kod hello azure ve tarafından kullanılan async modüllerini yükler **tasklist.js** ve hello tanımlar **TaskList** hello örneği geçirilen işlevi **görev** biz nesnesi daha önce tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="82fb3-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="82fb3-155">Toohello eklemeye devam **tasklist.js** çok kullanılan hello yöntemleri ekleyerek dosya**showTasks**, **addTask**, ve **tasklist.js**:</span><span class="sxs-lookup"><span data-stu-id="82fb3-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. <span data-ttu-id="82fb3-156">Merhaba Kaydet **tasklist.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="82fb3-157">App.js'yi değiştirme</span><span class="sxs-lookup"><span data-stu-id="82fb3-157">Modify app.js</span></span>
1. <span data-ttu-id="82fb3-158">Merhaba, **WebRole1** dizin, açık hello **app.js** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="82fb3-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="82fb3-159">Başında hello hello dosya, tooload hello azure Modülü aşağıdaki hello ekleyin ve hello tablo adı ve bölüm anahtarı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="82fb3-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="82fb3-160">Merhaba app.js dosyasında gördüğünüz toowhere kaydırarak hello satırı:</span><span class="sxs-lookup"><span data-stu-id="82fb3-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="82fb3-161">Satırları koddan hello ile önceki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="82fb3-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="82fb3-162">Bu kod örneğini <strong>görev</strong> bağlantı tooyour depolama hesabına sahip.</span><span class="sxs-lookup"><span data-stu-id="82fb3-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="82fb3-163">Merhaba <strong>görev</strong> toohello geçirilen <strong>TaskList</strong>, kullanan, toocommunicate hello tablo hizmeti ile:</span><span class="sxs-lookup"><span data-stu-id="82fb3-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="82fb3-164">Merhaba Kaydet **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="82fb3-165">Merhaba dizini görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="82fb3-165">Modify hello index view</span></span>
1. <span data-ttu-id="82fb3-166">Değiştirme dizinleri toohello **görünümleri** dizin ve açık hello **index.jade** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="82fb3-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="82fb3-167">Merhaba Hello içeriğini değiştirin **index.jade** koddan hello dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="82fb3-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="82fb3-168">Bu kod, varolan görevleri görüntülemek için hello görünümü tanımlayan ve yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form tanımlar.</span><span class="sxs-lookup"><span data-stu-id="82fb3-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
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
          if tasks != []
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
    ```

3. <span data-ttu-id="82fb3-169">Kaydet ve Kapat **index.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="82fb3-170">Merhaba genel düzenini değiştirme</span><span class="sxs-lookup"><span data-stu-id="82fb3-170">Modify hello global layout</span></span>
<span data-ttu-id="82fb3-171">Merhaba **layout.jade** hello dosyasında **görünümleri** dizin kullanılan genel bir şablon olarak diğer **.jade** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="82fb3-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="82fb3-172">Bu adımda, hello değiştirme **layout.jade** toouse dosya [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir Web sitesi kolaylaştıran bir araç olan.</span><span class="sxs-lookup"><span data-stu-id="82fb3-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="82fb3-173">Karşıdan yükleyip hello dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="82fb3-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="82fb3-174">Kopya hello **bootstrap.min.css** hello dosyasından **önyükleme\\dağ\\css** klasörü toohello **ortak\\stil sayfaları** tasklist uygulamanızın dizin.</span><span class="sxs-lookup"><span data-stu-id="82fb3-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="82fb3-175">Merhaba gelen **görünümleri** klasörü, açık hello **layout.jade** Metin Düzenleyicisi'nde dosya ve hello içeriği hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82fb3-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="82fb3-176">doctype html html head başlığını başlık bağlantısı = (rel 'stil', href='/stylesheets/bootstrap.min.css =) bağlantı (rel 'stil', href='/stylesheets/style.css =) body.app nav.navbar.navbar varsayılan div.navbar üstbilgi a.navbar-brand(href='/') My  İçerik görevleri engelle</span><span class="sxs-lookup"><span data-stu-id="82fb3-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="82fb3-177">Merhaba Kaydet **layout.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="82fb3-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="82fb3-178">Çalışan hello uygulama hello öykünücüsü</span><span class="sxs-lookup"><span data-stu-id="82fb3-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="82fb3-179">Komut toostart hello hello öykünücüsü uygulamasında aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="82fb3-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="82fb3-180">Merhaba tarayıcı açar ve sayfa aşağıdaki hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="82fb3-180">hello browser opens and displays hello following page:</span></span>

![Disk belleğine alınan web My görev listesi görevleri ve alanları tooadd içeren bir tablo ile yeni bir görev başlıklı.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="82fb3-182">Merhaba form tooadd öğeleri kullanın veya var olan öğeleri tamamlanmış olarak işaretleyerek kaldırın.</span><span class="sxs-lookup"><span data-stu-id="82fb3-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="82fb3-183">Yayımlama hello uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="82fb3-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="82fb3-184">Merhaba Windows PowerShell penceresinde, aşağıdaki cmdlet'i tooredeploy hello barındırılan hizmet tooAzure çağırın.</span><span class="sxs-lookup"><span data-stu-id="82fb3-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="82fb3-185">Değiştir **myuniquename** bu uygulama için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="82fb3-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="82fb3-186">Değiştir **datacentername** hello adıyla bir Azure veri merkezi gibi **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="82fb3-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="82fb3-187">Merhaba dağıtım tamamlandıktan sonra bir yanıt benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="82fb3-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="82fb3-188">Merhaba belirterek **-başlatma** hello Önceki cmdlet, hello tarayıcı seçeneğinde açar ve uygulamanızı yayımlama tamamlandığında, Azure'da çalışan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="82fb3-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Merhaba My görev listesi sayfasını gösteren bir tarayıcı penceresi.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="82fb3-191">Durdurma ve uygulamanızı silme</span><span class="sxs-lookup"><span data-stu-id="82fb3-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="82fb3-192">Uygulamanızı dağıttıktan sonra onu önce maliyetleri önlemek veya yapılandırabilir ve hello içindeki diğer uygulamaları dağıtmak için ücretsiz deneme süre toodisable isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fb3-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="82fb3-193">Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="82fb3-194">Uygulamanızı dağıtıldığında örnekler çalışmadığında ve hello durdurulmuş durumda olsa bile sunucu saati harcanır.</span><span class="sxs-lookup"><span data-stu-id="82fb3-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="82fb3-195">Merhaba aşağıdaki adımlarda size yol gösterecektir toostop ve uygulamanızı silin.</span><span class="sxs-lookup"><span data-stu-id="82fb3-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="82fb3-196">Merhaba Windows PowerShell penceresinde hello hizmet dağıtımı cmdlet aşağıdaki hello ile Merhaba önceki bölümde oluşturduğunuz durdurun:</span><span class="sxs-lookup"><span data-stu-id="82fb3-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="82fb3-197">Merhaba hizmetin durdurulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="82fb3-198">Merhaba hizmet durdurulduğunda bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="82fb3-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="82fb3-199">toodelete hello hizmeti, cmdlet aşağıdaki çağrı hello:</span><span class="sxs-lookup"><span data-stu-id="82fb3-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="82fb3-200">İstendiğinde, girin **Y** toodelete hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="82fb3-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="82fb3-201">Merhaba hizmetin silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="82fb3-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="82fb3-202">Merhaba hizmet silindikten sonra hello hizmeti silinmiş olduğunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="82fb3-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[Express kullanarak Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[depolama ve veri erişim]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/



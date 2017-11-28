---
title: "Tablo depolama (Node.js) ile Web uygulaması | Microsoft Docs"
description: "Azure Storage Hizmetleri ve Azure modülü ekleyerek Express öğretici Web uygulamasıyla derlemeler Öğreticisi."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="aef63-103">Depolama kullanarak node.js Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="aef63-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="aef63-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aef63-104">Overview</span></span>
<span data-ttu-id="aef63-105">Bu öğreticide oluşturduğunuz uygulama uzatır [Express kullanarak Node.js Web uygulaması] veri Yönetim Hizmetleri ile çalışmak için Node.js için Microsoft Azure istemci kitaplıkları kullanarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="aef63-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="aef63-106">Azure için dağıtabileceğiniz bir web tabanlı görev listesi uygulaması oluşturmak için uygulamanızın uzatır.</span><span class="sxs-lookup"><span data-stu-id="aef63-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="aef63-107">Görev listesi, kullanıcının görevleri almak, yeni görevler ekleyin ve Görevler tamamlandı olarak işaretle izin verir.</span><span class="sxs-lookup"><span data-stu-id="aef63-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="aef63-108">Görev öğeleri Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="aef63-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="aef63-109">Azure depolama hataya dayanıklı ve yüksek oranda kullanılabilir yapılandırılmamış veri depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="aef63-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="aef63-110">Azure depolama burada depolayabileceğiniz ve verilere erişmek ve REST API'leri aracılığıyla veya Node.js için Azure SDK'ın dahil API'leri depolama hizmetlerinden yararlanabilirsiniz birkaç veri yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="aef63-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="aef63-111">Daha fazla bilgi için bkz: [depolama ve veri erişim].</span><span class="sxs-lookup"><span data-stu-id="aef63-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="aef63-112">Bu öğretici, tamamladığınızı varsaymaktadır [Node.js Web uygulaması] ve [Node.js Express ile][Express kullanarak Node.js Web uygulaması] öğreticileri.</span><span class="sxs-lookup"><span data-stu-id="aef63-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="aef63-113">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="aef63-113">You will learn:</span></span>

* <span data-ttu-id="aef63-114">Jade şablon altyapısıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="aef63-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="aef63-115">Azure veri Yönetim Hizmetleri ile birlikte çalışma</span><span class="sxs-lookup"><span data-stu-id="aef63-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="aef63-116">Tamamlanmış uygulamanın bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="aef63-116">A screenshot of the completed application is below:</span></span>

![Internet Explorer'da tamamlanan web sayfası](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="aef63-118">Web.Config dosyasında depolama kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="aef63-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="aef63-119">Azure Storage erişmek için depolama kimlik bilgilerinde geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aef63-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="aef63-120">Bunu yapmak için web.config uygulama ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="aef63-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="aef63-121">Bu ayarları ortam değişkenleri olarak düğümü için Azure SDK'sı tarafından ardından okuma geçirilir.</span><span class="sxs-lookup"><span data-stu-id="aef63-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="aef63-122">Azure için uygulama dağıtıldığında depolama kimlik bilgileri yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aef63-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="aef63-123">Öykünücüde çalıştırırken, uygulama depolama öykünücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="aef63-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="aef63-124">Depolama hesabı bilgilerini almak ve bunları web.config ayarları eklemek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="aef63-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="aef63-125">Zaten açık değilse, gelen Azure PowerShell'i başlatın **Başlat** genişleterek menü **tüm programları, Azure**, sağ **Azure PowerShell**ve ardından seçin **Yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="aef63-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="aef63-126">Dizinleri uygulamanızı içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="aef63-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="aef63-127">Örneğin, C:\\düğümü\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="aef63-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="aef63-128">Azure Powershell penceresinden depolama hesabı bilgilerini almak için aşağıdaki cmdlet'i girin:</span><span class="sxs-lookup"><span data-stu-id="aef63-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="aef63-129">Bu depolama hesapları ve anahtarları barındırılan hizmetiniz ile ilişkili hesap listesini alır.</span><span class="sxs-lookup"><span data-stu-id="aef63-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aef63-130">Bir hizmet dağıttığınızda Azure SDK'yı bir depolama hesabı oluşturduğundan, bir depolama hesabı zaten önceki kılavuzları uygulamanızda dağıtma var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aef63-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="aef63-131">Açık **ServiceDefinition.csdef** uygulamayı Azure'a dağıtıldığında kullanılan ortam ayarlarını içeren dosyayı:</span><span class="sxs-lookup"><span data-stu-id="aef63-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="aef63-132">Altında aşağıdaki blok Ekle **ortam** {depolama hesabı} değiştirerek öğesi ve {depolama erişim tuşu} hesap adını ve dağıtım için kullanmak istediğiniz depolama hesabı için birincil anahtar:</span><span class="sxs-lookup"><span data-stu-id="aef63-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Web.cloud.config dosya içerikleri](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="aef63-134">Dosyayı kaydedin ve Not Defteri'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="aef63-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="aef63-135">Ek modüller yükleme</span><span class="sxs-lookup"><span data-stu-id="aef63-135">Install additional modules</span></span>
1. <span data-ttu-id="aef63-136">[Azure], yüklemek için aşağıdaki komutu kullanın [düğüm-UUID], [nconf] ve bunların bir girdiyi kaydetmek için de yerel olarak [async] modülleri **package.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="aef63-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="aef63-137">Bu komutun çıktısı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="aef63-137">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="aef63-138">Tablo hizmetinde bir düğüm uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="aef63-138">Using the Table service in a node application</span></span>
<span data-ttu-id="aef63-139">Bu bölümde temel uygulama tarafından oluşturulan uzatır **express** komutu ekleyerek bir **task.js** görevleriniz için model içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="aef63-140">Varolan değiştirecek **app.js** ve yeni bir **tasklist.js** modelini kullanan dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="aef63-141">Modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="aef63-141">Create the model</span></span>
1. <span data-ttu-id="aef63-142">İçinde **WebRole1** dizin adlı yeni bir dizin oluşturun **modelleri**.</span><span class="sxs-lookup"><span data-stu-id="aef63-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="aef63-143">İçinde **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**.</span><span class="sxs-lookup"><span data-stu-id="aef63-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="aef63-144">Bu dosya, uygulamanız tarafından oluşturulan görevlerin modelini içerir.</span><span class="sxs-lookup"><span data-stu-id="aef63-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="aef63-145">Başında **task.js** dosya, gerekli kitaplıklar başvurmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aef63-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="aef63-146">Ardından, Task nesnesini tanımlamak ve dışarı aktarmak için kod ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aef63-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="aef63-147">Bu nesne, tabloya bağlanmak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="aef63-147">This object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="aef63-148">Ardından, ek yöntemleri Task nesnesinde tanımlamak için aşağıdaki kodu tabloda depolanan verileri ile etkileşim sağlayan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aef63-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
        // use entityGenerator to set types
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

6. <span data-ttu-id="aef63-149">Kaydet ve Kapat **task.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="aef63-150">Denetleyiciyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aef63-150">Create the controller</span></span>
1. <span data-ttu-id="aef63-151">İçinde **WebRole1/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="aef63-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="aef63-152">Aşağıdaki kodu **tasklist.js**'ye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aef63-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="aef63-153">Bu tarafından kullanılan azure ve async modüllerini yükler **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="aef63-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="aef63-154">Bu ayrıca tanımlar **TaskList** bir örneği olarak geçirilmiş işlevi **görev** daha önce tanımladığımız:</span><span class="sxs-lookup"><span data-stu-id="aef63-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="aef63-155">Eklemeye devam **tasklist.js** için kullanılan yöntemleri ekleyerek dosya **showTasks**, **addTask**, ve **tasklist.js**:</span><span class="sxs-lookup"><span data-stu-id="aef63-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="aef63-156">Kaydet **tasklist.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="aef63-157">App.js'yi değiştirme</span><span class="sxs-lookup"><span data-stu-id="aef63-157">Modify app.js</span></span>
1. <span data-ttu-id="aef63-158">İçinde **WebRole1** dizin, açık **app.js** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="aef63-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="aef63-159">Dosyasının başında azure modülünü yüklemek ve tablo adı ve bölüm anahtarı ayarlamak için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aef63-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="aef63-160">App.js dosyasında aşağıdaki satırı gördüğünüz aşağıya doğru kaydırma:</span><span class="sxs-lookup"><span data-stu-id="aef63-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="aef63-161">Yukarıdaki satırlar aşağıda kod ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aef63-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="aef63-162">Bu örneği başlatılamıyor <strong>görev</strong> depolama hesabınıza bir bağlantıyla.</span><span class="sxs-lookup"><span data-stu-id="aef63-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="aef63-163">Bu geçirilir <strong>TaskList</strong>, hangi kullanır, tablo hizmeti ile iletişim kurmak için:</span><span class="sxs-lookup"><span data-stu-id="aef63-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="aef63-164">Kaydet **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="aef63-165">Dizin görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="aef63-165">Modify the index view</span></span>
1. <span data-ttu-id="aef63-166">Değiştirme dizinleri **görünümleri** dizin ve açık **index.jade** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="aef63-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="aef63-167">Değiştir **index.jade** aşağıdaki kod ile dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="aef63-168">Bu yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form yanı sıra var olan görevleri görüntülemek için görünümü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="aef63-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="aef63-169">Kaydet ve Kapat **index.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="aef63-170">Genel düzenini değiştirme</span><span class="sxs-lookup"><span data-stu-id="aef63-170">Modify the global layout</span></span>
<span data-ttu-id="aef63-171">**views** dizinindeki **layout.jade** dosyası diğer **.jade** dosyaları için genel bir şablon olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aef63-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="aef63-172">Bu adımda, iyi görünümlü bir web sitesi tasarlamayı kolaylaştıran bir araç seti olan [Twitter Bootstrap](https://github.com/twbs/bootstrap)'i kullanmak için bu dosyayı değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aef63-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="aef63-173">Karşıdan yükleyip dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="aef63-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="aef63-174">Kopya **bootstrap.min.css** dosya **önyükleme\\dağ\\css** klasörüne **ortak\\stil sayfaları** tasklist uygulamanızın dizin.</span><span class="sxs-lookup"><span data-stu-id="aef63-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="aef63-175">Gelen **görünümleri** klasörü, açık **layout.jade** metin düzenleyicinizde ve içeriğini aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="aef63-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="aef63-176">doctype html html head başlığını başlık bağlantısı = (rel 'stil', href='/stylesheets/bootstrap.min.css =) bağlantı (rel 'stil', href='/stylesheets/style.css =) body.app nav.navbar.navbar varsayılan div.navbar üstbilgi a.navbar-brand(href='/') My  İçerik görevleri engelle</span><span class="sxs-lookup"><span data-stu-id="aef63-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="aef63-177">Kaydet **layout.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="aef63-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="aef63-178">Uygulamayı Öykünücüde çalıştırma</span><span class="sxs-lookup"><span data-stu-id="aef63-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="aef63-179">Öykünücüde uygulamayı başlatmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="aef63-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="aef63-180">Tarayıcı açılır ve aşağıdaki sayfasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="aef63-180">The browser will open and displays the following page:</span></span>

![Disk belleğine alınan web görevleri ve yeni bir görev eklemek için alanları içeren bir tablo ile My görev listesi başlıklı.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="aef63-182">Öğeler eklemek için form kullanın veya var olan öğeleri tamamlanmış olarak işaretleyerek kaldırın.</span><span class="sxs-lookup"><span data-stu-id="aef63-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="aef63-183">Uygulamayı Azure'a yayımlama</span><span class="sxs-lookup"><span data-stu-id="aef63-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="aef63-184">Windows PowerShell penceresinde Azure barındırılan hizmete yeniden dağıtmak için aşağıdaki cmdlet'i çağırın.</span><span class="sxs-lookup"><span data-stu-id="aef63-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="aef63-185">Değiştir **myuniquename** bu uygulama için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="aef63-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="aef63-186">Değiştir **datacentername** bir Azure veri merkezi adı gibi **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="aef63-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="aef63-187">Dağıtım tamamlandıktan sonra aşağıdakine benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="aef63-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="aef63-188">Önceki gibi belirtilen çünkü **-başlatma** seçeneği, tarayıcı açılır ve uygulamanızı yayımlama tamamlandığında, Azure'da çalışan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aef63-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![My görev listesi sayfasını gösteren bir tarayıcı penceresi.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="aef63-191">Durdurma ve uygulamanızı silme</span><span class="sxs-lookup"><span data-stu-id="aef63-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="aef63-192">Uygulamanızı dağıttıktan sonra maliyetleri önlemek veya yapılandırabilir ve ücretsiz deneme süre içinde diğer uygulamaları dağıtmak için devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aef63-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="aef63-193">Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.</span><span class="sxs-lookup"><span data-stu-id="aef63-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="aef63-194">Uygulamanız dağıtıldıktan sonra örnekler çalışmadığında ve durdurulmuş halde olduğunda bile sunucu saati harcanır.</span><span class="sxs-lookup"><span data-stu-id="aef63-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="aef63-195">Aşağıdaki adımlar durdurmak ve uygulamanızı silmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="aef63-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="aef63-196">Windows PowerShell penceresinde önceki bölümde oluşturulan hizmet dağıtımını aşağıdaki cmdlet ile durdurun:</span><span class="sxs-lookup"><span data-stu-id="aef63-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="aef63-197">Hizmetin durdurulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="aef63-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="aef63-198">Hizmet durdurulduğunda bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="aef63-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="aef63-199">Hizmeti silmek için aşağıdaki cmdlet'i çağırın:</span><span class="sxs-lookup"><span data-stu-id="aef63-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="aef63-200">İstendiğinde hizmeti silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="aef63-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="aef63-201">Hizmetin silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="aef63-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="aef63-202">Hizmet silindikten sonra bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="aef63-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="aef63-203">[Express kullanarak Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="aef63-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="aef63-204">[depolama ve veri erişim]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="aef63-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="aef63-205">[Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="aef63-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>



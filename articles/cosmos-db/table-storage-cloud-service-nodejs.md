---
title: "Tablo depolama (Node.js) ile Web uygulaması | Microsoft Docs"
description: "Azure Storage Hizmetleri ve Azure modülü ekleyerek Express öğretici Web uygulamasıyla derlemeler Öğreticisi."
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
ms.openlocfilehash: b802f880c1131abb7eb9ba00dd8f2e65017bc802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="1b8f6-103">Depolama kullanarak node.js Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1b8f6-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="1b8f6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1b8f6-104">Overview</span></span>
<span data-ttu-id="1b8f6-105">Bu öğreticide, uygulamayı oluşturduğunuz [Express kullanarak Node.js Web uygulaması] Öğreticisi, Node.js için Microsoft Azure istemci kitaplıkları veri Yönetim Hizmetleri ile birlikte çalışmak üzere kullanımı genişletilir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-105">In this tutorial, the application you created in the [Node.js Web Application using Express] tutorial is extended using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="1b8f6-106">Uygulamanız için Azure dağıtabileceğiniz bir web tabanlı görev listesi uygulama oluşturarak genişletir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-106">You extend your application by creating a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="1b8f6-107">Görev listesi, kullanıcının görevleri almak, yeni görevler ekleyin ve Görevler tamamlandı olarak işaretle izin verir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="1b8f6-108">Görev öğeleri Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="1b8f6-109">Azure depolama hataya dayanıklı ve yüksek oranda kullanılabilir yapılandırılmamış veri depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="1b8f6-110">Azure depolama burada depolamak ve verilere birkaç veri yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="1b8f6-111">Depolama Hizmetleri REST API'leri aracılığıyla veya Node.js için Azure SDK'ın dahil API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-111">You can use the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="1b8f6-112">Daha fazla bilgi için bkz: [depolama ve veri erişim].</span><span class="sxs-lookup"><span data-stu-id="1b8f6-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="1b8f6-113">Bu öğretici, tamamladığınızı varsaymaktadır [Node.js Web uygulaması] ve [Node.js Express ile][Express kullanarak Node.js Web uygulaması] öğreticileri.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-113">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="1b8f6-114">Aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-114">It contains the following information:</span></span>

* <span data-ttu-id="1b8f6-115">Jade şablon altyapısıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-115">How to work with the Jade template engine</span></span>
* <span data-ttu-id="1b8f6-116">Azure veri Yönetim Hizmetleri ile birlikte çalışma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-116">How to work with Azure Data Management services</span></span>

<span data-ttu-id="1b8f6-117">Aşağıdaki ekran görüntüsünde tamamlanan uygulama gösterilir:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-117">The following screenshot shows the completed application:</span></span>

![Internet Explorer'da tamamlanan web sayfası](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="1b8f6-119">Web.Config dosyasında depolama kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="1b8f6-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="1b8f6-120">Azure depolama alanına erişmek için depolama kimlik bilgilerini geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-120">You must pass in storage credentials to access Azure Storage.</span></span> <span data-ttu-id="1b8f6-121">Bu, web.config uygulama ayarları yararlanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-121">This is done by utilizing the web.config application settings.</span></span>
<span data-ttu-id="1b8f6-122">Web.config ayarları ortam değişkenleri olarak düğümü için Azure SDK'sı tarafından ardından okuma geçirilir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-122">The web.config settings are passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="1b8f6-123">Azure için uygulama dağıtıldığında depolama kimlik bilgileri yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-123">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="1b8f6-124">Öykünücüde çalıştırırken, uygulama depolama öykünücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-124">When running in the emulator, the application uses the storage emulator.</span></span>
>
>

<span data-ttu-id="1b8f6-125">Depolama hesabı bilgilerini almak ve bunları web.config ayarları eklemek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-125">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="1b8f6-126">Zaten açık değilse, gelen Azure PowerShell'i başlatın **Başlat** genişleterek menü **tüm programları, Azure**, sağ **Azure PowerShell**ve ardından seçin **Yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-126">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="1b8f6-127">Dizinleri uygulamanızı içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-127">Change directories to the folder containing your application.</span></span> <span data-ttu-id="1b8f6-128">Örneğin, C:\\düğümü\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="1b8f6-129">Azure Powershell penceresinden depolama hesabı bilgilerini almak için aşağıdaki cmdlet'i girin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-129">From the Azure Powershell window, enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="1b8f6-130">Yukarıdaki cmdlet depolama hesaplarını ve anahtarlarını barındırılan hizmetiniz ile ilişkili hesap listesini alır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-130">The preceding cmdlet retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1b8f6-131">Bir hizmet dağıttığınızda Azure SDK'yı bir depolama hesabı oluşturduğundan, bir depolama hesabı zaten önceki kılavuzları uygulamanızda dağıtma var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-131">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="1b8f6-132">Açık **ServiceDefinition.csdef** uygulamayı Azure'a dağıtıldığında kullanılan ortam ayarlarını içeren dosyayı:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-132">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="1b8f6-133">Altında aşağıdaki blok Ekle **ortam** {depolama hesabı} değiştirerek öğesi ve {depolama erişim tuşu} hesap adını ve dağıtım için kullanmak istediğiniz depolama hesabı için birincil anahtar:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-133">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Web.cloud.config dosya içerikleri](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="1b8f6-135">Dosyayı kaydedin ve Not Defteri'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-135">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="1b8f6-136">Ek modüller yükleme</span><span class="sxs-lookup"><span data-stu-id="1b8f6-136">Install additional modules</span></span>
1. <span data-ttu-id="1b8f6-137">[Azure], yüklemek için aşağıdaki komutu kullanın [düğüm-UUID], [nconf] ve bunların bir girdiyi kaydetmek için de yerel olarak [async] modülleri **package.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-137">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="1b8f6-138">Bu komutun çıktısı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-138">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="1b8f6-139">Tablo hizmetinde bir düğüm uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-139">Using the Table service in a node application</span></span>
<span data-ttu-id="1b8f6-140">Bu bölümde, temel uygulama tarafından oluşturulan **express** komutu ekleyerek genişletilir bir **task.js** görevleriniz için model içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-140">In this section, the basic application created by the **express** command is extended by adding a **task.js** file containing the model for your tasks.</span></span> <span data-ttu-id="1b8f6-141">Varolan değiştirme **app.js** dosya ve yeni bir **tasklist.js** modelini kullanan dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-141">Modify the existing **app.js** file and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="1b8f6-142">Modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-142">Create the model</span></span>
1. <span data-ttu-id="1b8f6-143">İçinde **WebRole1** dizin adlı yeni bir dizin oluşturun **modelleri**.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-143">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="1b8f6-144">İçinde **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-144">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="1b8f6-145">Bu dosya, uygulamanız tarafından oluşturulan görevlerin modelini içerir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-145">This file contains the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="1b8f6-146">Başında **task.js** dosya, gerekli kitaplıklar başvurmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-146">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="1b8f6-147">Ardından, tanımlayın ve görev nesnesi dışarı aktarmak için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-147">Next, add code to define and export the Task object.</span></span> <span data-ttu-id="1b8f6-148">Görev nesnesi tabloya bağlanmak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-148">The Task object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="1b8f6-149">Ardından, ek yöntemleri Task nesnesinde tanımlamak için aşağıdaki kodu tabloda depolanan verileri ile etkileşim sağlayan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-149">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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

6. <span data-ttu-id="1b8f6-150">Kaydet ve Kapat **task.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-150">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="1b8f6-151">Denetleyiciyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-151">Create the controller</span></span>
1. <span data-ttu-id="1b8f6-152">İçinde **WebRole1/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-152">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="1b8f6-153">Aşağıdaki kodu **tasklist.js**'ye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-153">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="1b8f6-154">Bu kod tarafından kullanılan azure ve async modüllerini yükler **tasklist.js** ve tanımlar **TaskList** bir örneği olarak geçirilmiş işlevi **görev** biz nesnesi daha önce tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-154">This code loads the azure and async modules, which are used by **tasklist.js** and defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="1b8f6-155">Eklemeye devam **tasklist.js** için kullanılan yöntemleri ekleyerek dosya **showTasks**, **addTask**, ve **tasklist.js**:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="1b8f6-156">Kaydet **tasklist.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="1b8f6-157">App.js'yi değiştirme</span><span class="sxs-lookup"><span data-stu-id="1b8f6-157">Modify app.js</span></span>
1. <span data-ttu-id="1b8f6-158">İçinde **WebRole1** dizin, açık **app.js** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="1b8f6-159">Dosyasının başında azure modülünü yüklemek ve tablo adı ve bölüm anahtarı ayarlamak için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="1b8f6-160">App.js dosyasında aşağıdaki satırı gördüğünüz aşağıya doğru kaydırma:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="1b8f6-161">Önceki satırları aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-161">Replace the preceding lines with the following code.</span></span> <span data-ttu-id="1b8f6-162">Bu kod örneğini <strong>görev</strong> depolama hesabınıza bir bağlantıyla.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-162">This code initializes an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="1b8f6-163"><strong>Görev</strong> geçirilir <strong>TaskList</strong>, kullanan, tablo hizmeti ile iletişim kurmak için:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-163">The <strong>Task</strong> is passed to the <strong>TaskList</strong>, which uses it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="1b8f6-164">Kaydet **app.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="1b8f6-165">Dizin görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="1b8f6-165">Modify the index view</span></span>
1. <span data-ttu-id="1b8f6-166">Değiştirme dizinleri **görünümleri** dizin ve açık **index.jade** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="1b8f6-167">Değiştir **index.jade** aşağıdaki kod ile dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-167">Replace the contents of the **index.jade** file with the following code.</span></span> <span data-ttu-id="1b8f6-168">Bu kod, var olan görevleri görüntülemek için görünümü tanımlayan ve yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-168">This code defines the view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="1b8f6-169">Kaydet ve Kapat **index.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="1b8f6-170">Genel düzenini değiştirme</span><span class="sxs-lookup"><span data-stu-id="1b8f6-170">Modify the global layout</span></span>
<span data-ttu-id="1b8f6-171">**views** dizinindeki **layout.jade** dosyası diğer **.jade** dosyaları için genel bir şablon olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="1b8f6-172">Bu adımda, değişiklik **layout.jade** kullanmak üzere bir dosya [Twitter Bootstrap](https://github.com/twbs/bootstrap), iyi görünümlü bir Web sitesi tasarlamayı kolaylaştıran bir araç olan.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-172">In this step, modify the **layout.jade** file to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="1b8f6-173">Karşıdan yükleyip dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="1b8f6-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="1b8f6-174">Kopya **bootstrap.min.css** dosya **önyükleme\\dağ\\css** klasörüne **ortak\\stil sayfaları** tasklist uygulamanızın dizin.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="1b8f6-175">Gelen **görünümleri** klasörü, açık **layout.jade** Metin Düzenleyicisi'nde dosya ve içeriğini aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-175">From the **views** folder, open the **layout.jade** file in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="1b8f6-176">doctype html html head başlığını başlık bağlantısı = (rel 'stil', href='/stylesheets/bootstrap.min.css =) bağlantı (rel 'stil', href='/stylesheets/style.css =) body.app nav.navbar.navbar varsayılan div.navbar üstbilgi a.navbar-brand(href='/') My  İçerik görevleri engelle</span><span class="sxs-lookup"><span data-stu-id="1b8f6-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="1b8f6-177">Kaydet **layout.jade** dosya.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="1b8f6-178">Uygulamayı Öykünücüde çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1b8f6-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="1b8f6-179">Öykünücüde uygulamayı başlatmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="1b8f6-180">Tarayıcı açılır ve aşağıdaki sayfasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-180">The browser opens and displays the following page:</span></span>

![Disk belleğine alınan web görevleri ve yeni bir görev eklemek için alanları içeren bir tablo ile My görev listesi başlıklı.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="1b8f6-182">Öğeler eklemek için form kullanın veya var olan öğeleri tamamlanmış olarak işaretleyerek kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="1b8f6-183">Uygulamayı Azure'a yayımlama</span><span class="sxs-lookup"><span data-stu-id="1b8f6-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="1b8f6-184">Windows PowerShell penceresinde Azure barındırılan hizmete yeniden dağıtmak için aşağıdaki cmdlet'i çağırın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="1b8f6-185">Değiştir **myuniquename** bu uygulama için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="1b8f6-186">Değiştir **datacentername** bir Azure veri merkezi adı gibi **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="1b8f6-187">Dağıtım tamamlandıktan sonra aşağıdakine benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-187">After the deployment is complete, you should see a response similar to the following:</span></span>

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

<span data-ttu-id="1b8f6-188">Belirterek **-başlatma** Önceki cmdlet, tarayıcı seçeneğinde açar ve uygulamanızı yayımlama tamamlandığında, Azure'da çalışan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-188">By specifying the **-launch** option in the previous cmdlet, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![My görev listesi sayfasını gösteren bir tarayıcı penceresi.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="1b8f6-191">Durdurma ve uygulamanızı silme</span><span class="sxs-lookup"><span data-stu-id="1b8f6-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="1b8f6-192">Uygulamanızı dağıttıktan sonra maliyetleri önlemek veya yapılandırabilir ve ücretsiz deneme süre içinde diğer uygulamaları dağıtmak için devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="1b8f6-193">Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="1b8f6-194">Uygulamanız dağıtıldıktan sonra örnekler çalışmadığında ve durdurulmuş halde olduğunda bile sunucu saati harcanır.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="1b8f6-195">Aşağıdaki adımlar durdurmak ve uygulamanızı silmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="1b8f6-196">Windows PowerShell penceresinde önceki bölümde oluşturulan hizmet dağıtımını aşağıdaki cmdlet ile durdurun:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="1b8f6-197">Hizmetin durdurulması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="1b8f6-198">Hizmet durdurulduğunda bunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="1b8f6-199">Hizmeti silmek için aşağıdaki cmdlet'i çağırın:</span><span class="sxs-lookup"><span data-stu-id="1b8f6-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="1b8f6-200">İstendiğinde hizmeti silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="1b8f6-201">Hizmetin silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="1b8f6-202">Hizmet silindikten sonra hizmet silinmiş olduğunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1b8f6-202">After the service is deleted, you will receive a message indicating that the service was deleted.</span></span>

[Express kullanarak Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[depolama ve veri erişim]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/



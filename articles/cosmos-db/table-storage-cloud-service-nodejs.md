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
# <a name="nodejs-web-application-using-storage"></a>Depolama kullanarak node.js Web uygulaması
## <a name="overview"></a>Genel Bakış
Bu öğreticide oluşturduğunuz uygulama hello [Express kullanarak Node.js Web uygulaması] Öğreticisi, Node.js toowork veri Yönetim Hizmetleri ile Merhaba Microsoft Azure istemci kitaplıkları kullanarak genişletilir. Uygulamanızı tooAzure dağıtabileceğiniz bir web tabanlı görev listesi uygulama oluşturarak genişletir. Merhaba görev listesi, kullanıcının görevleri almak, yeni görevler ekleyin ve Görevler tamamlandı olarak işaretle izin verir.

Merhaba görev öğeleri Azure depolama alanında depolanır. Azure depolama hataya dayanıklı ve yüksek oranda kullanılabilir yapılandırılmamış veri depolama sağlar. Azure depolama burada depolamak ve verilere birkaç veri yapılarını içerir. Hello depolama Hizmetleri'ndeki hello Node.js için veya REST API'leri aracılığıyla hello Azure SDK'sını dahil API'leri kullanabilirsiniz. Daha fazla bilgi için bkz: [depolama ve veri erişim].

Bu öğretici hello tamamladığınızı varsaymaktadır [Node.js Web uygulaması] ve [Node.js Express ile][Express kullanarak Node.js Web uygulaması] öğreticileri.

Aşağıdaki bilgilerle hello içerir:

* Nasıl toowork ile Merhaba Jade şablon motoru
* Nasıl toowork Azure veri Yönetim Hizmetleri ile

Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:

![Internet Explorer'da web sayfası Hello tamamlandı](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Web.Config dosyasında depolama kimlik bilgilerini ayarlama
Depolama kimlik bilgileri tooaccess Azure Storage geçmesi gerekir. Bu, hello web.config uygulama ayarları yararlanarak gerçekleştirilir.
Merhaba web.config ayarları sonra hello Azure SDK'sı tarafından okuma ortam değişkenleri tooNode geçirilir.

> [!NOTE]
> Merhaba uygulaması dağıtılan tooAzure olduğunda depolama kimlik bilgileri yalnızca kullanılır. Merhaba öykünücüsünde çalıştırırken hello uygulama hello depolama öykünücüsü kullanır.
>
>

Adımları tooretrieve hello depolama hesabının kimlik bilgilerini aşağıdaki hello gerçekleştirmek ve bunları toohello web.config ayarları ekleyin:

1. Zaten açık değilse, hello hello Azure PowerShell Başlat **Başlat** genişleterek menü **tüm programları, Azure**, sağ tıklatın **Azure PowerShell**ve ardından seçin **Yönetici olarak çalıştır**.
2. Uygulamanızı içeren dizinleri toohello klasörü değiştirin. Örneğin, C:\\düğümü\\tasklist\\WebRole1.
3. Hello Azure Powershell penceresinden cmdlet tooretrieve hello depolama hesabı bilgilerini aşağıdaki hello girin:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Merhaba Önceki cmdlet hello depolama hesapları ve barındırılan hizmetiniz ile ilişkili hesap anahtarları listesini alır.

   > [!NOTE]
   > Bir hizmeti dağıtırken hello Azure SDK'yı bir depolama hesabı oluşturduğundan, bir depolama hesabı zaten hello önceki kılavuzları uygulamanızda dağıtma var olmalıdır.
   >
   >
4. Açık hello **ServiceDefinition.csdef** Merhaba uygulaması dağıtılan tooAzure olduğunda kullanılan hello ortam ayarlarını içeren dosyayı:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. INSERT hello aşağıdaki engelle altında **ortam** {depolama hesabı} değiştirerek öğesi ve {depolama erişim tuşu} hello hesap adını ve dağıtım için kullanmak istediğiniz toouse hello depolama hesabının birincil anahtarı hello:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Merhaba web.cloud.config dosya içerikleri](./media/table-storage-cloud-service-nodejs/node37.png)

6. Merhaba dosyayı kaydedin ve Not Defteri'ni kapatın.

### <a name="install-additional-modules"></a>Ek modüller yükleme
1. Komut tooinstall hello [azure] aşağıdaki kullanım hello, [düğüm-UUID], [nconf] ve yerel olarak toosave bir giriş için bunları toohello yanı sıra [async] modülleri **package.json** dosyası:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  Bu komutun çıktısı Hello benzer toohello aşağıdaki görünmelidir:

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

## <a name="using-hello-table-service-in-a-node-application"></a>Merhaba tablo hizmetini bir düğüm uygulamasında kullanma
Bu bölümde, temel uygulama hello tarafından oluşturulan hello **express** komutu ekleyerek genişletilir bir **task.js** görevleriniz için hello modeli içeren dosya. Merhaba varolan değiştirme **app.js** dosya ve yeni bir **tasklist.js** hello modelini kullanan dosya.

### <a name="create-hello-model"></a>Merhaba modeli oluşturma
1. Merhaba, **WebRole1** dizin adlı yeni bir dizin oluşturun **modelleri**.
2. Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**. Bu dosya, uygulamanız tarafından oluşturulan hello görevler için hello modeli içerir.
3. Merhaba hello başında **task.js** dosya, aşağıdaki kodu tooreference gerekli kitaplıkları hello ekleyin:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Ardından, kod toodefine ekleyin ve hello görev nesneyi verin. Merhaba görev nesnesi toohello tablo bağlamak için sorumludur.

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

5. Ardından, kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello hello tablosunda depolanan veriler ile etkileşim sağlayan ekleyin:

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

6. Kaydet ve Kapat hello **task.js** dosya.

### <a name="create-hello-controller"></a>Merhaba denetleyicisi oluşturun
1. Merhaba, **WebRole1/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.
2. Kod çok aşağıdaki hello eklemek**tasklist.js**. Bu kod hello azure ve tarafından kullanılan async modüllerini yükler **tasklist.js** ve hello tanımlar **TaskList** hello örneği geçirilen işlevi **görev** biz nesnesi daha önce tanımlanan:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Toohello eklemeye devam **tasklist.js** çok kullanılan hello yöntemleri ekleyerek dosya**showTasks**, **addTask**, ve **tasklist.js**:

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

4. Merhaba Kaydet **tasklist.js** dosya.

### <a name="modify-appjs"></a>App.js'yi değiştirme
1. Merhaba, **WebRole1** dizin, açık hello **app.js** dosyasını bir metin düzenleyicisinde.
2. Başında hello hello dosya, tooload hello azure Modülü aşağıdaki hello ekleyin ve hello tablo adı ve bölüm anahtarı ayarlayın:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. Merhaba app.js dosyasında gördüğünüz toowhere kaydırarak hello satırı:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Satırları koddan hello ile önceki hello değiştirin. Bu kod örneğini <strong>görev</strong> bağlantı tooyour depolama hesabına sahip. Merhaba <strong>görev</strong> toohello geçirilen <strong>TaskList</strong>, kullanan, toocommunicate hello tablo hizmeti ile:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Merhaba Kaydet **app.js** dosya.

### <a name="modify-hello-index-view"></a>Merhaba dizini görünümünü değiştirme
1. Değiştirme dizinleri toohello **görünümleri** dizin ve açık hello **index.jade** dosyasını bir metin düzenleyicisinde.
2. Merhaba Hello içeriğini değiştirin **index.jade** koddan hello dosyasıyla. Bu kod, varolan görevleri görüntülemek için hello görünümü tanımlayan ve yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form tanımlar.

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

3. Kaydet ve Kapat **index.jade** dosya.

### <a name="modify-hello-global-layout"></a>Merhaba genel düzenini değiştirme
Merhaba **layout.jade** hello dosyasında **görünümleri** dizin kullanılan genel bir şablon olarak diğer **.jade** dosyaları. Bu adımda, hello değiştirme **layout.jade** toouse dosya [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir Web sitesi kolaylaştıran bir araç olan.

1. Karşıdan yükleyip hello dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/). Kopya hello **bootstrap.min.css** hello dosyasından **önyükleme\\dağ\\css** klasörü toohello **ortak\\stil sayfaları** tasklist uygulamanızın dizin.
2. Merhaba gelen **görünümleri** klasörü, açık hello **layout.jade** Metin Düzenleyicisi'nde dosya ve hello içeriği hello şununla değiştirin:

    doctype html html head başlığını başlık bağlantısı = (rel 'stil', href='/stylesheets/bootstrap.min.css =) bağlantı (rel 'stil', href='/stylesheets/style.css =) body.app nav.navbar.navbar varsayılan div.navbar üstbilgi a.navbar-brand(href='/') My  İçerik görevleri engelle

3. Merhaba Kaydet **layout.jade** dosya.

### <a name="running-hello-application-in-hello-emulator"></a>Çalışan hello uygulama hello öykünücüsü
Komut toostart hello hello öykünücüsü uygulamasında aşağıdaki hello kullanın.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

Merhaba tarayıcı açar ve sayfa aşağıdaki hello görüntüler:

![Disk belleğine alınan web My görev listesi görevleri ve alanları tooadd içeren bir tablo ile yeni bir görev başlıklı.](./media/table-storage-cloud-service-nodejs/node44.png)

Merhaba form tooadd öğeleri kullanın veya var olan öğeleri tamamlanmış olarak işaretleyerek kaldırın.

## <a name="publishing-hello-application-tooazure"></a>Yayımlama hello uygulama tooAzure
Merhaba Windows PowerShell penceresinde, aşağıdaki cmdlet'i tooredeploy hello barındırılan hizmet tooAzure çağırın.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Değiştir **myuniquename** bu uygulama için benzersiz bir ada sahip. Değiştir **datacentername** hello adıyla bir Azure veri merkezi gibi **Batı ABD**.

Merhaba dağıtım tamamlandıktan sonra bir yanıt benzer toohello aşağıdaki görmeniz gerekir:

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

Merhaba belirterek **-başlatma** hello Önceki cmdlet, hello tarayıcı seçeneğinde açar ve uygulamanızı yayımlama tamamlandığında, Azure'da çalışan görüntüler.

![Merhaba My görev listesi sayfasını gösteren bir tarayıcı penceresi. Merhaba URL hello sayfası artık Azure üzerinde barındırılan gösterir.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Durdurma ve uygulamanızı silme
Uygulamanızı dağıttıktan sonra onu önce maliyetleri önlemek veya yapılandırabilir ve hello içindeki diğer uygulamaları dağıtmak için ücretsiz deneme süre toodisable isteyebilirsiniz.

Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır.
Uygulamanızı dağıtıldığında örnekler çalışmadığında ve hello durdurulmuş durumda olsa bile sunucu saati harcanır.

Merhaba aşağıdaki adımlarda size yol gösterecektir toostop ve uygulamanızı silin.

1. Merhaba Windows PowerShell penceresinde hello hizmet dağıtımı cmdlet aşağıdaki hello ile Merhaba önceki bölümde oluşturduğunuz durdurun:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Merhaba hizmetin durdurulması birkaç dakika sürebilir. Merhaba hizmet durdurulduğunda bunu belirten bir ileti alırsınız.

2. toodelete hello hizmeti, cmdlet aşağıdaki çağrı hello:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   İstendiğinde, girin **Y** toodelete hello hizmet.

   Merhaba hizmetin silinmesi birkaç dakika sürebilir. Merhaba hizmet silindikten sonra hello hizmeti silinmiş olduğunu belirten bir ileti alırsınız.

[Express kullanarak Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[depolama ve veri erişim]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web uygulaması]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/



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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Hello Azure tablo hizmeti kullanarak Node.js web uygulaması
## <a name="overview"></a>Genel Bakış
Bu öğreticide, Azure veri yönetimi toostore ve erişim verilerini nasıl toouse tablo hizmeti sağladığı gösterilmiştir bir [düğümü] uygulama barındırılan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları. Bu öğretici, düğüm kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar ve [Git].

Şunları öğreneceksiniz:

* Nasıl toouse npm (düğüm paketi Yöneticisi) tooinstall hello düğümü modülleri
* Nasıl toowork ile hello Azure tablo hizmeti
* Nasıl toouse hello Azure CLI toocreate bir web uygulaması.

Bu öğreticiyi izleyerek, basit bir web tabanlı oluşturacaksınız oluşturulmasını, alınmasını ve görevleri tamamlama sağlayan "Yapılacaklar listesi" uygulaması. Merhaba görevleri hello tablo hizmetinde depolanır.

Tamamlanan Merhaba uygulaması şöyledir:

![Boş bir tasklist görüntüleyen bir web sayfası][node-table-finished]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki yüklü olduğundan emin olun:

* [düğümü] sürüm 0.10.24 veya üzeri
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
Bir Azure Storage hesabı oluşturun. Merhaba uygulama bu hesabı toostore hello Yapılacaklar öğelerini kullanır.

1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).
2. Merhaba tıklatın **yeni** hello alt simgesine sol hello portallarına, ardından **veri + depolama** > **depolama**. Merhaba depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.
   
      ![Yeni düğmesi](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Merhaba depolama hesabı oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve hello depolama hesabının dikey penceresi açık toohello yeni kaynak ait tooshow grubunu oluşturulur.
3. Merhaba depolama hesabı dikey penceresinde tıklayın **ayarları** > **anahtarları**. Merhaba birincil erişim anahtarı toohello panoya kopyalayın.
   
    ![Erişim anahtarı][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Modüllerini yükleyin ve yapı iskelesi oluştur
Bu bölümde yeni bir düğüm uygulama oluşturma ve npm tooadd modülü paketleri kullanma. Bu uygulama için hello kullanacağı [Express] ve [Azure] modüller. Hello Express modülü düğümü için bir Model View Controller çerçeve sağlar, başlangıç sırasında Azure modülleri bağlantı toohello tablo hizmeti sağlar.

### <a name="install-express-and-generate-scaffolding"></a>Hızlı yükleme ve yapı iskelesi oluştur
1. Merhaba komut satırından adlı yeni bir dizin oluşturma **tasklist** ve anahtar toothat dizin.  
2. Komut tooinstall hello Express Modülü aşağıdaki hello girin.
   
        npm install express-generator@4.2.0 -g
   
    Merhaba işletim sistemine bağlı olarak tooput 'sudo' hello komutundan önce gerekebilir:
   
        sudo npm install express-generator@4.2.0 -g
   
    Aşağıdaki örneğine benzer toohello Hello çıktı görünür:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Merhaba '-g' parametresi hello modülü genel olarak yükler. Bu şekilde kullanırız **express** ek yol bilgileri tootype kalmadan toogenerate web uygulama iskele.
   > 
   > 
3. Merhaba uygulaması için toocreate hello askılamayı girin hello **express** komutu:
   
        express
   
    Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:
   
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
   
    Şimdi birkaç yeni dizin ve dosyaların hello sahip **tasklist** dizin.

### <a name="install-additional-modules"></a>Ek modüller yükleme
Merhaba birini dosyaları **express** oluşturur olan **package.json**. Bu dosya modülü bağımlılıkları listesini içerir. Daha sonra hello uygulama tooApp Service Web Apps dağıttığınızda, bu dosyayı Azure üzerinde yüklü toobe modüllerine gereksinim belirler.

Komut satırı Hello, komut tooinstall hello modülleri hello açıklanan aşağıdaki hello girin **package.json** dosya. Toouse 'sudo' gerekebilir.

    npm install

Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Ardından, komut tooinstall hello aşağıdaki hello girin [azure], [düğümü UUID], [nconf] ve [zaman uyumsuz] modülleri:

    npm install azure-storage node-uuid async nconf --save

Merhaba **--Kaydet** bayrağı ekler bu modülleri toohello girişlerinde **package.json** dosya.

Bu komutun çıktısı Hello aşağıdaki örneğine benzer toohello görünür:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Şimdi hazır toobuild Merhaba uygulaması demektir.

### <a name="create-a-model"></a>Bir model oluşturma
A *modeli* uygulamanızdaki hello verileri temsil eden bir nesnedir. Merhaba uygulaması için hello yalnızca hello Yapılacaklar listesi bir öğeyi temsil eden bir görev nesnesi modelidir. Görev alanları izleyen hello olacaktır:

* PartitionKey
* RowKey
* adı (dize)
* Kategori (dize)
* Tamamlanan (Boole)

**PartitionKey** ve **RowKey** hello tablo hizmeti tarafından tablo anahtarlar kullanılır. Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. Merhaba, **tasklist** dizin adlı yeni bir dizin oluşturun **modelleri**.
2. Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **task.js**. Bu dosya, uygulamanız tarafından oluşturulan hello görevler için hello modeli içerir.
3. Merhaba hello başında **task.js** dosya, aşağıdaki kodu tooreference gerekli kitaplıkları hello ekleyin:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Merhaba aşağıdaki toodefine kod ve hello görev nesne dışarı aktarma ekleyin. Bu nesne, toohello tablo bağlamak için sorumludur.
   
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
5. Kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello hello tablosunda depolanan veriler ile etkileşim sağlayan ekleyin:
   
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
6. Kaydet ve Kapat hello **task.js** dosya.

### <a name="create-a-controller"></a>Bir denetleyici oluşturma
A *denetleyicisi* HTTP isteklerini işler ve hello HTML yanıt işler.

1. Merhaba, **tasklist/yollar** dizin adlı yeni bir dosya oluşturun **tasklist.js** ve bir metin düzenleyicisinde açın.
2. Kod çok aşağıdaki hello eklemek**tasklist.js**. Bu tarafından kullanılan hello azure ve async modüllerini yükler **tasklist.js**. Bu ayrıca hello tanımlar **TaskList** hello örneği geçirilen işlevi **görev** daha önce tanımladığımız:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Tanımlayan bir **TaskList** nesnesi.
   
        function TaskList(task) {
          this.task = task;
        }
4. Yöntemleri çok aşağıdaki hello eklemek**TaskList**:
   
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

### <a name="modify-appjs"></a>App.js'yi değiştirme
1. Merhaba gelen **tasklist** dizin, açık hello **app.js** dosya. Merhaba çalıştırarak bu dosya daha önce oluşturulmuş **express** komutu.
2. Merhaba dosya Hello başında tooload hello azure modülü, kümesi hello tablo adı, bölüm anahtarı ve kümesi hello depolama Bu örnek tarafından kullanılan kimlik bilgileri aşağıdaki hello ekleyin:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > ortam değişkenleri veya hello nconf hello yapılandırma değerlerini yükler **config.json** daha sonra oluşturacağız dosya.
   > 
   > 
3. Merhaba app.js dosyasında gördüğünüz toowhere kaydırarak hello satırı:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Satırları yukarıda Hello aşağıda gösterilen hello kod ile değiştirin. Bu örneği başlatılamıyor <strong>görev</strong> bağlantı tooyour depolama hesabına sahip. Bu toohello geçirilen <strong>TaskList</strong>, hangi kullanır, toocommunicate hello tablo hizmeti ile:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Merhaba Kaydet **app.js** dosya.

### <a name="modify-hello-index-view"></a>Merhaba dizini görünümünü değiştirme
1. Açık hello **tasklist/views/index.jade** dosyasını bir metin düzenleyicisinde.
2. Merhaba dosyanın tüm içeriğini Hello koddan hello ile değiştirin. Bu, var olan görevleri görüntüler ve yeni görev eklemeye ve varolanları tamamlandı olarak işaretlemek için bir form içeren bir görünüm tanımlar.
   
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
3. Kaydet ve Kapat **index.jade** dosya.

### <a name="modify-hello-global-layout"></a>Merhaba genel düzenini değiştirme
Merhaba **layout.jade** hello dosyasında **görünümleri** dizindir diğer genel bir şablon **.jade** dosyaları. Bu adımda, toouse değiştirecek [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir web uygulaması kolaylaştıran bir araç olan.

Karşıdan yükleyip hello dosyaları ayıklayın [Twitter Bootstrap](http://getbootstrap.com/). Kopya hello **bootstrap.min.css** hello önyükleme dosyasından **css** hello klasörüne **ortak/stil sayfaları** uygulamanızın dizin.

Merhaba gelen **görünümleri** klasörü, açık **layout.jade** ve hello tüm içeriği hello şununla değiştirin:

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

### <a name="create-a-config-file"></a>Bir yapılandırma dosyası oluşturma
yerel olarak toorun hello uygulama için biz bir yapılandırma dosyasına Azure depolama kimlik put. Adlı bir dosya oluşturun **config.json* * JSON aşağıdaki hello ile:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Değiştir **depolama hesabı adı** hello depolama hello adla daha önce oluşturduğunuz hesap ve değiştirme **depolama erişim tuşu** hello depolama hesabınız için birincil erişim anahtarı ile. Örneğin:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Bu dosyayı kaydetmek *daha yüksek bir dizin düzeyinde* hello daha **tasklist** dizin şuna benzer:

    parent/
      |-- config.json
      |-- tasklist/

Bunu yapmak için hello hello config dosya kaynak denetimine denetimi tooavoid Burada, genel hale gelebilir nedenidir. Biz hello uygulama tooAzure dağıttığınızda, bir yapılandırma dosyası yerine ortam değişkenleri kullanacağız.

## <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma
yerel makinenizde tootest Merhaba uygulaması hello aşağıdaki adımları gerçekleştirin:

1. Komut satırı Hello, dizinleri toohello değiştirme **tasklist** dizin.
2. Komut toolaunch hello uygulama yerel olarak aşağıdaki hello kullan:
   
        npm start
3. Bir web tarayıcısı açın ve toohttp://127.0.0.1:3000 gidin.
   
    Aşağıdaki örnek bir web sayfası benzer toohello görünür.
   
    ![Bir Web sayfası boş tasklist görüntüleme][node-table-finished]
4. toocreate yeni bir Yapılacaklar öğesi bir adı ve kategori girin ve tıklayın **Öğe Ekle**. 
5. bir görevi tamamlandı, onay olarak toomark **tam** tıklatıp **güncelleştirme görevleri**.
   
    ![Merhaba görevlerin hello listesinde yeni öğe görüntüsü][node-table-list-items]

Hello uygulama yerel olarak çalışıyor olsa bile hello Azure tablo hizmeti hello veri depolama.

## <a name="deploy-your-application-tooazure"></a>Uygulama tooAzure dağıtma
Bu bölümdeki Hello adımları hello Azure komut satırı araçları toocreate yeni bir web uygulaması App Service'te ve ardından Git toodeploy uygulamanızı kullanın. tooperform adımları bir Azure aboneliğine sahip olmanız gerekir.

> [!NOTE]
> Bu adımları hello kullanılarak da gerçekleştirilebilir [Azure Portal](https://portal.azure.com/). Bkz: [derleme ve Azure App Service'te Node.js web uygulamasına dağıtma].
> 
> Merhaba, oluşturduğunuz ilk web uygulamanız varsa, bu uygulama hello Azure Portal toodeploy kullanmanız gerekir.
> 
> 

başlatıldı, tooget yükleme hello [Azure CLI] komutu hello komut satırından aşağıdaki hello girerek:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Yayımlama ayarlarını içeri aktarma
Bu adımda, aboneliğinizle ilgili bilgiler içeren bir dosya yüklenir.

1. Merhaba aşağıdaki komutu girin:
   
        azure login
   
    Bu komut, bir tarayıcı başlatılır ve toohello indirme sayfasına gider. İstenirse, Azure aboneliğinizle ilişkili hello hesapla oturum açın.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    Merhaba dosya indirme otomatik olarak başlatır; yoksa, hello sayfa toomanually indirme hello dosyasının hello başında hello bağlantıyı tıklatabilirsiniz. Merhaba dosya ve Not hello dosya yolu kaydedin.
2. Komut tooimport hello ayarlarını aşağıdaki hello girin:
   
        azure account import <path-to-file>
   
    Merhaba önceki adımda ayarları dosyasını indirdiğiniz yayımlama hello Hello yolu ve dosya adını belirtin.
3. Hello ayarları alındıktan sonra hello silme yayımlama ayarları dosyası. Artık gerekli değildir ve Azure aboneliğinize ilişkin hassas bilgi içeriyor.

### <a name="create-an-app-service-web-app"></a>Bir App Service web uygulaması oluşturma
1. Komut satırı Hello, dizinleri toohello değiştirme **tasklist** dizin.
2. Komut toocreate yeni bir web uygulaması aşağıdaki hello kullanın.
   
        azure site create --git
   
    Merhaba web uygulaması adı ve konumu için istenir. Benzersiz bir ad ve select hello Azure Storage hesabınızı aynı coğrafi konumda sağlayın.
   
    Merhaba `--git` parametresi bu web uygulaması için Azure üzerinde bir Git deposu oluşturur. Hiçbiri varsa ve ekler, ayrıca bir Git deposu hello geçerli dizinde başlatır bir [Git uzaktan] 'azure' olarak adlandırılan olduğu kullanılan toopublish hello uygulama tooAzure. Son olarak, oluşturduğu bir **web.config** Azure toohost düğümü uygulamaları tarafından kullanılan ayarları içeren dosya. Merhaba atlarsanız `--git` parametre ancak hello dizini içeren bir Git deposu, hello komutu hala 'azure' hello uzaktan oluşturun.
   
    Bu komut tamamlandığında, çıkış benzer toohello aşağıdaki görürsünüz. Bu hello satır başlayarak Not **Web sitesi oluşturduğu adresindeki** hello hello web uygulaması URL'sini içerir.
   
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
   > Merhaba ilk App Service web uygulaması için aboneliğiniz varsa belirtildiği toouse hello Azure Portal toocreate hello web uygulaması olacaktır. Daha fazla bilgi için bkz: [derleme ve Azure App Service'te Node.js web uygulamasına dağıtma].
   > 
   > 

### <a name="set-environment-variables"></a>Ortam değişkenlerini ayarlama
Bu adımda, Azure üzerinde ortam değişkenleri tooyour web uygulama yapılandırması ekleyeceksiniz.
Merhaba komut satırından hello aşağıdakileri girin:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Değiştir  **<storage account name>**  hello depolama hello adla daha önce oluşturduğunuz hesap ve değiştirme  **<storage access key>**  hello depolama hesabınız için birincil erişim anahtarı ile. (Değerlerini aynı hello daha önce oluşturduğunuz hello config.json dosyası olarak kullanın.)

Alternatif olarak, hello ortam değişkenlerini ayarlayabilirsiniz [Azure Portal](https://portal.azure.com/):

1. Hello web uygulamanızın dikey tıklatarak **Gözat** > **Web uygulamaları** >, web uygulaması adı.
2. Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları** > **uygulama ayarları**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Toohello aşağı **uygulama ayarları** bölümünde ve hello anahtar/değer çiftleri ekleyin.
   
     ![Uygulama ayarları](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. **KAYDET**'e tıklayın.

### <a name="publish-hello-application"></a>Merhaba uygulama yayımlama
toopublish hello uygulama hello kod dosyaları tooGit kaydetmek ve tooazure/ana gönderme.

1. Dağıtım kimlik bilgilerinizi ayarlayın.
   
        azure site deployment user set <name> <password>
2. Ekleme ve uygulama dosyalarınızı uygulayın.
   
        git add .
        git commit -m "adding files"
3. Merhaba yürütme toohello App Service web uygulaması gönderin:
   
        git push azure master
   
    Kullanım **ana** hello hedef dala olarak. Merhaba dağıtım Hello sonunda, örneğin aşağıdaki deyim benzer toohello bakın:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Merhaba gönderme işlemi tamamlandıktan sonra daha önce hello tarafından döndürülen toohello web uygulaması URL'si Gözat `azure create site` uygulamanız tooview komutu.

## <a name="next-steps"></a>Sonraki adımlar
Hello tablo hizmeti toostore bilgileri kullanarak bu makaledeki Hello adımları açıklayan olsa da kullanabilirsiniz [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Ek kaynaklar
[Azure CLI]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

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

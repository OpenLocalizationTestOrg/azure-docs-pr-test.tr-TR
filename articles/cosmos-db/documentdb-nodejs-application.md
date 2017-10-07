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
# <a name="_Toc395783175"></a>Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Bu Node.js Öğreticisi nasıl toouse Azure Cosmos DB ve hello bir Node.js Express uygulamasında DocumentDB API toostore ve erişim verileri Azure Web Siteleri'nde barındırılan gösterir. Görevlerin oluşturulmasını, alınmasını ve tamamlanmasını sağlayan basit bir web tabanlı görev yönetimi uygulaması, yani yapılacak işler uygulaması oluşturacaksınız. Merhaba görevleri Azure Cosmos DB JSON belgeleri olarak depolanır. Bu öğretici hello oluşturulmasını ve dağıtımını hello uygulama anlatılmaktadır ve her parçasında neler olduğunu açıklar.

![Merhaba bu Node.js öğreticisinde oluşturulan Yapılacaklar listem uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Yoksa zaman toocomplete hello öğretici ve yalnızca tooget hello eksiksiz çözüm istiyorsunuz? Bir sorun hello tam örnek çözümü alabilirsiniz [GitHub][GitHub]. Merhaba okunan [Benioku](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) dosyası nasıl toorun hello uygulama hakkında yönergeler için.

## <a name="_Toc395783176"></a>Önkoşullar
> [!TIP]
> Bu Node.js öğreticisi, Node.js ve Azure Web Siteleri'ni kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar.
> 
> 

Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:

* Etkin bir Azure hesabı. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).

   OR

   Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md) (yalnızca Windows).
* [Node.js][Node.js] sürüm v0.10.29 veya üzeri.
* [Express oluşturucu](http://www.expressjs.com/starter/generator.html) (bunu `npm install express-generator -g` aracılığıyla yükleyebilirsiniz)
* [Git][Git].

## <a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma
İlk olarak bir Azure Cosmos DB hesabı oluşturalım. Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: yeni bir Node.js uygulaması oluşturma](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>2. adım: yeni bir Node.js uygulaması oluşturma
Şimdi toocreate hello kullanarak temel bir Hello World Node.js projesi öğrenelim [Express](http://expressjs.com/) framework.

1. Merhaba Node.js komut istemi gibi sık kullandığınız Terminali açın.
2. Toostore hello yeni uygulama istediğiniz toohello dizinine gidin.
3. Yeni bir uygulama olarak adlandırılan hello express oluşturucuyu toogenerate kullanmak **Yapılacaklar**.
   
        express todo
4. Yeni **todo** dizininizi açın ve bağımlılıkları yükleyin.
   
        cd todo
        npm install
5. Yeni uygulamanızı çalıştırın.
   
        npm start
6. Tarayıcınız çok giderek yeni uygulamanızı görüntüleyebilirsiniz[http://localhost: 3000](http://localhost:3000).
   
    ![Node.js - hello bir tarayıcı penceresinde Hello World uygulamasının ekran görüntüsü öğrenin](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Ardından, uygulama Merhaba, terminal penceresinde hello CTRL + C tuşlarına basın ve ardından toostop **y** tooterminate hello toplu iş.

## <a name="_Toc395783179"></a>3. Adım: Ek modülleri yükleme
Merhaba **package.json** dosya hello hello proje kökünde oluşturulan hello dosyaları biridir. Bu dosya, Node.js uygulamanız için gerekli olan ek modüllerin listesini içerir. Daha sonra bu uygulama tooAzure Web siteleri dağıttığınızda, bu dosya üzerinde Azure toosupport uygulamanızın hangi modülleri gerek toobe yüklü kullanılan toodetermine ' dir. Hala tooinstall iki daha fazla paket Bu öğretici için ihtiyacımız var.

1. Merhaba geri hello terminal, yükleme **zaman uyumsuz** npm aracılığıyla modülü.
   
        npm install async --save
2. Merhaba yüklemek **documentdb** npm aracılığıyla modülü. Bu tüm hello Azure Cosmos DB Sihirli nerede olacağını hello modülüdür.
   
        npm install documentdb --save
3. Merhaba Hızlı Kontrol **package.json** hello uygulama dosyasının ek modüller hello göster. Bu dosyayı Azure hangi paketlerin toodownload söyleyin ve uygulamanızı çalıştırırken yükleyin. Merhaba aşağıdaki örneğe benzemelidir.
   
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
   
    Bu düğüm, Düğüme (ve daha sonra Azure’a) uygulamanızın bu ek modüllere bağlı olduğunu bildirir.

## <a name="_Toc395783180"></a>4. adım: hello Azure Cosmos DB hizmeti bir düğüm uygulamasında kullanma
Tüm hello ilk kurulumu ve yapılandırması, şimdi şimdi get mvc'deki toowhy burada çalışıyoruz ve Azure Cosmos DB kullanarak bazı kod toowrite olmasıdır.

### <a name="create-hello-model"></a>Merhaba modeli oluşturma
1. Merhaba proje dizininde adlı yeni bir dizin oluşturun **modelleri** hello içinde hello package.json dosyası ile aynı dizinde.
2. Merhaba, **modelleri** dizin adlı yeni bir dosya oluşturun **taskDao.js**. Bu dosya, uygulamamız tarafından oluşturulan hello görevler için hello modeli içerecektir.
3. İçinde aynı hello **modelleri** dizin adlı başka bir yeni dosya oluşturun **docdbUtils.js**. Bu dosya, uygulama genelinde kullanacağımız bazı yararlı ve yeniden kullanılabilir kodları içerir. 
4. Kopya hello aşağıdaki kod içinde çok**docdbUtils.js**
   
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
   
5. Kaydet ve Kapat hello **docdbUtils.js** dosya.
6. Merhaba hello başında **taskDao.js** dosya, aşağıdaki kod tooreference hello hello eklemek **DocumentDBClient** ve hello **docdbUtils.js** yukarıda oluşturduğumuz:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Ardından, kodu toodefine ekleyin ve hello görev nesneyi verin. Bu kod Task nesnemizin başlatılmasından ve veritabanı ve belge kullanacağız koleksiyonunu hello ayarlama sorumludur.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Ardından, kod toodefine ek yöntemleri hello Task nesnesinde aşağıdaki hello Azure Cosmos DB içinde depolanan verileri ile etkileşim sağlayan ekleyin.
   
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
9. Kaydet ve Kapat hello **taskDao.js** dosya. 

### <a name="create-hello-controller"></a>Merhaba denetleyicisi oluşturun
1. Merhaba, **yollar** , projenizin dizin adlı yeni bir dosya oluşturun **tasklist.js**. 
2. Kod çok aşağıdaki hello eklemek**tasklist.js**. Bu tarafından kullanılan hello DocumentDBClient ve async modüllerini yükler **tasklist.js**. Bu ayrıca hello tanımlanan **TaskList** hello örneği geçirilen işlevi **görev** daha önce tanımladığımız:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Toohello eklemeye devam **tasklist.js** çok kullanılan hello yöntemleri ekleyerek dosya**showTasks, addTask**, ve **tasklist.js**:
   
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
4. Kaydet ve Kapat hello **tasklist.js** dosya.

### <a name="add-configjs"></a>Config.js ekleme
1. Proje dizininizde **config.js** adlı yeni bir dosya oluşturun.
2. Çok Hello ekleyin**config.js**. Bu, uygulamamız için gereken yapılandırma ayarlarını ve değerlerini tanımlar.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. Merhaba, **config.js** dosya, güncelleştirme hello değerleri HOST ve auth_key değerlerini hello Azure Cosmos DB hesabınızdaki hello anahtarlar dikey penceresinde bulunan hello değerleri kullanarak [Microsoft Azure portal](https://portal.azure.com).
4. Kaydet ve Kapat hello **config.js** dosya.

### <a name="modify-appjs"></a>App.js'yi değiştirme
1. Merhaba Hello proje dizininde açın **app.js** dosya. Merhaba Express web uygulaması oluşturduğunuzda bu dosya daha önce oluşturulmuş.
2. Aşağıdaki kod toohello üstündeki hello eklemek **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Bu kod kullanılan hello yapılandırma dosyası toobe tanımlar ve tooread değerleri bu dosyadan yakında kullanacağımız bazı değişkenlere devam eder.
4. Aşağıdaki iki satırı hello yerine **app.js** dosyası:
   
        app.use('/', index);
        app.use('/users', users); 
   
      Aşağıdaki kod parçacığında hello ile:
   
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
5. Bu satırlar yeni bir örneğini tanımlar bizim **Config.js** nesnesiyle yeni bir bağlantı tooAzure Cosmos DB (okunan hello hello değerleri kullanarak **config.js**), hello görev nesnesini başlatır ve ardından form eylemlerini bağlama üzerinde toomethods bizim **TaskList** denetleyicisi. 
6. Son olarak, Kaydet ve Kapat hello **app.js** dosya, biz işimiz neredeyse bitti.

## <a name="_Toc395783181"></a>5. Adım: Kullanıcı arabirimi oluşturma
Şimdi uygulamamız ile bir kullanıcı gerçekte etkileşim kurabilmesi bizim dikkat toobuilding hello kullanıcı arabirimi dönelim. kullandığı oluşturduğumuz Express uygulaması hello **Jade** hello görüntüleme altyapısı olarak. Jade hakkında daha fazla bilgi için lütfen çok başvurun[http://jade-lang.com/](http://jade-lang.com/).

1. Merhaba **layout.jade** hello dosyasında **görünümleri** dizin kullanılan genel bir şablon olarak diğer **.jade** dosyaları. Bu adımda, toouse değiştirecek [Twitter Bootstrap](https://github.com/twbs/bootstrap), kolay toodesign iyi görünümlü bir Web sitesi kolaylaştıran bir araç olan. 
2. Açık hello **layout.jade** dosyası bulundu hello **görünümleri** hello aşağıdaki klasörü ve Değiştir hello içeriğiyle:

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

    Bu hello etkili bir şekilde söyler **Jade** toorender uygulamamız için bazı HTML altyapısı ve oluşturur bir **blok** adlı **içerik** burada biz tedarik hello düzeni bizim içerik için sayfaları.

    Bu **layout.jade** dosyasını kaydedin ve kapatın.

3. Şimdi hello açmak **index.jade** dosya, uygulamamız tarafından kullanılacak olan ve hello dosyanın Merhaba içeriğine hello şununla değiştirin hello görünümü:
   
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
   

Bu, düzeni genişletir ve içerik Merhaba sağlayan **içerik** hello gördüğümüz yer tutucu **layout.jade** önceki dosya.
   
Bu düzende iki HTML formu oluşturduk.

Merhaba ilk formu içeren bir tablo için verilerimizi ve bize çok göndererek tooupdate öğeleri sağlayan bir düğmeyi**/completetask** denetleyicimizin yöntemi.
    
Merhaba ikinci formu içeren bize çok göndererek toocreate yeni bir öğe sağlayan bir düğmeyi ve iki giriş alanını**/addtask** denetleyicimizin yöntemi.

Bu bizim uygulama toowork için ihtiyacımız tüm olmalıdır.

## <a name="_Toc395783181"></a>6. Adım: Uygulamanızı yerel olarak çalıştırma
1. tootest hello uygulamayı yerel makinenizde çalıştırma `npm start` terminal toostart uygulamanızı hello ve ardından yenileme, [http://localhost: 3000](http://localhost:3000) tarayıcı sayfası. Başlangıç sayfasında, aşağıdaki hello görüntü gibi görünmelidir:
   
    ![Merhaba bir tarayıcı penceresinde Yapılacaklar listem uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Merhaba layout.jade dosyasında veya hello index.jade dosyasında hello girinti hakkında bir hata alırsanız, her iki dosya hello ilk iki satır sola hizalı olduğunu, boşluk emin olun. Merhaba ilk iki satır önce boşluklar varsa, bunları kaldırmanız, her iki dosya kaydedin, sonra tarayıcı pencerenizi yenileyin. 

2. Merhaba öğesi, öğe adı ve kategori alanlarını tooenter yeni bir görev kullanın ve ardından **Öğe Ekle**. Bu işlemden sonra Azure Cosmos DB içinde bu özelliklere sahip bir belge oluşturulur. 
3. Merhaba sayfa öğesi hello Yapılacaklar listesinde yeni oluşturulan toodisplay hello güncelleştirmeniz gerekir.
   
    ![Merhaba Yapılacaklar listesinde yeni bir öğesiyle hello uygulamasının ekran görüntüsü](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete bir görev yalnızca hello tam sütununda hello onay kutusunu işaretleyin ve ardından **güncelleştirme görevleri**. Bu, önceden oluşturulmuş hello belge güncelleştirir.

5. toostop Merhaba uygulaması hello terminal penceresinde CTRL + C tuşlarına basın ve ardından **Y** tooterminate hello toplu iş.

## <a name="_Toc395783182"></a>7. adım: uygulama geliştirme projesi tooAzure Web siteleri dağıtma
1. Daha önce yapmadıysanız Azure Web Siteniz için bir git deposunu etkinleştirin. Hakkında yönergeler bulabilirsiniz toodo bu hello [yerel Git dağıtımı tooAzure uygulama hizmeti](../app-service-web/app-service-deploy-local-git.md) konu.
2. Azure Web Sitenizi bir git uzak öğesi olarak ekleyin.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Toohello uzak ileterek dağıtın.
   
        git push azure master
4. Birkaç saniye içinde git web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!

    Tebrikler! Yalnızca ilk Node.js Express Web Azure Cosmos DB kullanarak uygulamanızı oluşturdunuz ve bunu tooAzure Web siteleri yayımladınız.

    Toodownload istediğiniz veya toohello eksiksiz başvuru uygulaması Bu öğretici için bkz, onu yüklenebilir [GitHub][GitHub].

## <a name="_Toc395637775"></a>Sonraki adımlar

* Tooperform ölçek ve performans ile Azure Cosmos DB istiyorsunuz? Bkz. [Azure Cosmos DB ile Performans ve Ölçek Testi](performance-testing.md)
* Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).
* Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).
* Merhaba keşfedin [Azure Cosmos DB belgeleri](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app


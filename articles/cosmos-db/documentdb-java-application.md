---
title: "Azure Cosmos DB kullanarak aaaJava uygulaması geliştirme Öğreticisi | Microsoft Docs"
description: "Bu Java web uygulaması Öğreticisi nasıl toouse Azure Cosmos DB hello DocumentDB API toostore hello ve Azure Web Siteleri'nde barındırılan bir Java uygulamasında verilere gösterir."
keywords: "Uygulama geliştirme, veritabanı öğreticisi, java uygulaması, java web uygulaması öğreticisi, documentdb, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Azure Cosmos DB ve hello DocumentDB API kullanarak bir Java web uygulaması oluşturma
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Bu Java web uygulaması Öğreticisi şunların nasıl yapıldığını gösterir toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmeti toostore ve erişim verilerini Azure App Service Web Apps üzerinde barındırılan bir Java uygulamasında. Bu konu başlığında şunları öğreneceksiniz:

* Nasıl toobuild eclipse'te temel bir JavaServer sayfaları (JSP) uygulaması.
* Toowork hello Azure Cosmos DB ile nasıl hizmet hello kullanarak [Azure Cosmos DB Java SDK'sı](https://github.com/Azure/azure-documentdb-java).

Bu Java uygulaması Öğreticisi, toocreate, almak ve işareti etkinleştirir toocreate web tabanlı görev yönetimi uygulamasını nasıl görevler tamamlandı olarak hello görüntü aşağıdaki gösterildiği gibi gösterir. Her bir hello görev hello Yapılacaklar listesinde Azure Cosmos DB JSON belgeleri olarak depolanır.

![Yapılacaklar Listesi Java uygulamam](./media/documentdb-java-application/image1.png)

> [!TIP]
> Bu uygulama geliştirme öğreticisi, Java kullanımına ilişkin deneyim sahibi olduğunuzu varsayar. Yeni tooJava veya hello ise [önkoşul araçlarında](#Prerequisites), hello tam indirme öneririz [Yapılacaklar](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub ve kullanarak proje [hello sonunda hello bu yönergeleri makale](#GetProject). Oluşturduktan sonra hello makale toogain Insight hello proje hello bağlamında hello kodu gözden geçirebilirsiniz.  
> 
> 

## <a id="Prerequisites"></a>Bu Java web uygulaması öğreticisi için önkoşullar
Bu uygulama geliştirme Öğreticisine başlamadan önce hello şunlara sahip olmanız gerekir:

* Etkin bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/)

    OR

    Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).
* [Java Geliştirme Seti (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Java EE Geliştiricileri için Eclipse IDE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Etkin bir Java Çalışma zamanı ortamı (ör. Tomcat veya Jetty) sahip bir Azure Web sitesi.](../app-service-web/web-sites-java-get-started.md)

Hello için bu araçları ilk kez yüklüyorsanız coreservlets.com hello hızlı başlangıç bölümünde hello yükleme işleminin bir kılavuz sağlar. kendi [öğretici: tomcat7'yi yükleme ve Eclipse ile kullanma](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) makalesi.

## <a id="CreateDB"></a>1. adım: Azure Cosmos DB hesabı oluşturma
İlk olarak bir Azure Cosmos DB hesabı oluşturalım. Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: hello Java JSP uygulaması oluşturma](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>2. adım: Merhaba Java JSP uygulaması oluşturma
toocreate hello JSP uygulaması:

1. İlk olarak, bir Java projesi oluşturarak başlayacağız. Eclipse'i başlatın, ardından **Dosya**'ya tıklayın, **Yeni**'ye tıklayın ve ardından **Dinamik Web Projesi**'ne tıklayın. Görmüyorsanız, **dinamik Web projesi** kullanılabilir bir proje listelenen, aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**,'ı tıklatın **proje**... genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.
   
    ![JSP Java Uygulaması Geliştirme](./media/documentdb-java-application/image10.png)
2. Hello proje adı girin **proje adı** kutusunda ve hello **hedef çalışma zamanı** açılan menüsünde isteğe bağlı olarak bir değer (örn. Apache Tomcat v7.0) seçin ve ardından **Son**. Bir hedef çalışma zamanı seçildiğinde, toorun projeniz yerel olarak Eclipse aracılığıyla etkinleştirilir.
3. Eclipse'te, hello Proje Gezgini görünümünde projenizi genişletin. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.
4. Merhaba, **yeni JSP dosyası** iletişim kutusu, ad hello dosyası **index.jsp**. Merhaba üst klasörünü olarak **WebContent**, aşağıdaki çizimde hello ve ardından gösterildiği gibi **sonraki**.
   
    ![Yeni bir JSP Dosyası Oluşturma - Java Web Uygulaması Öğreticisi](./media/documentdb-java-application/image11.png)
5. Merhaba, **JSP şablon seç** iletişim kutusunda, Bu öğretici seçimi hello amaçla **yeni JSP dosyası (html)**ve ardından **son**.
6. Merhaba index.jsp dosyası Eclipse'te açıldığında, metin toodisplay ekleme **Merhaba Dünya!** Merhaba varolan içinde <body> öğesi. Güncelleştirilmiş <body> içerik hello kod aşağıdaki gibi görünmelidir:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Merhaba index.jsp dosyasını kaydedin.
8. 2. adımda bir hedef çalışma zamanı ayarlarsanız, tıklayabilirsiniz **proje** ve ardından **çalıştırmak** toorun JSP uygulamanızı yerel olarak:
   
    ![Hello World - Java Uygulaması Öğreticisi](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>3. adım: Merhaba DocumentDB Java SDK'sını yükleme
Merhaba hello DocumentDB Java SDK'sını ve bağımlılıklarını en kolay yolu toopull aracılığıyladır [Apache Maven](http://maven.apache.org/).

toodo bunu hello aşağıdaki adımları tamamlayarak proje tooa maven projenizi tooconvert gerekir:

1. Merhaba proje Gezgini'nde projenize sağ tıklayın, **yapılandırma**, tıklatın **tooMaven proje Dönüştür**.
2. Merhaba, **yeni POM Oluştur** penceresinde hello Varsayılanları kabul edin ve tıklatın **son**.
3. İçinde **Proje Gezgini**açın hello pom.xml dosyasını.
4. Merhaba üzerinde **bağımlılıkları** sekmede hello **bağımlılıkları** bölmesinde tıklatın **Ekle**.
5. Merhaba, **bağımlılık Seç** penceresinde, aşağıdaki hello:
   
   * Merhaba, **Grup Kimliği** kutusuna, com.microsoft.azure girin.
   * Merhaba, **Artifact ID** kutusuna, azure-documentdb girin.
   * Merhaba, **sürüm** kutusuna, 1.5.1 girin.
     
   ![DocumentDB Java Uygulaması SDK'sını yükleme](./media/documentdb-java-application/image13.png)
     
   * Grup Kimliği ve yapı kimliği için hello bağımlılık XML ekleyin bir metin düzenleyicisi aracılığıyla doğrudan toohello pom.xml:
     
        <dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency>
6. Tıklatın **Tamam** ve Maven hello DocumentDB Java SDK'sını yükler.
7. Merhaba pom.xml dosyasını kaydedin.

## <a id="UseService"></a>4. adım: hello Azure Cosmos DB hizmeti bir Java uygulamasında kullanma
1. İlk olarak, şimdi hello Todoıtem nesnesini TodoItem.java içinde tanımlayın:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    Bu projede kullanıyoruz [Project Lombok](http://projectlombok.org/) toogenerate hello oluşturucusu, alıcılar, ayarlayıcılar ve oluşturucu. Alternatif olarak, bu kodu el ile yazabilir veya sahip hello IDE oluşturur.
2. tooinvoke hello Azure Cosmos DB hizmeti, gerekir örneği yeni bir **DocumentClient**. Genel olarak, en iyi tooreuse hello olan **DocumentClient** - yerine sonraki her istek için yeni bir istemci oluşturmak. Biz hello istemci hello istemciyi yeniden bir **DocumentClientFactory**. DocumentClientFactory.java içinde tooyour Pano'da kaydettiğiniz toopaste hello URI ve birincil anahtar değerine ihtiyacı vardır [1. adım](#CreateDB). [YOUR\_ENDPOINT\_HERE] yerine URI'nizi ve [YOUR\_KEY\_HERE] yerine BİRİNCİL ANAHTARINIZI girin.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Şimdi bizim Yapılacaklar öğelerini tooAzure Cosmos DB kalıcı bir veri erişim nesnesi (DAO) tooabstract oluşturalım.
   
    İçinde toosave Yapılacaklar öğelerini tooa koleksiyonu sipariş, hello istemci tooknow çok hangi veritabanı ve koleksiyonu toopersist gerekir (tarafından başvurulduğu kendine bağlantılar). Genel olarak, en iyi toocache hello veritabanı ve koleksiyonu mümkün olduğunda olduğu tooavoid ek gidiş dönüş toohello veritabanı.
   
    Merhaba aşağıdaki kod gösterir nasıl tooretrieve veritabanımızın ve koleksiyonumuzun var veya yoksa yeni bir tane oluşturun:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. Merhaba sonraki adım toowrite toohello koleksiyonundaki bazı kod toopersist hello Todoıtems olduğu. Bu örnekte, kullanacağız [Gson](https://code.google.com/p/google-gson/) tooserialize ve seri durumundan Todoıtem eski basit Java nesnelerini (Pojo'lar) tooJSON belgeleri.
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Azure Cosmos DB veritabanları ve koleksiyonlarına benzer şekilde belgelere de kendine bağlantılar tarafından başvurulur. yardımcı işlevi sağlar bize alma belgeleri başka bir öznitelik (örneğin, "id") tarafından hello yerine kendi bağlantı:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Merhaba yardımcı yöntem kimliğine göre 5. adım tooretrieve bir Todoıtem JSON belgesini kullanın ve tooa POJO'ya seri durumdan:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Biz de hello DocumentClient tooget bir koleksiyonu veya Todoıtems DocumentDB SQL kullanarak listesini kullanarak şunları yapabilirsiniz:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Merhaba DocumentClient ile bir belge birçok yolu tooupdate vardır. Bizim Yapılacaklar listesi uygulaması Todoıtem tam olup toobe mümkün tootoggle istiyoruz. Hello hello belge içinde "tamamlandı" özniteliğini güncelleştirerek bunu yapabiliriz:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Son olarak, hello özelliği toodelete Todoıtem listemizden istiyoruz. toodo Bu, daha önce yazdığımız hello yardımcı yöntemini kullanırız tooretrieve kendi bağlantı hello ve hello istemci toodelete söyleyin onu:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>5. adım: Java uygulaması geliştirme projesinin hello hello kalan birlikte bağlantı kabloları
Biz hello eğlenceli kısımları tamamladığımıza göre şimdi bitleri - kalan tüm toobuild bir hızlı kullanıcı arabirimi ve DAO tooour wire.

1. İlk olarak, bir denetleyici toocall bizim DAO oluşturmaya başlayalım:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    Daha karmaşık bir uygulamada hello denetleyicisi hello DAO üstünde karmaşık iş mantığı barındırabilir.
2. Ardından, bir servlet tooroute HTTP isteklerini toohello denetleyicisi oluşturacağız:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Bir web kullanıcı arabirimi toodisplay toohello kullanıcı ihtiyacımız. Merhaba index.jsp daha önce oluşturduğumuz yeniden yazalım:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Son olarak, bazı istemci tarafı JavaScript tootie hello web kullanıcı arabirimini yazmak ve servlet'i birbirine hello:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Harika! Kalan tüm sunulmuştur tootest Merhaba uygulaması. Merhaba uygulamayı yerel olarak çalıştırın ve hello öğe adı ve kategoriyi doldurarak ve tıklayarak birkaç Yapılacaklar öğesi ekleyin **Görev Ekle**.
6. Merhaba öğe göründükten sonra hello onay kutusu geçiş ve tıklayarak tamamlanmadan olarak güncelleştirebilirsiniz **güncelleştirme görevleri**.

## <a id="Deploy"></a>6. adım: Java uygulaması tooAzure Web siteleri dağıtma
Uygulamanızı bir WAR dosyası olarak dışarı aktarma ve ya da kaynak denetimi (ör. Gıt) veya FTP aracılığıyla karşıya kadar basit Java uygulamalarını dağıtma azure Web siteleri yapar.

1. Uygulamanızı bir WAR dosyası olarak tooexport sağ tıklatın, projenizde üzerinde **Proje Gezgini**, tıklatın **verme**ve ardından **WAR dosyasını**.
2. Merhaba, **WAR dışarı** penceresinde, aşağıdaki hello:
   
   * Merhaba Web projesi kutusuna azure-documentdb-java-sample girin.
   * Merhaba hedef kutusunda bir hedef toosave hello WAR dosyası seçin.
   * **Son**'a tıklayın.
3. Eldeki elinizde bir WAR dosyası, yalnızca bu tooyour Azure Web sitesine ait yükleyebilirsiniz **webapps** dizin. Merhaba dosya karşıya yükleme ile ilgili yönergeler için bkz: [bir Java uygulaması tooAzure App Service Web Apps eklemek](../app-service-web/web-sites-java-add-app.md).
   
    Merhaba WAR dosyasını karşıya yüklenen toohello webapps dizinine eklendiğinde, hello çalışma zamanı ortamı bunu eklemiş ve otomatik olarak algılar.
4. tooview tamamlanmış ürününüzü toohttp://YOUR gidin\_SITE\_NAME.azurewebsites.net/azure-java-sample/ ve görevlerinizi eklemeye başlayın!

## <a id="GetProject"></a>Merhaba projeyi Github'dan alma
Bu öğreticideki tüm hello örnekleri hello dahil edilen [Yapılacaklar](https://github.com/Azure-Samples/documentdb-java-todo-app) projeyi github'dan edinilebilir. tooimport hello Yapılacaklar Eclipse, projeye emin olun hello yazılım ve hello listelenen kaynakları [Önkoşullar](#Prerequisites) bölümünde, ardından aşağıdaki hello:

1. [Proje Lombok](http://projectlombok.org/)'u yükleyin. Lombok kullanılan toogenerate Oluşturucular, alıcılar ve ayarlayıcılar hello projesinde olur. Merhaba lombok.jar dosyasını indirdikten sonra buna çift tıklayarak tooinstall onu veya hello komut satırından yükleyin.
2. Eclipse açıksa kapatın ve tooload Lombok yeniden başlatın.
3. Eclipse'te, hello **dosya** menüsünde tıklatın **alma**.
4. Merhaba, **alma** penceresinde, tıklatın **Git**, tıklatın **Git projeleri**ve ardından **sonraki**.
5. Merhaba üzerinde **depo kaynağı seçin** ekranında **URI'yi kopyalama**.
6. Merhaba üzerinde **kaynak Git deposu** ekranında hello **URI** kutusuna https://github.com/Azure-Samples/java-todo-app.git girin ve ardından **sonraki**.
7. Merhaba üzerinde **dal seçimi** ekranında, emin **ana** seçilir ve ardından **sonraki**.
8. Merhaba üzerinde **yerel hedef** ekranında **Gözat** tooselect burada hello deposu kopyalanabilir ve ardından bir klasörü **sonraki**.
9. Merhaba üzerinde **projeleri İçeri Aktarma Sihirbazı'nı toouse seçin** ekranında, emin **var olan projeleri içeri aktar** seçilir ve ardından **sonraki**.
10. Merhaba üzerinde **projeleri içeri aktar** ekran, Seçimi Kaldır hello **DocumentDB** proje ve ardından **son**. Merhaba DocumentDB projesi hello Azure Cosmos DB Java biz bağımlılık olarak ekleyeceğimiz SDK içerir.
11. İçinde **Proje Gezgini**, tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java gidin ve hello URI ve birincil anahtar hello HOST ve MASTER_KEY değerlerini değiştirin Azure Cosmos DB hesabını tıklatın ve ardından Kaydet hello dosya. Daha fazla bilgi için bkz. [1. Adım. Bir Azure Cosmos DB veritabanı hesabı oluşturma](#CreateDB).
12. İçinde **Proje Gezgini**, hello sağ tıklayın **azure-documentdb-java-sample**, tıklatın **yapı yolu**ve ardından **oluşturma yolunu Yapılandır**.
13. Merhaba üzerinde **Java oluşturma yolu** , hello sağ bölmede, select Merhaba ekranında **kitaplıkları** sekmesini ve ardından **dış Jar'lar Ekle**. Merhaba lombok.jar dosyasının konumunu toohello gidin ve tıklayın **açık**ve ardından **Tamam**.
14. Kullanım 12. adımı tooopen hello **özellikleri** penceresini tekrar ve ardından hello sol bölmedeki tıklatın **hedeflenen çalışma zamanları**.
15. Merhaba üzerinde **hedeflenen çalışma zamanları** ekranında **yeni**seçin **Apache Tomcat v7.0**ve ardından **Tamam**.
16. Kullanım 12. adımı tooopen hello **özellikleri** penceresini tekrar ve ardından hello sol bölmedeki tıklatın **proje modelleri**.
17. Merhaba üzerinde **proje modelleri** ekran, select **dinamik Web Modülü** ve **Java**ve ardından **Tamam**.
18. Merhaba üzerinde **sunucuları** sekmesinde hello ekranın hello altında sağ **Server localhost'ta Tomcat v7.0** ve ardından **ekleme ve kaldırma**.
19. Merhaba üzerinde **ekleme ve kaldırma** penceresinde taşıma **azure-documentdb-java-sample** toohello **yapılandırıldı** kutusuna ve ardından **son**.
20. Merhaba, **sunucuları** sekmesinde, sağ **Server localhost'ta Tomcat v7.0**ve ardından **yeniden**.
21. Bir tarayıcıda toohttp://localhost:8080 gidin / azure-documentdb-java-sample / ve tooyour görev listesi eklemeye başlayın. Varsayılan bağlantı noktası değerlerini değiştirdiyseniz, seçtiğiniz 8080 toohello değerini değiştirin unutmayın.
22. toodeploy, proje tooan Azure web sitesine bakın [adım 6. Uygulama tooAzure Web sitelerini dağıtmak](#Deploy).

[1]: media/documentdb-java-application/keys.png

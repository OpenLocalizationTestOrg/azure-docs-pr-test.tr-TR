---
<span data-ttu-id="1962e-101">Başlık: aaa "Azure Cosmos DB: Golang ile MongoDB API konsol uygulaması oluşturma ve Azure portal hello | Microsoft Docs"Açıklama: tooconnect tooand kullanabileceğiniz Golang kod örnek sorgu Azure Cosmos DB hizmetleri sunar: cosmos db Yazar: Durgaprasad Budhwani Yöneticisi: jhubbard Düzenleyicisi: mimig1</span><span class="sxs-lookup"><span data-stu-id="1962e-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="1962e-102">MS.Service: cosmos db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="1962e-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="1962e-103">Azure Cosmos DB: Golang ile MongoDB API konsol uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="1962e-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="1962e-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1962e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1962e-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1962e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="1962e-106">Bu hızlı başlangıç gösteren nasıl varolan toouse [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) yazılmış uygulama [Golang](https://golang.org/) ve MongoDB istemci bağlantılarını destekleyen tooyour Azure Cosmos DB veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1962e-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="1962e-107">Diğer bir deyişle, Golang uygulamanız yalnızca MongoDB API'lerini kullanarak tooa veritabanına bağlanma olduğunu bilir.</span><span class="sxs-lookup"><span data-stu-id="1962e-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="1962e-108">Saydam veri hello toohello uygulama Azure Cosmos DB içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="1962e-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1962e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1962e-109">Prerequisites</span></span>

- <span data-ttu-id="1962e-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1962e-110">An Azure subscription.</span></span> <span data-ttu-id="1962e-111">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1962e-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="1962e-112">[Git](https://golang.org/dl/) ve hello temel bilgiye [Git](https://golang.org/) dili.</span><span class="sxs-lookup"><span data-stu-id="1962e-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="1962e-113">Bir IDE: Jetbrains tarafından sağlanan [Gogland](https://www.jetbrains.com/go/), Microsoft tarafından sağlanan [Visual Studio Code](https://code.visualstudio.com/) veya [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="1962e-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="1962e-114">Bu öğreticide Goglang’i kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="1962e-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="1962e-115">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1962e-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="1962e-116">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="1962e-116">Clone hello sample application</span></span>

<span data-ttu-id="1962e-117">Merhaba örnek uygulaması kopyalama ve gerekli hello paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1962e-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="1962e-118">Varsayılan olarak C:\Go\ olan hello GOROOT\src klasörünün içindeki CosmosDBSample adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1962e-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="1962e-119">Git terminal penceresi git bash tooclone hello örnek deposu gibi hello CosmosDBSample klasörüne kullanarak komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1962e-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="1962e-120">Çalışma hello aşağıdaki tooget hello mgo paket komutu.</span><span class="sxs-lookup"><span data-stu-id="1962e-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="1962e-121">Merhaba [mgo](http://labix.org/mgo) sürücüsü (olarak belirgin *mango*) olan bir [MongoDB](http://www.mongodb.org/) hello için sürücü [Git dil](http://golang.org/) zengin bir uygular ve test Standart Git deyimleri aşağıdaki çok basit bir API altında özellik seçimi.</span><span class="sxs-lookup"><span data-stu-id="1962e-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="1962e-122">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1962e-122">Update your connection string</span></span>

<span data-ttu-id="1962e-123">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1962e-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="1962e-124">Tıklatın **Hızlı Başlangıç** sol gezinti menüsü hello ve ardından **diğer** tooview hello bağlantı dizesi bilgilerini hello Git uygulama tarafından gerekli.</span><span class="sxs-lookup"><span data-stu-id="1962e-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="1962e-125">Goglang, hello GOROOT\CosmosDBSample dizininde hello main.go dosyasını açın ve hello ekran aşağıdaki gösterildiği gibi hello bağlantı dizesi bilgileri hello Azure portal kullanarak kod satırı aşağıdaki hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1962e-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="1962e-126">Merhaba veritabanı adıdır hello hello öneki **konak** hello Azure portal bağlantı dizesi bölmesinde değeri.</span><span class="sxs-lookup"><span data-stu-id="1962e-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="1962e-127">Merhaba resimde gösterilen hello hesabı için golang Çalıştırıcı hello veritabanı adı değil.</span><span class="sxs-lookup"><span data-stu-id="1962e-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Hızlı Başlangıç bölmesi, diğer sekmesinde hello Azure portal gösteren hello bağlantı dizesi bilgileri](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="1962e-129">Merhaba main.go dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1962e-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="1962e-130">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="1962e-130">Review hello code</span></span>

<span data-ttu-id="1962e-131">Neler olduğuna dair hello main.go dosyasında hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="1962e-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="1962e-132">Merhaba Git uygulama tooAzure Cosmos DB bağlanma</span><span class="sxs-lookup"><span data-stu-id="1962e-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="1962e-133">Azure Cosmos DB hello SSL etkin MongoDB destekler.</span><span class="sxs-lookup"><span data-stu-id="1962e-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="1962e-134">tooconnect tooan SSL etkin MongoDB, gereksinim duyduğunuz toodefine hello **DialServer** işlevi [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)ve yapın hello kullan [tls. *Arama* ](http://golang.org/pkg/crypto/tls#Dial) işlev tooperform hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1962e-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="1962e-135">Golang kod parçacığını aşağıdaki hello hello Git uygulama Azure Cosmos DB MongoDB API'si ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1962e-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="1962e-136">Merhaba *DialInfo* sınıf, MongoDB kümesi ile bir oturumu için seçenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1962e-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="1962e-137">Merhaba **mgo. Dial()** yöntemi, hiçbir SSL bağlantısı olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1962e-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="1962e-138">Bir SSL bağlantısı için hello **mgo. DialWithInfo()** yöntemi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1962e-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="1962e-139">Merhaba örneği **DialWIthInfo {}** kullanılan toocreate hello oturum nesnesi bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="1962e-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="1962e-140">Merhaba oturum kurulduktan sonra aşağıdaki kod parçacığını hello kullanarak hello koleksiyonuna erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1962e-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="1962e-141">Belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="1962e-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="1962e-142">Bir belgeyi sorgulama veya okuma</span><span class="sxs-lookup"><span data-stu-id="1962e-142">Query or read a document</span></span>

<span data-ttu-id="1962e-143">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için zengin sorguların gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="1962e-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="1962e-144">Merhaba aşağıdaki örnek kod koleksiyonunuzda hello belgeleri karşı çalıştırabileceğiniz bir sorguyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1962e-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="1962e-145">Bir belgeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1962e-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="1962e-146">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="1962e-146">Delete a document</span></span>

<span data-ttu-id="1962e-147">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="1962e-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="1962e-148">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1962e-148">Run hello app</span></span>

1. <span data-ttu-id="1962e-149">Goglang içinde GOPATH emin olun (altında kullanılabilir **dosya**, **ayarları**, **Git**, **GOPATH**) hangi hello hello konumda içerir gopkg, USERPROFILE\go olduğu varsayılan olarak yüklendi.</span><span class="sxs-lookup"><span data-stu-id="1962e-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="1962e-150">Merhaba belge çalışan hello uygulamasının adını görebilmeniz için hello belge, satırları 91-96 Sil hello satırları açıklama.</span><span class="sxs-lookup"><span data-stu-id="1962e-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="1962e-151">Goglang’de **Çalıştır**’a ve ardından **'Main.go’yu derle ve çalıştır'ı çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1962e-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="1962e-152">Merhaba uygulama tamamlandıktan ve oluşturulan hello belge hello açıklamasını görüntüler [bir belge oluşturmak](#create-document).</span><span class="sxs-lookup"><span data-stu-id="1962e-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Merhaba uygulama Hello çıktısını gösteren Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="1962e-154">Veri Gezgini’nde belgenizi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="1962e-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="1962e-155">Azure portal toosee toohello Veri Gezgini belgenize dönün.</span><span class="sxs-lookup"><span data-stu-id="1962e-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="1962e-156">Tıklatın **Veri Gezgini (Önizleme)** hello sol gezinti menüsünde genişletin **golang Çalıştırıcı**, **paket**ve ardından **belgeleri**.</span><span class="sxs-lookup"><span data-stu-id="1962e-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="1962e-157">Merhaba, **belgeleri** sekmesini ve ardından hello \_kimliği toodisplay hello belge hello sağ bölmedeki.</span><span class="sxs-lookup"><span data-stu-id="1962e-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Veri Gezgini gösteren yeni oluşturulan hello belgesi](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="1962e-159">Daha sonra iş hello belge satır içi ve tıklatın **güncelleştirme** toosave onu.</span><span class="sxs-lookup"><span data-stu-id="1962e-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="1962e-160">Merhaba belge silin veya yeni belgeler veya sorgular oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1962e-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="1962e-161">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="1962e-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1962e-162">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="1962e-162">Clean up resources</span></span>

<span data-ttu-id="1962e-163">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="1962e-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="1962e-164">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1962e-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="1962e-165">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="1962e-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1962e-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1962e-166">Next steps</span></span>

<span data-ttu-id="1962e-167">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız ve Golang uygulamasını kullanarak çalışma MongoDB için API hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="1962e-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="1962e-168">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1962e-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1962e-169">Merhaba MongoDB API Azure Cosmos Veritabanına veri alma</span><span class="sxs-lookup"><span data-stu-id="1962e-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

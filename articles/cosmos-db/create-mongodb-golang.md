---
title: "Azure Cosmos DB: Golang ve Azure portalıyla bir MongoDB API'si konsol uygulaması oluşturma | Microsoft Docs"
description: "Azure Cosmos DB’ye bağlanmak ve veritabanını sorgulamak için kullanabileceğiniz bir Golang kod örneği sunar"
services: cosmos-db
author: Durgaprasad-Budhwani
manager: jhubbard
editor: mimig1
ms.service: cosmos-db
ms.topic: hero-article
ms.date: 07/21/2017
ms.author: mimig
ms.openlocfilehash: 9461a5d86b321fd02167379ba8751d44a861ebc2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="5517d-103">Azure Cosmos DB: Golang ve Azure portalıyla bir MongoDB API'si konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5517d-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

<span data-ttu-id="5517d-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="5517d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="5517d-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5517d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="5517d-106">Bu hızlı başlangıçta, [Golang](https://golang.org/) dilinde yazılmış mevcut bir [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) uygulamasını kullanma ve MongoDB istemci bağlantılarını destekleyen Azure Cosmos DB veritabanınıza bağlama işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5517d-106">This quick-start demonstrates how to use an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="5517d-107">Diğer bir deyişle, Golang uygulamanız yalnızca MongoDB API’lerini kullanarak bir veritabanına bağlandığını bilir.</span><span class="sxs-lookup"><span data-stu-id="5517d-107">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="5517d-108">Verilerin Azure Cosmos DB'de depolandığı uygulamaya açıkça gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5517d-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5517d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5517d-109">Prerequisites</span></span>

- <span data-ttu-id="5517d-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="5517d-110">An Azure subscription.</span></span> <span data-ttu-id="5517d-111">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5517d-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="5517d-112">[Go](https://golang.org/dl/) ve [Go](https://golang.org/) dilinde temel bilgi düzeyi.</span><span class="sxs-lookup"><span data-stu-id="5517d-112">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="5517d-113">Bir IDE: Jetbrains tarafından sağlanan [Gogland](https://www.jetbrains.com/go/), Microsoft tarafından sağlanan [Visual Studio Code](https://code.visualstudio.com/) veya [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="5517d-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="5517d-114">Bu öğreticide Goglang’i kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="5517d-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="5517d-115">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5517d-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="5517d-116">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="5517d-116">Clone the sample application</span></span>

<span data-ttu-id="5517d-117">Örnek uygulamayı kopyalayın ve gerekli paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5517d-117">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="5517d-118">GOROOT\src klasörünün (varsayılan olarak C:\Go\ konumundadır) içinde CosmosDBSample adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5517d-118">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="5517d-119">Git bash gibi bir git terminal penceresinde aşağıdaki komutu çalıştırarak örnek depoyu CosmosDBSample klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-119">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="5517d-120">Mgo paketini edinmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5517d-120">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="5517d-121">[Mgo](http://labix.org/mgo) sürücüsü (*mango* olarak telaffuz edilir), standart Go deyimlerini izleyen çok basit bir API altında zengin ve kendini kanıtlamış bir dizi özelliği uygulayan [Go diline](http://golang.org/) yönelik bir [MongoDB](http://www.mongodb.org/) sürücüsüdür.</span><span class="sxs-lookup"><span data-stu-id="5517d-121">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="5517d-122">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5517d-122">Update your connection string</span></span>

<span data-ttu-id="5517d-123">Bu adımda Azure portalına dönerek bağlantı dizesi bilgilerinizi kopyalayıp uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5517d-123">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="5517d-124">Go uygulaması için gerekli olan bağlantı dizesi verilerini görüntülemek için sol gezinti menüsünde **Hızlı başlangıç**’a ve ardından **Diğer**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-124">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="5517d-125">Goglang’de GOROOT\CosmosDBSample dizinindeki main.go dosyasını açın ve aşağıdaki ekran görüntüsünde gösterildiği gibi Azure portalından edinilen bağlantı dizesi bilgilerini kullanarak aşağıdaki kod satırlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5517d-125">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="5517d-126">Veritabanı adı, Azure portalı bağlantı dizesi bölmesindeki **Konak** değerinin ön ekidir.</span><span class="sxs-lookup"><span data-stu-id="5517d-126">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="5517d-127">Aşağıdaki resimde gösterilen hesap için Veritabanı adı golang-coach şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="5517d-127">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Azure portalında bağlantı dizesi bilgilerini gösteren Hızlı başlangıç bölmesi, Diğer sekmesi](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="5517d-129">Main.go adlı dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5517d-129">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="5517d-130">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="5517d-130">Review the code</span></span>

<span data-ttu-id="5517d-131">Main.go dosyasında gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="5517d-131">Let's make a quick review of what's happening in the main.go file.</span></span> 

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="5517d-132">Azure Cosmos DB’yi kullanarak Go uygulamasına bağlanma</span><span class="sxs-lookup"><span data-stu-id="5517d-132">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="5517d-133">Azure Cosmos DB, SSL kullanan MongoDB’yi destekler.</span><span class="sxs-lookup"><span data-stu-id="5517d-133">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="5517d-134">SSL kullanan bir MongoDB’ye bağlanmak için [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo)’da **DialServer** işlevini tanımlamanız ve bağlantıyı gerçekleştirmek için [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) işlevini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5517d-134">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="5517d-135">Aşağıdaki Golang kod parçacığı, Go uygulaması ile Azure Cosmos DB MongoDB API’si arasında bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="5517d-135">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="5517d-136">*DialInfo* sınıfı, bir MongoDB kümesiyle oturum bağlantısı kurmak için gereken seçenekleri barındırır.</span><span class="sxs-lookup"><span data-stu-id="5517d-136">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

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
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="5517d-137">SSL bağlantısı yoksa **mgo.Dial()** yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5517d-137">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="5517d-138">SSL bağlantısı için **mgo.DialWithInfo()** yöntemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5517d-138">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="5517d-139">Oturum nesnesinin oluşturulması için **DialWIthInfo{}** nesnesinin bir örneği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5517d-139">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="5517d-140">Oturum bağlantısı kurulduktan sonra aşağıdaki kod parçacığını kullanarak koleksiyona erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5517d-140">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="5517d-141">Belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="5517d-141">Create a document</span></span>

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

### <a name="query-or-read-a-document"></a><span data-ttu-id="5517d-142">Bir belgeyi sorgulama veya okuma</span><span class="sxs-lookup"><span data-stu-id="5517d-142">Query or read a document</span></span>

<span data-ttu-id="5517d-143">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için zengin sorguların gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="5517d-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="5517d-144">Aşağıdaki örnek kod, koleksiyonunuzdaki belgeler için çalıştırabileceğiniz bir sorguyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5517d-144">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="5517d-145">Bir belgeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5517d-145">Update a document</span></span>

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

### <a name="delete-a-document"></a><span data-ttu-id="5517d-146">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="5517d-146">Delete a document</span></span>

<span data-ttu-id="5517d-147">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="5517d-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="5517d-148">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5517d-148">Run the app</span></span>

1. <span data-ttu-id="5517d-149">Goglang’da GOPATH’inizin (**Dosya**, **Ayarlar**, **Go**, **GOPATH** altındadır) gopkg’nin yüklendiği ve varsayılan olarak USERPROFILE\go olan konumu içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5517d-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="5517d-150">Uygulamayı çalıştırdıktan sonra belgeyi görebilmeniz için 91.-96. satırlar arasında yer alan ve belgeyi silen satırları açıklama satırı yapın.</span><span class="sxs-lookup"><span data-stu-id="5517d-150">Comment out the lines that delete the document, lines 91-96, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="5517d-151">Goglang’de **Çalıştır**’a ve ardından **'Main.go’yu derle ve çalıştır'ı çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="5517d-152">Uygulama işlemi tamamlar ve [Belge oluşturma](#create-document)’da oluşturulan belgenin açıklamasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5517d-152">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Uygulamanın çıktısını gösteren Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="5517d-154">Veri Gezgini’nde belgenizi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="5517d-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="5517d-155">Belgenizi Veri Gezgini’nde görmek için Azure portalına dönün.</span><span class="sxs-lookup"><span data-stu-id="5517d-155">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="5517d-156">Sol gezinti menüsünde **Veri Gezgini (Önizleme)** seçeneğine tıklayın, **golang-coach**, **paket** seçeneğini genişletin ve **Belgeler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-156">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="5517d-157">**Belgeler** sekmesinde \_id seçeneğine tıklayarak belgeyi sağ bölmede görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5517d-157">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![Yeni oluşturulan belgeyi görüntüleyen Veri Gezgini](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="5517d-159">Daha sonra belgeyle satır içi çalışabilir ve **Güncelleştir**’e tıklayarak belgeyi kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5517d-159">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="5517d-160">Belgeyi silme veya yeni belgeler ya da sorgular oluşturma seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="5517d-160">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="5517d-161">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="5517d-161">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="5517d-162">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="5517d-162">Clean up resources</span></span>

<span data-ttu-id="5517d-163">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu hızlı başlangıç tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="5517d-163">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="5517d-164">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-164">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="5517d-165">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5517d-165">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5517d-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5517d-166">Next steps</span></span>

<span data-ttu-id="5517d-167">Bu hızlı başlangıçta Azure Cosmos DB hesabı oluşturmayı ve MongoDB API’sini kullanarak bir Golang uygulamasını çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5517d-167">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="5517d-168">Şimdi Cosmos DB hesabınıza ek veri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5517d-168">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5517d-169">MongoDB API'si için Azure Cosmos DB’ye veri aktarma</span><span class="sxs-lookup"><span data-stu-id="5517d-169">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

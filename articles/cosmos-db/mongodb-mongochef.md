---
title: "Azure Cosmos DB MongoChef kullanın | Microsoft Docs"
description: "Bir Azure Cosmos DB ile MongoChef kullanmayı öğrenin: API MongoDB hesabı"
keywords: mongochef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="70321-104">Bir Azure Cosmos DB ile MongoChef kullanın: API MongoDB hesabı</span><span class="sxs-lookup"><span data-stu-id="70321-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="70321-105">Bir Azure Cosmos DB'ye bağlanmasına: API MongoDB hesabı için yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="70321-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="70321-106">İndirme ve yükleme [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="70321-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="70321-107">Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri</span><span class="sxs-lookup"><span data-stu-id="70321-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="70321-108">İçinde MongoChef bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70321-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="70321-109">Azure Cosmos DB eklemek için: API MongoDB hesabına MongoChef Bağlantı Yöneticisi için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="70321-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="70321-110">Azure Cosmos DB almak: API MongoDB bağlantı bilgilerini yönergeleri kullanarak [burada](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="70321-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="70321-112">Tıklatın **Bağlan** Bağlantı Yöneticisi'ni açmak için ardından **yeni bağlantı**</span><span class="sxs-lookup"><span data-stu-id="70321-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="70321-114">İçinde **yeni bağlantı** penceresi, **Server** sekmesinde, Azure Cosmos DB ana bilgisayar (FQDN) girin: API MongoDB hesabı ve bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="70321-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![MongoChef Bağlantı Yöneticisi'ni sunucu sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="70321-116">İçinde **yeni bağlantı** penceresi, **kimlik doğrulaması** sekmesinde, kimlik doğrulama modu seçin **standart (CR MONGODB veya SCARM-SHA-1)** ve kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="70321-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="70321-117">Varsayılan kimlik doğrulama db (Yönetici) kabul edin veya kendi değer sağlayın.</span><span class="sxs-lookup"><span data-stu-id="70321-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![MongoChef Bağlantı Yöneticisi kimlik doğrulaması sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="70321-119">İçinde **yeni bağlantı** penceresi, **SSL** sekmesi, onay **bağlanmak için SSL kullan Protokolü** onay kutusunu ve **sunucu otomatik olarak imzalanan SSL sertifikalarını kabul et**  radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70321-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![MongoChef Bağlantı Yöneticisi SSL sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="70321-121">Tıklatın **Bağlantıyı Sına** bağlantı bilgilerini doğrulamak için düğmesi **Tamam** yeni bağlantı penceresine geri dönün ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="70321-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![MongoChef test bağlantısı penceresinin ekran görüntüsü](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="70321-123">Bir veritabanı, koleksiyon ve belge oluşturmak için MongoChef kullanın</span><span class="sxs-lookup"><span data-stu-id="70321-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="70321-124">Bir veritabanı, koleksiyon ve MongoChef kullanarak belgeleri oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="70321-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="70321-125">İçinde **Bağlantı Yöneticisi**, bağlantı vurgulayıp **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="70321-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="70321-127">Konağı sağ tıklatın ve seçin **veritabanı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="70321-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="70321-128">Bir veritabanı adı girin ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70321-128">Provide a database name and click **OK**.</span></span>

    ![MongoChef veritabanı ekleme seçeneği ekran görüntüsü](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="70321-130">Veritabanını sağ tıklatın ve seçin **topluluk Ekle**.</span><span class="sxs-lookup"><span data-stu-id="70321-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="70321-131">Koleksiyon adı sağlayın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70321-131">Provide a collection name and click **Create**.</span></span>

    ![MongoChef topluluk Ekle seçeneğini ekran görüntüsü](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="70321-133">Tıklatın **koleksiyonu** menü öğesi, ardından **Belge Ekle**.</span><span class="sxs-lookup"><span data-stu-id="70321-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![MongoChef Belge Ekle menü öğesi ekran görüntüsü](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="70321-135">Belge Ekle iletişim kutusunda, aşağıdaki yapıştırın ve ardından **Belge Ekle**.</span><span class="sxs-lookup"><span data-stu-id="70321-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="70321-136">Başka bir belge, bu süre aşağıdaki içeriğe sahip ekleyin.</span><span class="sxs-lookup"><span data-stu-id="70321-136">Add another document, this time with the following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="70321-137">Bir örnek sorgu yürütün.</span><span class="sxs-lookup"><span data-stu-id="70321-137">Execute a sample query.</span></span> <span data-ttu-id="70321-138">Örneğin, ailesi Soyadı 'Andersen' ile arayın ve üst ve durum alanları döndürür.</span><span class="sxs-lookup"><span data-stu-id="70321-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Mongo Chef sorgu sonuçları ekran görüntüsü](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="70321-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="70321-140">Next steps</span></span>
* <span data-ttu-id="70321-141">Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="70321-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>

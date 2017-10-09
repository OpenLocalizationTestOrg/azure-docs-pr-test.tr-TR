---
title: aaaUse Azure Cosmos DB MongoChef | Microsoft Docs
description: "Bilgi nasıl toouse bir Azure Cosmos DB ile MongoChef: API MongoDB hesabı"
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
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="d6ed5-104">Bir Azure Cosmos DB ile MongoChef kullanın: API MongoDB hesabı</span><span class="sxs-lookup"><span data-stu-id="d6ed5-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="d6ed5-105">tooconnect tooan Azure Cosmos DB: API MongoDB hesabı için yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6ed5-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="d6ed5-106">İndirme ve yükleme [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="d6ed5-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="d6ed5-107">Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri</span><span class="sxs-lookup"><span data-stu-id="d6ed5-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="d6ed5-108">İçinde MongoChef Hello bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6ed5-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="d6ed5-109">tooadd Azure Cosmos DB: API Bağlantı Yöneticisi ' ni toohello MongoChef MongoDB hesabı için hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="d6ed5-110">Azure Cosmos DB almak: API MongoDB bağlantı bilgilerini hello yönergeleri kullanarak [burada](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="d6ed5-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Merhaba bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="d6ed5-112">Tıklatın **Bağlan** tooopen Bağlantı Yöneticisi hello ve ardından **yeni bağlantı**</span><span class="sxs-lookup"><span data-stu-id="d6ed5-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Merhaba MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="d6ed5-114">Merhaba, **yeni bağlantı** penceresinde hello **Server** sekmesinde, ana bilgisayar (FQDN) hello Azure Cosmos DB hello girin: API MongoDB hesabı ve başlangıç bağlantı noktası için.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Merhaba MongoChef Bağlantı Yöneticisi'ni sunucu sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="d6ed5-116">Merhaba, **yeni bağlantı** penceresinde hello **kimlik doğrulaması** sekmesinde, kimlik doğrulama modu seçin **standart (CR MONGODB veya SCARM-SHA-1)** ve hello kullanıcı adı girin ve PAROLA.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="d6ed5-117">Merhaba varsayılan kimlik doğrulama db (Yönetici) kabul edin veya kendi değer sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Merhaba MongoChef Bağlantı Yöneticisi kimlik doğrulaması sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="d6ed5-119">Merhaba, **yeni bağlantı** penceresinde hello **SSL** sekmesinde, hello denetleyin **SSL kullan Protokolü tooconnect** onay kutusunu ve hello **kabul sunucu otomatik olarak imzalanan SSL sertifikaları** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Merhaba MongoChef Bağlantı Yöneticisi SSL sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="d6ed5-121">Merhaba tıklatın **Bağlantıyı Sına** toovalidate hello bağlantı bilgilerini düğmesini tıklatın, **Tamam** tooreturn toohello yeni bağlantı penceresinde ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Merhaba MongoChef test bağlantısı penceresinin ekran görüntüsü](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="d6ed5-123">MongoChef toocreate bir veritabanı, koleksiyon ve belgeler kullanın</span><span class="sxs-lookup"><span data-stu-id="d6ed5-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="d6ed5-124">toocreate bir veritabanı, koleksiyon ve belgeleri MongoChef, kullanarak hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="d6ed5-125">İçinde **Bağlantı Yöneticisi**, hello bağlantı vurgulayıp **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Merhaba MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="d6ed5-127">Merhaba konağa sağ tıklayın ve seçin **veritabanı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="d6ed5-128">Bir veritabanı adı girin ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-128">Provide a database name and click **OK**.</span></span>

    ![Merhaba MongoChef veritabanı ekleme seçeneği ekran görüntüsü](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="d6ed5-130">Merhaba veritabanını sağ tıklatın ve seçin **topluluk Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="d6ed5-131">Koleksiyon adı sağlayın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-131">Provide a collection name and click **Create**.</span></span>

    ![Merhaba MongoChef topluluk Ekle seçeneği ekran görüntüsü](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="d6ed5-133">Merhaba tıklatın **koleksiyonu** menü öğesi, ardından **Belge Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Merhaba MongoChef Belge Ekle menü öğesi ekran görüntüsü](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="d6ed5-135">Merhaba aşağıdaki Hello Belge Ekle iletişim kutusuna yapıştırın ve ardından **Belge Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="d6ed5-136">Başka bir belge, bu kez içeriği aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="d6ed5-137">Bir örnek sorgu yürütün.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-137">Execute a sample query.</span></span> <span data-ttu-id="d6ed5-138">Örneğin, aileleri hello Soyadı 'Andersen', dönüş hello üst ve durum alanları arayın.</span><span class="sxs-lookup"><span data-stu-id="d6ed5-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Mongo Chef sorgu sonuçları ekran görüntüsü](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="d6ed5-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6ed5-140">Next steps</span></span>
* <span data-ttu-id="d6ed5-141">Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d6ed5-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>

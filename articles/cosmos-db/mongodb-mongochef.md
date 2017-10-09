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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Bir Azure Cosmos DB ile MongoChef kullanın: API MongoDB hesabı

tooconnect tooan Azure Cosmos DB: API MongoDB hesabı için yapmanız gerekir:

* İndirme ve yükleme [MongoChef](http://3t.io/mongochef)
* Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri

## <a name="create-hello-connection-in-mongochef"></a>İçinde MongoChef Hello bağlantısı oluşturma
tooadd Azure Cosmos DB: API Bağlantı Yöneticisi ' ni toohello MongoChef MongoDB hesabı için hello aşağıdaki adımları gerçekleştirin.

1. Azure Cosmos DB almak: API MongoDB bağlantı bilgilerini hello yönergeleri kullanarak [burada](connect-mongodb-account.md).

    ![Merhaba bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Tıklatın **Bağlan** tooopen Bağlantı Yöneticisi hello ve ardından **yeni bağlantı**

    ![Merhaba MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectionManager.png)
3. Merhaba, **yeni bağlantı** penceresinde hello **Server** sekmesinde, ana bilgisayar (FQDN) hello Azure Cosmos DB hello girin: API MongoDB hesabı ve başlangıç bağlantı noktası için.

    ![Merhaba MongoChef Bağlantı Yöneticisi'ni sunucu sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. Merhaba, **yeni bağlantı** penceresinde hello **kimlik doğrulaması** sekmesinde, kimlik doğrulama modu seçin **standart (CR MONGODB veya SCARM-SHA-1)** ve hello kullanıcı adı girin ve PAROLA.  Merhaba varsayılan kimlik doğrulama db (Yönetici) kabul edin veya kendi değer sağlayın.

    ![Merhaba MongoChef Bağlantı Yöneticisi kimlik doğrulaması sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. Merhaba, **yeni bağlantı** penceresinde hello **SSL** sekmesinde, hello denetleyin **SSL kullan Protokolü tooconnect** onay kutusunu ve hello **kabul sunucu otomatik olarak imzalanan SSL sertifikaları** radyo düğmesi.

    ![Merhaba MongoChef Bağlantı Yöneticisi SSL sekmesinin Ekran görüntüsü](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Merhaba tıklatın **Bağlantıyı Sına** toovalidate hello bağlantı bilgilerini düğmesini tıklatın, **Tamam** tooreturn toohello yeni bağlantı penceresinde ve ardından **kaydetmek**.

    ![Merhaba MongoChef test bağlantısı penceresinin ekran görüntüsü](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>MongoChef toocreate bir veritabanı, koleksiyon ve belgeler kullanın
toocreate bir veritabanı, koleksiyon ve belgeleri MongoChef, kullanarak hello aşağıdaki adımları gerçekleştirin.

1. İçinde **Bağlantı Yöneticisi**, hello bağlantı vurgulayıp **Bağlan**.

    ![Merhaba MongoChef Bağlantı Yöneticisi ekran görüntüsü](./media/mongodb-mongochef/ConnectToAccount.png)
2. Merhaba konağa sağ tıklayın ve seçin **veritabanı ekleme**.  Bir veritabanı adı girin ve tıklayın **Tamam**.

    ![Merhaba MongoChef veritabanı ekleme seçeneği ekran görüntüsü](./media/mongodb-mongochef/AddDatabase1.png)
3. Merhaba veritabanını sağ tıklatın ve seçin **topluluk Ekle**.  Koleksiyon adı sağlayın ve tıklatın **oluşturma**.

    ![Merhaba MongoChef topluluk Ekle seçeneği ekran görüntüsü](./media/mongodb-mongochef/AddCollection.png)
4. Merhaba tıklatın **koleksiyonu** menü öğesi, ardından **Belge Ekle**.

    ![Merhaba MongoChef Belge Ekle menü öğesi ekran görüntüsü](./media/mongodb-mongochef/AddDocument1.png)
5. Merhaba aşağıdaki Hello Belge Ekle iletişim kutusuna yapıştırın ve ardından **Belge Ekle**.

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
6. Başka bir belge, bu kez içeriği aşağıdaki hello ekleyin.

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
7. Bir örnek sorgu yürütün. Örneğin, aileleri hello Soyadı 'Andersen', dönüş hello üst ve durum alanları arayın.

    ![Mongo Chef sorgu sonuçları ekran görüntüsü](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Sonraki adımlar
* Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).

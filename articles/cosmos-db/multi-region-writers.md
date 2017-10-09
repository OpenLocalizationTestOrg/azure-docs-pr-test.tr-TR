---
title: "Azure Cosmos DB ile aaaMulti ana veritabanı mimarileri | Microsoft Docs"
description: "Yerel toodesign uygulama mimarilerindeki okur ve Azure Cosmos DB ile birden çok coğrafi bölgeler arasında Yazar hakkında bilgi edinin."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Birden çok ana veritabanı mimarileri Azure Cosmos DB ile genel çoğaltılan
Azure Cosmos DB destekleyen anahtar teslimi [genel çoğaltma](distribute-data-globally.md), olanak sağlayan düşük gecikmeli erişim hello iş yükünü başka bir yerindeki toodistribute veri toomultiple bölgeleri. Bu model yayımcı/tüketici iş yükleri için yaygın olarak kullanılan bir yazıcı tek bir coğrafi bölge içinde ve genel olarak dağıtılmış okuyucuları (okuma) diğer bölgelerdeki olduğu. 

İçinde yazarlar ve okuyucular genel olarak dağıtılan Azure Cosmos veritabanı genel çoğaltma destek toobuild uygulamalar da kullanabilirsiniz. Bu belgede Azure Cosmos DB kullanarak dağıtılmış yazarların yerel yazma ve yerel okuma erişimi elde sağlayan bir deseni açıklar.

## <a id="ExampleScenario"></a>İçerik Yayımlama - örnek bir senaryo
Gerçek dünya senaryosu toodescribe Genel dağıtılmış çok-region/çok-ana okuma yazma desenleri Azure Cosmos DB ile nasıl kullanabileceğiniz bakalım. Azure Cosmos DB'de yerleşik bir içerik yayımlama platform göz önünde bulundurun. Bu platform için harika kullanıcı deneyimi Yayımcılar ve tüketicileri için uyması gereken bazı gereksinimler şunlardır.

* Yazarlar ve abonelerin Merhaba Dünya yayılır 
* Yazarları (yazma) makaleleri tootheir yerel (en yakın) bölge yayımlamanız gerekir
* Yazarları okuyucular/Merhaba Dünya çapında dağıtılan aboneleri kendi makalelerin vardır. 
* Yeni makaleler yayımlandığında aboneleri bir bildirim almanız gerekir.
* Aboneler kendi yerel bölge mümkün tooread makalelerinden olması gerekir. Ayrıca mümkün tooadd incelemeler toothese makaleleri olması gerekir. 
* Herkes hello Yazar hello makalelerin dahil olmak üzere tüm incelemeleri ekli tooarticles yerel bölgesinden hello mümkün görünümü olmalıdır. 

Kullanıcıları ve yayımcılarına makaleler, milyarlarca ile milyonlarca varsayılarak tooconfront hello sorunları yere göre erişim güvence altına almak birlikte ölçeğin yakında sunuyoruz. Çoğu ölçeklenebilirlik sorunlar gibi iyi bir bölümleme stratejinize hello çözüm arasındadır. Ardından, şimdi nasıl toomodel makaleleri gözden ve bildirimleri belgeleri olarak Azure Cosmos DB hesaplarını yapılandırma sırasında arayın ve veri erişim katmanı uygulayın. 

Toolearn bölümlendirme ve bölüm anahtarları hakkında daha fazla bilgi isterseniz bkz [bölümlendirme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).

## <a id="ModelingNotifications"></a>Modelleme bildirimleri
Veri akışları belirli tooa kullanıcı bildirimleri var. Bu nedenle, hello erişimi desenleri bildirimleri belgeler için her zaman hello tek bir kullanıcı bağlamında alır. Örneğin, "bildirim tooa kullanıcı post" veya "belirli bir kullanıcı için tüm bildirimleri fetch". Bu nedenle, bu tür olacaktır için bölümlendirme anahtarı en iyi seçeneği hello `UserId`.

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a>Modelleme abonelikleri
Abonelikler, makalelerin ilgi alanı veya belirli bir yayımcı belirli bir kategorideki gibi çeşitli ölçütlerine oluşturulabilir. Bu nedenle hello `SubscriptionFilter` bölüm anahtarı için iyi bir seçimdir.

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <a id="ModelingArticles"></a>Modelleme makaleleri
Bir makale aracılığıyla bildirimleri tanımlandıktan sonra sonraki sorguları genellikle üzerinde hello dayalı `Article.Id`. Seçme `Article.Id` bölümü olarak hello anahtar nedenle makaleleri bir Azure Cosmos DB koleksiyonu içinde depolamak için en iyi dağıtım hello sağlar. 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a>Modelleme incelemeleri
Makaleler gibi incelemeler çoğunlukla yazılmış ve makale hello bağlamında okuyun. Seçme `ArticleId` bir bölümü olarak anahtar en iyi dağıtım ve makalesiyle ilişkilendirilen incelemeleri, etkili erişim sağlar. 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <a id="DataAccessMethods"></a>Veri erişim katmanı yöntemleri
Şimdi hello ana veri erişim yöntemleri tooimplement ihtiyacımız bakalım. Merhaba yöntemlerin listesi hello işte `ContentPublishDatabase` gerekir:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Azure Cosmos DB hesabı yapılandırması
tooguarantee yerel okuma ve yazma, biz yalnızca bölüm anahtarı verileri bölüm gerekir, ancak ayrıca bölgelere hello coğrafi erişimi deseni temel alınarak. bir coğrafi olarak çoğaltılmış Azure Cosmos DB veritabanı hesabı her bölge için sahip Hello modeli kullanır. Örneğin, iki bölgede ile İşte bir kurulum bölgeli yazmalar için:

| Hesap Adı | Bölge yazma | Okuma bölge |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Merhaba Aşağıdaki diyagramda okuma ve yazma işlemleri bu kurulum ile tipik bir uygulamada nasıl gerçekleştirilir gösterilmektedir:

![Azure Cosmos DB birden çok yöneticili mimarisi](./media/multi-region-writers/multi-master.png)

Nasıl tooinitialize hello hello çalıştıran bir DAL istemcileri gösteren bir kod parçacığı aşağıda verilmiştir `West US` bölge.
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

Kurulum önceki hello ile tüm yazma toohello yerel hesap dağıtıldığı üzerinde temel hello veri erişim katmanı iletebilirsiniz. Okuma hesapları hem tooget hello genel görünüm veri okunurken tarafından gerçekleştirilir. Bu yaklaşım olabilir tooas gerektiği gibi birçok bölgeler genişletilmiş. Örneğin, üç coğrafi bölgeler Kurulum'a şöyledir:

| Hesap Adı | Bölge yazma | Bölge 1 okuma | Bölge 2 okuma |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Veri erişim katmanı uygulaması
Şimdi iki yazılabilir bölgeleri ile bir uygulama için hello veri erişim katmanı (DAL) hello uyarlamasını bakalım. Merhaba DAL hello aşağıdaki adımları uygulamanız gerekir:

* Birden çok örneğini oluşturma `DocumentClient` her hesap için. İki bölgede ile her DAL örneği varsa `writeClient` ve bir `readClient`. 
* Merhaba uygulaması dağıtılan hello bölgeyi temel alan, hello uç noktaları için yapılandırma `writeclient` ve `readClient`. Merhaba DAL Örneğin, dağıtılmış `West US` kullanan `contentpubdatabase-usa.documents.azure.com` yazma işlemlerini gerçekleştirme. Merhaba DAL dağıtılan `NorthEurope` kullanan `contentpubdatabase-europ.documents.azure.com` yazmalar için.

Kurulum önceki hello ile Merhaba veri erişimi yöntemleri uygulanabilir. Yazma işlemleri iletmek hello yazma toohello karşılık gelen `writeClient`.

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

Bildirimleri ve incelemeler okumak için bölgeler hem birleşim hello sonuçları hello aşağıdaki kod parçacığında gösterildiği gibi okumanız gerekir:

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

Bu nedenle, bir iyi bölümleme anahtar ve hesap tabanlı statik bölümleme seçerek, bölgeli yerel yazma ve okuma Azure Cosmos DB kullanarak elde edebilirsiniz.

## <a id="NextSteps"></a>Sonraki adımlar
Bu makalede, Azure Cosmos Örnek senaryo olarak içerik yayımlama kullanarak DB ile genel dağıtılmış bölgeli okuma yazma desenleri nasıl kullanabileceğiniz açıklanmaktadır.

* Azure Cosmos DB nasıl desteklediği hakkında bilgi edinin [genel dağıtım](distribute-data-globally.md)
* Hakkında bilgi edinin [Azure Cosmos veritabanı otomatik ve el ile yük devretme](regional-failover.md)
* Hakkında bilgi edinin [Azure Cosmos DB ile genel tutarlılık](consistency-levels.md)
* Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)
* Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)
* Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - tablo API](tutorial-global-distribution-table.md)

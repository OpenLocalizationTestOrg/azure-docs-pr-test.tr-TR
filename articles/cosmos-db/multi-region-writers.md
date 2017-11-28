---
title: "Azure Cosmos DB ile birden çok ana veritabanı mimarileri | Microsoft Docs"
description: "Azure Cosmos DB ile birden çok coğrafi bölgeler arasında yerel okuma ve yazma işlemleri ile uygulama Mimari Tasarım hakkında bilgi edinin."
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="ed116-103">Birden çok ana veritabanı mimarileri Azure Cosmos DB ile genel çoğaltılan</span><span class="sxs-lookup"><span data-stu-id="ed116-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="ed116-104">Azure Cosmos DB destekleyen anahtar teslimi [genel çoğaltma](distribute-data-globally.md), iş yükünü başka bir yerindeki düşük gecikme süresi erişimi olan birden çok bölgeye verilerini dağıtmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed116-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="ed116-105">Bu model yayımcı/tüketici iş yükleri için yaygın olarak kullanılan bir yazıcı tek bir coğrafi bölge içinde ve genel olarak dağıtılmış okuyucuları (okuma) diğer bölgelerdeki olduğu.</span><span class="sxs-lookup"><span data-stu-id="ed116-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="ed116-106">İçinde yazarlar ve okuyucular genel olarak dağıtılan uygulamaları geliştirmek için Azure Cosmos DB'ın genel çoğaltma desteği de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed116-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="ed116-107">Bu belgede Azure Cosmos DB kullanarak dağıtılmış yazarların yerel yazma ve yerel okuma erişimi elde sağlayan bir deseni açıklar.</span><span class="sxs-lookup"><span data-stu-id="ed116-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="ed116-108"><a id="ExampleScenario"></a>İçerik Yayımlama - örnek bir senaryo</span><span class="sxs-lookup"><span data-stu-id="ed116-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="ed116-109">Genel olarak dağıtılmış çok-region/çok-ana okuma yazma desenleri Azure Cosmos DB ile nasıl kullanabileceğiniz açıklamak için gerçek dünya senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="ed116-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="ed116-110">Azure Cosmos DB'de yerleşik bir içerik yayımlama platform göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ed116-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="ed116-111">Bu platform için harika kullanıcı deneyimi Yayımcılar ve tüketicileri için uyması gereken bazı gereksinimler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ed116-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="ed116-112">Yazarlar ve abonelerin world yayılır</span><span class="sxs-lookup"><span data-stu-id="ed116-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="ed116-113">Yazarlar kendi yerel (en yakın) bölgesine (yazma) makaleleri yayımlamanız gerekir</span><span class="sxs-lookup"><span data-stu-id="ed116-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="ed116-114">Yazarları okuyucular/dünya çapında dağıtılan aboneleri kendi makalelerin vardır.</span><span class="sxs-lookup"><span data-stu-id="ed116-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="ed116-115">Yeni makaleler yayımlandığında aboneleri bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed116-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="ed116-116">Aboneler kendi yerel bölgesinden makaleleri okuyabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed116-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="ed116-117">Bunlar ayrıca bu makaleler incelemeler eklemeniz mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed116-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="ed116-118">Herkes makaleleri yazarı dahil olmak üzere tüm değerlendirmeleri makaleler için yerel bir bölgesinden bağlı mümkün görünümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed116-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="ed116-119">Kullanıcıları ve yayımcılarına makaleler, milyarlarca ile milyonlarca varsayılarak yakında biz yere göre erişim güvence altına almak birlikte ölçeği sorunları üstesinden gelir gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed116-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="ed116-120">Çoğu ölçeklenebilirlik sorunları olduğu gibi ile iyi bölümleme stratejisine içinde çözüm arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ed116-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="ed116-121">Ardından, makaleler, gözden geçirme ve bildirimleri belgeleri olarak model, Azure Cosmos DB hesaplarını yapılandırın ve veri erişim katmanı uygulama ne bakalım.</span><span class="sxs-lookup"><span data-stu-id="ed116-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="ed116-122">Bölümlendirme ve bölüm anahtarları hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [bölümlendirme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="ed116-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="ed116-123"><a id="ModelingNotifications"></a>Modelleme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="ed116-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="ed116-124">Bildirimler, bir kullanıcı için belirli veri akışları ' dir.</span><span class="sxs-lookup"><span data-stu-id="ed116-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="ed116-125">Bu nedenle, bildirimler belgeler için erişim düzenlerini her zaman tek bir kullanıcı bağlamında olur.</span><span class="sxs-lookup"><span data-stu-id="ed116-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="ed116-126">Örneğin, "bir kullanıcıya bir bildirim post" veya "belirli bir kullanıcı için tüm bildirimleri fetch".</span><span class="sxs-lookup"><span data-stu-id="ed116-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="ed116-127">Bu nedenle, bu türü için anahtar bölümlendirme, en iyi seçenek olacaktır `UserId`.</span><span class="sxs-lookup"><span data-stu-id="ed116-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="ed116-128"><a id="ModelingSubscriptions"></a>Modelleme abonelikleri</span><span class="sxs-lookup"><span data-stu-id="ed116-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="ed116-129">Abonelikler, makalelerin ilgi alanı veya belirli bir yayımcı belirli bir kategorideki gibi çeşitli ölçütlerine oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="ed116-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="ed116-130">Bu nedenle `SubscriptionFilter` bölüm anahtarı için iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="ed116-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="ed116-131"><a id="ModelingArticles"></a>Modelleme makaleleri</span><span class="sxs-lookup"><span data-stu-id="ed116-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="ed116-132">Bir makale aracılığıyla bildirimleri tanımlandıktan sonra sonraki sorguları genellikle temel alan `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="ed116-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="ed116-133">Seçme `Article.Id` bölümü olarak anahtar nedenle makaleleri bir Azure Cosmos DB koleksiyonu içinde depolamak için en iyi dağıtım sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed116-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="ed116-134"><a id="ModelingReviews"></a>Modelleme incelemeleri</span><span class="sxs-lookup"><span data-stu-id="ed116-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="ed116-135">Makaleler gibi incelemeler çoğunlukla yazılmış ve makale bağlamında okuyun.</span><span class="sxs-lookup"><span data-stu-id="ed116-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="ed116-136">Seçme `ArticleId` bir bölümü olarak anahtar en iyi dağıtım ve makalesiyle ilişkilendirilen incelemeleri, etkili erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed116-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="ed116-137"><a id="DataAccessMethods"></a>Veri erişim katmanı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="ed116-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="ed116-138">Şimdi ana veri erişim yöntemleri uygulamak için ihtiyacımız bakalım.</span><span class="sxs-lookup"><span data-stu-id="ed116-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="ed116-139">Yöntemlerin listesi İşte, `ContentPublishDatabase` gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed116-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="ed116-140"><a id="Architecture"></a>Azure Cosmos DB hesabı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed116-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="ed116-141">Yerel okuma ve yazma, bölüm gerekir güvence altına almak için veri bölüme anahtar, ancak ayrıca temel alınarak coğrafi erişim desenini bölgeleri tam değil.</span><span class="sxs-lookup"><span data-stu-id="ed116-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="ed116-142">Model bir coğrafi olarak çoğaltılmış Azure Cosmos DB veritabanı hesabı her bölge için sahip kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed116-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="ed116-143">Örneğin, iki bölgede ile İşte bir kurulum bölgeli yazmalar için:</span><span class="sxs-lookup"><span data-stu-id="ed116-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="ed116-144">Hesap adı</span><span class="sxs-lookup"><span data-stu-id="ed116-144">Account Name</span></span> | <span data-ttu-id="ed116-145">Bölge yazma</span><span class="sxs-lookup"><span data-stu-id="ed116-145">Write Region</span></span> | <span data-ttu-id="ed116-146">Okuma bölge</span><span class="sxs-lookup"><span data-stu-id="ed116-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="ed116-147">Aşağıdaki diyagramda, okuma ve yazma işlemleri bu kurulum ile tipik bir uygulamada nasıl gerçekleştirilir gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ed116-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB birden çok yöneticili mimarisi](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="ed116-149">Nasıl çalışır durumda bir DAL istemcilere başlatılacağını gösteren bir kod parçacığı aşağıda verilmiştir `West US` bölge.</span><span class="sxs-lookup"><span data-stu-id="ed116-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="ed116-150">Önceki kurulum ile veri erişim katmanı dağıtıldığı üzerinde dayalı yerel hesap tüm yazma işlemlerini iletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed116-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="ed116-151">Okuma okunurken verilerin genel görünümünü almak için her iki hesap tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ed116-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="ed116-152">Bu yaklaşım, gerektiği kadar bölgeler için genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed116-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="ed116-153">Örneğin, üç coğrafi bölgeler Kurulum'a şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ed116-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="ed116-154">Hesap adı</span><span class="sxs-lookup"><span data-stu-id="ed116-154">Account Name</span></span> | <span data-ttu-id="ed116-155">Bölge yazma</span><span class="sxs-lookup"><span data-stu-id="ed116-155">Write Region</span></span> | <span data-ttu-id="ed116-156">Bölge 1 okuma</span><span class="sxs-lookup"><span data-stu-id="ed116-156">Read Region 1</span></span> | <span data-ttu-id="ed116-157">Bölge 2 okuma</span><span class="sxs-lookup"><span data-stu-id="ed116-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="ed116-158"><a id="DataAccessImplementation"></a>Veri erişim katmanı uygulaması</span><span class="sxs-lookup"><span data-stu-id="ed116-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="ed116-159">Şimdi iki yazılabilir bölgeleri ile bir uygulama için veri erişim katmanı (DAL) uyarlamasını bakalım.</span><span class="sxs-lookup"><span data-stu-id="ed116-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="ed116-160">DAL, aşağıdaki adımları uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed116-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="ed116-161">Birden çok örneğini oluşturma `DocumentClient` her hesap için.</span><span class="sxs-lookup"><span data-stu-id="ed116-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="ed116-162">İki bölgede ile her DAL örneği varsa `writeClient` ve bir `readClient`.</span><span class="sxs-lookup"><span data-stu-id="ed116-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="ed116-163">Uygulama dağıtılan bölgeyi temel alan, uç noktaları için yapılandırma `writeclient` ve `readClient`.</span><span class="sxs-lookup"><span data-stu-id="ed116-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="ed116-164">DAL Örneğin, dağıtılmış `West US` kullanan `contentpubdatabase-usa.documents.azure.com` yazma işlemlerini gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="ed116-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="ed116-165">DAL dağıtılmış `NorthEurope` kullanan `contentpubdatabase-europ.documents.azure.com` yazmalar için.</span><span class="sxs-lookup"><span data-stu-id="ed116-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="ed116-166">Önceki Kurulum'a veri erişimi yöntemleri uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ed116-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="ed116-167">Karşılık gelen yazma işlemleri iletmek yazma `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="ed116-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="ed116-168">Bildirimler ve incelemeler okumak için bölgeler hem UNION sonuçları aşağıdaki kod parçacığında gösterildiği gibi okumanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed116-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="ed116-169">Bu nedenle, bir iyi bölümleme anahtar ve hesap tabanlı statik bölümleme seçerek, bölgeli yerel yazma ve okuma Azure Cosmos DB kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed116-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="ed116-170"><a id="NextSteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed116-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="ed116-171">Bu makalede, Azure Cosmos Örnek senaryo olarak içerik yayımlama kullanarak DB ile genel dağıtılmış bölgeli okuma yazma desenleri nasıl kullanabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ed116-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="ed116-172">Azure Cosmos DB nasıl desteklediği hakkında bilgi edinin [genel dağıtım](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="ed116-173">Hakkında bilgi edinin [Azure Cosmos veritabanı otomatik ve el ile yük devretme](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="ed116-174">Hakkında bilgi edinin [Azure Cosmos DB ile genel tutarlılık](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="ed116-175">Kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="ed116-176">Kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="ed116-177">Kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - tablo API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="ed116-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>

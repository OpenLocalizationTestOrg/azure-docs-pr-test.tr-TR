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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="eb78b-103">Birden çok ana veritabanı mimarileri Azure Cosmos DB ile genel çoğaltılan</span><span class="sxs-lookup"><span data-stu-id="eb78b-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="eb78b-104">Azure Cosmos DB destekleyen anahtar teslimi [genel çoğaltma](distribute-data-globally.md), olanak sağlayan düşük gecikmeli erişim hello iş yükünü başka bir yerindeki toodistribute veri toomultiple bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="eb78b-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="eb78b-105">Bu model yayımcı/tüketici iş yükleri için yaygın olarak kullanılan bir yazıcı tek bir coğrafi bölge içinde ve genel olarak dağıtılmış okuyucuları (okuma) diğer bölgelerdeki olduğu.</span><span class="sxs-lookup"><span data-stu-id="eb78b-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="eb78b-106">İçinde yazarlar ve okuyucular genel olarak dağıtılan Azure Cosmos veritabanı genel çoğaltma destek toobuild uygulamalar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb78b-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="eb78b-107">Bu belgede Azure Cosmos DB kullanarak dağıtılmış yazarların yerel yazma ve yerel okuma erişimi elde sağlayan bir deseni açıklar.</span><span class="sxs-lookup"><span data-stu-id="eb78b-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="eb78b-108"><a id="ExampleScenario"></a>İçerik Yayımlama - örnek bir senaryo</span><span class="sxs-lookup"><span data-stu-id="eb78b-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="eb78b-109">Gerçek dünya senaryosu toodescribe Genel dağıtılmış çok-region/çok-ana okuma yazma desenleri Azure Cosmos DB ile nasıl kullanabileceğiniz bakalım.</span><span class="sxs-lookup"><span data-stu-id="eb78b-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="eb78b-110">Azure Cosmos DB'de yerleşik bir içerik yayımlama platform göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eb78b-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="eb78b-111">Bu platform için harika kullanıcı deneyimi Yayımcılar ve tüketicileri için uyması gereken bazı gereksinimler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="eb78b-112">Yazarlar ve abonelerin Merhaba Dünya yayılır</span><span class="sxs-lookup"><span data-stu-id="eb78b-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="eb78b-113">Yazarları (yazma) makaleleri tootheir yerel (en yakın) bölge yayımlamanız gerekir</span><span class="sxs-lookup"><span data-stu-id="eb78b-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="eb78b-114">Yazarları okuyucular/Merhaba Dünya çapında dağıtılan aboneleri kendi makalelerin vardır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="eb78b-115">Yeni makaleler yayımlandığında aboneleri bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="eb78b-116">Aboneler kendi yerel bölge mümkün tooread makalelerinden olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="eb78b-117">Ayrıca mümkün tooadd incelemeler toothese makaleleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="eb78b-118">Herkes hello Yazar hello makalelerin dahil olmak üzere tüm incelemeleri ekli tooarticles yerel bölgesinden hello mümkün görünümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="eb78b-119">Kullanıcıları ve yayımcılarına makaleler, milyarlarca ile milyonlarca varsayılarak tooconfront hello sorunları yere göre erişim güvence altına almak birlikte ölçeğin yakında sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="eb78b-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="eb78b-120">Çoğu ölçeklenebilirlik sorunlar gibi iyi bir bölümleme stratejinize hello çözüm arasındadır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="eb78b-121">Ardından, şimdi nasıl toomodel makaleleri gözden ve bildirimleri belgeleri olarak Azure Cosmos DB hesaplarını yapılandırma sırasında arayın ve veri erişim katmanı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eb78b-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="eb78b-122">Toolearn bölümlendirme ve bölüm anahtarları hakkında daha fazla bilgi isterseniz bkz [bölümlendirme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="eb78b-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="eb78b-123"><a id="ModelingNotifications"></a>Modelleme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="eb78b-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="eb78b-124">Veri akışları belirli tooa kullanıcı bildirimleri var.</span><span class="sxs-lookup"><span data-stu-id="eb78b-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="eb78b-125">Bu nedenle, hello erişimi desenleri bildirimleri belgeler için her zaman hello tek bir kullanıcı bağlamında alır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="eb78b-126">Örneğin, "bildirim tooa kullanıcı post" veya "belirli bir kullanıcı için tüm bildirimleri fetch".</span><span class="sxs-lookup"><span data-stu-id="eb78b-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="eb78b-127">Bu nedenle, bu tür olacaktır için bölümlendirme anahtarı en iyi seçeneği hello `UserId`.</span><span class="sxs-lookup"><span data-stu-id="eb78b-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

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

## <span data-ttu-id="eb78b-128"><a id="ModelingSubscriptions"></a>Modelleme abonelikleri</span><span class="sxs-lookup"><span data-stu-id="eb78b-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="eb78b-129">Abonelikler, makalelerin ilgi alanı veya belirli bir yayımcı belirli bir kategorideki gibi çeşitli ölçütlerine oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="eb78b-130">Bu nedenle hello `SubscriptionFilter` bölüm anahtarı için iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="eb78b-131"><a id="ModelingArticles"></a>Modelleme makaleleri</span><span class="sxs-lookup"><span data-stu-id="eb78b-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="eb78b-132">Bir makale aracılığıyla bildirimleri tanımlandıktan sonra sonraki sorguları genellikle üzerinde hello dayalı `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="eb78b-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="eb78b-133">Seçme `Article.Id` bölümü olarak hello anahtar nedenle makaleleri bir Azure Cosmos DB koleksiyonu içinde depolamak için en iyi dağıtım hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb78b-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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

## <span data-ttu-id="eb78b-134"><a id="ModelingReviews"></a>Modelleme incelemeleri</span><span class="sxs-lookup"><span data-stu-id="eb78b-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="eb78b-135">Makaleler gibi incelemeler çoğunlukla yazılmış ve makale hello bağlamında okuyun.</span><span class="sxs-lookup"><span data-stu-id="eb78b-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="eb78b-136">Seçme `ArticleId` bir bölümü olarak anahtar en iyi dağıtım ve makalesiyle ilişkilendirilen incelemeleri, etkili erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb78b-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

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

## <span data-ttu-id="eb78b-137"><a id="DataAccessMethods"></a>Veri erişim katmanı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="eb78b-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="eb78b-138">Şimdi hello ana veri erişim yöntemleri tooimplement ihtiyacımız bakalım.</span><span class="sxs-lookup"><span data-stu-id="eb78b-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="eb78b-139">Merhaba yöntemlerin listesi hello işte `ContentPublishDatabase` gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb78b-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="eb78b-140"><a id="Architecture"></a>Azure Cosmos DB hesabı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="eb78b-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="eb78b-141">tooguarantee yerel okuma ve yazma, biz yalnızca bölüm anahtarı verileri bölüm gerekir, ancak ayrıca bölgelere hello coğrafi erişimi deseni temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="eb78b-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="eb78b-142">bir coğrafi olarak çoğaltılmış Azure Cosmos DB veritabanı hesabı her bölge için sahip Hello modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="eb78b-143">Örneğin, iki bölgede ile İşte bir kurulum bölgeli yazmalar için:</span><span class="sxs-lookup"><span data-stu-id="eb78b-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="eb78b-144">Hesap Adı</span><span class="sxs-lookup"><span data-stu-id="eb78b-144">Account Name</span></span> | <span data-ttu-id="eb78b-145">Bölge yazma</span><span class="sxs-lookup"><span data-stu-id="eb78b-145">Write Region</span></span> | <span data-ttu-id="eb78b-146">Okuma bölge</span><span class="sxs-lookup"><span data-stu-id="eb78b-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="eb78b-147">Merhaba Aşağıdaki diyagramda okuma ve yazma işlemleri bu kurulum ile tipik bir uygulamada nasıl gerçekleştirilir gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eb78b-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB birden çok yöneticili mimarisi](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="eb78b-149">Nasıl tooinitialize hello hello çalıştıran bir DAL istemcileri gösteren bir kod parçacığı aşağıda verilmiştir `West US` bölge.</span><span class="sxs-lookup"><span data-stu-id="eb78b-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
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

<span data-ttu-id="eb78b-150">Kurulum önceki hello ile tüm yazma toohello yerel hesap dağıtıldığı üzerinde temel hello veri erişim katmanı iletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb78b-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="eb78b-151">Okuma hesapları hem tooget hello genel görünüm veri okunurken tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="eb78b-152">Bu yaklaşım olabilir tooas gerektiği gibi birçok bölgeler genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="eb78b-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="eb78b-153">Örneğin, üç coğrafi bölgeler Kurulum'a şöyledir:</span><span class="sxs-lookup"><span data-stu-id="eb78b-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="eb78b-154">Hesap Adı</span><span class="sxs-lookup"><span data-stu-id="eb78b-154">Account Name</span></span> | <span data-ttu-id="eb78b-155">Bölge yazma</span><span class="sxs-lookup"><span data-stu-id="eb78b-155">Write Region</span></span> | <span data-ttu-id="eb78b-156">Bölge 1 okuma</span><span class="sxs-lookup"><span data-stu-id="eb78b-156">Read Region 1</span></span> | <span data-ttu-id="eb78b-157">Bölge 2 okuma</span><span class="sxs-lookup"><span data-stu-id="eb78b-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="eb78b-158"><a id="DataAccessImplementation"></a>Veri erişim katmanı uygulaması</span><span class="sxs-lookup"><span data-stu-id="eb78b-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="eb78b-159">Şimdi iki yazılabilir bölgeleri ile bir uygulama için hello veri erişim katmanı (DAL) hello uyarlamasını bakalım.</span><span class="sxs-lookup"><span data-stu-id="eb78b-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="eb78b-160">Merhaba DAL hello aşağıdaki adımları uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb78b-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="eb78b-161">Birden çok örneğini oluşturma `DocumentClient` her hesap için.</span><span class="sxs-lookup"><span data-stu-id="eb78b-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="eb78b-162">İki bölgede ile her DAL örneği varsa `writeClient` ve bir `readClient`.</span><span class="sxs-lookup"><span data-stu-id="eb78b-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="eb78b-163">Merhaba uygulaması dağıtılan hello bölgeyi temel alan, hello uç noktaları için yapılandırma `writeclient` ve `readClient`.</span><span class="sxs-lookup"><span data-stu-id="eb78b-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="eb78b-164">Merhaba DAL Örneğin, dağıtılmış `West US` kullanan `contentpubdatabase-usa.documents.azure.com` yazma işlemlerini gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="eb78b-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="eb78b-165">Merhaba DAL dağıtılan `NorthEurope` kullanan `contentpubdatabase-europ.documents.azure.com` yazmalar için.</span><span class="sxs-lookup"><span data-stu-id="eb78b-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="eb78b-166">Kurulum önceki hello ile Merhaba veri erişimi yöntemleri uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="eb78b-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="eb78b-167">Yazma işlemleri iletmek hello yazma toohello karşılık gelen `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="eb78b-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

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

<span data-ttu-id="eb78b-168">Bildirimleri ve incelemeler okumak için bölgeler hem birleşim hello sonuçları hello aşağıdaki kod parçacığında gösterildiği gibi okumanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb78b-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

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

<span data-ttu-id="eb78b-169">Bu nedenle, bir iyi bölümleme anahtar ve hesap tabanlı statik bölümleme seçerek, bölgeli yerel yazma ve okuma Azure Cosmos DB kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb78b-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="eb78b-170"><a id="NextSteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb78b-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="eb78b-171">Bu makalede, Azure Cosmos Örnek senaryo olarak içerik yayımlama kullanarak DB ile genel dağıtılmış bölgeli okuma yazma desenleri nasıl kullanabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eb78b-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="eb78b-172">Azure Cosmos DB nasıl desteklediği hakkında bilgi edinin [genel dağıtım](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="eb78b-173">Hakkında bilgi edinin [Azure Cosmos veritabanı otomatik ve el ile yük devretme](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="eb78b-174">Hakkında bilgi edinin [Azure Cosmos DB ile genel tutarlılık](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="eb78b-175">Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="eb78b-176">Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="eb78b-177">Hello kullanarak birden fazla bölge ile geliştirme [Azure Cosmos DB - tablo API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="eb78b-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>

---
title: "Azure akış Analizi ile aaaReal zamanı Twitter düşünceleri çözümleme | Microsoft Docs"
description: "Bilgi nasıl toouse Stream Analytics gerçek zamanlı Twitter düşünceleri çözümleme için. Olay oluşturma toodata canlı bir Pano üzerinde Adım Adım Kılavuzu."
keywords: "gerçek zamanlı twitter eğilim analizi, düşünceleri analiz, sosyal medya analizi, eğilim analizi örneği"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="0930b-105">Azure Stream Analytics gerçek zamanlı Twitter düşünceleri analizi</span><span class="sxs-lookup"><span data-stu-id="0930b-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="0930b-106">Bilgi nasıl toobuild düşünceleri analiz çözümü gerçek zamanlı getiren tarafından sosyal medya analizi için Twitter olayları Azure Event Hubs'a.</span><span class="sxs-lookup"><span data-stu-id="0930b-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="0930b-107">Bir Azure akış analizi sorgu tooanalyze hello veri ve iki depoda hello sonuçlar daha sonra kullanmak için veya bir Pano kullanın sonra yazma ve [Power BI](https://powerbi.com/) tooprovide Öngörüler gerçek zamanlı.</span><span class="sxs-lookup"><span data-stu-id="0930b-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="0930b-108">Sosyal medya analiz araçları, kuruluşların oluşturan eğilim konularını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0930b-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="0930b-109">Konular ve sosyal medya içinde postaları hacmi yüksek olan alışkanlıklarınızı bunun oluşturan eğilim konulardır.</span><span class="sxs-lookup"><span data-stu-id="0930b-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="0930b-110">Olarak da adlandırılır düşünceleri analiz *fikir araştırma*, sosyal medya analizi araçları toodetermine alışkanlıklarınızı ürün, fikir ve benzeri doğru kullanır.</span><span class="sxs-lookup"><span data-stu-id="0930b-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="0930b-111">Gerçek zamanlı Twitter eğilim analizi hello diyez abonelik modeli toolisten toospecific anahtar sözcükler (diyez etiketlerini) sağladığından harika bir analiz Aracı'nın bir örnektir ve akış hello düşünceleri analizini geliştirin.</span><span class="sxs-lookup"><span data-stu-id="0930b-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="0930b-112">Senaryo: Sosyal medya düşünceleri gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="0930b-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="0930b-113">Bir haber medya Web sitesi olan bir şirket rakiplere üzerinde bir avantaj hemen ilgili tooits okuyucular olduğu site içeriğin bulunduğu tarafından sağlamasını ilgileniyor.</span><span class="sxs-lookup"><span data-stu-id="0930b-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="0930b-114">Hello şirket Twitter veri analizini gerçek zamanlı düşünceleri yaparak ilgili tooreaders olan konularda sosyal medya çözümlemesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0930b-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="0930b-115">Twitter'da, gerçek zamanlı tooidentify oluşturan eğilim konuları şirket gereksinimlerini gerçek zamanlı analiz hello tweet birim ve önemli konular için düşünceleri hakkında hello.</span><span class="sxs-lookup"><span data-stu-id="0930b-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="0930b-116">Diğer bir deyişle, hello gerek akış bu sosyal medya üzerinde temel alan bir düşünceleri analiz analytics altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="0930b-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0930b-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0930b-117">Prerequisites</span></span>
<span data-ttu-id="0930b-118">Bu öğreticide, tooTwitter bağlanır ve (hangi ayarlayabileceğiniz) belirli diyez etiketlerini sahip tweet'leri benzeyen bir istemci uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="0930b-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="0930b-119">Sırayla toorun uygulama hello ve analiz hello Azure akış analizi kullanarak tweet'leri hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0930b-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="0930b-120">Bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="0930b-120">An Azure subscription</span></span>
* <span data-ttu-id="0930b-121">Bir Twitter hesabı</span><span class="sxs-lookup"><span data-stu-id="0930b-121">A Twitter account</span></span> 
* <span data-ttu-id="0930b-122">Bir Twitter uygulama ve hello [OAuth erişim belirtecinin](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) bu uygulama için.</span><span class="sxs-lookup"><span data-stu-id="0930b-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="0930b-123">Üst düzey hakkında yönergeler sağlıyoruz toocreate Twitter uygulamayı daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0930b-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="0930b-124">Merhaba Twitter okur Merhaba TwitterWPFClient uygulaması akış.</span><span class="sxs-lookup"><span data-stu-id="0930b-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="0930b-125">tooget bu uygulama, yükleme hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) dosya Github'dan ve bilgisayarınızdaki bir klasöre hello paketin sıkıştırmasını.</span><span class="sxs-lookup"><span data-stu-id="0930b-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="0930b-126">Toosee hello kaynak kodu istediğiniz ve bir hata ayıklayıcıda Merhaba uygulaması Çalıştır hello kaynak kodundan alabilir [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="0930b-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="0930b-127">Bir event hub'akış analizi girişi için oluşturma</span><span class="sxs-lookup"><span data-stu-id="0930b-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="0930b-128">Merhaba örnek uygulaması olaylar oluşturur ve bunları tooan Azure olay hub'ı iter.</span><span class="sxs-lookup"><span data-stu-id="0930b-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="0930b-129">Azure event hubs'a akış analizi için olay alım hello tercih edilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="0930b-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="0930b-130">Daha fazla bilgi için bkz: Merhaba [Azure Event Hubs belgelerine](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0930b-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="0930b-131">Bir olay hub'ad alanı ve olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="0930b-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="0930b-132">Bu yordam, önce bir olay hub'ad alanı oluşturun ve ardından bir olay hub'ı toothat ad alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0930b-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="0930b-133">Olay hub'ı ad alanları kullanılır toologically grubunun ilişkili olay bus örnekleri.</span><span class="sxs-lookup"><span data-stu-id="0930b-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="0930b-134">Oturum toohello Azure portal ve tıklatın **yeni** > **nesnelerin interneti** > **olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="0930b-135">Merhaba, **ad alanı oluşturma** dikey penceresinde gibi bir ad alanı adı girin `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="0930b-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="0930b-136">Merhaba ad alanı için herhangi bir ad kullanabilirsiniz, ancak hello adı geçerli bir URL olmalıdır ve Azure arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="0930b-137">Bir aboneliği seçin ve oluşturmak veya bir kaynak grubu seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0930b-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Bir olay hub'ad alanı oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="0930b-139">Merhaba ad alanı dağıtmayı bitirdiğinde hello olay hub'ad alanı, Azure kaynak listesinde bulun.</span><span class="sxs-lookup"><span data-stu-id="0930b-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="0930b-140">Merhaba yeni ad alanına tıklayın ve hello ad alanı dikey penceresinde tıklayın  **+ &nbsp;olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="0930b-141">Yeni bir olay hub'ı oluşturmak için hello Event Hub'ı Ekle düğmesi</span><span class="sxs-lookup"><span data-stu-id="0930b-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="0930b-142">Ad hello yeni olay hub'ı `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="0930b-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="0930b-143">Farklı bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0930b-143">You can use a different name.</span></span> <span data-ttu-id="0930b-144">Bunu yaparsanız, hello adı daha sonra gerektiğinden, not edin.</span><span class="sxs-lookup"><span data-stu-id="0930b-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="0930b-145">Merhaba olay hub'ı için diğer seçenekleri tooset gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0930b-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Yeni bir olay hub'ı oluşturmak için dikey penceresi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="0930b-147">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="0930b-148">GRANT erişim toohello olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="0930b-148">Grant access toohello event hub</span></span>

<span data-ttu-id="0930b-149">Bir işlem tooan event hub'ı veri göndermeden önce hello olay hub'ı, uygun erişim veren bir ilke olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="0930b-150">Merhaba erişim ilkesi yetkilendirme bilgilerini içeren bir bağlantı dizesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0930b-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="0930b-151">Merhaba olay ad alanı dikey penceresinde tıklayın **olay hub'ları** ve ardından yeni olay hub'ınızı hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="0930b-152">Merhaba olay hub dikey penceresinde tıklayın **paylaşılan erişim ilkeleri** ve ardından  **+ &nbsp;Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0930b-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0930b-153">Merhaba olay hub değil hello olay hub'ı ad çalıştığınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="0930b-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="0930b-154">Adlı ilke Ekle `socialtwitter-access` ve **talep**seçin **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="0930b-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Yeni bir olay hub'ı erişim ilkesi oluşturmak için dikey penceresi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="0930b-156">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-156">Click **Create**.</span></span>

5.  <span data-ttu-id="0930b-157">Hello İlkesi dağıtıldıktan sonra paylaşılan erişim ilkeleri hello listesinde tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="0930b-158">Etiketli Bul hello kutusunu **bağlantı dize birincil anahtarı** ve hello Kopyala düğmesine bir sonraki toohello bağlantı dizesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0930b-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Merhaba erişim ilkesinden Hello birincil bağlantı dizesi anahtarını kopyalama](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="0930b-160">Merhaba bağlantı dizesi, bir metin düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0930b-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="0930b-161">Bazı küçük düzenlemeler tooit yaptıktan sonra hello için sonraki bölümde, bu bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="0930b-162">Merhaba bağlantı dizesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="0930b-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="0930b-163">Merhaba bağlantı dizesi noktalı virgülle ayırarak, birden çok anahtar-değer çiftleri içerdiğine dikkat edin: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, ve `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="0930b-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="0930b-164">Güvenlik için hello bağlantı dizesi hello örnekte bölümleri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="0930b-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="0930b-165">Merhaba Metin Düzenleyicisi'nde hello kaldırmak `EntityPath` hello bağlantı dizesinden çifti (yakalanması tooremove hello noktalı unutmayın).</span><span class="sxs-lookup"><span data-stu-id="0930b-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="0930b-166">İşiniz bittiğinde, hello bağlantı dizesi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="0930b-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="0930b-167">Yapılandırma ve hello Twitter istemci uygulamasını başlatın</span><span class="sxs-lookup"><span data-stu-id="0930b-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="0930b-168">Merhaba istemci uygulaması tweet olayları doğrudan Twitter'dan alır.</span><span class="sxs-lookup"><span data-stu-id="0930b-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="0930b-169">İçinde toodo bunu sipariş, izni toocall hello akış API'leri Twitter gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="0930b-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="0930b-170">izni, uygulamanın benzersiz kimlik bilgilerini (örneğin, OAuth belirteci) oluşturur Twitter oluşturduğunuz tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0930b-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="0930b-171">API çağrıları yaptığında, daha sonra bu kimlik bilgileri hello istemci uygulaması toouse yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0930b-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="0930b-172">Bir Twitter uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0930b-172">Create a Twitter application</span></span>
<span data-ttu-id="0930b-173">Bu öğretici için kullanabileceğiniz bir Twitter uygulaması zaten yoksa bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0930b-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="0930b-174">Zaten bir Twitter hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="0930b-175">bir uygulama oluşturma ve hello anahtarları, gizli ve belirteç alma Twitter tam işleminde Hello değişebilir.</span><span class="sxs-lookup"><span data-stu-id="0930b-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="0930b-176">Bu yönergeleri hello Twitter sitesinde bakın eşleşmiyorsa, toohello Twitter Geliştirici belgelerinize bakın.</span><span class="sxs-lookup"><span data-stu-id="0930b-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="0930b-177">Toohello Git [Twitter Uygulama Yönetimi sayfasında](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="0930b-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="0930b-178">Yeni bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0930b-178">Create a new application.</span></span> 

    * <span data-ttu-id="0930b-179">Merhaba Web sitesi URL'si için geçerli bir URL belirtin.</span><span class="sxs-lookup"><span data-stu-id="0930b-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="0930b-180">Canlı site toobe yok.</span><span class="sxs-lookup"><span data-stu-id="0930b-180">It does not have toobe a live site.</span></span> <span data-ttu-id="0930b-181">(Yalnızca belirtemezsiniz `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="0930b-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="0930b-182">Merhaba geri çağırma alanı boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="0930b-182">Leave hello callback field blank.</span></span> <span data-ttu-id="0930b-183">Bu öğretici için kullandığınız Merhaba istemci uygulaması geri aramalar gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="0930b-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Twitter içinde bir uygulama oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="0930b-185">İsteğe bağlı olarak, yalnızca tooread hello uygulamanın izinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0930b-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="0930b-186">Merhaba uygulaması oluşturulduğunda toohello Git **anahtarları ve erişim belirteçleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0930b-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="0930b-187">Merhaba düğmesi toogenerate bir erişim belirteci ve erişim belirteci gizli anahtarı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0930b-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="0930b-188">Hello sonraki yordamda gerektiğinden bu bilgiler faydalı, tutun.</span><span class="sxs-lookup"><span data-stu-id="0930b-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="0930b-189">Merhaba anahtarları ve gizli anahtarları hello Twitter uygulama için erişim tooyour Twitter hesabı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="0930b-190">Bu bilgileri gizli olarak değerlendirir, Twitter parolanızı olduğu gibi aynı hello.</span><span class="sxs-lookup"><span data-stu-id="0930b-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="0930b-191">Örneğin, bir uygulama tooothers size bu bilgileri katıştırma.</span><span class="sxs-lookup"><span data-stu-id="0930b-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="0930b-192">Merhaba istemci uygulaması yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0930b-192">Configure hello client application</span></span>
<span data-ttu-id="0930b-193">TooTwitter verileri kullanarak bağlanan bir istemci uygulaması oluşturduk [Twitter'ın akış API'leri](https://dev.twitter.com/streaming/overview) toocollect tweet olaylar hakkında konular belirli bir dizi.</span><span class="sxs-lookup"><span data-stu-id="0930b-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="0930b-194">Merhaba uygulamanın kullandığı hello [Sentiment140](http://help.sentiment140.com/) düşünceleri değeri tooeach tweet aşağıdaki hello atar açık kaynak aracı:</span><span class="sxs-lookup"><span data-stu-id="0930b-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="0930b-195">0 negatif =</span><span class="sxs-lookup"><span data-stu-id="0930b-195">0 = negative</span></span>
* <span data-ttu-id="0930b-196">2 = neutral =</span><span class="sxs-lookup"><span data-stu-id="0930b-196">2 = neutral</span></span>
* <span data-ttu-id="0930b-197">4 pozitif =</span><span class="sxs-lookup"><span data-stu-id="0930b-197">4 = positive</span></span>

<span data-ttu-id="0930b-198">Merhaba tweet olayları düşünceleri değeri atandıktan sonra bunlar daha önce oluşturduğunuz toohello olay hub'ı atılır.</span><span class="sxs-lookup"><span data-stu-id="0930b-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="0930b-199">Merhaba uygulamayı çalıştırmadan önce hello Twitter anahtarları ve hello olay hub bağlantı dizesine gibi belirli bilgileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0930b-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="0930b-200">Bu yolla hello yapılandırma bilgileri sağlayabilir:</span><span class="sxs-lookup"><span data-stu-id="0930b-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="0930b-201">Merhaba uygulamayı çalıştırın ve ardından hello uygulamanın UI tooenter hello anahtarları, gizli ve bağlantı dizesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0930b-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="0930b-202">Bunu yaparsanız, hello yapılandırma bilgilerini geçerli oturumunuz için kullanılır, ancak bunu kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="0930b-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="0930b-203">Merhaba uygulamanın .config dosyasına ve kümesi hello değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="0930b-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="0930b-204">Bu yaklaşım hello yapılandırma bilgilerini devam ederse, ancak aynı zamanda bu olası hassas bilgiler düz metin, bilgisayarınızda depolanır gelir.</span><span class="sxs-lookup"><span data-stu-id="0930b-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="0930b-205">Merhaba aşağıdaki yordamı her iki yaklaşımın belgeler.</span><span class="sxs-lookup"><span data-stu-id="0930b-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="0930b-206">Karşıdan yükleyip hello sıkıştırması açılmış olduğundan emin olun [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) hello önkoşullarını listelendiği gibi uygulama.</span><span class="sxs-lookup"><span data-stu-id="0930b-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="0930b-207">tooset hello değerleri çalışma zamanında (ve yalnızca hello geçerli oturum için), çalıştırmak hello `TwitterWPFClient.exe` uygulama.</span><span class="sxs-lookup"><span data-stu-id="0930b-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="0930b-208">Merhaba uygulaması istediğinde, hello aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="0930b-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="0930b-209">Merhaba Twitter tüketici anahtarı (API anahtarı).</span><span class="sxs-lookup"><span data-stu-id="0930b-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="0930b-210">Merhaba Twitter tüketici gizli anahtarı (API gizli).</span><span class="sxs-lookup"><span data-stu-id="0930b-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="0930b-211">Merhaba Twitter erişim belirteci.</span><span class="sxs-lookup"><span data-stu-id="0930b-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="0930b-212">Merhaba Twitter erişim belirteci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0930b-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="0930b-213">daha önce kaydettiğiniz hello bağlantı dizesi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0930b-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="0930b-214">Merhaba kaldırdığınız hello bağlantı dizesini kullandığınızdan emin olun `EntityPath` gelen anahtar-değer çifti.</span><span class="sxs-lookup"><span data-stu-id="0930b-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="0930b-215">toodetermine düşünceleri için istediğiniz hello Twitter anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="0930b-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Çalıştıran, örtülü ayarları gösteren TwitterWpfClient uygulama](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="0930b-217">tooset hello değerleri kalıcı olarak, bir metin düzenleyicisi tooopen hello TwitterWpfClient.exe.config dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0930b-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="0930b-218">Merhaba sonra `<appSettings>` öğesi, bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="0930b-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="0930b-219">Ayarlama `oauth_consumer_key` toohello Twitter tüketici anahtarı (API anahtarı).</span><span class="sxs-lookup"><span data-stu-id="0930b-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="0930b-220">Ayarlama `oauth_consumer_secret` toohello Twitter tüketici gizli anahtarı (API gizli).</span><span class="sxs-lookup"><span data-stu-id="0930b-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="0930b-221">Ayarlama `oauth_token` toohello Twitter erişim belirteci.</span><span class="sxs-lookup"><span data-stu-id="0930b-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="0930b-222">Ayarlama `oauth_token_secret` toohello Twitter erişim belirteci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0930b-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="0930b-223">Merhaba devamındaki `<appSettings>` öğesi, bu değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="0930b-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="0930b-224">Ayarlama `EventHubName` toohello olay hub'ı adı (diğer bir deyişle, hello varlık yolu toohello değeri).</span><span class="sxs-lookup"><span data-stu-id="0930b-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="0930b-225">Ayarlama `EventHubNameConnectionString` toohello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="0930b-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="0930b-226">Merhaba kaldırdığınız hello bağlantı dizesini kullandığınızdan emin olun `EntityPath` gelen anahtar-değer çifti.</span><span class="sxs-lookup"><span data-stu-id="0930b-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="0930b-227">Merhaba `<appSettings>` bölümü aşağıdaki örneğine hello gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="0930b-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="0930b-228">(Daha anlaşılır olması ve güvenlik için biz bazı satırlar Sarmalanan ve bazı karakterler kaldırılmış.)</span><span class="sxs-lookup"><span data-stu-id="0930b-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Merhaba Twitter anahtarları ve gizli anahtarları ve hello olay hub'ı bağlantı dizesi bilgilerini gösteren bir metin düzenleyicisinde TwitterWpfClient uygulama yapılandırma dosyası](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="0930b-230">Merhaba uygulaması zaten başlatmadıysanız TwitterWpfClient.exe Şimdi Çalıştır.</span><span class="sxs-lookup"><span data-stu-id="0930b-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="0930b-231">Merhaba Yeşil Başlat düğmesi toocollect sosyal düşünceleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0930b-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="0930b-232">Merhaba Tweet olaylara bakın **CreatedAt**, **konu**, ve **SentimentScore** tooyour olay hub'ı gönderilen değerler.</span><span class="sxs-lookup"><span data-stu-id="0930b-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Tweet'leri listesini gösteren TwitterWpfClient uygulaması çalışıyor](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="0930b-234">Hataları görmek ve hello alt kısmında hello penceresinde görüntülenen tweet'leri akışı görmüyorsanız, hello anahtarları ve gizli anahtarları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0930b-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="0930b-235">Ayrıca hello bağlantı dizesini kontrol edin (Merhaba içermediğinden emin olun `EntityPath` anahtar ve değer.)</span><span class="sxs-lookup"><span data-stu-id="0930b-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0930b-236">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0930b-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="0930b-237">Twitter gelen gerçek zamanlı akış tweet olaylarını, akış analizi işi tooanalyze bu olayları gerçek zamanlı olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0930b-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="0930b-238">Hello Azure portal'ı tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.</span><span class="sxs-lookup"><span data-stu-id="0930b-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="0930b-239">Ad hello iş `socialtwitter-sa-job` ve abonelik, kaynak grubunu ve konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="0930b-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="0930b-240">Bir fikir tooplace hello iş ve hello event hub'ında hello olan en iyi performans ve bunu için aynı bölge bölgeler arasında tootransfer veri ödemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0930b-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Yeni bir Stream Analytics işi oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="0930b-242">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-242">Click **Create**.</span></span>

    <span data-ttu-id="0930b-243">Merhaba iş oluşturulur ve hello portal iş ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0930b-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="0930b-244">Merhaba iş giriş belirtin</span><span class="sxs-lookup"><span data-stu-id="0930b-244">Specify hello job input</span></span>

1. <span data-ttu-id="0930b-245">Stream Analytics işinizde altında **iş topoloji** hello iş dikey penceresinde hello ortadaki tıklatın **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="0930b-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="0930b-246">Merhaba, **girişleri** dikey penceresinde tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="0930b-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="0930b-247">**Giriş diğer adı**: hello adını kullan `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="0930b-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="0930b-248">Farklı bir ad kullanırsanız, daha sonra gerektiğinden, not edin.</span><span class="sxs-lookup"><span data-stu-id="0930b-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="0930b-249">**Kaynak türünü**: seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="0930b-250">**Kaynak**: seçin **olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="0930b-251">**Alma seçeneği**: seçin **geçerli aboneliğe ilişkin kullanım olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="0930b-252">**Hizmet veri yolu ad alanı**: daha önce oluşturduğunuz hello olay hub'ad alanı seçin (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="0930b-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="0930b-253">**Olay hub'ı**: daha önce oluşturduğunuz Select hello olay hub'ı (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="0930b-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="0930b-254">**Olay hub'ı ilke adı**: daha önce oluşturduğunuz hello erişim ilkesi seçin (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="0930b-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Akış analizi işi için yeni giriş oluşturma](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="0930b-256">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="0930b-257">Merhaba iş sorgusu belirtin</span><span class="sxs-lookup"><span data-stu-id="0930b-257">Specify hello job query</span></span>

<span data-ttu-id="0930b-258">Akış analizi dönüşümleri açıklayan bir basit ve bildirim temelli sorgu modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="0930b-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="0930b-259">toolearn hello dili hakkında daha fazla bilgi görmek hello [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="0930b-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="0930b-260">Bu öğretici, yazar ve birkaç sorgu Twitter verileri üzerinde test yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0930b-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="0930b-261">kullanabileceğiniz belirtilenlerden konular arasındaki toocompare hello sayısı, bir [atlayan pencere](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello beş saniyede belirtilenlerden konusuna göre sayısı.</span><span class="sxs-lookup"><span data-stu-id="0930b-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="0930b-262">Kapat hello **girişleri** yapmadıysanız dikey.</span><span class="sxs-lookup"><span data-stu-id="0930b-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="0930b-263">Merhaba iş dikey penceresinde hello tıklayın **sorgu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="0930b-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="0930b-264">Azure hello girişleri listeler ve toohello çıktı gönderilmiş gibi hello proje için yapılandırılmış ve olanak sağlayan bir sorgu oluşturmanıza olanak tanır çıkışları hello Giriş akışı Dönüştür.</span><span class="sxs-lookup"><span data-stu-id="0930b-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="0930b-265">Bu hello TwitterWpfClient uygulama çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0930b-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="0930b-266">Merhaba, **sorgu** dikey penceresinde hello nokta sonraki toohello tıklatın `TwitterStream` girin ve ardından **örnek giriş verilerinden**.</span><span class="sxs-lookup"><span data-stu-id="0930b-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Menü seçeneklerini toouse için örnek veri hello akış analizi işi girişi, verilerle"Seçili örnek Giriş"](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="0930b-268">Bu akış ne kadar süreyle tooread hello girişi bakımından tanımlanmış ne kadar örnek veri tooget belirtmenize olanak sağlar. bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="0930b-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="0930b-269">Ayarlama **dakika** too3 ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0930b-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    !["3 Seçili dakika ile" Merhaba Giriş akışı örnekleme seçenekleri.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="0930b-271">Azure hello Giriş akışı verilerden 3 dakika eşitleyeceğini örnekleri ve hello örnek verileri hazır olduğunda size bildirir.</span><span class="sxs-lookup"><span data-stu-id="0930b-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="0930b-272">(Bu kısa biraz uzun sürebilir.)</span><span class="sxs-lookup"><span data-stu-id="0930b-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="0930b-273">Merhaba örnek verileri geçici olarak depolanır ve açmak hello sorgu penceresi açıkken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0930b-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="0930b-274">Hello sorgu penceresini kapattığınızda, hello örnek veriler atılır ve yeni bir örnek veri kümesi toocreate sahip.</span><span class="sxs-lookup"><span data-stu-id="0930b-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="0930b-275">Merhaba Kod Düzenleyicisi toohello aşağıdaki Hello sorguyu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0930b-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="0930b-276">Varsa kullanmadı `TwitterStream` hello giriş için diğer ad hello, diğer adınızı alternatif `TwitterStream` hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="0930b-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="0930b-277">Bu sorgu hello kullanan **TIMESTAMP BY** anahtar sözcüğü toospecify hello yükü toobe hello zamana bağlı hesaplamanın kullanılan bir zaman damgası alanı.</span><span class="sxs-lookup"><span data-stu-id="0930b-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="0930b-278">Bu alan belirtilmezse, hello Pencereleme işlemi her olay hello olay hub'ına gelen hello saati kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0930b-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="0930b-279">Merhaba "geliş saati vs uygulama zamanı" bölümünde daha fazla bilgi edinin [Stream Analytics sorgu başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="0930b-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="0930b-280">Ayrıca bu sorgu hello kullanarak bir zaman damgası her penceresinde hello sonunun erişir **System.Timestamp** özelliği.</span><span class="sxs-lookup"><span data-stu-id="0930b-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="0930b-281">Tıklatın **Test**.</span><span class="sxs-lookup"><span data-stu-id="0930b-281">Click **Test**.</span></span> <span data-ttu-id="0930b-282">Merhaba sorgu, örneklenen hello veri karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="0930b-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="0930b-283">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-283">Click **Save**.</span></span> <span data-ttu-id="0930b-284">Bu hello sorgu hello akış analizi işi bir parçası olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0930b-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="0930b-285">(Merhaba örnek verileri kaydetmez.)</span><span class="sxs-lookup"><span data-stu-id="0930b-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="0930b-286">Deneme hello akışından farklı alanları kullanma</span><span class="sxs-lookup"><span data-stu-id="0930b-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="0930b-287">Hello aşağıdaki tablo veri akışı JSON hello parçası olan hello alanları listeler.</span><span class="sxs-lookup"><span data-stu-id="0930b-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="0930b-288">Ücretsiz tooexperiment hello sorgu Düzenleyicisi'nde eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="0930b-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="0930b-289">JSON özelliği</span><span class="sxs-lookup"><span data-stu-id="0930b-289">JSON property</span></span> | <span data-ttu-id="0930b-290">Tanım</span><span class="sxs-lookup"><span data-stu-id="0930b-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="0930b-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="0930b-291">CreatedAt</span></span> | <span data-ttu-id="0930b-292">Başlangıç saati, hello tweet oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0930b-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="0930b-293">Konu</span><span class="sxs-lookup"><span data-stu-id="0930b-293">Topic</span></span> | <span data-ttu-id="0930b-294">Merhaba eşleşen hello konu belirtilen anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="0930b-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="0930b-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="0930b-295">SentimentScore</span></span> | <span data-ttu-id="0930b-296">Merhaba düşünceleri puan Sentiment140</span><span class="sxs-lookup"><span data-stu-id="0930b-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="0930b-297">Yazar</span><span class="sxs-lookup"><span data-stu-id="0930b-297">Author</span></span> | <span data-ttu-id="0930b-298">Merhaba tweet gönderilen hello Twitter tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="0930b-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="0930b-299">Metin</span><span class="sxs-lookup"><span data-stu-id="0930b-299">Text</span></span> | <span data-ttu-id="0930b-300">Merhaba tam hello tweet gövdesi</span><span class="sxs-lookup"><span data-stu-id="0930b-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="0930b-301">Çıkış havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0930b-301">Create an output sink</span></span>

<span data-ttu-id="0930b-302">Şimdi bir olay akışı, bir olay hub'ı giriş tooingest olayları ve sorgu tooperform dönüştürme hello akış üzerinden tanımladınız.</span><span class="sxs-lookup"><span data-stu-id="0930b-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="0930b-303">Merhaba son toodefine hello işi için çıkış havuzu adımdır.</span><span class="sxs-lookup"><span data-stu-id="0930b-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="0930b-304">Bu öğreticide, bir araya getirilir hello tweet olayları hello iş sorgu tooAzure Blob Depolama yazma.</span><span class="sxs-lookup"><span data-stu-id="0930b-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="0930b-305">SQL Database, Azure Table storage, sonuçları tooAzure olay hub'ları da gönderebilir veya Power BI bağlı olarak uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="0930b-306">Merhaba iş çıktısı belirtin</span><span class="sxs-lookup"><span data-stu-id="0930b-306">Specify hello job output</span></span>

1. <span data-ttu-id="0930b-307">Merhaba, **iş topoloji** bölümünde, hello tıklatın **çıkış** kutusu.</span><span class="sxs-lookup"><span data-stu-id="0930b-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="0930b-308">Merhaba, **çıkışları** dikey penceresinde tıklatın  **+ &nbsp;Ekle** ve ardından hello dikey şu değerlerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="0930b-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="0930b-309">**Çıkış diğer adları**: hello adını kullan `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="0930b-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="0930b-310">**Havuz**: seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="0930b-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="0930b-311">**İçe aktarma seçenekleri**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.</span><span class="sxs-lookup"><span data-stu-id="0930b-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="0930b-312">**Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-312">**Storage account**.</span></span> <span data-ttu-id="0930b-313">Seçin **yeni bir depolama hesabı oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="0930b-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="0930b-314">**Depolama hesabı** (ikinci kutusu).</span><span class="sxs-lookup"><span data-stu-id="0930b-314">**Storage account** (second box).</span></span> <span data-ttu-id="0930b-315">Girin `YOURNAMEsa`, burada `YOURNAME` adınızı veya başka bir benzersiz bir dize.</span><span class="sxs-lookup"><span data-stu-id="0930b-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="0930b-316">Merhaba adı yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0930b-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="0930b-317">**Kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="0930b-317">**Container**.</span></span> <span data-ttu-id="0930b-318">Girin `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="0930b-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="0930b-319">Merhaba depolama hesabı adı ve kapsayıcı adı kullanılan birlikte tooprovide bu gibi hello blob depolama için bir URI şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0930b-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Stream Analytics işi için "Yeni çıkış" dikey](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="0930b-321">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-321">Click **Create**.</span></span> 

    <span data-ttu-id="0930b-322">Azure hello depolama hesabı oluşturur ve bir anahtarı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0930b-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="0930b-323">Kapat hello **çıkışları** dikey.</span><span class="sxs-lookup"><span data-stu-id="0930b-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="0930b-324">Merhaba işi Başlat</span><span class="sxs-lookup"><span data-stu-id="0930b-324">Start hello job</span></span>

<span data-ttu-id="0930b-325">İş Girişi, sorgu ve çıktı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0930b-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="0930b-326">Hazır toostart hello Stream Analytics işi var.</span><span class="sxs-lookup"><span data-stu-id="0930b-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="0930b-327">Bu hello TwitterWpfClient uygulama çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0930b-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="0930b-328">Merhaba iş dikey penceresinde tıklayın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="0930b-328">In hello job blade, click **Start**.</span></span>

    ![Merhaba Stream Analytics işi Başlat](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="0930b-330">Merhaba, **başlangıç işi** dikey penceresinde için **iş çıktısı başlangıç zamanı**seçin **şimdi** ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="0930b-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Dikey penceresinde hello Stream Analytics işi "işlemini Başlat"](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="0930b-332">Azure sizi uyarır hello iş başlatıldı ve hello iş dikey penceresinde hello durumu olarak görüntülendiğinde **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="0930b-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![İşi çalıştırma](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="0930b-334">Görünüm çıktı düşünceleri analiz için</span><span class="sxs-lookup"><span data-stu-id="0930b-334">View output for sentiment analysis</span></span>

<span data-ttu-id="0930b-335">İşinizi çalışmaya başladıktan ve hello gerçek zamanlı Twitter akışı işleme sonra hello çıktı düşünceleri analiz için görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0930b-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="0930b-336">Gibi bir araç kullanabilirsiniz [Azure Storage Gezgini](https://http://storageexplorer.com/) veya [Azure Gezgini](http://www.cerebrata.com/products/azure-explorer/introduction) işinizi çıktı gerçek zamanlı olarak tooview.</span><span class="sxs-lookup"><span data-stu-id="0930b-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="0930b-337">Buradan, kullandığınız [Power BI](https://powerbi.com/) tooextend, uygulama tooinclude özelleştirilmiş bir pano gibi bir ekran aşağıdaki hello gösterilen hello:</span><span class="sxs-lookup"><span data-stu-id="0930b-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="0930b-339">Tooidentify oluşturan eğilim konuları başka bir sorgu oluşturun</span><span class="sxs-lookup"><span data-stu-id="0930b-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="0930b-340">Toounderstand Twitter düşünceleri kullanabileceğiniz başka bir sorguya dayalı bir [kayan pencere](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="0930b-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="0930b-341">tooidentify oluşturan eğilim konular, belirtilen sürede belirtilenlerden için eşik değer arası konuları arayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="0930b-342">Bu öğreticinin Hello amaçları doğrultusunda, 20 katından fazla hello son 5 saniye açıklanan konuları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0930b-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="0930b-343">Merhaba iş dikey penceresinde tıklayın **durdurmak** toostop hello işi.</span><span class="sxs-lookup"><span data-stu-id="0930b-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="0930b-344">Merhaba, **iş topoloji** bölümünde, hello tıklatın **sorgu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="0930b-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="0930b-345">Merhaba sorgu toohello aşağıdakileri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0930b-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="0930b-346">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0930b-346">Click **Save**.</span></span>

5. <span data-ttu-id="0930b-347">Bu hello TwitterWpfClient uygulama çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0930b-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="0930b-348">Tıklatın **Başlat** hello yeni bir sorgu kullanarak toorestart hello işi.</span><span class="sxs-lookup"><span data-stu-id="0930b-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="0930b-349">Destek alın</span><span class="sxs-lookup"><span data-stu-id="0930b-349">Get support</span></span>
<span data-ttu-id="0930b-350">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0930b-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0930b-351">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0930b-351">Next steps</span></span>
* [<span data-ttu-id="0930b-352">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="0930b-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0930b-353">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0930b-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0930b-354">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="0930b-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0930b-355">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="0930b-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0930b-356">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="0930b-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

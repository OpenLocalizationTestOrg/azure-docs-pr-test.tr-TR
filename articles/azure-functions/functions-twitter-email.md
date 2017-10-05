---
title: "Azure Logic Apps ile tümleşen bir işlev oluşturun | Microsoft Docs"
description: "Tweet düşünceleri kategorilere ayırmak ve düşünceleri düşük olduğunda bildirim göndermek için Azure Logic Apps ve Azure Bilişsel hizmetler ile tümleşen bir işlev oluşturun."
services: functions, logic-apps, cognitive-services
keywords: "iş akışı, bulut uygulamaları, bulut hizmetleri, iş süreçleri, sistem tümleştirme, kuruluş uygulaması tümleştirme, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="cb0ea-104">Azure Logic Apps ile tümleşen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="cb0ea-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="cb0ea-105">Azure işlevleri Logic Apps Tasarımcısı'nda Azure Logic Apps ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="cb0ea-106">Bu tümleştirme işlevleri bilgi işlem gücü düzenlemelerin de diğer Azure ve üçüncü taraf hizmetleri ile kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="cb0ea-107">Bu öğretici işlevleri Logic Apps ile Azure Bilişsel hizmetler Twitter gönderileri gelen düşünceleri çözümlemek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="cb0ea-108">Bir HTTP tetiklenen işlevi tweet'leri yeşil, sarı veya kırmızı düşünceleri puan dayalı olarak kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="cb0ea-109">Zayıf düşünceleri algılandığında bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-109">An email is sent when poor sentiment is detected.</span></span> 

![ilk iki adım uygulamasının mantığı Uygulama Tasarımcısı'nda Görüntü](media/functions-twitter-email/designer1.png)

<span data-ttu-id="cb0ea-111">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="cb0ea-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb0ea-112">Bilişsel Hizmetler hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="cb0ea-113">Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="cb0ea-114">Twitter hesabına bağlanan bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="cb0ea-115">Düşünceleri algılama mantığı uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="cb0ea-116">Mantıksal uygulama işlevine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="cb0ea-117">İşlev yanıttan dayalı bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb0ea-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-118">Prerequisites</span></span>

+ <span data-ttu-id="cb0ea-119">Etkin bir [Twitter](https://twitter.com/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="cb0ea-120">Bir [Outlook.com](https://outlook.com/) hesap (bildirim göndermek için).</span><span class="sxs-lookup"><span data-stu-id="cb0ea-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="cb0ea-121">Bu konu başlığında, başlangıç noktası olarak [Azure portalında ilk işlevinizi oluşturma](functions-create-first-azure-function.md) bölümünde oluşturulan kaynaklar kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="cb0ea-122">Zaten yapmadıysanız, işlev uygulaması oluşturmak için şimdi aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="cb0ea-123">Bilişsel Hizmetler hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb0ea-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="cb0ea-124">Bilişsel Hizmetler hesabı izlenmekte olan tweet'leri düşünceleri algılamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="cb0ea-125">[Azure Portal](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="cb0ea-126">Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="cb0ea-127">Tıklatın **veri + analiz** > **Bilişsel Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="cb0ea-128">Ardından, tabloda belirtildiği gibi ayarları kullanmak için koşullarını kabul edin ve denetleyin **panoya Sabitle**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Bilişsel hesabı dikey penceresi oluşturma](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="cb0ea-130">Ayar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-130">Setting</span></span>      |  <span data-ttu-id="cb0ea-131">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="cb0ea-131">Suggested value</span></span>   | <span data-ttu-id="cb0ea-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb0ea-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="cb0ea-133">**Ad**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-133">**Name**</span></span> | <span data-ttu-id="cb0ea-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="cb0ea-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="cb0ea-135">Benzersiz bir hesap adı seçin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="cb0ea-136">**API türü**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-136">**API type**</span></span> | <span data-ttu-id="cb0ea-137">Metin Analizi API’si</span><span class="sxs-lookup"><span data-stu-id="cb0ea-137">Text Analytics API</span></span> | <span data-ttu-id="cb0ea-138">Metin çözümlemek için kullanılan API.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="cb0ea-139">**Konum**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-139">**Location**</span></span> | <span data-ttu-id="cb0ea-140">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="cb0ea-140">West US</span></span> | <span data-ttu-id="cb0ea-141">Şu anda yalnızca **Batı ABD** metin analizi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="cb0ea-142">**Fiyatlandırma katmanı**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-142">**Pricing tier**</span></span> | <span data-ttu-id="cb0ea-143">F0</span><span class="sxs-lookup"><span data-stu-id="cb0ea-143">F0</span></span> | <span data-ttu-id="cb0ea-144">En düşük katman ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-144">Start with the lowest tier.</span></span> <span data-ttu-id="cb0ea-145">Çağrıları dışında çalıştırırsanız, daha yüksek bir katmana ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="cb0ea-146">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-146">**Resource group**</span></span> | <span data-ttu-id="cb0ea-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb0ea-147">myResourceGroup</span></span> | <span data-ttu-id="cb0ea-148">Aynı kaynak grubunun tüm hizmetler için bu öğreticiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="cb0ea-149">Tıklatın **oluşturma** hesabınızı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-149">Click **Create** to create your account.</span></span> <span data-ttu-id="cb0ea-150">Hesap oluşturulduktan sonra yeni Bilişsel hesabı panosuna sabitlediğiniz hizmetleriniz tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="cb0ea-151">Hesabı'nda tıklatın **anahtarları**ve ardından değerini kopyalayın **anahtar 1** ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="cb0ea-152">Bilişsel hizmetler hesabınıza mantıksal uygulama bağlanmak için bu anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![Anahtarlar](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="cb0ea-154">İşlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb0ea-154">Create the function</span></span>

<span data-ttu-id="cb0ea-155">İşlevler bir iş akışındaki logic apps işleme görevlerini boşaltmak için harika bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="cb0ea-156">Bu öğretici, tweet düşünceleri puanları Bilişsel Hizmetleri'nden işlemek ve bir kategori değeri döndürmek için bir HTTP tetiklenen işlevi kullanır.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="cb0ea-157">İşlev uygulamanızı genişletin, tıklayın  **+**  düğmesine **işlevleri**, tıklatın **HTTPTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="cb0ea-158">Tür `CategorizeSentiment` işlevi için **adı** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![İşlev uygulamalar dikey penceresinde, İşlevler +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="cb0ea-160">Run.csx dosyasının içeriğini aşağıdaki kodla değiştirin ve ardından **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="cb0ea-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="cb0ea-161">Bu işlev kodu istekte alınan düşünceleri puan bağlı bir renk kategori döndürür.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="cb0ea-162">İşlevi test etmek için tıklatın **Test** Test sekmesi genişletmek sağ uçta. Değerini yazın `0.2` için **istek gövdesinde**ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="cb0ea-163">Değerini **kırmızı** yanıt gövdesinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Azure portalında işlevi test etme](./media/functions-twitter-email/test.png)

<span data-ttu-id="cb0ea-165">Artık düşünceleri puanları kategorilere ayıran bir işlev var.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="cb0ea-166">Ardından, işlevinizi Twitter ve Bilişsel hizmetler hesaplarınızı ile tümleşen bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="cb0ea-167">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb0ea-167">Create a logic app</span></span>   

1. <span data-ttu-id="cb0ea-168">Azure portalında tıklatın **yeni** düğme Azure portalında sol üst köşesinde bulundu.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="cb0ea-169">Tıklatın **Kurumsal tümleştirme** > **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="cb0ea-170">Ardından, tablo, onay belirtildiği gibi ayarları kullanın **panoya Sabitle**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="cb0ea-171">Ardından, bir **adı** gibi `TweetSentiment`tablosunda belirtilen ayarları kullanmak, koşulları kabul edin ve denetleyin **panoya Sabitle**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Azure portalında mantıksal uygulama oluşturma](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="cb0ea-173">Ayar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-173">Setting</span></span>      |  <span data-ttu-id="cb0ea-174">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="cb0ea-174">Suggested value</span></span>   | <span data-ttu-id="cb0ea-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb0ea-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="cb0ea-176">**Ad**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-176">**Name**</span></span> | <span data-ttu-id="cb0ea-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="cb0ea-177">TweetSentiment</span></span> | <span data-ttu-id="cb0ea-178">Uygulamanız için uygun bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="cb0ea-179">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-179">**Resource group**</span></span> | <span data-ttu-id="cb0ea-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb0ea-180">myResourceGroup</span></span> | <span data-ttu-id="cb0ea-181">Metin çözümlemek için kullanılan API.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="cb0ea-182">**Konum**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-182">**Location**</span></span> | <span data-ttu-id="cb0ea-183">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="cb0ea-183">East US</span></span> | <span data-ttu-id="cb0ea-184">Yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="cb0ea-185">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-185">**Resource group**</span></span> | <span data-ttu-id="cb0ea-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb0ea-186">myResourceGroup</span></span> | <span data-ttu-id="cb0ea-187">Var olan kaynak grubunu olarak önce seçin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="cb0ea-188">Tıklatın **oluşturma** mantıksal uygulamanızı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="cb0ea-189">Uygulama oluşturulduktan sonra yeni mantıksal uygulamanızı panosuna sabitlediğiniz tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="cb0ea-190">Ardından Logic Apps Tasarımcısı'nda aşağı kaydırın ve tıklatın **boş mantıksal uygulama** şablonu.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Boş Logic Apps şablon](media/functions-twitter-email/blank.png)

<span data-ttu-id="cb0ea-192">Logic Apps Tasarımcısı'nı şimdi hizmetler ve tetikleyiciler uygulamanıza eklemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="cb0ea-193">Twitter hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="cb0ea-193">Connect to Twitter</span></span>

<span data-ttu-id="cb0ea-194">İlk olarak, Twitter hesabınız için bir bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="cb0ea-195">Mantıksal uygulama çalıştırmak için uygulamayı tetiklemek tweet'leri için yoklar.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="cb0ea-196">Tasarımcısı'nda tıklayın **Twitter** 'ı tıklatın ve hizmeti **yeni tweet zaman nakledilir** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="cb0ea-197">Twitter hesabınızda oturum açın ve hesabınızı kullanmak için Logic Apps yetkisi verin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="cb0ea-198">Tabloda belirtildiği gibi Twitter tetikleyici ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Twitter Bağlayıcısı ayarları](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="cb0ea-200">Ayar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-200">Setting</span></span>      |  <span data-ttu-id="cb0ea-201">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="cb0ea-201">Suggested value</span></span>   | <span data-ttu-id="cb0ea-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb0ea-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="cb0ea-203">**Arama metni**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-203">**Search text**</span></span> | <span data-ttu-id="cb0ea-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="cb0ea-204">#Azure</span></span> | <span data-ttu-id="cb0ea-205">Seçilen zaman aralığını yeni tweet'leri oluşturmak için yeterli için popülerdir diyez kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="cb0ea-206">Ücretsiz katmanı ve, diyez kullanarak çok popüler olduğunda, hızlı bir şekilde işlemleri Bilişsel hizmetler hesabınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="cb0ea-207">**Sıklık**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-207">**Frequency**</span></span> | <span data-ttu-id="cb0ea-208">Dakika</span><span class="sxs-lookup"><span data-stu-id="cb0ea-208">Minute</span></span> | <span data-ttu-id="cb0ea-209">Twitter yoklama için kullanılan sıklık birim.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="cb0ea-210">**Aralığı**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-210">**Interval**</span></span> | <span data-ttu-id="cb0ea-211">15</span><span class="sxs-lookup"><span data-stu-id="cb0ea-211">15</span></span> | <span data-ttu-id="cb0ea-212">Twitter istekler sıklığı birimleri arasında geçen süre.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="cb0ea-213">Tıklatın **kaydetmek** Twitter hesabınıza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="cb0ea-214">Artık uygulamanızı Twitter hesabına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="cb0ea-215">Ardından, toplanan tweet'leri düşünceleri algılamak için metin analizi'ne bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="cb0ea-216">Düşünceleri algılama ekleme</span><span class="sxs-lookup"><span data-stu-id="cb0ea-216">Add sentiment detection</span></span>

1. <span data-ttu-id="cb0ea-217">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Yeni adım ve bir eylem Ekle](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="cb0ea-219">İçinde **bir eylem seçin**, tıklatın **metin analizi**ve ardından **düşünceleri algılamak** eylem.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Düşünceleri Algıla](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="cb0ea-221">Bir bağlantı adı gibi yazın `MyCognitiveServicesConnection`kaydedilen Bilişsel Hizmetler hesabı için anahtarını yapıştırın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="cb0ea-222">Tıklatın **çözümlemek için metin** > **Tweet metin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Düşünceleri Algıla](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="cb0ea-224">Düşünceleri algılama yapılandırılır, işlevinizi düşünceleri puan çıktısını kullanan bir bağlantı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="cb0ea-225">Düşünceleri çıktı, işlevine bağlayın</span><span class="sxs-lookup"><span data-stu-id="cb0ea-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="cb0ea-226">Logic Apps Tasarımcısı'nda tıklayın **yeni adım** > **Eylem Ekle**ve ardından **Azure işlevleri**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="cb0ea-227">Tıklatın **bir Azure işlevi seçin**seçin **CategorizeSentiment** daha önce oluşturduğunuz işlevi.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Bir Azure işlevi Seç gösteren azure işlevi kutusu](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="cb0ea-229">İçinde **iste gövde**, tıklatın **puan** ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Puan](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="cb0ea-231">Şimdi, düşünceleri puan mantığı uygulamadan gönderildiğinde işlevinizi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="cb0ea-232">Bir renk kodlu kategorisi mantıksal uygulama işlevi tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="cb0ea-233">Sonra düşünceleri değeri, gönderilen bir e-posta bildirimi ekleyin **kırmızı** işlevinden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="cb0ea-234">E-posta bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="cb0ea-234">Add email notifications</span></span>

<span data-ttu-id="cb0ea-235">Bir e-posta olarak düşünceleri puanlanır zaman tetiklemek için iş akışı son parçası olan _kırmızı_.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="cb0ea-236">Bu konuda bir Outlook.com bağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="cb0ea-237">Gmail veya Office 365 Outlook Bağlayıcısı'nı kullanmak için benzer adımları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="cb0ea-238">Logic Apps Tasarımcısı'nda tıklayın **yeni adım** > **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="cb0ea-239">Tıklatın **bir değer seçin**, ardından **gövde**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="cb0ea-240">Seçin **eşittir**, tıklatın **bir değer seçin** ve türü `RED`, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Bir koşul mantıksal uygulama ekleyin.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="cb0ea-242">İçinde **Evet ise, hiçbir şey yapma**, tıklatın **Eylem Ekle**, arama `outlook.com`, tıklatın **bir e-posta Gönder**ve Outlook.com hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Koşul için bir eylem seçin.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="cb0ea-244">Bir Outlook.com hesabınız yoksa, Gmail veya Office 365 Outlook gibi başka bir bağlayıcı seçebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cb0ea-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="cb0ea-245">İçinde **bir e-posta Gönder** eylem, belirtilen tabloda olarak e-posta ayarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Bir e-posta eylem göndermek için e-postayı yapılandırın.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="cb0ea-247">Ayar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-247">Setting</span></span>      |  <span data-ttu-id="cb0ea-248">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="cb0ea-248">Suggested value</span></span>   | <span data-ttu-id="cb0ea-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb0ea-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="cb0ea-250">**Hedef**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-250">**To**</span></span> | <span data-ttu-id="cb0ea-251">E-posta adresinizi yazın</span><span class="sxs-lookup"><span data-stu-id="cb0ea-251">Type your email address</span></span> | <span data-ttu-id="cb0ea-252">Bildirim aldığı e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="cb0ea-253">**Konu**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-253">**Subject**</span></span> | <span data-ttu-id="cb0ea-254">Negatif tweet düşünceleri algılandı</span><span class="sxs-lookup"><span data-stu-id="cb0ea-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="cb0ea-255">E-posta bildirimi konu satırı.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="cb0ea-256">**Gövde**</span><span class="sxs-lookup"><span data-stu-id="cb0ea-256">**Body**</span></span> | <span data-ttu-id="cb0ea-257">Tweet metin, konumu</span><span class="sxs-lookup"><span data-stu-id="cb0ea-257">Tweet text, Location</span></span> | <span data-ttu-id="cb0ea-258">Tıklatın **Tweet metin** ve **konumu** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="cb0ea-259">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-259">Click **Save**.</span></span>

<span data-ttu-id="cb0ea-260">İş akışı tamamlandığına göre mantıksal uygulama etkinleştirin ve iş yerindeki işlevine bakın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="cb0ea-261">İş akışını sınayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-261">Test the workflow</span></span>

1. <span data-ttu-id="cb0ea-262">Mantıksal Uygulama Tasarımcısı'nda tıklayın **çalıştırmak** uygulamayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="cb0ea-263">Sol sütunda tıklatın **genel bakış** mantıksal uygulama durumunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Mantıksal uygulama yürütme durumu](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="cb0ea-265">(İsteğe bağlı) Yürütme ayrıntılarını görmek için çalışır birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="cb0ea-266">Git, işlevi, günlükleri görüntülemek ve düşünceleri değerleri alınan ve işlenen olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![İşlev günlüklerini görüntüle](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="cb0ea-268">Potansiyel olarak negatif düşünceleri algılandığında, bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="cb0ea-269">Bir e-posta almadıysanız, kırmızı döndürmek için işlev kodu değiştirebilirsiniz her zaman:</span><span class="sxs-lookup"><span data-stu-id="cb0ea-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="cb0ea-270">E-posta bildirimleri doğruladıktan sonra özgün kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cb0ea-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="cb0ea-271">Bu öğreticiyi tamamladıktan sonra mantıksal uygulama devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="cb0ea-272">Uygulama devre dışı bırakarak yürütmeleri için kartınızdan ve Bilişsel hizmetler hesabınızda işlemleri kullanarak kaçının.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="cb0ea-273">Şimdi işlevleri Logic Apps iş akışı ile tümleştirmek için ne kadar kolay olduğunu gördünüz.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="cb0ea-274">Mantıksal uygulama devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cb0ea-274">Disable the logic app</span></span>

<span data-ttu-id="cb0ea-275">Mantıksal uygulama devre dışı bırakmak için **genel bakış** ve ardından **devre dışı** ekranın üstünde.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="cb0ea-276">Bu mantıksal uygulama çalıştıran ve uygulamayı silmeden ücretlerinin yansıtılmasını durdurur.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![İşlev günlükleri](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="cb0ea-278">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb0ea-278">Next steps</span></span>

<span data-ttu-id="cb0ea-279">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="cb0ea-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb0ea-280">Bilişsel Hizmetler hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="cb0ea-281">Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="cb0ea-282">Twitter hesabına bağlanan bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="cb0ea-283">Düşünceleri algılama mantığı uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="cb0ea-284">Mantıksal uygulama işlevine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="cb0ea-285">İşlev yanıttan dayalı bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="cb0ea-286">İşlevinizi için sunucusuz bir API oluşturma konusunda bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="cb0ea-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="cb0ea-287">Azure İşlevlerini kullanarak sunucusuz bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb0ea-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="cb0ea-288">Logic Apps hakkında daha fazla bilgi için bkz: [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="cb0ea-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>


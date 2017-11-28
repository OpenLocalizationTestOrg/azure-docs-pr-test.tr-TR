---
title: "aaaCreate Azure Logic Apps ile tümleşen bir işlev | Microsoft Docs"
description: "Azure mantıksal uygulamaları ve Azure Bilişsel hizmetler toocategorize tweet düşünceleri ile tümleşen bir işlev oluşturun ve düşünceleri düşük olduğunda bildirimleri gönderin."
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="38d0d-104">Azure Logic Apps ile tümleşen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="38d0d-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="38d0d-105">Azure işlevleri hello Logic Apps Tasarımcısı Azure Logic Apps ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="38d0d-106">Bu tümleştirme işlevlerin diğer Azure ve üçüncü taraf hizmetleri düzenlemelerin içinde gücünün hello kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="38d0d-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="38d0d-107">Bu öğreticide gösterilmiştir toouse nasıl çalıştığını Twitter gönderileri gelen Logic Apps ve Azure Bilişsel hizmetler tooanalyze düşünceleri ile.</span><span class="sxs-lookup"><span data-stu-id="38d0d-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="38d0d-108">Bir HTTP tetiklenen işlevi tweet'leri yeşil, sarı veya kırmızı hello düşünceleri puan üzerinde dayalı olarak kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="38d0d-109">Zayıf düşünceleri algılandığında bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-109">An email is sent when poor sentiment is detected.</span></span> 

![ilk iki adım uygulamasının mantığı Uygulama Tasarımcısı'nda Görüntü](media/functions-twitter-email/designer1.png)

<span data-ttu-id="38d0d-111">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="38d0d-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38d0d-112">Bilişsel Hizmetler hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="38d0d-113">Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="38d0d-114">TooTwitter bağlayan bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="38d0d-115">Düşünceleri algılama toohello mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="38d0d-116">Merhaba mantığı uygulama toohello işlevi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="38d0d-117">Merhaba işlevi hello yanıttan dayalı bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38d0d-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="38d0d-118">Prerequisites</span></span>

+ <span data-ttu-id="38d0d-119">Etkin bir [Twitter](https://twitter.com/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="38d0d-120">Bir [Outlook.com](https://outlook.com/) hesap (bildirim göndermek için).</span><span class="sxs-lookup"><span data-stu-id="38d0d-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="38d0d-121">Bu konu içinde oluşturulan başlangıç noktası hello kaynaklarını kullanan [hello Azure portal ' ilk işlevinizi oluşturma](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="38d0d-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="38d0d-122">Zaten yapmadıysanız, bu adımları şimdi toocreate işlevi uygulamanızı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="38d0d-123">Bilişsel Hizmetler hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="38d0d-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="38d0d-124">Bilişsel hizmetler izlenmekte olan tweet'leri, gerekli toodetect hello düşünceleri hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="38d0d-125">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38d0d-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="38d0d-126">Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="38d0d-127">Tıklatın **veri + analiz** > **Bilişsel Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="38d0d-128">Ardından, olarak hello ayarları kullan hello tablosunda belirtilen hello koşullarını kabul edin ve denetleyin **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Bilişsel hesabı dikey penceresi oluşturma](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="38d0d-130">Ayar</span><span class="sxs-lookup"><span data-stu-id="38d0d-130">Setting</span></span>      |  <span data-ttu-id="38d0d-131">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="38d0d-131">Suggested value</span></span>   | <span data-ttu-id="38d0d-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38d0d-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="38d0d-133">**Ad**</span><span class="sxs-lookup"><span data-stu-id="38d0d-133">**Name**</span></span> | <span data-ttu-id="38d0d-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="38d0d-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="38d0d-135">Benzersiz bir hesap adı seçin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="38d0d-136">**API türü**</span><span class="sxs-lookup"><span data-stu-id="38d0d-136">**API type**</span></span> | <span data-ttu-id="38d0d-137">Metin Analizi API’si</span><span class="sxs-lookup"><span data-stu-id="38d0d-137">Text Analytics API</span></span> | <span data-ttu-id="38d0d-138">API tooanalyze metin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="38d0d-139">**Konum**</span><span class="sxs-lookup"><span data-stu-id="38d0d-139">**Location**</span></span> | <span data-ttu-id="38d0d-140">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="38d0d-140">West US</span></span> | <span data-ttu-id="38d0d-141">Şu anda yalnızca **Batı ABD** metin analizi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="38d0d-142">**Fiyatlandırma katmanı**</span><span class="sxs-lookup"><span data-stu-id="38d0d-142">**Pricing tier**</span></span> | <span data-ttu-id="38d0d-143">F0</span><span class="sxs-lookup"><span data-stu-id="38d0d-143">F0</span></span> | <span data-ttu-id="38d0d-144">Merhaba düşük katmanı ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-144">Start with hello lowest tier.</span></span> <span data-ttu-id="38d0d-145">Çağrıları dışında çalıştırırsanız, tooa daha yüksek katman ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="38d0d-146">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="38d0d-146">**Resource group**</span></span> | <span data-ttu-id="38d0d-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38d0d-147">myResourceGroup</span></span> | <span data-ttu-id="38d0d-148">Kullanım hello aynı kaynak grubu bu öğreticideki tüm hizmetler için.</span><span class="sxs-lookup"><span data-stu-id="38d0d-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="38d0d-149">Tıklatın **oluşturma** toocreate hesabınızı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="38d0d-150">Merhaba hesabı oluşturulduktan sonra yeni Bilişsel Hizmetler hesabı sabitlenmiş toohello panonuz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="38d0d-151">Merhaba hesabında tıklatın **anahtarları**ve ardından hello değerini kopyalayın **anahtar 1** ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="38d0d-152">Bu anahtar tooconnect hello mantığı uygulama tooyour Bilişsel Hizmetler hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![Anahtarlar](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="38d0d-154">Create Hello işlevi</span><span class="sxs-lookup"><span data-stu-id="38d0d-154">Create hello function</span></span>

<span data-ttu-id="38d0d-155">İşlevleri işleme görevlerini bir iş akışındaki logic apps mükemmel şekilde toooffload sağlar.</span><span class="sxs-lookup"><span data-stu-id="38d0d-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="38d0d-156">Bu öğretici, bir HTTP tetiklenen işlevi tooprocess tweet düşünceleri puanları Bilişsel hizmetler ve return bir kategori değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="38d0d-157">İşlevi uygulamanızı genişletin, hello tıklayın  **+**  sonraki çok düğmesini**işlevleri**, hello tıklatın **HTTPTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="38d0d-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="38d0d-158">Tür `CategorizeSentiment` hello işlevi için **adı** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![İşlev uygulamalar dikey penceresinde, İşlevler +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="38d0d-160">Merhaba hello run.csx dosyasının içeriğini koddan hello ile değiştirin ve ardından **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="38d0d-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    <span data-ttu-id="38d0d-161">Bu işlev kodu hello istekte alınan hello düşünceleri puan bağlı bir renk kategori döndürür.</span><span class="sxs-lookup"><span data-stu-id="38d0d-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="38d0d-162">tootest hello işlevi,'ı tıklatın **Test** hello en sağdaki tooexpand hello Test sekmesinde. Değerini yazın `0.2` hello için **istek gövdesinde**ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="38d0d-163">Değerini **kırmızı** hello hello yanıt gövdesinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="38d0d-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Merhaba işlevi hello Azure portal test etme](./media/functions-twitter-email/test.png)

<span data-ttu-id="38d0d-165">Artık düşünceleri puanları kategorilere ayıran bir işlev var.</span><span class="sxs-lookup"><span data-stu-id="38d0d-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="38d0d-166">Ardından, işlevinizi Twitter ve Bilişsel hizmetler hesaplarınızı ile tümleşen bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="38d0d-167">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="38d0d-167">Create a logic app</span></span>   

1. <span data-ttu-id="38d0d-168">İçinde Azure portal Merhaba, hello tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="38d0d-169">Tıklatın **Kurumsal tümleştirme** > **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="38d0d-170">Ardından, olarak hello ayarları kullan hello tablosunda belirtilen denetleyin **PIN toodashboard**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="38d0d-171">Ardından, türü bir **adı** gibi `TweetSentiment`hello tablosunda belirtilen hello ayarları kullanmak, hello koşullarını kabul edin ve denetleyin **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Hello Azure portal mantıksal uygulama oluşturma](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="38d0d-173">Ayar</span><span class="sxs-lookup"><span data-stu-id="38d0d-173">Setting</span></span>      |  <span data-ttu-id="38d0d-174">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="38d0d-174">Suggested value</span></span>   | <span data-ttu-id="38d0d-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38d0d-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="38d0d-176">**Ad**</span><span class="sxs-lookup"><span data-stu-id="38d0d-176">**Name**</span></span> | <span data-ttu-id="38d0d-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="38d0d-177">TweetSentiment</span></span> | <span data-ttu-id="38d0d-178">Uygulamanız için uygun bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="38d0d-179">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="38d0d-179">**Resource group**</span></span> | <span data-ttu-id="38d0d-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38d0d-180">myResourceGroup</span></span> | <span data-ttu-id="38d0d-181">API tooanalyze metin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="38d0d-182">**Konum**</span><span class="sxs-lookup"><span data-stu-id="38d0d-182">**Location**</span></span> | <span data-ttu-id="38d0d-183">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="38d0d-183">East US</span></span> | <span data-ttu-id="38d0d-184">Konum Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="38d0d-185">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="38d0d-185">**Resource group**</span></span> | <span data-ttu-id="38d0d-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38d0d-186">myResourceGroup</span></span> | <span data-ttu-id="38d0d-187">Seçin öncekiyle aynı olan bir kaynak grubunu hello.</span><span class="sxs-lookup"><span data-stu-id="38d0d-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="38d0d-188">Tıklatın **oluşturma** toocreate mantıksal uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="38d0d-189">Merhaba uygulama oluşturulduktan sonra yeni bir mantıksal uygulama sabitlenmiş toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="38d0d-190">Ardından hello Logic Apps Tasarımcı'da, aşağı kaydırın ve hello tıklatın **boş mantıksal uygulama** şablonu.</span><span class="sxs-lookup"><span data-stu-id="38d0d-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Boş Logic Apps şablon](media/functions-twitter-email/blank.png)

<span data-ttu-id="38d0d-192">Artık hello Logic Apps Tasarımcısı tooadd hizmetler ve tetikleyiciler tooyour uygulamasını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="38d0d-193">TooTwitter Bağlan</span><span class="sxs-lookup"><span data-stu-id="38d0d-193">Connect tooTwitter</span></span>

<span data-ttu-id="38d0d-194">İlk olarak, bir bağlantı tooyour Twitter hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="38d0d-195">Merhaba mantıksal uygulama hello uygulama toorun tetiklemek tweet'leri için yoklar.</span><span class="sxs-lookup"><span data-stu-id="38d0d-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="38d0d-196">Merhaba Tasarımcısı'nda hello tıklayın **Twitter** hello'ı tıklatın ve hizmeti **yeni tweet zaman nakledilir** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="38d0d-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="38d0d-197">Tooyour Twitter hesabıyla oturum açın ve Logic Apps toouse hesabınızı yetkisi verin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="38d0d-198">Merhaba tabloda belirtildiği gibi Hello Twitter tetikleyici ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Twitter Bağlayıcısı ayarları](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="38d0d-200">Ayar</span><span class="sxs-lookup"><span data-stu-id="38d0d-200">Setting</span></span>      |  <span data-ttu-id="38d0d-201">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="38d0d-201">Suggested value</span></span>   | <span data-ttu-id="38d0d-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38d0d-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="38d0d-203">**Arama metni**</span><span class="sxs-lookup"><span data-stu-id="38d0d-203">**Search text**</span></span> | <span data-ttu-id="38d0d-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="38d0d-204">#Azure</span></span> | <span data-ttu-id="38d0d-205">Seçilen hello aralığa toogenerate yeni tweet'leri için yeterince popüler bir hashtag kullanın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="38d0d-206">Hello ücretsiz katmanı ve, diyez kullanarak çok popüler olduğunda, hızlı bir şekilde hello işlemleri Bilişsel hizmetler hesabınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38d0d-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="38d0d-207">**Sıklık**</span><span class="sxs-lookup"><span data-stu-id="38d0d-207">**Frequency**</span></span> | <span data-ttu-id="38d0d-208">Dakika</span><span class="sxs-lookup"><span data-stu-id="38d0d-208">Minute</span></span> | <span data-ttu-id="38d0d-209">Merhaba sıklığı birimi twitter yoklama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="38d0d-210">**Aralığı**</span><span class="sxs-lookup"><span data-stu-id="38d0d-210">**Interval**</span></span> | <span data-ttu-id="38d0d-211">15</span><span class="sxs-lookup"><span data-stu-id="38d0d-211">15</span></span> | <span data-ttu-id="38d0d-212">Merhaba sıklığı birimlerindeki Twitter istekleri arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="38d0d-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="38d0d-213">Tıklatın **kaydetmek** tooconnect tooyour Twitter hesabı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="38d0d-214">Uygulamanızı bağlı tooTwitter sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="38d0d-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="38d0d-215">Ardından, tootext analytics toodetect hello düşünceleri toplanan tweet'leri, bağlanın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="38d0d-216">Düşünceleri algılama ekleme</span><span class="sxs-lookup"><span data-stu-id="38d0d-216">Add sentiment detection</span></span>

1. <span data-ttu-id="38d0d-217">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Yeni adım ve bir eylem Ekle](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="38d0d-219">İçinde **bir eylem seçin**, tıklatın **metin analizi**ve ardından hello **düşünceleri algılamak** eylem.</span><span class="sxs-lookup"><span data-stu-id="38d0d-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Düşünceleri Algıla](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="38d0d-221">Bir bağlantı adı gibi yazın `MyCognitiveServicesConnection`kaydedilen Bilişsel Hizmetler hesabı için başlangıç anahtarını yapıştırın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="38d0d-222">Tıklatın **metin tooanalyze** > **Tweet metin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Düşünceleri Algıla](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="38d0d-224">Düşünceleri algılama yapılandırılır, hello düşünceleri puan çıktısını kullanan bir bağlantı tooyour işlevi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38d0d-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="38d0d-225">Düşünceleri çıktı tooyour işlevi Bağlan</span><span class="sxs-lookup"><span data-stu-id="38d0d-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="38d0d-226">Hello Logic Apps Tasarımcı'da, tıklatın **yeni adım** > **Eylem Ekle**ve ardından **Azure işlevleri**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="38d0d-227">Tıklatın **bir Azure işlevi seçin**seçin hello **CategorizeSentiment** daha önce oluşturduğunuz işlevi.</span><span class="sxs-lookup"><span data-stu-id="38d0d-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Bir Azure işlevi Seç gösteren azure işlevi kutusu](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="38d0d-229">İçinde **iste gövde**, tıklatın **puan** ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Puan](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="38d0d-231">Şimdi, düşünceleri puan hello mantığı uygulamadan gönderildiğinde işlevinizi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="38d0d-232">Ren kodlu bir kategori toohello mantıksal uygulama hello fonksiyonu tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="38d0d-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="38d0d-233">Sonra düşünceleri değeri, gönderilen bir e-posta bildirimi ekleyin **kırmızı** hello işlevinden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="38d0d-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="38d0d-234">E-posta bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="38d0d-234">Add email notifications</span></span>

<span data-ttu-id="38d0d-235">Merhaba son hello iş akışının bir parçası olduğunda tootrigger bir e-posta olarak hello düşünceleri puanlanır _kırmızı_.</span><span class="sxs-lookup"><span data-stu-id="38d0d-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="38d0d-236">Bu konuda bir Outlook.com bağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="38d0d-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="38d0d-237">Benzer adımları toouse Gmail veya Office 365 Outlook bağlayıcı gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38d0d-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="38d0d-238">Hello Logic Apps Tasarımcı'da, tıklatın **yeni adım** > **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="38d0d-239">Tıklatın **bir değer seçin**, ardından **gövde**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="38d0d-240">Seçin **eşittir**, tıklatın **bir değer seçin** ve türü `RED`, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="38d0d-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Bir koşul toohello mantıksal uygulama ekleyin.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="38d0d-242">İçinde **Evet ise, hiçbir şey yapma**, tıklatın **Eylem Ekle**, aramak `outlook.com`, tıklatın **bir e-posta Gönder**ve tooyour Outlook.com hesap oturum.</span><span class="sxs-lookup"><span data-stu-id="38d0d-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Merhaba koşul için bir eylem seçin.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="38d0d-244">Bir Outlook.com hesabınız yoksa, Gmail veya Office 365 Outlook gibi başka bir bağlayıcı seçebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="38d0d-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="38d0d-245">Merhaba, **bir e-posta Gönder** eylem olarak hello e-posta ayarları kullan hello tablosunda belirtilen.</span><span class="sxs-lookup"><span data-stu-id="38d0d-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Merhaba e-posta e-posta eylemin hello göndermek için yapılandırın.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="38d0d-247">Ayar</span><span class="sxs-lookup"><span data-stu-id="38d0d-247">Setting</span></span>      |  <span data-ttu-id="38d0d-248">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="38d0d-248">Suggested value</span></span>   | <span data-ttu-id="38d0d-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38d0d-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="38d0d-250">**Hedef**</span><span class="sxs-lookup"><span data-stu-id="38d0d-250">**To**</span></span> | <span data-ttu-id="38d0d-251">E-posta adresinizi yazın</span><span class="sxs-lookup"><span data-stu-id="38d0d-251">Type your email address</span></span> | <span data-ttu-id="38d0d-252">Merhaba bildirim aldığı hello e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="38d0d-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="38d0d-253">**Konu**</span><span class="sxs-lookup"><span data-stu-id="38d0d-253">**Subject**</span></span> | <span data-ttu-id="38d0d-254">Negatif tweet düşünceleri algılandı</span><span class="sxs-lookup"><span data-stu-id="38d0d-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="38d0d-255">Merhaba e-posta bildirimi Hello konu satırı.</span><span class="sxs-lookup"><span data-stu-id="38d0d-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="38d0d-256">**Gövde**</span><span class="sxs-lookup"><span data-stu-id="38d0d-256">**Body**</span></span> | <span data-ttu-id="38d0d-257">Tweet metin, konumu</span><span class="sxs-lookup"><span data-stu-id="38d0d-257">Tweet text, Location</span></span> | <span data-ttu-id="38d0d-258">Merhaba tıklatın **Tweet metin** ve **konumu** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="38d0d-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="38d0d-259">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-259">Click **Save**.</span></span>

<span data-ttu-id="38d0d-260">Merhaba iş akışı tamamlandığına göre hello mantıksal uygulama etkinleştirin ve iş yerindeki hello işlevine bakın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="38d0d-261">Test hello iş akışı</span><span class="sxs-lookup"><span data-stu-id="38d0d-261">Test hello workflow</span></span>

1. <span data-ttu-id="38d0d-262">Hello mantığı Uygulama Tasarımcısı'de, tıklatın **çalıştırmak** toostart hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="38d0d-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="38d0d-263">Merhaba sol sütunda tıklatın **genel bakış** hello mantıksal uygulama toosee hello durumu.</span><span class="sxs-lookup"><span data-stu-id="38d0d-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Mantıksal uygulama yürütme durumu](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="38d0d-265">(İsteğe bağlı) Merhaba çalışır toosee hello yürütme ayrıntılarını birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="38d0d-266">Git tooyour işlevi, hello günlüklerini görüntülemek ve düşünceleri değerleri alınan ve işlenen olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![İşlev günlüklerini görüntüle](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="38d0d-268">Potansiyel olarak negatif düşünceleri algılandığında, bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="38d0d-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="38d0d-269">Bir e-posta almadıysanız, her zaman hello işlevi kod tooreturn kırmızı değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38d0d-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="38d0d-270">E-posta bildirimleri doğruladıktan sonra geri toohello özgün kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="38d0d-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="38d0d-271">Bu öğreticiyi tamamladıktan sonra hello mantıksal uygulama devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38d0d-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="38d0d-272">Merhaba uygulama devre dışı bırakarak yürütmeleri için kartınızdan ve Bilişsel hizmetler hesabınızda hello işlemleri kullanarak kaçının.</span><span class="sxs-lookup"><span data-stu-id="38d0d-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="38d0d-273">Şimdi ne kadar kolay toointegrate işlevleri Logic Apps akışına olduğunu gördünüz.</span><span class="sxs-lookup"><span data-stu-id="38d0d-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="38d0d-274">Merhaba mantıksal uygulama devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="38d0d-274">Disable hello logic app</span></span>

<span data-ttu-id="38d0d-275">toodisable hello mantıksal uygulama'ı tıklatın **genel bakış** ve ardından **devre dışı** Merhaba ekranında hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="38d0d-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="38d0d-276">Çalıştıran ve hello uygulama silmeden ücretlerinin yansıtılmasını hello mantıksal uygulama durdurur.</span><span class="sxs-lookup"><span data-stu-id="38d0d-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![İşlev günlükleri](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="38d0d-278">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38d0d-278">Next steps</span></span>

<span data-ttu-id="38d0d-279">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="38d0d-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38d0d-280">Bilişsel Hizmetler hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="38d0d-281">Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="38d0d-282">TooTwitter bağlayan bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d0d-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="38d0d-283">Düşünceleri algılama toohello mantıksal uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="38d0d-284">Merhaba mantığı uygulama toohello işlevi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="38d0d-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="38d0d-285">Merhaba işlevi hello yanıttan dayalı bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="38d0d-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="38d0d-286">Toohello sonraki öğretici toolearn nasıl ilerlemek için işlevinizi toocreate sunucusuz bir API.</span><span class="sxs-lookup"><span data-stu-id="38d0d-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="38d0d-287">Azure İşlevlerini kullanarak sunucusuz bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="38d0d-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="38d0d-288">Logic Apps hakkında daha fazla toolearn bkz [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="38d0d-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>


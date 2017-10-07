---
title: "aaaScenario - müşteri öngörüleri Panosu Azure sunucusuz ile oluşturma | Microsoft Docs"
description: "Nasıl bir örnek bir Pano toomanage müşteri geri bildirim, sosyal veriler ve Azure Logic Apps ve Azure işlevleri ile daha fazla oluşturabilirsiniz."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="4af25-103">Azure işlevleri ve Azure Logic Apps ile gerçek zamanlı müşteri öngörüleri panosu oluşturun</span><span class="sxs-lookup"><span data-stu-id="4af25-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="4af25-104">Azure sunucusuz araçları altyapısıyla ilgili toothink gerek kalmadan güçlü özellikleri tooquickly hello bulutta yapı ve ana bilgisayar uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4af25-104">Azure Serverless tools provide powerful capabilities tooquickly build and host applications in hello cloud, without having toothink about infrastructure.</span></span>  <span data-ttu-id="4af25-105">Bu senaryoda, bir Pano tootrigger müşteri geri bildirimi oluşturur, machine learning ile geribildirim çözümlemek ve Power BI veya Azure Data Lake gibi bir kaynak Öngörüler yayımlama.</span><span class="sxs-lookup"><span data-stu-id="4af25-105">In this scenario, we will create a dashboard tootrigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-hello-scenario-and-tools-used"></a><span data-ttu-id="4af25-106">Merhaba senaryo ve kullanılan Araçları'na genel bakış</span><span class="sxs-lookup"><span data-stu-id="4af25-106">Overview of hello scenario and tools used</span></span>

<span data-ttu-id="4af25-107">Bu çözüm tooimplement sipariş, Azure içinde sunucusuz uygulamaların hello iki anahtar bileşenleri özelliğinden yararlanır: [Azure işlevleri](https://azure.microsoft.com/services/functions/) ve [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="4af25-107">In order tooimplement this solution, we will leverage hello two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="4af25-108">Logic Apps hello bulutta sunucusuz iş akışı altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="4af25-108">Logic Apps is a serverless workflow engine in hello cloud.</span></span>  <span data-ttu-id="4af25-109">Orchestration sunucusuz bileşenlerinde sağlar ve ayrıca tooover 100 Hizmetleri ve API bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4af25-109">It provides orchestration across serverless components, and also connects tooover 100 services and APIs.</span></span>  <span data-ttu-id="4af25-110">Bu senaryoda, müşterilerin görüşleri üzerinde bir mantıksal uygulama tootrigger oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="4af25-110">For this scenario, we will create a logic app tootrigger on feedback from customers.</span></span>  <span data-ttu-id="4af25-111">Tanımlandığında toocustomer geri bildirim yardımcı olabilecek hello bağlayıcılar Outlook.com, Office 365, anket Monkey, Twitter ve bir HTTP isteği bazıları [bir web formundan](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="4af25-111">Some of hello connectors that can assist in reacting toocustomer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="4af25-112">Merhaba iş akışı için aşağıdaki biz diyez Twitter'da izlenir.</span><span class="sxs-lookup"><span data-stu-id="4af25-112">For hello workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="4af25-113">İşlevler hello bulutta sunucusuz işlem sağlar.</span><span class="sxs-lookup"><span data-stu-id="4af25-113">Functions provide serverless compute in hello cloud.</span></span>  <span data-ttu-id="4af25-114">Bu senaryoda, bir dizi önceden tanımlanmış anahtar sözcükleri dayalı müşterilerden Azure işlevleri tooflag tweet'leri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="4af25-114">In this scenario, we will use Azure Functions tooflag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="4af25-115">çözümün tamamında Hello olabilir [Visual Studio'da derleme](logic-apps-deploy-from-vs.md) ve [kaynak şablon bir parçası olarak dağıtılan](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="4af25-115">hello entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="4af25-116">Ayrıca videosu hello senaryonun olan [Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="4af25-116">There is also video walkthrough of hello scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a><span data-ttu-id="4af25-117">Müşteri verilerine Hello mantığı uygulama tootrigger derleme</span><span class="sxs-lookup"><span data-stu-id="4af25-117">Build hello logic app tootrigger on customer data</span></span>

<span data-ttu-id="4af25-118">Sonra [bir mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md) Visual Studio veya hello Azure portalı:</span><span class="sxs-lookup"><span data-stu-id="4af25-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or hello Azure portal:</span></span>

1. <span data-ttu-id="4af25-119">İçin bir tetikleyici eklemek **üzerinde yeni Tweet'leri** Twitter gelen</span><span class="sxs-lookup"><span data-stu-id="4af25-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="4af25-120">Merhaba tetikleyici toolisten tootweets bir anahtar sözcüğü veya diyez yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4af25-120">Configure hello trigger toolisten tootweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4af25-121">Merhaba yinelenme hello tetikleyici özellikte yoklama tabanlı tetikleyiciler üzerinde yeni öğeler için hello mantıksal uygulama hangi sıklıkta denetleyeceğini belirler</span><span class="sxs-lookup"><span data-stu-id="4af25-121">hello recurrence property on hello trigger will determine how frequently hello logic app checks for new items on polling-based triggers</span></span>

   ![Twitter tetikleyici örneği][1]

<span data-ttu-id="4af25-123">Bu uygulama artık tüm yeni tweet'leri ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="4af25-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="4af25-124">Biz sonra tweet verileri alabilir ve ifade hello düşünceleri daha iyi anlamak.</span><span class="sxs-lookup"><span data-stu-id="4af25-124">We can then take that tweet data and understand more of hello sentiment expressed.</span></span>  <span data-ttu-id="4af25-125">Merhaba bu için kullandığımız [Azure Bilişsel hizmeti](https://azure.microsoft.com/services/cognitive-services/) toodetect düşünceleri metin.</span><span class="sxs-lookup"><span data-stu-id="4af25-125">For this we use hello [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) toodetect sentiment of text.</span></span>

1. <span data-ttu-id="4af25-126">Tıklatın **yeni adım**</span><span class="sxs-lookup"><span data-stu-id="4af25-126">Click **New Step**</span></span>
1. <span data-ttu-id="4af25-127">Seçin veya arama Merhaba **metin analizi** Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4af25-127">Select or search for hello **Text Analytics** connector</span></span>
1. <span data-ttu-id="4af25-128">Select hello **algılamak düşünceleri** işlemi</span><span class="sxs-lookup"><span data-stu-id="4af25-128">Select hello **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="4af25-129">İstenirse, hello metin Analytics hizmeti için geçerli bir Bilişsel hizmetler anahtarı sağlayın</span><span class="sxs-lookup"><span data-stu-id="4af25-129">If prompted, provide a valid Cognitive Services key for hello Text Analytics service</span></span>
1. <span data-ttu-id="4af25-130">Merhaba eklemek **Tweet metin** metin tooanalyze hello gibi.</span><span class="sxs-lookup"><span data-stu-id="4af25-130">Add hello **Tweet Text** as hello text tooanalyze.</span></span>

<span data-ttu-id="4af25-131">Biz hello tweet veri ve öngörü hello tweet üzerinde sahip olduğunuza göre diğer bağlayıcıları çeşitli uygun olabilir:</span><span class="sxs-lookup"><span data-stu-id="4af25-131">Now that we have hello tweet data, and insights on hello tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="4af25-132">Power BI - satırları tooStreaming veri kümesi ekleyin: görünümü tweet'leri gerçek zamanlı bir Power BI Panoda.</span><span class="sxs-lookup"><span data-stu-id="4af25-132">Power BI - Add Rows tooStreaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="4af25-133">Azure Data Lake - dosya ekleme: müşteri verileri tooan Azure Data Lake dataset tooinclude analytics işleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4af25-133">Azure Data Lake - Append file: Add customer data tooan Azure Data Lake dataset tooinclude in analytics jobs.</span></span>
* <span data-ttu-id="4af25-134">SQL - satırları ekleyin: deposundaki verileri sonraki alma için bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="4af25-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="4af25-135">Boşluk - iletisi gönderin: Eylemler gerektirir olumsuz görüşler slack kanalda uyar.</span><span class="sxs-lookup"><span data-stu-id="4af25-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="4af25-136">Bir Azure işlevi de daha fazla özel işlem hello veri üzerinde kullanılan toodo olabilir.</span><span class="sxs-lookup"><span data-stu-id="4af25-136">An Azure Function can also be used toodo more custom compute on top of hello data.</span></span>

## <a name="enriching-hello-data-with-an-azure-function"></a><span data-ttu-id="4af25-137">Merhaba verilerle zenginleştirmek bir Azure işlevi</span><span class="sxs-lookup"><span data-stu-id="4af25-137">Enriching hello data with an Azure Function</span></span>

<span data-ttu-id="4af25-138">Bir işlev oluşturabilmeniz için önce kimliğinizi uygulamamız Azure aboneliğimiz toohave bir işlev uygulaması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="4af25-138">Before we can create a function, we need toohave a function app in our Azure subscription.</span></span>  <span data-ttu-id="4af25-139">Merhaba portalında bir Azure işlevi oluşturma ile ilgili ayrıntılar için [bulunabilir burada](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4af25-139">Details on creating an Azure Function in hello portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="4af25-140">Doğrudan mantığı uygulamadan adlı bir işlev toobe için bunu ihtiyaçlarını toohave bir HTTP tetiklemek bağlama.</span><span class="sxs-lookup"><span data-stu-id="4af25-140">For a function toobe called directly from a logic app, it needs toohave an HTTP trigger binding.</span></span>  <span data-ttu-id="4af25-141">Merhaba kullanmanızı öneririz **HttpTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="4af25-141">We recommend using hello **HttpTrigger** template.</span></span>

<span data-ttu-id="4af25-142">Bu senaryoda, hello Azure işlevi hello istek gövdesi hello tweet metin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4af25-142">In this scenario, hello request body of hello Azure Function would be hello tweet text.</span></span>  <span data-ttu-id="4af25-143">Bir anahtar sözcük veya tümcecik Hello tweet metin içeriyorsa, hello işlevi kodda mantığı üzerinde yalnızca tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4af25-143">In hello function code, simply define logic on if hello tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="4af25-144">Merhaba işlevi kendisi kadar basit veya karmaşık hello senaryo için gerektiği şekilde tutulması.</span><span class="sxs-lookup"><span data-stu-id="4af25-144">hello function itself could be kept as simple or complex as needed for hello scenario.</span></span>

<span data-ttu-id="4af25-145">Merhaba işlevi Hello sonunda, yalnızca bir yanıt toohello mantıksal uygulama bazı verilerle döndür.</span><span class="sxs-lookup"><span data-stu-id="4af25-145">At hello end of hello function, simply return a response toohello logic app with some data.</span></span>  <span data-ttu-id="4af25-146">Bu basit bir Boole değeri olabilir (örneğin `containsKeyword`), veya karmaşık bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4af25-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Yapılandırılmış Azure işlevi adım][2]

> [!TIP]
> <span data-ttu-id="4af25-148">Karmaşık bir yanıt bir mantıksal uygulama bir işlevden erişirken hello ayrıştırma JSON eylemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4af25-148">When accessing a complex response from a function in a logic app, use hello Parse JSON action.</span></span>

<span data-ttu-id="4af25-149">Merhaba işlevi kaydedildikten sonra yukarıda oluşturduğunuz hello mantıksal uygulama içine eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4af25-149">Once hello function is saved, it can be added into hello logic app created above.</span></span>  <span data-ttu-id="4af25-150">Merhaba mantıksal uygulama içinde:</span><span class="sxs-lookup"><span data-stu-id="4af25-150">In hello logic app:</span></span>

1. <span data-ttu-id="4af25-151">Tooadd tıklatın bir **yeni adım**</span><span class="sxs-lookup"><span data-stu-id="4af25-151">Click tooadd a **New Step**</span></span>
1. <span data-ttu-id="4af25-152">Select hello **Azure işlevleri** Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4af25-152">Select hello **Azure Functions** connector</span></span>
1. <span data-ttu-id="4af25-153">Toochoose var olan işlevi seçin ve oluşturulan toohello işlevi Gözat</span><span class="sxs-lookup"><span data-stu-id="4af25-153">Select toochoose an existing function, and browse toohello function created</span></span>
1. <span data-ttu-id="4af25-154">Hello Gönder **Tweet metin** hello için **istek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="4af25-154">Send in hello **Tweet Text** for hello **Request Body**</span></span>

## <a name="running-and-monitoring-hello-solution"></a><span data-ttu-id="4af25-155">Çalıştıran ve izleme hello çözümü</span><span class="sxs-lookup"><span data-stu-id="4af25-155">Running and monitoring hello solution</span></span>

<span data-ttu-id="4af25-156">Logic Apps içinde sunucusuz düzenlemelerin yazma hello avantajları hello zengin hata ayıklama ve izleme kapasiteleri biridir.</span><span class="sxs-lookup"><span data-stu-id="4af25-156">One of hello benefits of authoring serverless orchestrations in Logic Apps is hello rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="4af25-157">Tüm çalışma (geçerli veya geçmiş) Visual Studio'dan hello Azure portal veya hello REST API ve SDK aracılığıyla görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="4af25-157">Any run (current or historic) can be viewed from within Visual Studio, hello Azure portal, or via hello REST API and SDKs.</span></span>

<span data-ttu-id="4af25-158">Merhaba en kolay yolu tootest bir mantıksal uygulama birini kullanarak hello **çalıştırmak** hello Tasarımcısı'nda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4af25-158">One of hello easiest ways tootest a logic app is using hello **Run** button in hello designer.</span></span>  <span data-ttu-id="4af25-159">Tıklatarak **çalıştırmak** toopoll hello tetikleyici bir olay algılandığında kadar her 5 saniyede devam edecek ve dinamik bir görünüm Çalıştır hello ilerledikçe verin.</span><span class="sxs-lookup"><span data-stu-id="4af25-159">Clicking **Run** will continue toopoll hello trigger every 5 seconds until an event is detected, and give a live view as hello run progresses.</span></span>

<span data-ttu-id="4af25-160">Önceki çalıştırma geçmişlerini hello genel bakış dikey penceresinde hello Azure portal veya hello Visual Studio Cloud Explorer kullanılarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="4af25-160">Previous run histories can be viewed on hello Overview blade in hello Azure portal, or using hello Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="4af25-161">Otomatik dağıtımları için dağıtım şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4af25-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="4af25-162">Bir çözüm geliştirilen sonra yakalanan ve Azure dağıtım şablonu tooany Merhaba Dünya Azure bölgesinde aracılığıyla dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4af25-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template tooany Azure region in hello world.</span></span>  <span data-ttu-id="4af25-163">Bu parametre için de değiştirme bu iş akışı farklı sürümleri için aynı zamanda bu çözümü derleme ve sürüm ardışık düzeninde tümleştirmek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="4af25-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="4af25-164">Bir dağıtım şablonu oluşturma hakkında ayrıntılar bulunabilir [bu makalede](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="4af25-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="4af25-165">Merhaba tüm çözümü tüm bağımlılıkları tek bir şablon olarak yönetilecek şekilde azure işlevleri de hello dağıtım şablonunda - birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4af25-165">Azure Functions can also be incorporated in hello deployment template - so hello entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="4af25-166">Bir işlev dağıtım şablonu örneği hello bulunabilir [Azure Hızlı Başlangıç şablonu deposu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="4af25-166">An example of a function deployment template can be found in hello [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4af25-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4af25-167">Next steps</span></span>

* [<span data-ttu-id="4af25-168">Diğer örnekleri ve senaryoları Azure Logic Apps için bkz.</span><span class="sxs-lookup"><span data-stu-id="4af25-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="4af25-169">Bu çözüm uçtan uca Oluşturma videosu izleme</span><span class="sxs-lookup"><span data-stu-id="4af25-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="4af25-170">Bilgi nasıl bir mantıksal uygulama içinde toohandle ve catch özel durumları</span><span class="sxs-lookup"><span data-stu-id="4af25-170">Learn how toohandle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png
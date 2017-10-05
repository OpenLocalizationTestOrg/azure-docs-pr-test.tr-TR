---
title: "Senaryo - bir müşteri öngörüleri Panosu Azure sunucusuz ile oluşturma | Microsoft Docs"
description: "Müşteri geri bildirimi, sosyal veriler ve Azure Logic Apps ve Azure işlevleri ile daha fazlasını yönetmek için bir Pano nasıl oluşturulacağına ilişkin bir örnek."
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
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="c1669-103">Azure işlevleri ve Azure Logic Apps ile gerçek zamanlı müşteri öngörüleri panosu oluşturun</span><span class="sxs-lookup"><span data-stu-id="c1669-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="c1669-104">Azure sunucusuz araçları hızlı bir şekilde oluşturmak ve bulut uygulamalarında altyapı hakkında düşünmek zorunda kalmadan barındırmak için güçlü özellikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c1669-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="c1669-105">Bu senaryoda, Power BI veya Azure Data Lake gibi bir kaynak müşteri geri bildirimi tetiklemek, machine learning ile geribildirim çözümlemek ve Öngörüler yayımlamak için bir Pano oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c1669-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="c1669-106">Senaryo ve kullanılan Araçları'na genel bakış</span><span class="sxs-lookup"><span data-stu-id="c1669-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="c1669-107">Bu çözümü uygulamak için Azure sunucusuz uygulamalarında iki anahtar bileşenlerinin nden: [Azure işlevleri](https://azure.microsoft.com/services/functions/) ve [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="c1669-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="c1669-108">Logic Apps, bulutta bir sunucusuz iş akışı altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="c1669-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="c1669-109">Orchestration sunucusuz bileşenlerinde sağlar ve ayrıca 100'den Hizmetleri ve API bağlar.</span><span class="sxs-lookup"><span data-stu-id="c1669-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="c1669-110">Bu senaryoda, müşterilerin görüşleri tetiklemek için bir mantıksal uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c1669-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="c1669-111">Müşteri geri bildirimi tepki yardımcı olabilecek bağlayıcılar Outlook.com, Office 365, anket Monkey, Twitter ve bir HTTP isteği bazıları [bir web formundan](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="c1669-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="c1669-112">İş akışı için aşağıdaki biz diyez Twitter'da izlenir.</span><span class="sxs-lookup"><span data-stu-id="c1669-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="c1669-113">Bulutta sunucusuz işlem işlevler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c1669-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="c1669-114">Bu senaryoda, bir dizi önceden tanımlanmış anahtar sözcükleri dayalı müşterilerden tweet'leri bayrak için Azure işlevleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c1669-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="c1669-115">Çözümün tamamında olabilir [Visual Studio'da derleme](logic-apps-deploy-from-vs.md) ve [kaynak şablon bir parçası olarak dağıtılan](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="c1669-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="c1669-116">Ayrıca videosu senaryonun olan [Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="c1669-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="c1669-117">Müşteri verilerine tetiklemek için mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="c1669-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="c1669-118">Sonra [bir mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md) Visual Studio veya Azure Portalı'nda:</span><span class="sxs-lookup"><span data-stu-id="c1669-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="c1669-119">İçin bir tetikleyici eklemek **üzerinde yeni Tweet'leri** Twitter gelen</span><span class="sxs-lookup"><span data-stu-id="c1669-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="c1669-120">Bir anahtar sözcüğü veya diyez tweet'leri dinlemek için tetikleyici yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c1669-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1669-121">Tetikleyici yinelenme özellikte yoklama tabanlı tetikleyiciler üzerinde yeni öğeler için mantıksal uygulama hangi sıklıkta denetleyeceğini belirler</span><span class="sxs-lookup"><span data-stu-id="c1669-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Twitter tetikleyici örneği][1]

<span data-ttu-id="c1669-123">Bu uygulama artık tüm yeni tweet'leri ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="c1669-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="c1669-124">Biz sonra tweet verileri alabilir ve daha fazla ifade düşünceleri anlama.</span><span class="sxs-lookup"><span data-stu-id="c1669-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="c1669-125">Bunun için kullandığımız [Azure Bilişsel hizmet](https://azure.microsoft.com/services/cognitive-services/) metnin düşünceleri algılamak için.</span><span class="sxs-lookup"><span data-stu-id="c1669-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="c1669-126">Tıklatın **yeni adım**</span><span class="sxs-lookup"><span data-stu-id="c1669-126">Click **New Step**</span></span>
1. <span data-ttu-id="c1669-127">Seçin veya arama **metin analizi** Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="c1669-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="c1669-128">Seçin **algılamak düşünceleri** işlemi</span><span class="sxs-lookup"><span data-stu-id="c1669-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="c1669-129">İstenirse, metin Analytics hizmeti için geçerli bir Bilişsel hizmetler anahtarı sağlayın</span><span class="sxs-lookup"><span data-stu-id="c1669-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="c1669-130">Ekleme **Tweet metin** çözümlemek için metin olarak.</span><span class="sxs-lookup"><span data-stu-id="c1669-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="c1669-131">Biz tweet veri ve Öngörüler üzerinde tweet sahip olduğunuza göre diğer bağlayıcıları çeşitli uygun olabilir:</span><span class="sxs-lookup"><span data-stu-id="c1669-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="c1669-132">Power BI - akış veri kümesine satırları ekleyin: görünümü tweet'leri gerçek zamanlı bir Power BI Panoda.</span><span class="sxs-lookup"><span data-stu-id="c1669-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="c1669-133">Azure Data Lake - dosya ekleme: müşteri verilerini analytics işlerini dahil etmek için bir Azure Data Lake veri kümesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1669-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="c1669-134">SQL - satırları ekleyin: deposundaki verileri sonraki alma için bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c1669-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="c1669-135">Boşluk - iletisi gönderin: Eylemler gerektirir olumsuz görüşler slack kanalda uyar.</span><span class="sxs-lookup"><span data-stu-id="c1669-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="c1669-136">Bir Azure işlevi, verileri üzerinde daha fazla özel işlem yapmak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1669-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="c1669-137">Bir Azure işlevi verilerle zenginleştirmek</span><span class="sxs-lookup"><span data-stu-id="c1669-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="c1669-138">Bir işlev oluşturabilmeniz için önce uygulamamız Azure aboneliğimiz bir işlev uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1669-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="c1669-139">Portalda bir Azure işlevi oluşturma ile ilgili ayrıntılar için [bulunabilir burada](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c1669-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="c1669-140">Bir HTTP sağlamak gereken doğrudan mantığı uygulamadan çağrılacak işlev için bağlama tetikler.</span><span class="sxs-lookup"><span data-stu-id="c1669-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="c1669-141">Kullanmanızı öneririz **HttpTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="c1669-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="c1669-142">Bu senaryoda, istek gövdesini Azure işlevinin tweet metin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c1669-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="c1669-143">Bir anahtar sözcük veya tümcecik tweet metin içeriyorsa, işlev kodu mantığı üzerinde yalnızca tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c1669-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="c1669-144">İşlev kadar basit veya karmaşık senaryo için gerektiği şekilde tutulması.</span><span class="sxs-lookup"><span data-stu-id="c1669-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="c1669-145">İşlev sonunda, yalnızca bazı verilerle mantıksal uygulama için bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="c1669-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="c1669-146">Bu basit bir Boole değeri olabilir (örneğin `containsKeyword`), veya karmaşık bir nesne.</span><span class="sxs-lookup"><span data-stu-id="c1669-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Yapılandırılmış Azure işlevi adım][2]

> [!TIP]
> <span data-ttu-id="c1669-148">Karmaşık bir yanıt bir mantıksal uygulama bir işlevden erişirken ayrıştırma JSON eylemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1669-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="c1669-149">İşlev kaydedildikten sonra yukarıda oluşturduğunuz mantıksal uygulama içine eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c1669-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="c1669-150">Mantıksal uygulama:</span><span class="sxs-lookup"><span data-stu-id="c1669-150">In the logic app:</span></span>

1. <span data-ttu-id="c1669-151">Eklemek için tıklatın bir **yeni adım**</span><span class="sxs-lookup"><span data-stu-id="c1669-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="c1669-152">Seçin **Azure işlevleri** Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="c1669-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="c1669-153">Var olan işlevi seçin ve oluşturulan işlevi gözatmak için seçin</span><span class="sxs-lookup"><span data-stu-id="c1669-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="c1669-154">Gönder **Tweet metin** için **istek gövdesinde**</span><span class="sxs-lookup"><span data-stu-id="c1669-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="c1669-155">Çalıştıran ve izleme çözümü</span><span class="sxs-lookup"><span data-stu-id="c1669-155">Running and monitoring the solution</span></span>

<span data-ttu-id="c1669-156">Logic Apps içinde sunucusuz düzenlemelerin yazma avantajlarını zengin hata ayıklama ve izleme olanakları biridir.</span><span class="sxs-lookup"><span data-stu-id="c1669-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="c1669-157">Tüm çalışma (geçerli veya geçmiş) Visual Studio'dan Azure portal ya da SDK'ları ve REST API aracılığıyla görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="c1669-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="c1669-158">Bir mantıksal uygulama test etmek için en kolay yollarından biri kullanarak **çalıştırmak** Tasarımcısı'nda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c1669-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="c1669-159">Tıklatarak **çalıştırmak** tetikleyici bir olay algılandığında kadar her 5 saniyede yoklamak ve çalışma ilerledikçe dinamik bir görünüm vermek devam eder.</span><span class="sxs-lookup"><span data-stu-id="c1669-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="c1669-160">Genel Bakış dikey penceresinde Azure portalında veya Visual Studio Cloud Explorer'ı kullanarak önceki çalıştırma geçmişlerini görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="c1669-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="c1669-161">Otomatik dağıtımları için dağıtım şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c1669-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="c1669-162">Bir çözüm geliştirilen sonra yakalanan ve dünya Azure herhangi bir bölgede bir Azure dağıtım şablonu aracılığıyla dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c1669-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="c1669-163">Bu parametre için de değiştirme bu iş akışı farklı sürümleri için aynı zamanda bu çözümü derleme ve sürüm ardışık düzeninde tümleştirmek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c1669-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="c1669-164">Bir dağıtım şablonu oluşturma hakkında ayrıntılar bulunabilir [bu makalede](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="c1669-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="c1669-165">Çözümün tamamında tüm bağımlılıkları tek bir şablon olarak yönetilecek şekilde azure işlevleri de dağıtım şablonu - birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c1669-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="c1669-166">Bir işlev dağıtım şablonu örneği bulunabilir [Azure Hızlı Başlangıç şablonu deposu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="c1669-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1669-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1669-167">Next steps</span></span>

* [<span data-ttu-id="c1669-168">Diğer örnekleri ve senaryoları Azure Logic Apps için bkz.</span><span class="sxs-lookup"><span data-stu-id="c1669-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="c1669-169">Bu çözüm uçtan uca Oluşturma videosu izleme</span><span class="sxs-lookup"><span data-stu-id="c1669-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="c1669-170">İşlemek ve bir mantıksal uygulama içinde özel durumlarını yakalama hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c1669-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png
---
title: "aaaAutomate Azure Application Insights Microsoft Flow işler."
description: "Microsoft Flow nasıl kullanabileceğinizi öğrenin tooquickly hello Application Insights Bağlayıcısı'nı kullanarak yinelenebilir işlemleri otomatikleştirme."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="d5ec5-103">İçin Microsoft Flow hello Bağlayıcısı ile Azure Application Insights süreçleri otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="d5ec5-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="d5ec5-104">Kendiniz art arda hello hizmetinizi düzgün çalıştığından, telemetri verileri toocheck aynı sorguları çalıştırma bulurum?</span><span class="sxs-lookup"><span data-stu-id="d5ec5-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="d5ec5-105">Görünümlü tooautomate eğilimleri ve daha fazla bilgi bulmak için bu sorgular ve ardından bunları geçici kendi iş akışları oluşturmak mı? Hello Azure Application Insights (Önizleme) için Microsoft Flow hello doğru aracı bu amaçlar için Bağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="d5ec5-106">İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan artık çok sayıda süreçlerini otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="d5ec5-107">Application Insights eylemini kullanarak bir akış oluşturduktan sonra hello akış uygulama Öngörüler Analytics sorgunuzu otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="d5ec5-108">Ek Eylemler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-108">You can add additional actions as well.</span></span> <span data-ttu-id="d5ec5-109">Microsoft Flow Eylemler yüzlerce kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="d5ec5-110">Örneğin, Microsoft Flow tooautomatically Gönder bir e-posta bildirimi kullanın ya da Visual Studio Team Services içinde oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="d5ec5-111">Merhaba biri birçok kullanabilirsiniz [şablonları](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) Microsoft Flow hello bağlayıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="d5ec5-112">Bu şablonları bir akış oluşturma hello işlemi hızlandırmak.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="d5ec5-113">Bir akış için Application Insights oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5ec5-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="d5ec5-114">Bu öğreticide, nasıl bir web uygulaması için hello verilerdeki hello Analytics otomatik küme algoritması toogroup kullanan bir akış toocreate öznitelikleri öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="d5ec5-115">Merhaba akış hello sonuçları e-posta ile tek bir örneği nasıl Microsoft Flow ve uygulama Öngörüler Analytics birlikte kullanabileceğiniz otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="d5ec5-116">1. adım: bir akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5ec5-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="d5ec5-117">Çok oturum[Microsoft Flow](http://flow.microsoft.com)ve ardından **My akar**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="d5ec5-118">Tıklatın **bir akışı boş iken oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="d5ec5-119">2. adım: akışınız için bir Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5ec5-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="d5ec5-120">Seçin **zamanlama**ve ardından **çizelgesi - yinelenme**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="d5ec5-121">Merhaba, **sıklığı** kutusunda **gün**ve hello **aralığı** kutusuna **1**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow tetikleyici iletişim kutusu](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="d5ec5-123">3. adım: Application Insights Eylem Ekle</span><span class="sxs-lookup"><span data-stu-id="d5ec5-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="d5ec5-124">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="d5ec5-125">Arama **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="d5ec5-126">Tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Analytics sorgu penceresi](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="d5ec5-128">4. adım: tooan Application Insights kaynağı bağlanma</span><span class="sxs-lookup"><span data-stu-id="d5ec5-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="d5ec5-129">toocomplete Bu adım, kaynak için bir uygulama kimliği ve bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="d5ec5-130">Bunları Azure portal hello hello Aşağıdaki diyagramda gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5ec5-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Hello Azure portalında uygulama kimliği](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="d5ec5-132">Merhaba uygulama kimliği ve API anahtarı ile birlikte bağlantınız için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Microsoft Flow bağlantı penceresi](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="d5ec5-134">5. adım: hello Analytics sorgu ve grafik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="d5ec5-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="d5ec5-135">Bu örnek sorgu hello başarısız istekleri hello son gün içinde seçer ve bunları hello işleminin bir parçası oluşan özel durumları ile karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="d5ec5-136">Analytics bunları hello operation_Id tanımlayıcısına göre hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="d5ec5-137">Merhaba sorgu hello autocluster algoritması kullanılarak hello sonuçları sonra kesim.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="d5ec5-138">Kendi sorguları oluşturduğunuzda, tooyour akış eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="d5ec5-139">Analytics sorgu aşağıdaki hello ekleyin ve ardından hello HTML tablo grafik türü seçin.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Analytics sorgu yapılandırma penceresi](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="d5ec5-141">6. adım: hello akış toosend e-posta yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d5ec5-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="d5ec5-142">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="d5ec5-143">Arama **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="d5ec5-144">Tıklatın **Office 365 Outlook – bir e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook seçim penceresi](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="d5ec5-146">Merhaba, **bir e-posta Gönder** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="d5ec5-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="d5ec5-147">a.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-147">a.</span></span> <span data-ttu-id="d5ec5-148">Merhaba alıcı Hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="d5ec5-149">b.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-149">b.</span></span> <span data-ttu-id="d5ec5-150">Merhaba e-posta için bir konu yazın.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="d5ec5-151">c.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-151">c.</span></span> <span data-ttu-id="d5ec5-152">Hello herhangi bir yere tıklayın **gövde** kutusuna ve ardından hello sağdaki açan hello dinamik içerik menüsünden seçin **gövde**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="d5ec5-153">d.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-153">d.</span></span> <span data-ttu-id="d5ec5-154">Tıklatın **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-154">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook yapılandırma](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="d5ec5-156">Merhaba dinamik içerik menüsünden aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="d5ec5-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="d5ec5-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-157">a.</span></span> <span data-ttu-id="d5ec5-158">Seçin **ek adı**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="d5ec5-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-159">b.</span></span> <span data-ttu-id="d5ec5-160">Seçin **ek içerik**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="d5ec5-161">c.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-161">c.</span></span> <span data-ttu-id="d5ec5-162">Merhaba, **HTML'dir** kutusunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 e-posta yapılandırma penceresi](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="d5ec5-164">7. adım: Kaydetmek ve akışınız test</span><span class="sxs-lookup"><span data-stu-id="d5ec5-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="d5ec5-165">Merhaba, **Akış adı** kutusuna akışınız için bir ad ekleyin ve ardından **akışı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="d5ec5-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Akış oluşturma penceresi](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="d5ec5-167">Bu eylemin hello tetikleyici toorun için bekleyebilir veya hello akış hemen göre çalıştırabilirsiniz [isteğe bağlı çalışan hello tetikleyici](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="d5ec5-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="d5ec5-168">Merhaba akışı çalıştığında, hello e-posta listesinde belirtilen hello alıcılar hello şuna benzeyen bir e-posta iletisi alırsınız:</span><span class="sxs-lookup"><span data-stu-id="d5ec5-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Örnek e-posta](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="d5ec5-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5ec5-170">Next steps</span></span>

- <span data-ttu-id="d5ec5-171">Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="d5ec5-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="d5ec5-172">Daha fazla bilgi edinmek [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d5ec5-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->






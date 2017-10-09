---
title: "aaaAutomate Logic Apps kullanarak Azure Application Insights işler."
description: "Nasıl hızlı bir şekilde yinelenebilir işlemler hello Application Insights Bağlayıcısı tooyour mantıksal uygulama ekleyerek otomatikleştirebilirsiniz öğrenin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="5d381-103">Logic Apps kullanarak Application Insights işlemlerini otomatik hale</span><span class="sxs-lookup"><span data-stu-id="5d381-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="5d381-104">Kendiniz hizmetinizi düzgün çalışıp çalışmadığını Merhaba, telemetri verileri toocheck aynı sorgu tekrar tekrar çalıştırmayı bulurum?</span><span class="sxs-lookup"><span data-stu-id="5d381-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="5d381-105">Görünümlü tooautomate eğilimleri ve daha fazla bilgi bulmak için bu sorgular ve ardından bunları geçici kendi iş akışları oluşturmak mı? Logic Apps için Hello Azure Application Insights Bağlayıcısı (Önizleme) hello sağ bu amaçla aracıdır.</span><span class="sxs-lookup"><span data-stu-id="5d381-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="5d381-106">İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan çeşitli işlemleri otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d381-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="5d381-107">Mantıksal uygulama oluşturma hello Application Insights ile bağlayıcı tooquickly otomatikleştirmek herhangi bir Application Insights işlem.</span><span class="sxs-lookup"><span data-stu-id="5d381-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="5d381-108">Ek Eylemler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d381-108">You can add additional actions as well.</span></span> <span data-ttu-id="5d381-109">Azure App Service Logic Apps özelliğini Hello Eylemler yüzlerce kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="5d381-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="5d381-110">Örneğin, bir mantıksal uygulama kullanarak, yapabilir otomatik olarak bir e-posta bildirim göndermek veya bir hata Visual Studio Team Services içinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d381-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="5d381-111">Merhaba birini kullanılabilir birçok kullanabilirsiniz [şablonları](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp mantıksal uygulamanızı oluşturma hello işlemini hızlandırabilir.</span><span class="sxs-lookup"><span data-stu-id="5d381-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="5d381-112">Application Insights için bir mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d381-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="5d381-113">Bu öğreticide, nasıl toocreate hello Analytics autocluster algoritması toogroup kullanan bir mantıksal uygulama bir web uygulaması için hello veri öznitelikleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5d381-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="5d381-114">Merhaba akış hello sonuçları e-posta ile tek bir örneği nasıl uygulama Öngörüler analizi ve Logic Apps birlikte kullanabileceğiniz otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="5d381-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="5d381-115">1. adım: bir mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d381-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="5d381-116">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d381-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5d381-117">Merhaba, **yeni** bölmesinde, **Web + mobil**ve ardından **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="5d381-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Yeni mantıksal uygulama penceresi](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="5d381-119">2. adım: mantıksal uygulamanız için bir Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d381-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="5d381-120">Merhaba, **mantığı Uygulama Tasarımcısı** penceresi altında **Başlat sahip ortak bir tetikleyici**seçin **yineleme**.</span><span class="sxs-lookup"><span data-stu-id="5d381-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı penceresi](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="5d381-122">Merhaba, **sıklığı** kutusunda **gün** ve ardından hello **aralığı** kutusuna **1**.</span><span class="sxs-lookup"><span data-stu-id="5d381-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı "Recurrence" penceresi](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="5d381-124">3. adım: Application Insights Eylem Ekle</span><span class="sxs-lookup"><span data-stu-id="5d381-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="5d381-125">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5d381-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="5d381-126">Merhaba, **bir eylem seçin** arama kutusuna **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5d381-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="5d381-127">Altında **Eylemler**, tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="5d381-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı penceresinin "bir eylem seçin"](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="5d381-129">4. adım: tooan Application Insights kaynağı bağlanma</span><span class="sxs-lookup"><span data-stu-id="5d381-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="5d381-130">toocomplete Bu adım, kaynak için bir uygulama kimliği ve bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d381-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="5d381-131">Bunları Azure portal hello hello Aşağıdaki diyagramda gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5d381-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Hello Azure portalında uygulama kimliği](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="5d381-133">Bağlantı, hello uygulama kimliği ve hello API anahtarı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5d381-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Mantıksal Uygulama Tasarımcısı akış bağlantısı penceresi](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="5d381-135">5. adım: hello Analytics sorgu ve grafik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="5d381-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="5d381-136">Aşağıdaki örneğine hello hello sorgu hello başarısız istekleri hello son gün içinde seçer ve hello işleminin bir parçası oluşan özel durumları ile bunlara karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5d381-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="5d381-137">Analytics hello operation_Id tanımlayıcısına göre hello başarısız istekleri hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="5d381-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="5d381-138">Merhaba sorgu hello autocluster algoritması kullanılarak hello sonuçları sonra kesim.</span><span class="sxs-lookup"><span data-stu-id="5d381-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="5d381-139">Kendi sorguları oluşturduğunuzda, tooyour akış eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5d381-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="5d381-140">Merhaba, **sorgu** kutusunda, Analytics sorgu aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d381-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="5d381-141">Merhaba, **grafik türü** kutusunda **Html tablosu**.</span><span class="sxs-lookup"><span data-stu-id="5d381-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Analytics sorgu yapılandırma penceresi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="5d381-143">6. adım: hello mantığı uygulama toosend e-postayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5d381-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="5d381-144">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5d381-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="5d381-145">Merhaba arama kutusuna yazın **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="5d381-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="5d381-146">Tıklatın **Office 365 Outlook – bir e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="5d381-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook seçimi](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="5d381-148">Merhaba, **bir e-posta Gönder** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5d381-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="5d381-149">a.</span><span class="sxs-lookup"><span data-stu-id="5d381-149">a.</span></span> <span data-ttu-id="5d381-150">Merhaba alıcı Hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="5d381-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="5d381-151">b.</span><span class="sxs-lookup"><span data-stu-id="5d381-151">b.</span></span> <span data-ttu-id="5d381-152">Merhaba e-posta için bir konu yazın.</span><span class="sxs-lookup"><span data-stu-id="5d381-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="5d381-153">c.</span><span class="sxs-lookup"><span data-stu-id="5d381-153">c.</span></span> <span data-ttu-id="5d381-154">Hello herhangi bir yere tıklayın **gövde** kutusuna ve ardından hello sağdaki açan hello dinamik içerik menüsünden seçin **gövde**.</span><span class="sxs-lookup"><span data-stu-id="5d381-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="5d381-155">d.</span><span class="sxs-lookup"><span data-stu-id="5d381-155">d.</span></span> <span data-ttu-id="5d381-156">Tıklatın **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="5d381-156">Click **Show advanced options**.</span></span>

      ![Office 365 Outlook yapılandırma](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="5d381-158">Merhaba dinamik içerik menüsünden aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5d381-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="5d381-159">a.</span><span class="sxs-lookup"><span data-stu-id="5d381-159">a.</span></span> <span data-ttu-id="5d381-160">Seçin **ek adı**.</span><span class="sxs-lookup"><span data-stu-id="5d381-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="5d381-161">b.</span><span class="sxs-lookup"><span data-stu-id="5d381-161">b.</span></span> <span data-ttu-id="5d381-162">Seçin **ek içerik**.</span><span class="sxs-lookup"><span data-stu-id="5d381-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="5d381-163">c.</span><span class="sxs-lookup"><span data-stu-id="5d381-163">c.</span></span> <span data-ttu-id="5d381-164">Merhaba, **HTML'dir** kutusunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="5d381-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Office 365 e-posta yapılandırma ekranında](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="5d381-166">7. adım: Kaydedin ve mantıksal uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="5d381-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="5d381-167">Tıklatın **kaydetmek** toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="5d381-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="5d381-168">Merhaba tetikleyici toorun hello mantıksal uygulama için bekleyebilir veya seçerek hello mantıksal uygulamayı hemen çalıştırabilirsiniz **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="5d381-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Logic app oluşturma ekran](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="5d381-170">Mantıksal uygulamanızı çalıştığında hello e-posta listesinde belirtilen hello alıcılar hello şuna benzeyen bir e-posta alırsınız:</span><span class="sxs-lookup"><span data-stu-id="5d381-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Mantıksal uygulama e-posta iletisi](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="5d381-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5d381-172">Next steps</span></span>

- <span data-ttu-id="5d381-173">Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="5d381-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="5d381-174">Daha fazla bilgi edinmek [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="5d381-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->






---
title: "Logic Apps kullanarak Azure Application Insights işlemlerini otomatik hale."
description: "Nasıl hızlı bir şekilde yinelenebilir işlemler mantığı uygulamanıza Application Insights Bağlayıcısı'nı ekleyerek otomatikleştirebilirsiniz öğrenin."
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
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="18fb2-103">Logic Apps kullanarak Application Insights işlemlerini otomatik hale</span><span class="sxs-lookup"><span data-stu-id="18fb2-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="18fb2-104">Kendiniz hizmetinizi düzgün çalışıp çalışmadığını denetlemek için telemetri verileri sürekli olarak çalışan aynı sorgu bulurum?</span><span class="sxs-lookup"><span data-stu-id="18fb2-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="18fb2-105">Eğilimler ve daha fazla bilgi bulmak için bu sorguları otomatik hale getirme ve ardından etrafında kendi iş akışları oluşturmak istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="18fb2-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="18fb2-106">Azure Application Insights (Önizleme) Logic Apps için doğru aracı bu amaçla Bağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="18fb2-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="18fb2-107">İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan çeşitli işlemleri otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18fb2-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="18fb2-108">Hızlı bir şekilde tüm Application Insights işlemini otomatikleştirmek için Application Insights Bağlayıcısı ile bir mantıksal uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18fb2-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="18fb2-109">Ek Eylemler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18fb2-109">You can add additional actions as well.</span></span> <span data-ttu-id="18fb2-110">Azure App Service Logic Apps özelliğidir Eylemler yüzlerce kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="18fb2-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="18fb2-111">Örneğin, bir mantıksal uygulama kullanarak, yapabilir otomatik olarak bir e-posta bildirim göndermek veya bir hata Visual Studio Team Services içinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18fb2-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="18fb2-112">Kullanılabilir çok birini de kullanabilirsiniz [şablonları](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) mantıksal uygulamanızı oluşturma işlemi hızlandırmak yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="18fb2-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="18fb2-113">Application Insights için bir mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="18fb2-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="18fb2-114">Bu öğreticide, verileri bir web uygulaması için Grup öznitelikleri Analytics autocluster algoritmasını kullanan bir mantıksal uygulama oluşturma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="18fb2-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="18fb2-115">Akış sonuçları e-posta ile tek bir örneği nasıl uygulama Öngörüler analizi ve Logic Apps birlikte kullanabileceğiniz otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="18fb2-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="18fb2-116">1. adım: bir mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="18fb2-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="18fb2-117">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="18fb2-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="18fb2-118">İçinde **yeni** bölmesinde, **Web + mobil**ve ardından **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Yeni mantıksal uygulama penceresi](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="18fb2-120">2. adım: mantıksal uygulamanız için bir Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="18fb2-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="18fb2-121">İçinde **mantığı Uygulama Tasarımcısı** penceresi altında **Başlat sahip ortak bir tetikleyici**seçin **yineleme**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı penceresi](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="18fb2-123">İçinde **sıklığı** kutusunda **gün** , daha sonra **aralığı** kutusuna **1**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı "Recurrence" penceresi](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="18fb2-125">3. adım: Application Insights Eylem Ekle</span><span class="sxs-lookup"><span data-stu-id="18fb2-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="18fb2-126">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="18fb2-127">İçinde **bir eylem seçin** arama kutusuna **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="18fb2-128">Altında **Eylemler**, tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı penceresinin "bir eylem seçin"](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="18fb2-130">4. adım: bir Application Insights kaynağına bağlanma</span><span class="sxs-lookup"><span data-stu-id="18fb2-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="18fb2-131">Bu adımı tamamlamak için kaynak için bir uygulama kimliği ve bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="18fb2-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="18fb2-132">Bunları Azure portalından, aşağıdaki çizimde gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18fb2-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Azure portalında uygulama kimliği](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="18fb2-134">Bağlantınızı, uygulama kimliği ve API anahtarı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="18fb2-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Mantıksal Uygulama Tasarımcısı akış bağlantısı penceresi](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="18fb2-136">5. adım: Analytics sorgu ve grafik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="18fb2-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="18fb2-137">Aşağıdaki örnekte, sorgu başarısız isteklerin son gün içinde seçer ve bunları işleminin bir parçası oluşan özel durumları ile karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="18fb2-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="18fb2-138">Analytics operation_Id tanımlayıcısına göre başarısız isteklerin hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="18fb2-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="18fb2-139">Sorgu sonuçları autocluster algoritması kullanılarak sonra kesim.</span><span class="sxs-lookup"><span data-stu-id="18fb2-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="18fb2-140">Kendi sorguları oluşturduğunuzda, akışınızı eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="18fb2-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="18fb2-141">İçinde **sorgu** kutusunda, aşağıdaki Analytics sorgu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="18fb2-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="18fb2-142">İçinde **grafik türü** kutusunda **Html tablosu**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Analytics sorgu yapılandırma penceresi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="18fb2-144">6. adım: e-posta göndermek için mantıksal uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="18fb2-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="18fb2-145">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="18fb2-146">Arama kutusuna **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="18fb2-147">Tıklatın **Office 365 Outlook – bir e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook seçimi](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="18fb2-149">İçinde **bir e-posta Gönder** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="18fb2-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="18fb2-150">a.</span><span class="sxs-lookup"><span data-stu-id="18fb2-150">a.</span></span> <span data-ttu-id="18fb2-151">Alıcı e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="18fb2-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="18fb2-152">b.</span><span class="sxs-lookup"><span data-stu-id="18fb2-152">b.</span></span> <span data-ttu-id="18fb2-153">E-posta için bir konu yazın.</span><span class="sxs-lookup"><span data-stu-id="18fb2-153">Type a subject for the email.</span></span>

   <span data-ttu-id="18fb2-154">c.</span><span class="sxs-lookup"><span data-stu-id="18fb2-154">c.</span></span> <span data-ttu-id="18fb2-155">Herhangi bir yeri tıklatın **gövde** kutusuna ve ardından sağ tarafta açılan dinamik içerik menüsünde seçin **gövde**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="18fb2-156">d.</span><span class="sxs-lookup"><span data-stu-id="18fb2-156">d.</span></span> <span data-ttu-id="18fb2-157">Tıklatın **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-157">Click **Show advanced options**.</span></span>

      ![Office 365 Outlook yapılandırma](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="18fb2-159">Dinamik içerik menüsünde, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="18fb2-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="18fb2-160">a.</span><span class="sxs-lookup"><span data-stu-id="18fb2-160">a.</span></span> <span data-ttu-id="18fb2-161">Seçin **ek adı**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="18fb2-162">b.</span><span class="sxs-lookup"><span data-stu-id="18fb2-162">b.</span></span> <span data-ttu-id="18fb2-163">Seçin **ek içerik**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="18fb2-164">c.</span><span class="sxs-lookup"><span data-stu-id="18fb2-164">c.</span></span> <span data-ttu-id="18fb2-165">İçinde **HTML'dir** kutusunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Office 365 e-posta yapılandırma ekranında](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="18fb2-167">7. adım: Kaydedin ve mantıksal uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="18fb2-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="18fb2-168">Tıklatın **kaydetmek** yaptığınız değişiklikleri kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="18fb2-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="18fb2-169">Tetikleyicinin mantığını uygulamayı çalıştırmak bekleyebilir veya seçerek mantıksal uygulamayı hemen çalıştırabilirsiniz **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="18fb2-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Logic app oluşturma ekran](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="18fb2-171">Mantıksal uygulamanızı çalıştığında, e-posta listesinde belirtilen alıcılara aşağıdakine benzer bir e-posta alırsınız:</span><span class="sxs-lookup"><span data-stu-id="18fb2-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Mantıksal uygulama e-posta iletisi](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="18fb2-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18fb2-173">Next steps</span></span>

- <span data-ttu-id="18fb2-174">Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="18fb2-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="18fb2-175">Daha fazla bilgi edinmek [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="18fb2-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->






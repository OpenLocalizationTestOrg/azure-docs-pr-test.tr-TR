---
title: "Microsoft Flow ile Azure Application Insights işlemlerini otomatik hale getirme"
description: "Hızlı bir şekilde yinelenebilir işlemler Application Insights Bağlayıcısı'nı kullanarak otomatik hale getirmek için Microsoft Flow nasıl kullanabileceğinizi öğrenin."
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="d262a-103">İçin Microsoft Flow connector ile Azure Application Insights süreçleri otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="d262a-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="d262a-104">Kendiniz hizmetinizi düzgün çalışıp çalışmadığını denetlemek için telemetri verileri sürekli olarak çalışan aynı sorgu bulurum?</span><span class="sxs-lookup"><span data-stu-id="d262a-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="d262a-105">Eğilimler ve daha fazla bilgi bulmak için bu sorguları otomatik hale getirme ve ardından etrafında kendi iş akışları oluşturmak istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="d262a-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="d262a-106">Azure Application Insights (Önizleme) Microsoft Flow için doğru aracı bu amaçlar için Bağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d262a-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="d262a-107">İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan artık çok sayıda süreçlerini otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d262a-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="d262a-108">Application Insights eylemini kullanarak bir akış oluşturduktan sonra akış uygulama Öngörüler Analytics sorgunuzu otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d262a-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="d262a-109">Ek Eylemler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d262a-109">You can add additional actions as well.</span></span> <span data-ttu-id="d262a-110">Microsoft Flow Eylemler yüzlerce kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d262a-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="d262a-111">Örneğin, otomatik olarak bir e-posta bildirim göndermek veya Visual Studio Team Services içinde oluşturma için Microsoft Flow kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d262a-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="d262a-112">Çok birini de kullanabilirsiniz [şablonları](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) Microsoft Flow için bağlayıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d262a-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="d262a-113">Bu şablonları bir akış oluşturma işlemi hızlandırmak.</span><span class="sxs-lookup"><span data-stu-id="d262a-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="d262a-114">Bir akış için Application Insights oluşturma</span><span class="sxs-lookup"><span data-stu-id="d262a-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="d262a-115">Bu öğreticide, verileri bir web uygulaması için Grup öznitelikleri Analytics otomatik küme algoritmasını kullanan bir akışı oluşturmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d262a-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="d262a-116">Akış sonuçları e-posta ile tek bir örneği nasıl Microsoft Flow ve uygulama Öngörüler Analytics birlikte kullanabileceğiniz otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="d262a-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="d262a-117">1. adım: bir akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d262a-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="d262a-118">Oturum [Microsoft Flow](http://flow.microsoft.com)ve ardından **My akar**.</span><span class="sxs-lookup"><span data-stu-id="d262a-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="d262a-119">Tıklatın **bir akışı boş iken oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="d262a-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="d262a-120">2. adım: akışınız için bir Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="d262a-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="d262a-121">Seçin **zamanlama**ve ardından **çizelgesi - yinelenme**.</span><span class="sxs-lookup"><span data-stu-id="d262a-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="d262a-122">İçinde **sıklığı** kutusunda **gün**hem de **aralığı** kutusuna **1**.</span><span class="sxs-lookup"><span data-stu-id="d262a-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow tetikleyici iletişim kutusu](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="d262a-124">3. adım: Application Insights Eylem Ekle</span><span class="sxs-lookup"><span data-stu-id="d262a-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="d262a-125">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d262a-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="d262a-126">Arama **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d262a-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="d262a-127">Tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="d262a-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Analytics sorgu penceresi](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="d262a-129">4. adım: bir Application Insights kaynağına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d262a-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="d262a-130">Bu adımı tamamlamak için kaynak için bir uygulama kimliği ve bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d262a-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="d262a-131">Bunları Azure portalından, aşağıdaki çizimde gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d262a-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Azure portalında uygulama kimliği](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="d262a-133">Uygulama kimliği ve API anahtarı ile birlikte bağlantınız için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d262a-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Microsoft Flow bağlantı penceresi](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="d262a-135">5. adım: Analytics sorgu ve grafik türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="d262a-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="d262a-136">Bu örnek sorgu son gün içinde başarısız olan istekleri seçer ve bunları işleminin bir parçası oluşan özel durumları ile karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d262a-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="d262a-137">Analytics bunları operation_Id tanımlayıcısına göre hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="d262a-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="d262a-138">Sorgu sonuçları autocluster algoritması kullanılarak sonra kesim.</span><span class="sxs-lookup"><span data-stu-id="d262a-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="d262a-139">Kendi sorguları oluşturduğunuzda, akışınızı eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d262a-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="d262a-140">Aşağıdaki Analytics sorgu ekleyin ve ardından HTML tablo grafik türü seçin.</span><span class="sxs-lookup"><span data-stu-id="d262a-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="d262a-142">6. adım: e-posta göndermek için akışı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="d262a-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="d262a-143">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d262a-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="d262a-144">Arama **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="d262a-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="d262a-145">Tıklatın **Office 365 Outlook – bir e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="d262a-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook seçim penceresi](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="d262a-147">İçinde **bir e-posta Gönder** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="d262a-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="d262a-148">a.</span><span class="sxs-lookup"><span data-stu-id="d262a-148">a.</span></span> <span data-ttu-id="d262a-149">Alıcı e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="d262a-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="d262a-150">b.</span><span class="sxs-lookup"><span data-stu-id="d262a-150">b.</span></span> <span data-ttu-id="d262a-151">E-posta için bir konu yazın.</span><span class="sxs-lookup"><span data-stu-id="d262a-151">Type a subject for the email.</span></span>

   <span data-ttu-id="d262a-152">c.</span><span class="sxs-lookup"><span data-stu-id="d262a-152">c.</span></span> <span data-ttu-id="d262a-153">Herhangi bir yeri tıklatın **gövde** kutusuna ve ardından sağ tarafta açılan dinamik içerik menüsünde seçin **gövde**.</span><span class="sxs-lookup"><span data-stu-id="d262a-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="d262a-154">d.</span><span class="sxs-lookup"><span data-stu-id="d262a-154">d.</span></span> <span data-ttu-id="d262a-155">Tıklatın **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="d262a-155">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook yapılandırma](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="d262a-157">Dinamik içerik menüsünde, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="d262a-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="d262a-158">a.</span><span class="sxs-lookup"><span data-stu-id="d262a-158">a.</span></span> <span data-ttu-id="d262a-159">Seçin **ek adı**.</span><span class="sxs-lookup"><span data-stu-id="d262a-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="d262a-160">b.</span><span class="sxs-lookup"><span data-stu-id="d262a-160">b.</span></span> <span data-ttu-id="d262a-161">Seçin **ek içerik**.</span><span class="sxs-lookup"><span data-stu-id="d262a-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="d262a-162">c.</span><span class="sxs-lookup"><span data-stu-id="d262a-162">c.</span></span> <span data-ttu-id="d262a-163">İçinde **HTML'dir** kutusunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d262a-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 e-posta yapılandırma penceresi](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="d262a-165">7. adım: Kaydetmek ve akışınız test</span><span class="sxs-lookup"><span data-stu-id="d262a-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="d262a-166">İçinde **Akış adı** kutusuna akışınız için bir ad ekleyin ve ardından **akışı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="d262a-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Akış oluşturma penceresi](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="d262a-168">Bu eylem tetikleyici için bekleyebilir veya akış hemen göre çalıştırabilirsiniz [tetikleyici talep üzerine çalıştırmaya](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="d262a-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="d262a-169">Akışı çalıştığında, e-posta listesinde belirtilen alıcılara aşağıdakine benzer bir e-posta iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="d262a-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Örnek e-posta](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="d262a-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d262a-171">Next steps</span></span>

- <span data-ttu-id="d262a-172">Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="d262a-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="d262a-173">Daha fazla bilgi edinmek [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d262a-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->






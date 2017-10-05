---
title: "Azure genel bir Web kancası tarafından tetiklenen bir işlev oluşturun | Microsoft Docs"
description: "Azure işlevleri, bir Web kancası Azure tarafından çağrılan sunucusuz bir işlev oluşturmak için kullanın."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: f283f8d79c5ae5fb6a72c84c9e9edb7bb8de4a83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="82a58-103">Genel bir Web kancası tarafından tetiklenen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="82a58-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="82a58-104">Azure İşlevleri, öncelikle bir VM oluşturmak veya bir web uygulaması yayımlamak zorunda kalmadan kodunuzu sunucusuz bir ortamda yürütmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="82a58-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="82a58-105">Örneğin, Azure İzleyici tarafından verilen bir uyarı tarafından tetiklenen bir işlev yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82a58-105">For example, you can configure a function to be triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="82a58-106">Bu konu bir kaynak grubu aboneliğinize eklendiğinde, C# kodunun nasıl çalıştırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="82a58-106">This topic shows you how to execute C# code when a resource group is added to your subscription.</span></span>   

![Azure portalında işlevi genel Web kancası tetiklendi](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="82a58-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="82a58-108">Prerequisites</span></span> 

<span data-ttu-id="82a58-109">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="82a58-109">To complete this tutorial:</span></span>

+ <span data-ttu-id="82a58-110">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82a58-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="82a58-111">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82a58-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="82a58-112">Ardından, yeni işlev uygulamasında bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82a58-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="82a58-113"><a name="create-function"></a>Genel Web kancası tetiklenen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="82a58-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="82a58-114">İşlev uygulamanızı genişletin ve **İşlevler**'in yanındaki **+** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82a58-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="82a58-115">Bu işlev listedeki birinci işlevi uygulamanız gerekiyorsa seçin **özel işlevi**.</span><span class="sxs-lookup"><span data-stu-id="82a58-115">If this function is the first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="82a58-116">Böylece işlev şablonlarının tamamı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="82a58-116">This displays the complete set of function templates.</span></span>

    ![Azure portalındaki İşlevler hızlı başlangıç sayfası](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="82a58-118">Seçin **Genel Web kancası - C#** şablonu.</span><span class="sxs-lookup"><span data-stu-id="82a58-118">Select the **Generic WebHook - C#** template.</span></span> <span data-ttu-id="82a58-119">C# işlevi için bir ad yazın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="82a58-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Azure portalında tetiklenen Genel Web kancası işlevi oluşturma](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="82a58-121">Yeni işlevinizi tıklatın **<> / Get işlevi URL**, daha sonra kopyalayın ve değeri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="82a58-121">In your new function, click **</> Get function URL**, then copy and save the value.</span></span> <span data-ttu-id="82a58-122">Web kancası yapılandırmak için bu değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="82a58-122">You use this value to configure the webhook.</span></span> 

    ![İşlev kodunu gözden geçirme](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="82a58-124">Ardından, bir etkinlik günlüğü uyarı Azure İzleyicisi'nde bir Web kancası uç noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82a58-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="82a58-125">Bir etkinlik günlüğü uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="82a58-125">Create an activity log alert</span></span>

1. <span data-ttu-id="82a58-126">Azure portalında gidin **İzleyici** hizmeti, select **uyarıları**, tıklatıp **etkinlik günlüğü uyarı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="82a58-126">In the Azure portal, navigate to the **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![İzleme](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="82a58-128">Tabloda belirtilen ayarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="82a58-128">Use the settings as specified in the table:</span></span>

    ![Bir etkinlik günlüğü uyarı oluşturabilir.](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="82a58-130">Ayar</span><span class="sxs-lookup"><span data-stu-id="82a58-130">Setting</span></span>      |  <span data-ttu-id="82a58-131">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="82a58-131">Suggested value</span></span>   | <span data-ttu-id="82a58-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82a58-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="82a58-133">**Etkinlik günlüğü uyarı adı**</span><span class="sxs-lookup"><span data-stu-id="82a58-133">**Activity log alert name**</span></span> | <span data-ttu-id="82a58-134">kaynak-grubu-oluştur-uyarı</span><span class="sxs-lookup"><span data-stu-id="82a58-134">resource-group-create-alert</span></span> | <span data-ttu-id="82a58-135">Etkinlik günlüğü uyarı adı.</span><span class="sxs-lookup"><span data-stu-id="82a58-135">Name of the activity log alert.</span></span> |
    | <span data-ttu-id="82a58-136">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="82a58-136">**Subscription**</span></span> | <span data-ttu-id="82a58-137">Aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="82a58-137">Your subscription</span></span> | <span data-ttu-id="82a58-138">Bu öğretici için kullanmakta olduğunuz abonelik.</span><span class="sxs-lookup"><span data-stu-id="82a58-138">The subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="82a58-139">**Kaynak Grubu**</span><span class="sxs-lookup"><span data-stu-id="82a58-139">**Resource Group**</span></span> | <span data-ttu-id="82a58-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82a58-140">myResourceGroup</span></span> | <span data-ttu-id="82a58-141">Uyarı kaynakları dağıtılan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="82a58-141">The resource group that the alert resources are deployed to.</span></span> <span data-ttu-id="82a58-142">Aynı kaynak grubunda işlevi kullanarak öğreticiyi tamamladıktan sonra temizlemek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="82a58-142">Using the same resource group as your function app makes it easier to clean up after you complete the tutorial.</span></span> |
    | <span data-ttu-id="82a58-143">**Olay kategorisi**</span><span class="sxs-lookup"><span data-stu-id="82a58-143">**Event category**</span></span> | <span data-ttu-id="82a58-144">Yönetim</span><span class="sxs-lookup"><span data-stu-id="82a58-144">Administrative</span></span> | <span data-ttu-id="82a58-145">Bu kategori Azure kaynaklarında yapılan değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="82a58-145">This category includes changes made to Azure resources.</span></span>  |
    | <span data-ttu-id="82a58-146">**Kaynak türü**</span><span class="sxs-lookup"><span data-stu-id="82a58-146">**Resource type**</span></span> | <span data-ttu-id="82a58-147">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="82a58-147">Resource groups</span></span> | <span data-ttu-id="82a58-148">Kaynak grubu etkinlikler için uyarı filtreleri.</span><span class="sxs-lookup"><span data-stu-id="82a58-148">Filters alerts to resource group activities.</span></span> |
    | <span data-ttu-id="82a58-149">**Kaynak Grubu**</span><span class="sxs-lookup"><span data-stu-id="82a58-149">**Resource Group**</span></span><br/><span data-ttu-id="82a58-150">ve **kaynak**</span><span class="sxs-lookup"><span data-stu-id="82a58-150">and **Resource**</span></span> | <span data-ttu-id="82a58-151">Tümü</span><span class="sxs-lookup"><span data-stu-id="82a58-151">All</span></span> | <span data-ttu-id="82a58-152">Tüm kaynaklar izleyin.</span><span class="sxs-lookup"><span data-stu-id="82a58-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="82a58-153">**İşlem adı**</span><span class="sxs-lookup"><span data-stu-id="82a58-153">**Operation name**</span></span> | <span data-ttu-id="82a58-154">Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="82a58-154">Create Resource Group</span></span> | <span data-ttu-id="82a58-155">İşlemler oluşturmak için uyarıları filtreler.</span><span class="sxs-lookup"><span data-stu-id="82a58-155">Filters alerts to create operations.</span></span> |
    | <span data-ttu-id="82a58-156">**Düzeyi**</span><span class="sxs-lookup"><span data-stu-id="82a58-156">**Level**</span></span> | <span data-ttu-id="82a58-157">Bilgilendirme</span><span class="sxs-lookup"><span data-stu-id="82a58-157">Informational</span></span> | <span data-ttu-id="82a58-158">Bilgilendirici düzeyi uyarılar içerir.</span><span class="sxs-lookup"><span data-stu-id="82a58-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="82a58-159">**Durumu**</span><span class="sxs-lookup"><span data-stu-id="82a58-159">**Status**</span></span> | <span data-ttu-id="82a58-160">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="82a58-160">Succeeded</span></span> | <span data-ttu-id="82a58-161">Uyarılar başarıyla tamamladınız eylemlerine filtreler.</span><span class="sxs-lookup"><span data-stu-id="82a58-161">Filters alerts to actions that have completed successfully.</span></span> |
    | <span data-ttu-id="82a58-162">**Eylem grubu**</span><span class="sxs-lookup"><span data-stu-id="82a58-162">**Action group**</span></span> | <span data-ttu-id="82a58-163">Yeni</span><span class="sxs-lookup"><span data-stu-id="82a58-163">New</span></span> | <span data-ttu-id="82a58-164">Bir uyarı verildiğinde hangi eylemini alır tanımlayan yeni bir eylem grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82a58-164">Create a new action group, which defines the action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="82a58-165">**Eylem grup adı**</span><span class="sxs-lookup"><span data-stu-id="82a58-165">**Action group name**</span></span> | <span data-ttu-id="82a58-166">Web kancası işlevi</span><span class="sxs-lookup"><span data-stu-id="82a58-166">function-webhook</span></span> | <span data-ttu-id="82a58-167">Eylem grubunu tanımlamak için bir ad.</span><span class="sxs-lookup"><span data-stu-id="82a58-167">A name to identify the action group.</span></span>  | 
    | <span data-ttu-id="82a58-168">**Kısa ad**</span><span class="sxs-lookup"><span data-stu-id="82a58-168">**Short name**</span></span> | <span data-ttu-id="82a58-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="82a58-169">funcwebhook</span></span> | <span data-ttu-id="82a58-170">Eylem grubu için kısa bir ad.</span><span class="sxs-lookup"><span data-stu-id="82a58-170">A short name for the action group.</span></span> |  

3. <span data-ttu-id="82a58-171">İçinde **Eylemler**, tabloda belirtildiği gibi ayarları kullanarak bir eylem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82a58-171">In **Actions**, add an action using the settings as specified in the table:</span></span> 

    ![Bir eylem grubu Ekle](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="82a58-173">Ayar</span><span class="sxs-lookup"><span data-stu-id="82a58-173">Setting</span></span>      |  <span data-ttu-id="82a58-174">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="82a58-174">Suggested value</span></span>   | <span data-ttu-id="82a58-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82a58-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="82a58-176">**Ad**</span><span class="sxs-lookup"><span data-stu-id="82a58-176">**Name**</span></span> | <span data-ttu-id="82a58-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="82a58-177">CallFunctionWebhook</span></span> | <span data-ttu-id="82a58-178">Eylem için bir ad.</span><span class="sxs-lookup"><span data-stu-id="82a58-178">A name for the action.</span></span> |
    | <span data-ttu-id="82a58-179">**Eylem türü**</span><span class="sxs-lookup"><span data-stu-id="82a58-179">**Action type**</span></span> | <span data-ttu-id="82a58-180">Web Kancası</span><span class="sxs-lookup"><span data-stu-id="82a58-180">Webhook</span></span> | <span data-ttu-id="82a58-181">Uyarı yanıta bir Web kancası URL'si olarak adlandırılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="82a58-181">The response to the alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="82a58-182">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="82a58-182">**Details**</span></span> | <span data-ttu-id="82a58-183">İşlev URL'si</span><span class="sxs-lookup"><span data-stu-id="82a58-183">Function URL</span></span> | <span data-ttu-id="82a58-184">Daha önce kopyaladığınız işlevi Web kancası URL'sini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="82a58-184">Paste in the webhook URL of the function that you copied earlier.</span></span> |<span data-ttu-id="82a58-185">v</span><span class="sxs-lookup"><span data-stu-id="82a58-185">v</span></span>

4. <span data-ttu-id="82a58-186">Tıklatın **Tamam** uyarı ve eylem grubu oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="82a58-186">Click **OK** to create the alert and action group.</span></span>  

<span data-ttu-id="82a58-187">Bir kaynak grubu, aboneliğinizde oluşturulduğunda Web kancası şimdi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="82a58-187">The webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="82a58-188">Ardından, istek gövdesinde JSON günlük verileri işlemek için işlev kodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="82a58-188">Next, you update the code in your function to handle the JSON log data in the body of the request.</span></span>   

## <a name="update-the-function-code"></a><span data-ttu-id="82a58-189">İşlev kodunu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="82a58-189">Update the function code</span></span>

1. <span data-ttu-id="82a58-190">Portal işlevi uygulamanızda geri gidin ve işlevinizi genişletin.</span><span class="sxs-lookup"><span data-stu-id="82a58-190">Navigate back to your function app in the portal, and expand your function.</span></span> 

2. <span data-ttu-id="82a58-191">Portalda işlevindeki C# betik kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82a58-191">Replace the C# script code in the function in the portal with the following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get the activityLog object from the JSON in the message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if the resource in the activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about the created resource group to the streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="82a58-192">Şimdi, aboneliğinizde yeni bir kaynak grubu oluşturarak işlevi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82a58-192">Now you can test the function by creating a new resource group in your subscription.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="82a58-193">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="82a58-193">Test the function</span></span>

1. <span data-ttu-id="82a58-194">Kaynak grubu seçin Azure portalının sol simgesini **+ Ekle**, bir **kaynak grubu adı**ve seçin **oluşturma** boş bir kaynak grubu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="82a58-194">Click the resource group icon in the left of the Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** to create an empty resource group.</span></span>
    
    ![Bir kaynak grubu oluşturun.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="82a58-196">İşlevinizi için geri dönün ve genişletin **günlükleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="82a58-196">Go back to your function and expand the **Logs** window.</span></span> <span data-ttu-id="82a58-197">Kaynak grubu oluşturulduktan sonra Web kancası etkinlik günlüğü uyarıyı tetikleyen ve işlev yürütür.</span><span class="sxs-lookup"><span data-stu-id="82a58-197">After the resource group is created, the activity log alert triggers the webhook and the function executes.</span></span> <span data-ttu-id="82a58-198">Günlüklere yazılan yeni kaynak grubu adını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="82a58-198">You see the name of the new resource group written to the logs.</span></span>  

    ![Bir test uygulama ayarı ekleyin.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="82a58-200">(İsteğe bağlı) Geri dönün ve sizin oluşturduğunuz kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82a58-200">(Optional) Go back and delete the resource group that you created.</span></span> <span data-ttu-id="82a58-201">Bu etkinlik Tetik işlevi değil unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82a58-201">Note that this activity doesn't trigger the function.</span></span> <span data-ttu-id="82a58-202">Bunun nedeni, operations filtrelenir uyarı tarafından silin.</span><span class="sxs-lookup"><span data-stu-id="82a58-202">This is because delete operations are filtered out by the alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="82a58-203">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="82a58-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="82a58-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82a58-204">Next steps</span></span>

<span data-ttu-id="82a58-205">Genel bir Web kancası bir istek alındığında çalıştırılan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="82a58-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="82a58-206">Web kancası bağlamaları hakkında daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="82a58-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="82a58-207">C# işlevleri geliştirme hakkında daha fazla bilgi için bkz: [Azure işlevleri C# betik Geliştirici Başvurusu](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="82a58-207">To learn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>


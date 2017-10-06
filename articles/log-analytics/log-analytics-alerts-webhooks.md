---
title: "OMS günlük analizi aaaWebhook uyarı eylemi örnek | Microsoft Docs"
description: "Günlük analizi uyarısıdır yanıt tooa içinde çalıştırabilirsiniz hello eylemlerden birini bir * tooinvoke bir dış işlem üzerinden tek bir HTTP isteği sağlayan Web kancası *. Bu makalede bir Web kancası eylem kayma kullanarak günlük analizi uyarıda oluşturma örneği anlatılmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="fd875-104">Bir uyarı Web kancası eylem OMS günlük analizi toosend ileti tooSlack oluşturun</span><span class="sxs-lookup"><span data-stu-id="fd875-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="fd875-105">Yanıt tooa çalıştırabilirsiniz hello eylemlerden birini [günlük analizi uyarı](log-analytics-alerts.md) olan bir *Web kancası*, olanak sağlayan tooinvoke bir dış işlem üzerinden tek bir HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="fd875-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="fd875-106">Uyarılar ve Web kancalarını içinde ayrıntıları hakkında bilgi edinebilirsiniz [günlük analizi uyarıları](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="fd875-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="fd875-107">Bu makalede, sizi bir ileti sistemi hizmeti olan kayma kullanarak günlük analizi uyarıda bir Web kancası eylem oluşturma örneği adım geçireceğiz.</span><span class="sxs-lookup"><span data-stu-id="fd875-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="fd875-108">Bu örnek Slack hesap toocomplete olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd875-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="fd875-109">Ücretsiz bir hesap için kaydolabilirsiniz [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fd875-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="fd875-110">1. adım - kayma içinde etkinleştir Web kancaları</span><span class="sxs-lookup"><span data-stu-id="fd875-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="fd875-111">Oturum açma sırasında tooSlack [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fd875-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="fd875-112">Bir kanal hello seçin **kanalları** hello sol bölmesindeki bölümünde.</span><span class="sxs-lookup"><span data-stu-id="fd875-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="fd875-113">Bu hello kanalıdır hello ileti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="fd875-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="fd875-114">Merhaba varsayılan kanalları birini gibi seçebilirsiniz **genel** veya **rastgele**.</span><span class="sxs-lookup"><span data-stu-id="fd875-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="fd875-115">Bir üretim senaryosunda, büyük olasılıkla özel kanal gibi oluşturacak **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="fd875-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="fd875-117">Tıklatın **bir uygulama veya özel tümleştirme ekleme** tooopen hello uygulama dizini.</span><span class="sxs-lookup"><span data-stu-id="fd875-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="fd875-118">Tür *kancalarını* hello arama kutusuna ve ardından **gelen Web Kancalarını**.</span><span class="sxs-lookup"><span data-stu-id="fd875-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="fd875-120">Tıklatın **yükleme** sonraki tooyour ekip adı.</span><span class="sxs-lookup"><span data-stu-id="fd875-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="fd875-121">Tıklatın **yapılandırması eklemek**.</span><span class="sxs-lookup"><span data-stu-id="fd875-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="fd875-122">Bu örnek için toouse oluşturacağız ve ardından select hello hello kanal **eklemek gelen Web Kancalarını tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="fd875-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="fd875-123">Kopya hello **Web kancası URL'si**.</span><span class="sxs-lookup"><span data-stu-id="fd875-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="fd875-124">Bu hello uyarı yapılandırma yapıştırdığınız.</span><span class="sxs-lookup"><span data-stu-id="fd875-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="fd875-126">2. adım - günlük analizi uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="fd875-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="fd875-127">[Bir uyarı kuralı oluştur](log-analytics-alerts.md) ayarları aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="fd875-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="fd875-128">Sorgu:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="fd875-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="fd875-129">Bu uyarıyı denetleme her: 5 dakika</span><span class="sxs-lookup"><span data-stu-id="fd875-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="fd875-130">sonuçları Hello sayısıdır: 10'dan büyük</span><span class="sxs-lookup"><span data-stu-id="fd875-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="fd875-131">Bu zaman penceresi üzerinden: 60 dakika</span><span class="sxs-lookup"><span data-stu-id="fd875-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="fd875-132">Seçin **Evet** için **Web kancası** ve **Hayır** hello diğer eylemler.</span><span class="sxs-lookup"><span data-stu-id="fd875-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="fd875-133">Merhaba içine yapıştırma hello kayma URL **Web kancası URL'si** alan.</span><span class="sxs-lookup"><span data-stu-id="fd875-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="fd875-134">Çok olarak Hello seçeneğini**özel JSON yükünü dahil et**.</span><span class="sxs-lookup"><span data-stu-id="fd875-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="fd875-135">Kayma JSON'adlı bir parametre ile biçimlendirilmiş bir yükü bekliyor *metin*.</span><span class="sxs-lookup"><span data-stu-id="fd875-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="fd875-136">Bu oluşturduğu hello iletisinde görüntüleyecek hello metindir.</span><span class="sxs-lookup"><span data-stu-id="fd875-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="fd875-137">Bir veya daha fazla hello kullanarak hello uyarı parametrelerini kullanabilirsiniz  *#*  gibi aşağıdaki örneğine hello olduğu gibi simge.</span><span class="sxs-lookup"><span data-stu-id="fd875-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Örnek JSON yükü](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="fd875-139">Tıklatın **kaydetmek** toosave hello uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="fd875-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="fd875-140">Oluşturulan bir uyarı toobe yeterli bir süre bekleyin ve ardından kayma benzer toohello aşağıdaki olacağı bir ileti için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fd875-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![Örnek Web kancası kayma içinde](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="fd875-142">Web kancası yükü kayma için Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="fd875-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="fd875-143">Gelen iletiler kayma ile kapsamlı bir şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd875-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="fd875-144">Daha fazla bilgi için bkz: [gelen Web Kancalarını](https://api.slack.com/incoming-webhooks) hello Slack Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="fd875-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="fd875-145">Daha karmaşık bir yükü toocreate biçimlendirmeye sahip zengin bir ileti aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fd875-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="fd875-146">Bu ileti Slack benzer toohello aşağıdakileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fd875-146">This would generate a message in Slack similar toohello following.</span></span>

![Kayma örnek iletisi](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="fd875-148">Özet</span><span class="sxs-lookup"><span data-stu-id="fd875-148">Summary</span></span>
<span data-ttu-id="fd875-149">Bu uyarı kuralı ile yerinde Hello ölçütleri karşılanıyorsa her zaman gönderilen ileti tooSlack gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd875-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="fd875-150">Bu yalnızca bir yanıt tooan uyarıda oluşturabileceğiniz bir eylem örneğidir.</span><span class="sxs-lookup"><span data-stu-id="fd875-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="fd875-151">Bir runbook'un Azure Otomasyon ya da bir e-posta eylem toosend başka bir dış hizmet, bir runbook eylemi toostart çağıran bir Web kancası eylemi posta tooyourself veya diğer alıcılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd875-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="fd875-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fd875-152">Next Steps</span></span>
* <span data-ttu-id="fd875-153">Diğer hakkında bilgi edinin [uyarı günlük analizi Eylemler](log-analytics-alerts-actions.md) diğer Eylemler dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="fd875-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>



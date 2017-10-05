---
title: "OMS günlük analizi uyarılarını yanıtlarını | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya düzeltmenize girişiminde Eylemler çağırma.  Bu makalede, bir uyarı kuralı ve ayrıntıları yapabilecekleri farklı eylemler oluşturmayı açıklar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="f7408-104">Günlük analizi uyarı kurallarında eylemleri ekleyin</span><span class="sxs-lookup"><span data-stu-id="f7408-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="f7408-105">Zaman bir [uyarı günlük analizi oluşturulan](log-analytics-alerts.md), seçeneğiniz vardır [uyarı kuralı yapılandırma](log-analytics-alerts.md) bir veya daha fazla eylemleri gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f7408-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="f7408-106">Bu makalede, her tür yapılandırma hakkında ayrıntılar ve kullanılabilir farklı eylemler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f7408-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="f7408-107">Eylem</span><span class="sxs-lookup"><span data-stu-id="f7408-107">Action</span></span> | <span data-ttu-id="f7408-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="f7408-109">E-posta</span><span class="sxs-lookup"><span data-stu-id="f7408-109">Email</span></span>](#email-actions) | <span data-ttu-id="f7408-110">Bir veya daha fazla alıcıya uyarı ayrıntılarını içeren bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="f7408-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="f7408-111">Web kancası</span><span class="sxs-lookup"><span data-stu-id="f7408-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="f7408-112">Bir dış işlem tek bir HTTP POST isteği üzerinden çağırır.</span><span class="sxs-lookup"><span data-stu-id="f7408-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="f7408-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="f7408-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="f7408-114">Bir runbook, Azure Automation'da başlatın.</span><span class="sxs-lookup"><span data-stu-id="f7408-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="f7408-115">E-posta Eylemler</span><span class="sxs-lookup"><span data-stu-id="f7408-115">Email actions</span></span>
<span data-ttu-id="f7408-116">E-posta Eylemler bir veya daha fazla alıcıya uyarı ayrıntılarını içeren bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="f7408-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="f7408-117">Posta konusunu belirtebilirsiniz, ancak buna ait günlük analizi tarafından oluşturulan standart bir biçim içeriktir.</span><span class="sxs-lookup"><span data-stu-id="f7408-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="f7408-118">Uyarı günlüğü araması tarafından döndürülen en fazla on kayıt ayrıntılarını yanı sıra adı gibi özet bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f7408-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="f7408-119">Ayrıca, kayıt kümesinin tamamını Bu sorgudan döndürülecek günlük analizi günlük arama bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="f7408-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="f7408-120">Posta gönderen *Microsoft Operations Management Suite ekibi &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="f7408-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="f7408-121">E-posta eylemler özellikler aşağıdaki tabloda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f7408-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="f7408-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="f7408-122">Property</span></span> | <span data-ttu-id="f7408-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f7408-124">Konu</span><span class="sxs-lookup"><span data-stu-id="f7408-124">Subject</span></span> |<span data-ttu-id="f7408-125">E-postayla konu.</span><span class="sxs-lookup"><span data-stu-id="f7408-125">Subject in the email.</span></span>  <span data-ttu-id="f7408-126">Posta gövdesini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="f7408-127">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="f7408-127">Recipients</span></span> |<span data-ttu-id="f7408-128">Tüm e-posta alıcıları adresleri.</span><span class="sxs-lookup"><span data-stu-id="f7408-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="f7408-129">Birden fazla adres belirtirseniz, adreslerini noktalı virgül (;) ayırın.</span><span class="sxs-lookup"><span data-stu-id="f7408-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="f7408-130">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="f7408-130">Webhook actions</span></span>

<span data-ttu-id="f7408-131">Web kancası eylemleri, bir dış işlem tek bir HTTP POST isteği üzerinden çağırma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f7408-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="f7408-132">Çağrılan Hizmet Web kancalarını destekleyen ve tüm yükü nasıl kullanacağınızı belirleyin aldığı.</span><span class="sxs-lookup"><span data-stu-id="f7408-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="f7408-133">Ayrıca, istek API özelliğini algılayan bir biçimde olduğu sürece, özellikle Web kancalarını desteklemeyen bir REST API'si çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="f7408-134">Bir Web kancası yanıt olarak bir uyarı kullanma örnekleri bir ileti gönderiyorsunuz [Slack'e](http://slack.com) veya bir olay oluşturma [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="f7408-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="f7408-135">Kayma çağırmak için bir Web kancası ile bir uyarı kuralı oluşturma izlenecek tam yol şu adresten edinilebilir [Kancalarını günlük analizi uyarılar](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="f7408-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="f7408-136">Web kancası eylemleri özellikler aşağıdaki tabloda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f7408-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="f7408-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="f7408-137">Property</span></span> | <span data-ttu-id="f7408-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f7408-139">Web kancası URL'si</span><span class="sxs-lookup"><span data-stu-id="f7408-139">Webhook URL</span></span> |<span data-ttu-id="f7408-140">Web kancası URL'si.</span><span class="sxs-lookup"><span data-stu-id="f7408-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="f7408-141">Özel JSON yükü</span><span class="sxs-lookup"><span data-stu-id="f7408-141">Custom JSON payload</span></span> |<span data-ttu-id="f7408-142">Web kancası ile göndermek için özel yükü.</span><span class="sxs-lookup"><span data-stu-id="f7408-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="f7408-143">Ayrıntılar için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="f7408-143">See below for details.</span></span> |


<span data-ttu-id="f7408-144">Web kancası bir URL ve dış hizmete gönderilen veriler JSON biçimli bir yükü içerir.</span><span class="sxs-lookup"><span data-stu-id="f7408-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="f7408-145">Varsayılan olarak, aşağıdaki tabloda değerleri yükü içerir.</span><span class="sxs-lookup"><span data-stu-id="f7408-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="f7408-146">Bu yük özel bir kendi tarihle seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="f7408-147">Bu durumda, değişkenleri tabloda her parametre için değer özel yükünüzü dahil etmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="f7408-148">Parametre</span><span class="sxs-lookup"><span data-stu-id="f7408-148">Parameter</span></span> | <span data-ttu-id="f7408-149">Değişken</span><span class="sxs-lookup"><span data-stu-id="f7408-149">Variable</span></span> | <span data-ttu-id="f7408-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f7408-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="f7408-151">AlertRuleName</span></span> |<span data-ttu-id="f7408-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="f7408-152">#alertrulename</span></span> |<span data-ttu-id="f7408-153">Uyarı kuralı adı.</span><span class="sxs-lookup"><span data-stu-id="f7408-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="f7408-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="f7408-154">AlertThresholdOperator</span></span> |<span data-ttu-id="f7408-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="f7408-155">#thresholdoperator</span></span> |<span data-ttu-id="f7408-156">Uyarı kuralı için eşik işleci.</span><span class="sxs-lookup"><span data-stu-id="f7408-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="f7408-157">*Büyük* veya *değerinden*.</span><span class="sxs-lookup"><span data-stu-id="f7408-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="f7408-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="f7408-158">AlertThresholdValue</span></span> |<span data-ttu-id="f7408-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="f7408-159">#thresholdvalue</span></span> |<span data-ttu-id="f7408-160">Uyarı kuralı için eşik değer.</span><span class="sxs-lookup"><span data-stu-id="f7408-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="f7408-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="f7408-161">LinkToSearchResults</span></span> |<span data-ttu-id="f7408-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="f7408-162">#linktosearchresults</span></span> |<span data-ttu-id="f7408-163">Günlük analizi günlük kayıtları uyarı oluşturulan sorgudan döndüren bir arama bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f7408-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="f7408-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="f7408-164">ResultCount</span></span> |<span data-ttu-id="f7408-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="f7408-165">#searchresultcount</span></span> |<span data-ttu-id="f7408-166">Arama sonuçlarında kayıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="f7408-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="f7408-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="f7408-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="f7408-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="f7408-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="f7408-169">Bitiş saati UTC biçiminde bir sorgu için.</span><span class="sxs-lookup"><span data-stu-id="f7408-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="f7408-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="f7408-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="f7408-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="f7408-171">#searchinterval</span></span> |<span data-ttu-id="f7408-172">Zaman penceresi için uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="f7408-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="f7408-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="f7408-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="f7408-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="f7408-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="f7408-175">Sorgu saati UTC biçiminde başlatın.</span><span class="sxs-lookup"><span data-stu-id="f7408-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="f7408-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="f7408-176">SearchQuery</span></span> |<span data-ttu-id="f7408-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="f7408-177">#searchquery</span></span> |<span data-ttu-id="f7408-178">Uyarı kuralı tarafından kullanılan günlük arama sorgusu.</span><span class="sxs-lookup"><span data-stu-id="f7408-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="f7408-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="f7408-179">SearchResults</span></span> |<span data-ttu-id="f7408-180">Aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="f7408-180">See below</span></span> |<span data-ttu-id="f7408-181">JSON biçiminde sorgu tarafından döndürülen kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f7408-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="f7408-182">5. 000'ilk kayıtları sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="f7408-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="f7408-183">Workspaceıd</span><span class="sxs-lookup"><span data-stu-id="f7408-183">WorkspaceID</span></span> |<span data-ttu-id="f7408-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="f7408-184">#workspaceid</span></span> |<span data-ttu-id="f7408-185">OMS çalışma alanı kimliği.</span><span class="sxs-lookup"><span data-stu-id="f7408-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="f7408-186">Örneğin, adlı tek bir parametre içeren aşağıdaki özel yükü belirtebilir *metin*.</span><span class="sxs-lookup"><span data-stu-id="f7408-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="f7408-187">Bu Web kancası çağırır hizmet, bu parametre bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="f7408-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="f7408-188">Bu örnek yükü için Web kancası gönderildiğinde aşağıdaki gibi bir şey çözümlemek.</span><span class="sxs-lookup"><span data-stu-id="f7408-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="f7408-189">Özel bir yükte arama sonuçlarında en üst düzey özelliği json yükü olarak aşağıdaki satırı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f7408-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="f7408-190">Örneğin, yalnızca uyarı adı ve arama sonuçlarını içeren özel bir yükü oluşturmak için aşağıdakileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="f7408-191">Dış bir hizmeti başlatmak için bir Web kancası ile bir uyarı kuralı oluşturma tam bir örnek size yol [Slack'e ileti göndermek için OMS günlük analizi uyarı Web kancası eylem oluşturma](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="f7408-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="f7408-192">Runbook eylemleri</span><span class="sxs-lookup"><span data-stu-id="f7408-192">Runbook actions</span></span>
<span data-ttu-id="f7408-193">Runbook eylemleri, Azure Automation'da bir runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="f7408-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="f7408-194">Bu eylemin türünü kullanmak için bilmeniz gereken [Otomasyon çözümünü](log-analytics-add-solutions.md) yüklenir ve OMS çalışma alanınızda yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f7408-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="f7408-195">Otomasyon çözümünü yapılandırılmış Otomasyon hesabında runbook'ları arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7408-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="f7408-196">Runbook eylemleri özellikler aşağıdaki tabloda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f7408-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="f7408-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="f7408-197">Property</span></span> | <span data-ttu-id="f7408-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="f7408-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="f7408-199">Runbook</span></span> | <span data-ttu-id="f7408-200">Bir uyarı oluşturulduğunda başlatmak istediğiniz Runbook.</span><span class="sxs-lookup"><span data-stu-id="f7408-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="f7408-201">Üzerinde çalışır</span><span class="sxs-lookup"><span data-stu-id="f7408-201">Run on</span></span> | <span data-ttu-id="f7408-202">Belirtin **Azure** runbook bulutta çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="f7408-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="f7408-203">Belirtin **karma çalışanı** runbook'u ile bir aracı çalıştırmayı [karma Runbook çalışanı](../automation/automation-hybrid-runbook-worker.md ) yüklü.</span><span class="sxs-lookup"><span data-stu-id="f7408-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="f7408-204">Runbook eylemleri başlatmak kullanarak runbook bir [Web kancası](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="f7408-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="f7408-205">Uyarı kuralı oluşturduğunuzda, runbook için yeni bir Web kancası adı ile otomatik olarak oluşturacağı **OMS uyarı düzeltme** bir GUID ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="f7408-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="f7408-206">Runbook'un parametreleri doğrudan doldurulamıyor ancak [$WebhookData parametresi](../automation/automation-webhooks.md) oluşturulduğu günlük arama sonuçları dahil olmak üzere Uyarı ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f7408-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="f7408-207">Runbook tanımlamanız gereken **$WebhookData** uyarı özelliklerine erişmek için bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="f7408-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="f7408-208">Uyarı verileri json biçiminde adlı tek bir özellik bulunur **SearchResults** içinde **RequestBody** özelliği **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="f7408-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="f7408-209">Bu, aşağıdaki tabloda özelliklere sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f7408-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="f7408-210">Node</span><span class="sxs-lookup"><span data-stu-id="f7408-210">Node</span></span> | <span data-ttu-id="f7408-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7408-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f7408-212">id</span><span class="sxs-lookup"><span data-stu-id="f7408-212">id</span></span> |<span data-ttu-id="f7408-213">Yol ve arama GUID.</span><span class="sxs-lookup"><span data-stu-id="f7408-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="f7408-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="f7408-214">__metadata</span></span> |<span data-ttu-id="f7408-215">Arama sonuçlarını durumunu ve kayıt sayısı dahil olmak üzere uyarı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="f7408-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="f7408-216">değer</span><span class="sxs-lookup"><span data-stu-id="f7408-216">value</span></span> |<span data-ttu-id="f7408-217">Arama sonuçlarında her kayıt için ayrı girişi.</span><span class="sxs-lookup"><span data-stu-id="f7408-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="f7408-218">Giriş ayrıntılarını özellikleri ve kayıt değerleri ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="f7408-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="f7408-219">Örneğin, aşağıdaki runbook, günlük araması tarafından döndürülen kayıtları Ayıkla ve her kayıt türüne göre farklı özellikler atayın.</span><span class="sxs-lookup"><span data-stu-id="f7408-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="f7408-220">Runbook dönüştürerek başlatır Not **RequestBody** , BT ile PowerShell nesne olarak çalışılabilecek biçimde json öğesinden.</span><span class="sxs-lookup"><span data-stu-id="f7408-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="f7408-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f7408-221">Next steps</span></span>
- <span data-ttu-id="f7408-222">İzlenecek yollar için tamamlamak [bir webook yapılandırma](log-analytics-alerts-webhooks.md) bir uyarı kuralı ile.</span><span class="sxs-lookup"><span data-stu-id="f7408-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="f7408-223">Nasıl yazılacağını öğrenmek [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) uyarılar tarafından tanımlanan sorunları düzeltmek için.</span><span class="sxs-lookup"><span data-stu-id="f7408-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>
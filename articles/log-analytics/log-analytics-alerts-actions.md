---
title: "OMS günlük analizi içinde aaaResponses tooalerts | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya Eylemler tooattempt toocorrect çağırma bunları.  Bu makalede nasıl toocreate bir uyarı kuralı ve ayrıntıları hello farklı eylemlerini yapabilecekleri açıklanmaktadır."
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
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="84da7-104">Günlük analizi Eylemler tooalert kuralları ekleme</span><span class="sxs-lookup"><span data-stu-id="84da7-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="84da7-105">Zaman bir [uyarı günlük analizi oluşturulan](log-analytics-alerts.md), hello seçeneğiniz vardır [yapılandırma hello uyarı kuralı](log-analytics-alerts.md) tooperform bir veya daha fazla eylem.</span><span class="sxs-lookup"><span data-stu-id="84da7-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="84da7-106">Bu makalede, her tür yapılandırma üzerinde kullanılabilir hello farklı eylemler ve Ayrıntılar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84da7-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="84da7-107">Eylem</span><span class="sxs-lookup"><span data-stu-id="84da7-107">Action</span></span> | <span data-ttu-id="84da7-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="84da7-109">E-posta</span><span class="sxs-lookup"><span data-stu-id="84da7-109">Email</span></span>](#email-actions) | <span data-ttu-id="84da7-110">Merhaba uyarı tooone veya daha fazla alıcı hello ayrıntılarını içeren bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="84da7-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="84da7-111">Web kancası</span><span class="sxs-lookup"><span data-stu-id="84da7-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="84da7-112">Bir dış işlem tek bir HTTP POST isteği üzerinden çağırır.</span><span class="sxs-lookup"><span data-stu-id="84da7-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="84da7-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="84da7-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="84da7-114">Bir runbook, Azure Automation'da başlatın.</span><span class="sxs-lookup"><span data-stu-id="84da7-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="84da7-115">E-posta Eylemler</span><span class="sxs-lookup"><span data-stu-id="84da7-115">Email actions</span></span>
<span data-ttu-id="84da7-116">E-posta Eylemler hello uyarı tooone veya daha fazla alıcı hello ayrıntılarını içeren bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="84da7-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="84da7-117">Merhaba konu hello posta belirtebilirsiniz, ancak buna ait günlük analizi tarafından oluşturulan standart bir biçim içeriktir.</span><span class="sxs-lookup"><span data-stu-id="84da7-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="84da7-118">Merhaba günlük araması tarafından döndürülen tooten kayıtları yukarı toplama toodetails hello uyarı hello adı gibi özet bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="84da7-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="84da7-119">Bunu ayrıca bir bağlantı tooa günlük arama hello tüm kayıt kümesini Bu sorgudan döndürülecek günlük analizi içerir.</span><span class="sxs-lookup"><span data-stu-id="84da7-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="84da7-120">Merhaba gönderen hello posta *Microsoft Operations Management Suite ekibi &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="84da7-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="84da7-121">E-posta eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84da7-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="84da7-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="84da7-122">Property</span></span> | <span data-ttu-id="84da7-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="84da7-124">Konu</span><span class="sxs-lookup"><span data-stu-id="84da7-124">Subject</span></span> |<span data-ttu-id="84da7-125">Merhaba e-postayla konu.</span><span class="sxs-lookup"><span data-stu-id="84da7-125">Subject in hello email.</span></span>  <span data-ttu-id="84da7-126">Merhaba hello posta gövdesini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="84da7-127">Alıcıları</span><span class="sxs-lookup"><span data-stu-id="84da7-127">Recipients</span></span> |<span data-ttu-id="84da7-128">Tüm e-posta alıcıları adresleri.</span><span class="sxs-lookup"><span data-stu-id="84da7-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="84da7-129">Noktalı virgül (;) birden fazla adres sonra ayrı hello adresleri belirtirseniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="84da7-130">Web kancası eylemleri</span><span class="sxs-lookup"><span data-stu-id="84da7-130">Webhook actions</span></span>

<span data-ttu-id="84da7-131">Web kancası eylemleri tooinvoke bir dış işlem tek bir HTTP POST isteği üzerinden izin verin.</span><span class="sxs-lookup"><span data-stu-id="84da7-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="84da7-132">çağrılan hello Hizmet Web kancalarını destekleyen ve tüm yükü nasıl kullanacağınızı belirleyin aldığı.</span><span class="sxs-lookup"><span data-stu-id="84da7-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="84da7-133">Ayrıca hello isteği bir biçimde API anlar bu hello olduğu sürece, özellikle Web kancalarını desteklemeyen bir REST API'si çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="84da7-134">Bir Web kancası yanıt tooan uyarıda kullanma örnekleri bir ileti gönderiyorsunuz [Slack'e](http://slack.com) veya bir olay oluşturma [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="84da7-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="84da7-135">Bir Web kancası toocall kayma bir uyarı kuralı oluşturma izlenecek tam yol şu adresten edinilebilir [Kancalarını günlük analizi uyarılar](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="84da7-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="84da7-136">Web kancası eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84da7-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="84da7-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="84da7-137">Property</span></span> | <span data-ttu-id="84da7-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="84da7-139">Web kancası URL'si</span><span class="sxs-lookup"><span data-stu-id="84da7-139">Webhook URL</span></span> |<span data-ttu-id="84da7-140">Merhaba Web kancası URL'si Hello.</span><span class="sxs-lookup"><span data-stu-id="84da7-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="84da7-141">Özel JSON yükü</span><span class="sxs-lookup"><span data-stu-id="84da7-141">Custom JSON payload</span></span> |<span data-ttu-id="84da7-142">Özel yük toosend hello Web kancası ile.</span><span class="sxs-lookup"><span data-stu-id="84da7-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="84da7-143">Ayrıntılar için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="84da7-143">See below for details.</span></span> |


<span data-ttu-id="84da7-144">Web kancası URL ekleme ve toohello dış hizmet hello veriler JSON biçimlendirilmiş bir yükü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="84da7-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="84da7-145">Varsayılan olarak, aşağıdaki tablonun hello hello değerleri hello yükü içerir.</span><span class="sxs-lookup"><span data-stu-id="84da7-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="84da7-146">Bu yük kendi özel bir tane ile tooreplace seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="84da7-147">Bu durumda, hello tablosundaki hello değişkenler her hello parametreleri tooinclude değerlerine özel yükünüzü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="84da7-148">Parametre</span><span class="sxs-lookup"><span data-stu-id="84da7-148">Parameter</span></span> | <span data-ttu-id="84da7-149">Değişken</span><span class="sxs-lookup"><span data-stu-id="84da7-149">Variable</span></span> | <span data-ttu-id="84da7-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="84da7-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="84da7-151">AlertRuleName</span></span> |<span data-ttu-id="84da7-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="84da7-152">#alertrulename</span></span> |<span data-ttu-id="84da7-153">Merhaba uyarı kuralının adı.</span><span class="sxs-lookup"><span data-stu-id="84da7-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="84da7-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="84da7-154">AlertThresholdOperator</span></span> |<span data-ttu-id="84da7-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="84da7-155">#thresholdoperator</span></span> |<span data-ttu-id="84da7-156">Merhaba uyarı kuralı için eşik işleci.</span><span class="sxs-lookup"><span data-stu-id="84da7-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="84da7-157">*Büyük* veya *değerinden*.</span><span class="sxs-lookup"><span data-stu-id="84da7-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="84da7-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="84da7-158">AlertThresholdValue</span></span> |<span data-ttu-id="84da7-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="84da7-159">#thresholdvalue</span></span> |<span data-ttu-id="84da7-160">Merhaba uyarı kuralı için eşik değer.</span><span class="sxs-lookup"><span data-stu-id="84da7-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="84da7-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="84da7-161">LinkToSearchResults</span></span> |<span data-ttu-id="84da7-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="84da7-162">#linktosearchresults</span></span> |<span data-ttu-id="84da7-163">Merhaba uyarı oluşturulan hello sorgudan hello kayıtları döndüren tooLog Analytics günlük arama bağlayın.</span><span class="sxs-lookup"><span data-stu-id="84da7-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="84da7-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="84da7-164">ResultCount</span></span> |<span data-ttu-id="84da7-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="84da7-165">#searchresultcount</span></span> |<span data-ttu-id="84da7-166">Merhaba arama sonuçlarında kayıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="84da7-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="84da7-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="84da7-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="84da7-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="84da7-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="84da7-169">Bitiş saati UTC biçiminde hello sorgu için.</span><span class="sxs-lookup"><span data-stu-id="84da7-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="84da7-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="84da7-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="84da7-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="84da7-171">#searchinterval</span></span> |<span data-ttu-id="84da7-172">Merhaba uyarı kuralı için zaman penceresi.</span><span class="sxs-lookup"><span data-stu-id="84da7-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="84da7-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="84da7-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="84da7-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="84da7-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="84da7-175">UTC biçiminde hello sorgunun süresi başlatın.</span><span class="sxs-lookup"><span data-stu-id="84da7-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="84da7-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="84da7-176">SearchQuery</span></span> |<span data-ttu-id="84da7-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="84da7-177">#searchquery</span></span> |<span data-ttu-id="84da7-178">Merhaba uyarı kuralı tarafından kullanılan günlük arama sorgusu.</span><span class="sxs-lookup"><span data-stu-id="84da7-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="84da7-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="84da7-179">SearchResults</span></span> |<span data-ttu-id="84da7-180">Aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="84da7-180">See below</span></span> |<span data-ttu-id="84da7-181">JSON biçiminde hello sorgu tarafından döndürülen kaydeder.</span><span class="sxs-lookup"><span data-stu-id="84da7-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="84da7-182">Sınırlı toohello ilk 5.000 kaydeder.</span><span class="sxs-lookup"><span data-stu-id="84da7-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="84da7-183">Workspaceıd</span><span class="sxs-lookup"><span data-stu-id="84da7-183">WorkspaceID</span></span> |<span data-ttu-id="84da7-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="84da7-184">#workspaceid</span></span> |<span data-ttu-id="84da7-185">OMS çalışma alanı kimliği.</span><span class="sxs-lookup"><span data-stu-id="84da7-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="84da7-186">Örneğin, adlı tek bir parametre içeren özel yükü aşağıdaki hello belirtebilir *metin*.</span><span class="sxs-lookup"><span data-stu-id="84da7-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="84da7-187">Bu Web kancası çağırır hello hizmet, bu parametre bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="84da7-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="84da7-188">Bu örnek yükü hello olduğunda aşağıdaki gibi toosomething toohello Web kancası gönderilen çözümlemek.</span><span class="sxs-lookup"><span data-stu-id="84da7-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="84da7-189">özel bir yükü tooinclude arama sonuçlarında en üst düzey özellik hello json yükü olarak satırı aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="84da7-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="84da7-190">Örneğin, toocreate yalnızca hello uyarı adı ve hello arama sonuçlarını içeren özel bir yükü, aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="84da7-191">Bir uyarı kuralı, bir dış hizmeti ile bir Web kancası toostart oluşturma tam bir örnek size yol [OMS günlük analizi toosend ileti tooSlack uyarı Web kancası eylem oluşturma](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="84da7-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="84da7-192">Runbook eylemleri</span><span class="sxs-lookup"><span data-stu-id="84da7-192">Runbook actions</span></span>
<span data-ttu-id="84da7-193">Runbook eylemleri, Azure Automation'da bir runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="84da7-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="84da7-194">İçinde bu tür eylem toouse sipariş, hello olmalıdır [Otomasyon çözümünü](log-analytics-add-solutions.md) yüklenir ve OMS çalışma alanınızda yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="84da7-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="84da7-195">Merhaba Otomasyon çözümünü yapılandırılmış hello Otomasyon hesabı hello runbook'lar arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84da7-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="84da7-196">Runbook eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84da7-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="84da7-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="84da7-197">Property</span></span> | <span data-ttu-id="84da7-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="84da7-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="84da7-199">Runbook</span></span> | <span data-ttu-id="84da7-200">Runbook bir uyarı oluşturulduğunda toostart istiyor.</span><span class="sxs-lookup"><span data-stu-id="84da7-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="84da7-201">Üzerinde çalışır</span><span class="sxs-lookup"><span data-stu-id="84da7-201">Run on</span></span> | <span data-ttu-id="84da7-202">Belirtin **Azure** toorun hello runbook hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="84da7-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="84da7-203">Belirtin **karma çalışanı** toorun hello runbook ile bir aracı üzerinde [karma Runbook çalışanı](../automation/automation-hybrid-runbook-worker.md ) yüklü.</span><span class="sxs-lookup"><span data-stu-id="84da7-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="84da7-204">Runbook eylemleri başlatmak runbook hello kullanarak bir [Web kancası](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="84da7-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="84da7-205">Merhaba uyarı kuralı oluşturduğunuzda, yeni bir Web kancası hello runbook için hello adıyla otomatik olarak oluşturacağı **OMS uyarı düzeltme** bir GUID ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="84da7-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="84da7-206">Doğrudan hello runbook'un herhangi bir parametre doldurmak, ancak hello [$WebhookData parametresi](../automation/automation-webhooks.md) hello hello oluşturulduğu hello günlük arama sonuçlarını da dahil olmak üzere hello uyarı ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="84da7-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="84da7-207">Merhaba runbook toodefine gerekir **$WebhookData** bir parametre olarak hello uyarı özelliklerini tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="84da7-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="84da7-208">Merhaba uyarı verileri adlı tek bir özellik json biçiminde kullanılabilir **SearchResults** hello içinde **RequestBody** özelliği **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="84da7-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="84da7-209">Bu, aşağıdaki tablonun hello hello özellikleriyle gerekir.</span><span class="sxs-lookup"><span data-stu-id="84da7-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="84da7-210">Node</span><span class="sxs-lookup"><span data-stu-id="84da7-210">Node</span></span> | <span data-ttu-id="84da7-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84da7-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="84da7-212">id</span><span class="sxs-lookup"><span data-stu-id="84da7-212">id</span></span> |<span data-ttu-id="84da7-213">Yol ve hello GUİD'si arayın.</span><span class="sxs-lookup"><span data-stu-id="84da7-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="84da7-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="84da7-214">__metadata</span></span> |<span data-ttu-id="84da7-215">Merhaba uyarı dahil olmak üzere hello kayıt sayısını ve hello arama sonuçlarının durumu hakkındaki bilgileri.</span><span class="sxs-lookup"><span data-stu-id="84da7-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="84da7-216">değer</span><span class="sxs-lookup"><span data-stu-id="84da7-216">value</span></span> |<span data-ttu-id="84da7-217">Ayrı giriş hello arama sonuçlarında her kayıt için.</span><span class="sxs-lookup"><span data-stu-id="84da7-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="84da7-218">Merhaba girdisinin Hello ayrıntıları hello özellikleri ve değerleri hello kaydının eşleşir.</span><span class="sxs-lookup"><span data-stu-id="84da7-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="84da7-219">Örneğin, hello aşağıdaki runbook hello günlük araması tarafından döndürülen hello kayıtları ayıklayın ve hello her kayıt türüne göre farklı özelliklerini atayın.</span><span class="sxs-lookup"><span data-stu-id="84da7-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="84da7-220">Bu hello runbook başlatır dönüştürerek Not **RequestBody** , BT ile PowerShell nesne olarak çalışılabilecek biçimde json öğesinden.</span><span class="sxs-lookup"><span data-stu-id="84da7-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="84da7-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84da7-221">Next steps</span></span>
- <span data-ttu-id="84da7-222">İzlenecek yollar için tamamlamak [bir webook yapılandırma](log-analytics-alerts-webhooks.md) bir uyarı kuralı ile.</span><span class="sxs-lookup"><span data-stu-id="84da7-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="84da7-223">Öğrenin nasıl toowrite [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) tooremediate sorunları uyarıları ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="84da7-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>

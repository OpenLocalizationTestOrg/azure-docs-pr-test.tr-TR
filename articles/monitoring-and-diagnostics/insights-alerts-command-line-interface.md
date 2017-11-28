---
title: "Azure Hizmetleri - platformlar arası CLI aaaCreate uyarıları | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="caa9e-103">Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde, platformlar arası CLI oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="caa9e-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="caa9e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="caa9e-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="caa9e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="caa9e-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="caa9e-106">CLI</span><span class="sxs-lookup"><span data-stu-id="caa9e-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="caa9e-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="caa9e-107">Overview</span></span>
<span data-ttu-id="caa9e-108">Bu makale size nasıl tooset kullanarak Azure ölçüm uyarıları hello platformlar arası komut satırı arabirimi (CLI) gösterir.</span><span class="sxs-lookup"><span data-stu-id="caa9e-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="caa9e-109">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="caa9e-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="caa9e-110">Ancak, başlangıç ad alanları ve bu nedenle aşağıdaki hello komutları hala hello "ınsights" içeriyor.</span><span class="sxs-lookup"><span data-stu-id="caa9e-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="caa9e-111">İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caa9e-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="caa9e-112">**Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="caa9e-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="caa9e-113">Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.</span><span class="sxs-lookup"><span data-stu-id="caa9e-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="caa9e-114">**Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur.</span><span class="sxs-lookup"><span data-stu-id="caa9e-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="caa9e-115">Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="caa9e-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="caa9e-116">Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="caa9e-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="caa9e-117">e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder</span><span class="sxs-lookup"><span data-stu-id="caa9e-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="caa9e-118">e-posta, belirttiğiniz tooadditional e-postalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="caa9e-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="caa9e-119">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="caa9e-119">call a webhook</span></span>
* <span data-ttu-id="caa9e-120">bir Azure runbook'tan (yalnızca Azure portal şu anda hello) yürütülmesini Başlat</span><span class="sxs-lookup"><span data-stu-id="caa9e-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="caa9e-121">Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="caa9e-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="caa9e-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="caa9e-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="caa9e-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="caa9e-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="caa9e-124">komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="caa9e-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="caa9e-125">Azure monitör REST API'si</span><span class="sxs-lookup"><span data-stu-id="caa9e-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="caa9e-126">Bir komut yazarak komutlar için Yardım her zaman alabilir ve koyma - hello sonunda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="caa9e-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="caa9e-127">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="caa9e-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="caa9e-128">Merhaba CLI kullanarak uyarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa9e-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="caa9e-129">Merhaba önkoşulları ve oturum açma tooAzure gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="caa9e-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="caa9e-130">Bkz: [Azure İzleyici CLI örnekleri](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="caa9e-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="caa9e-131">Kısacası, hello CLI yükleyin ve bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="caa9e-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="caa9e-132">Bunlar, oturum açmış almak için hangi aboneliğe ve toorun Azure İzleyici komutları hazırlama göster.</span><span class="sxs-lookup"><span data-stu-id="caa9e-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="caa9e-133">toolist var olan bir kaynak grubu üzerinde kurallarıyla form aşağıdaki hello **uyarıları kural listesi azure Öngörüler** *[Seçenekler] &lt;kaynak grubu&gt;*</span><span class="sxs-lookup"><span data-stu-id="caa9e-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="caa9e-134">bir kural toocreate toohave birkaç önemli bilgi parçasından önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa9e-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="caa9e-135">Merhaba **kaynak kimliği** hello kaynak için bir uyarı tooset istiyor</span><span class="sxs-lookup"><span data-stu-id="caa9e-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="caa9e-136">Merhaba **ölçüm tanımlarını** kaynağı için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="caa9e-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="caa9e-137">Tek yönlü tooget hello kaynak kimliği toouse hello Azure portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="caa9e-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="caa9e-138">Merhaba kaynak zaten oluşturulmuş olduğu varsayılarak, hello Portalı'nda seçin.</span><span class="sxs-lookup"><span data-stu-id="caa9e-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="caa9e-139">Merhaba sonraki dikey penceresinde, ardından *özellikleri* hello altında *ayarları* bölümü.</span><span class="sxs-lookup"><span data-stu-id="caa9e-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="caa9e-140">Merhaba *kaynak kimliği* hello sonraki dikey penceresinde bir alandır.</span><span class="sxs-lookup"><span data-stu-id="caa9e-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="caa9e-141">Başka bir yoldur toouse hello [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="caa9e-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="caa9e-142">Bir web uygulaması için bir örnek kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="caa9e-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="caa9e-143">tooget hello kullanılabilir Ölçümler ve bu ölçümleri hello önceki kaynak Örneğin, CLI komutu aşağıdaki kullanım hello için birim listesi:</span><span class="sxs-lookup"><span data-stu-id="caa9e-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="caa9e-144">*PT1M* hello ayrıntı hello kullanılabilir ölçüm (1 dakikalık aralıklarla) kalıyor.</span><span class="sxs-lookup"><span data-stu-id="caa9e-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="caa9e-145">Farklı ayrıntı kullanarak farklı ölçüm seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="caa9e-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="caa9e-146">toocreate bir ölçüm tabanlı uyarı kuralı, hello form aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="caa9e-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="caa9e-147">**Uyarı kuralı ölçüm kümesi azure Öngörüler** *[Seçenekler] &lt;ruleName&gt; &lt;konumu&gt; &lt;resourceGroup&gt; &lt;pencereboyutu&gt; &lt;işleci&gt; &lt;eşik&gt; &lt;uç noktası Targetresourceıd&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="caa9e-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="caa9e-148">bir web sitesi kaynakta bir uyarı örnek ayarlar aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="caa9e-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="caa9e-149">5 dakikada bir ve yeniden zaman 5 dakika boyunca hiçbir trafik aldığı için herhangi bir trafik tutarlı bir şekilde aldığı zaman hello uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="caa9e-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="caa9e-150">Ölçüm bir uyarı oluşturulduğunda toocreate Web kancası veya gönderme e-posta, hello e-posta ve/veya Web kancalarını önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="caa9e-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="caa9e-151">Merhaba kural hemen oluşturmak daha sonra.</span><span class="sxs-lookup"><span data-stu-id="caa9e-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="caa9e-152">Web kancası veya e-posta kuralları hello CLI kullanarak önceden oluşturulmuş ilişkilendiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="caa9e-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="caa9e-153">Uyarılarınızı düzgün bir şekilde tek bir kuralı bakarak oluşturulduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caa9e-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="caa9e-154">toodelete kuralları, bir komut hello formunun kullanın:</span><span class="sxs-lookup"><span data-stu-id="caa9e-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="caa9e-155">**Uyarı kuralı silme Öngörüler** [Seçenekler] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="caa9e-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="caa9e-156">Bu komutlar, bu makalede daha önce oluşturduğunuz hello kuralları silin.</span><span class="sxs-lookup"><span data-stu-id="caa9e-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="caa9e-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="caa9e-157">Next steps</span></span>
* <span data-ttu-id="caa9e-158">[Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="caa9e-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="caa9e-159">Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="caa9e-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="caa9e-160">Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="caa9e-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="caa9e-161">Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="caa9e-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="caa9e-162">Alma bir [tanılama günlüklerinin toplanması genel bakış](monitoring-overview-of-diagnostic-logs.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="caa9e-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="caa9e-163">Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="caa9e-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>

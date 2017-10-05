---
title: "Azure Hizmetleri - platformlar arası CLI için uyarı oluşturma | Microsoft Docs"
description: "Belirttiğiniz koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
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
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="6b65f-103">Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde, platformlar arası CLI oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="6b65f-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b65f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6b65f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="6b65f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b65f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="6b65f-106">CLI</span><span class="sxs-lookup"><span data-stu-id="6b65f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="6b65f-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6b65f-107">Overview</span></span>
<span data-ttu-id="6b65f-108">Bu makalede platformlar arası komut satırı arabirimi (CLI) kullanarak Azure ölçüm uyarılarını ayarlama gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6b65f-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="6b65f-109">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="6b65f-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="6b65f-110">Bununla birlikte, ad alanları ve bu nedenle aşağıdaki komutları yine "ınsights" içerir.</span><span class="sxs-lookup"><span data-stu-id="6b65f-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="6b65f-111">İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b65f-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="6b65f-112">**Ölçüm değerleri** -herhangi bir yönde atadığınız bir eşik değeri, belirtilen bir ölçüm kestiği olduğunda uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="6b65f-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="6b65f-113">Diğer bir deyişle, her ikisi de tetikler koşul ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.</span><span class="sxs-lookup"><span data-stu-id="6b65f-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="6b65f-114">**Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur.</span><span class="sxs-lookup"><span data-stu-id="6b65f-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="6b65f-115">Etkinlik günlüğü Uyarıları hakkında daha fazla bilgi edinmek için [burayı tıklatın](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6b65f-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="6b65f-116">Tetikler, aşağıdakileri yapmak için bir ölçüm uyarısı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b65f-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="6b65f-117">Hizmet yöneticisini ve ortak Yöneticiler e-posta bildirimleri gönder</span><span class="sxs-lookup"><span data-stu-id="6b65f-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="6b65f-118">Belirttiğiniz ek e-postalar için e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="6b65f-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="6b65f-119">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="6b65f-119">call a webhook</span></span>
* <span data-ttu-id="6b65f-120">(yalnızca Azure portalından şu anda) Azure bir runbook'un yürütülmesi Başlat</span><span class="sxs-lookup"><span data-stu-id="6b65f-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="6b65f-121">Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="6b65f-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="6b65f-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6b65f-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="6b65f-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b65f-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="6b65f-124">komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="6b65f-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="6b65f-125">Azure monitör REST API'si</span><span class="sxs-lookup"><span data-stu-id="6b65f-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="6b65f-126">Bir komut yazarak komutlar için Yardım her zaman alabilir ve koyma - sonunda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6b65f-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="6b65f-127">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6b65f-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="6b65f-128">CLI kullanarak uyarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b65f-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="6b65f-129">Azure oturum açma ve önkoşullar gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b65f-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="6b65f-130">Bkz: [Azure İzleyici CLI örnekleri](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b65f-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="6b65f-131">Kısacası, CLI'yı yükledikten ve bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6b65f-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="6b65f-132">Bunlar, oturum açmış almak için kullanmakta olduğunuz ve Azure İzleyici komutları çalıştırmak için hazırlamanız hangi aboneliğe göster.</span><span class="sxs-lookup"><span data-stu-id="6b65f-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="6b65f-133">Bir kaynak grubu üzerinde mevcut kurallar listelemek için aşağıdaki formu kullanın **uyarıları kural listesi azure Öngörüler** *[Seçenekler] &lt;kaynak grubu&gt;*</span><span class="sxs-lookup"><span data-stu-id="6b65f-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="6b65f-134">Bir kural oluşturmak için birkaç önemli bilgi parçasından önce olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b65f-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="6b65f-135">**Kaynak kimliği** için uyarı ayarlamak istediğiniz kaynak için</span><span class="sxs-lookup"><span data-stu-id="6b65f-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="6b65f-136">**Ölçüm tanımlarını** kaynağı için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="6b65f-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="6b65f-137">Kaynak Kimliği almanın bir yolu, Azure Portalı'nı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="6b65f-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="6b65f-138">Kaynak zaten oluşturulmuş olduğu varsayılarak, portalda seçin.</span><span class="sxs-lookup"><span data-stu-id="6b65f-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="6b65f-139">Sonraki dikey penceresinde, ardından *özellikleri* altında *ayarları* bölümü.</span><span class="sxs-lookup"><span data-stu-id="6b65f-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="6b65f-140">*Kaynak kimliği* sonraki dikey bir alandır.</span><span class="sxs-lookup"><span data-stu-id="6b65f-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="6b65f-141">Başka bir yolu kullanmaktır [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6b65f-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="6b65f-142">Bir web uygulaması için bir örnek kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="6b65f-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="6b65f-143">Bu ölçümleri önceki kaynak örnek için kullanılabilir ölçümlere ve birimlerin listesini almak için aşağıdaki CLI komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="6b65f-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="6b65f-144">*PT1M* (1 dakikalık aralıklarla) kullanılabilir ölçü ayrıntı kalıyor.</span><span class="sxs-lookup"><span data-stu-id="6b65f-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="6b65f-145">Farklı ayrıntı kullanarak farklı ölçüm seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="6b65f-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="6b65f-146">Ölçüm tabanlı bir uyarı kuralı oluşturmak için aşağıdaki biçimde bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="6b65f-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="6b65f-147">**Uyarı kuralı ölçüm kümesi azure Öngörüler** *[Seçenekler] &lt;ruleName&gt; &lt;konumu&gt; &lt;resourceGroup&gt; &lt;pencereboyutu&gt; &lt;işleci&gt; &lt;eşik&gt; &lt;uç noktası Targetresourceıd&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="6b65f-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="6b65f-148">Aşağıdaki örnek bir web sitesi kaynakta bir uyarı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6b65f-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="6b65f-149">5 dakikada bir ve yeniden zaman 5 dakika boyunca hiçbir trafik aldığı için herhangi bir trafik tutarlı bir şekilde aldığında uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="6b65f-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="6b65f-150">Web kancası oluşturma veya ölçüm bir uyarı oluşturulduğunda e-posta göndermek için önce e-posta ve/veya Web kancası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b65f-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="6b65f-151">Kural hemen oluşturmak daha sonra.</span><span class="sxs-lookup"><span data-stu-id="6b65f-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="6b65f-152">CLI kullanarak kurallar önceden oluşturulmuş Web kancası veya e-posta ilişkilendiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b65f-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="6b65f-153">Uyarılarınızı düzgün bir şekilde tek bir kuralı bakarak oluşturulduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b65f-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="6b65f-154">Kural silmek için formun komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="6b65f-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="6b65f-155">**Uyarı kuralı silme Öngörüler** [Seçenekler] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="6b65f-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="6b65f-156">Bu komutlar, bu makalede daha önce oluşturduğunuz kurallar silin.</span><span class="sxs-lookup"><span data-stu-id="6b65f-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="6b65f-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b65f-157">Next steps</span></span>
* <span data-ttu-id="6b65f-158">[Azure izleme genel bir bakış elde](monitoring-overview.md) toplamak ve izlemek bilgi türlerini de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="6b65f-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="6b65f-159">Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6b65f-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="6b65f-160">Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6b65f-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="6b65f-161">Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6b65f-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="6b65f-162">Alma bir [tanılama günlüklerinin toplanması genel bakış](monitoring-overview-of-diagnostic-logs.md) hizmetinizde ayrıntılı yüksek sıklıkta ölçümleri toplamak için.</span><span class="sxs-lookup"><span data-stu-id="6b65f-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="6b65f-163">Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="6b65f-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>

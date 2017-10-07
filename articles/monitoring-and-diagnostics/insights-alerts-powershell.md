---
title: "Azure Hizmetleri - PowerShell aaaCreate uyarıları | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="1c7f0-103">Ölçüm uyarılar Azure İzleyicisi'nde Azure Hizmetleri - PowerShell oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c7f0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1c7f0-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="1c7f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c7f0-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="1c7f0-106">CLI</span><span class="sxs-lookup"><span data-stu-id="1c7f0-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="1c7f0-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1c7f0-107">Overview</span></span>
<span data-ttu-id="1c7f0-108">Bu makalede, Azure ölçüm yukarı tooset PowerShell kullanarak nasıl uyarıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="1c7f0-109">İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="1c7f0-110">**Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="1c7f0-111">Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="1c7f0-112">**Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="1c7f0-113">Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1c7f0-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="1c7f0-114">Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c7f0-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="1c7f0-115">e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder</span><span class="sxs-lookup"><span data-stu-id="1c7f0-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="1c7f0-116">e-posta, belirttiğiniz tooadditional e-postalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="1c7f0-117">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="1c7f0-117">call a webhook</span></span>
* <span data-ttu-id="1c7f0-118">bir Azure runbook'tan (yalnızca Azure portal hello) yürütülmesini Başlat</span><span class="sxs-lookup"><span data-stu-id="1c7f0-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="1c7f0-119">Yapılandırma ve uyarı kuralları kullanma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="1c7f0-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="1c7f0-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1c7f0-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="1c7f0-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c7f0-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="1c7f0-122">komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="1c7f0-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="1c7f0-123">Azure monitör REST API'si</span><span class="sxs-lookup"><span data-stu-id="1c7f0-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="1c7f0-124">Ek bilgi için her zaman yazabilirsiniz ```Get-Help``` ve PowerShell komutunu hakkında Yardım istediğiniz hello.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="1c7f0-125">PowerShell'de uyarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c7f0-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="1c7f0-126">TooAzure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="1c7f0-127">Bir listesini almak hello abonelikleri sahip olduğunuz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="1c7f0-128">Merhaba doğru aboneliği çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="1c7f0-129">Aksi takdirde, toohello sağa bir ayarla hello çıktısını kullanarak `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="1c7f0-130">toolist var olan bir kaynak grubu kurallarında hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c7f0-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="1c7f0-131">bir kural toocreate toohave birkaç önemli bilgi parçasından önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="1c7f0-132">Merhaba **kaynak kimliği** hello kaynak için bir uyarı tooset istiyor</span><span class="sxs-lookup"><span data-stu-id="1c7f0-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="1c7f0-133">Merhaba **ölçüm tanımlarını** kaynağı için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c7f0-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="1c7f0-134">Tek yönlü tooget hello kaynak kimliği toouse hello Azure portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="1c7f0-135">Merhaba kaynak zaten oluşturulmuş olduğu varsayılarak, hello Portalı'nda seçin.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="1c7f0-136">Merhaba sonraki dikey penceresinde, ardından *özellikleri* hello altında *ayarları* bölümü.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="1c7f0-137">**Kaynak Kimliği** hello sonraki dikey penceresinde bir alandır.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="1c7f0-138">Başka bir yoldur toouse hello [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1c7f0-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="1c7f0-139">Bir web uygulaması için bir örnek kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="1c7f0-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="1c7f0-140">Kullanabileceğiniz `Get-AzureRmMetricDefinition` tooview hello belirli bir kaynak için tüm ölçüm açıklamalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="1c7f0-141">Hello aşağıdaki örnek tablo hello ölçüm adı ile ve bu ölçümü için hello birim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="1c7f0-142">Get-AzureRmMetricDefinition için kullanılabilir seçenekleri tam bir listesi, Get-MetricDefinitions çalıştırarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="1c7f0-143">bir web sitesi kaynakta bir uyarı örnek ayarlar aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="1c7f0-144">5 dakikada bir ve yeniden zaman 5 dakika boyunca hiçbir trafik aldığı için herhangi bir trafik tutarlı bir şekilde aldığı zaman hello uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="1c7f0-145">bir uyarıyı tetikleyen zaman toocreate Web kancası veya gönderme e-posta, hello e-posta ve/veya Web kancalarını önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="1c7f0-146">Merhaba kural daha sonra hemen oluştururken hello - Eylemler etiketi ve hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="1c7f0-147">Web kancası veya e-posta zaten kuralları PowerShell aracılığıyla oluşturulan ilişkilendiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="1c7f0-148">uyarılarınızı düzgün şekilde hello tek tek kurallarında bakarak oluşturulduğunu tooverify.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="1c7f0-149">Uyarılarınızı silin.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-149">Delete your alerts.</span></span> <span data-ttu-id="1c7f0-150">Bu komutlar, bu makalede daha önce oluşturduğunuz hello kuralları silin.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="1c7f0-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c7f0-151">Next steps</span></span>
* <span data-ttu-id="1c7f0-152">[Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="1c7f0-153">Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1c7f0-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="1c7f0-154">Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1c7f0-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="1c7f0-155">Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1c7f0-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1c7f0-156">Alma bir [tanılama günlüklerinin toplanması genel bakış](monitoring-overview-of-diagnostic-logs.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="1c7f0-157">Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="1c7f0-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>

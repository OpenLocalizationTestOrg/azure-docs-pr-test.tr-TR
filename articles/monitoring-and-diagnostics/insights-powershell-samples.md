---
title: "Azure İzleyici PowerShell hızlı başlangıç örnekleri. | Microsoft Belgeleri"
description: "Otomatik ölçeklendirme, uyarılar, Web kancalarını ve etkinlik günlükleri arama gibi Azure İzleyicisi özelliklerine erişmek için PowerShell kullanın."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="dfb44-104">Azure İzleyici PowerShell hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="dfb44-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="dfb44-105">Bu makale Azure İzleyicisi özelliklerine erişmenize yardımcı olması için PowerShell komutlarını örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="dfb44-106">Azure İzleyici otomatik ölçeklendirme bulut Hizmetleri, sanal makineleri ve Web uygulamaları ve uyarı bildirimleri gönderebilir veya web URL'leri yapılandırılmış telemetri verilerini değerlerine göre arama için sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfb44-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="dfb44-107">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="dfb44-108">Bununla birlikte, ad alanları ve bu nedenle aşağıdaki komutları yine "ınsights" içerir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="dfb44-109">PowerShell ayarlayın</span><span class="sxs-lookup"><span data-stu-id="dfb44-109">Set up PowerShell</span></span>
<span data-ttu-id="dfb44-110">Henüz yapmadıysanız, bilgisayarınızda çalıştırmak için PowerShell ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="dfb44-111">Daha fazla bilgi için bkz: [yükleme ve yapılandırma PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfb44-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="dfb44-112">Bu makaledeki örnekler</span><span class="sxs-lookup"><span data-stu-id="dfb44-112">Examples in this article</span></span>
<span data-ttu-id="dfb44-113">Makaledeki örneklerde Azure İzleyici cmdlet'lerini nasıl kullanabileceğinizi göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="dfb44-114">Azure İzleyici PowerShell cmdlet'leri tüm listesini gözden geçirebilirsiniz [Azure İzleyicisi'ni (Öngörüler) cmdlet'leri](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb44-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="dfb44-115">Oturum açma ve abonelikleri kullanın</span><span class="sxs-lookup"><span data-stu-id="dfb44-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="dfb44-116">İlk olarak, Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="dfb44-117">Bu oturum açmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-117">This requires you to sign in.</span></span> <span data-ttu-id="dfb44-118">Hesabınızı yaptıktan sonra Tenantıd ve varsayılan abonelik kimliği görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="dfb44-119">Tüm Azure cmdlet'lerini varsayılan aboneliğinizin bağlamında çalışır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="dfb44-120">Erişiminiz Aboneliklerin listesini görüntülemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="dfb44-121">Farklı bir aboneliğe çalışma içeriğiniz değiştirmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="dfb44-122">Bir abonelik için etkinlik günlüğü Al</span><span class="sxs-lookup"><span data-stu-id="dfb44-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="dfb44-123">Kullanım `Get-AzureRmLog` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="dfb44-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="dfb44-124">Sık karşılaşılan bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-124">The following are some common examples.</span></span>

<span data-ttu-id="dfb44-125">Günlük girişlerini bu zaman/sunmak için başlangıç tarihi alın:</span><span class="sxs-lookup"><span data-stu-id="dfb44-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="dfb44-126">Günlük girdilerini arasında bir saat/tarih aralığı alın:</span><span class="sxs-lookup"><span data-stu-id="dfb44-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="dfb44-127">Günlük girişlerini belirli kaynak grubundan alın:</span><span class="sxs-lookup"><span data-stu-id="dfb44-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="dfb44-128">Bir saat/tarih aralığı arasında belirli bir kaynak Sağlayıcısı'ndan günlük girişlerini alın:</span><span class="sxs-lookup"><span data-stu-id="dfb44-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="dfb44-129">Tüm günlük girişleri belirli çağıran ile alın:</span><span class="sxs-lookup"><span data-stu-id="dfb44-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="dfb44-130">Aşağıdaki komut etkinlik günlüğünden son 1000 olayları alır:</span><span class="sxs-lookup"><span data-stu-id="dfb44-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="dfb44-131">`Get-AzureRmLog`pek çok parametrelerden destekler.</span><span class="sxs-lookup"><span data-stu-id="dfb44-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="dfb44-132">Bkz: `Get-AzureRmLog` daha fazla bilgi için başvuru.</span><span class="sxs-lookup"><span data-stu-id="dfb44-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="dfb44-133">`Get-AzureRmLog`yalnızca 15 gün geçmişi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfb44-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="dfb44-134">Kullanarak **- MaxEvents** parametresi, 15 gün ötesinde son N olayları sorgu olanak verir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="dfb44-135">Erişim için 15 gün sayısından önceki olayların, REST API veya SDK'sı (SDK'sını kullanarak C# örnek) kullanın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="dfb44-136">Dahil etmezseniz **StartTime**, varsayılan değer ise **EndTime** bir saat eksi.</span><span class="sxs-lookup"><span data-stu-id="dfb44-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="dfb44-137">Dahil etmezseniz **EndTime**, sonra da geçerli saati varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="dfb44-138">Tüm saatler UTC biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="dfb44-139">Uyarı geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="dfb44-139">Retrieve alerts history</span></span>
<span data-ttu-id="dfb44-140">Tüm uyarı olaylarını görüntülemek için aşağıdaki örnekleri kullanarak Azure Resource Manager günlüklerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="dfb44-141">Belirli bir uyarı kuralı geçmişini görüntülemek için kullanabileceğiniz `Get-AzureRmAlertHistory` cmdlet, uyarı kuralı kaynak Kimliğini geçirme.</span><span class="sxs-lookup"><span data-stu-id="dfb44-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="dfb44-142">`Get-AzureRmAlertHistory` Cmdlet çeşitli parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="dfb44-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="dfb44-143">Daha fazla bilgi için bkz: [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb44-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="dfb44-144">Uyarı kuralları hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="dfb44-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="dfb44-145">Aşağıdaki komutların tümü "montest" adlı bir kaynak grubu üzerinde davranır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="dfb44-146">Uyarı kuralı tüm özelliklerini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="dfb44-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="dfb44-147">Bir kaynak grubu üzerinde tüm uyarıları Al:</span><span class="sxs-lookup"><span data-stu-id="dfb44-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="dfb44-148">Tüm uyarı kuralı için bir hedef kaynak kümesini alır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="dfb44-149">Örneğin, bir VM üzerinde tüm uyarı kurallarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="dfb44-150">`Get-AzureRmAlertRule`diğer parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="dfb44-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="dfb44-151">Bkz: [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="dfb44-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="dfb44-152">Ölçüm uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfb44-152">Create metric alerts</span></span>
<span data-ttu-id="dfb44-153">Kullanabileceğiniz `Add-AlertRule` cmdlet'ini oluşturmak, güncelleştirmek veya bir uyarı kuralı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="dfb44-154">Kullanarak e-posta ve Web kancası özellikleri oluşturabilirsiniz `New-AzureRmAlertRuleEmail` ve `New-AzureRmAlertRuleWebhook`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="dfb44-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="dfb44-155">Uyarı kuralı cmdlet eylemlerini olarak atamak **Eylemler** uyarı kuralı özelliği.</span><span class="sxs-lookup"><span data-stu-id="dfb44-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="dfb44-156">Aşağıdaki tabloda, parametreler ve bir ölçüm kullanarak bir uyarı oluşturmak için kullanılan değerleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="dfb44-157">Parametre</span><span class="sxs-lookup"><span data-stu-id="dfb44-157">parameter</span></span> | <span data-ttu-id="dfb44-158">değer</span><span class="sxs-lookup"><span data-stu-id="dfb44-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="dfb44-159">Ad</span><span class="sxs-lookup"><span data-stu-id="dfb44-159">Name</span></span> |<span data-ttu-id="dfb44-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="dfb44-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="dfb44-161">Bu uyarı kuralı konumu</span><span class="sxs-lookup"><span data-stu-id="dfb44-161">Location of this alert rule</span></span> |<span data-ttu-id="dfb44-162">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="dfb44-162">East US</span></span> |
| <span data-ttu-id="dfb44-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfb44-163">ResourceGroup</span></span> |<span data-ttu-id="dfb44-164">montest</span><span class="sxs-lookup"><span data-stu-id="dfb44-164">montest</span></span> |
| <span data-ttu-id="dfb44-165">Uç noktası Targetresourceıd</span><span class="sxs-lookup"><span data-stu-id="dfb44-165">TargetResourceId</span></span> |<span data-ttu-id="dfb44-166">/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="dfb44-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="dfb44-167">Oluşturulan uyarının MetricName</span><span class="sxs-lookup"><span data-stu-id="dfb44-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="dfb44-168">\PhysicalDisk (_Total) \Disk Yazma/sn. Bkz: `Get-MetricDefinitions` cmdlet tam ölçüm adları alma hakkında</span><span class="sxs-lookup"><span data-stu-id="dfb44-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="dfb44-169">işleci</span><span class="sxs-lookup"><span data-stu-id="dfb44-169">operator</span></span> |<span data-ttu-id="dfb44-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="dfb44-170">GreaterThan</span></span> |
| <span data-ttu-id="dfb44-171">Eşik değeri (sayısı/sn olarak bu ölçüm için)</span><span class="sxs-lookup"><span data-stu-id="dfb44-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="dfb44-172">1</span><span class="sxs-lookup"><span data-stu-id="dfb44-172">1</span></span> |
| <span data-ttu-id="dfb44-173">Pencereboyutu (ss: dd: biçimi)</span><span class="sxs-lookup"><span data-stu-id="dfb44-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="dfb44-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="dfb44-174">00:05:00</span></span> |
| <span data-ttu-id="dfb44-175">Toplayıcı (istatistiği ölçüsünün ortalama sayısı, bu durumda kullanır)</span><span class="sxs-lookup"><span data-stu-id="dfb44-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="dfb44-176">Ortalama</span><span class="sxs-lookup"><span data-stu-id="dfb44-176">Average</span></span> |
| <span data-ttu-id="dfb44-177">özel e-postalar (dize dizisi)</span><span class="sxs-lookup"><span data-stu-id="dfb44-177">custom emails (string array)</span></span> |<span data-ttu-id="dfb44-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="dfb44-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="dfb44-179">sahipleri, Katkıda Bulunanlar ve okuyucular için e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="dfb44-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="dfb44-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="dfb44-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="dfb44-181">Bir e-posta eylem oluşturun</span><span class="sxs-lookup"><span data-stu-id="dfb44-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="dfb44-182">Bir Web kancası eylem oluşturun</span><span class="sxs-lookup"><span data-stu-id="dfb44-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="dfb44-183">Klasik bir VM'de CPU % ölçüm uyarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfb44-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="dfb44-184">Uyarı kuralı alma</span><span class="sxs-lookup"><span data-stu-id="dfb44-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="dfb44-185">Belirli özellikler için bir uyarı kuralı zaten varsa Ekle uyarı cmdlet de kuralı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="dfb44-186">Bir uyarı kuralı devre dışı bırakmak için parametresi dahil **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="dfb44-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="dfb44-187">Uyarılar için kullanılabilir ölçümler listesini al</span><span class="sxs-lookup"><span data-stu-id="dfb44-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="dfb44-188">Kullanabileceğiniz `Get-AzureRmMetricDefinition` belirli bir kaynak için tüm ölçümleri listesini görmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dfb44-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="dfb44-189">Aşağıdaki örnek, ölçüm adı içeren bir tablo ve onun için birim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfb44-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="dfb44-190">Tam listesi için kullanılabilir seçenekleri `Get-AzureRmMetricDefinition` şu adresten edinilebilir [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb44-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="dfb44-191">Otomatik ölçeklendirme ayarlarını oluşturun ve yönetin</span><span class="sxs-lookup"><span data-stu-id="dfb44-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="dfb44-192">VM, bulut hizmet veya sanal makine ölçek kümesi, bir Web uygulaması gibi bir kaynak için yapılandırılmış tek otomatik ölçeklendirme ayarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="dfb44-193">Bununla birlikte, her otomatik ölçeklendirme ayarında birden çok profil olabilir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="dfb44-194">Örneğin, bir performans tabanlı ölçek profili ve ikinci bir zamanlama tabanlı profil için.</span><span class="sxs-lookup"><span data-stu-id="dfb44-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="dfb44-195">Her profil yapılandırılmış birden çok kural bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="dfb44-196">Otomatik ölçeklendirme hakkında daha fazla bilgi için bkz: [otomatik ölçeklendirme bir uygulamanın nasıl](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="dfb44-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="dfb44-197">Kullanacağız adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dfb44-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="dfb44-198">Kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-198">Create rule(s).</span></span>
2. <span data-ttu-id="dfb44-199">Profillere daha önce oluşturduğunuz kurallar eşleme profillerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="dfb44-200">İsteğe bağlı: Web kancası ve e-posta özellikleri yapılandırarak otomatik ölçeklendirme bildirimleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="dfb44-201">Profilleri ve önceki adımlarda oluşturduğunuz bildirimler eşleyerek hedef kaynak üzerindeki bir ada sahip bir otomatik ölçeklendirme ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="dfb44-202">Aşağıdaki örnekler, bir sanal makine ölçek kümesi CPU kullanımı ölçümü kullanarak temel Windows işletim sistemi için otomatik ölçeklendirme ayarının nasıl oluşturabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="dfb44-203">İlk olarak, bir kural oluşturun örnek sayısı artan ölçek dışı.</span><span class="sxs-lookup"><span data-stu-id="dfb44-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="dfb44-204">Ardından, bir kural oluşturun ölçek bileşeniyle, bir örnek sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="dfb44-205">Ardından, kural için bir profil oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="dfb44-206">Bir Web kancası özellik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="dfb44-207">Bildirim özelliği otomatik ölçeklendirme ayarının, e-posta ve daha önce oluşturduğunuz Web kancası için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="dfb44-208">Son olarak, yukarıda oluşturduğunuz profili eklemek için otomatik ölçeklendirme ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfb44-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="dfb44-209">Otomatik ölçeklendirme ayarlarını yönetme hakkında daha fazla bilgi için bkz: [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb44-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="dfb44-210">Otomatik ölçeklendirme geçmişi</span><span class="sxs-lookup"><span data-stu-id="dfb44-210">Autoscale history</span></span>
<span data-ttu-id="dfb44-211">Aşağıdaki örnek, son otomatik ölçeklendirme ve uyarı olayları nasıl görüntüleyebileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="dfb44-212">Otomatik ölçeklendirme geçmişini görüntülemek için etkinlik günlüğü aramayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="dfb44-213">Kullanabileceğiniz `Get-AzureRmAutoScaleHistory` otomatik ölçeklendirme geçmişi almak üzere.</span><span class="sxs-lookup"><span data-stu-id="dfb44-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="dfb44-214">Daha fazla bilgi için bkz: [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb44-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="dfb44-215">Otomatik ölçeklendirme ayarı için ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="dfb44-215">View details for an autoscale setting</span></span>
<span data-ttu-id="dfb44-216">Kullanabileceğiniz `Get-Autoscalesetting` otomatik ölçeklendirme ayarı hakkında daha fazla bilgi almak üzere.</span><span class="sxs-lookup"><span data-stu-id="dfb44-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="dfb44-217">Aşağıdaki örnekte kaynak grubu 'myrg1' tüm otomatik ölçeklendirme ayarları hakkında ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="dfb44-218">Aşağıdaki örnekte kaynak grubu 'myrg1' tüm otomatik ölçeklendirme ayarlarını ve özellikle 'MyScaleVMSSSetting' adlı otomatik ölçeklendirme ayarı hakkında ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfb44-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="dfb44-219">Otomatik ölçeklendirme ayarı kaldırın</span><span class="sxs-lookup"><span data-stu-id="dfb44-219">Remove an autoscale setting</span></span>
<span data-ttu-id="dfb44-220">Kullanabileceğiniz `Remove-Autoscalesetting` cmdlet'ini bir otomatik ölçeklendirme ayarı silin.</span><span class="sxs-lookup"><span data-stu-id="dfb44-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="dfb44-221">Etkinlik günlüğü için günlük profilleri Yönet</span><span class="sxs-lookup"><span data-stu-id="dfb44-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="dfb44-222">Oluşturabileceğiniz bir *oturum profili* ve etkinlik günlüğü verileri dışa bir depolama hesabı ve veri saklama için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="dfb44-223">İsteğe bağlı olarak, olay Hub'ınıza ayrıca veri akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="dfb44-224">Bu özellik şu anda Önizleme ve, olduğuna dikkat edin, yalnızca abonelik başına bir günlük profili oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="dfb44-225">Günlük profilleri oluşturmak ve yönetmek için geçerli aboneliğiniz ile aşağıdaki cmdlet'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="dfb44-226">Belirli bir abonelik de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="dfb44-227">Geçerli abonelik PowerShell Varsayılanları olsalar bile, her zaman bu kullanarak değiştirebilirsiniz `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="dfb44-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="dfb44-228">Etkinlik günlüğü herhangi bir depolama hesabı veya olay hub'ın bu abonelik içindeki rota verileri için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="dfb44-229">Veriler JSON biçiminde blob dosyaları olarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="dfb44-230">Günlük profilini Al</span><span class="sxs-lookup"><span data-stu-id="dfb44-230">Get a log profile</span></span>
<span data-ttu-id="dfb44-231">Var olan günlük profillerinizi getirmek için kullanmak `Get-AzureRmLogProfile` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="dfb44-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="dfb44-232">Veri saklama olmayan günlük profili Ekle</span><span class="sxs-lookup"><span data-stu-id="dfb44-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="dfb44-233">Günlük profilini Kaldır</span><span class="sxs-lookup"><span data-stu-id="dfb44-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="dfb44-234">Veri saklama günlük profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="dfb44-234">Add a log profile with data retention</span></span>
<span data-ttu-id="dfb44-235">Belirleyebileceğiniz **- RetentionInDays** özelliği ile verileri nerede tutulur, pozitif bir tamsayı olarak gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="dfb44-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="dfb44-236">Günlük profiliyle saklama ve EventHub ekleyin</span><span class="sxs-lookup"><span data-stu-id="dfb44-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="dfb44-237">Depolama hesabına verilerinizi yönlendirmenin yanı sıra, ayrıca, bir olay Hub'ına akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfb44-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="dfb44-238">Bu önizleme sürümü ve depolama hesabı yapılandırması zorunludur ancak olay hub'ı yapılandırma isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dfb44-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="dfb44-239">Tanılama günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dfb44-239">Configure diagnostics logs</span></span>
<span data-ttu-id="dfb44-240">Çoğu Azure hizmeti ek günlükleri ve yapılandırılan Azure depolama hesabınızdaki veri kaydetmek için Event Hubs'a gönderme ve/veya bir OMS günlük analizi çalışma alanına gönderilen telemetriyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfb44-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="dfb44-241">Bu işlem yalnızca bir kaynak düzeyinde gerçekleştirilebilir ve depolama hesabı veya olay hub'ı tanılama ayarını yapılandırıldığı aynı bölgede hedef kaynak olarak mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dfb44-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="dfb44-242">Tanılama ayarını alma</span><span class="sxs-lookup"><span data-stu-id="dfb44-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="dfb44-243">Tanılama ayarını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="dfb44-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="dfb44-244">Bekletme olmadan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dfb44-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="dfb44-245">Bekletme olan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dfb44-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="dfb44-246">Bekletme belirli günlük kategori için tanılama ayarıyla etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dfb44-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="dfb44-247">Olay hub'ları için tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dfb44-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="dfb44-248">OMS tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dfb44-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```

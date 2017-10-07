---
title: "aaaAzure İzleyici PowerShell hızlı başlangıç örnekleri. | Microsoft Belgeleri"
description: "PowerShell tooaccess otomatik ölçeklendirme, uyarılar, Web kancalarını ve etkinlik günlükleri arama gibi Azure İzleyicisi özellikleri kullanın."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="07fef-104">Azure İzleyici PowerShell hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="07fef-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="07fef-105">Bu makale Azure İzleyicisi özelliklerine erişim PowerShell komutları toohelp örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="07fef-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="07fef-106">Azure İzleyici tooAutoScale bulut Hizmetleri, sanal makineler ve Web uygulamaları ve toosend Uyarı bildirimlerinin veya yapılandırılmış telemetri verilerini değerlerine göre çağrısı web URL'leri sağlar.</span><span class="sxs-lookup"><span data-stu-id="07fef-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="07fef-107">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="07fef-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="07fef-108">Bununla birlikte, hello ad alanları ve bu nedenle hala komutları aşağıdaki hello hello "ınsights" içerir.</span><span class="sxs-lookup"><span data-stu-id="07fef-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="07fef-109">PowerShell ayarlayın</span><span class="sxs-lookup"><span data-stu-id="07fef-109">Set up PowerShell</span></span>
<span data-ttu-id="07fef-110">Henüz yapmadıysanız, bilgisayarınızda PowerShell toorun ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="07fef-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="07fef-111">Daha fazla bilgi için bkz: [nasıl tooInstall ve yapılandırma PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07fef-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="07fef-112">Bu makaledeki örnekler</span><span class="sxs-lookup"><span data-stu-id="07fef-112">Examples in this article</span></span>
<span data-ttu-id="07fef-113">Merhaba örnekler hello makalede Azure İzleyici cmdlet'lerini nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="07fef-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="07fef-114">Merhaba tüm Azure İzleyici PowerShell cmdlet'leri listesini gözden geçirebilirsiniz [Azure İzleyicisi'ni (Öngörüler) cmdlet'leri](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fef-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="07fef-115">Oturum açma ve abonelikleri kullanın</span><span class="sxs-lookup"><span data-stu-id="07fef-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="07fef-116">İlk olarak, tooyour Azure aboneliği oturum açın.</span><span class="sxs-lookup"><span data-stu-id="07fef-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="07fef-117">Bu, toosign gerektirir.</span><span class="sxs-lookup"><span data-stu-id="07fef-117">This requires you toosign in.</span></span> <span data-ttu-id="07fef-118">Hesabınızı yaptıktan sonra Tenantıd ve varsayılan abonelik kimliği görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="07fef-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="07fef-119">Tüm Azure cmdlet'lerini iş varsayılan aboneliğinizin hello bağlamında hello.</span><span class="sxs-lookup"><span data-stu-id="07fef-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="07fef-120">tooview hello Aboneliklerin listesini erişebilirsiniz, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="07fef-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="07fef-121">toochange çalışma bağlam tooa farklı aboneliğiniz, komutu aşağıdaki kullanım hello.</span><span class="sxs-lookup"><span data-stu-id="07fef-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="07fef-122">Bir abonelik için etkinlik günlüğü Al</span><span class="sxs-lookup"><span data-stu-id="07fef-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="07fef-123">Kullanım hello `Get-AzureRmLog` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="07fef-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="07fef-124">Merhaba, ortak bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="07fef-124">hello following are some common examples.</span></span>

<span data-ttu-id="07fef-125">Günlük girişlerini bu saat/tarih toopresent alın:</span><span class="sxs-lookup"><span data-stu-id="07fef-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="07fef-126">Günlük girdilerini arasında bir saat/tarih aralığı alın:</span><span class="sxs-lookup"><span data-stu-id="07fef-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="07fef-127">Günlük girişlerini belirli kaynak grubundan alın:</span><span class="sxs-lookup"><span data-stu-id="07fef-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="07fef-128">Bir saat/tarih aralığı arasında belirli bir kaynak Sağlayıcısı'ndan günlük girişlerini alın:</span><span class="sxs-lookup"><span data-stu-id="07fef-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="07fef-129">Tüm günlük girişleri belirli çağıran ile alın:</span><span class="sxs-lookup"><span data-stu-id="07fef-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="07fef-130">Son 1000 hello etkinlik günlüğü olaylarını alır hello komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="07fef-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="07fef-131">`Get-AzureRmLog`pek çok parametrelerden destekler.</span><span class="sxs-lookup"><span data-stu-id="07fef-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="07fef-132">Merhaba bkz `Get-AzureRmLog` daha fazla bilgi için başvuru.</span><span class="sxs-lookup"><span data-stu-id="07fef-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="07fef-133">`Get-AzureRmLog`yalnızca 15 gün geçmişi sağlar.</span><span class="sxs-lookup"><span data-stu-id="07fef-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="07fef-134">Hello kullanarak **- MaxEvents** parametresi, tooquery hello son N olayları, 15 gün ötesinde verir.</span><span class="sxs-lookup"><span data-stu-id="07fef-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="07fef-135">15 günden eski tooaccess olayları hello REST API veya SDK'sı (Merhaba SDK kullanarak C# örnek) kullanın.</span><span class="sxs-lookup"><span data-stu-id="07fef-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="07fef-136">Dahil etmezseniz **StartTime**, hello varsayılan değer ise **EndTime** bir saat eksi.</span><span class="sxs-lookup"><span data-stu-id="07fef-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="07fef-137">Dahil etmezseniz **EndTime**, geçerli saati hello varsayılan değeri olur.</span><span class="sxs-lookup"><span data-stu-id="07fef-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="07fef-138">Tüm saatler UTC biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="07fef-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="07fef-139">Uyarı geçmişini alma</span><span class="sxs-lookup"><span data-stu-id="07fef-139">Retrieve alerts history</span></span>
<span data-ttu-id="07fef-140">tüm olayları Sorgulayabileceğiniz uyarı tooview örnek hello kullanarak Azure Resource Manager günlüklerini hello.</span><span class="sxs-lookup"><span data-stu-id="07fef-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="07fef-141">tooview hello geçmişi için özel bir uyarı kuralı, hello kullanabileceğiniz `Get-AzureRmAlertHistory` cmdlet, hello uyarı kuralının kaynak Kimliğine hello geçirme.</span><span class="sxs-lookup"><span data-stu-id="07fef-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="07fef-142">Merhaba `Get-AzureRmAlertHistory` cmdlet çeşitli parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="07fef-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="07fef-143">Daha fazla bilgi için bkz: [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fef-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="07fef-144">Uyarı kuralları hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="07fef-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="07fef-145">Tüm komutları aşağıdaki hello "montest" adlı bir kaynak grubu üzerinde davranır.</span><span class="sxs-lookup"><span data-stu-id="07fef-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="07fef-146">Merhaba uyarı kuralı tüm hello özelliklerini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="07fef-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="07fef-147">Bir kaynak grubu üzerinde tüm uyarıları Al:</span><span class="sxs-lookup"><span data-stu-id="07fef-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="07fef-148">Tüm uyarı kuralı için bir hedef kaynak kümesini alır.</span><span class="sxs-lookup"><span data-stu-id="07fef-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="07fef-149">Örneğin, bir VM üzerinde tüm uyarı kurallarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="07fef-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="07fef-150">`Get-AzureRmAlertRule`diğer parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="07fef-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="07fef-151">Bkz: [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="07fef-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="07fef-152">Ölçüm uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="07fef-152">Create metric alerts</span></span>
<span data-ttu-id="07fef-153">Merhaba kullanabilirsiniz `Add-AlertRule` cmdlet toocreate güncelleştirmek veya bir uyarı kuralı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="07fef-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="07fef-154">Kullanarak e-posta ve Web kancası özellikleri oluşturabilirsiniz `New-AzureRmAlertRuleEmail` ve `New-AzureRmAlertRuleWebhook`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="07fef-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="07fef-155">Merhaba uyarı kuralı cmdlet'te, bu eylemleri toohello olarak atamak **Eylemler** hello uyarı kuralı özelliği.</span><span class="sxs-lookup"><span data-stu-id="07fef-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="07fef-156">Aşağıdaki tablonun hello hello parametreleri açıklar ve bir ölçüm kullanarak bir uyarı kullanılan toocreate değerleri.</span><span class="sxs-lookup"><span data-stu-id="07fef-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="07fef-157">Parametre</span><span class="sxs-lookup"><span data-stu-id="07fef-157">parameter</span></span> | <span data-ttu-id="07fef-158">değer</span><span class="sxs-lookup"><span data-stu-id="07fef-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="07fef-159">Ad</span><span class="sxs-lookup"><span data-stu-id="07fef-159">Name</span></span> |<span data-ttu-id="07fef-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="07fef-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="07fef-161">Bu uyarı kuralı konumu</span><span class="sxs-lookup"><span data-stu-id="07fef-161">Location of this alert rule</span></span> |<span data-ttu-id="07fef-162">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="07fef-162">East US</span></span> |
| <span data-ttu-id="07fef-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="07fef-163">ResourceGroup</span></span> |<span data-ttu-id="07fef-164">montest</span><span class="sxs-lookup"><span data-stu-id="07fef-164">montest</span></span> |
| <span data-ttu-id="07fef-165">Uç noktası Targetresourceıd</span><span class="sxs-lookup"><span data-stu-id="07fef-165">TargetResourceId</span></span> |<span data-ttu-id="07fef-166">/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="07fef-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="07fef-167">Oluşturulan hello uyarının MetricName</span><span class="sxs-lookup"><span data-stu-id="07fef-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="07fef-168">\PhysicalDisk (_Total) \Disk Yazma/sn. Merhaba bkz `Get-MetricDefinitions` cmdlet'inin nasıl tooretrieve hello tam ölçüm adlar hakkında</span><span class="sxs-lookup"><span data-stu-id="07fef-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="07fef-169">işleci</span><span class="sxs-lookup"><span data-stu-id="07fef-169">operator</span></span> |<span data-ttu-id="07fef-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="07fef-170">GreaterThan</span></span> |
| <span data-ttu-id="07fef-171">Eşik değeri (sayısı/sn olarak bu ölçüm için)</span><span class="sxs-lookup"><span data-stu-id="07fef-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="07fef-172">1</span><span class="sxs-lookup"><span data-stu-id="07fef-172">1</span></span> |
| <span data-ttu-id="07fef-173">Pencereboyutu (ss: dd: biçimi)</span><span class="sxs-lookup"><span data-stu-id="07fef-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="07fef-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="07fef-174">00:05:00</span></span> |
| <span data-ttu-id="07fef-175">Toplayıcı (ortalama sayısı, bu durumda kullanır hello ölçüsünün istatistiği)</span><span class="sxs-lookup"><span data-stu-id="07fef-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="07fef-176">Ortalama</span><span class="sxs-lookup"><span data-stu-id="07fef-176">Average</span></span> |
| <span data-ttu-id="07fef-177">özel e-postalar (dize dizisi)</span><span class="sxs-lookup"><span data-stu-id="07fef-177">custom emails (string array)</span></span> |<span data-ttu-id="07fef-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="07fef-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="07fef-179">e-posta tooowners, Katkıda Bulunanlar ve okuyucular Gönder</span><span class="sxs-lookup"><span data-stu-id="07fef-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="07fef-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="07fef-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="07fef-181">Bir e-posta eylem oluşturun</span><span class="sxs-lookup"><span data-stu-id="07fef-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="07fef-182">Bir Web kancası eylem oluşturun</span><span class="sxs-lookup"><span data-stu-id="07fef-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="07fef-183">Merhaba CPU % ölçüm klasik bir VM'de Hello uyarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="07fef-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="07fef-184">Merhaba uyarı kuralını Al</span><span class="sxs-lookup"><span data-stu-id="07fef-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="07fef-185">bir uyarı kuralı özellikleri verilen Merhaba zaten varsa hello Ekle uyarı cmdlet ayrıca hello kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="07fef-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="07fef-186">toodisable bir uyarı kuralı dahil hello parametresi **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="07fef-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="07fef-187">Uyarılar için kullanılabilir ölçümler listesini al</span><span class="sxs-lookup"><span data-stu-id="07fef-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="07fef-188">Merhaba kullanabilirsiniz `Get-AzureRmMetricDefinition` cmdlet tooview hello belirli bir kaynak için tüm ölçümleri listesi.</span><span class="sxs-lookup"><span data-stu-id="07fef-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="07fef-189">Merhaba aşağıdaki örnek hello ölçüm adı ile tablo ve onun için birim hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="07fef-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="07fef-190">Tam listesi için kullanılabilir seçenekleri `Get-AzureRmMetricDefinition` şu adresten edinilebilir [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fef-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="07fef-191">Otomatik ölçeklendirme ayarlarını oluşturun ve yönetin</span><span class="sxs-lookup"><span data-stu-id="07fef-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="07fef-192">VM, bulut hizmet veya sanal makine ölçek kümesi, bir Web uygulaması gibi bir kaynak için yapılandırılmış tek otomatik ölçeklendirme ayarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="07fef-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="07fef-193">Bununla birlikte, her otomatik ölçeklendirme ayarında birden çok profil olabilir.</span><span class="sxs-lookup"><span data-stu-id="07fef-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="07fef-194">Örneğin, bir performans tabanlı ölçek profili ve ikinci bir zamanlama tabanlı profil için.</span><span class="sxs-lookup"><span data-stu-id="07fef-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="07fef-195">Her profil yapılandırılmış birden çok kural bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="07fef-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="07fef-196">Otomatik ölçeklendirme hakkında daha fazla bilgi için bkz: [nasıl tooAutoscale uygulama](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="07fef-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="07fef-197">Kullanacağız hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="07fef-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="07fef-198">Kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-198">Create rule(s).</span></span>
2. <span data-ttu-id="07fef-199">Profil oluşturma eşleme hello kuralları toohello profilleri daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="07fef-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="07fef-200">İsteğe bağlı: Web kancası ve e-posta özellikleri yapılandırarak otomatik ölçeklendirme bildirimleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="07fef-201">Hello profilleri ve hello önceki adımlarda oluşturduğunuz bildirimler eşleyerek hello hedef kaynak üzerindeki bir ada sahip bir otomatik ölçeklendirme ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="07fef-202">Merhaba Aşağıdaki örnekler, bir sanal makine ölçek kümesi'hello CPU kullanımı ölçümü kullanarak temel Windows işletim sistemi için otomatik ölçeklendirme ayarının nasıl oluşturabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="07fef-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="07fef-203">İlk olarak, bir kural tooscale genişletme, örnek sayısı artışı ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="07fef-204">Ardından, bir kural tooscale içinde bir örnek sayısı azaltma ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="07fef-205">Ardından, hello kuralları için bir profil oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="07fef-206">Bir Web kancası özellik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="07fef-207">E-posta dahil olmak üzere hello otomatik ölçeklendirme ayarının Hello bildirim özelliği oluşturabilir ve daha önce oluşturduğunuz Web kancası hello.</span><span class="sxs-lookup"><span data-stu-id="07fef-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="07fef-208">Son olarak, yukarıda oluşturduğunuz hello otomatik ölçeklendirme ayarı tooadd hello profili oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07fef-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="07fef-209">Otomatik ölçeklendirme ayarlarını yönetme hakkında daha fazla bilgi için bkz: [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fef-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="07fef-210">Otomatik ölçeklendirme geçmişi</span><span class="sxs-lookup"><span data-stu-id="07fef-210">Autoscale history</span></span>
<span data-ttu-id="07fef-211">Merhaba aşağıdaki örnekte, son otomatik ölçeklendirme ve uyarı olayları nasıl görüntüleyebileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="07fef-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="07fef-212">Merhaba etkinlik günlüğü arama tooview hello otomatik ölçeklendirme geçmişini kullanın.</span><span class="sxs-lookup"><span data-stu-id="07fef-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="07fef-213">Merhaba kullanabilirsiniz `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve otomatik ölçeklendirme geçmişi.</span><span class="sxs-lookup"><span data-stu-id="07fef-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="07fef-214">Daha fazla bilgi için bkz: [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fef-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="07fef-215">Otomatik ölçeklendirme ayarı için ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="07fef-215">View details for an autoscale setting</span></span>
<span data-ttu-id="07fef-216">Merhaba kullanabilirsiniz `Get-Autoscalesetting` cmdlet tooretrieve hello otomatik ölçeklendirme ayarı hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="07fef-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="07fef-217">Merhaba aşağıdaki örnekte tüm otomatik ölçeklendirme ayarları hakkında ayrıntılı hello kaynak grubu 'myrg1' gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="07fef-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="07fef-218">Merhaba aşağıdaki örnekte tüm otomatik ölçeklendirme ayarları hakkında ayrıntılı hello kaynak grubu 'myrg1' gösterir ve özellikle 'MyScaleVMSSSetting' adlı otomatik ölçeklendirme ayarı hello.</span><span class="sxs-lookup"><span data-stu-id="07fef-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="07fef-219">Otomatik ölçeklendirme ayarı kaldırın</span><span class="sxs-lookup"><span data-stu-id="07fef-219">Remove an autoscale setting</span></span>
<span data-ttu-id="07fef-220">Merhaba kullanabilirsiniz `Remove-Autoscalesetting` cmdlet toodelete bir otomatik ölçeklendirme ayarı.</span><span class="sxs-lookup"><span data-stu-id="07fef-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="07fef-221">Etkinlik günlüğü için günlük profilleri Yönet</span><span class="sxs-lookup"><span data-stu-id="07fef-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="07fef-222">Oluşturabileceğiniz bir *oturum profili* ve etkinlik günlüğü tooa depolama hesabınız ve verileri dışa veri saklama için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07fef-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="07fef-223">İsteğe bağlı olarak, hello veri tooyour olay hub'ı akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07fef-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="07fef-224">Bu özellik şu anda Önizleme ve, olduğuna dikkat edin, yalnızca abonelik başına bir günlük profili oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07fef-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="07fef-225">Geçerli abonelik toocreate cmdlet'leriyle aşağıdaki hello kullanın ve günlük profillerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="07fef-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="07fef-226">Belirli bir abonelik de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07fef-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="07fef-227">PowerShell toohello geçerli abonelik Varsayılanları olsalar bile, her zaman bu kullanarak değiştirebilirsiniz `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="07fef-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="07fef-228">Bu aboneliğin etkinlik günlüğü tooroute veri tooany depolama hesabı veya olay hub'ı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07fef-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="07fef-229">Veriler JSON biçiminde blob dosyaları olarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="07fef-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="07fef-230">Günlük profilini Al</span><span class="sxs-lookup"><span data-stu-id="07fef-230">Get a log profile</span></span>
<span data-ttu-id="07fef-231">toofetch mevcut günlük profillerinizi kullanmak hello `Get-AzureRmLogProfile` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="07fef-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="07fef-232">Veri saklama olmayan günlük profili Ekle</span><span class="sxs-lookup"><span data-stu-id="07fef-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="07fef-233">Günlük profilini Kaldır</span><span class="sxs-lookup"><span data-stu-id="07fef-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="07fef-234">Veri saklama günlük profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="07fef-234">Add a log profile with data retention</span></span>
<span data-ttu-id="07fef-235">Merhaba belirtebilirsiniz **- RetentionInDays** hello verileri nerede tutulur, pozitif bir tamsayı olarak gün hello sayısı özelliği.</span><span class="sxs-lookup"><span data-stu-id="07fef-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="07fef-236">Günlük profiliyle saklama ve EventHub ekleyin</span><span class="sxs-lookup"><span data-stu-id="07fef-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="07fef-237">Toplama toorouting veri toostorage hesabınızı, ayrıca, sağlanabilir tooan olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="07fef-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="07fef-238">Bu önizleme sürümü ve hello depolama hesabı yapılandırması zorunludur ancak olay hub'ı yapılandırma isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="07fef-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="07fef-239">Tanılama günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="07fef-239">Configure diagnostics logs</span></span>
<span data-ttu-id="07fef-240">Çoğu Azure hizmeti ek günlükleri ve yapılandırılmış toosave veriler Azure depolama hesabınızdaki olabilir telemetri Gönder tooEvent hub sağlamak ve/veya tooan OMS günlük analizi çalışma alanı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="07fef-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="07fef-241">Bu işlem yalnızca bir kaynak düzeyinde gerçekleştirilebilir ve hello depolama hesabı veya olay hub'hello mevcut hello tanılama ayarını yapılandırdığınız yerde aynı bölgede hello hedef kaynak olarak.</span><span class="sxs-lookup"><span data-stu-id="07fef-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="07fef-242">Tanılama ayarını alma</span><span class="sxs-lookup"><span data-stu-id="07fef-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="07fef-243">Tanılama ayarını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="07fef-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="07fef-244">Bekletme olmadan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="07fef-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="07fef-245">Bekletme olan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="07fef-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="07fef-246">Bekletme belirli günlük kategori için tanılama ayarıyla etkinleştir</span><span class="sxs-lookup"><span data-stu-id="07fef-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="07fef-247">Olay hub'ları için tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="07fef-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="07fef-248">OMS tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="07fef-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```

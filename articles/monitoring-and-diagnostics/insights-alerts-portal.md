---
title: "Azure Hizmetleri için-uyarı oluşturma Azure portalı | Microsoft Docs"
description: "Belirttiğiniz koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="4c7e4-103">Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde oluşturma Azure portalı</span><span class="sxs-lookup"><span data-stu-id="4c7e4-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c7e4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4c7e4-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="4c7e4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c7e4-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="4c7e4-106">CLI</span><span class="sxs-lookup"><span data-stu-id="4c7e4-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="4c7e4-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4c7e4-107">Overview</span></span>
<span data-ttu-id="4c7e4-108">Bu makalede Azure portalını kullanarak Azure ölçüm uyarılarını ayarlama gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="4c7e4-109">İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="4c7e4-110">**Ölçüm değerleri** -herhangi bir yönde atadığınız bir eşik değeri, belirtilen bir ölçüm kestiği olduğunda uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="4c7e4-111">Diğer bir deyişle, her ikisi de tetikler koşul ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="4c7e4-112">**Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="4c7e4-113">Etkinlik günlüğü Uyarıları hakkında daha fazla bilgi edinmek için [burayı tıklatın](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4c7e4-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="4c7e4-114">Tetikler, aşağıdakileri yapmak için bir ölçüm uyarısı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7e4-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="4c7e4-115">Hizmet yöneticisini ve ortak Yöneticiler e-posta bildirimleri gönder</span><span class="sxs-lookup"><span data-stu-id="4c7e4-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="4c7e4-116">Belirttiğiniz ek e-postalar için e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="4c7e4-117">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="4c7e4-117">call a webhook</span></span>
* <span data-ttu-id="4c7e4-118">(yalnızca Azure portalından) Azure bir runbook'un yürütülmesi Başlat</span><span class="sxs-lookup"><span data-stu-id="4c7e4-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="4c7e4-119">Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="4c7e4-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="4c7e4-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c7e4-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="4c7e4-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c7e4-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="4c7e4-122">komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="4c7e4-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="4c7e4-123">Azure monitör REST API'si</span><span class="sxs-lookup"><span data-stu-id="4c7e4-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="4c7e4-124">Azure portal ile bir ölçüm bir uyarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7e4-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="4c7e4-125">İçinde [portal](https://portal.azure.com/), izleme ilgilenen kaynak bulup seçin.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="4c7e4-126">Seçin **uyarıları** veya **uyarı kuralları** izleme bölümünde.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="4c7e4-127">Metin ve simge farklı kaynaklar için biraz değişebilir.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-127">The text and icon may vary slightly for different resources.</span></span>  

    ![İzleme](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="4c7e4-129">Seçin **uyarı Ekle** komut ve alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Uyarı ekleme](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="4c7e4-131">**Ad** , uyarı kuralı ve seçin bir **açıklama**, bildirim e-postalarda da gösterir.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="4c7e4-132">Seçin **ölçüm** izlemek ve ardından istediğiniz bir **koşulu** ve **eşik** ölçüm için değer.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="4c7e4-133">Aynı zamanda seçtiğiniz **süresi** ölçüm kuralı uyarı Tetikleyicileri önce karşılanması gereken süre.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="4c7e4-134">Dolayısıyla örneğin CPU % 80 5 dakika boyunca sürekli olarak yukarıdaki kaldığında "PT5M" dönemi kullanıyorsanız ve Uyarınız % 80 CPU görünüyor, uyarıyı tetikleyen.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="4c7e4-135">İlk tetikleyici oluşur sonra 5 dakika boyunca % 80 CPU kaldığında oluşan yeniden tetikler.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="4c7e4-136">CPU ölçüm, 1 dakikada oluşur.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="4c7e4-137">Denetleme **e-posta sahipleri...**  yöneticileri ve ortak Yöneticiler uyarı oluşturulduğunda e-posta gönderilip istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="4c7e4-138">Uyarı oluşturulduğunda bir bildirim almak için ek e-postaları istiyorsanız, bunları ekleyin **ek yönetici email(s)** alan.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="4c7e4-139">Birden çok e-postaları - noktalı virgülle ayırın  *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="4c7e4-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="4c7e4-140">Geçerli bir URI koymak **Web kancası** adlı uyarı oluşturulduğunda istiyorsanız alan.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="4c7e4-141">Azure Otomasyonu kullanırsanız, uyarı oluşturulduğunda çalıştırılacak bir Runbook seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="4c7e4-142">Seçin **Tamam** uyarı oluşturmak için yapıldığında.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="4c7e4-143">Birkaç dakika içinde uyarı etkindir ve daha önce açıklandığı şekilde tetikler.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="4c7e4-144">Uyarılarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="4c7e4-144">Managing your alerts</span></span>
<span data-ttu-id="4c7e4-145">Bir uyarı oluşturduktan sonra bunu seçebilirsiniz ve:</span><span class="sxs-lookup"><span data-stu-id="4c7e4-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="4c7e4-146">Ölçüm eşiği ve önceki gün gerçek değerleri gösteren bir grafik görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="4c7e4-147">Düzenleyin veya silin.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-147">Edit or delete it.</span></span>
* <span data-ttu-id="4c7e4-148">**Devre dışı** veya **etkinleştirmek** , geçici olarak durdurmak veya bu uyarı için bildirimleri almaya devam etmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c7e4-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c7e4-149">Next steps</span></span>
* <span data-ttu-id="4c7e4-150">[Azure izleme genel bir bakış elde](monitoring-overview.md) toplamak ve izlemek bilgi türlerini de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="4c7e4-151">Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4c7e4-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="4c7e4-152">Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4c7e4-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="4c7e4-153">Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4c7e4-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="4c7e4-154">Alma bir [tanılama günlükleri'ne genel bakış](monitoring-overview-of-diagnostic-logs.md) hizmetinizde ayrıntılı yüksek sıklıkta ölçümleri toplamak ve.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="4c7e4-155">Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="4c7e4-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>

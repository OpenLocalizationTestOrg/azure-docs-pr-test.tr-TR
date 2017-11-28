---
title: "Azure Hizmetleri - aaaCreate uyarıları Azure portalı | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="7fb52-103">Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde oluşturma Azure portalı</span><span class="sxs-lookup"><span data-stu-id="7fb52-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fb52-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7fb52-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="7fb52-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb52-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="7fb52-106">CLI</span><span class="sxs-lookup"><span data-stu-id="7fb52-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="7fb52-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7fb52-107">Overview</span></span>
<span data-ttu-id="7fb52-108">Bu makalede Azure portal kullanarak Azure ölçüm uyarıları tooset hello nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7fb52-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="7fb52-109">İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb52-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="7fb52-110">**Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="7fb52-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="7fb52-111">Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.</span><span class="sxs-lookup"><span data-stu-id="7fb52-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="7fb52-112">**Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur.</span><span class="sxs-lookup"><span data-stu-id="7fb52-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="7fb52-113">Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7fb52-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="7fb52-114">Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7fb52-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="7fb52-115">e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder</span><span class="sxs-lookup"><span data-stu-id="7fb52-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="7fb52-116">e-posta, belirttiğiniz tooadditional e-postalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="7fb52-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="7fb52-117">bir Web kancası çağırın</span><span class="sxs-lookup"><span data-stu-id="7fb52-117">call a webhook</span></span>
* <span data-ttu-id="7fb52-118">bir Azure runbook'tan (yalnızca Azure portal hello) yürütülmesini Başlat</span><span class="sxs-lookup"><span data-stu-id="7fb52-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="7fb52-119">Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="7fb52-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="7fb52-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7fb52-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="7fb52-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb52-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="7fb52-122">komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="7fb52-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="7fb52-123">Azure monitör REST API'si</span><span class="sxs-lookup"><span data-stu-id="7fb52-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="7fb52-124">Ölçüm hello Azure portal ile bir uyarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fb52-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="7fb52-125">Merhaba, [portal](https://portal.azure.com/), izleme ilgilenen hello kaynak bulup seçin.</span><span class="sxs-lookup"><span data-stu-id="7fb52-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="7fb52-126">Seçin **uyarıları** veya **uyarı kuralları** hello izleme bölümü altında.</span><span class="sxs-lookup"><span data-stu-id="7fb52-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="7fb52-127">Merhaba metin ve simge farklı kaynaklar için biraz değişebilir.</span><span class="sxs-lookup"><span data-stu-id="7fb52-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![İzleme](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="7fb52-129">Select hello **uyarı Ekle** komut ve hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="7fb52-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Uyarı ekleme](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="7fb52-131">**Ad** , uyarı kuralı ve seçin bir **açıklama**, bildirim e-postalarda da gösterir.</span><span class="sxs-lookup"><span data-stu-id="7fb52-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="7fb52-132">Select hello **ölçüm** toomonitor istediğiniz sonra seçin bir **koşulu** ve **eşik** hello ölçüm için değer.</span><span class="sxs-lookup"><span data-stu-id="7fb52-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="7fb52-133">Ayrıca hello Seçtiğiniz **süresi** ölçüm hello süresini kural hello uyarı Tetikleyicileri önce yerine getirilmesi gereken.</span><span class="sxs-lookup"><span data-stu-id="7fb52-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="7fb52-134">Dolayısıyla örneğin Hello CPU % 80 5 dakika boyunca sürekli olarak yukarıdaki kaldığında hello süresi "PT5M" kullanıyorsanız ve uyarıyı % 80 CPU arar hello uyarı tetikler.</span><span class="sxs-lookup"><span data-stu-id="7fb52-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="7fb52-135">Merhaba ilk tetikleyici oluşur sonra hello CPU 5 dakika boyunca % 80'altında kaldığında oluşan yeniden tetikler.</span><span class="sxs-lookup"><span data-stu-id="7fb52-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="7fb52-136">Merhaba CPU ölçüm, 1 dakikada oluşur.</span><span class="sxs-lookup"><span data-stu-id="7fb52-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="7fb52-137">Denetleme **e-posta sahipleri... ** e-posta ile yöneticileri ve ortak Yöneticiler toobe istiyorsanız, ne zaman uyarı ateşlenir hello.</span><span class="sxs-lookup"><span data-stu-id="7fb52-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="7fb52-138">Ek e-postaları tooreceive hello olduğunda bir bildirim istiyorsanız uyarı ateşlenir, hello eklemek **ek yönetici email(s)** alan.</span><span class="sxs-lookup"><span data-stu-id="7fb52-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="7fb52-139">Birden çok e-postaları - noktalı virgülle ayırın * email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="7fb52-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="7fb52-140">Merhaba geçerli bir URI koymak **Web kancası** alan adlı istiyorsanız, ne zaman hello uyarı etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="7fb52-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="7fb52-141">Azure Otomasyonu kullanırsanız, hello uyarı oluşturulduğunda çalıştırmak bir Runbook toobe seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb52-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="7fb52-142">Seçin **Tamam** zaman Bitti'yi toocreate hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="7fb52-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="7fb52-143">Birkaç dakika içinde hello uyarı etkin ve daha önce açıklandığı şekilde tetikler.</span><span class="sxs-lookup"><span data-stu-id="7fb52-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="7fb52-144">Uyarılarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="7fb52-144">Managing your alerts</span></span>
<span data-ttu-id="7fb52-145">Bir uyarı oluşturduktan sonra bunu seçebilirsiniz ve:</span><span class="sxs-lookup"><span data-stu-id="7fb52-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="7fb52-146">Önceki gün Hello ölçüm eşiği ve hello hello gerçek değerleri gösteren bir grafik görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7fb52-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="7fb52-147">Düzenleyin veya silin.</span><span class="sxs-lookup"><span data-stu-id="7fb52-147">Edit or delete it.</span></span>
* <span data-ttu-id="7fb52-148">**Devre dışı** veya **etkinleştirmek** onu, tootemporarily durdurma veya bu uyarı için bildirimleri almaya devam etmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="7fb52-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fb52-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7fb52-149">Next steps</span></span>
* <span data-ttu-id="7fb52-150">[Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="7fb52-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="7fb52-151">Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7fb52-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="7fb52-152">Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7fb52-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="7fb52-153">Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7fb52-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="7fb52-154">Alma bir [tanılama günlükleri'ne genel bakış](monitoring-overview-of-diagnostic-logs.md) hizmetinizde ayrıntılı yüksek sıklıkta ölçümleri toplamak ve.</span><span class="sxs-lookup"><span data-stu-id="7fb52-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="7fb52-155">Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="7fb52-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>

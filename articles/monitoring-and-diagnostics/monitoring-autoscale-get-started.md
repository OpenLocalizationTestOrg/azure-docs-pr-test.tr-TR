---
title: "Otomatik ölçeklendirme Azure kullanmaya başlama | Microsoft Docs"
description: "Azure'da kaynağınız ölçeklendirmek öğrenin."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="04052-103">Otomatik ölçeklendirme Azure kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="04052-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="04052-104">Bu makalede, Microsoft Azure Portalı'nda, kaynak için otomatik ölçeklendirme ayarlarınızı ayarlama açıklar.</span><span class="sxs-lookup"><span data-stu-id="04052-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="04052-105">Azure İzleyici otomatik ölçeklendirme, yalnızca sanal makine ölçek kümeleri, bulut Hizmetleri, Azure uygulama hizmeti planları ve uygulama hizmeti ortamları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="04052-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="04052-106">Otomatik ölçeklendirme ayarlarını aboneliğinizde Bul</span><span class="sxs-lookup"><span data-stu-id="04052-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="04052-107">Otomatik ölçeklendirme Azure İzleyicisi'nde geçerli olduğu tüm kaynakları bulabilir.</span><span class="sxs-lookup"><span data-stu-id="04052-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="04052-108">Adım adım kılavuz için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="04052-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="04052-109">Açık [Azure portalı.][1]</span><span class="sxs-lookup"><span data-stu-id="04052-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="04052-110">Sol bölmede Azure İzleyici simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04052-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="04052-111">![Açık Azure İzleyicisi][2]</span><span class="sxs-lookup"><span data-stu-id="04052-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="04052-112">Tıklatın **otomatik ölçeklendirme** otomatik ölçeklendirme olduğu geçerli otomatik ölçeklendirme durumlarıyla birlikte uygulanabilir tüm kaynakları görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="04052-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="04052-113">![Otomatik ölçeklendirme Azure İzleyicisi'nde Bul][3]</span><span class="sxs-lookup"><span data-stu-id="04052-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="04052-114">Belirli bir kaynak grubunun, belirli kaynak türlerine veya belirli bir kaynak kaynakları seçmek için üst kapsam listede aşağı Filtre bölmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="04052-115">Her bir kaynağın geçerli örnek sayısına ve otomatik ölçeklendirme durum bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="04052-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="04052-116">Otomatik ölçeklendirme Durum aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="04052-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="04052-117">**Yapılandırılmamış**: otomatik ölçeklendirme henüz bu kaynak için etkinleştirdiğiniz değil.</span><span class="sxs-lookup"><span data-stu-id="04052-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="04052-118">**Etkin**: Bu kaynak için otomatik ölçeklendirme etkin.</span><span class="sxs-lookup"><span data-stu-id="04052-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="04052-119">**Devre dışı**: Bu kaynak için otomatik ölçeklendirme devre dışı bırakmış.</span><span class="sxs-lookup"><span data-stu-id="04052-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="04052-120">İlk otomatik ölçeklendirme ayarı oluşturun</span><span class="sxs-lookup"><span data-stu-id="04052-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="04052-121">Şimdi, ilk otomatik ölçeklendirme ayarı oluşturmak için bir basit adım adım kılavuz şimdi gidin.</span><span class="sxs-lookup"><span data-stu-id="04052-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="04052-122">Açık **otomatik ölçeklendirme** dikey penceresinde Azure izlemek ve ölçeklendirmek istediğiniz bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="04052-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="04052-123">(Bir web uygulaması ile ilişkili bir uygulama hizmeti planı aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="04052-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="04052-124">Yapabilecekleriniz [ilk ASP.NET web uygulamanızı 5 dakika içinde oluşturma.] [4])</span><span class="sxs-lookup"><span data-stu-id="04052-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="04052-125">Geçerli örnek sayısı 1 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04052-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="04052-126">Tıklatın **etkinleştirmek otomatik ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="04052-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="04052-127">![Yeni web uygulaması için ölçek ayarı][5]</span><span class="sxs-lookup"><span data-stu-id="04052-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="04052-128">Ölçek ayarı için bir ad sağlayın ve ardından **bir kural eklemek**.</span><span class="sxs-lookup"><span data-stu-id="04052-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="04052-129">İçerik bölmesinde sağ tarafında olarak açın ölçek kuralı seçeneklerini dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="04052-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="04052-130">Varsayılan olarak, bu kaynak CPU yüzdesi yüzde 70 aşarsa, örnek sayınız 1 ile ölçeklendirme seçeneği ayarlar.</span><span class="sxs-lookup"><span data-stu-id="04052-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="04052-131">Kendi varsayılan değerlerinde bırakın ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="04052-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="04052-132">![Bir web uygulaması için ölçek ayar oluşturun][6]</span><span class="sxs-lookup"><span data-stu-id="04052-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="04052-133">İlk ölçek kuralı şimdi oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="04052-133">You've now created your first scale rule.</span></span> <span data-ttu-id="04052-134">Not UX en iyi yöntemler önerir ve "En az bir ölçek kuralı için önerilir olduğunu." durumları</span><span class="sxs-lookup"><span data-stu-id="04052-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="04052-135">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="04052-135">To do so:</span></span>
  
    <span data-ttu-id="04052-136">a.</span><span class="sxs-lookup"><span data-stu-id="04052-136">a.</span></span> <span data-ttu-id="04052-137">Tıklatın **bir kural eklemek**.</span><span class="sxs-lookup"><span data-stu-id="04052-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="04052-138">b.</span><span class="sxs-lookup"><span data-stu-id="04052-138">b.</span></span> <span data-ttu-id="04052-139">Ayarlama **işleci** için **değerinden**.</span><span class="sxs-lookup"><span data-stu-id="04052-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="04052-140">c.</span><span class="sxs-lookup"><span data-stu-id="04052-140">c.</span></span> <span data-ttu-id="04052-141">Ayarlama **eşik** için **20**.</span><span class="sxs-lookup"><span data-stu-id="04052-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="04052-142">d.</span><span class="sxs-lookup"><span data-stu-id="04052-142">d.</span></span> <span data-ttu-id="04052-143">Ayarlama **işlemi** için **azaltmak sayısına göre**.</span><span class="sxs-lookup"><span data-stu-id="04052-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="04052-144">Ölçek ayarını şimdi olmalıdır ölçek genişletme/ölçekler olduğunu içinde tabanlı CPU kullanımı.</span><span class="sxs-lookup"><span data-stu-id="04052-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="04052-145">![CPU üzerinde göre ölçeklendirin][8]</span><span class="sxs-lookup"><span data-stu-id="04052-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="04052-146">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04052-146">Click **Save**.</span></span>

<span data-ttu-id="04052-147">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="04052-147">Congratulations!</span></span> <span data-ttu-id="04052-148">İlk ölçek ayarınız web uygulamanızı CPU kullanım amaçlarına göre otomatik ölçeklendirme artık başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="04052-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="04052-149">Aynı adımlar bir sanal makine ölçek kümesi ile çalışmaya başlama veya Bulut hizmet rolü için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="04052-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="04052-150">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="04052-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="04052-151">Bir zamanlamaya göre ölçeği</span><span class="sxs-lookup"><span data-stu-id="04052-151">Scale based on a schedule</span></span>
<span data-ttu-id="04052-152">CPU üzerinde göre ölçeklendirin yanı sıra, Ölçek farklı için haftanın belirli günleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="04052-153">Tıklatın **ölçek koşul Ekle**.</span><span class="sxs-lookup"><span data-stu-id="04052-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="04052-154">Ölçek modu ve kuralları ayarlama varsayılan koşulu ile aynı olur.</span><span class="sxs-lookup"><span data-stu-id="04052-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="04052-155">Seçin **yineleyin belirli günleri** zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="04052-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="04052-156">Gün ve ölçek koşul ne zaman uygulanacağını için başlangıç/bitiş saati seçin.</span><span class="sxs-lookup"><span data-stu-id="04052-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Zamanlamaya göre ölçeği koşulu][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="04052-158">Farklı belirli tarihleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="04052-158">Scale differently on specific dates</span></span>
<span data-ttu-id="04052-159">CPU üzerinde göre ölçeklendirin yanı sıra, Ölçek farklı belirli tarihler için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="04052-160">Tıklatın **ölçek koşul Ekle**.</span><span class="sxs-lookup"><span data-stu-id="04052-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="04052-161">Ölçek modu ve kuralları ayarlama varsayılan koşulu ile aynı olur.</span><span class="sxs-lookup"><span data-stu-id="04052-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="04052-162">Seçin **belirt başlangıç/bitiş tarihlerini** zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="04052-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="04052-163">Başlangıç/bitiş tarihleri ve ölçek koşul ne zaman uygulanacağını için başlangıç/bitiş saati seçin.</span><span class="sxs-lookup"><span data-stu-id="04052-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Tarihleri temel alınarak ölçek koşulu][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="04052-165">Kaynağınız ölçek geçmişini görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="04052-165">View the scale history of your resource</span></span>
<span data-ttu-id="04052-166">Kaynağınız yukarı veya aşağı ölçeklendirilir her etkinlik günlüğünde bir olay kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="04052-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="04052-167">Geçerek son 24 saat için kaynağınız ölçek geçmişini görüntüleyebilirsiniz **çalıştırma geçmişi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="04052-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![çalıştırma geçmişi][11]

<span data-ttu-id="04052-169">(En fazla 90 gün için) tam ölçek geçmişini görüntülemek isteyip istemediğinizi seçin **daha fazla ayrıntı görmek için burayı tıklatın**.</span><span class="sxs-lookup"><span data-stu-id="04052-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="04052-170">Etkinlik günlüğü kaynak ve kategori için önceden seçilmiş otomatik ölçeklendirme ile açılır.</span><span class="sxs-lookup"><span data-stu-id="04052-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="04052-171">Kaynağınız ölçek tanımını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="04052-171">View the scale definition of your resource</span></span>
<span data-ttu-id="04052-172">Otomatik ölçeklendirme bir Azure Resource Manager kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="04052-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="04052-173">Ölçek tanımı JSON'de geçerek görüntüleyebileceğiniz **JSON** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="04052-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Ölçek tanımı][12]

<span data-ttu-id="04052-175">JSON'da doğrudan gerekirse değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="04052-176">Bunları kaydettikten sonra bu değişiklikleri yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="04052-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="04052-177">Otomatik ölçeklendirme devre dışı bırakın ve el ile örneklerinizi ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="04052-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="04052-178">Geçerli ölçek ayarını devre dışı bırakın ve el ile kaynağınız ölçeklendirmek istediğiniz zaman zamanlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="04052-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="04052-179">Tıklatın **otomatik ölçeklendirme devre dışı bırakma** üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="04052-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="04052-180">![Otomatik ölçeklendirme devre dışı bırak][13]</span><span class="sxs-lookup"><span data-stu-id="04052-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="04052-181">Bu seçenek yapılandırmanızı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="04052-181">This option disables your configuration.</span></span> <span data-ttu-id="04052-182">Otomatik ölçeklendirme yeniden etkinleştirildikten sonra ancak, geri için edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="04052-183">Şimdi, el ile ölçeklendirmek istediğiniz örneklerinin sayısını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04052-183">You can now set the number of instances that you want to scale to manually.</span></span>

![El ile ölçek kümesi][14]

<span data-ttu-id="04052-185">Tıklatarak her zaman için otomatik ölçeklendirme dönebilirsiniz **etkinleştirmek otomatik ölçeklendirme** ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="04052-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04052-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04052-186">Next steps</span></span>
- [<span data-ttu-id="04052-187">Bir etkinlik günlüğü aboneliğinizi tüm otomatik ölçeklendirme motoru işlemleri izlemek için uyarı oluştur</span><span class="sxs-lookup"><span data-stu-id="04052-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="04052-188">Bir etkinlik günlüğü aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemleri izlemek için uyarı oluştur</span><span class="sxs-lookup"><span data-stu-id="04052-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png


---
title: "otomatik ölçeklendirme Azure aaaGet Başlarken | Microsoft Docs"
description: "Bilgi nasıl tooscale kaynağınız azure'da."
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
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="548c3-103">Otomatik ölçeklendirme Azure kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="548c3-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="548c3-104">Bu makalede nasıl hello Microsoft Azure Portalı'nda, kaynak için otomatik ölçeklendirme ayarlarını tooset.</span><span class="sxs-lookup"><span data-stu-id="548c3-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="548c3-105">Azure İzleyici otomatik ölçeklendirme yalnızca toovirtual makine ölçekleme kümeleri, bulut Hizmetleri, Azure uygulama hizmeti planları ve uygulama hizmeti ortamları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="548c3-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="548c3-106">Merhaba otomatik ölçeklendirme ayarlarını aboneliğinizde Bul</span><span class="sxs-lookup"><span data-stu-id="548c3-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="548c3-107">Otomatik ölçeklendirme Azure İzleyicisi'nde geçerli olduğu tüm hello kaynakları bulabilir.</span><span class="sxs-lookup"><span data-stu-id="548c3-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="548c3-108">Aşağıdaki adımları adım adım kılavuz hello kullan:</span><span class="sxs-lookup"><span data-stu-id="548c3-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="548c3-109">Açık hello [Azure portalı.][1]</span><span class="sxs-lookup"><span data-stu-id="548c3-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="548c3-110">Merhaba sol bölmede Hello Azure İzleyici simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="548c3-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="548c3-111">![Açık Azure İzleyicisi][2]</span><span class="sxs-lookup"><span data-stu-id="548c3-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="548c3-112">Tıklatın **otomatik ölçeklendirme** tooview hangi otomatik ölçeklendirme için tüm hello kaynakları geçerli otomatik ölçeklendirme durumlarıyla birlikte uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="548c3-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="548c3-113">![Otomatik ölçeklendirme Azure İzleyicisi'nde Bul][3]</span><span class="sxs-lookup"><span data-stu-id="548c3-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="548c3-114">Belirli bir kaynak grubunun, belirli kaynak türlerine veya belirli bir kaynak hello listesi tooselect kaynakları aşağı hello üst tooscope adresindeki hello Filtre bölmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="548c3-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="548c3-115">Her bir kaynağın hello geçerli örnek sayısına ve hello otomatik ölçeklendirme durum bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="548c3-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="548c3-116">Merhaba otomatik ölçeklendirme Durum aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="548c3-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="548c3-117">**Yapılandırılmamış**: otomatik ölçeklendirme henüz bu kaynak için etkinleştirdiğiniz değil.</span><span class="sxs-lookup"><span data-stu-id="548c3-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="548c3-118">**Etkin**: Bu kaynak için otomatik ölçeklendirme etkin.</span><span class="sxs-lookup"><span data-stu-id="548c3-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="548c3-119">**Devre dışı**: Bu kaynak için otomatik ölçeklendirme devre dışı bırakmış.</span><span class="sxs-lookup"><span data-stu-id="548c3-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="548c3-120">İlk otomatik ölçeklendirme ayarı oluşturun</span><span class="sxs-lookup"><span data-stu-id="548c3-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="548c3-121">Şimdi şimdi basit adım adım toocreate ilk otomatik ölçeklendirme ayarına gidin.</span><span class="sxs-lookup"><span data-stu-id="548c3-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="548c3-122">Açık hello **otomatik ölçeklendirme** dikey Azure İzleyici ve tooscale istediğiniz bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="548c3-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="548c3-123">(Merhaba aşağıdaki adımlar bir web uygulaması ile ilişkili bir uygulama hizmeti planı kullanın.</span><span class="sxs-lookup"><span data-stu-id="548c3-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="548c3-124">Yapabilecekleriniz [ilk ASP.NET web uygulamanızı 5 dakika içinde oluşturma.] [4])</span><span class="sxs-lookup"><span data-stu-id="548c3-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="548c3-125">Merhaba geçerli örnek sayısı 1 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="548c3-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="548c3-126">Tıklatın **etkinleştirmek otomatik ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="548c3-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="548c3-127">![Yeni web uygulaması için ölçek ayarı][5]</span><span class="sxs-lookup"><span data-stu-id="548c3-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="548c3-128">Merhaba ölçeği ayarlamak için bir ad sağlayın ve ardından **bir kural eklemek**.</span><span class="sxs-lookup"><span data-stu-id="548c3-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="548c3-129">İçerik bölmesinde hello sağ tarafında olarak açın hello ölçek kuralı seçeneklerini dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="548c3-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="548c3-130">Varsayılan olarak, bu hello seçeneği tooscale örneğinizi sayısı 1 ile yüzde 70'hello hello kaynak CPU yüzdesini aşarsa, ayarlar.</span><span class="sxs-lookup"><span data-stu-id="548c3-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="548c3-131">Kendi varsayılan değerlerinde bırakın ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="548c3-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="548c3-132">![Bir web uygulaması için ölçek ayar oluşturun][6]</span><span class="sxs-lookup"><span data-stu-id="548c3-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="548c3-133">İlk ölçek kuralı şimdi oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="548c3-133">You've now created your first scale rule.</span></span> <span data-ttu-id="548c3-134">UX önerir en iyi yöntemler ve bildiren bu hello unutmayın "toohave önerilen en az bir ölçek kuralında."</span><span class="sxs-lookup"><span data-stu-id="548c3-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="548c3-135">toodo için:</span><span class="sxs-lookup"><span data-stu-id="548c3-135">toodo so:</span></span>
  
    <span data-ttu-id="548c3-136">a.</span><span class="sxs-lookup"><span data-stu-id="548c3-136">a.</span></span> <span data-ttu-id="548c3-137">Tıklatın **bir kural eklemek**.</span><span class="sxs-lookup"><span data-stu-id="548c3-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="548c3-138">b.</span><span class="sxs-lookup"><span data-stu-id="548c3-138">b.</span></span> <span data-ttu-id="548c3-139">Ayarlama **işleci** çok**değerinden**.</span><span class="sxs-lookup"><span data-stu-id="548c3-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="548c3-140">c.</span><span class="sxs-lookup"><span data-stu-id="548c3-140">c.</span></span> <span data-ttu-id="548c3-141">Ayarlama **eşik** çok**20**.</span><span class="sxs-lookup"><span data-stu-id="548c3-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="548c3-142">d.</span><span class="sxs-lookup"><span data-stu-id="548c3-142">d.</span></span> <span data-ttu-id="548c3-143">Ayarlama **işlemi** çok**azaltmak sayısına göre**.</span><span class="sxs-lookup"><span data-stu-id="548c3-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="548c3-144">Ölçek ayarını şimdi olmalıdır ölçek genişletme/ölçekler olduğunu içinde tabanlı CPU kullanımı.</span><span class="sxs-lookup"><span data-stu-id="548c3-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="548c3-145">![CPU üzerinde göre ölçeklendirin][8]</span><span class="sxs-lookup"><span data-stu-id="548c3-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="548c3-146">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="548c3-146">Click **Save**.</span></span>

<span data-ttu-id="548c3-147">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="548c3-147">Congratulations!</span></span> <span data-ttu-id="548c3-148">Web uygulamanızı CPU kullanımı dikkate alarak, ilk ölçek ayarı tooautoscale şimdi başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="548c3-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="548c3-149">Merhaba adımlarıyla aynıdır ile bir sanal makine ölçek kullanmaya uygun tooget kümesi veya Bulut hizmet rolü.</span><span class="sxs-lookup"><span data-stu-id="548c3-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="548c3-150">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="548c3-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="548c3-151">Bir zamanlamaya göre ölçeği</span><span class="sxs-lookup"><span data-stu-id="548c3-151">Scale based on a schedule</span></span>
<span data-ttu-id="548c3-152">Ayrıca CPU üzerinde temel tooscale, Ölçek farklı hello haftanın belirli günleri için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="548c3-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="548c3-153">Tıklatın **ölçek koşul Ekle**.</span><span class="sxs-lookup"><span data-stu-id="548c3-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="548c3-154">Merhaba ölçek modu ve hello kurallarının ayarlanması olduğu hello aynı hello varsayılan koşulu olarak.</span><span class="sxs-lookup"><span data-stu-id="548c3-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="548c3-155">Seçin **yineleyin belirli günleri** hello zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="548c3-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="548c3-156">Merhaba gün ve hello ölçek koşul ne zaman uygulanacağını için hello başlangıç/bitiş saati seçin.</span><span class="sxs-lookup"><span data-stu-id="548c3-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Zamanlamaya göre ölçeği koşulu][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="548c3-158">Farklı belirli tarihleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="548c3-158">Scale differently on specific dates</span></span>
<span data-ttu-id="548c3-159">Ayrıca CPU üzerinde temel tooscale, Ölçek farklı belirli tarihler için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="548c3-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="548c3-160">Tıklatın **ölçek koşul Ekle**.</span><span class="sxs-lookup"><span data-stu-id="548c3-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="548c3-161">Merhaba ölçek modu ve hello kurallarının ayarlanması olduğu hello aynı hello varsayılan koşulu olarak.</span><span class="sxs-lookup"><span data-stu-id="548c3-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="548c3-162">Seçin **belirt başlangıç/bitiş tarihlerini** hello zamanlama için.</span><span class="sxs-lookup"><span data-stu-id="548c3-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="548c3-163">Merhaba başlangıç/bitiş tarihleri ve hello ölçek koşul ne zaman uygulanacağını için hello başlangıç/bitiş saati seçin.</span><span class="sxs-lookup"><span data-stu-id="548c3-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Tarihleri temel alınarak ölçek koşulu][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="548c3-165">Kaynağınız hello ölçek geçmişini görüntüle</span><span class="sxs-lookup"><span data-stu-id="548c3-165">View hello scale history of your resource</span></span>
<span data-ttu-id="548c3-166">Kaynağınız yukarı veya aşağı ölçeklendirilir her bir olay hello etkinlik günlüğüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="548c3-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="548c3-167">Toohello geçerek son 24 saat hello kaynak hello ölçek geçmişini görüntüleyebilirsiniz **çalıştırma geçmişi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="548c3-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![çalıştırma geçmişi][11]

<span data-ttu-id="548c3-169">Tooview hello tam ölçek geçmişi istiyorsanız (için yukarı too90 gün), select **toosee daha fazla ayrıntı burayı**.</span><span class="sxs-lookup"><span data-stu-id="548c3-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="548c3-170">Hello etkinlik günlüğünde, kaynak ve kategori için önceden seçilmiş otomatik ölçeklendirme ile açılır.</span><span class="sxs-lookup"><span data-stu-id="548c3-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="548c3-171">Merhaba ölçek, kaynak tanımını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="548c3-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="548c3-172">Otomatik ölçeklendirme bir Azure Resource Manager kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="548c3-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="548c3-173">Merhaba ölçek tanımı JSON'de toohello geçerek görüntüleyebileceğiniz **JSON** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="548c3-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Ölçek tanımı][12]

<span data-ttu-id="548c3-175">JSON'da doğrudan gerekirse değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="548c3-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="548c3-176">Bunları kaydettikten sonra bu değişiklikleri yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="548c3-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="548c3-177">Otomatik ölçeklendirme devre dışı bırakın ve el ile örneklerinizi ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="548c3-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="548c3-178">Ne zaman toodisable geçerli ölçek ayarınız isterseniz ve elle kaynağınız ölçeklendirme kez olabilir.</span><span class="sxs-lookup"><span data-stu-id="548c3-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="548c3-179">Merhaba tıklatın **otomatik ölçeklendirme devre dışı bırakma** hello üst düğmesini.</span><span class="sxs-lookup"><span data-stu-id="548c3-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="548c3-180">![Otomatik ölçeklendirme devre dışı bırak][13]</span><span class="sxs-lookup"><span data-stu-id="548c3-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="548c3-181">Bu seçenek yapılandırmanızı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="548c3-181">This option disables your configuration.</span></span> <span data-ttu-id="548c3-182">Ancak, otomatik ölçeklendirme yeniden etkinleştirildikten sonra tooit geri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="548c3-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="548c3-183">Şimdi hello tooscale toomanually istediğiniz örneklerinin sayısını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="548c3-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![El ile ölçek kümesi][14]

<span data-ttu-id="548c3-185">Tıklatarak tooAutoscale her zaman dönebilirsiniz **etkinleştirmek otomatik ölçeklendirme** ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="548c3-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="548c3-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="548c3-186">Next steps</span></span>
- [<span data-ttu-id="548c3-187">Bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturma</span><span class="sxs-lookup"><span data-stu-id="548c3-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="548c3-188">Bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="548c3-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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


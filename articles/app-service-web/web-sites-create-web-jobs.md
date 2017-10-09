---
title: "Web işleri ile aaaRun arka plan görevleri"
description: "Azure'da toorun arka plan görevleri uygulamaları nasıl web öğrenin."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="d82e7-103">WebJobs ile arka plan görevleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d82e7-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="d82e7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d82e7-104">Overview</span></span>
<span data-ttu-id="d82e7-105">İçinde Web işleri, programları veya komut dosyaları çalıştırabilirsiniz, [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web uygulaması üç yolla: isteğe bağlı olarak, sürekli olarak veya bir zamanlamaya göre.</span><span class="sxs-lookup"><span data-stu-id="d82e7-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="d82e7-106">Hiçbir ek maliyet toouse WebJobs yoktur.</span><span class="sxs-lookup"><span data-stu-id="d82e7-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="d82e7-107">Bu makalede nasıl kullanarak Web işleri toodeploy hello gösterilmektedir [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d82e7-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="d82e7-108">Hakkında bilgi için Visual Studio veya sürekli teslim işlemini kullanarak toodeploy bkz [nasıl tooDeploy Azure Web işleri tooWeb uygulamaları](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="d82e7-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="d82e7-109">Hello Azure WebJobs SDK, birçok WebJobs programlama görevini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="d82e7-110">Daha fazla bilgi için bkz: [hello WebJobs SDK nedir](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d82e7-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="d82e7-111">Azure işlevleri, başka bir şekilde toorun programları ve betikleri bir sunucusuz ortamından veya bir uygulama hizmeti uygulamadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="d82e7-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="d82e7-112">Daha fazla bilgi için bkz: [Azure işlevlerine genel bakış](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d82e7-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="d82e7-113"><a name="acceptablefiles"></a>Komut dosyaları veya programlar için kabul edilebilir dosya türleri</span><span class="sxs-lookup"><span data-stu-id="d82e7-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="d82e7-114">Şu dosya türlerini hello kabul edilir:</span><span class="sxs-lookup"><span data-stu-id="d82e7-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="d82e7-115">.cmd, .bat, .exe (windows cmd kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="d82e7-116">.ps1 (powershell kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="d82e7-117">.sh (bash kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-117">.sh (using bash)</span></span>
* <span data-ttu-id="d82e7-118">.php (php kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-118">.php (using php)</span></span>
* <span data-ttu-id="d82e7-119">.py (python kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-119">.py (using python)</span></span>
* <span data-ttu-id="d82e7-120">.js (düğümünü kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-120">.js (using node)</span></span>
* <span data-ttu-id="d82e7-121">.jar (java kullanarak)</span><span class="sxs-lookup"><span data-stu-id="d82e7-121">.jar (using java)</span></span>

## <span data-ttu-id="d82e7-122"><a name="CreateOnDemand"></a>Merhaba Portalı'nda bir üzerinde isteğe bağlı WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="d82e7-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="d82e7-123">Merhaba, **Web uygulaması** hello dikey [Azure Portal](https://portal.azure.com), tıklatın **tüm ayarları > Web işleri** tooshow hello **WebJobs** dikey.</span><span class="sxs-lookup"><span data-stu-id="d82e7-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Web işi dikey penceresi](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="d82e7-125">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-125">Click **Add**.</span></span> <span data-ttu-id="d82e7-126">Merhaba **WebJob Ekle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Web işi dikey ekleme](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="d82e7-128">Altında **adı**, hello Web işi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="d82e7-129">Merhaba ad bir harf veya sayı ile başlamalı ve özel karakterler içeremez "-" ve "_".</span><span class="sxs-lookup"><span data-stu-id="d82e7-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="d82e7-130">Merhaba, **nasıl tooRun** kutusunda, seçin **isteğe bağlı olarak**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="d82e7-131">Merhaba, **dosyayı karşıya yüklemeyi** kutusuna hello klasör simgesine tıklayın ve komut dosyanızı içeren toohello zip dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="d82e7-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="d82e7-132">Merhaba zip dosyası yürütülebilir dosyanın (.exe .cmd .bat .sh .php .py .js) toorun program veya komut dosyası hello yanı sıra tüm destekleyici dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="d82e7-133">Denetleme **oluşturma** tooupload hello betik tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d82e7-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="d82e7-134">Hello hello Web işi için belirtilen ad hello hello listede görünür **WebJobs** dikey.</span><span class="sxs-lookup"><span data-stu-id="d82e7-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="d82e7-135">toorun hello Web işi, hello listesi ve tıklatın adına sağ tıklayın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Web işini çalıştırma](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="d82e7-137"><a name="CreateContinuous"></a>Sürekli olarak çalışan bir WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="d82e7-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="d82e7-138">toocreate sürekli olarak çalışan bir WebJob izleyin aynı adımlar için bir WebJob oluşturma bir kez çalışır, ancak hello hello **nasıl tooRun** kutusunda, seçin **sürekli**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="d82e7-139">toostart veya Dur bir sürekli Webjob'un sağ hello WebJob hello listesi ve tıklatın **Başlat** veya **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="d82e7-140">Web uygulamanız birden çok örneğinde çalışıyorsa, sürekli olarak çalışan bir WebJob tüm örneklerinizi çalışır.</span><span class="sxs-lookup"><span data-stu-id="d82e7-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="d82e7-141">Yük Dengeleme Microsoft Azure tarafından seçilen tek bir örneğinde isteğe bağlı ve zamanlanmış Web işleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="d82e7-142">İçin sürekli Webjob'lar toorun güvenilir bir şekilde ve tüm örneklerini etkinleştirin her zaman açık hello * yapılandırma ayarı durabilirsiniz hello SCM ana site uzun süre boşta zaman çalıştıran hello web uygulaması için Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="d82e7-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="d82e7-143"><a name="CreateScheduledCRON"></a>CRON ifade kullanılarak zamanlanmış bir WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="d82e7-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="d82e7-144">Bu teknik kullanılabilir tooWeb uygulamaları temel, standart veya Premium modunda çalışıyor ve hello **her zaman açık** hello uygulamasını etkin toobe ayarlama.</span><span class="sxs-lookup"><span data-stu-id="d82e7-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="d82e7-145">yalnızca tooturn bir üzerinde isteğe bağlı WebJob zamanlanmış Web işi içine dahil bir `settings.job` hello kökündeki WebJob ZIP dosyasının dosya.</span><span class="sxs-lookup"><span data-stu-id="d82e7-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="d82e7-146">Bu JSON dosyası içermelidir bir `schedule` özelliği ile bir [CRON ifade](https://en.wikipedia.org/wiki/Cron), aşağıdaki örnek başına.</span><span class="sxs-lookup"><span data-stu-id="d82e7-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="d82e7-147">Merhaba CRON ifade 6 alanlarının oluşur: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="d82e7-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="d82e7-148">Örneğin, tootrigger, WebJob her 15 dakikada, `settings.job` gerekir:</span><span class="sxs-lookup"><span data-stu-id="d82e7-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="d82e7-149">Diğer CRON zamanlama örnekler:</span><span class="sxs-lookup"><span data-stu-id="d82e7-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="d82e7-150">(Yani hello dakika sayısı 0 olduğunda) her saat:`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="d82e7-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="d82e7-151">09: 00 too5 gelen her saat PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="d82e7-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="d82e7-152">09:30:00 her gün:`0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="d82e7-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="d82e7-153">09:30:00 her haftanın günü:`0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="d82e7-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="d82e7-154">**Not**: Visual Studio'dan bir Web işi dağıtırken toomark emin olun, `settings.job` dosya özellikleri 'Kopya olarak yeniyse'.</span><span class="sxs-lookup"><span data-stu-id="d82e7-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="d82e7-155"><a name="CreateScheduled"></a>Hello Azure Zamanlayıcı'yı kullanarak bir zamanlanmış WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="d82e7-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="d82e7-156">Alternatif yöntem aşağıdaki hello hello Azure Scheduler ' kullanır.</span><span class="sxs-lookup"><span data-stu-id="d82e7-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="d82e7-157">Bu durumda, WebJob hello zamanlama doğrudan bilgisi yok.</span><span class="sxs-lookup"><span data-stu-id="d82e7-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="d82e7-158">Bunun yerine, hello Azure Scheduler, yapılandırılmış tootrigger, WebJob bir zamanlamayla alır.</span><span class="sxs-lookup"><span data-stu-id="d82e7-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="d82e7-159">Hello Azure Portal zamanlanmış Web işi hello özelliği toocreate henüz yoksa, ancak bu özellik eklenene kadar hello kullanarak bunu yapabilirsiniz [Klasik portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d82e7-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="d82e7-160">Merhaba, [Klasik portal](http://manage.windowsazure.com) toohello WebJob sayfasına gidin ve'ı tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="d82e7-161">Merhaba, **nasıl tooRun** kutusunda, seçin **bir zamanlamaya göre çalışmasını**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Yeni zamanlanmış işi][NewScheduledJob]
3. <span data-ttu-id="d82e7-163">Merhaba seçin **Zamanlayıcı bölge** , işinizi ve ardından hello ekranın sağ hello iletişim tooproceed toohello sonraki hello okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="d82e7-164">Merhaba, **işi oluştur** iletişim kutusunda, hello türünü seçin **yineleme** istediğiniz: **kerelik iş** veya **yinelenen iş**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Zamanlama yinelenme][SchdRecurrence]
5. <span data-ttu-id="d82e7-166">Ayrıca bir **başlangıç** saat: **şimdi** veya **belirli bir zamanda**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Zamanlamanın başlangıç zamanı][SchdStart]
6. <span data-ttu-id="d82e7-168">Belirli bir zamanda toostart istiyorsanız, başlangıç saati değerlerinizi altında tercih **başlangıç üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="d82e7-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Belirli bir zamanda zamanlama Başlat][SchdStartOn]
7. <span data-ttu-id="d82e7-170">Yinelenen bir işi seçerseniz, hello sahip **Yinele her** seçeneği toospecify hello sıklığı geçişi ve hello **bitiş üzerinde** seçeneği toospecify bir bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="d82e7-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Zamanlama yinelenme][SchdRecurEvery]
8. <span data-ttu-id="d82e7-172">Seçerseniz **hafta**, hello seçebileceğiniz **üzerinde bir belirli bir zamanlama** kutusuna ve istediğiniz hello haftanın günlerini hello hello iş toorun belirtin.</span><span class="sxs-lookup"><span data-stu-id="d82e7-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Merhaba haftalık zamanlama gün][SchdWeeksOnParticular]
9. <span data-ttu-id="d82e7-174">Seçerseniz **ay** ve select hello **üzerinde bir belirli bir zamanlama** kutusunda ayarlayabileceğiniz hello iş toorun numaralı belirli **gün** hello aydaki.</span><span class="sxs-lookup"><span data-stu-id="d82e7-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Belirli tarihleri hello aylık zamanlama][SchdMonthsOnPartDays]
10. <span data-ttu-id="d82e7-176">Seçerseniz **haftanın günleri**, istediğiniz üzerinde iş toorun hello hello ayın hangi gün veya hello haftanın günlerini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82e7-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Ay içinde belirli haftanın günleri zamanlama][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="d82e7-178">Son olarak, aynı zamanda hello kullanabilirsiniz **oluşum** seçeneği toochoose hello ayın hangi haftası (birinci, ikinci, üçüncü vb.) belirttiğiniz haftanın günleri hello iş toorun hello üzerinde istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d82e7-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Belirli bir ay haftalarda üzerinde belirli haftanın günleri zamanlama][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="d82e7-180">Bir veya daha fazla iş oluşturduktan sonra adları, durumları, zamanlama türü ve diğer bilgileri ile Merhaba WebJobs sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="d82e7-181">Merhaba son 30 WebJobs için geçmiş bilgileri korunur.</span><span class="sxs-lookup"><span data-stu-id="d82e7-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![İşlerini listesi][WebJobsListWithSeveralJobs]

### <span data-ttu-id="d82e7-183"><a name="Scheduler"></a>Zamanlanan işler ve Azure Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="d82e7-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="d82e7-184">Zamanlanan işler hello Azure Scheduler sayfalarında Merhaba, daha da yapılandırılabilir [Klasik portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d82e7-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="d82e7-185">Merhaba işin Hello Web işleri sayfasında, tıklatın **zamanlama** bağlantı toonavigate toohello Azure Scheduler portal sayfası.</span><span class="sxs-lookup"><span data-stu-id="d82e7-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Bağlantı tooAzure Zamanlayıcı][LinkToScheduler]
2. <span data-ttu-id="d82e7-187">Merhaba Zamanlayıcı sayfasında hello işini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Merhaba Zamanlayıcı portal sayfasında iş][SchedulerPortal]
3. <span data-ttu-id="d82e7-189">Merhaba **iş eylemi** sayfası açılır, burada daha fazla hello işini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82e7-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![İş eylemi PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="d82e7-191"><a name="ViewJobHistory"></a>Merhaba iş geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d82e7-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="d82e7-192">tooview hello yürütme geçmişi bir işin hello WebJobs SDK ile oluşturulan işler de dahil olmak üzere hello altında ilgili bağlantıyı tıklatın **günlükleri** hello Web işleri dikey sütun.</span><span class="sxs-lookup"><span data-stu-id="d82e7-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="d82e7-193">(Dilerseniz hello Pano simge toocopy hello URL'si hello günlük dosyası sayfa toohello Pano kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d82e7-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Günlükleri bağlantı](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="d82e7-195">Tıklatmak hello bağlantı hello Web işi için hello Ayrıntılar sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="d82e7-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="d82e7-196">Merhaba komutu Çalıştır adını hello bu sayfa gösterir çalıştırdığınız, son kez ve başarı veya başarısızlık hello.</span><span class="sxs-lookup"><span data-stu-id="d82e7-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="d82e7-197">Altında **en son iş çalıştırmaları**, zaman toosee ilgili diğer Ayrıntılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="d82e7-199">Merhaba **WebJob çalıştırma ayrıntıları** sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="d82e7-200">Tıklatın **geçiş çıktı** hello günlük İçindekiler toosee hello metin.</span><span class="sxs-lookup"><span data-stu-id="d82e7-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="d82e7-201">Merhaba çıkış günlüğü metin biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-201">hello output log is in text format.</span></span> 
   
    ![Web işi ayrıntı çalıştırın][WebJobRunDetails]
4. <span data-ttu-id="d82e7-203">toosee hello çıkış metnini ayrı bir tarayıcı penceresinde hello tıklatın **karşıdan** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d82e7-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="d82e7-204">toodownload hello metnin kendisi, hello bağlantıya sağ tıklayın ve tarayıcı seçenekleri toosave hello dosya içeriğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d82e7-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Günlük çıktısı indirme][DownloadLogOutput]
5. <span data-ttu-id="d82e7-206">Merhaba **WebJobs** bağlantı hello sayfanın üst kısmındaki hello uygun şekilde tooget tooa listesini sağlar WebJobs hello geçmişi Panoda.</span><span class="sxs-lookup"><span data-stu-id="d82e7-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Bağlantı tooWebJobs listesi][WebJobsLinkToDashboardList]
   
    ![Geçmiş Pano Web işleri listesinde][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="d82e7-209">Aşağıdaki bağlantılardan birini tıklamak seçtiğiniz hello işi için toohello Web işi ayrıntıları sayfasına götürür.</span><span class="sxs-lookup"><span data-stu-id="d82e7-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="d82e7-210"><a name="WHPNotes"></a>Notlar</span><span class="sxs-lookup"><span data-stu-id="d82e7-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="d82e7-211">Web uygulamaları ücretsiz modda istekleri toohello scm (dağıtım) site vardır ve hello web uygulamanızın portal Azure'da açık değilse, 20 dakika sonra zaman aşımına görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82e7-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="d82e7-212">İstekleri toohello gerçek site bu sıfırlama değil.</span><span class="sxs-lookup"><span data-stu-id="d82e7-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="d82e7-213">Sürekli bir işe kod sonsuz bir döngüde toorun yazılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d82e7-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="d82e7-214">Sürekli işler yalnızca hello web uygulaması çalıştığında sürekli olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d82e7-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="d82e7-215">Temel ve hangi özellik standart modları teklif hello her zaman üzerinde etkin olduğunda, web uygulamaları boşta hale gelmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="d82e7-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="d82e7-216">Web işleri sürekli çalışan yalnızca ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82e7-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="d82e7-217">Zamanlanmış veya isteğe bağlı Webjob hata ayıklama desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d82e7-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="d82e7-218"><a name="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d82e7-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d82e7-219">Daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="d82e7-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png


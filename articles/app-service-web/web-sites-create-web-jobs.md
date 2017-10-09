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
# <a name="run-background-tasks-with-webjobs"></a>WebJobs ile arka plan görevleri çalıştırma
## <a name="overview"></a>Genel Bakış
İçinde Web işleri, programları veya komut dosyaları çalıştırabilirsiniz, [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web uygulaması üç yolla: isteğe bağlı olarak, sürekli olarak veya bir zamanlamaya göre. Hiçbir ek maliyet toouse WebJobs yoktur.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Bu makalede nasıl kullanarak Web işleri toodeploy hello gösterilmektedir [Azure Portal](https://portal.azure.com). Hakkında bilgi için Visual Studio veya sürekli teslim işlemini kullanarak toodeploy bkz [nasıl tooDeploy Azure Web işleri tooWeb uygulamaları](websites-dotnet-deploy-webjobs.md).

Hello Azure WebJobs SDK, birçok WebJobs programlama görevini basitleştirir. Daha fazla bilgi için bkz: [hello WebJobs SDK nedir](websites-dotnet-webjobs-sdk.md).

 Azure işlevleri, başka bir şekilde toorun programları ve betikleri bir sunucusuz ortamından veya bir uygulama hizmeti uygulamadan sağlar. Daha fazla bilgi için bkz: [Azure işlevlerine genel bakış](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Komut dosyaları veya programlar için kabul edilebilir dosya türleri
Şu dosya türlerini hello kabul edilir:

* .cmd, .bat, .exe (windows cmd kullanarak)
* .ps1 (powershell kullanarak)
* .sh (bash kullanarak)
* .php (php kullanarak)
* .py (python kullanarak)
* .js (düğümünü kullanarak)
* .jar (java kullanarak)

## <a name="CreateOnDemand"></a>Merhaba Portalı'nda bir üzerinde isteğe bağlı WebJob oluşturma
1. Merhaba, **Web uygulaması** hello dikey [Azure Portal](https://portal.azure.com), tıklatın **tüm ayarları > Web işleri** tooshow hello **WebJobs** dikey.
   
    ![Web işi dikey penceresi](./media/web-sites-create-web-jobs/wjblade.png)
2. **Ekle**'ye tıklayın. Merhaba **WebJob Ekle** iletişim kutusu görüntülenir.
   
    ![Web işi dikey ekleme](./media/web-sites-create-web-jobs/addwjblade.png)
3. Altında **adı**, hello Web işi için bir ad sağlayın. Merhaba ad bir harf veya sayı ile başlamalı ve özel karakterler içeremez "-" ve "_".
4. Merhaba, **nasıl tooRun** kutusunda, seçin **isteğe bağlı olarak**.
5. Merhaba, **dosyayı karşıya yüklemeyi** kutusuna hello klasör simgesine tıklayın ve komut dosyanızı içeren toohello zip dosyasını bulun. Merhaba zip dosyası yürütülebilir dosyanın (.exe .cmd .bat .sh .php .py .js) toorun program veya komut dosyası hello yanı sıra tüm destekleyici dosyaları içermelidir.
6. Denetleme **oluşturma** tooupload hello betik tooyour web uygulaması. 
   
    Hello hello Web işi için belirtilen ad hello hello listede görünür **WebJobs** dikey.
7. toorun hello Web işi, hello listesi ve tıklatın adına sağ tıklayın **çalıştırmak**.
   
    ![Web işini çalıştırma](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Sürekli olarak çalışan bir WebJob oluşturma
1. toocreate sürekli olarak çalışan bir WebJob izleyin aynı adımlar için bir WebJob oluşturma bir kez çalışır, ancak hello hello **nasıl tooRun** kutusunda, seçin **sürekli**.
2. toostart veya Dur bir sürekli Webjob'un sağ hello WebJob hello listesi ve tıklatın **Başlat** veya **durdurmak**.

> [!NOTE]
> Web uygulamanız birden çok örneğinde çalışıyorsa, sürekli olarak çalışan bir WebJob tüm örneklerinizi çalışır. Yük Dengeleme Microsoft Azure tarafından seçilen tek bir örneğinde isteğe bağlı ve zamanlanmış Web işleri çalıştırın.
> 
> İçin sürekli Webjob'lar toorun güvenilir bir şekilde ve tüm örneklerini etkinleştirin her zaman açık hello * yapılandırma ayarı durabilirsiniz hello SCM ana site uzun süre boşta zaman çalıştıran hello web uygulaması için Aksi takdirde.
> 
> 

## <a name="CreateScheduledCRON"></a>CRON ifade kullanılarak zamanlanmış bir WebJob oluşturma
Bu teknik kullanılabilir tooWeb uygulamaları temel, standart veya Premium modunda çalışıyor ve hello **her zaman açık** hello uygulamasını etkin toobe ayarlama.

yalnızca tooturn bir üzerinde isteğe bağlı WebJob zamanlanmış Web işi içine dahil bir `settings.job` hello kökündeki WebJob ZIP dosyasının dosya. Bu JSON dosyası içermelidir bir `schedule` özelliği ile bir [CRON ifade](https://en.wikipedia.org/wiki/Cron), aşağıdaki örnek başına.

Merhaba CRON ifade 6 alanlarının oluşur: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Örneğin, tootrigger, WebJob her 15 dakikada, `settings.job` gerekir:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Diğer CRON zamanlama örnekler:

* (Yani hello dakika sayısı 0 olduğunda) her saat:`0 0 * * * *` 
* 09: 00 too5 gelen her saat PM:`0 0 9-17 * * *` 
* 09:30:00 her gün:`0 30 9 * * *`
* 09:30:00 her haftanın günü:`0 30 9 * * 1-5`

**Not**: Visual Studio'dan bir Web işi dağıtırken toomark emin olun, `settings.job` dosya özellikleri 'Kopya olarak yeniyse'.

## <a name="CreateScheduled"></a>Hello Azure Zamanlayıcı'yı kullanarak bir zamanlanmış WebJob oluşturma
Alternatif yöntem aşağıdaki hello hello Azure Scheduler ' kullanır. Bu durumda, WebJob hello zamanlama doğrudan bilgisi yok. Bunun yerine, hello Azure Scheduler, yapılandırılmış tootrigger, WebJob bir zamanlamayla alır. 

Hello Azure Portal zamanlanmış Web işi hello özelliği toocreate henüz yoksa, ancak bu özellik eklenene kadar hello kullanarak bunu yapabilirsiniz [Klasik portal](http://manage.windowsazure.com).

1. Merhaba, [Klasik portal](http://manage.windowsazure.com) toohello WebJob sayfasına gidin ve'ı tıklatın **Ekle**.
2. Merhaba, **nasıl tooRun** kutusunda, seçin **bir zamanlamaya göre çalışmasını**.
   
    ![Yeni zamanlanmış işi][NewScheduledJob]
3. Merhaba seçin **Zamanlayıcı bölge** , işinizi ve ardından hello ekranın sağ hello iletişim tooproceed toohello sonraki hello okuna tıklayın.
4. Merhaba, **işi oluştur** iletişim kutusunda, hello türünü seçin **yineleme** istediğiniz: **kerelik iş** veya **yinelenen iş**.
   
    ![Zamanlama yinelenme][SchdRecurrence]
5. Ayrıca bir **başlangıç** saat: **şimdi** veya **belirli bir zamanda**.
   
    ![Zamanlamanın başlangıç zamanı][SchdStart]
6. Belirli bir zamanda toostart istiyorsanız, başlangıç saati değerlerinizi altında tercih **başlangıç üzerinde**.
   
    ![Belirli bir zamanda zamanlama Başlat][SchdStartOn]
7. Yinelenen bir işi seçerseniz, hello sahip **Yinele her** seçeneği toospecify hello sıklığı geçişi ve hello **bitiş üzerinde** seçeneği toospecify bir bitiş saati.
   
    ![Zamanlama yinelenme][SchdRecurEvery]
8. Seçerseniz **hafta**, hello seçebileceğiniz **üzerinde bir belirli bir zamanlama** kutusuna ve istediğiniz hello haftanın günlerini hello hello iş toorun belirtin.
   
    ![Merhaba haftalık zamanlama gün][SchdWeeksOnParticular]
9. Seçerseniz **ay** ve select hello **üzerinde bir belirli bir zamanlama** kutusunda ayarlayabileceğiniz hello iş toorun numaralı belirli **gün** hello aydaki. 
   
    ![Belirli tarihleri hello aylık zamanlama][SchdMonthsOnPartDays]
10. Seçerseniz **haftanın günleri**, istediğiniz üzerinde iş toorun hello hello ayın hangi gün veya hello haftanın günlerini seçebilirsiniz.
    
     ![Ay içinde belirli haftanın günleri zamanlama][SchdMonthsOnPartWeekDays]
11. Son olarak, aynı zamanda hello kullanabilirsiniz **oluşum** seçeneği toochoose hello ayın hangi haftası (birinci, ikinci, üçüncü vb.) belirttiğiniz haftanın günleri hello iş toorun hello üzerinde istediğiniz.
    
    ![Belirli bir ay haftalarda üzerinde belirli haftanın günleri zamanlama][SchdMonthsOnPartWeekDaysOccurences]
12. Bir veya daha fazla iş oluşturduktan sonra adları, durumları, zamanlama türü ve diğer bilgileri ile Merhaba WebJobs sekmesi görüntülenir. Merhaba son 30 WebJobs için geçmiş bilgileri korunur.
    
    ![İşlerini listesi][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Zamanlanan işler ve Azure Zamanlayıcı
Zamanlanan işler hello Azure Scheduler sayfalarında Merhaba, daha da yapılandırılabilir [Klasik portal](http://manage.windowsazure.com).

1. Merhaba işin Hello Web işleri sayfasında, tıklatın **zamanlama** bağlantı toonavigate toohello Azure Scheduler portal sayfası. 
   
   ![Bağlantı tooAzure Zamanlayıcı][LinkToScheduler]
2. Merhaba Zamanlayıcı sayfasında hello işini tıklatın.
   
    ![Merhaba Zamanlayıcı portal sayfasında iş][SchedulerPortal]
3. Merhaba **iş eylemi** sayfası açılır, burada daha fazla hello işini yapılandırabilirsiniz. 
   
    ![İş eylemi PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Merhaba iş geçmişini görüntüleme
1. tooview hello yürütme geçmişi bir işin hello WebJobs SDK ile oluşturulan işler de dahil olmak üzere hello altında ilgili bağlantıyı tıklatın **günlükleri** hello Web işleri dikey sütun. (Dilerseniz hello Pano simge toocopy hello URL'si hello günlük dosyası sayfa toohello Pano kullanabilirsiniz.)
   
    ![Günlükleri bağlantı](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Tıklatmak hello bağlantı hello Web işi için hello Ayrıntılar sayfası açılır. Merhaba komutu Çalıştır adını hello bu sayfa gösterir çalıştırdığınız, son kez ve başarı veya başarısızlık hello. Altında **en son iş çalıştırmaları**, zaman toosee ilgili diğer Ayrıntılar'ı tıklatın.
   
    ![WebJobDetails][WebJobDetails]
3. Merhaba **WebJob çalıştırma ayrıntıları** sayfası görüntülenir. Tıklatın **geçiş çıktı** hello günlük İçindekiler toosee hello metin. Merhaba çıkış günlüğü metin biçimindedir. 
   
    ![Web işi ayrıntı çalıştırın][WebJobRunDetails]
4. toosee hello çıkış metnini ayrı bir tarayıcı penceresinde hello tıklatın **karşıdan** bağlantı. toodownload hello metnin kendisi, hello bağlantıya sağ tıklayın ve tarayıcı seçenekleri toosave hello dosya içeriğini kullanın.
   
    ![Günlük çıktısı indirme][DownloadLogOutput]
5. Merhaba **WebJobs** bağlantı hello sayfanın üst kısmındaki hello uygun şekilde tooget tooa listesini sağlar WebJobs hello geçmişi Panoda.
   
    ![Bağlantı tooWebJobs listesi][WebJobsLinkToDashboardList]
   
    ![Geçmiş Pano Web işleri listesinde][WebJobsListInJobsDashboard]
   
    Aşağıdaki bağlantılardan birini tıklamak seçtiğiniz hello işi için toohello Web işi ayrıntıları sayfasına götürür.

## <a name="WHPNotes"></a>Notlar
* Web uygulamaları ücretsiz modda istekleri toohello scm (dağıtım) site vardır ve hello web uygulamanızın portal Azure'da açık değilse, 20 dakika sonra zaman aşımına görüntüleyebilirsiniz. İstekleri toohello gerçek site bu sıfırlama değil.
* Sürekli bir işe kod sonsuz bir döngüde toorun yazılmış toobe gerekir.
* Sürekli işler yalnızca hello web uygulaması çalıştığında sürekli olarak çalıştırılır.
* Temel ve hangi özellik standart modları teklif hello her zaman üzerinde etkin olduğunda, web uygulamaları boşta hale gelmesini engeller.
* Web işleri sürekli çalışan yalnızca ayıklayabilirsiniz. Zamanlanmış veya isteğe bağlı Webjob hata ayıklama desteklenmiyor.

## <a name="NextSteps"></a>Sonraki Adımlar
Daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları][WebJobsRecommendedResources].

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


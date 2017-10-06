---
title: "aaaAzure WebJobs belge kaynakları"
description: "Bilgi edinme kaynakları önerilen nasıl toouse Azure Web işleri ve Azure WebJobs SDK hello."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Azure Web işleri belge kaynakları
## <a name="overview"></a>Genel Bakış
Bu konu hakkındaki toodocumentation kaynakların bağlantıları toouse Azure Web işleri ve Azure WebJobs SDK hello. Azure Web işleri sağlamak kolay bir yolu toorun komut dosyaları veya programları olarak arka plan işlemleri hello bağlamındaki bir [App Service web uygulaması, API uygulaması veya mobil uygulama](../app-service/app-service-value-prop-what-is.md). Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar. Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.

Merhaba hello amacı [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) toosimplify hello kodu yazma için bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi genel görevleri ve e-postaları gönderme. Merhaba Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özelliğine sahiptir. Ayrıca, sahip toobe Genişletilebilir tasarlanmış ve var olan bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Azure işlevleri](../azure-functions/functions-overview.md) (halen Önizleme) hello C# betik, Node.js ve diğer dilleri ile çalışır WebJobs SDK sürümünü temel alır. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir. Şablonlardan Web işleri oluşturmak, yayımlama ve (çalıştırmak, durdurmak, izleme ve hata ayıklama) yönetmek bunları. 

Merhaba WebJobs hello Azure portal panosunda hello özelliği tooinvoke tek tek işlevlerinde Web işleri de dahil olmak üzere Web işleri, hello yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar. Merhaba Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler. 

## <a name="getstarted"></a>Web işleri ve hello WebJobs SDK ile çalışmaya başlama
* [Giriş tooAzure Web işleri](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure Web işleri harika ve hemen kullanmaya başlamanız gerekir!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Blog yayını Troya aramaya tarafından.)
* [Azure Web işleri özellikleri](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Merhaba WebJobs SDK nedir](websites-dotnet-webjobs-sdk.md)
* [Microsoft desenleri ve uygulamalar tarafından arka plan işleri Kılavuzu](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Merhaba 1.1.0 tanışın RTM, Microsoft Azure Web işleri SDK'si](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Hello Azure WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk-get-started.md)
* [Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Nasıl toouse Azure tablo depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Web işleri SDK'si toouse Azure Service Bus ile nasıl hello](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs SDK hızlı başvuru (PDF indirme)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Web işleri ayarları belgeler github](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Videolar
  * [Web işleri ve hello Web işleri SDK'si](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Visual Studio Araçları ile tanışın Web işleri](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Azure Web işleri güncelleştirme ile Pranav Rastogi - sürüm 1.1 genişletilebilirliği](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Merhaba bölümleri aşağıdaki Ayrıca bkz. [dağıtma WebJobs](#deploy) ve [test ve hata ayıklama Web işleri](#debug).

## <a name="deploy"></a>Web işleri dağıtma
* [Nasıl tooDeploy Visual Studio kullanarak Azure Web işleri](websites-dotnet-deploy-webjobs.md)
* [Nasıl toodeploy WebJobs kullanma izin ver hello Azure portalı](web-sites-create-web-jobs.md)
* [Azure Web işleri komut satırı veya sürekli dağıtımını etkinleştirme](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [WebJobs kullanan bir .NET konsol uygulaması tooAzure dağıtma Git](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [F # WebJob tooAzure dağıtma](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Azure Webjobs olarak özel Hizmetleri dağıtma](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Videolar
  * [Visual Studio Araçları ile tanışın Web işleri](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Web işleri planlaması
* [Hello Azure WebJob iletişim kutusu Ekle](websites-dotnet-deploy-webjobs.md#configure)
* [Hello Azure Portal zamanlanmış WebJob oluşturma](web-sites-create-web-jobs.md#CreateScheduled)
* [Zamanlayıcı İş tooa WebJob takma](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Azure Web işleri cron ifadelerle planlama](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Merhaba WebJobs SDK TimerTrigger kullanarak tek tek Web işi işlevleri planlama](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Test ve WebJobs hata ayıklama
* [Yeni Geliştirici ve Visual Studio'da Azure Web işleri için hata ayıklama özellikleri](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Merhaba Web işleri Panosu'nu görüntülemek](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Nasıl toowrite günlüklerini kullanarak Web işleri SDK'si hello ve hello Pano görüntüleyin](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Uzaktan hata ayıklama Web işleri](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Kimin bu blob yazdı?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Etkileşimli kodda hello bulut barındırma](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [İzleme tooAzure WebJobs ekleme](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [İzleme, tanılama ve Microsoft Azure Storage sorunlarını giderme](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Videolar
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Web işleri ölçeklendirme
* [Web uygulamanızı Azure Web siteleri ile ölçeklendirme](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure uygulama hizmeti: Büyük ölçekli işletme için hazır Web uygulamaları mimariden](https://channel9.msdn.com/Events/Build/2014/3-626). Web uygulamalarının hello Web işleri SDK'si dahil olmak üzere Web işleri ile kapsar ölçeklendirme.
* Videolar
  * [Web işleri ölçeklendirme](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Ek Web işleri kaynaklar
* [Azure Web işleri GA blog gönderisi Magnus Mårtensson tarafından](http://magnusmartensson.com/azure-webjobs-ga)
* [PowerShell Web işleri Azure uygulama hizmeti üzerinde çalışan](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Azure Web işleri tetiklendiğinde bildirim tamamlar](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Web işleri ile basit Web uygulaması yedekleme bekletme ilkesi](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Azure Web uygulamaları ve bulut Hizmetleri yavaş ilk isteği](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Nasıl toouse WebJobs toosimulate hello yalnızca hello standart fiyatlandırma katmanı için kullanılabilir AlwaysOn özelliğini gösterir.
* [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). İçin Web işleri SDK'si kapama, bkz: [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).)
* [Azure Web işleri & AzCopy yedeklemelerde otomatikleştirme](http://markjbrown.com/azure-webjobs-azcopy/)
* Videolar
  * [Azure Web işleri videolar Magnus Mårtensson tarafından](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Ek Web işleri SDK'si kaynaklar
* [WebJobs SDK sürüm notları](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [WebJobs SDK kaynak kodu](https://github.com/Azure/azure-webjobs-sdk)
* [WebJobs SDK uzantıları kaynak kodu](https://github.com/Azure/azure-webjobs-sdk-extensions), ile [ayrıntılı kılavuz toohello genişletilebilirlik modeli](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [WebJobs SDK komut dosyası kaynak kodu](https://github.com/Azure/azure-webjobs-sdk-script/) (için kullanılan [Azure işlevleri](../azure-functions/functions-overview.md))
* [WebJob tooupload FREB dosyaları tooAzure depolama kullanan hello Web işleri SDK'si](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Azure Web işleri Azure dışında barındırma, Azure avantajları günlüğü hello ile Web işi barındırılan](http://bypassion.dk/?p=510)
* [Veri alma aracı ile Azure Web işleri oluşturma](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Azure işlevlerine genel bakış](../azure-functions/functions-overview.md)
* Videolar
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Örnek Web işi uygulamalar
* [Github'da hello WebJobs ekibi tarafından sağlanan örnek uygulamaları](https://github.com/azure/azure-webjobs-sdk-samples)
* [Basit Azure Web uygulaması Web işleri hello Web işleri SDK'si kullanarak arka ucu ile](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Zamanlanmış ve olay denetimli Web işleri kullanımını göstermektedir. Merhaba blog gönderisi bkz [Rebuilding hello Azure WebJobs SDK'sını kullanarak SiteMonitR](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogları
* [Azure blogu](/blog)
* [Amit Apple'nın blogu](http://blog.amitapple.com/). Web işleri (değil SDK hello) odaklanır.
* [Magnus Mårtensson'ın blogu](http://magnusmartensson.com/)

## <a name="gethelp"></a>Web işleri ile ilgili Yardım alma
* [Web işleri için StackOverflow](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [Merhaba WebJobs SDK StackOverflow](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [Azure işlevleri için StackOverflow](http://stackoverflow.com/questions/tagged/azure-functions)
* [Azure ve ASP.NET Forumu](http://forums.asp.net/1247.aspx)
* [Azure App Service Web Apps Forumu](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Azure Web Apps kullanıcı sesi site](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Merhaba diyez #AzureWebJobs kullanın.
* [Web işleri hata veya sorun raporu](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)


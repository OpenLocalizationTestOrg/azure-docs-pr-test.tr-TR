---
title: "Azure Web işleri belge kaynakları"
description: "Azure Web işleri ve Azure WebJobs SDK nasıl kullanılacağını öğrenmek için kaynaklar önerilir."
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
ms.openlocfilehash: 05062d7396bdbb3e589d2ab5f0443d1dca54342a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Azure Web işleri belge kaynakları
## <a name="overview"></a>Genel Bakış
Azure Web işleri ve Azure WebJobs SDK nasıl kullanılacağı hakkında belge kaynakları bu konuda bağlantılar. Azure Web işleri bağlamında arka plan işlemleri olarak program veya komut dosyaları çalıştırmak için kolay bir yol sağlayan bir [App Service web uygulaması, API uygulaması veya mobil uygulama](../app-service/app-service-value-prop-what-is.md). Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar. Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.

Amacı [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi ortak görevler için yazdığınız kodları kolaylaştırmaktır ve e-postaları gönderme. Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özellikler vardır. Ayrıca, Genişletilebilir olmak için tasarlanmıştır ve var. bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Azure işlevleri](../azure-functions/functions-overview.md) (halen Önizleme) bir C# betik, Node.js ve diğer dilleri ile çalışır WebJobs SDK sürümünü temel alır. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir. Şablonlardan Web işleri oluşturmak, yayımlama ve (çalıştırmak, durdurmak, izleme ve hata ayıklama) yönetmek bunları. 

Web işleri Panosu'nu Azure portalında WebJobs, Web işleri içinde tek tek işlevleri çağırma yeteneği dahil olmak üzere yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar. Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler. 

## <a name="getstarted"></a>Web işleri ve WebJobs SDK ile çalışmaya başlama
* [Azure Web işleri giriş](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure Web işleri harika ve hemen kullanmaya başlamanız gerekir!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Blog yayını Troya aramaya tarafından.)
* [Azure Web işleri özellikleri](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [WebJobs SDK nedir](websites-dotnet-webjobs-sdk.md)
* [Microsoft desenleri ve uygulamalar tarafından arka plan işleri Kılavuzu](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [1.1.0 tanışın Microsoft Azure WebJobs SDK'ın RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Azure WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk-get-started.md)
* [Web İşleri SDK’sı ile Azure kuyruk depolama kullanımı](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Web İşleri SDK’sı ile Azure blob depolama kullanımı](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Web İşleri SDK’sı ile Azure tablo depolama kullanımı](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Web İşleri SDK’sı ile Azure Service Bus kullanımı](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs SDK hızlı başvuru (PDF indirme)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Web işleri ayarları belgeler github](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Videolar
  * [Web işleri ve Web işleri SDK'si](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Visual Studio Araçları ile tanışın Web işleri](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Azure Web işleri güncelleştirme ile Pranav Rastogi - sürüm 1.1 genişletilebilirliği](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Aşağıdaki bölümlerde ayrıca bakın [dağıtma Web işleri](#deploy) ve [test ve hata ayıklama Web işleri](#debug).

## <a name="deploy"></a>Web işleri dağıtma
* [Nasıl yapılır Azure Visual Studio'yu kullanarak Web işleri dağıtma](websites-dotnet-deploy-webjobs.md)
* [Azure Portalı'nı kullanarak Web işleri dağıtma](web-sites-create-web-jobs.md)
* [Azure Web işleri komut satırı veya sürekli dağıtımını etkinleştirme](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Bir .NET konsol uygulaması Web işleri kullanarak Azure'a dağıtma Git](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [F # Web işi Azure'a dağıtma](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Azure Webjobs olarak özel Hizmetleri dağıtma](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Videolar
  * [Visual Studio Araçları ile tanışın Web işleri](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Web işleri planlaması
* [Azure Web işi iletişim ekleyin](websites-dotnet-deploy-webjobs.md#configure)
* [Azure portalında bir zamanlanmış WebJob oluşturma](web-sites-create-web-jobs.md#CreateScheduled)
* [Bir Web işi için bir zamanlayıcı iş takma](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Azure Web işleri cron ifadelerle planlama](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [WebJobs SDK TimerTrigger kullanarak tek tek Web işi işlevleri planlama](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Test ve WebJobs hata ayıklama
* [Yeni Geliştirici ve Visual Studio'da Azure Web işleri için hata ayıklama özellikleri](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Web işleri Panosu'nu görüntülemek](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [WebJobs SDK'sını kullanarak günlüklerini yazma ve panosunda Göster](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Uzaktan hata ayıklama Web işleri](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Kimin bu blob yazdı?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Etkileşimli kodu bulutta barındırma](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Azure Web işleri izleme ekleme](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [İzleme, tanılama ve Microsoft Azure Storage sorunlarını giderme](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Videolar
  * [Web işleri araçları ve uzaktan hata ayıklama](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Web işleri ölçeklendirme
* [Web uygulamanızı Azure Web siteleri ile ölçeklendirme](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure uygulama hizmeti: Büyük ölçekli işletme için hazır Web uygulamaları mimariden](https://channel9.msdn.com/Events/Build/2014/3-626). WebJobs, Web işleri SDK'si dahil olmak üzere ile web uygulamaları, perde ölçeklendirme.
* Videolar
  * [Web işleri ölçeklendirme](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Ek Web işleri kaynaklar
* [Azure Web işleri GA blog gönderisi Magnus Mårtensson tarafından](http://magnusmartensson.com/azure-webjobs-ga)
* [PowerShell Web işleri Azure uygulama hizmeti üzerinde çalışan](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Azure Web işleri tetiklendiğinde bildirim tamamlar](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Web işleri ile basit Web uygulaması yedekleme bekletme ilkesi](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Azure Web uygulamaları ve bulut Hizmetleri yavaş ilk isteği](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Web işleri yalnızca standart fiyatlandırma katmanı için kullanılabilir olan AlwaysOn özelliği benzetimini yapmak için nasıl kullanılacağını gösterir.
* [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). İçin Web işleri SDK'si kapama, bkz: [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).)
* [Azure Web işleri & AzCopy yedeklemelerde otomatikleştirme](http://markjbrown.com/azure-webjobs-azcopy/)
* Videolar
  * [Azure Web işleri videolar Magnus Mårtensson tarafından](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Ek Web işleri SDK'si kaynaklar
* [WebJobs SDK sürüm notları](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [WebJobs SDK kaynak kodu](https://github.com/Azure/azure-webjobs-sdk)
* [WebJobs SDK uzantıları kaynak kodu](https://github.com/Azure/azure-webjobs-sdk-extensions), ile [genişletilebilirlik modeline ayrıntılı kılavuz](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [WebJobs SDK komut dosyası kaynak kodu](https://github.com/Azure/azure-webjobs-sdk-script/) (için kullanılan [Azure işlevleri](../azure-functions/functions-overview.md))
* [Azure WebJobs SDK'sını kullanarak depolama birimine FREB dosyaları karşıya yükleme için Web işi](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Azure Web işleri Azure dışında barındırma, günlük avantajları Azure ile Web işi barındırılan](http://bypassion.dk/?p=510)
* [Veri alma aracı ile Azure Web işleri oluşturma](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Azure işlevlerine genel bakış](../azure-functions/functions-overview.md)
* Videolar
  * [Azure Web işleri Channel 9 video serisi](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Örnek Web işi uygulamalar
* [Github'da WebJobs ekibi tarafından sağlanan örnek uygulamaları](https://github.com/azure/azure-webjobs-sdk-samples)
* [Basit Azure Web uygulaması Web işleri WebJobs SDK'sını kullanarak arka ucu ile](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Zamanlanmış ve olay denetimli Web işleri kullanımını göstermektedir. Blog gönderisine bakın [Azure WebJobs SDK'sını kullanarak SiteMonitR yeniden](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogları
* [Azure blogu](/blog)
* [Amit Apple'nın blogu](http://blog.amitapple.com/). Web işleri (değil SDK) odaklanır.
* [Magnus Mårtensson'ın blogu](http://magnusmartensson.com/)

## <a name="gethelp"></a>Web işleri ile ilgili Yardım alma
* [Web işleri için StackOverflow](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow WebJobs SDK'sı](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [Azure işlevleri için StackOverflow](http://stackoverflow.com/questions/tagged/azure-functions)
* [Azure ve ASP.NET Forumu](http://forums.asp.net/1247.aspx)
* [Azure App Service Web Apps Forumu](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Azure Web Apps kullanıcı sesi site](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Diyez #AzureWebJobs kullanın.
* [Web işleri hata veya sorun raporu](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)


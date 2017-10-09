---
title: "Application Insights ile aaaSCOM tümleştirme | Microsoft Docs"
description: "SCOM kullanıcı değilseniz, Application Insights ile sorunlarını tanılamak ve performansını izleyebilir. Kapsamlı panoları, akıllı uyarıları, güçlü tanılama araçları ve analiz sorguları."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>SCOM için Application Insights kullanarak uygulama performansı izleme
System Center Operations Manager (SCOM) toomanage sunucularınız kullanıyorsanız, performansı izleyerek ve hello Yardımı ile performans sorunlarını tanılamanıza [Azure Application Insights](app-insights-asp-net.md). Application Insights REST ve SQL çağrıları, özel durumlar ve günlük izlemelerini giden web uygulamanızın gelen istekleri izler. Panolar ölçüm grafikler ve akıllı uyarıları yanı sıra güçlü tanılama arama ve analitik sorguları ile bu telemetri sağlar. 

SCOM Yönetim Paketi kullanarak Application Insights izleme geçiş yapabilirsiniz.

## <a name="before-you-start"></a>Başlamadan önce
Biz varsayın:

* Web sunucuları ile SCOM tanıdık ve IIS SCOM 2012 R2 veya 2016 toomanage kullanın.
* Application Insights ile toomonitor istediğiniz bir web uygulaması sunucularınıza zaten yüklediniz.
* Uygulama framework .NET 4.5 veya üzeri sürümüdür.
* Erişim tooa abonelik sahip [Microsoft Azure](https://azure.com) ve toohello kaydolabilirsiniz [Azure portal](https://portal.azure.com). Kuruluşunuz bir aboneliğe sahip ve Microsoft hesabı tooit ekleyebilirsiniz.

(Merhaba geliştirme ekip hello [Application Insights SDK'sı](app-insights-asp-net.md) hello web uygulamada. Bu derleme araçları bunları özel telemetri yazma büyük esneklik sağlar. Ancak, önemli değildir: ile ya da SDK'sı yerleşik olarak hello olmadan burada açıklanan başlangıç adımları izleyebilirsiniz.)

## <a name="one-time-install-application-insights-management-pack"></a>(Bir saat) Application Insights Yönetimi paketini yükleyin
Operations Manager çalıştırdığı hello makinede:

1. Merhaba Yönetim Paketi herhangi bir eski sürümü kaldırın:
   1. Operations Manager'da yönetim, yönetim paketleri açın. 
   2. Merhaba eski sürümünü silin.
2. İndirip hello Yönetim Paketi hello Kataloğu'ndan yükleyin.
3. Operations Manager'ı yeniden başlatın.

## <a name="create-a-management-pack"></a>Bir yönetim paketi oluşturun
1. Operations Manager'da açmak **yazma**, **.NET Application Insights ile...**, **izleme Ekleme Sihirbazı'nı**, yeniden seçin **.NET Application Insights ile...**.
   
    ![](./media/app-insights-scom/020.png)
2. Uygulamanızı sonra adı hello yapılandırması. (Bir zamanda tooinstrument bir uygulama vardır.)
   
    ![](./media/app-insights-scom/030.png)
3. Üzerinde hello aynı sihirbaz sayfasında, ya da oluşturma yeni bir Yönetim Paketi veya Application Insights için daha önce oluşturduğunuz bir paket seçin.
   
     (Application Insights hello [Yönetim Paketi](https://technet.microsoft.com/library/cc974491.aspx) örneği oluşturduğunuz bir şablonu. Merhaba aynı örnek daha sonra yeniden kullanabilirsiniz.)

    ![Hello genel özellikler sekmesi, hello uygulama hello adını yazın. Yeni'yi tıklatın ve bir Yönetim Paketi için bir ad yazın. Tamam'ı tıklatın, sonra İleri'yi tıklatın.](./media/app-insights-scom/040.png)

1. Bir uygulama seçin toomonitor istiyor. sunucularınızda yüklü uygulamalar arasında Hello arama özelliğini arar.
   
    ![Hangi tooMonitor sekmesinde Ekle'yi tıklatın, hello uygulama ad bölümünü yazın, Ara'yı tıklatın, hello uygulama ve ekleme, Tamam'ı seçin.](./media/app-insights-scom/050.png)
   
    tüm sunucuları toomonitor hello uygulamada istemiyorsanız hello isteğe bağlı izleme kapsamı alan kullanılan toospecify, sunucularınızın bir alt olabilir.
2. Merhaba sonraki sihirbaz sayfasında, kimlik bilgileri toosign tooMicrosoft Azure içinde ilk sağlamanız gerekir.
   
    Bu sayfada hello Application Insights kaynağı Analiz ve görüntülenen hello telemetri verileri toobe istediğiniz yeri seçin. 
   
   * Merhaba uygulama geliştirme sırasında Application Insights için yapılandırıldıysa, var olan kaynağı seçin.
   * Aksi takdirde, başlangıç uygulaması için adlı yeni bir kaynak oluşturun. Bileşenlerinin başka uygulamalar varsa hello aynı sistem put bunları hello aynı kaynak grubu, toomake erişim toohello telemetri daha kolay toomanage.
     
     Bu ayarları daha sonra değiştirebilirsiniz.
     
     ![Application Insights Ayarlar sekmesinde, 'oturum aç' tıklayın ve Azure için Microsoft hesabı kimlik bilgilerinizi sağlayın. Ardından bir abonelik, kaynak grubu ve kaynak seçin.](./media/app-insights-scom/060.png)
3. Tam hello Sihirbazı.
   
    ![Oluştur’a tıklayın](./media/app-insights-scom/070.png)

Toomonitor istediğiniz her uygulama için bu yordamı yineleyin.

Toochange ayarları daha sonra gerekirse hello İzleyicisi Merhaba yazma penceresinde hello özelliklerini yeniden açın.

![Yazma, .NET uygulama performansı izleme Application Insights ile seçin, sizin İzleyicisi'ni seçin ve Özellikler'i tıklatın.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>İzleme doğrulayın
Merhaba İzleyicisi her sunucuda yüklü uygulamanızı arar. Burada hello uygulama bulur Application Insights Durum İzleyicisi toomonitor hello uygulama yapılandırır. Gerekirse, hello sunucuda ilk Durum İzleyicisi'ni yükler.

Merhaba uygulama hangi örneklerini bulduğu doğrulayabilirsiniz:

![İzleme, Application Insights açın](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Application Insights telemetrisi görünümü
Merhaba, [Azure portal](https://portal.azure.com), uygulamanız için toohello kaynak göz atın. [Telemetri gösteren grafikleri görmek](app-insights-dashboards.md) uygulamanızdan. (Hello ana sayfasında henüz gösterilen kurmadı, Canlı ölçümleri akış'ı tıklatın.)

## <a name="next-steps"></a>Sonraki adımlar
* [Bir Pano ayarlamak](app-insights-dashboards.md) toobring birlikte hello en önemli grafikleri bu ve diğer uygulamalar izleme.
* [Ölçümler hakkında bilgi edinin](app-insights-metrics-explorer.md)
* [Uyarıları ayarlayın](app-insights-alerts.md)
* [Performans sorunlarını tanılama](app-insights-detect-triage-diagnose.md)
* [Güçlü Analytics sorgular](app-insights-analytics.md)
* [Kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md)


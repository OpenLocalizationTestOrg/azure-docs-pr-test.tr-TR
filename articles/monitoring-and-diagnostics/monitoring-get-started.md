---
title: "aaaGet Azure İzleyicisi ile başlatılan | Microsoft Docs"
description: "Azure İzleyici toogain hello işlem kaynaklarınızın bir anlayış kullanmaya başlamanıza ve verilerini temizleyebilirsiniz temel adımları uygulayın."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Azure İzleyici’yi kullanmaya başlama
Azure İzleyici Azure kaynakları izlemek için tek bir kaynak sağlar hello platform hizmetidir. Azure izleme ile görselleştirme, sorgulama yapabilir, yol, arşiv ve hello ölçümleri ve Azure kaynaklarında'ten gelen günlükleri üzerinde işlem gerçekleştirin. Merhaba İzleyici portal dikey penceresinde, kullanarak bu verilerle çalışma [İzleyici PowerShell cmdlet'leri](insights-powershell-samples.md), [platformlar arası CLI](insights-cli-samples.md), veya [Azure İzleyici REST API'lerini](https://msdn.microsoft.com/library/dn931943.aspx). Bu makalede, hello anahtar tanıtımı için hello portal'ı kullanarak Azure İzleyicisi bileşenlerinin bazılarını size rehberlik eder.

1. Merhaba Portalı'nda çok gidin**daha fazla hizmet** ve hello bulur **İzleyici** seçeneği. Böylece her zaman hello sol gezinti çubuğunda kolayca erişilebilir hello yıldız simgesine tooadd bu seçeneği tooyour Sık Kullanılanlar listesine tıklayın.
   
    ![Merhaba Hizmetler listesinde izleme](./media/monitoring-get-started/monitor-more-services.png)
2. Merhaba tıklatın **İzleyici** hello ayarlama seçeneği tooopen **İzleyici** dikey. Bu dikey pencere tüm izleme ayarlarınızı ve verilerinizi tek bir birleştirilmiş görünümde gösterir. Toohello ilk açıldığında **etkinlik günlüğü** bölümü.
   
    ![İzleyici dikey penceresinde gezinme](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Azure İzleyicisi izleme verilerinin üç temel kategorisi vardır: Merhaba **etkinlik günlüğü**, **ölçümleri**, ve **tanılama günlükleri**.
3. Tıklatın **etkinlik günlüğü** etkinlik günlük bölümü hello tooensure görüntülenir.
   
    ![Etkinlik Günlüğü dikey penceresi](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Merhaba [ **etkinlik günlüğü** ](monitoring-overview-activity-logs.md) aboneliğinizde kaynaklar üzerinde gerçekleştirilen tüm işlemler açıklanmaktadır. Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz ' ne, kimin, ne zaman ve ' herhangi bir oluşturma için güncelleştirme veya silme işlemleri aboneliğinizde kaynaklardaki. Örneğin, hello etkinlik günlüğü, ne zaman bir web uygulaması durduruldu ve kimlerin durduruldu bildirir. Etkinlik günlüğü olaylarını hello platform ve kullanılabilir tooquery 90 gün süreyle depolanır.
   
    Oluşturun ve her zaman Ölçütünüzle eşleşen olaylar meydana gelmiş bilirsiniz ortak filtreleri sonra PIN hello en önemli sorguları tooa portal panosu için sorgular kaydedin.
4. Geçen hafta hello Hello görünüm tooa belirli kaynak grubu filtre ve ardından hello **kaydetmek** düğmesi.
   
    ![Etkinlik günlüğü sorgusunu kaydedin](./media/monitoring-get-started/monitor-act-log-save.png)
5. Şimdi, hello tıklayın **PIN** düğmesi.
   
    ![Etkinlik günlüğü için sabitle düğmesine tıklayın](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    Bu kılavuzda hello görünümleri çoğunu sabitlenmiş tooa Pano olabilir. Bunun yapılması, hizmetlerinize ilişkin çalışma verilerine ait tek bir bilgi kaynağı oluşturmanıza yardımcı olur. 
6. Tooyour Pano döndür. Şimdi, hello sorgu (ve sonuç sayısı) Panonuzda görüntülendiğini görebilirsiniz. Bu, aboneliğinizde son ör oluşan herhangi bir yüksek profilli eylem tooquickly bakın istiyorsanız kullanışlıdır. yeni bir rolün atanması veya bir sanal makinenin silinmesi) hızlıca görmek istiyorsanız bunun yapılması yararlıdır.
   
    ![Etkinlik günlüğü sabitlenmiş toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Toohello dönmek **İzleyici** parçasında ve hello tıklatın **ölçümleri** bölümü. İlk filtreleme ve hello dikey penceresinde hello üstünde hello açılan seçenekleri kullanarak seçerek tooselect kaynak gerekir.
   
    ![Ölçümler için kaynak filtreleme](./media/monitoring-get-started/monitor-met-filter.png)
   
    Tüm Azure kaynakları [**ölçümler**](monitoring-overview-metrics.md) gösterir. Bu görünüm, kaynaklarınızın performansını kolayca anlayabilmeniz için tüm ölçümleri tek bir cam bölmede bir araya getirir.
8. Bir kaynak seçtikten sonra tüm kullanılabilir ölçümler yan hello dikey pencerenin sol hello üzerinde görüntülenir. Ölçümleri seçerek aynı anda birden çok ölçümleri grafik ve hello grafik türü ve zaman aralığını değiştirebilirsiniz. Ayrıca bu kaynak üzerinde oluşturulmuş tüm ölçüm uyarılarını görüntüleyebilirsiniz.
   
    ![Ölçüm dikey penceresi](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Bazı ölçümler yalnızca kaynağınızda [Application Insights](../application-insights/app-insights-overview.md) ve/veya Windows ya da Linux Azure Tanılama etkinleştirilerek kullanılabilir.
   > 
   > 
9. Grafiğinizi hazır olduğunuzda, hello kullanabilirsiniz **PIN** düğmesini toopin onu tooyour Pano.
10. Toohello iade **İzleyici** tıklayın ve dikey **tanılama günlükleri**.
    
    ![Tanılama günlükleri dikey penceresi](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Tanılama günlüklerini** ](monitoring-overview-of-diagnostic-logs.md) olan yayılan günlükleri *tarafından* hello işlemi, belirli bir kaynak hakkında veri sağlayan bir kaynak. Örneğin, Ağ Güvenliği Grup Kuralı Sayaçları ve Mantıksal Uygulama İş Akışı Günlükleri, tanılama günlüğü türleridir. Bu günlükler akış tooan olay hub'ı bir depolama hesabında depolanan ve/veya çok gönderilen[günlük analizi](../log-analytics/log-analytics-overview.md). Log Analytics, Microsoft'un gelişmiş arama ve uyarı vermeye yönelik işletimsel bilgi ürünüdür.
    
    Hello Portalı'nda görüntüleyin ve etkin tanılama günlükleri varsa, abonelik tooidentify tüm kaynakların bir listesini filtreleyin.
11. Merhaba tanılama günlüklerini dikey penceresinde bir kaynak'ı tıklatın. Tanılama günlükleriniz bir depolama hesabına kaydediliyorsa doğrudan indirebileceğiniz saatlik günlüklerin bir listesini görürsünüz.
    
    ![Bir kaynağın tanılama günlükleri](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    Tıklatarak **tanılama ayarlarını**, hangi yukarı tooset izin verir veya tooEvent hub akış veya tooa günlük analizi çalışma alanı gönderme ayarlarınızı arşivleme tooa depolama hesabı için değiştirin.
    
    ![Tanılama günlüklerini etkinleştirme](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Tanılama günlüklerini tooLog Analytics ayarlarsanız, sonra bunları hello arayabilirsiniz **günlük arama** hello portalı bölümü.
12. Toohello gidin **uyarıları** hello İzleyici dikey bölümü.
    
    ![genel kullanıma yönelik uyarılar dikey penceresi](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Burada Azure kaynaklarınıza ilişkin tüm [**uyarıları**](monitoring-overview-alerts.md) yönetebilirsiniz. Bu ölçümleri, etkinlik günlüğü olaylarını, Application Insights web testleri (konumlara) ve Application Insights öngörülü tanılama uyarılarını içerir. Uyarılar, gönderilen e-posta toobe ya da bir HTTP POST tooa Web kancası URL'si tetikleyebilir.
13. Tıklatın **ölçüm uyarı Ekle** toocreate bir uyarı.
    
    ![ölçüm uyarısı ekleme](./media/monitoring-get-started/monitor-alerts-add.png)
    
    Herhangi bir zamanda durumuna PIN bir uyarı tooyour Pano tooeasily bkz sonra kullanabilirsiniz.
14. Merhaba izleme bölümü de içerir bağlantılar çok[Application Insights](../application-insights/app-insights-overview.md) uygulamaları ve [günlük analizi](../log-analytics/log-analytics-overview.md) yönetim çözümleri. Bu diğer Microsoft ürünleri, Azure İzleyici ile kapsamlı tümleştirmeye sahiptir.
15. Application Insights veya Log Analytics kullanmıyorsanız Azure İzleyici mevcut izleme, günlüğe kaydetme ve uyarı verme ürünleriyle bir ortaklığa sahip olabilir. Bkz: bizim [iş ortakları sayfasında](monitoring-partners.md) tam listesi ve hakkında yönergeler için toointegrate.

Şu adımları izleyin ve tüm ilgili döşeme tooa panoya sabitleme, uygulama ve bunun gibi altyapı kapsamlı görünümlerini oluşturabilirsiniz:

![Azure İzleyici panosu](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Sonraki Adımlar
* Okuma hello [Azure İzleyicisi'ne genel bakış](monitoring-overview.md)


---
title: "Azure İzleyicisi ile çalışmaya başlama | Microsoft Docs"
description: "Kaynaklarınızın çalışmasını anlamak ve verilere dayalı işlem yapmak için Azure İzleyici kullanmaya başlayın."
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
ms.date: 09/25/2017
ms.author: johnkem
ms.openlocfilehash: ba4e8fe0d54deb4a980174ff7d0904854c794d3d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-monitor"></a>Azure İzleyici’yi kullanmaya başlama
Azure İzleyici, Azure kaynaklarını izlemeye yönelik tek bir kaynak sağlayan platform hizmetidir. Azure İzleyici ile Azure’daki kaynaklardan gelen ölçüm ve günlükleri görüntüleyebilir, sorgulayabilir, yönlendirebilir ve bunlar üzerinde işlem yapabilirsiniz. İzleyici portal dikey penceresi, [İzleyici PowerShell Cmdlet’leri](insights-powershell-samples.md), [Platformlar Arası CLI](insights-cli-samples.md) veya [Azure İzleyici REST API’leri](https://msdn.microsoft.com/library/dn931943.aspx) kullanarak bu verilerle çalışabilirsiniz. Bu makalede portal gösterim amacıyla kullanılarak Azure İzleyici’nin temel bileşenlerinden birkaç tanesi gösterilecektir.

## <a name="walkthrough"></a>Kılavuz
1. Portalda **Diğer hizmetler**’e gidin ve **İzleyici** seçeneğini bulun. Bu seçeneği sol gezinti çubuğundan kolayca erişilebilmesi için sık kullanılanlar listenize eklemek üzere yıldız simgesine tıklayın.

    ![Hizmet listesinde İzleyici](./media/monitoring-get-started/monitor-more-services.png)
2. **İzleyici** seçeneğine tıklayarak **İzleyici** dikey penceresini açın. Bu dikey pencere tüm izleme ayarlarınızı ve verilerinizi tek bir birleştirilmiş görünümde gösterir. İlk olarak **Etkinlik günlüğü** bölümü açılır.

    ![İzleyici dikey penceresinde gezinme](./media/monitoring-get-started/monitor-blade-nav.png)

    Azure İzleyici, verileri üç temel kategoride izler: **etkinlik günlüğü**, **ölçümler** ve **tanılama günlükleri**.
3. Etkinlik günlüğü bölümünün gösterildiğinden emin olmak için **Etkinlik günlüğü**’ne tıklayın.

    ![Etkinlik Günlüğü dikey penceresi](./media/monitoring-get-started/monitor-act-log-blade.png)

    [**Etkinlik günlüğü**](monitoring-overview-activity-logs.md), aboneliğinizdeki kaynaklar üzerinde gerçekleştirilen tüm işlemleri açıklar. Etkinlik Günlüğü’nü kullanarak aboneliğinizdeki kaynaklarla ilgili herhangi bir oluşturma, güncelleştirme veya silme işlemine ilişkin ‘ne, kim ve ne zaman’ sorularına yanıt bulabilirsiniz. Örneğin, Etkinlik Günlüğü bir web uygulamasının ne zaman ve kim tarafından durdurulduğunu söyler. Etkinlik Günlüğü olayları platforma depolanır ve 90 gün boyunca sorgulanabilir.

    Ortak filtrelere yönelik sorgular oluşturup kaydedebilir ve sonra ölçütlerinizi karşılayan olayların gerçekleşip gerçekleşmediğinden her zaman haberdar olmak için en önemli sorguları bir portal panosuna sabitleyebilirsiniz.
4. Görünümü son bir haftadaki belirli bir kaynak grubu ile filtreleyin, ardından **Kaydet** düğmesine tıklayın.

    ![Etkinlik günlüğü sorgusunu kaydedin](./media/monitoring-get-started/monitor-act-log-save.png)
5. Şimdi **Sabitle** düğmesine tıklayın.

    ![Etkinlik günlüğü için sabitle düğmesine tıklayın](./media/monitoring-get-started/monitor-act-log-pin.png)

    Bu kılavuzdaki görünümlerin birçoğu panoya sabitlenebilir. Bunun yapılması, hizmetlerinize ilişkin çalışma verilerine ait tek bir bilgi kaynağı oluşturmanıza yardımcı olur.
6. Panonuza geri dönün. Şu anda sorgunun (ve sonuç sayısının) panonuzda gösterildiğini görebilirsiniz. Bu hızlı bir şekilde, aboneliğinizde son oluşan herhangi bir yüksek profilli eylem görmek istiyorsanız, örneğin yeni bir rolü atandı veya VM silindi yararlı olur.

    ![Panosuna sabitlediğiniz etkinlik günlükleri](./media/monitoring-get-started/monitor-act-log-db.png)
7. **İzleyici** kutucuğuna geri dönüp **Ölçümler** bölümüne tıklayın. İlk kaynak filtreleme ve dikey pencerenin en üstünde açılan Seçenekleri'ni kullanarak seçerek seçmeniz gerekir.

    ![Ölçümler için kaynak filtreleme](./media/monitoring-get-started/monitor-met-filter.png)

    Tüm Azure kaynakları [**ölçümler**](monitoring-overview-metrics.md) gösterir. Bu görünüm, kaynaklarınızın performansını kolayca anlayabilmeniz için tüm ölçümleri tek bir cam bölmede bir araya getirir. Ayrıca bizim marka denetleyin [deneyimi grafik yeni ölçümü](https://aka.ms/azuremonitor/new-metrics-charts) tıklayarak **ölçümleri (Önizleme)** sekmesi.
8. Bir kaynak seçmenizden sonra kullanılabilen tüm ölçümler dikey pencerenin sol tarafında görünür. Ölçümleri seçip grafik türü ile saat aralığını değiştirerek birden fazla ölçümün grafiğini tek seferde oluşturabilirsiniz. Ayrıca bu kaynak üzerinde oluşturulmuş tüm ölçüm uyarılarını görüntüleyebilirsiniz.

    ![Ölçüm dikey penceresi](./media/monitoring-get-started/monitor-metric-blade.png)

   > [!NOTE]
   > Bazı ölçümler yalnızca kaynağınızda [Application Insights](../application-insights/app-insights-overview.md) ve/veya Windows ya da Linux Azure Tanılama etkinleştirilerek kullanılabilir.
   >
   >
9. Grafiğiniz hazır olduğunda **Sabitle** düğmesini kullanarak grafiği panoya sabitleyebilirsiniz.
10. **İzleyici** dikey penceresine geri dönüp **Tanılama günlükleri**’ne tıklayın.

    ![Tanılama günlükleri dikey penceresi](./media/monitoring-get-started/monitor-diaglogs-blade.png)

    [**Tanılama günlükleri**](monitoring-overview-of-diagnostic-logs.md), kendi çalışması hakkında veriler sağlayan belirli bir kaynak *tarafından* gösterilen günlüklerdir. Örneğin, Ağ Güvenliği Grup Kuralı Sayaçları ve Mantıksal Uygulama İş Akışı Günlükleri, tanılama günlüğü türleridir. Bu günlükler bir depolama hesabına depolanabilir, Event Hub’da yayınlanabilir ve/veya [Log Analytics](../log-analytics/log-analytics-overview.md)’e gönderilebilir. Log Analytics, Microsoft'un gelişmiş arama ve uyarı vermeye yönelik işletimsel bilgi ürünüdür.

    Portalda, aboneliğinizdeki tüm kaynakların listesini görüntüleyebilir ve tanılama günlüklerinin etkin olup olmadığını belirlemek üzere bu listeyi filtreleyebilirsiniz.
11. Tanılama günlükleri dikey penceresinde bir kaynağa tıklayın. Tanılama günlükleriniz bir depolama hesabına kaydediliyorsa doğrudan indirebileceğiniz saatlik günlüklerin bir listesini görürsünüz.

    ![Bir kaynağın tanılama günlükleri](./media/monitoring-get-started/monitor-diaglogs-detail.png)

    Bir depolama hesabına arşivleme, Event Hubs’da yayınlama veya Log Analytics çalışma alanına gönderme amacıyla ayarlarınızı düzenlemek veya değiştirmek için **Tanılama Ayarları**’na da tıklayabilirsiniz.

    ![Tanılama günlüklerini etkinleştirme](./media/monitoring-get-started/monitor-diaglogs-enable.png)

    Log Analytics için tanılama günlüklerini ayarladıysanız bu tanılama günlüklerini portalın **Günlük arama** bölümünde arayabilirsiniz.
12. İzleyici dikey penceresinin **Uyarılar** bölümüne gidin.

    ![genel kullanıma yönelik uyarılar dikey penceresi](./media/monitoring-get-started/monitor-alerts-nopp.png)

    Burada Azure kaynaklarınıza ilişkin tüm [**uyarıları**](monitoring-overview-alerts.md) yönetebilirsiniz. Bu ölçümleri, etkinlik günlüğü olaylarını, Application Insights web testleri (konumlara) ve Application Insights öngörülü tanılama uyarılarını içerir. Uyarılar bir e-posta gönderilmesini veya bir web kancası URL’sine HTTP POST işlemi yapılmasını tetikleyebilir.
13. Uyarı oluşturmak için **Ölçüm uyarısı ekle**’ye tıklayın.

    ![ölçüm uyarısı ekleme](./media/monitoring-get-started/monitor-alerts-add.png)

    Bundan sonra uyarının durumunu dilediğiniz zaman kolayca görmek için uyarıyı panonuza sabitleyebilirsiniz.

    Ayrıca Azure İzleyici artık sahiptir [ **yakın gerçek zamanlı ölçüm uyarıları**](https://aka.ms/azuremonitor/near-real-time-alerts)(Önizleme) sıklığı her dakika kadar düşük yapılamıyor!
    
14. İzleyici bölümünde [Application Insights](../application-insights/app-insights-overview.md) uygulamaları ve [Log Analytics](../log-analytics/log-analytics-overview.md) yönetim çözümleriyle ilgili bağlantılar da bulunur. Bu diğer Microsoft ürünleri, Azure İzleyici ile kapsamlı tümleştirmeye sahiptir.
15. Application Insights veya Log Analytics kullanmıyorsanız Azure İzleyici mevcut izleme, günlüğe kaydetme ve uyarı verme ürünleriyle bir ortaklığa sahip olabilir. Tam liste ve tümleştirme yönergeleri için [ortaklar sayfamıza](monitoring-partners.md) bakın.

Aşağıdaki adımları izleyerek ve tüm ilgili kutucukları panoya sabitleyerek uygulamanızın ve altyapınızın aşağıdaki gibi kapsamlı görünümlerini oluşturabilirsiniz:

![Azure İzleyici panosu](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure İzleyici’ye Genel Bakış](monitoring-overview.md) makalesini okuyun

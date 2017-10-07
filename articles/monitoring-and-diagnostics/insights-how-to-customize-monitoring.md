---
title: "Microsoft Azure ölçümlerini aaaOverview | Microsoft Docs"
description: "Azure'da toocustomize izleme nasıl grafikleri öğrenin."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure ölçümlerini genel bakış
Tüm Azure hizmetlerini toomonitor hello sistem durumu, performans, kullanılabilirlik ve hizmetlerinizi kullanımını izin anahtar ölçümleri izleyin. Bu ölçümler hello Azure portalında görebilir ve bu hello de kullanabilirsiniz [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello kümesini ölçümleri programlamayla.

Bazı hizmetler için hiçbir ölçümleri sipariş toosee tanılamada üzerinde tooturn gerekebilir. Sanal makineleri gibi başkalarının ölçümleri temel bir dizi alırsınız, ancak tooenable tamamını yüksek sıklıkta ölçümleri hello. Bkz: [izleme ve tanılama](insights-how-to-use-diagnostics.md) toolearn daha fazla.

## <a name="using-monitoring-charts"></a>İzleme grafikleri kullanma
Merhaba ölçümleri hiçbirini grafik seçtiğiniz herhangi bir süre boyunca onları.

1. Merhaba, [Azure Portal](https://portal.azure.com/), tıklatın **Gözat**, ve ardından kaynak izleme İlgilendiğiniz.
2. Merhaba **izleme** bölüm her Azure kaynağı için en önemli ölçümleri hello içerir. Örneğin, bir web uygulaması sahip **istekleri ve hataları**, burada bir sanal makine yaptığınız gibi **CPU yüzdesi** ve **Disk okuma ve yazma**: ![izleme Mercek](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Tüm grafik tıklatıldığında gösterir, hello **ölçüm** dikey. Merhaba dikey penceresinde, ayrıca toohello, grafiktir toplamalar hello ölçümleri (örneğin, ortalama, minimum ve maksimum seçtiğiniz hello zaman aralığı içinde) gösteren bir tablo. Hello hello kaynak için uyarı kuralları olan.
    ![Ölçüm dikey penceresi](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. görünen toocustomize hello satırları tıklatın hello **Düzenle** düğmesine hello grafikte veya hello **grafiği Düzenle** hello ölçüm dikey penceresi komutunu.
5. Merhaba Sorgu Düzenle dikey penceresinde üç şeyler yapabilir:
   
   * Merhaba zaman aralığını değiştirme
   * Merhaba görünümü arasında geçiş çubuğu ve satırı
   * Farklı metics seçin ![Sorgu Düzenle](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Merhaba zaman aralığını değiştirmek, farklı bir aralık seçmek kadar kolay (gibi **son bir saat**) tıklayıp **kaydetmek** hello dikey penceresinde hello sonundaki. Ayrıca seçebilirsiniz **özel**, olanak sağlayan toochoose tüm süre hello son 2 hafta. Örneğin, tüm iki hafta veya yalnızca 1 saat dün hello görebilirsiniz. Merhaba metin kutusu tooenter farklı bir tür saat.
    ![Özel zaman aralığı](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Merhaba zaman aralığını altına, kanal ölçümleri tooshow hello grafik herhangi bir sayıda seçin.
8. Kaydet tıklattığınızda değişikliklerinizi belirli bu kaynak için kaydedilir. Örneğin, iki sanal makineye sahip bir grafikte değiştirirseniz, bu hello diğer etkilemez.

## <a name="creating-side-by-side-charts"></a>Yan yana grafikleri oluşturma
Merhaba güçlü özelleştirme hello portalında ile istediğiniz sayıda grafikleri ekleyebilirsiniz.

1. Merhaba, **...**  hello dikey penceresinde hello üstündeki menü **eklemek döşeme**:  
    ![Menü ekleme](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Daha sonra Seç hello bir grafik seçin **galeri** ekranınızın sağ tarafında hello: ![Galerisi](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. İstediğiniz hello ölçüm görmüyorsanız, her zaman birini ekleyebileceğiniz hello ölçümleri, önceden ve **Düzenle** ihtiyacınız grafik tooshow hello ölçüm hello.

## <a name="monitoring-usage-quotas"></a>Kullanım kotalarını izleme
Kullanım kotalarını gibi belirli veri bir eşik zaman içinde nokta bilgileriyle olan ancak çoğu ölçümleri zamanla eğilimlerini gösterir.

Merhaba dikey kotaları sahip kaynaklar için kullanım kotalarını de görebilirsiniz:

![Kullanım](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Ölçümleri ile Merhaba kullanabileceğiniz gibi [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello kümesini kullanım kotalarını programlı olarak.

## <a name="next-steps"></a>Sonraki adımlar
* [Uyarı Bildirimleri Alma](insights-receive-alert-notifications.md) her bir ölçüm kestiği bir eşiği.
* [İzleme ve tanılama](insights-how-to-use-diagnostics.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.
* [Örnek sayısı otomatik olarak ölçeklendirme](insights-how-to-scale.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
* [Uygulama performansı izleme](../application-insights/app-insights-azure-web-apps.md) tam olarak kodunuzu hello bulutta nasıl gerçekleştiriyor toounderstand istiyorsanız.
* Kullanım [JavaScript uygulamaları ve web sayfaları için Application Insights](../application-insights/app-insights-web-track-usage.md) tooget istemci analytics bir web sayfasını ziyaret hello tarayıcılar hakkında.
* [Kullanılabilirlik ve yanıt hızını herhangi bir web sayfası izleme](../application-insights/app-insights-monitor-web-app-availability.md) , sayfanızın aşağı olup olmadığını öğrenmek için Application Insights ile.


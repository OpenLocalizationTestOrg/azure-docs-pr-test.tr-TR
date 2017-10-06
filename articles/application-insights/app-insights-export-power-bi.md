---
title: Application Insights gelen aaaExport tooPower BI | Microsoft Docs
description: "Power BI'da analiz sorguları görüntülenebilir."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Power BI Application Insights akış
[Power BI](http://www.powerbi.com/) yardımcı iş analiz araçları dizisi verileri çözümlemek ve paylaşmak Öngörüler. Zengin panolar her cihazda kullanılabilir. Analytics sorgularından dahil olmak üzere pek çok kaynaktan veri birleştirebilirsiniz [Azure Application Insights](app-insights-overview.md).

Application Insights veri tooPower BI verme üç önerilen yöntem vardır. Bunları ayrı olarak veya birlikte kullanabilirsiniz.

* [**Power BI bağdaştırıcısı** ](#power-pi-adapter) -uygulamanızdan telemetrinin bir tam Pano ayarlayın. grafikler Hello dizi önceden tanımlanmış ancak kendi sorgularınızı diğer kaynaklardan gelen ekleyebilirsiniz.
* [**Analitik sorguları dışarı** ](#export-analytics-queries) -herhangi bir yazma analizi kullanarak istediğiniz ve tooPower BI verme sorgu. Bu sorgu, diğer verilerin bir Panoda yerleştirebilirsiniz.
* [**Sürekli dışarı aktarma ve akış analizi** ](app-insights-export-stream-analytics.md) -bu yukarı daha fazla iş tooset içerir. Uzun süre boyunca, verilerinizi tookeep istiyorsanız kullanışlıdır. Aksi takdirde hello diğer yöntemleri önerilir.

## <a name="power-bi-adapter"></a>Power BI bağdaştırıcısı
Bu yöntem telemetri tam bir Pano oluşturur. Merhaba ilk veri kümesi önceden, ancak daha fazla veri tooit ekleyebilirsiniz.

### <a name="get-hello-adapter"></a>Merhaba bağdaştırıcısı Al
1. Çok oturum[Power BI](https://app.powerbi.com/).
2. Açık **veri alma**, **Hizmetleri**, **Application Insights**
   
    ![Application Insights veri kaynağından veri alın](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Application Insights kaynağınıza Hello ayrıntılarını sağlayın.
   
    ![Application Insights veri kaynağından veri alın](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Bir veya iki içeri hello veri toobe için dakika bekleyin.
   
    ![Power BI bağdaştırıcısı](./media/app-insights-export-power-bi/010.png)

Merhaba Application Insights grafikleri olanla diğer kaynakları ve analiz sorguları birleştirme hello panoyu düzenleyebilirsiniz. Burada, daha fazla grafik alabilirsiniz ve her bir grafik ayarlayabileceğiniz bir parametre yok görselleştirme galeri yoktur.

Merhaba sonra ilk alma, hello Pano ve hello raporları tooupdate günlük devam eder. Merhaba Yenileme zamanlaması hello veri kümesi üzerinde kontrol edebilirsiniz.

## <a name="export-analytics-queries"></a>Analitik sorguları dışarı aktarma
Bu yol toowrite sağlayan herhangi Analytics sorgu ister ve bu tooa Power BI panosuna dışarı aktarma. (Merhaba bağdaştırıcısı tarafından oluşturulan toohello Panoda ekleyebilirsiniz.)

### <a name="one-time-install-power-bi-desktop"></a>Bir kez: Power BI Desktop yükleyin
tooimport Application Insights sorgunuzu hello Power BI Masaüstü sürümünü kullanın. Ancak daha sonra onu toohello web veya tooyour Power BI bulut çalışma yayımlayabilirsiniz. 

Yükleme [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Analytics sorgusu dışarı aktarma
1. [Analytics açın ve sorgunuzu yazma](app-insights-analytics-tour.md).
2. Test ve hello Sonuçlardan memnun kaldıysanız kadar hello sorgu daraltın.

   **Merhaba sorgulayan çalıştırır doğru önce analytics'te dışa emin olun.**
3. Merhaba üzerinde **verme** menüsünde seçin **Power BI (M)**. Merhaba metin dosyasını kaydedin.
   
    ![Power BI sorgu verme](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. Power BI Desktop seçin **Veri Al, boş sorgu** ve hello Düzenleyicisi altında sorgu **Görünüm** seçin **Gelişmiş sorgu düzenleyici**.

    İçine yapıştırma dışarı hello M Dil komut dosyası hello Gelişmiş Sorgu Düzenleyici.

    ![Gelişmiş Sorgu Düzenleyici](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Tooprovide kimlik bilgileri tooallow Power BI tooaccess Azure olabilir. Microsoft hesabınızla 'kuruluş hesabı' toosign kullanın.
   
    ![Application Insights sorgunuzu Azure kimlik tooenable Power BI toorun sağlayın](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Tooverify hello kimlik bilgileri gerekiyorsa, hello veri kaynağı ayarları menü komutu hello sorgu Düzenleyicisi'ni kullanın. Power BI için kimlik bilgilerinizi farklı olabilir Azure için kullandığınız toospecify hello kimlik özen.)
2. Sorgunuz için bir görsel öğe seçin ve x ekseni, y ekseni ve boyut kesimlere hello alanları seçin.
   
    ![Görselleştirme seçin](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Rapor tooyour Power BI bulut alanınıza yayımlayın. Buradan, eşitlenen sürüm diğer web sayfalarına eklenebilir.
   
    ![Görselleştirme seçin](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Merhaba rapor aralıklarla el ile yenileme veya zamanlanan yenileme hello seçenekleri sayfasında ayarlayın.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="401-or-403-unauthorized"></a>401 veya 403 yetkisiz 
Refesh belirtecinizi güncelleştirilmez bu durum meydana gelebilir. Bu adımları tooensure hala erişiminiz deneyin. Erişiminiz ve refershing hello kimlik bilgileri çalışmıyor, Lütfen bir destek bileti açın.

1. Azure Portal Hello oturum ve hello kaynak erişebildiğinden emin olun
2. Merhaba Pano toorefresh hello kimlik bilgilerini deneyin

### <a name="502-bad-gateway"></a>502 hatalı ağ geçidi
Bunun nedeni genellikle çok fazla veri döndüren bir Analytics sorgusu. Küçük bir zaman aralığı kullanarak denemelisiniz veya hello kullanarak [önce](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) veya [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) yalnızca işlevleri [proje](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello gereksinim alanları.

Merhaba Analytics sorgusundan gelen hello dataset azaltma gereksinimlerinizi karşılamıyorsa hello kullanmayı düşünmelisiniz [API](https://dev.applicationinsights.io/documentation/overview) toopull daha büyük bir veri kümesi. Burada, tooconvert hello M sorgu toouse hello API nasıl dışarı aktarma yönergeleri verilmiştir.

1. Oluşturma bir [API anahtarı](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Güncelleştirme hello değiştirerek Analytics'ten dışarı Power BI M betik ARM URL AI API ile Merhaba (aşağıdaki örneğe bakın)
   * Değiştir **https://management.azure.com/subscriptions/...**
   * ile **https://api.applicationinsights.io/beta/apps/...**
3. Son olarak, kimlik bilgileri toobasic güncelleştirin ve API anahtarınızı kullanın
  

**Varolan komut dosyası**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Güncelleştirilmiş bir komut dosyası**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Örnekleme hakkında
Uygulamanız çok miktarda veri gönderiyorsa hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin. Merhaba, el ile örnekleme hello SDK veya alım ayarladıysanız doğru aynıdır. [Örnekleme hakkında daha fazla bilgi edinin.](app-insights-sampling.md)


## <a name="next-steps"></a>Sonraki adımlar
* [Power BI - öğrenin](http://www.powerbi.com/learning/)
* [Analytics Öğreticisi](app-insights-analytics-tour.md)


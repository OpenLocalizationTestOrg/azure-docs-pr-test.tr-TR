---
title: "araç sağlık ve yürüten aaaPower BI panosuna alışkanlıklarınıza - Azure | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Araç telemetri analizi çözüm şablon Power BI panosuna kurulum yönergeleri
Bu **menü** bu playbook toohello bölümlerde bağlar. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Merhaba araç Telemetri analiz çözümü araba dealerships, otomobil üreticileri ve sigorta şirketler araç sistem durumu ve yürüten Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler hello özelliklerini nasıl yararlanabilir genişletilebileceğini gösterir. R & D ve pazarlama kampanyaları hello alanında alışkanlıklarınıza toodrive geliştirmeleri müşteri deneyimi. Bu belge hello çözüm aboneliğinizde dağıtıldıktan sonra hello Power BI raporları ve panoyu nasıl yapılandırabileceğiniz adım adım yönergeler içerir. 

## <a name="prerequisites"></a>Ön koşullar
1. Merhaba dağıtmak [Telemetri analizi](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) çözümü  
2. [Microsoft Power BI Desktop yükleyin](http://www.microsoft.com/download/details.aspx?id=45331)
3. Bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/). Bir Azure aboneliğiniz yoksa, ücretsiz Azure aboneliği ile çalışmaya başlama
4. Microsoft Power BI hesabı

## <a name="cortana-intelligence-suite-components"></a>Cortana Intelligence Suite bileşenleri
Merhaba araç Telemetri analizi çözüm şablonu bir parçası olarak, aboneliğinizde Cortana Intelligence Hizmetleri aşağıdaki hello dağıtılır.

* **Olay hub'ı** Azure'da araç telemetri olayları milyonlarca alma için.
* **Akış analizi** araç sistem üzerinde gerçek zamanlı Öngörüler öğrenilmesi ve bu verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.
* **Machine Learning** anomali algılama gerçek zamanlı ve toplu toogain Tahmine dayalı Öngörüler işleme.
* **Hdınsight** ölçekte çevrelerini tootransform veriler
* **Veri Fabrikası** planlama, kaynak yönetimi ve izleme hello toplu işleme ardışık orchestration işler.

**Power BI** gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano bu çözümü sunar. 

Merhaba çözümü kullanan iki farklı veri kaynakları: **benzetimli araç sinyalleri ve tanılama veri kümesi** ve **araç katalog**.

Bir araç telematik simulator bu çözümün bir parçası olarak dahil edilir. Tanılama bilgisi yayar ve hello araç ve belirli bir noktada yönlendirmeli düzeni karşılık gelen toohello durumunu zamanında işaret eder. 

Merhaba araç katalog bir başvuru veri kümesi içeren Toplamıdır toomodel eşlemedir

## <a name="power-bi-dashboard-preparation"></a>Power BI panosuna hazırlama
### <a name="setup-power-bi-real-time-dashboard"></a>Kurulum Power BI gerçek zamanlı Panosu

**Merhaba gerçek zamanlı Pano uygulaması başlangıç** hello dağıtım tamamlandıktan sonra hello el ile işlem yönergeleri izlemelisiniz.

* Gerçek zamanlı Pano uygulaması RealtimeDashboardApp.zip indirin ve onu sıkıştırmasını açın.
*  Merhaba sıkıştırması açılmış klasöründe, uygulama yapılandırma dosyası 'RealtimeDashboardApp.exe.config' Değiştir appSettings Eventhub, Blob Storage ve ML hizmet bağlantıları hello değerlerle hello el ile işlem yönergeleri ve değişikliklerinizi kaydetmek için açın.
* Uygulama RealtimeDashboardApp.exe çalıştırın. Bir oturum açma penceresi açılır, geçerli Powerbı kimlik bilgilerinizi sağlayın ve hello tıklatın **kabul** düğmesi. Merhaba uygulama toorun sonra başlar.

   ![Oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI panosuna izinleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Oturum açma tooPowerBI Web sitesine gidin ve gerçek zamanlı bir pano oluşturun.

Şimdi, hazır tooconfigure hello Power BI panosuna gerçek zamanlı zengin Görselleştirmelerini toogain sahip olduğunuz ve Tahmine dayalı Öngörüler araç sistem durumu ve yürüten alışkanlıklarınıza. Tüm hello raporları ve hello Pano yapılandırma tooan saat toocreate yaklaşık 45 dakika sürer. 

### <a name="configure-power-bi-reports"></a>Power BI raporları yapılandırın
Merhaba gerçek zamanlı raporlar ve hello Pano 30-45 dakika toocomplete hakkında alın. Çok Gözat[http://powerbi.com](http://powerbi.com) ve oturum açma.

![Oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Yeni bir veri kümesi Power BI'da oluşturulur. Merhaba tıklatın **ConnectedCarsRealtime** veri kümesi.

![Bağlı eçildiğindeki araba gerçek zamanlı veri kümesi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Boş bir rapor Hello kullanarak Kaydet **Ctrl + s**.

![Boş raporu kaydedin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Rapor adı sağlayın *araç Telemetri analizi gerçek zamanlı - raporları*.

![Rapor adı belirtin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Gerçek zamanlı raporları
Bu çözümde üç gerçek zamanlı raporları vardır:

1. İşlemde araçları
2. Bakım gerektiren araçları
3. Araçlar sağlık istatistikleri

Tüm hello üç gerçek zamanlı raporları tooconfigure seçin veya sonra herhangi bir aşama durdurup hello toplu raporları yapılandırma toohello sonraki bölüme geçin. Tüm toocreate öneririz hello üç toovisualize hello tam Öngörüler hello çözümün hello gerçek zamanlı yolunun bildirir.  

### <a name="1-vehicles-in-operation"></a>1. İşlemde araçları
Çift **sayfa 1** ve çok yeniden adlandırma "Taşıtlardan işleminde"  
    ![Araba - bağlı Taşıtlardan işleminde](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Seçin **toplamıdır** alanının **alanları** ve görselleştirme türü olarak seçin **"Kart"**.  

Kart görselleştirme şekilde gösterildiği gibi oluşturulur.  
    ![Bağlı araba - Select toplamıdır](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **Şehir** ve **toplamıdır** alanlarından. Görselleştirme çok değiştirme**"Harita"**. Sürükleme **toplamıdır** değerleri alanında. Sürükleme **Şehir** alanlarından çok**gösterge** alanı.   
    ![Araba - kart görselleştirme bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Seçin **biçimi** konusundaki **görselleştirmeleri**, tıklatın **başlık** hello değiştirip **metin** çok**"araçları işlem şehre göre"**.  
    ![Araba - bağlı Taşıtlardan işlemde şehre göre](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

Son görselleştirme şekilde gösterildiği gibi görünüyor.    
    ![Bağlı araba - son Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **Şehir** ve **toplamıdır**, görselleştirme türünü çok değiştirme**kümelenmiş sütun grafiği**. Sağlamak **Şehir** alanındaki **eksen alanı** ve **toplamıdır** içinde **alan değeri**  

Sıralama grafik tarafından **"Toplamıdır sayısı"**  
    ![Bağlı araba - toplamıdır sayısı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Değişiklik grafik **başlık** çok**"Araçlar işlemde şehre göre"**  

Merhaba tıklatın **biçimi** bölümünde sonra seçin **veri renkleri**, hello'ı tıklatın **"Açık"** çok**Tümünü Göster**  
    ![Bağlı araba - tüm veri renkleri göster](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Renk simgesine tıklayarak tek tek Şehir Hello rengini değiştirin.  
    ![Araba - değişiklik renkleri bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **kümelenmiş sütun grafiği** görselleştirmeleri, gelen görselleştirme sürükleyin **Şehir** alanındaki **eksen** alanı **modeli** içinde **gösterge** alan ve **toplamıdır** içinde **değeri** alanı.  
    ![Bağlı araba - kümelenmiş sütun grafiği](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Bağlı araba - işleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Bu sayfadaki tüm görselleştirme şekilde gösterildiği gibi yeniden düzenleyin.  
    ![Bağlı araba - görselleştirmeleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Merhaba "Araçlar işleminde" gerçek zamanlı rapor başarıyla yapılandırdınız. Toocreate hello sonraki gerçek zamanlı rapora devam veya buraya durdurun ve hello Pano yapılandırın. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Bakım gerektiren araçları
Tıklatın ![Ekle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd yeni bir rapor çok yeniden adlandırma**"Taşıtlardan gerektiren bakım"**

![Bağlı araba - bakım gerektiren araçları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Seçin **toplamıdır** alan ve görselleştirme türünü çok değiştirmek**kartı**.  
    ![Bağlı araba - toplamıdır kartı Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Biz hello kümesinde "MaintenanceLabel" adlı bir alana sahip. Bu alan "0" veya "1" değeri olabilir." Çözümün bir parçası sağlandı ve hello gerçek zamanlı yolu ile tümleşik hello Azure Machine Learning modeli tarafından ayarlanır. bir araç bakım gerektirir "1" Merhaba değeri gösterir. 

tooadd bir **sayfa düzeyi** bakım gerektiren taşıtlardan verileri göstermek için filtre: 

1. Sürükleme hello **"MaintenanceLabel"** içine alan **sayfa düzeyi filtrelerini**.  
   ![Bağlı araba - sayfa düzeyi filtreleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Tıklatın **temel filtreleme** menü MaintenanceLabel sayfa düzeyi filtresi altındaki mevcut.  
   ![Araba - bağlı temel filtreleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Filtre değeri çok ayarlamak**"1"**    
   ![Bağlı araba - filtre değeri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **kümelenmiş sütun grafiği** görselleştirmeleri gelen  
![Bağlı araba - Vind kartı Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Bağlı araba - kümelenmiş sütun grafiği](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Sürükleme alan **modeli** içine **eksen** alanı **toplamıdır** çok**değeri** alanı. Görselleştirme tarafından sıralama **toplamıdır sayısı**.  Değişiklik grafik **başlık** çok**"modeli tarafından bakım gerektiren Taşıtlardan"**  

Sürükleme **toplamıdır** içine alanları **doygunluğu** adresindeki mevcut **alanları** ![alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) bölümünü **görselleştirme** sekmesi  
![Bağlı araba - doygunluğu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Değişiklik **veri renkleri** görselleştirmeleri içinde **biçimi** bölümü  
Minimum rengini: **F2C812**  
Maksimum rengini: **FF6300**  
![Araba - renk değişiklikleri bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Yeni görselleştirme renkleri araba - bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **kümelenmiş sütun grafiği** görselleştirmeleri sürükleyin **toplamıdır** içine alan **değeri** alanında, sürükle **Şehir** içine alan **eksen** alanı. Sıralama grafik tarafından **"Toplamıdır sayısı"**. Değişiklik grafik **başlık** çok**"şehre göre bakım gerektiren Taşıtlardan"**   
![Bağlı araba - şehre göre bakım gerektiren araçları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Seçin **çok satır kartı** görselleştirmeleri, gelen görselleştirme sürükleyin **modeli** ve **toplamıdır** hello içine **alanları** alanı.  
![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Tüm hello görselleştirme yeniden düzenleme, hello son raporu şu şekilde görünür:  
![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Merhaba "Taşıtlardan gerektiren bakım" gerçek zamanlı rapor başarıyla yapılandırdınız. Toocreate hello sonraki gerçek zamanlı rapora devam veya buraya durdurun ve hello Pano yapılandırın. 

### <a name="3-vehicles-health-statistics"></a>3. Araçlar sağlık istatistikleri
Tıklatın ![Ekle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd yeni rapor, çok yeniden adlandırma**"Taşıtlardan sağlık İstatistikleri"**  

Seçin **ölçer** görselleştirme görselleştirmeleri, öğesinden sonra hello sürükleyin **hızı** içine alan **değeri Minimum, maksimum değer** alanları.  
![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Değiştirme hello varsayılan toplama, **hızı** içinde **değeri alanı** çok**ortalama** 

Değiştirme hello varsayılan toplama, **hızı** içinde **Minimum alan** çok**en az**

Değiştirme hello varsayılan toplama, **hızı** içinde **maksimum alan** çok**maksimum**

![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Merhaba yeniden adlandırma **ölçer başlık** çok**"Ortalama hızı"** 

![Bağlı araba - ölçer](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.  

Benzer şekilde ekleme bir **ölçer** için **ortalama altyapısı Petrol**, **ortalama yakıt**, ve **ortalama altyapısı Sıcaklığın**.  

Değiştirme adımları yukarıda göre her ölçer alanların hello varsayılan toplama **"Ortalama hızı"** ölçer.

![Bağlı araba - ölçerler](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.

Seçin **çizgi ve kümelenmiş sütun grafiği** görselleştirmeleri sonra sürükleyin **Şehir** içine alan **paylaşılan eksen**, sürükleyin **hızı**, **tirepressure ve engineoil alanları** içine **sütun değerlerini** alanı, kendi toplama türü çok değiştirme**ortalama**. 

Sürükleme hello **engineTemperature** içine alan **satır değerleri** alanı hello toplama türü çok değiştirme**ortalama**. 

![Bağlı araba - görselleştirmeleri alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Değişiklik hello grafik **başlık** çok**"Ortalama hızı, lastiği baskısı, altyapısı Petrol ve altyapısı Sıcaklık"**.  

![Bağlı araba - görselleştirmeleri alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.

Seçin **Treemap** görselleştirmeleri, gelen görselleştirme sürükleyin hello **modeli** hello içine alan **grup** alan ve sürükleme hello alan  **MaintenanceProbability** hello içine **değerleri** alanı.

Değişiklik hello grafik **başlık** çok**"araç modelleri bakım gerektiren"**.

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.

Seçin **% 100 Yığılmış grafik** görselleştirme hello sürükleyin **Şehir** hello içine alan **eksen** alan ve sürükleme hello **MaintenanceProbability**, **RecallProbability** hello alanlarına **değeri** alanı.

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Tıklatın **biçimi**seçin **veri renkleri**ve kümesi hello **MaintenanceProbability** renk toohello değeri **"F2C80F"**.

Değişiklik hello **başlık** Merhaba grafik çok**"Olasılık, araç bakım & geri çağırma tarafından Şehir"**.

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.

Seçin **alan grafiği** görselleştirmeleri gelen görselleştirme hello sürükleyin **modeli** hello içine alan **eksen** alan ve sürükleme hello **engineOil, tirepressure, hız ve MaintenanceProbability** hello alanlarına **değerleri** alanı. Toplama tipine çok değiştirme**"Ortalama"**. 

![Bağlı araba - toplama türünü değiştir](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Merhaba grafik Hello başlığını çok değiştirmek**"Ortalama altyapısı petrol, lastiği baskısı, hızlı ve Bakım olasılık modeli tarafından"**.

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Merhaba boş alanı tooadd yeni görselleştirme tıklatın:

1. Seçin **dağılım grafiği** görselleştirme görselleştirmeleri gelen.
2. Sürükleme hello **modeli** hello içine alan **ayrıntıları** ve **gösterge** alanı.
3. Sürükleme hello **yakıt** hello içine alan **x ekseni** alanı hello toplama çok değiştirme**ortalama**.
4. Sürükleme **engineTemparature** içine **y ekseni alanında**, hello toplama çok değiştirmek**ortalama**
5. Sürükleme hello **toplamıdır** hello içine alan **boyutu** alanı.

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Değişiklik hello grafik **başlık** çok**"Yakıt ortalamalar, modeli tarafından altyapısı Sıcaklık"**.

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

Merhaba son rapor aşağıda gösterildiği gibi arar.

![Bağlı araba son raporu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>PIN görselleştirmeleri panosundan hello raporları toohello gerçek zamanlı
Boş bir Pano üzerinde sonraki tooDashboards hello artı simgesine tıklayarak oluşturun. "Araç Telemetri analizi Pano" adı

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

PIN hello görselleştirme raporları toohello Pano yukarıda hello gelen. 

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

Tüm hello üç raporları oluşturulur ve görselleştirmeleri karşılık gelen hello sabitlenmiş toohello Pano olduğunda hello Panosu aşağıdaki gibi görünmelidir. Tüm hello raporları oluşturmadıysanız panonuz farklı görünebilir. 

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Tebrikler! Merhaba gerçek zamanlı Pano başarıyla oluşturdunuz. Tooexecute CarEventGenerator.exe ve RealtimeDashboardApp.exe devam ederken, başlangıç panosunda canlı güncelleştirmeler görmeniz gerekir. Yaklaşık 10 too15 dakika toocomplete hello aşağıdaki adımları gerçekleştirmelisiniz.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Power BI toplu işleme Pano Kurulumu
> [!NOTE]
> Yaklaşık iki saat (Merhaba hello dağıtımının başarılı tamamlama) hello son tooend toplu işleme ardışık düzen toofinish yürütmesi için alır ve üretilen veri yıl tutarında işlem. Bu nedenle toofinish hello sonraki adımlara devam etmeden önce işleme hello bekleyin. 
> 
> 

**Merhaba Power BI Tasarımcısı dosyasını indirin**

* Önceden yapılandırılmış bir Power BI Tasarımcısı dosyasına el ile işlem yönergeleri hello dağıtımının bir parçası olarak dahil edilir
* 2 arayın. Kurulum Powerbı toplu işleme Pano burada adlı toplu işlem Pano için hello Powerbı şablonu yükleyebilir **ConnectedCarsPbiReport.pbix**.
* Yerel olarak Kaydet

**Power BI raporları yapılandırın**

* Açık hello Tasarımcısı dosyasına '**ConnectedCarsPbiReport.pbix**' Power BI Desktop kullanma. Değil zaten varsa yüklerseniz Power BI Desktop'hello [Power BI Desktop yükleme](http://www.microsoft.com/download/details.aspx?id=45331). 
* Merhaba tıklatın **Düzenle sorguları**.

![Power BI Sorgu Düzenle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Merhaba çift **kaynak**.

![Kümesi Power BI kaynağı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Sunucu bağlantı dizesi hello dağıtımının bir parçası sağlanan hello Azure SQL server ile güncelleştirin.  Merhaba el ile işlem yönergeleri altında bakın 

    4. Azure SQL Database
    
    * Sunucu: somethingsrv.database.windows.net
    * Veritabanı: connectedcar
    * Kullanıcı adı: kullanıcı adı
    * Parola: SQL server parolanızı Azure portalından yönetebilirsiniz

* Bırakın **veritabanı** olarak *connectedcar*.

![Set Power BI veritabanı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* **Tamam** düğmesine tıklayın.
* Göreceğiniz **Windows kimlik bilgileri** sekmesi seçili varsayılan olarak, çok değiştirme**veritabanı kimlik bilgileri** tıklayarak **veritabanı** sekmesini sağ.
* Merhaba sağlamak **kullanıcıadı** ve **parola** onun dağıtım kurulumu sırasında belirtilen, Azure SQL veritabanı'nın.

![Veritabanı kimlik bilgileri sağlayın](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Tıklatın **Bağlan**
* Her hello üç kalan sorgu sağ bölmesinde mevcut Hello yukarıdaki adımları yineleyin ve ardından hello veri kaynağı bağlantı ayrıntıları güncelleştirin.
* Tıklatın **kapatın ve yük**. Power BI Desktop dosyası veri kümeleri bağlı tooSQL Azure veritabanı tabloları ' dir.
* **Kapat** Power BI Desktop dosyası.

![Power BI desktop Kapat](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Tıklatın **kaydetmek** düğmesini toosave hello değişiklikleri. 

Artık toohello toplu işleme hello çözüm yolunda karşılık gelen tüm hello raporları yapılandırdınız. 

## <a name="upload-toopowerbicom"></a>Çok karşıya*powerbi.com*
1. Toohello Power BI web portalında http://powerbi.com ve oturum açma gidin.
2. Tıklatın **veri alma**  
3. Merhaba Power BI Desktop dosyası karşıya yükleyin.  
4. tooupload, tıklatın **Veri Al -> dosya alma yerel dosya ->**  
5. Toohello gidin **"**ConnectedCarsPbiReport.pbix**"**  
6. Merhaba dosya yüklendikten sonra geri tooyour gittiğinizde Power BI çalışma alanı olacaktır.  

Bir veri kümesi, rapor ve boş bir Pano sizin için oluşturulur.  

PIN grafikleri tooa yeni pano adlı **araç Telemetri analizi Pano** içinde **Power BI**. Yukarıda oluşturduğunuz hello boş Pano tıklayın ve ardından toohello gidin **raporları** bölümünde hello yeni rapor karşıya.  

![Araç Telemetri güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Not hello rapor altı sayfa vardır:**  
Sayfa 1: Araç yoğunluğu  
Sayfa 2: Gerçek zamanlı araç sistem durumu  
Sayfa 3: Titizlikle Taşıtlardan güdümlü   
Sayfa 4: Geri çekilen araçları  
Sayfa 5: Verimli bir şekilde Taşıtlardan güdümlü yakıt  
Sayfa 6: Contoso logosu  

![Bağlı araba güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Sayfa 3**, hello aşağıdaki PIN:  

1. Toplamıdır sayısı  
   ![Bağlı araba güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Agresif taşıtlardan Waterfall grafik model tarafından yönetilen  
   ![Araç Telemetri - PIN grafikleri 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Sayfa 5**, hello aşağıdaki PIN: 

1. Toplamıdır sayısı    
   ![Araç Telemetri - PIN grafikleri 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Verimli taşıtlardan modeli tarafından Yakıt Al: Kümelenmiş sütun grafiği  
   ![Araç Telemetri - PIN grafik 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Sayfa 4**, hello aşağıdaki PIN:  

1. Toplamıdır sayısı  
   ![Araç Telemetri - PIN grafikleri 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Şehir tarafından geri çekilen taşıtlardan model: Treemap  
   ![Araç Telemetri - PIN grafikleri 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Sayfa 6**, hello aşağıdaki PIN:  

1. Contoso Motors logosu  
   ![Araç Telemetri - PIN grafikleri 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Merhaba Pano düzenleme**  

1. Toohello Pano gidin
2. Her grafiğinin üzerine getirin ve hello tam Pano resimde sağlanan hello adlandırma göre yeniden adlandırın. Ayrıca hello grafikleri toolook hello Panosu aşağıdaki gibi geçici taşıyın.  
   ![Araç Telemetri - Pano 2 düzenleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Araç Telemetri güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Bu belgede belirtildiği gibi tüm hello raporları oluşturduysanız, hello son tamamlanan Panosu aşağıdaki şekilde hello gibi görünmelidir. 

![Araç Telemetri - Pano 2 düzenleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Tebrikler! Merhaba raporları başarıyla oluşturdunuz ve Pano toogain gerçek zamanlı, Tahmine dayalı hello ve toplu işlem ınsights araç sistem durumu ve yürüten alışkanlıklarınıza.  

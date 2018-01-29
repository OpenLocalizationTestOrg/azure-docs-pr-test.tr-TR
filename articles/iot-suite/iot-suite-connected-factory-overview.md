---
title: "Bağlı fabrika bakım çözümüne genel bakış - Azure | Microsoft Docs"
description: "Azure IoT Paketi önceden yapılandırılmış Bağlı fabrika çözümü açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2017
ms.author: dobett
ms.openlocfilehash: bd68859e3837f7e5adbe911518631cb7abc2c2ce
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/12/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a>Önceden yapılandırılmış bağlı fabrika çözümlerini kullanmaya başlama

Azure IoT Paketi [önceden yapılandırılmış çözümleri][lnk-preconfigured-solutions], ortak IoT iş senaryolarını uygulayan uçtan uca çözümler sunmak için birden çok Azure IoT hizmetini birleştirir. Önceden yapılandırılmış *Bağlı fabrika* çözümü endüstriyel cihazlarınıza bağlanır ve cihazları izler. Çözümü kullanarak cihazlarınızdan yapılan veri akışını analiz edebilir, operasyonel verimliliği ve karlılığı artırabilirsiniz.

Bu öğretici, önceden yapılandırılmış Bağlı fabrika çözümünün nasıl hazırlanacağını gösterir. Ayrıca, önceden yapılandırılmış çözümün temel özelliklerinde rehberlik sağlar. Bu özelliklerin birçoğuna önceden yapılandırılmış çözümün bir parçası olarak dağıtılan çözüm *panosundan* erişebilirsiniz:

![Önceden yapılandırılmış bağlı fabrika çözümü panosu][img-cf-home]

Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.

> [!NOTE]
> Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].

## <a name="provision-the-solution"></a>Çözüm sağlama

1. Azure hesabı kimlik bilgilerinizi kullanarak azureiotsuite.com adresinde oturum açın ve çözüm oluşturmak için “**+**” seçeneğine tıklayın.
2. **Bağlı fabrika** kutucuğunda **Seç**’e tıklayın.
3. Önceden yapılandırılmış Bağlı fabrika çözümünüz için bir **Çözüm adı** girin.
4. Çözümü hazırlarken kullanmak istediğiniz **Abonelik** ve **Bölge** seçimini yapın.
5. Hazırlama işlemini başlatmak için **Çözümü Oluştur**'a tıklayın. Bu işlemin çalışması genellikle birkaç dakika sürer.

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a>Hazırlama işleminin tamamlanmasını beklerken

1. Çözümünüzün **Hazırlama** durumuna sahip olan kutucuğuna tıklayın.
2. Azure hizmetleri Azure aboneliğinize dağıtılırken **Hazırlama durumlarına** dikkat edin.
3. Hazırlama tamamlandığında durum **Hazır** olarak değişir.
4. Kutucuğa tıkladığınızda sağ bölmede çözümünüzün ayrıntılarını görürsünüz.

> [!NOTE]
> Önceden yapılandırılmış çözümün dağıtımında sorunlarla karşılaşırsanız bkz. [Azureiotsuite.com sitesindeki izinler][lnk-permissions] ve [Connected factory SSS](iot-suite-faq-cf.md). Sorunlar devam ederse [portalda][lnk-portal] bir hizmet bileti oluşturun.

Görmeyi beklediğiniz ancak çözümünüz için listelenmemiş ayrıntılar mı var? [User Voice](https://feedback.azure.com/forums/321918-azure-iot) sitesinde özellik önerilerinde bulunun.

## <a name="scenario-overview"></a>Senaryoya genel bakış

Önceden yapılandırılmış Bağlı fabrika çözümünü dağıttığınızda, genel bir endüstriyel senaryoyu adım adım görmenize olanak sağlayan kaynaklar ile önceden doldurulur. Bu senaryoda, çözüme bağlı çeşitli fabrikalar genel donanım verimliliğini (OEE) ve ana performans göstergelerini (KPI) hesaplamak için gereken veri değerlerini raporlar. Aşağıdaki bölümlerde şunları nasıl yapacağınız açıklanır:

* Fabrikayı, üretim hatlarını, istasyon OEE ve KPI değerlerini izleme
* Azure Zaman Serisi Görüşlerini kullanarak bu cihazlardan oluşturulan telemetri verilerini analiz etme
* Sorunları gidermek için alarmlara göre işlem yapma

Bu senaryonun temel bir özelliği, çözüm panosu kullanılarak tüm bu eylemlerin uzaktan gerçekleştirilebiliyor olmasıdır. Cihazlara fiziksel erişiminizin olması gerekmez.

## <a name="view-the-solution-dashboard"></a>Çözüm panosunu görüntüleme

Çözüm panosu, dağıtılan çözümü yönetmenizi sağlar. Bu, genel fabrika yapılandırmasının hiyerarşik gösterimidir. Örneğin, OEE ve KPI’leri görüntüleyebilir, telemetri için yeni düğümler yayımlayabilir ve alarmları eyleme dönüştürebilirsiniz.

1. Sağlama tamamlandığında ve önceden yapılandırılmış çözümünüzün kutucuğu **Hazır**’ı gösterdiğinde, Bağlı fabrika çözümü portalınızı yeni bir sekmede açmak için **Başlat**’ı seçin.

    ![Önceden yapılandırılmış çözümü başlatma][img-launch-solution]

1. Varsayılan olarak, çözüm portalı *panoyu* gösterir. Portalın diğer alanlarına gitmek için sayfanın sol tarafındaki menüyü kullanın.

    ![Önceden yapılandırılmış bağlı fabrika çözümü panosu][cf-img-menu]

Pano aşağıdaki bilgileri gösterir:

* Çözümdeki durumu, konumu ve geçerli üretim yapılandırmasını gösteren bir **fabrika konumları** paneli. Çözümü ilk kez çalıştırdığınızda, bir dizi sanal cihaz bulunur. Üretim hattı benzetimi, üretim hattı başına benzetimi yapılan görevleri gerçekleştiren ve verileri paylaşan üç gerçek OPC UA sunucusundan oluşur. OPC UA hakkında daha fazla bilgi için bkz. [Connected factory SSS](iot-suite-faq-cf.md).
* Çözüme bağlı olan her cihazın konumunu görüntüleyen bir **harita**. Çözüm, bilgileri haritaya çizmek için Bing Haritalar API’sini kullanabilir. Aboneliğiniz Bing Haritalar Kurumsal API’si için etkinleştirildiyse, bu özellik otomatik olarak kullanılır. Etkinleştirilmediyse, haritayı nasıl dinamik hale getireceğinizi öğrenmek için [SSS][lnk-faq] bölümüne bakın.
* Telemetri veya OEE/KPI değeri belirli bir eşiği aştığında oluşturulan alarmların gösterildiği **Alarmlar** paneli.
* Kuruluşun tamamı için veya görüntülediğiniz fabrika/üretim hattı/istasyon için OEE değerlerinin gösterildiği **Genel Donanım Verimliliği** paneli. Bu değer, kurumsal düzeyi bulmak için istasyon görünümünden toplanır. OEE şekli ve bu şekli oluşturan öğeler daha fazla analiz edilebilir.
* Kuruluşun tamamında veya görüntülediğiniz fabrika/üretim hattı/istasyonda üretilen birimlerin ve kullanılan enerjinin görüntülendiği **Ana Performans Göstergeleri** paneli. Bu değerler, kurumsal düzeyi bulmak için istasyon görünümünden toplanır.

## <a name="view-factories"></a>Fabrikaları görüntüleme

*Fabrika Konumları* paneli çözümdeki tüm fabrikaların coğrafi konumunu, durumlarını ve geçerli üretim yapılandırmasını gösterir. Konum listesinden, çözüm hiyerarşisindeki diğer düzeylere gidebilirsiniz. Listedeki satırlar, söz konusu konumdaki üretim hatlarının ayrıntılarına bağlanan birer köprüdür. Böylelikle, üretim hattının detaylarına ve istasyon düzeyi görünümüne gitmek mümkün olur. Ayrıca listeye filtre uygulayabilirsiniz.

![Önceden yapılandırılmış bağlı fabrika çözümü fabrikaları][cf-img-factories]

1. **Fabrika paneli**’nde bu çözümün fabrika listesi gösterilir.

2. Fabrika listesi başlangıçta hazırlama işlemi tarafından oluşturulan altı fabrika gösterir. Çözüme başka sanal ve fiziksel cihazlar ekleyebilirsiniz.

3. Fabrikanın ayrıntılarını görüntülemek için fabrika listesindeki satıra tıklayın.

4. Üretim hattının ayrıntılarını görüntülemek için listedeki satıra tıklayın.

5. Üretim hattında bir istasyonun yayımlanmış OPC UA düğümlerini görüntülemek için listedeki satıra tıklayın.

6. İstasyondaki belirli bir düğümün ayrıntılarını görüntülemek için listedeki satıra tıklayın. Bu eylem, Zaman Serisi Görüşleri görselleriyle bağlam panelini başlatır. Zaman Serisi Görüşleri gezgin ortamında daha fazla analiz yapmak için bu grafiklere tıklayın.

## <a name="view-map"></a>Haritayı görüntüleme

Aboneliğinizin Bing Haritalar API’sine erişimi varsa, *Fabrikalar* haritasında size çözümdeki tüm fabrikaların coğrafi konumu ve durumu gösterilir. Konumun detaylarına gitmek için haritada görüntülenen konumlara tıklayın.

![Önceden yapılandırılmış bağlı fabrika çözümü haritası][cf-img-map]

## <a name="view-alarms"></a>Uyarıları görüntüleme

**Alarmlar** panelinde, raporlanan bir değerin veya hesaplanan OEE/KPI değerinin yapılandırılmış eşiği aşmasından dolayı oluşturulan alarmlar gösterilir. Bu panelde, istasyon düzeyi görünümünden genel görünüme kadar her hiyerarşi düzeyindeki alarmlar görüntülenir. Alarmlar, alarmın açıklamasını, tarihini, saatini, konumunu ve tekrarlanma sayısını içerir. Time Series Insights verilerini kullanarak alarma neden olan fikirlerle ilgili görüş sahibi olabilirsiniz. Time Series Insights’ın verileri, uygun olduğunda alarmlarda görselleştirilir. Yöneticiyseniz alarmlar üzerinde şu varsayılan eylemleri gerçekleştirebilirsiniz:

* Alarmı kapatma.
* Alarmı kabul etme.

İsteğe bağlı olarak, daha karmaşık eylemler de gerçekleştirebilirsiniz. Örneğin, Montajın Basınç OPC UA Düğümü için şunları yapabilirsiniz:

* Destek bilgilerini yeni bir tarayıcı penceresinde bir web sayfasında gösterme.
* Cihazda OPC UA metodunu çağırarak alarma olan sorunu giderme.
* Varsayılan eylemlerin kullanılabilirliğini engelleme.

    ![Önceden yapılandırılmış Bağlı fabrika çözümü alarmları][cf-img-alerts]

> [!NOTE]
> Bu alarmlar, önceden yapılandırılmış çözümdeki yapılandırma dosyasında belirtilen kurallar tarafından oluşturulur. Bu kurallar, OEE veya KPI rakamları veya OPC UA Düğüm değerleri yapılandırılmış eşiği aştığında alarmlar oluşturur.

1. **Alarmlar panosunda**, bu çözümde oluşturulan alarmlar gösterilir.

2. Alarmların ayrıntılarını görüntülemek için, alarmlar panelinde alarma tıklayın.

3. Alarm verilerinde daha fazla analiz yapmak için, alarm panelindeki grafiğe tıklayarak Time Series Insights gezgin ortamını açın.

4. Alarmı adreslemek için, alarm panelinde çeşitli eylemler sağlanır. Kendinize uygun seçeneği seçin ve eylemi yürütme komut düğmesine tıklayın.

## <a name="view-overall-equipment-efficiency"></a>Genel donanım verimliliğini görüntüleme

OEE, üretimle ilgili önemli operasyonel parametreleri kullanarak üretim sürecinin verimliliğini derecelendirir. OEE, kullanılabilirlik oranı, performans oranı ve kalite oranının çarpılmasıyla hesaplanan standart bir endüstri ölçümüdür: OEE = kullanılabilirlik x performans x kalite.

![Önceden yapılandırılmış bağlı fabrika çözümü OEE][cf-img-oee]

1. Hiyerarşideki herhangi bir düzeyin OEE ölçümünü görüntülemek için, ihtiyacınız olan görünüme gidin. Söz konusu görünümün OEE’si panelde OEE yüzdesini oluşturan öğelerden her biriyle birlikte görüntülenir.

2. Hiyerarşi verilerinin herhangi bir düzeyinde OEE’de daha fazla analiz yapmak için, OEE, kullanılabilirlik, performans veya kalite yüzdesine tıklayın. Son bir saatin, son 24 saatin ve son 7 günün verilerinin gösterildiği, Zaman Serisi Görüşleri ile desteklenen görselleştirmelerle bir bağlam paneli görüntülenir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI görselleştirmesi][cf-img-tsi-visualization]

3. Alarm verilerini daha fazla çözümlemek için, alarm panelindeki grafiğe tıklayın. Bu eylem Zaman Serisi Görüşleri düzenleyici ortamını açar.

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI gezgini][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Önemli Performans Göstergelerini görüntüleme

Çözüm iki önemli performans göstergesi (*saat başına birim sayısı* ve *kWh cinsinden kullanılan enerji*) sağlar.

![Önceden yapılandırılmış bağlı fabrika çözümü KPI][cf-img-kpi]

1. Hiyerarşideki herhangi bir düzeyin saat başına birim sayısını veya kullanılan enerji miktarını görüntülemek için, ihtiyacınız olan görünüme gidin. Saat başına birim sayısı ve kullanılan enerji miktarı panelde görüntülenir.

2. Hiyerarşinin herhangi bir düzeyinde saat başına birim sayısını ve kullanılan enerji miktarını çözümleyebilmek için, **Önemli Performans Göstergeleri** panelindeki ölçere tıklayın. Son bir saatin, son 24 saatin ve son 7 günün verilerini görebilmenizi sağlayan Zaman Serisi Görüşleri ile desteklenen görselleştirmelerle bir bağlam paneli görüntülenir.

## <a name="scenario-review"></a>Senaryo gözden geçirme

Bu senaryoda, panoda fabrikalarınızın OEE ve KPI değerlerini izlediniz. Ardından, anormallikleri saptayabilmek için OEE ve KPI’lerin telemetri verilerinde daha fazla detaya gitmenize yardımcı olacak daha fazla bilgi sağlamak üzere Zaman Serisi Görüşleri’ni kullandınız. Ayrıca, fabrikalarınızdaki sorunları görüntülemek üzere alarm panosundan yararlandınız ve alarmın sorununu çözmek için size sağlanan eylemleri kullandınız.

## <a name="other-features"></a>Diğer özellikler

Aşağıdaki bölümlerde, Bağlı fabrika çözümünün önceki senaryoda bahsedilmeyen bazı ek özellikleri açıklanmaktadır.

## <a name="apply-filters"></a>Filtreleri uygulama

1. Fabrika konumları veya alarmlar panelinde kullanılabilir filtrelerin listesini görüntülemek için **huni** simgesine tıklayın.

2. Sizin için filtreler paneli görüntülenir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter]

3. Gerek duyduğunuz filtreyi seçin. Filtre alanlarına serbest metin yazmak mümkündür.

4. Ardından filtre sizin için uygulanır. Panoda, fabrikalar ve alarmlar tablolarının içinde görüntülenen bir huni aracılığıyla filtrenin durumu da gösterilir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Etkin bir filtre görüntülenen OEE ve KPI değerlerini etkilemez; yalnızca liste içeriğini filtreler.

5. Filtreyi temizlemek için huniye tıklayın ve filtre bağlam panelinde filtreye tıklayın. Fabrikalar ve alarmlar tablolarında **Tümü** metni görüntülenir.

## <a name="browse-an-opc-ua-server"></a>OPC UA sunucusuna göz atma

Önceden yapılandırılmış çözümü dağıttığınızda, çözüm tarayıcısı üzerinden göz atabileceğiniz sanal OPC UA sunucularını otomatik olarak hazırlarsınız. Bu sunucular, *sanal OPC UA sunucularıdır*. Sanal sunucular herhangi bir gerçek ve fiziksel sunucuya dağıtmaya gerek kalmadan önceden yapılandırılmış çözümü denemenizi kolaylaştırır. Çözüme gerçek bir OPC UA sunucusu bağlamak istemiyorsanız [OPC UA cihazınızı önceden yapılandırılmış Bağlı fabrika çözümüne bağlama][lnk-connect-cf] öğreticisine bakın.

1. Pano gezinti çubuğunda **tarayıcı simgesine** tıklayın.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu tarayıcısı][cf-img-server-browser]

2. Önceden yapılandırılmış listedeki sunuculardan birini seçin. Bu listede, önceden yapılandırılmış çözümde sizin için dağıtılan sunucular gösterilir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu seçimi][cf-img-server-choice]

3. **Bağlan**’a tıklayın; güvenlik iletişim kutusu görüntülenir. Benzetim için, **Devam Et**’e tıklamak güvenlidir

4. Sunucu ağacındaki düğümlerden herhangi birini genişletmek için düğüme tıklayın. Yayımlama telemetrisi olan düğümlerin yanında bir onay işareti vardır.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu ağacı][cf-img-server-tree]

5. Düğümü okumak, yazmak, yayımlamak veya çağırmak için bir öğeye sağ tıklayın. Kullanabileceğiniz eylemler, izinlerinize ve düğümün özniteliklerine bağlıdır. Okuma seçeneği belirli bir düğümün değerini gösteren bağlam panelini görüntüler. Yazma seçeneği yeni değer girebileceğiniz bir bağlam paneli görüntüler. Çağırma seçeneği çağrı için parametreleri girebileceğiniz bir düğüm görüntüler.

## <a name="publish-a-node"></a>Düğümü yayımlama

*Sanal OPC UA sunucusuna* göz attığınızda, yeni düğümleri yayımlamayı da seçebilirsiniz. Çözümde bu düğümlerden gelen telemetriyi analiz edebilirsiniz. Bu *sanal OPC UA sunucuları* gerçek ve fiziksel cihaza dağıtmaya gerek olmadan önceden yapılandırılmış çözümü denemenizi kolaylaştırır.

1. OPC UA sunucusu tarayıcı ağacında yayımlamak istediğiniz düğüme göz atın.

2. Düğüme sağ tıklayın.

3. **Yayımla**’yı seçin.

    ![Bağlı fabrika yayımlama düğümü][cf-img-publish-node]

4. Yayımlama işleminin başarılı olduğunu bildiren bir bağlam paneli görüntülenir. Düğüm, istasyon düzeyi görünümünde yanında bir onay işaretiyle gösterilir.

    ![Önceden yapılandırılmış bağlı fabrika yayımlama başarısı][cf-img-publish-success]

## <a name="command-and-control"></a>Komut ve denetim

Bağlı fabrika, endüstri cihazlarınızı doğrudan buluttan kumanda etmenize ve denetlemenize olanak tanır. Cihaz tarafından oluşturulan alarmları yanıtlamak için bu özelliği kullanabilirsiniz. Örneğin, buluttan cihaza bir komut gönderebilirsiniz. Kullanılabilir komutları, OPC UA sunucuları tarayıcı ağacındaki **StationCommands** düğümünde bulabilirsiniz. Bu senaryoda, Münih’teki üretim hattının montaj istasyonundaki basınç tahliye vanasını açıyorsunuz. Kumanda etme ve denetleme işlevselliğini kullanmak için, önceden yapılandırılmış çözüm dağıtımında **Yönetici** rolünde olmanız gerekir.

1. OPC UA sunucusu tarayıcı düğümünde **StationCommands** düğümüne göz atın.

2. Kullanmak istediğiniz komutu seçin.

3. Düğüme sağ tıklayın.

4. **Çağır**’ı seçin.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağır komutu][cf-img-call-command]

5. Çağırmak üzere olduğunuz yöntem ve uygulanabilecek parametre ayrıntıları hakkında bilgi veren bir bağlam paneli açılır.

6. **Çağır**’ı seçin.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı bağlamı][cf-img-call-context]

7. Bağlam paneli, yöntem çağrısının başarılı olduğunu bildirecek şekilde güncelleştirilir. Çağrı sonucu güncelleştirilen basınç düğümünün değerini okuyarak çağrının başarılı olduğunu doğrulayabilirsiniz.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı başarısı][cf-img-call-success]

## <a name="behind-the-scenes"></a>Arka planda

Önceden yapılandırılmış bir çözümü dağıttığınızda, dağıtım işlemi seçtiğiniz Azure aboneliğinde birden çok kaynak oluşturur. Bu kaynakları Azure [portalında][lnk-portal] görüntüleyebilirsiniz. Dağıtım işlemi, önceden yapılandırılmış çözümünüz için seçtiğiniz adı temel alan bir ada sahip bir **kaynak grubu** oluşturur:

![Azure portalında önceden yapılandırılmış çözüm][img-cf-portal]

Her bir kaynağın ayarlarını, kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.

Önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz. Önceden yapılandırılmış Bağlı fabrika çözümünün kaynak kodu [azure-iot-connected-factory][lnk-cfgithub] GitHub deposundadır:

İşiniz bittiğinde önceden yapılandırılmış çözümü [azureiotsuite.com][lnk-azureiotsuite] sitesindeki Azure aboneliğinizden silebilirsiniz. Bu site, önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm kaynakları kolayca silmenize imkan tanır.

> [!NOTE]
> Önceden yapılandırılmış çözümle ilgili her şeyi sildiğinizden emin olmak için bu öğeleri [azureiotsuite.com][lnk-azureiotsuite] sitesinde silin. Portalda kaynak grubunu silmeyin.

## <a name="next-steps"></a>Sonraki Adımlar

Çalışan bir önceden yapılandırılmış çözüm dağıttığınıza göre aşağıdaki makaleleri okuyarak IoT Paketi ile çalışmaya başlayabilirsiniz:

* [Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]
* [Cihazınızı önceden yapılandırılmış Bağlı fabrika çözümüne bağlama][lnk-connect-cf]
* [azureiotsuite.com sitesindeki izinler][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-v1-permissions.md
[lnk-faq]: iot-suite-v1-faq.md
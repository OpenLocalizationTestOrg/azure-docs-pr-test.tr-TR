---
title: "önceden yapılandırılmış çözüm aaaPredictive bakım | Microsoft Docs"
description: "Hello Azure IOT paketi Tahmine dayalı bakım açıklamasını önceden yapılandırılmış çözümü."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Önceden yapılandırılmış tahmine dayalı bakım çözümüne genel bakış

Merhaba *Tahmine dayalı Bakım* [önceden yapılandırılmış çözüm] [ lnk_preconfigured_solutions] hello biri [Microsoft Azure IOT paketi] [ lnk_iot_suite] önceden yapılandırılmış çözümler. Bu çözüm, gerçek zamanlı cihaz telemetri koleksiyonunu [Azure Machine Learning][lnk-machine-learning] kullanılarak oluşturulan tahmine dayalı modelle tümleştirir.

Azure IOT paketi ile ve hızlı bir şekilde ve kolayca tooand İzleyici varlıklar bağlanmak, gerçek zamanlı panolar ve görselleştirmeleri telemetri analiz edin. Hello Tahmine dayalı bakım çözümü hello panolar ve görselleştirmeleri, verimlilikleri yönetebilen ve gelir akışlarını geliştiren yeni zekaya sahip sağlar.

## <a name="hello-scenario"></a>Merhaba senaryosu

Fabrikam, rekabetçi fiyatlarıyla büyük müşteri deneyimine odaklanan bölgesel bir havayoludur. Uçuş rötarlarının bir nedeni bakım sorunlarıdır ve uçak motorunun bakımı özellikle zordur. Böylece olarak kendi motorları muayene eder ve tooa planı göre bakım zamanlar Fabrikam uçuş sırasında maliyeti, motor arızasından kaçınmalısınız. Ancak, uçak motorları her zaman yıpranmaz aynı hello. Motorlardı bazı gereksiz bakımlar gerçekleştirilir. Daha da önemlisi, bakım yapılana kadar çıkan sorunlar nedeniyle uçağın yerde kalmasıdır. Bir konumda Uçağın olduğunda, burada doğru teknisyenlerin Merhaba veya yedek parçaların kullanılabilir değil, bu sorunları özellikle maliyetli olabilir.

Fabrikam uçağının, Hello motorları, uçuş sırasında motor koşullarını izleyen algılayıcılar ile donatılmıştır. Fabrikam hello Tahmine dayalı bakım çözümü toocollect hello algılayıcı verilerini hello uçuş sırasında toplanan kullanır. Motor çalışması yıllarca biriktirdikten sonra hatası verileri Fabrikam'ın veri bilimcilerine şekilde toopredict hello uçak motorunun kalan kullanım ömrü (RUL) modeli oluşturmuştur. Merhaba modeli dört hello altyapısı algılayıcı verilerinden ve tooeventual hatası müşteri adayları motor yıpranmasıyla ilişkili arasında bir ilişki kullanır. Fabrikam tooperform normal incelemeleri tooensure güvenliği devam ederken, bunu şimdi hello modelleri toocompute hello RUL her motor için her uçuştan sonra kullanabilirsiniz. Merhaba modeli hello motorlarından hello uçuş sırasında toplanan hello telemetri kullanır. Fabrikam artık arızanın ve bakım planının ileri tarihli noktalarını tahmin edebiliyor ve önceden onarıyor.

> [!NOTE]
> Merhaba çözüm modeli asıl motor yıpranması verilerini kullanır.

Bakım gerekli olduğunda hello noktayı tahmin ederek çalışmasını, Fabrikam, işlemleri tooreduce maliyetleri en iyi duruma getirebilirsiniz.

Bakım düzenleyicileri, zamanlayıcılar ile çalışarak:

- Belirli bir konumda Uçağın ile bakım toocoincide planlayın.
- Yeterli zaman bozmadan hello uçak toobe hizmet dışına için kullanılabilir olduğundan emin olun.
- tooschedule teknisyenleri tooensure Uçağın bekleme süresi olmadan verimli bir şekilde sunulur.

Stok denetimi yöneticileri bakım planlarını alır; bu nedenle, sipariş sürecini ve yedek parça stoğunu en iyi hale getirebilirler.

Bu etkinlikler Fabrikam toominimize Uçağın yerdeki süresini etkinleştir ve Yolcuların ve personelin hello güvenliğini sağlarken işletim maliyetlerini azaltabilirsiniz.

toounderstand nasıl [Azure IOT paketi] [ lnk_iot_suite] hello müşterilerin gereksinim toorealize hello olası sağlar Tahmine dayalı bakım bu gözden [bilgi grafiği] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Merhaba Tahmine dayalı bakım çözümü nasıl oluşturulur

Hello çözüm bir var olan Azure Machine Learning modeli IOT paketi hizmetleriyle toplanan cihaz telemetrisi çalışma bu özellikler bir şablon tooshow kullanır. Microsoft'ta bir [regresyon modeli] [ lnk_regression_model] herkese açık verilerine dayalı uçak motorunun<sup>\[1\]</sup>ve adım adım nasıl toouse hello model konusunda yönergeler.

Hello Azure IOT Tahmine dayalı bakım çözümü bu şablondan oluşturulan hello regresyon modeli kullanır. Merhaba modeli Azure aboneliğinize dağıtılır ve otomatik olarak oluşturulan bir API üretir. Merhaba çözüm içeren bir alt kümesini 4 (toplamda 100) temsil eden veri sınama hello motorları ve hello 4 (of toplamda 21) algılayıcı veri akışı. Yeterli tooprovide hello eğitilen model ait doğru sonuç verilerdir.

*\[1\] A. Saxena ve K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set" (Turbofan Motor Bozulması Benzetimi Veri Kümesi), NASA Ames Prognostics Veri Deposu (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Tahmine dayalı bakım ile çalışmaya başlama

Bu öğretici nasıl tooprovision hello Tahmine dayalı bakım çözümü gösterir. Bu ayrıca, hello hello Tahmine dayalı bakım çözümü, temel özellikleri açıklanmaktadır. Bu özelliklerin yanı sıra hello önceden yapılandırılmış çözümü dağıtır hello çözüm Panosu üzerinden erişebilirsiniz.

toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.

> [!NOTE]
> Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].

1. Çok oturum[azureiotsuite.com] [ lnk-azureiotsuite] Azure kullanarak hesap kimlik bilgilerini ve tıklatın  **+**  toocreate bir çözüm.
1. Tıklatın **seçin** hello **Tahmine dayalı Bakım** döşeme.
1. Tahmine dayalı bakım için önceden yapılandırılmış çözümünüze ait bir **Çözüm adı** girin.
1. Select hello **bölge** ve **abonelik** toouse tooprovision hello çözüm istiyorsunuz.
1. Tıklatın **çözümü Oluştur** toobegin hello sağlama işlemi. Bu işlem genellikle birkaç dakika toorun alır.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>İşlem toocomplete sağlama Merhaba bekleyin

1. Çözümünüzle birlikte Hello kutucuğa tıklayın **sağlama** durumu.
1. Bildirim hello **hazırlama durumlarına** gibi Azure Hizmetleri Azure aboneliğinize dağıtılır.
1. Hazırlama tamamlandığında durum değişikliklerini çok hello**hazır**.
1. Merhaba döşeme toosee hello hello sağ bölmede çözümünüzün ayrıntılarını'ı tıklatın. Bu bölmesinden hello çözüm panosu ve erişim hello Machine Learning çalışma alanı başlatabilirsiniz.

> [!NOTE]
> Merhaba önceden yapılandırılmış çözümü dağıtma sorunlarla karşılaşırsanız, gözden [hello azureiotsuite.com sitesindeki izinler] [ lnk-permissions] ve hello [SSS] [ lnk-faq]. Merhaba sorunları devam ederse, bir hizmet bileti hello üzerinde oluşturma [portal][lnk-portal].

Çözümünüz için listelenmeyen toosee beklediğiniz ayrıntılar bulunur? [User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.

## <a name="view-hello-solution"></a>Merhaba çözümü görüntüle

Bu bölümde, hello çözümü kullanıcı Arabirimi aracılığıyla size yol gösterir.

### <a name="predictive-maintenance-dashboard"></a>Tahmine Dayalı Bakım Panosu

Merhaba web uygulamasındaki bu sayfa Powerbı JavaScript denetimlerini kullanır (Merhaba bkz [Powerbı-visuals repository][lnk-powerbi]) toovisualize:

* blob depolama hello Stream Analytics işlerine Hello çıktı verileri.
* Merhaba RUL ve döngüsü uçak motoru başına sayısı.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Merhaba hello bulut çözümünün davranışını Gözlemleme

İçinde Azure portal Merhaba, toohello kaynak grubuna gidin hello çözüm adı ile hazırlanan kaynaklarınızı tooview seçtiniz.

![][img-resource-group]

Merhaba önceden yapılandırılmış çözümü hazırlarken, bir bağlantı toohello Machine Learning çalışma alanı içeren bir e-posta alırsınız. Merhaba toohello Machine Learning çalışma alanına da gidebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] sağlanan çözümünüz için sayfa. Merhaba çözüm hello olduğunda bir kutucuğu bu sayfada kullanılabilir **hazır** durumu.

![][img-machine-learning]

Merhaba çözüm portalında hello örneği iki motorları her dört algılayıcılar uçak başına ile dört sanal cihaz toorepresent iki uçak ile sağlandığında görebilirsiniz. Toohello çözüm portalına ilk gittiğinizde hello benzetim durdurulur.

![][img-simulation-stopped]

Tıklatın **benzetimi Başlat** toobegin hello benzetimi. Merhaba algılayıcı geçmişi, RUL, döngüler ve RUL geçmişini doldurmak hello Pano.

![][img-simulation-running]

RUL değeri 160 altındaysa (gösterim amaçlı seçilen rastgele eşik) olduğunda hello çözüm portalı RUL görüntülemek bir uyarı simgesi sonraki bir toohello görüntüler. Merhaba çözüm portalı da hello uçak motorunu sarı vurgular. Nasıl hello RUL değerleri bir genel düşüş eğilimi dikkat edin, ancak toobounce yukarı ve aşağı eğilimindedir. Bu davranış hello değişen döngü uzunlukları ve hello model doğruluğundan sonuçlanır.

![][img-simulation-warning]

Merhaba tam benzetim, 148 Döngüyü yaklaşık 35 dakika toocomplete alır. Merhaba 160 RUL eşiği ilk seferinde yaklaşık 5 dakika Merhaba karşılanır ve her iki motor hello eşiğine yaklaşık 8 dakikada vardı.

Merhaba benzetim 148 döngü için hello tam veri kümesinde çalışır ve son RUL ve döngü değerlerinde de kapanır.

Merhaba benzetimi herhangi durdurabilirsiniz noktası ancak tıklatarak **benzetimi Başlat** yürütmelerini hello hello dataset hello başından benzetimi.

## <a name="next-steps"></a>Sonraki adımlar

Azure IOT okuma Tahmine dayalı bakım senaryolarını nasıl sağladığı hakkında daha fazla toolearn [hello nesnelerin interneti'nden değer yakalama][lnk_capture_value].

Ele bir [izlenecek] [ lnk-predictive-walkthrough] hello Tahmine dayalı bakım çözümü.

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [IoT Paketi için sık sorulan sorular][lnk-faq]
* [Merhaba IOT güvenlikten plan][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/
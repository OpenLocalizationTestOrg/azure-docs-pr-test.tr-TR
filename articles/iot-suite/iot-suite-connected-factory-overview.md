---
title: "IOT paketi aaaAzure bağlı Fabrika genel bakış | Microsoft Docs"
description: "Hello Azure IOT paketi açıklamasını Fabrika önceden yapılandırılmış çözüm bağlı."
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
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Bağlı hello Fabrika önceden yapılandırılmış çözümü ile çalışmaya başlama

Azure IOT paketi [önceden yapılandırılmış çözümleri] [ lnk-preconfigured-solutions] ortak IOT iş senaryolarını uygulayan birden çok Azure IOT Hizmetleri toodeliver uçtan uca çözümler birleştirin. Merhaba *bağlı Fabrika* önceden yapılandırılmış çözüm endüstriyel aygıtlarınızı tooand izleyiciler bağlanır. Merhaba çözüm tooanalyze hello akış cihazlarınız ve toodrive işletimsel verimliliğini ve Karlılık verilerini kullanabilirsiniz.

Bu öğretici, tooprovision hello Fabrika nasıl bağlanacağını gösterir. önceden yapılandırılmış çözümü. Bu ayrıca, hello aracılığıyla hello önceden yapılandırılmış çözümün temel özellikleri açıklanmaktadır. Bu özelliklerin çoğunu hello çözümden erişebilirsiniz *Pano* hello önceden yapılandırılmış çözümün bir parçası dağıtır:

![önceden yapılandırılmış bağlı fabrika çözümü panosu][img-cf-home]

toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.

> [!NOTE]
> Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Sağlama hello çözümü

1. Azure hesabı kimlik bilgilerinizi kullanarak tooazureiotsuite.com üzerinde oturum öğesini tıklatıp "**+**" toocreate bir çözüm.
2. Tıklatın **seçin** hello üzerinde **bağlı Fabrika** döşeme.
3. Önceden yapılandırılmış bağlı fabrika çözümünüz için bir **Çözüm adı** girin.
4. Select hello **abonelik** ve **bölge** toouse tooprovision hello çözüm istiyorsunuz.
5. Tıklatın **çözümü Oluştur** toobegin hello sağlama işlemi. Bu işlem genellikle birkaç dakika toorun alır.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>İşlem toocomplete sağlama hello için beklerken

1. Çözümünüzle birlikte Hello kutucuğa tıklayın **sağlama** durumu.
2. Bildirim hello **hazırlama durumlarına** gibi Azure Hizmetleri Azure aboneliğinize dağıtılır.
3. Hazırlama tamamlandığında durum değişikliklerini çok hello**hazır**.
4. Merhaba döşeme toosee hello hello sağ bölmede çözümünüzün ayrıntılarını'ı tıklatın.

> [!NOTE]
> Merhaba önceden yapılandırılmış çözümü dağıtma sorunlarla karşılaşırsanız, gözden [hello azureiotsuite.com sitesindeki izinler] [ lnk-permissions] ve hello [bağlı Fabrika SSS](iot-suite-faq-cf.md). Merhaba sorunları devam ederse, bir hizmet bileti hello üzerinde oluşturma [portal][lnk-portal].

Çözümünüz için listelenmeyen toosee beklediğiniz ayrıntılar bulunur? [User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.

## <a name="scenario-overview"></a>Senaryoya genel bakış

Bağlı hello dağıttığınızda Fabrika önceden yapılandırılmış çözüm, bu ortak endüstriyel senaryosu aracılığıyla toostep kaynak ile önceden doldurulmaz. Bu senaryoda, birkaç oluşturucuları bağlı hello veri değerleri gerekli toocompute toohello çözüm raporu genel donanım verimliliği (OEE) ve ana performans göstergelerini (KPI'lar). Merhaba aşağıdaki bölümlerde, nasıl göstermek için:

* Fabrikayı, üretim hatlarını, istasyon OEE ve KPI değerlerini izleme
* Azure zaman serisi Öngörüler kullanarak bu cihazlardan oluşturulan hello telemetri verilerini çözümleme
* Uyarıları toofix sorunları hareket

Bir anahtar, bu senaryo bu eylemleri uzaktan hello çözüm panodan için gerçekleştirebilir özelliğidir. Fiziksel erişim toohello aygıtları gerekmez.

## <a name="view-hello-solution-dashboard"></a>Görünüm hello çözüm Panosu

Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar. Bu, genel fabrika yapılandırmasının hiyerarşik gösterimidir. Örneğin, OEE ve KPI’leri görüntüleyebilir, telemetri için yeni düğümler yayımlayabilir ve uyarıları eyleme dönüştürebilirsiniz.

1. Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen bağlı Fabrika çözümü portalınızı yeni bir sekmede.

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*. toonavigate tooother alanları hello portalının hello sol taraftaki hello sayfasının hello menüsünü kullanın.

    ![Önceden yapılandırılmış bağlı fabrika çözümü panosu][cf-img-menu]

Başlangıç Panosu aşağıdaki bilgilerle hello görüntüler:

* A **Fabrika listesi** hello durumu, konum ve üretim yapılandırmasına hello çözümde gösterir paneli. Merhaba çözümü ilk kez çalıştırdığınızda, çok sayıda sanal cihaz vardır. Merhaba üretim hattı benzetimi sanal görevlerini gerçekleştiren, veri paylaşımı üç gerçek OPC UA sunucularının üretim hattı başına oluşur. Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).
* A **harita** her cihazın görüntüler hello konumu toohello çözüm bağlı. Merhaba çözüm hello haritada hello Bing Haritalar API'si tooplot bilgileri kullanabilirsiniz. Aboneliğiniz Bing Haritalar Kurumsal API’si için etkinleştirildiyse, bu özellik otomatik olarak kullanılır. Değilse, hello bkz [SSS] [ lnk-faq] toolearn nasıl toomake hello harita dinamik.
* Telemetri veya OEE/KPI değeri belirli bir eşiği aştığında oluşturulan uyarıların gösterildiği **Uyarılar** paneli.
* Bir **genel donanım verimliliği** hello tüm kuruluş veya hello Fabrika/üretim hello OEE değerleri satır /, istasyon gösterir görüntüleme paneli. Bu değer hello istasyon görünüm toohello Kurumsal düzeyden toplanır. Merhaba OEE şekil ve bağlı öğeleri daha fazla analiz.
* **Ana performans göstergelerini** üretilen birim ve hello tüm kuruluş veya hello Fabrika/üretim hattı tarafından kullanılan enerji hello sayısını görüntüler /, istasyon paneli görüntülemekte olduğunuz. Bu değerleri istasyon görünüm toohello kuruluş düzeyinde toplanır.

## <a name="view-factories"></a>Fabrikaları görüntüleme

Merhaba *oluşturucuları* panel hello çözüm, durum ve üretim yapılandırmasına tüm hello factory'leri coğrafi konumunu hello gösterir. Merhaba konumları listeden hello çözüm hiyerarşideki diğer düzeyleri toohello gidebilirsiniz. Merhaba satırları hello listesinde hello Üretim satırları bu konumda ayrıntılarını bağlantı köprüleri edilir. Bundan sonra olası toodrill hello üretim satırı ayrıntıları ve toohello istasyon seviye görünümü aşağı olur. Ayrıca, bir filtre toohello listesi uygulayabilirsiniz.

![Önceden yapılandırılmış bağlı fabrika çözümü fabrikaları][cf-img-factories] 

1. Merhaba **Fabrika paneli** hello Bu çözüm için Fabrika listesini gösterir.

2. Merhaba Fabrika liste başlangıçta altı oluşturucuları hello sağlama işlemi tarafından oluşturulan gösterir. Ek sanal ve fiziksel cihaz toohello çözüm ekleyebilirsiniz.

3. bir Fabrika tooview hello ayrıntılarını hello Fabrika listesindeki hello satır'ı tıklatın.

4. bir üretim satırının tooview hello Ayrıntılar hello listesindeki hello satır'ı tıklatın.

5. istasyonu hello üretim satırındaki OPC UA düğümlerinin tooview hello yayımlanan, hello listesinde hello satıra tıklayın.

6. Merhaba istasyon, belirli bir düğümde tooview Ayrıntılar hello listesindeki hello satır'ı tıklatın. Bu eylemin hello bağlam panel zaman serisi Öngörüler görselleştirmeleri ile başlatır. Bu grafik toodo çözümlemeler hello zaman serisi Öngörüler explorer ortamında'ı tıklatın.

## <a name="view-map"></a>Haritayı görüntüleme

Aboneliğinizi erişim toohello Bing Haritalar API'si varsa, hello *oluşturucuları* eşlemesini gösterir, hello coğrafi konumu ve tüm hello oluşturucuları durumunu hello çözümde. Merhaba konum ayrıntıları içine toodrill hello haritada görüntülenmelerini hello konumları'ı tıklatın.

![Önceden yapılandırılmış bağlı fabrika çözümü haritası][cf-img-map]

## <a name="view-alerts"></a>Uyarıları görüntüleme

Merhaba **uyarı** paneli gösterir, son oluşturulan uyarıların tooa bildirilen değer veya yapılandırılmış eşiğini aşan bir hesaplanmış OEE/KPI değeri. Bu panoyu hello hiyerarşiden başlangıç istasyon düzey görünümü toohello genel görünümü her düzeyinde uyarıları görüntüler. Merhaba uyarıları hello uyarı, tarih, saat, konum ve yineleme sayısı açıklamasını içerir. Merhaba zaman serisi istatistik verilerine kullanarak hello uyarıya neden toohello veri öngörü elde edebilirsiniz. Merhaba zaman serisi içindeki veri görselleştirilen Insights uyarıları uygunsa hello. Bir yöneticiyseniz, gibi hello Uyarılardaki varsayılan eylemleri gerçekleştirebilirsiniz:

* Kapat hello uyarı.
* Merhaba uyarı kabul ediyorsunuz.

İsteğe bağlı olarak, daha karmaşık eylemler de gerçekleştirebilirsiniz. Örneğin, Merhaba baskısı OPC UA hello derleme düğümünün, olabilir:

* Destek bilgilerini yeni bir tarayıcı penceresinde bir web sayfasında gösterme.
* Merhaba hello uyarı hello aygıtta bir OPC UA yöntemini çağırarak en aza.
* Merhaba varsayılan eylemleri Hello kullanılabilirliğini engelleyin.

    ![Önceden yapılandırılmış bağlı fabrika çözümü uyarıları][cf-img-alerts]

> [!NOTE]
> Bu uyarılar hello önceden yapılandırılmış çözümde yapılandırma dosyasında belirtilen kurallar tarafından oluşturulan. Merhaba OEE veya KPI rakamları veya OPC UA düğüm değerlerini kendi yapılandırılan eşiği aşıldığında bu kurallar uyarılar oluşturabilir.

1. Merhaba **uyarıları paneli** hello bu çözümde oluşturulan uyarıları gösterir.

2. tooview hello bir uyarının ayrıntılarını hello uyarıları panelinde hello uyarıyı tıklatın.

3. toofurther hello uyarı verileri çözümlemek, hello grafik ortamında hello uyarı paneli tooopen hello zaman serisi Öngörüler explorer'ı tıklatın.

4. Uyarı tooaddress Merhaba, çeşitli eylemler hello uyarı panelinde kullanılabilir. Merhaba sizin için uygun seçeneği seçin ve hello tıklatın eylem komut düğmesi yürütün.

## <a name="view-overall-equipment-efficiency"></a>Genel donanım verimliliğini görüntüleme

OEE oranları anahtar bir üretim ile ilgili işletimsel parametrelerini kullanarak hello üretim işlem verimliliğini hello. OEE olan standart ölçü hesaplanan hello kullanılabilirlik oranı, performans oranı ve kalite oranı çarparak sektör: OEE kullanılabilirlik performans x kalitesi x =.

![Önceden yapılandırılmış bağlı fabrika çözümü OEE][cf-img-oee]

1. tooview OEE hello hiyerarşideki herhangi bir düzeye için ihtiyaç duyduğunuz toohello belirli görünüm gidin. Merhaba OEE bu görünümün hello paneli OEE yüzdesi hello yapmak hello öğelerin her biri ile birlikte görüntüler.

2. toofurther Merhaba OEE hello hiyerarşi verilerinde herhangi bir düzeye çözümlemek, hello OEE, kullanılabilirlik, performans veya kalite yüzdesi'ı tıklatın. Bir bağlam paneli zaman serisi Insights ile Merhaba son bir saat, son 24 saat ve son 7 gün verileri gösterir güç beslemeli görselleştirmeleri görüntülenir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI görselleştirmesi][cf-img-tsi-visualization]

3. toofurther hello uyarı verileri çözümlemek, hello uyarı panelinde hello grafiğe tıklayın. Bu eylemin hello zaman serisi Öngörüler explorer ortamı açılır.

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI gezgini][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Önemli Performans Göstergelerini görüntüleme

Merhaba çözümdür iki ana performans göstergelerini *saat başına birim* ve *KW/saat içinde kullanılan enerji*.

![Önceden yapılandırılmış bağlı fabrika çözümü KPI][cf-img-kpi]

1. saat veya hello hiyerarşideki herhangi bir düzeye için kullanılan enerji başına tooview birim toohello belirli görünüm ihtiyaç duyduğunuz gidin. saat ve enerji başına Hello birim hello Masası'nda görünen kullanılır.

2. saat veya daha fazla hello hiyerarşideki herhangi bir düzeye için kullanılan enerji başına tooanalyze birim tıklatın hello hello ölçerde **anahtar performans göstergelerini** paneli. Zaman serisi gücü Öngörüler görselleştirmelerle hello son bir saat hello son 24 saat ve son 7 gün tooview verilerden etkinleştirme bağlamı paneli görüntülenir.

## <a name="scenario-review"></a>Senaryo gözden geçirme

Bu senaryoda, oluşturucuları OEE ve KPI'leri değerler hello panosunda izlenen. Ardından anormallikleri algılama ile OEE ve KPI'leri toohelp için zaman serisi Öngörüler tooprovide daha fazla bilgi toohelp ayrıntıya daha fazla hello telemetri verileri kullanılır. Ayrıca hello uyarı paneli tooview sorunları, oluşturucuları ile kullanılan ve hello eylemleri kullanılabilir tooyou tooresolve hello uyarı kullanılır.

## <a name="other-features"></a>Diğer özellikler

Aşağıdaki bölümlerde hello hello önceki senaryoda açıklanan olmayan bazı ek bağlı hello Fabrika çözüm özelliklerini açıklar.

## <a name="apply-filters"></a>Filtreleri uygulama

1. Merhaba tıklatın **Köşeli Çift Ayraca** toodisplay hello Fabrika konumları paneli veya hello uyarıları panelinde kullanılabilir filtrelerin listesi.

2. Merhaba Filtreler paneli sizin için görüntülenir. 

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter]

3. İhtiyaç duyduğunuz hello filtre seçin. Olası tootype serbest metin hello filtre alanlara da sağlar.

4. Merhaba filtre ardından sizin için uygulanır. Merhaba filtre durumu hello factory'leri görüntüler ve tabloları uyarıları bir huni aracılığıyla hello panosunda da gösterilmektedir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Etkin bir filtreyi görüntülenen hello OEE ve KPI değerleri etkilemez yalnızca hello listesi içeriğine filtre uygular.

5. tooclear bir filtre hello Huni tıklayın ve filtre hello filtre bağlamı panelinde'yi tıklatın. Merhaba metin **tüm** hello factory'leri görüntülenir ve tabloları uyarır.

## <a name="browse-an-opc-ua-server"></a>OPC UA sunucusuna göz atma

Hello önceden yapılandırılmış çözümü dağıttığınızda, hello çözüm tarayıcı yoluyla göz atabilirsiniz benzetimli OPC UA sunucuları otomatik olarak sağlayın. Bu sunucular, *sanal OPC UA sunucularıdır*. Sanal sunucuları sizin için tooexperiment Merhaba, gerek toodeploy gerçek, fiziksel sunucuları olmadan hello önceden yapılandırılmış Çözümle kolaylaştırır. Merhaba tooconnect gerçek OPC UA sunucu toohello çözüm istiyorsanız bkz [OPC UA cihaz bağlı toohello Fabrika önceden yapılandırılmış çözümünüz bağlanmak] [ lnk-connect-cf] Öğreticisi.

1. Merhaba tıklatın **Fabrika simgesi** hello Panosu gezinti çubuğunda.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu tarayıcısı][cf-img-server-browser]

2. Merhaba sunuculardan biri hello önceden yapılandırılmış listeden seçin. Bu liste, sizin için önceden yapılandırılmış hello çözümde dağıtılan hello sunucularını gösterir.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu seçimi][cf-img-server-choice]

3. **Bağlan**’a tıklayın; güvenlik iletişim kutusu görüntülenir. İsteğe bağlı olarak Hello benzetimi için güvenli tooclick olan **devam et**

4. tooexpand herhangi bir hello sunucu ağacında hello düğüme tıklayın. Yayımlama telemetrisi olan düğümlerin yanında bir onay işareti vardır.

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu ağacı][cf-img-server-tree]

5. Bir öğe tooread sağ tıklatın, yazma, yayımlama veya bu düğüm çağırın. Merhaba eylemleri kullanılabilir tooyou, izinleri ve hello düğümü hello özniteliklerini bağlıdır. Merhaba seçeneği toodisplays hello belirli düğüm hello değerini gösteren bir bağlam panel okuyun. Yeni bir değer girebileceğiniz bir bağlam panel Hello yazma seçeneği görüntüler. Merhaba çağrısı seçeneği hello çağrısı için başlangıç parametreleri girebilecekleri bir düğüm görüntüler.

## <a name="publish-a-node"></a>Düğümü yayımlama

Göz atarken bir *benzetimli OPC UA sunucu*, yeni düğümler toopublish de seçebilirsiniz. Bu düğümden hello çözüm de hello telemetri analiz edebilirsiniz. Bunlar *benzetimli OPC UA sunucuları* gerçek, fiziksel cihazları dağıtmadan hello önceden yapılandırılmış çözümü ile kolay tooexperiment kolaylaştırır.

1. Merhaba toopublish istediğiniz OPC UA sunucu tarayıcı ağaç düğümünde tooa göz atın.

2. Merhaba düğümünü sağ tıklatın.

3. **Yayımla**’yı seçin.

    ![Bağlı fabrika yayımlama düğümü][cf-img-publish-node]

4. Merhaba yayımlama söyleyen bir bağlam paneli görünür başarılı oldu. Merhaba düğümü hello istasyon düzeyi görünümünde yanında bir onay işareti görünür.

    ![Önceden yapılandırılmış bağlı fabrika çözümü yayımlama başarısı][cf-img-publish-success]

## <a name="command-and-control"></a>Komut ve denetim

Merhaba bağlı Fabrika komut ve endüstri aygıtlarınızı hello bulut doğrudan denetim sağlar. Bu özellik toorespond tooalerts hello aygıt tarafından üretilen kullanabilirsiniz. Örneğin, bir komut toohello aygıt hello buluttan gönderebilir. Kullanılabilir komutlar hello hello bulabilirsiniz **StationCommands** hello OPC UA sunucuları tarayıcı ağaç düğümü. Bu senaryoda, bir baskısı yayın Vana Münih bir üretim satırının hello derleme istasyondaki açın. toouse hello komut ve denetim işlevleri, hello olmalıdır **yönetici** rolü hello için önceden yapılandırılmış Çözüm dağıtımı.

1. Toohello Gözat **StationCommands** hello OPC UA sunucu tarayıcı ağaç düğümü.

2. Kullanmak istediğiniz hello komutu seçin.

3. Merhaba düğümünü sağ tıklatın.

4. **Çağır**’ı seçin.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağır komutu][cf-img-call-command]

5. Bir bağlam panel hangi yöntemi bildiren hakkında toocall olan ve herhangi bir parametre ayrıntıyı uygulanabilir olduğunda görünür.

6. **Çağır**’ı seçin.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı bağlamı][cf-img-call-context]

7. yöntem çağrısının Merhaba, başarılı bir şekilde güncelleştirilmiş tooinform Hello bağlam panosudur. Merhaba çağrı sonucunda güncelleştirilmiş hello baskısı düğümü hello değeri okuyarak başarılı hello çağrısı doğrulayabilirsiniz.

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı başarısı][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Merhaba arka planda

Önceden yapılandırılmış çözümü dağıttığınızda, hello dağıtım işlemi hello Seçtiğiniz Azure aboneliği birden çok kaynak oluşturur. Bu kaynaklar hello Azure görüntüleyebilirsiniz [portal][lnk-portal]. Merhaba dağıtım işlemi oluşturur bir **kaynak grubu** önceden yapılandırılmış çözümünüz için seçtiğiniz hello adına dayalı bir ada sahip:

![Önceden yapılandırılmış çözümde hello Azure portalı][img-cf-portal]

Her bir kaynağın hello ayarları hello hello kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.

Merhaba hello önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz. Merhaba bağlı Fabrika önceden yapılandırılmış çözümün kaynak kodunu olduğu hello [azure-IOT-bağlı-Fabrika] [ lnk-cfgithub] GitHub deposunu:

İşiniz bittiğinde, Azure aboneliğinizin hello üzerinde hello önceden yapılandırılmış çözüm silebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] site. Bu sitenin tüm hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan kaynakları hello tooeasily Sil sağlar.

> [!NOTE]
> her şeyi silin tooensure toohello önceden yapılandırılmış çözümle ilgili, üzerinde hello silme [azureiotsuite.com] [ lnk-azureiotsuite] site. Merhaba portal Hello kaynak grubunda silmeyin.

## <a name="next-steps"></a>Sonraki Adımlar

Çalışan bir önceden çözüm dağıttıktan sonra aşağıdaki makaleler hello okuyarak IOT paketi ile Başlarken devam edebilirsiniz:

* [Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]
* [Cihaz toohello bağlı Fabrika önceden yapılandırılmış çözümünüz Bağlan][lnk-connect-cf]
* [Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]

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
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md
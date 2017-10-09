---
title: "aaaUse iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde | Microsoft Docs"
description: "Bilgi nasıl toouse iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Azure Data lake Analytics işleri için iş tarayıcı ve iş görünümünde kullanın
Hello Azure Data Lake Analytics hizmeti arşivler gönderilen işler bir [sorgu deposu](#query-store). Bu makaledeki bilgileri nasıl toouse iş tarayıcı ve Visual Studio toofind hello geçmiş için Azure Data Lake araçları iş görünümünde iş öğrenin. 

Varsayılan olarak, hello Data Lake Analytics hizmeti 30 gün boyunca hello işleri arşivler. Merhaba sona erme süresi özelleştirilmiş hello süre sonu ilkesi yapılandırarak hello Azure portal ' yapılandırılabilir. Mümkün tooaccess hello işi bilgileri dolduktan sonra olmaz. 

## <a name="prerequisites"></a>Ön koşullar
Bkz: [Visual Studio Önkoşullar için Data Lake Araçları](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Merhaba iş tarayıcı açın
Erişim hello iş tarayıcı yoluyla **Sunucu Gezgini > Azure > Data Lake Analytics > işleri** Visual Studio.  Merhaba iş tarayıcı kullanarak, bir Data Lake Analytics hesabı hello sorgu deposu erişebilir. İş tarayıcı Query Store sol, hello üzerinde temel iş bilgilerini gösterir ve iş görünümünde hello sağ gösteren ayrıntılı iş bilgi.

## <a name="job-view"></a>İşi görüntüle
İşi bir iş ile ilgili ayrıntılı bilgileri gösterir hello görüntüleyin. bir iş tooopen hello iş tarayıcı işinde çift tıklatın veya iş görünümünde tıklayarak hello Data Lake menüsünü açın. Merhaba iş URL ile doldurulan bir iletişim kutusu görmeniz gerekir.

![Visual Studio Proje tarayıcı Data Lake araçları](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

İş görünümünde içerir:

* İş Özeti
  
    Merhaba iş görünümünde yenileme toosee hello çalışan işi daha yeni bilgiler.
  
  * İş durumu (grafiği):
    
      İş durumu hello proje aşamalarını özetlenmektedir:
    
      ![Azure Data Lake Analytics işi aşamaları durumu](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Hazırlama: derleme ve hello derleme hizmeti kullanılarak hello komut en iyi duruma getirme, komut dosyası toohello bulut karşıya yükleyin.
    * Sıraya: Olan işleri için yeterli kaynak bekleyen sıraya alınan whey veya hesap sınırlaması başına en fazla eşzamanlı iş hello hello işleri aşan. Merhaba öncelik ayarı hello sıraya alınan işleri - hello düşük hello sayı hello yüksek hello öncelik sırasını belirler.
    * Çalışan: hello işi aslında Data Lake Analytics hesabınızı çalışıyor.
    * Sonlandırılıyor: hello işi (örneğin hello dosyası sonlandırılıyor) üzeredir.
      
      Merhaba iş her aşamasında başarısız olabilir. Örneğin, derleme hataları hello hazırlama aşamasında, zaman aşımı hataları hello sıraya alınan aşamasında ve hello çalışan aşaması, vb. yürütme hataları.
  * Temel bilgiler
    
      Merhaba temel iş bilgilerini hello alt kısmında hello iş özeti paneli gösterir.
    
      ![Azure Data Lake Analytics işi aşamaları durumu](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * İş sonuç: Başarılı veya başarısız oldu. Merhaba iş her aşamasında başarısız olabilir.
    * Toplam süre: saat gönderiliyor ve bitiş saati arasındaki saatin (süresi) duvar.
    * Toplam işlem süresi: her köşe yürütme süresi toplamı Merhaba, hello süresi gibi bu hello iş içinde yalnızca bir köşe yürütülür düşünebilirsiniz. TooTotal köşeleri toofind köşe hakkında daha fazla bilgi bakın.
    * Gönder/başlangıç/bitiş saati: hello zaman zaman iş gönderme/başlatır toorun hello hello Data Lake Analytics hizmeti alır iş/hello işi başarılı bir şekilde sona erer.
    * Derleme/sıraya alınan/çalışıyor: Duvar saati süresi hello sıraya alınan/hazırlama/çalışan aşamasında harcanan.
    * Hesap: hello Data Lake Analytics hesabı hello işi çalıştırmak için kullanılır.
    * Yazar: hello işinin hello kullanıcının gerçek bir kişinin hesap veya bir sistem hesabı olabilir.
    * Önceliği: Merhaba iş hello önceliği. Merhaba alt hello numarası hello yüksek hello önceliği. Yalnızca hello sırasındaki hello işleri hello dizisini de etkiler. Daha yüksek öncelik ayarı çalışan işlerin önüne geçer değil.
    * Paralellik: hello sayısının eşzamanlı Azure Data Lake Analytics birimleri (ADLAUs), diğer adıyla köşeleri istedi. Şu anda bir köşesinin eşit tooone VM iki sanal çekirdek ve altı GB RAM, bu yükseltme ancak Data Lake Analytics gelecekte güncelleştirir.
    * Bayt sol: hello iş tamamlanana kadar işlenen toobe gereken bayt sayısı.
    * Okuma ve yazılan bayt: çalışmaya başladığı hello işinden bu yana okunan ve yazılan silinmiş bayt sayısı.
    * Toplam köşeleri: hello iş parçalara pek çok parçalı bir işin, her parça işin bir köşe denir. Bu değer, kaç tane parçalı bir işin hello iş oluşan açıklar. Temel işlem birim olarak, diğer adıyla Azure Data Lake Analytics birim (ADLAU), bir köşe düşünebilirsiniz ve köşeleri paralellik çalıştırabilirsiniz. 
    * Tamamlanan/çalışan/başarısız oldu: tamamlandı/çalışan/başarısız tepe sayısı hello. Köşeleri tooboth kullanıcı kodu ve sistem hataları başarısız olabilir, ancak hello sistem yeniden deneme köşeleri otomatik olarak birkaç kez başarısız oldu. Merhaba köşe denedikten sonra yine başarısız olursa hello tüm işi başarısız olur.
* İş grafiği
  
    U-SQL betiği giriş veri toooutput veri dönüştürme hello mantığı temsil eder. Merhaba betik derlenir ve tooa fiziksel yürütme planı hello hazırlama aşamasında, en iyi duruma getirilmiş. İş grafiğinin tooshow hello fiziksel yürütme planı ' dir.  Aşağıdaki diyagramda hello hello işlemi gösterilmektedir:
  
    ![Azure Data Lake Analytics işi aşamaları durumu](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Bir iş, çok parçalı bir işin ayrılır. Her parça işin bir köşe adı verilir. Merhaba köşeleri Süper köşe (diğer adıyla aşama) gruplandırılmış ve iş grafiği görünür. Hello yeşil aşama placards hello iş grafikte hello aşamalarını gösterir.
  
    Her bir aşamasında köşe hello yaptığını aynı tür hello farklı parçalarının aynı iş verileri. Örneğin, bir TB veri sahip bir dosya varsa ve buradan okuma köşeleri yüzlerce vardır, bunların her biri bir öbek okuyor. Bu köşeleri hello gruplandırılır aynı Aşama ve aynı bulunurken aynı girdi dosyası farklı parçalarının çalışır.
  
  * <a name="state-information"></a>Aşama bilgileri
    
      Belirli bir aşamada, bazı numaralarını hello afişinde gösterilmektedir.
    
      ![Azure Data Lake Analytics işi grafik aşaması](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Ayıkla: numarası ve hello işlemi yöntemi tarafından adlı bir aşamasının hello adı.
    * 84 köşeleri: Bu aşamada hello köşeleri toplam sayısı. Merhaba şekil kaç parçalı bir işin bu aşamada bölünmüş gösterir.
    * 12.90 s/köşe: Bu aşama için ortalama köşe yürütme süresi hello. Bu şekil SUM (her köşe yürütme süresi) tarafından hesaplanır / (toplam köşe sayısı). Yani paralellik içinde yürütülen tüm hello köşeleri atayabilir, hello tüm aşama tamamlandı 12.90 s. Ayrıca anlamı tüm iş hello varsa bu aşamada seri olarak yapılır, hello maliyet #vertices olacaktır * ortalama zaman.
    * yazılan 850,895 satırlar: toplam satır sayısı bu aşamada yazılır.
    * R/w miktarda veri okunur/yazılan bayt bu aşamasında.
    * Renkler: Renkler hello aşama tooindicate farklı köşe durumunda kullanılır.
      
      * Yeşil hello köşe başarılı gösterir.
      * Turuncu hello köşe denenen gösterir. Denenen hello köşe başarısız oldu, ancak otomatik olarak yeniden denenir ve başarıyla hello sistemi ve genel hello aşaması başarıyla tamamlandı. Merhaba köşe denenen ancak hala başarısız oldu, hello rengi kırmızı ve hello tüm işi başarısız oldu etkinleştirir.
      * Kırmızı başarısız, gösterir belirli bir köşe başka bir deyişle, hello sistem tarafından birkaç kez yeniden denendi ancak hala başarısız oldu. Bu senaryo hello tüm iş toofail neden olur.
      * Belirli bir köşe çalıştıran mavi anlamına gelir.
      * Beyaz gösterir hello köşe bekliyor. Merhaba köşe bir ADLAU kullanılabilir duruma gelir veya kendi giriş verilerini hazır olmayabilir beri bu girişi bekleniyor sonra zamanlanmış bekleme toobe olabilir.
      
      Fare imlecinizi bir duruma göre gelerek hello aşaması için daha fazla ayrıntı bulabilirsiniz:
      
      ![Azure Data Lake Analytics iş grafiği aşama ayrıntıları](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Köşeleri: hello köşeleri ayrıntıları, örneğin, kaç tane köşeleri tamamladınız, toplamda kaç köşeleri başarısız oldu veya hala çalışıyor/bekleme, vb. olan açıklar.
  * Veri okuma arası/içi pod: dosyaları ve verileri depolanmış olan birden çok pod'ları içinde dağıtılmış dosya sistemi. Buraya Hello değer ne kadar veri hello aynı pod veya pod arası Okunmuş açıklar.
  * Toplam işlem süresi: hello toplam ele tüm hello aşamasında çalışıyorsanız hello saat içinde yalnızca bir köşe yürütülür gibi hello aşama'da her köşe yürütme süresini, onu düşünebilirsiniz.
  * Veri ve satır yazılmış/okuma: ne kadar veri satırları okunan ve yazılan veya toobe gereksinim gösterir okuyun.
  * Köşe okuma hataları: kaç köşeleri veri okuma sırasında başarısız olan açıklar.
  * Köşe yinelenen atar: köşe çok yavaş çalışıyorsa, birden çok köşeleri hello sistem zamanlayabilir toorun hello aynı parça işin. Merhaba köşeleri birini tamamladıktan sonra başarıyla reductant köşeleri atılacak. Köşe yinelenen kayıtları hello yinelenen hello aşamasında atılır tepe sayısı atar.
  * Köşe iptalleri: hello köşe başarıyla gerçekleştirildi, ancak daha sonra toosome nedenlerden dolayı yeniden. Örneğin, aşağı akış köşe Ara giriş verisi kesilirse, hello Yukarı Akış köşe toorerun sorar.
  * Köşe zamanlama yürütmeleri: hello köşeleri zamanlanmış hello toplam süre.
  * Ortalama/min/Max köşe veri okuma: hello minimum/ortalama/maksimum her köşesinin verileri okuma.
  * : Bir aşamayı alır, hello duvar saati süresi, bu değer tooload profili toosee gerekir.
  * İş Kayıttan Yürütme
    
      Data Lake Analytics işleri çalıştırır ve arşivler hello hello köşeleri ne zaman başlatılır gibi hello işleri bilgilerinin çalıştıran köşeleri durduruldu, başarısız olan ve bunların nasıl denenen, vs. Merhaba bilgilerin tümünü otomatik olarak hello sorgu deposunda oturum açmış ve kendi iş profil içinde saklanır. Merhaba iş görünümünde "Yük profili" ile iş profiline indirebilirsiniz ve hello iş profili indirdikten sonra hello iş kayıttan yürütme görüntüleyebilirsiniz.
    
      İş kayıttan yürütme hello kümede ne, epitome görselleştirme ' dir. İş yürütme ilerleme durumunu izleyin ve performans anormalliklerini ve sorunlarını çok kısa bir süre içinde (değerinden genellikle 30s) kullanıma görsel olarak algıla yardımcı olur.
  * İş ısı Haritası görüntüleme 
    
      İş grafiğinin hello görünen açılır aracılığıyla iş ısı Haritası seçilebilir. 
    
      ![Azure Data Lake Analytics işi grafik yığın harita görünümü](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Merhaba g/ç, saati ve verimlilik ısı Haritası üzerinden nerede hello iş hello zamanının çoğunu harcadığı veya işinizi bir g/ç sınır işi olup bulabilir ve benzeri bir işin gösterir.
    
      ![Azure Data Lake Analytics işi grafik yığın eşleme örneği](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * İlerleme durumu: Merhaba iş yürütme ilerleme durumunu, bilgilerine bakın [aşama bilgi](#stage-information).
    * Okuma ve yazılan veriler: hello ısı Haritası toplam veri her aşamada okunur/yazılır.
    * Saat işlem: hello ısı Haritası SUM (her köşe yürütme süresi) dikkate almanız bu hello aşamasında tüm iş ile yalnızca 1 köşe yürütülürse uzun sürecektir nasıl.
    * Düğüm başına ortalama yürütme süresi: hello ısı Haritası SUM (her köşe yürütme süresi) / (köşe numarası). Hangi paralellik içinde yürütülen tüm hello köşeleri atarsanız, bu zaman dilimi içinde hello tüm aşama biteceğini gösterir.
    * Giriş/Çıkış işleme: giriş/çıkış işleme, her bir aşamaya hello ısı haritası, işinizi bir g/ç ilişkili işi bu aracılığıyla olup olmadığını onaylayabilirsiniz.
* Meta veri işlemleri
  
    U-SQL komut dosyanıza bazı meta veri işlemleri, aşağıdaki gibi bir veritabanı oluşturmak, drop table, vb.. Bu işlemlerin sonra derleme meta veri işlemi gösterilmektedir. Onaylar bulmak, varlıkları oluşturma, varlıkları buraya bırak.
  
    ![Azure Data Lake Analytics iş görünümünde meta veri işlemleri](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Durum geçmişi
  
    Merhaba Durum geçmişi ayrıca iş özeti görselleştirilen ancak burada daha fazla bilgi alabilirsiniz. Ayrıntılı hello bulabilirsiniz hello işi zaman hazırlanmış gibi bilgileri sıraya çalışmaya başladığı, sona erdi. Merhaba iş derlenmiş kaç kez de bulabilirsiniz (CcsAttempts hello: 1), hello iş gönderilen toohello küme gerçekte olduğunda (ayrıntı hello: iş toocluster gönderme), vb..
  
    ![Azure Data Lake Analytics iş görünümünde durumu geçmişi](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Tanılama
  
    Merhaba aracı iş yürütme otomatik olarak tanılar. Bazı hatalar veya işleriniz performans sorunları olduğunda uyarı alırsınız. Lütfen toodownload profili tooget tam buradaki bilgiler gerektiğini unutmayın. 
  
    ![Azure Data Lake Analytics iş görünümünde tanılama](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Uyarı: Bir uyarı burada ile derleyici uyarısı görüntülenir. Merhaba uyarı göründükten sonra daha fazla ayrıntı "x sorunları" bağlantı toohave tıklayabilirsiniz.
  * Çok uzun çalıştırma köşe: herhangi bir izdüşümünü saati (deyin 5 saat) dışında çalıştırıyorsa, sorunları burada bulunacaktır.
  * Kaynak Kullanımı: gerekenden daha fazla veya yeterli paralellik ayırdığınızda, sorunları burada bulunacaktır. Ayrıca daha fazla ayrıntı kaynak kullanım toosee tıklatın ve durum senaryoları toofind daha iyi kaynak ayırma gerçekleştirin (daha fazla ayrıntı için bu Kılavuzu'na bakın).
  * Bellek onay: herhangi bir izdüşümünü 5 GB'den fazla bellek kullanıyorsa, sorunları burada bulunacaktır. Sistem sınırlaması daha fazla bellek kullanıyorsa, iş yürütme sistem tarafından sonlandırıldı.

## <a name="job-detail"></a>İş ayrıntısı
İş ayrıntısı hello komut dosyası, kaynakları ve köşe yürütme görünümü de dahil olmak üzere hello işin ayrıntılı bilgileri gösterir.

![Azure Data Lake Analytics iş ayrıntısı](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Betik
  
    U-SQL betiği hello işin Hello hello sorgu deposunda saklanır. Merhaba özgün U-SQL betiği görüntülemek ve gerekirse yeniden gönderin.
* Kaynaklar
  
    Kaynakları aracılığıyla hello sorgu deposunda depolanan hello iş derleme çıkışları bulabilirsiniz. Örneği için "kullanılan tooshow hello iş grafiği, kaydettiğiniz hello derlemeler, burada vb. olan algebra.xml" bulabilirsiniz.
* Köşe yürütme görünümü
  
    Bu, köşe yürütme ayrıntıları gösterir. Merhaba iş profili toplam veri okunur/yazılır, çalışma zamanı, durum, vb. gibi her köşe yürütme günlüğü arşivler. Bu görünüm nasıl bir işin çalışma hakkında daha fazla ayrıntı elde edebilirsiniz. Daha fazla bilgi için bkz: [kullanım hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Sonraki Adımlar
* toolog tanılama bilgilerini görmek [Azure Data Lake Analytics için tanılama günlükleri erişme](data-lake-analytics-diagnostic-logs.md)
* toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).
* toouse köşe yürütme görünümü bkz [kullanım hello Visual Studio için Data Lake araçları, köşe yürütme görünümü](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)


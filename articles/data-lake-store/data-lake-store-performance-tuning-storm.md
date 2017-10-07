---
title: "aaaAzure Data Lake deposu Storm performans yönergeleri ayarlama | Microsoft Docs"
description: "Azure Data Lake Store Storm performans kuralları ayarlama"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Performans Kılavuzu Hdınsight ve Azure Data Lake Store üzerinde Storm için ayarlama

Bir Azure Storm topolojisinin hello performansı ayarlamak yükleyen düşünülmesi gereken hello Etkenler anlayın. Örneğin, önemli toounderstand hello hello spout'lar ve hello Cıvatalar (Merhaba iş g/ç yoğun olup) tarafından yapılan hello iş özelliklerini olur. Bu makalede, performans ayarlama yönergeleri, ortak sorunları da dahil olmak üzere çeşitli yer almaktadır.

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.
* **Data Lake Store üzerinde Storm kümesi çalıştıran**. Daha fazla bilgi için bkz: [Hdınsight üzerinde Storm](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Performans ayarlama yönergeleri Data Lake Store üzerinde**.  Genel performans için bkz [Data Lake deposu performans ayarlama Kılavuzu](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Merhaba paralellik hello topolojisinin ayarlama

Data Lake Store gelen hello g/ç tooand artan hello eşzamanlılığı tarafından mümkün tooimprove performans olabilir. Bir Storm topolojisinin hello paralellik belirlemek yapılandırmaları kümesi vardır:
* (Merhaba VM'ler arasında hello çalışanları olacak şekilde eşit dağıtılır) çalışan işlem sayısı.
* Spout Yürütücü örneği sayısı.
* Cıvata Yürütücü örneği sayısı.
* Spout görev sayısı.
* Cıvata görev sayısı.

Örneğin, 4 VM'ler ve 4 çalışan işlemleri, 32 spout yürütücüler 32 spout görevleri ve 256 Cıvata yürütücüler ve 512 Cıvata görevleri ile bir kümede hello aşağıdakileri göz önünde bulundurun:

Çalışan düğümüne olan her yönetici tek bir çalışan Java sanal makine (JVM) işlemi vardır. Bu JVM işlem 4 spout iş parçacıkları ve 64 Cıvata iş parçacığı yönetir. Her iş parçacığı içinde görevleri sırayla çalışır. Yapılandırma önceki hello ile 1 görev her spout iş parçacığı vardır ve her Cıvata iş parçacığı 2 görevleri vardır.

Storm, ilgili çeşitli bileşenleri hello işte ve sahip olduğunuz paralellik hello düzeyini nasıl etkilediklerini:
* Merhaba baş düğümü (Storm içinde çağrılan Nimbus) kullanılan toosubmit olduğu ve işleri yönetin. Bu düğümler üzerinde hello paralellik derecesi herhangi bir etkisi vardır.
* Hello Yöneticisi düğümleri. Hdınsight'ta, bu tooa çalışan düğümüne Azure VM karşılık gelir.
* Merhaba VM'ler çalışan Storm işlemler Hello çalışan görevlerdir. Her çalışan görev tooa JVM örneği karşılık gelir. Storm dağıtır hello numarası çalışan işlemleri, toohello çalışan düğümleri mümkün olduğunca eşit belirtin.
* Spout ve yürütücü örnekleri Cıvata. Her bir yürütücü örneği hello çalışanları (JVMs) içinde çalışan tooa iş parçacığı karşılık gelir.
* Storm görevler. Bunların her birini Çalıştır iş parçacıkları mantıksal görevlerdir. Yürütücü başına birden çok görev veya gerekiyorsa değerlendirmelidir şekilde bu paralellik, hello düzeyini değiştirmez.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Data Lake Deposu'ndan veri Hello en iyi performansı elde

Aşağıdaki Merhaba, Data Lake Store ile çalışırken, hello en iyi performansı elde:
* Birleşim küçük ve büyük boyutları (İdeal olarak 4 MB) ekler.
* Mümkün olduğu kadar eşzamanlı istek yapın. Her Cıvata iş parçacığı engelleme okuma yapmak için herhangi bir yerde aralığındaki hello çekirdek başına 8-12 iş parçacığı toohave istiyorsunuz. Bu da kullanılan hello NIC ve hello CPU tutar. Daha büyük bir VM daha fazla istek sağlar.  

### <a name="example-topology"></a>Örnek topoloji

Bir 8 çalışan düğümü küme D13v2 Azure VM ile sahip varsayalım. Bu VM, 8 çekirdek sahip, bu nedenle arasında 8 çalışan düğümleri Merhaba, 64 toplam çekirdeğe sahip.

Biz çekirdek başına 8 Cıvata iş parçacığı yapmak varsayalım. 64 çekirdek, 512 toplam Cıvata Yürütücü örnekleri (diğer bir deyişle, iş parçacıkları) istiyoruz anlamına gelir. Bu durumda, biz VM başına bir JVM başlayın ve çoğunlukla hello iş parçacığı eşzamanlılık hello JVM tooachieve eşzamanlılık içinde kullanmak varsayalım. 8 çalışan görevler (Azure VM başına bir tane) ve 512 Cıvata yürütücüler ihtiyacımız anlamına gelir. Bu yapılandırma verildiğinde, Storm her bir çalışan düğümünün 1 vermiş toodistribute hello çalışanları çalışan düğümleri (olarak da bilinen yönetici düğümler), arasında eşit olarak çalıştığında JVM. Merhaba denetçiler içinde Storm toodistribute hello yürütücüler denetçiler arasında eşit olarak çalışır. Şimdi her yönetici (diğer bir deyişle, JVM) vermiş 8 her iş parçacıkları.

## <a name="tune-additional-parameters"></a>Ek parametrelerini ayarlama
Merhaba temel topoloji aldıktan sonra tootweak hello parametrelerinden herhangi birini isteyip istemediğinizi düşünebilirsiniz:
* **Çalışan düğüm başına JVMs sayısı.** Büyük veri yapısı (örneğin, bir arama tablosu) varsa, barındıran bellekte her JVM ayrı bir kopyasını gerektirir. Alternatif olarak, daha az JVMs varsa birçok iş parçacıkları arasında hello veri yapısı kullanabilirsiniz. Merhaba Cıvata'nın g/ç JVMs hello sayısı kadar hello bu JVMs eklenen iş parçacığı sayısı olarak farkının yapmaz. İsteğe bağlı olarak kolaylık sağlamak için bir fikir toohave biri olan çalışan başına JVM. Bu sayı toochange gerekebilir rağmen Cıvata yaptıklarını veya hangi uygulama, işleme bağlı olarak, gerektirir.
* **Spout yürütücüler sayısı.** Merhaba önceki örnekte Cıvatalar tooData Lake Store yazmak için kullandığı için hello spout'lar değil doğrudan ilgili toohello Cıvata performans sayısıdır. Ancak, hello miktarda işleme veya gerçekleştiği hello spout iyi bir fikirdir g/ç bağlı olarak, en iyi performans için tootune hello spout'lar. Yeterli spout'lar toobe mümkün tookeep hello Cıvatalar meşgul olduğundan emin olun. Merhaba spout'lar Hello çıkış oranları hello Cıvatalar hello verimini eşleşmelidir. Merhaba gerçek yapılandırma üzerinde hello spout bağlıdır.
* **Görev sayısı.** Her Cıvata tek bir iş parçacığı çalıştırır. Ek görevler Cıvata başına herhangi bir ek eşzamanlılık sağlamaz. yararı oldukları hello yalnızca, işleminin hello tuple aktarımının Cıvata yürütme süresi büyük bir kısmının alır, saattir. Merhaba Cıvata onay göndermeden önce birçok başlıkları daha geniş bir içine ekleme iyi bir fikir toogroup olur. Bu nedenle, çoğu durumda, birden çok görevler ek fayda sağlar.
* **Yerel veya karışık gruplandırma.** Bu ayar etkinleştirildiğinde, tanımlama grupları toobolts hello içinde gönderilen aynı çalışan işlemi. Bu işlemler arası iletişim ve ağ çağrıları azaltır. Bu, çoğu Topolojileri için önerilir.

Bu temel senaryo iyi bir başlangıç noktasıdır. Kendi veri tootweak hello parametreleri tooachieve en iyi performans önceki sınayın.

## <a name="tune-hello-spout"></a>Merhaba spout ayarlama

Hello ayarları tootune hello spout aşağıdaki değiştirebilirsiniz.

- **Tuple zaman aşımı: topology.message.timeout.secs**. Bu ayar, hello bir ileti gereken süreyi toocomplete belirler ve kabul edilmeden önce onay, almak başarısız oldu.

- **Çalışan işlemi başına maksimum bellek: worker.childopts**. Bu ayarı ek komut satırı parametreleri toohello Java çalışanları belirtmenize olanak sağlar. en yaygın olarak kullanılan hello ayarı burada hello ayrılan en fazla bellek tooa JVM'ın yığın belirler XmX ' dir.

- **Max spout bekleyen: topology.max.spout.pending**. Bu ayar hello (henüz onaylanan da hello topoloji tüm düğümlerde) uçuş spout iş parçacığı başına herhangi bir zamanda buna olabilir başlıkların sayısını belirler.

 İyi hesaplama toodo tooestimate hello her, başlık boyutudur. Sonra ne kadar bellek bir spout iş parçacığı olduğunu göstermektedir. Merhaba tooa iş parçacığı, bu değer ile bölünmüş ayrılan toplam bellek size hello üst sınırı için hello max spout parametre bekliyor.

## <a name="tune-hello-bolt"></a>Merhaba Cıvata ayarlama
TooData Lake Store yazarken boyutu eşitleme ilkesi (Merhaba istemci tarafı arabelleği) ayarlamak too4 MB. Yalnızca hello arabellek boyutu bu değerde hello olduğunda bir temizleme veya hsync() sonra gerçekleştirilir. açıkça bir hsync() gerçekleştirmediğiniz sürece hello Data Lake Store sürücü hello çalışan VM üzerinde otomatik olarak bu arabelleğe yapar.

Merhaba varsayılan Data Lake deposu Storm Cıvata kullanılan tootune olabilecek bir boyutu eşitleme ilkesi parametre (fileBufferSize) Bu parametre içeriyor.

İsteğe bağlı olarak g/Ç kullanımı yoğun topolojide iyi bir fikir toohave olan her Cıvata iş parçacığı, bir dosya döndürme İlkesi (fileRotationSize) tooits kendi dosya ve tooset yazma. Merhaba dosya belirli bir boyuta ulaştığında hello akışı otomatik olarak Temizlenen ve yeni bir dosya yazılır. Dosya boyutu döndürme için önerilen hello 1 GB'tır.

### <a name="handle-tuple-data"></a>Tuple veri işleme

Açıkça hello Cıvata tarafından onaylanan kadar Storm bir spout tooa tuple tutar. Bir tanımlama grubu hello Cıvata tarafından okunabilir ancak henüz onaylanan değil, Data Lake Store arka uç hello spout kalıcı. Bir tanımlama grubu kabul edildikten sonra hello spout hello Cıvata tarafından Kalıcılık güvence altına alınabilir ve hello kaynak verileri içinden okuma ne olursa olsun kaynağından sonra silebilirsiniz.  

Data Lake Store üzerinde en iyi performans için hello Cıvata sahip 4 MB tanımlama grubu veri arabellek. Ardından Data Lake Store geri son bir 4 MB yazma toohello yazın. Merhaba veri başarıyla yazılı toohello deposu sonra (arama hflush()) tarafından hello Cıvata hello veri geri toohello spout kabul. Bu hangi hello örnektir sağlanan burada mu Cıvata. Aynı zamanda kabul edilebilir toohold fazla sayıda hello hflush() araması yapılmadan önce tanımlama grupları ve hello olan diziler onaylanır. Ancak, bu hello hello spout toohold gerekir ve bu nedenle artar JVM gerekli bellek miktarını hello yürütülen başlıkların sayısını artırır.

> [!NOTE]
Uygulamaların diğer olmayan performans nedenleriyle bir gereksinim tooacknowledge başlıkları daha sık (adresindeki veri boyutları'dan 4 MB) olabilir. Ancak, hello g/ç işleme toohello depolama arka ucu etkileyebilir. Bu kolaylığını hello Cıvata'nın g/ç performansı karşı dikkatle tartmanız.

Uzun süre toofill Hello 4 MB'lık arabelleğe alır şekilde hello gelen oran başlık değil, yüksekse, bu azaltıcı göz önünde bulundurun:
* Cıvatalar Hello sayısının azaltılması, bu nedenle vardır daha az arabellek toofill.
* Bir hflush() olduğu bir saat veya sayısı tabanlı ilke sahip her Boşaltılma x veya her y milisaniye tetiklenir ve o ana kadarki birikmiş hello diziler geri onaylanır.

Merhaba verimlilik bu durumda düşüktür, ancak olayları yavaş oranı ile en yüksek verimlilik hello büyük hedefi yine de değil unutmayın. Bu Azaltıcı Etkenler bir tanımlama grubu tooflow toohello deposu üzerinden geçen toplam süre hello azaltmanıza yardımcı olur. Düşük olay hızı bile ile gerçek zamanlı bir işlem hattı istiyorsanız bu önemli. Ayrıca, gelen tanımlama grubu hızı düşükse, bunlar alma sırasında zaman aşımı hello diziler olmayan şekilde, hello topology.message.timeout_secs parametre olarak ayarlaması gerektiğini Not arabelleğe veya işlenen.

## <a name="monitor-your-topology-in-storm"></a>Topolojiniz Storm içindeki izleme  
Topolojiniz çalışırken hello Storm kullanıcı arabiriminde izleyebilirsiniz. Merhaba ana parametreleri toolook adresindeki şunlardır:

* **Toplam işlem yürütme gecikme süresi.** Bir tanımlama grubu hello spout'un yayılan, hello Cıvata tarafından işlenir ve onaylanan toobe hello ortalama süreyi budur.

* **Toplam Cıvata işlem gecikme süresi.** Bir bildirim alıncaya kadar hello Cıvata adresindeki hello tanımlama grubu tarafından harcanan hello ortalama süre budur.

* **Toplam Cıvata gecikme yürütün.** Bu hello ortalamadır hello içinde hello Cıvata tarafından harcanan süre yürütme yöntemi.

* **Başarısızlık sayısı.** Bu, bunlar zaman aşımına uğramadan önce tam olarak işlenen toobe başarısız başlıkların toohello sayısını ifade eder.

* **Kapasitesi.** Bu, sisteminizi ne kadar meşgul olduğundan bir ölçüsüdür. Bu sayı 1 ise, Cıvatalar yapabilir kadar hızlı çalışmaktadır. 1'den küçük, hello paralellik artırın. 1'den büyükse, hello paralellik azaltın.

## <a name="troubleshoot-common-problems"></a>Sık karşılaşılan sorunları giderme
Birkaç genel sorun giderme senaryoları şunlardır.
* **Birçok diziler zaman aşımına uğruyor.** Merhaba topoloji toodetermine içindeki her bir düğümün hello performans sorunu olduğu bakın. Merhaba en yaygın nedeni bu hello Cıvatalar mümkün tookeep yukarı hello spout'lar olmamasıdır. Bu, işlenen bekleme toobe sırasında hello iç arabellek tıkamasını tootuples yol açar. Merhaba zaman aşımı değerini artırmayı veya bekleyen hello max spout azaltarak göz önünde bulundurun.

* **Yüksek toplam işlem yürütme gecikmesi, ancak düşük Cıvata işlem gecikme yoktur.** Bu durumda, hello diziler yeterince hızlı alınıyor değil, mümkündür. Acknowledgers yeterli sayıda olup olmadığını denetleyin. Başka bir olasılık hello işlemeden başlangıç Cıvatalar önce bunlar sırada hello çok uzun süre beklediğini olabilir. Merhaba max spout bekleyen azaltın.

* **Yüksek Cıvata yürütme gecikme süresi yok.** Başka bir deyişle, Cıvata hello execute() yöntemi çok uzun sürüyor. Merhaba kodu en iyi duruma veya yazma boyutlarda görünüş ve davranışı temizleme.

### <a name="data-lake-store-throttling"></a>Data Lake Store azaltma
Data Lake Store tarafından sağlanan bant genişliğinin hello sınırına ulaşıp görev hataları görebilirsiniz. Hataları azaltma için görev günlüklerini denetleyin. Kapsayıcı boyutu artırarak hello paralellik düşürebilir.    

Kısıtlanan, toocheck hello hata ayıklama hello istemci tarafında günlüğü etkinleştir:

1. İçinde **Ambari** > **Storm** > **Config** > **storm çalışan log4j Gelişmiş**, değiştirme  **&lt;kök düzeyi "bilgi" =&gt;**  çok**&lt;kök düzeyi "hata ayıklama" =&gt;**. Merhaba yapılandırma tootake etkisi için tüm hello düğümleri/hizmetini yeniden başlatın.
2. İzleyici hello Storm topolojisini günlüklerini çalışan düğümlerine (/var/log/storm/worker-artifacts altında /&lt;TopologyName&gt;/&lt;bağlantı noktası&gt;/worker.log) özel durumları azaltma Data Lake Store için.

## <a name="next-steps"></a>Sonraki adımlar
Storm olarak başvurulabilir için ek performans ayarlaması [bu blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Ek örnek toorun için bkz: [github'daki bu bir](https://github.com/hdinsight/storm-performance-automation).

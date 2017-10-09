---
title: "aaaBatch ve HPC çözümleri - hello bulutta Azure | Microsoft Docs"
description: "Azure’de toplu işlem ve yüksek performanslı bilgi işlem (HPC ve Big Compute) senaryoları ve çözüm seçenekleri hakkında bilgi alın"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Büyük ölçekli bilgi işlem iş yükleri için Batch ve HPC çözümleri

Azure toplu işlem ve *Big Compute* olarak da bilinen yüksek performanslı bilgi işlem (HPC) için verimli, ölçeklenebilir bulut çözümleri sunar. Burada Big Compute iş yükleri ve Azure Hizmetleri toosupport hakkında bilgi ya da doğrudan çok atlama[çözüm senaryoları](#scenarios) bu makalenin ilerisinde yer. Bu makalede temel olarak teknik karar verenler, BT yöneticileri ve bağımsız yazılım satıcıları için olan, ancak BT toofamiliarize kendilerini diğer BT profesyonelleri ve geliştiricilerin bu çözümleri ile kullanabilirsiniz.

Kuruluşlarda büyük ölçekli bilgi işlem sorunları vardır: mühendislik tasarımı ve analizi, görüntü işleme, karmaşık modelleme, Monte Carlo benzetimleri, finansal risk hesaplamaları ve diğerleri. Azure, kuruluşların hello kaynaklar, ölçek ve zamanlama ile bu sorunların çözülmesine yardımcı olur. Azure’le kuruluşların yapabildikleri:

* Bir şirket içi HPC küme toooffload yoğun iş yükleri toohello buluta uzanan karma çözümler oluşturma
* HPC küme araçlarını ve iş yüklerini tamamen Azure'da çalıştırma
* Yönetilen ve ölçeklenebilir Azure hizmetlerini gibi kullandığınız [toplu](https://azure.microsoft.com/documentation/services/batch/) toodeploy kalmadan toorun yoğun iş yükleri ve bilgi işlem altyapısı yönetme

Merhaba bu makalenin kapsamı olsa da, ötesinde Azure de geliştiriciler ve ortakları özellikleri, mimari seçim ve geliştirme araçları toobuild büyük ölçekli, özel Big Compute iş akışlarını tam kümesi sağlar. Ve büyüyen bir ortak ekosistemi Big Compute iş yüklerinizi hello Azure bulut üretken yaptığınız hazır toohelp.

## <a name="batch-and-hpc-applications"></a>Batch ve HPC uygulamaları
Web uygulamalarından ve birçok iş kolu uygulamalarından farklı olarak, toplu işlem ve HPC uygulamalarında tanımlı bir başlangıç ve bitiş vardır;zamanlamayla veya istek üzerine bazen saatlerce ve hatta daha uzun çalışabilirler. Çoğu iki ana kategoriye ayrılır: *doğası gereği paralel* (Merhaba sorunları çözdüklerinden kendilerini toorunning birden çok bilgisayarda veya işlemciler üzerinde paralel ödünç vermek için "utandırıcı derecede paralel" de denir) ve *sıkı şekilde bağlı*. Bu uygulama türleri hakkında daha fazla bilgi için aşağıdaki tablonun hello bakın. Bazı Azure çözüm bir türü ya da diğer hello için daha iyi iş yaklaşıyor.

> [!NOTE]
> Batch ve HPC çözümlerinde uygulamanın çalışan bir örneği olan ve yaygın adıyla *iş* ya da her iş *görevlere* ayrılır. Ve hello Merhaba uygulaması kümelenmiş işlem kaynakları genellikle denir *işlem düğümleri*.
> 
> 

| Tür | Özellikler | Örnekler |
| --- | --- | --- |
| **Doğası gereği paralel**<br/><br/>![Doğası gereği paralel][parallel] |• Tek tek bilgisayarlar uygulama mantığını bağımsız çalıştırır<br/><br/> • Bilgisayar eklenmesi hello uygulama tooscale ve azaltma hesaplama zamanı sağlar<br/><br/>• Uygulama ayrı yürütülebilir öğelerden oluşur veya istemcinin başlattığı hizmet grubuna bölünür (hizmet odaklı mimari veya SOA uygulaması) |• Finansal risk modelleme<br/><br/>• Görüntü işleme <br/><br/>• Medya kodlama ve kodlama dönüştürme<br/><br/>• Monte Carlo benzetimleri<br/><br/>• Yazılım testi |
| **Sıkı şekilde bağlı**<br/><br/>![Sıkı şekilde bağlı][coupled] |• Uygulama işlem düğümleri toointeract veya exchange Ara sonuçların gerektirir<br/><br/>• İşlem düğümleri kullanılarak iletişime geçebilirler Merhaba ileti geçirme arabirimi (MPI), paralel bilgi işlem için yaygın bir iletişim protokolü<br/><br/>• hello hassas toonetwork gecikme süresi ve bant genişliği uygulamadır<br/><br/>• Uygulama performansı, InfiniBand ve doğrudan uzak bellek erişimi (RDMA) gibi yüksek hızlı ağ teknolojileri kullanılarak geliştirilebilir. |• Petrol ve gaz rezervuarı modelleme<br/><br/>• Mühendislik tasarımı ve hesaplama sıvı dinamiği gibi analizi<br/><br/>• Araba kazaları ve nükleer tepkiler gibi fiziksel benzetimler<br/><br/>• Hava durumu tahmini |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Batch ve HPC uygulamaları hello bulutta çalışan dikkat edilmesi gereken noktalar
Şirket içi HPC küme tooAzure veya tooa karma (şirket içi) ortamında tasarlanmış toorun olan birçok uygulamaları kolayca geçirebilirsiniz. Ancak, bazı sınırlamalar veya değerlendirmeler olabilir; örneğin şunlar:

* **Bulut kaynaklarının kullanılabilirliği** -bir iş çalışırken kullandığınız bulut işlem kaynaklarının hello türüne bağlı olarak, mümkün toorely sürekli makine kullanılabilirliğine olmayabilir. Durum işleme ve ilerleme işaret eden ortak teknikleri toohandle olası geçici hataları ve daha fazla gerekli bulut kaynaklarını kullanan alındığında denetleyin.
* **Veri erişimi** -veri erişim teknikleri sık NFS gibi Kurumsal kümelerinde hello bulutta özel yapılandırma gerekebilir. Ya da tooadopt farklı veri erişimi uygulamaları ve desenleri hello bulut için gerekebilir.
* **Veri taşıma** - işlem büyük miktarlarda verinin stratejileri gerekli toomove hello verileri bulut depolama ve toocompute kaynakları olan uygulamalar için. [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) gibi yüksek hızda şirket içi ve dışı karışık ağa gerek duyabilirsiniz. Ayrıca, bu verileri depolama ve erişme hakkında yasal, düzenleme ve ilke kısıtlamalarını dikkate alın.
* **Lisans** - hello satıcısı ile lisans için ticari uygulamaları denetleyin veya çalışan diğer kısıtlamalar hello bulut. Satıcıların tümü kullandıkça öde lisansı sunmaz. Çözümünüz için bir lisans sunucusu hello bulutta tooplan ihtiyacınız olabilir veya tooan şirket içi lisans sunucusuna bağlanın.

### <a name="big-compute-or-big-data"></a>Big Compute mü, yoksa Büyük Veri mi?
Big Compute ile büyük veri uygulamaları arasındaki çizgi bölerek hello her zaman NET değildir ve bazı uygulamalar her ikisi de özelliklerine sahip olabilir. Her ikisi de, çoğunlukla da bilgisayar kümelerinde çalışan büyük ölçekli hesaplamalardan oluşur. Ancak hello çözüm yaklaşımları ve Destek Araçları farklı olabilir.

• **Big Compute** CPU gücüne ve belleğe gibi mühendislik benzetimleri, finansal risk modelleme Bel tooinvolve uygulamalar ve dijital işleme eğilimlidir. Big Compute çözümünü Hello altyapısı ham tooperform hesaplama, özelleştirilmiş çok çekirdekli işlemcilere sahip bilgisayarlar ve özelleştirilmiş, yüksek hızlı ağ donanım tooconnect hello bilgisayarları içerebilir.

• **Büyük Veri**, tek bir bilgisayarla veya veritabanı yönetim sistemiyle yönetilemeyen yüksek miktarda verilerden oluşan veri analizi sorunlarını çözümler. büyük hacimli web günlükleri veya diğer iş zekası verileri bunun örneklerindendir. Büyük veri toorely daha fazla disk kapasitesine ve g/ç performansına fazla CPU gücü eğilimlidir. Apache Hadoop toomanage hello küme ve bölüm hello verileri gibi özel büyük veri araçlar vardır. (Azure HDInsight ve diğer Azure Hadoop çözümleri hakkında bilgi için bkz. [Hadoop](https://azure.microsoft.com/solutions/hadoop/).)

## <a name="compute-management-and-job-scheduling"></a>İşlem yönetimi ve iş zamanlama
Batch ve HPC uygulamalarının çalıştırılmasında çoğunlukla bir *Küme Yöneticisi'ni* ve *İş Zamanlayıcısı* toohelp kümelenmiş işlem kaynaklarının yönetilmesine ve hello işleri çalıştırma toohello uygulamaları ayırın. Bu işlevler ayrı araçlarla, tümleştirilmiş araçla veya hizmetle elde edilebilir.

* **Küme yöneticisi** - Sağlamalar, yayımlar ve yönetici işlem kaynakları (veya işlem düğümleri). Bir Küme Yöneticisi'ni yükleme, işletim sistemi görüntülerinin otomatikleştirebilir ve uygulamaların işlem düğümlerine toodemands göre işlem kaynaklarını ölçeklendirme ve hello düğümleri hello performansını izleme.
* **İş Zamanlayıcı** -hello kaynaklarını belirtir çalıştırıldığında (işlemci veya bellek gibi) bir uygulama ihtiyaçlarını ve hello koşulları. İş Zamanlayıcı bir iş kuyruğu tutar ve atanan öncelik veya başka özelliklere göre kaynakları toothem ayırır.

Kümeleme ve iş zamanlama araçları Windows ve Linux tabanlı kümeler için iyi tooAzure geçirebilirsiniz. Örneğin, Windows ve Linux HPC iş yükleri için Microsoft'un ücretsiz işlem kümesi çözümü olan [Microsoft HPC Paketi](https://technet.microsoft.com/library/cc514029), Azure'da çalışma için çeşitli seçenekler sunmaktadır. Torque ve SLURM gibi açık kaynaklı araçları toorun Linux kümeleri de oluşturabilirsiniz. Ticari kılavuz çözümleri tooAzure gibi getirebilirsiniz [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [IBM Spektrumun Symphony ve Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), ve [Univa Grid Engine](http://www.univa.com/products/grid-engine).

Aşağıdaki bölümlerde hello gösterildiği gibi işlem kaynakları Azure Hizmetleri toomanage yararlanmak ve işleri olmadan (veya ek olarak) geleneksel küme yönetim araçlarının zamanlama.

## <a name="scenarios"></a>Senaryolar
İşte üç yaygın senaryo toorun Big Compute iş yüklerini Azure'da mevcut HPC küme çözümlerini, Azure Hizmetleri veya hello iki birleşimini kullanarak. Her senaryoyu seçmeyle ilgili önemli kararlar listelenmiş olsa da bunlar pek kapsamlı değildir. Daha fazla çözümünüzde kullanabilir hello kullanabildiğiniz Azure hizmetleri hakkında hello makalenin ilerideki bölümlerindedir.

| Senaryo | Neden seçiliyor? |
| --- | --- | --- |
| **HPC küme tooAzure veri bloğu**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Daha fazla bilgi edinin:<br/>• [TooAzure çalışan örnekleri HPC paketi ile veri bloğu](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [HPC Paketi ile karma işlem kümesi ayarlama](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [TooAzure HPC paketi ile toplu veri bloğu](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• [Microsoft HPC Paketini](https://technet.microsoft.com/library/cc514029) veya başka şirket içi kümesini karma bir çözümde ek Azure kaynaklarıyla birleştirin.<br/><br/>• Bir hizmet (PaaS) sanal makine örnekleri (şu anda yalnızca Windows Server) Big Compute iş yüklerini toorun platformunda genişletir.<br/><br/>• İsteğe bağlı bir Azure sanal ağını kullanarak şirket içi lisans sunucusuna veya veri deposuna erişin |
| **HPC kümesini Azure’da tamamen oluşturma**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Daha fazla bilgi edinin:<br/>• [Azure’de HPC kümesi çözümleri](big-compute-resources.md)<br/><br/> |• Uygulamalarınızı ve küme araçlarınızı standart veya özel Windows ya da Linux hizmet olarak altyapı (IaaS) sanal makinelerine hızlı ve tutarlı bir şekilde dağıtın.<br/><br/>• Tercih ettiğiniz çözüm zamanlama hello işi kullanarak çeşitli Big Compute iş yüklerini çalıştırın.<br/><br/>• Ağ ve depolama toocreate tam bulut tabanlı çözümlerle dahil olmak üzere ek Azure Hizmetleri kullanın. |
| **Paralel uygulama tooAzure ölçeklendirme**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Daha fazla bilgi edinin:<br/>• [Azure Batch temel bilgileri](batch-technical-overview.md)<br/><br/>• [.NET için hello Azure Batch kitaplığını kullanmaya başlama](batch-dotnet-get-started.md) |• Geliştirin [Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale havuzları Windows veya Linux sanal makineleri üzerinde çeşitli Big Compute iş yüklerini toorun çıkışı.<br/><br/>• Bir Azure platformu hizmet toomanage dağıtımı ve otomatik ölçeklendirmeyi sanal makineler, iş zamanlaması, olağanüstü durum kurtarma, veri taşıma, bağımlılık yönetimi ve uygulama dağıtımı kullanın. |

## <a name="azure-services-for-big-compute"></a>Big Compute için Azure Hizmetleri
Merhaba işlem, veri, ağ ve ilgili hizmetler, birleştirebilirsiniz Big Compute çözümleri ve iş akışları hakkında daha fazla bilgi aşağıdadır. Azure hizmetleri hakkında ayrıntılı yönergeler için bkz, Azure Hizmetleri hello [belgelerine](https://azure.microsoft.com/documentation/). Merhaba [senaryoları](#scenarios) bu makalenin önceki bölümlerinde bu hizmetleri kullanmanın bazı yollarını gösterir.

> [!NOTE]
> Azure düzenli olarak senaryonuz için yararlı olabilecek yeni hizmetler sunar. Sorularınız varsa, [Azure iş ortağı](https://pinpoint.microsoft.com/en-US/search?keyword=azure) ile görüşün veya *bigcompute@microsoft.com* adresine e-posta gönderin.
> 
> 

### <a name="compute-services"></a>İşlem hizmetleri
Azure işlem Hizmetleri Big Compute çözümü ve hello farklı işlem Hizmetleri farklı senaryolar için avantaj teklif hello çekirdek oluşturulur. Temel düzeyde, bu hizmetleri, uygulamaları toorun Azure Windows Server Hyper-V teknolojisini kullanarak sağladığı sanal makine tabanlı işlem örneklerini üzerinde farklı modu sunmaktadır. Bu örnekler standart ve özel Linux ve Windows işletim sistemlerinin ve araçlarını çalıştırabilir. Azure, CPU çekirdekleri, bellek, disk kapasitesi ve diğer özelliklerin farklı yapılandırmalarıyla size [örnek boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) seçimi sağlar. Gereksinimlerinize bağlı olarak, çekirdek hello örnekleri toothousands ölçeklendirme ve daha az kaynak gerektiğinde de ölçeklendirmeyi azaltın.

> [!NOTE]
> Hello Azure yararlanmak [işlem yoğunluklu örnekler H-serisi hello gibi](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove hello performans ve ölçeklenebilirlik HPC iş yüklerinin. Bu örnekler, düşük gecikme ve yüksek üretimli bir uygulama ağı gerektiren paralel MPI uygulamalarını da destekler. Ayrıca verilmektedir [N-serisi](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) NVIDIA GPU tooexpand hello Azure bilgi işlem ve görselleştirme senaryolarda aralığını olan VM'ler.  
> 
> 

| Hizmet | Açıklama |
| --- | --- |
| **[Sanal makineler](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Microsoft Hyper-V teknolojisi kullanarak işlem hizmet olarak altyapısı (IaaS) sağlarlar<br/><br/>• Tooflexibly sağlama etkinleştirmek ve hello standart Windows Server veya Linux görüntü kalıcı bulut bilgisayarlarını yönetmek [Azure Marketi](https://azure.microsoft.com/marketplace/), veya sağladığınız görüntüler ve veri diskleri<br/><br/>• Dağıtılması ve olarak yönetilen [VM ölçek kümesi](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild büyük ölçekli aynı sanal makinelerden otomatik olarak otomatik ölçeklendirmeyi azaltın veya tooincrease kapasiteyle Hizmetleri<br/><br/>• Şirket içi işlem kümesi araçlarını ve uygulamalarını çalıştırırlar hello bulut<br/><br/> |
| **[Bulut hizmetleri](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Çalışan rolü örneklerinde, Windows Server’ın bir sürümünü çalıştıran ve tamamen Azure tarafından yönetilen sanal makineler olan Big Compute uygulamalarını çalıştırabilirler<br/><br/>• Düşük yönetici desteğiyle hizmet olarak platform (PaaS) modelinde çalışan ölçeklenebilir, güvenli uygulamaları etkinleştirirler<br/><br/>• Ek araçlar veya şirket içi HPC Kümesi çözümleriyle geliştirme toointegrate gerektirebilir |
| **[Batch](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Tam olarak yönetilen bir hizmette büyük ölçekli paralel ve toplu işlem iş yüklerini çalıştırır<br/><br/>• Sanal makinelerin iş zamanlamasını ve yönetilen havuzun otomatik ölçeklendirilmesini sağlar<br/><br/>• Bir hizmet olarak toobuild ve çalışma uygulamaları geliştiriciler verir veya Bulut-uygulamalarınız etkinleştir<br/> |

### <a name="storage-services"></a>Storage hizmetleri
Big Compute çözümü tipik olarak bir dizi girdi verisi üzerinde çalışır ve sonuçları için veri üretir. Hello Azure storage Hizmetleri Big Compute çözümlerinde kullanılan bazıları şunlardır:

* [Blob, tablo ve kuyruk depolama](https://azure.microsoft.com/documentation/services/storage/) - Büyük miktarda yapılandırılmamış verileri, SQL dışı verileri, iş akışı ve iletişim iletilerini bu sırayla yönetin. Örneğin, büyük teknik veri kümelerinde ya da hello girdi görüntülerini blob depolama kullanabilir veya uygulamanızın işlediği medya dosyaları. Çözümdeki uyumsuz iletişim için kuyrukları kullanabilirsiniz. Bkz: [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).
* [Azure File storage](https://azure.microsoft.com/services/storage/files/) -paylaşımları ortak dosyaları ve Azure kullanarak verileri Merhaba, bazı HPC küme çözümleri için gerekli olan standart SMB protokolü.
* [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) -hello bulut, toplu işlemi için gerçek zamanlı, kullanışlı ve etkileşimli analiz için ölçekte bir Apache Hadoop dağıtılmış dosya sistemi sağlar.

### <a name="data-and-analysis-services"></a>Veri ve analiz hizmetleri
Bazı Big Compute senaryoları büyük ölçekli veri akışlarından oluşur ya da daha fazla işleme veya analiz gereken veriler üretir. Azure aşağıdakiler dahil birkaç veri ve analiz hizmeti sunar:

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) - Şirket içi, bulut tabanlı ve İnternet veri depolarına ait verilerle birleşen, yığılan ve dönüştüren veri temelli iş akışlarını (işlem hattı) derler.
* [SQL veritabanı](https://azure.microsoft.com/documentation/services/sql-database/) -yönetilen bir hizmette Microsoft SQL Server ilişkisel veritabanı yönetim sisteminin hello anahtar özellikleri sağlar.
* [Hdınsight](https://azure.microsoft.com/documentation/services/hdinsight/) - dağıtır ve hazırlar hello Windows Server veya Linux tabanlı Apache Hadoop kümelerini toomanage bulut, çözümleme ve raporlama büyük verileri.
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) - Tam yönetilen bir hizmette tahmine dayalı analitik çözümleri bulutta oluşturmanıza, test etmenize, çalıştırmanıza ve yönetmenize yardımcı olur.

### <a name="additional-services"></a>Ek hizmetler
Big Compute çözümünüze diğer Azure Hizmetleri tooconnect tooresources şirket içi gerekebilir veya diğer ortamlarda. Örneklere şunlar dahildir:

* [Sanal ağ](https://azure.microsoft.com/documentation/services/virtual-network/) -Azure tooconnect Azure kaynaklarını tooeach diğer veya tooyour şirket içi veri merkezi içinde mantıksal olarak yalıtılmış bir bölüm oluşturur. Şirket içi ve dışı karışık bir sanal ağ ile Big Compute uygulamaları şirket içi verilere, Active Directory hizmetlerine ve lisans sunucularına erişebilir
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) - Microsoft veri merkezleri ile şirketinizde veya bir birlikte bulundurma ortamında bulunan altyapı arasında özel bir bağlantı oluşturur. ExpressRoute hello Internet daha yüksek güvenlik, daha fazla güvenilirlik, yüksek hız ve genel bağlantılara daha düşük gecikme sağlar.
* [Hizmet veri yolu](https://azure.microsoft.com/documentation/services/service-bus/) -başka bir bulut platformunda ya da bir veri merkezinde Azure üzerinde bulundukları olup olmadığını toocommunicate veya exchange verileri, uygulamalar için birçok mekanizma sağlar.

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [Batch ve HPC için teknik kaynaklar](big-compute-resources.md) toofind teknik kılavuz toobuild çözümünüzü.
* Azure seçeneklerinizi Cycle Computing, Rescale ve UberCloud dahil olmak üzere iş ortaklarınızla tartışın.
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) ve [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088) tarafından sağlanan Azure Big Compute çözümleri hakkında okuyun.
* Merhaba Hello son Duyurular için bkz: [Microsoft HPC ve Batch ekip blogu](http://blogs.technet.com/b/windowshpc/) ve hello [Azure blogu](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png

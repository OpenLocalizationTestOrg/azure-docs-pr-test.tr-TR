---
title: "Azure Iaas diskler için yedekleme ve olağanüstü durum kurtarma | Microsoft Docs"
description: "Bu makalede, biz yedekleme ve olağanüstü durum kurtarma (DR) Iaas sanal makineleri (VM'ler) için planlama açıklanacaktır ve Azure diskleri. Bu belge hem yönetilen hem de yönetilmeyen diskler kapsar"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 03d38bc3383b5fd39eca5ca67c315b34b98f0c39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Azure Iaas diskler için yedekleme ve olağanüstü durum kurtarma

Bu makalede, biz yedekleme ve olağanüstü durum kurtarma (DR) Iaas sanal makineleri (VM'ler) için planlama açıklanacaktır ve Azure diskleri. Bu belge, yönetilen ve yönetilmeyen diskleri kapsar.

Biz öncelikle yerel arızaya karşı koruma sağlamak yardımcı olan yerleşik hata toleransı özellikleri hakkında Azure platformu konuşun. Biz sonra tam olarak yerleşik özellikleri tarafından kapsanan olağanüstü durum senaryolar bu belge tarafından gönderilen ana konu olduğu ele alacağız. Burada farklı yedekleme ve kurtarma konuları uygulayabilir iş yükü senaryoları bazı örnekleri de göstereceğiz. Biz ardından olası çözümler için Iaas disklerini DR gözden geçirin. 

## <a name="introduction"></a>Giriş

Azure platformu yedeklik ve hataya dayanıklılık için çeşitli yöntemler oluşabilir yerelleştirilmiş donanım hatalarından müşterilerin korunmasına yardımcı olmak için kullanır. Bu sunucu üzerinde bir sanal disk için verilerin bir kısmını ya da bir SSD veya HDD hatalarının depolayan bir Azure depolama sunucu makinesindeki sorunlar yerel hataları içerebilir. Bu tür yalıtılmış donanım bileşeni arızalarına normal işlemler sırasında oluşabilir ve platform bu hatalarına dayanıklı olacak şekilde tasarlanmıştır. Ana afetler hataları veya depolama sunucuları veya tam bir veri merkezinde çok sayıda inaccessibility neden olabilir. VM'ler ve diskleri yerelleştirilmiş hatalarından normalde korunur, ancak İş yükünüzün VM ve diskleri etkileyebilecek bölge çapında geri dönülemez arızasına karşı (örneğin, büyük bir felaket) korumak ek adımlar gereklidir.

Platform hataları olasılığını ek olarak, müşteri uygulaması veya veri sorunlar oluşabilir. Örneğin, uygulamanızın yeni bir sürümünü yanlışlıkla verileri değiştirme sonu kalmasına neden olabilir. Bu durumda, uygulama ve veri bilinen son iyi duruma içeren bir önceki sürüme geri isteyebilirsiniz. Bu, düzenli yedeklemeler koruma gerektirir.

Bölgesel olağanüstü durum kurtarma için farklı bir bölgeye, Iaas VM diskleri yedekleme gerekir. 

Şimdi biz yedekleme ve kurtarma seçeneklerini Ara önce yerelleştirilmiş hata işleme için birkaç yöntem kullanılabilir olduðunu.

### <a name="azure-iaas-resiliency"></a>Azure Iaas dayanıklılık

*Dayanıklılık* donanım bileşenleri ortaya normal hata toleransı başvuruyor. Dayanıklılık, arızalardan kurtarmak ve çalışmaya devam yeteneğidir. Hataları önleme, ancak hataları kapalı kalma süresi veya veri kaybı önler şekilde yanıt verme hakkında değil. Uygulamaya bir hatasının ardından tam çalışır bir duruma geri dönmek için dayanıklılık belirtilir. Azure sanal makineleri ve diskleri için genel donanım hataları dayanıklı olacak şekilde tasarlanmıştır. Bize Azure Iaas platform bu dayanıklılık nasıl sağladığını adresindeki arayın.

Bir sanal makine çoğunlukla iki bölümden oluşur: (1) bir işlem sunucusu ve (2 kalıcı diskler. Her ikisi de bir sanal makinenin hata toleransı etkiler.

VM barındırıldığı Azure işlem ana bilgisayar sunucusu (Bu nadir) bir donanım hatası yaşarsa, Azure otomatik olarak VM başka bir sunucuya geri yüklemek için tasarlanmıştır. Bu durumda, yeniden başlatma yaşar ve VM yedekleme bir süre sonra olacaktır. Azure otomatik olarak bu tür donanım hataları algılar ve VM müşteri olabildiğince çabuk kullanılabilir olacak sağlamaya yardımcı olmak için kurtarma yürütür.

Iaas disklerini ilgili veri dayanıklılığı kalıcı depolama platform için kritik öneme sahiptir. Azure müşterilerin önemli iş uygulamaları Iaas'da çalışan sahip ve veri kalıcılığı üzerinde bağlıdır. Bu üç yedek kopyaları Iaas diskleri için Azure tasarımları koruma yerel olarak depolanan verilerin yerel hatalarına karşı yüksek dayanıklılık sağlama. Diskinizin tutan donanım bileşenleri biri başarısız olursa, disk isteklerini desteklemek için iki ek kopyalarını olduğundan, VM etkilenmez. Bir disk destekleyen iki farklı donanım bileşenleri (hangi çok nadir olur) aynı anda başarısız olsa bile düzgün çalışır. Üç kopyaları biri kullanılamaz hale gelirse biz her zaman üç çoğaltmaları bakımını sağlamak üzere Azure Storage hizmeti otomatik olarak arka planda verileri yeni bir kopyasını olarak çoğaltılır. Bu nedenle, bu hataya dayanıklılık için Azure disklerle RAID kullanmak için gerekli olmamalıdır. Basit bir RAID 0 yapılandırma diskleri bölmek için gerekirse daha büyük birimleri oluşturmak yeterli olmalıdır.

Bu mimari nedeniyle **Azure Kurumsal düzeyde tutarlı bir şekilde teslim Iaas için dayanıklılık diskleri, bir endüstri lideri ile sıfır % [değer yıllık hata oranı](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Yerelleştirilmiş donanım hataları işlem üzerinde barındıran veya depolama platform tarafından ele VM için geçici olarak kullanım dışı kalması sonucunda bazen olabilir. [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) VM kullanılabilirlik. Azure, endüstri lideri SLA Premium depolama diski kullanan tek VM örnekleri için de sağlar.

Bir disk veya VM geçici kullanılamama nedeniyle kapalı kalma süresini uygulama iş yüklerini korumak için müşteriler yararlanabilirsiniz [kullanılabilirlik kümeleri](../../virtual-machines/windows/manage-availability.md). Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makine uygulama için artıklık sağlar. Azure daha sonra bu sanal makineleri ve diskleri ayrı hata etki alanlarında farklı güç, ağ ve sunucu bileşenleri ile oluşturur. Bu nedenle, yerelleştirilmiş donanım hataları genellikle kümedeki birden çok VM aynı anda uygulamanız için yüksek düzeyde kullanılabilirlik sağladığınızdan etkilemez. Yüksek kullanılabilirlik gerekli olduğunda kullanılabilirlik kümeleri kullanmak iyi bir uygulama olarak kabul edilir. Daha fazla bilgi için aşağıdaki ayrıntılı olağanüstü durum kurtarma yönlerini bakın.

### <a name="backup-and-disaster-recovery"></a>Yedekleme ve olağanüstü durum kurtarma

Olağanüstü Durum Kurtarma (DR) olan kaynaklı nadir ancak büyük olayların kurtarabilirsiniz: tüm bölgeyi etkiler hizmet kesintisi gibi geçici olmayan, geniş ölçekli hataları. Olağanüstü durum kurtarma, veri yedekleme ve arşivleme içerir ve bir veritabanını yedekten geri yükleme gibi el ile müdahale içerebilir.

Yerelleştirilmiş hata karşı yerleşik koruma Azure platformun VM'ler/diskleri büyük ölçekli kesintileri neden önemli afetler durumunda tam koruma. Bu bir hortum, deprem, yangın veya büyük ölçekli donanım birim hataları tarafından ziyaret bir veri merkezi gibi geri dönülemez olaylarını içerir. Ayrıca, uygulama veya veri sorunları nedeniyle hataları karşılaşabilirsiniz.

Iaas iş yüklerinizi kesintilere karşı korunmasına yardımcı olmak için artıklık ve kurtarmayı etkinleştirmek için yedeklemeler için planlamanız gerekir. Olağanüstü durum kurtarma için artıklık ve yedekleme birincil sitesinden farklı bir coğrafi konumda planlamanız gerekir. Bu, yedekleme ilk olarak VM veya disklerin etkilenen aynı olayı tarafından etkilenmez sağlamaya yardımcı olur. Daha fazla bilgi için bkz: [olağanüstü durum kurtarma uygulamaları için Azure üzerinde oluşturulmuş](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

DR konularınızdan aşağıdaki açıları içerebilir:

1. Yüksek kullanılabilirlik (HA) önemli bir kapalı kalma süresi olmadan sağlıklı bir durumda çalışmaya devam etmesini uygulama özelliğidir. "Sağlıklı durumuna göre" biz esnek bir uygulamasıdır ve kullanıcıların uygulamaya bağlanmak ve onlarla etkileşime anlamına gelir. Belirli görev açısından kritik uygulamalar ve veritabanları bile platform hatası olduğunda her zaman kullanılabilir olması için gerekli olabilir. Bu iş yükleri için artıklık verilerin yanı sıra uygulama için planlama gerekebilir.

2. Veri dayanıklılığı: Bazı durumlarda, olağanüstü durum oluşması durumunda verilerin korunduğundan ana göz önünde bulundurarak emin olmaktır. Bu nedenle, bir yedekleme verilerinizin farklı bir sitede gerekebilir. Bu tür iş yükleri için tam yedekleme uygulama ancak disklerin normal yedekleme için gerekmeyebilir.

## <a name="backup-and-dr-scenarios"></a>Yedekleme ve kurtarma senaryoları

Uygulama iş yükü senaryoları için ve olağanüstü durum kurtarma planlama konuları, bazı tipik örnekler bakalım.

### <a name="scenario-1-major-database-solutions"></a>Senaryo 1: Birincil veritabanı çözümleri

Bir üretim veritabanı sunucusuna SQL Server veya yüksek kullanılabilirlik destekleyebilir Oracle gibi göz önünde bulundurun. Kritik üretim uygulamaların ve kullanıcıların bu veritabanında bağlıdır. Bu sistem için olağanüstü durum kurtarma planı aşağıdaki gereksinimleri desteklemesi gerekebilir:

1. Verilerin korunan ve kurtarılabilir olması gerekir.
2.  Sunucusunun kullanılabilir olması gerekir.

Bu, yedek olarak farklı bir bölgede veritabanının bir kopyasını koruyarak gerektirebilir. Sunucu kullanılabilirliği ve veri kurtarma gereksinimlerine bağlı olarak, çözümü etkin-etkin veya etkin-Pasif bir kopya sitesinden veri düzenli çevrimdışı yedeklemeler için çeşitli işlemleri ifade edebilir. SQL Server ve Oracle gibi ilişkisel veritabanları çoğaltma için çeşitli seçenekler sağlar. SQL Server için [SQL Server Always On kullanılabilirlik grupları](https://msdn.microsoft.com/library/hh510230.aspx) yüksek kullanılabilirlik için kullanılabilir.

MongoDB gibi NoSQL veritabanlarını da destek [çoğaltmaları](https://docs.mongodb.com/manual/replication/) artıklık için. Yüksek kullanılabilirlik çoğaltmaları kullanılabilir.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Senaryo 2: Küme yedek VM'ler

Artıklık sağlamak ve Yük Dengeleme sanal makineleri bir küme tarafından işlenen bir iş yükü göz önünde bulundurun. Bir örnek bir bölgeye dağıtılmış bir Cassandra kümesi olabilir. Bu tür bir mimari zaten bu bölgedeki artıklık yüksek düzeyde sağlar. Ancak, iş yükü bölgesel bir düzey arızasına karşı korumak için küme iki bölgeler arasında yayılmak veya başka bir bölgeye düzenli yedeklemeler yapma düşünmelisiniz.

### <a name="scenario-3-iaas-application-workload"></a>Senaryo 3: Iaas uygulama iş yükü

Bu, bir Azure VM üzerinde çalışan bir tipik bir üretim iş yükünü olabilir. Örneğin, bir web sunucusu veya dosya sunucusu içeriği ve diğer kaynakları bir sitenin bulunduran olabilir. Ayrıca, verileri, kaynaklar ve uygulama durumunu VM disklerinde depolanan bir VM üzerinde çalışan bir özel olarak geliştirilmiş iş uygulaması de olabilir. Bu durumda, düzenli aralıklarla yedekleri alması emin olmak önemlidir. Yedekleme sıklığı VM iş yükü doğasına bağlı olmalıdır. Örneğin, uygulama her gün çalışır ve veri değiştirir, yedekleme saatte gerçekleştirilmelidir.

Başka bir örnek diğer kaynaklardan veri çekmek raporlama sunucusudur ve birleşik raporları oluşturur. Bu VM veya diskleri kaybı raporları kaybına neden. Ancak, raporlama işlemi yeniden çalıştırın ve çıktıyı yeniden oluşturmak mümkün olabilir. Bu durumda, Raporlama sunucusunda veri parçası kaybetme dayanıklılık daha yüksek düzeyde olabilir şekilde Raporlama sunucusu olağanüstü durum ile bile ulaşılırsa veri kaybı gerçekten yok. Bu durumda, daha az sık gerçekleştirilen yedeklemeler, maliyetini azaltmak için bir seçenek değil.

### <a name="scenario-4-iaas-application-data-issues"></a>Senaryo 4: Iaas uygulama verileri sorunları

Hesaplar, korur ve fiyatlandırma bilgileri gibi kritik ticari verileri hizmet veren bir uygulamaya sahip. Uygulamanızı yeni bir sürümü yanlış fiyatlandırma hesaplanan ve platform tarafından sunulan varolan ticaret verileri bozuk bir yazılım hata vardı. Burada, ilk uygulama ve verilerin önceki sürümüne geri dönmek için iyi davranış biçimini olacaktır. Bu ayarı etkinleştirmek için sisteminizi düzenli yedeklemelerini alın.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Olağanüstü durum kurtarma çözümü: Azure yedekleme hizmeti

[Azure Backup hizmeti](https://azure.microsoft.com/services/backup/) ile çalışır ve yedekleme ve kurtarma için kullanılabilir olan [yönetilen diskleri](../../virtual-machines/windows/managed-disks-overview.md) yanı [yönetilmeyen diskleri](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). Bir yedekleme işi zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri oluşturabilirsiniz. 

Kullanırsanız [Premium depolama diskleri](storage-premium-storage.md), [yönetilen diskleri](../../virtual-machines/windows/managed-disks-overview.md), veya diğer disk türlerinde [yerel olarak yedekli depolama (LRS)](storage-redundancy.md#locally-redundant-storage) seçeneği, onu önemlidir düzenli DR yedeklemeler yararlanmak özellikle. Azure yedekleme kurtarma Hizmetleri kasanız uzun vadeli bekletme için verileri depolar. Seçin [coğrafi olarak yedekli depolama (GRS)](storage-redundancy.md#geo-redundant-storage) yedekleme kurtarma Hizmetleri kasası için seçeneği. Yedeklemeleri bölgesel olağanüstü durumlarını koruma için farklı bir Azure bölgesine çoğaltılır ilişkilendirilmesini sağlar.

İçin [yönetilmeyen diskleri](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), Iaas disklerini LRS depolama türü kullanır, ancak Azure yedekleme için kurtarma Hizmetleri kasası GRS seçeneğiyle etkinleştirildiğinden emin olun.

**Kullanırsanız [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) seçeneği yönetilmeyen disklerinizi, yine için yedekleme ve kurtarma için tutarlı anlık görüntüler gerekir.** Ya da kullanmalıdır [Azure Backup hizmeti](https://azure.microsoft.com/services/backup/) veya [tutarlı anlık görüntüleri](#alternative-solution-consistent-snapshots).

DR çözümleri bir özeti verilmiştir.

| Senaryo | Otomatik çoğaltma | DR çözümü |
| --- | --- | --- |
| *Premium depolama diskleri* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilen Diskler* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilmeyen LRS diskleri* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilmeyen GRS diskleri* | Çapraz bölge ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Tutarlı anlık görüntüler](#alternative-solution-consistent-snapshots) |
| *Yönetilmeyen RA-GRS diskleri* | Çapraz bölge ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Tutarlı anlık görüntüler](#alternative-solution-consistent-snapshots) |

Yüksek kullanılabilirlik en iyi göre karşılanmış yönetilen disklerin bir kullanılabilirlik grubunda yanı sıra Azure Backup aracılığıyla. Yönetilmeyen diskler kullanıyorsanız, Azure Backup DR için kullanmaya devam edebilirsiniz. Azure Yedekleme'yi yapamıyorsanız, ardından alma [tutarlı anlık görüntüleri](#alternative-solution-consistent-snapshots) açıklandığı gibi daha sonraki bir bölüme bir alternatif için yedekleme ve kurtarma çözümüdür.

Seçimlerinizi yüksek kullanılabilirlik için yedekleme ve uygulama veya altyapı düzeylerinde DR temsil olarak aşağıda:

| *Düzeyi* | Yüksek kullanılabilirlik   | Yedekleme / DR |
| --- | --- | --- |
| *Uygulama* | Her zaman açık SQL | Azure Backup |
| *Altyapı*  | Kullanılabilirlik Kümesi  | GRS ile tutarlı anlık görüntüler |

### <a name="using-the-azure-backup-service"></a>Azure Backup hizmeti kullanma

[Azure yedekleme](../../backup/backup-azure-vms-introduction.md) Azure kurtarma Hizmetleri Kasası'na Windows veya Linux çalıştıran, sanal makineleri yedekleyebilirsiniz. Yedekleme ve geri yükleme iş açısından kritik verilerin veri üretmek uygulamaları çalıştırırken, iş açısından kritik verilerin yedeklenmesi gereken olgusu karmaşık. Bu sorunu çözmek için Azure Backup veri depolama için doğru yazıldığından emin olmak için birim gölge hizmeti (VSS) kullanarak uygulamayla tutarlı yedeklemeler Microsoft iş yükleri için sağlar. Linux işlevselliği VSS'ye eşdeğer olmadığından Linux VM'ler için yalnızca dosya tutarlı yedeklemeler olasılığı vardır

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Azure Backup, zamanlanan saatte bir yedekleme işi başlattığında, zaman içinde nokta anlık almak için VM'de yüklü yedekleme uzantısını tetikler. Bir anlık görüntü kapatmak zorunda kalmadan sanal makinenin disklerinin tutarlı bir anlık görüntü almak için VSS koordinasyon alınır. VM yedekleme uzantısına tüm disklerin tutarlı anlık önce tüm yazma işlemlerini aktarır. Anlık görüntü oluşturulduğunda sonra verileri Azure yedekleme tarafından yedekleme Kasası'na aktarılır. Yedekleme işlemini daha verimli hale getirmek için hizmet tanımlar ve yalnızca son yedeklemeden sonra değiştirilen veri blokları aktarır.


Geri yüklemek için Azure Backup aracılığıyla kullanılabilir yedeklemeleri görüntüleyebilir ve geri yükleme başlatmak. Oluşturma ve Azure yedeklemeleri aracılığıyla geri [Azure portal](https://portal.azure.com/), [PowerShell kullanarak](../../backup/backup-azure-vms-automation.md ), veya kullanarak [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install). Daha fazla bilgi için Azure yedekleme konusuna bakın.

### <a name="steps-to-enable-backup"></a>Yedeklemeyi etkinleştirmek için adımları

Aşağıdaki adımları kullanarak, Vm'lerde yedeklerini etkinleştirmek için genellikle kullanılan [Azure Portal](https://portal.azure.com/). Tam senaryonuza bağlı olarak bazı farklılıklar olacaktır. Başvurmak [Azure Backup](../../backup/backup-azure-vms-introduction.md) tam Ayrıntılar için belgelerine bakın. Azure ayrıca yedekleme [yönetilen diske sahip sanal makineleri destekleyen](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Bir kurtarma Hizmetleri kasası için aşağıdaki adımları kullanarak bir VM oluşturun:

    a.  Kullanarak [Azure portal](https://portal.azure.com/)tüm kaynaklara göz atın ve "Kurtarma Hizmetleri kasalarının" bulunamıyor.

    b.  Kurtarma Hizmetleri kasaları menüsünde Ekle'yi tıklatın ve VM ile aynı bölgede yeni bir kasa oluşturmak için aşağıdaki adımları izleyin. Örneğin, VM'yi Batı ABD bölgesi ise, Batı ABD için kasa seçin.

2.  Yeni oluşturulan kasa için depolama çoğaltma doğrulayın. Bunu yapmak için kurtarma Hizmetleri kasaları dikey penceresinden kasaya erişim ve ayarları/yedekleme yapılandırması gidin. GRS seçeneği varsayılan olarak seçili olduğundan emin olun. Bu, kasanızı ikincil veri merkezine otomatik olarak çoğaltılır güvence altına alır. Örneğin, Batı ABD, kasaya Doğu ABD için otomatik olarak çoğaltılır.

3.  Yedekleme ilkesi yapılandırın ve aynı kullanıcı Arabiriminden VM seçin.

4.  Backup Aracısı VM üzerinde yüklü olduğundan emin olun. VM Azure galerisinde görüntü kullanarak oluşturulmuşsa, Yedekleme aracısı zaten yüklüdür. (Diğer bir deyişle, özel bir görüntü kullanıyorsanız) Aksi durumda, yönergeleri kullanın [VM Aracısı sanal makineye yükleme](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  VM yedekleme hizmetinin çalışması için ağ bağlantısı verdiğinden emin olun. Bu yönergeleri izleyin [ağ bağlantınızı](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Yukarıdaki adımları tamamladıktan sonra yedekleme İlkesi belirtildiği gibi düzenli aralıklarla yedekleme çalıştırın. Gerekirse ilk yedekleme Azure portalındaki kasa Panosu el ile tetikleyebilirsiniz.

Azure komut dosyalarını kullanarak yedekleme otomatikleştirmek için lütfen [VM yedekleme için PowerShell cmdlet'leri](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Kurtarma için adımları

Onarmak veya VM yeniden ihtiyacınız varsa, yedekleme kurtarma noktalarının kasadaki birinden VM geri yükleyebilirsiniz. Birkaç kurtarmayı gerçekleştirmek için farklı seçenekler vardır:

1.  Yeni bir VM, yedeklenen VM olarak zaman içinde nokta gösterimini oluşturabilirsiniz.

2.  Diskleri geri yükleyin ve özelleştirin ve geri yüklenen VM yeniden oluşturmak için VM şablonu kullanın. 

Yönergeler için bkz: [kullanım Azure portalı sanal makineleri geri](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). Belge ayrıca birincil veri merkezinde bir olağanüstü durum söz konusu olduğunda, coğrafi olarak yedekli yedekleme kasası kullanarak eşleştirilmiş veri merkezine yedeklenen sanal makineleri geri yüklemek için belirli adımlar açıklanmaktadır. Bu durumda, Azure Backup geri yüklenen sanal makine oluşturmak için ikincil bölgesinden işlem hizmeti kullanır.

PowerShell için de kullanabilirsiniz [VM geri](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) veya [yeni bir sanal makineden oluşturma geri diskleri](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatif çözüm: Tutarlı anlık görüntüler

Azure Yedekleme hizmetini kullanmak erişemiyorsanız anlık görüntülerini kullanarak kendi yedekleme mekanizması uygulayabilirsiniz. Bir VM tarafından kullanılan tüm diskler için tutarlı anlık görüntüler oluşturmak ve ardından bu anlık görüntülerin başka bir bölgeye çoğaltmak karmaşıktır. Bu nedenle, Azure Backup hizmeti özel çözüm oluşturma değerinden daha iyi bir seçenek yararlanarak göz önünde bulundurur. RA-GRS/GRS depolama için diskleri kullanırsanız, anlık görüntüler bir ikincil veri merkezine otomatik olarak çoğaltılır. LRS depolama için diskleri kullanırsanız, kendiniz veri çoğaltmak gerekir. Daha fazla bilgi için bkz: [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](../../virtual-machines/windows/incremental-snapshots.md).

Bir nesne belirli bir noktada bir gösterimini zaman içinde bir anlık görüntüdür. Anlık isteğe bağlı olarak veri için artımlı boyutu ayrı tutma faturalama uygulanabilir. Daha fazla bilgi için bkz: [blob anlık görüntü](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-the-vm-is-running"></a>VM çalışırken anlık görüntüleri oluşturma

VM çalışıyorsa, herhangi bir zamanda bir anlık görüntü alabilir, ancak hala disklere akıtılan veri yoktur ve anlık görüntüleri uçuş modunda olan kısmi işlemleri içerebilir. Söz konusu birden çok disk varsa, ayrıca, farklı disklerin anlık görüntüleri farklı zamanlarda bu anlık görüntüleri Eşgüdümlü olmayabilir yani oluşmuş olabilir. Bu değişikliği yedekleme sırasında yapılmışsa, dosya bozuk şeritli birimler için özellikle sorunlu oluşturur.

Bu durumu önlemek için yedekleme işlemi aşağıdaki adımları uygulamanız gerekir:

1.  Tüm disklerin dondurma

2.  Bekleyen tüm yazma işlemlerini boşaltmaya

3.  Ardından, [blob anlık görüntü](../blobs/storage-blob-snapshots.md) tüm diskler için

SQL Server gibi bazı Windows uygulamaları uygulama tutarlı yedeklemeler oluşturmak için VSS aracılığıyla koordineli bir yedekleme mekanizması sağlar. Linux üzerinde dosya tutarlı yedeklemeler, ancak değil uygulamayla tutarlı anlık görüntüleri sağlar diskleri düzenlemekten fsfreeze gibi bir araç kullanabilirsiniz. Bu karmaşık bir işlemdir, bu nedenle ve kullanmayı düşünmelisiniz [Azure yedekleme](../../backup/backup-azure-vms-introduction.md) veya bu zaten uygulayan bir üçüncü taraf yedekleme çözümünün.

Yukarıdaki işlem VM belirli bir zaman içinde nokta görünümünü temsil eden tüm VM diskleri için Eşgüdümlü anlık görüntü koleksiyonu neden olur. VM için bir yedekleme geri yükleme noktası budur. Zamanlanan aralıklarla düzenli yedeklemeler oluşturmak için bu işlemi yineleyebilirsiniz. Aşağıdaki adımları için bkz: [yedeklemeler başka bir bölgeye kopyalama](#copy-the-snapshots-to-another-region) DR için.

### <a name="creating-snapshots-while-the-vm-is-offline"></a>VM çevrimdışı durumdayken anlık görüntüleri oluşturma

Tutarlı yedeklemeler oluşturmak için başka bir seçenek VM kapatma ve her disk blob anlık görüntüleri alma. Bu denetleyici çalışan bir VM anlık kolaydır, ancak birkaç dakika kalma süresi gerekir. Bu işlem, şu adımları izleyin:

1. VM kapatma.

2. Bir anlık görüntü yalnızca birkaç saniye sürer her VHD BLOB oluşturun.

    Bir anlık görüntü oluşturmak için kullanabileceğiniz [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), [Azure Storage Rest API'sini](https://msdn.microsoft.com/library/azure/ee691971.aspx), [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install), veya gibi Azure Storage istemci kitaplıklarından birini [.NET için depolama istemci Kitaplığı](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Kapalı kalma süresi sona VM başlatın. Genellikle tüm işlemi birkaç dakika içinde tamamlanır.

Bu işlem, VM için bir yedekleme geri yükleme noktası sağlama tüm diskler için tutarlı anlık görüntüler koleksiyonu verir. Anlık görüntüler için başka bir bölge için DR kopyalamak adımları için aşağıya bakın.

### <a name="copy-the-snapshots-to-another-region"></a>Başka bir bölgeye anlık görüntüleri kopyalama

Tek başına anlık görüntü oluşturmaya DR için yeterli olmayabilir. Ayrıca, başka bir bölgeye anlık görüntüsü yedekleri çoğaltılması gerekir.

Ardından, disklerin GRS veya RA-GRS kullanıyorsanız, anlık görüntüleri ikincil bölge'ye otomatik olarak çoğaltılır. Önce çoğaltma gecikmesi, birkaç dakika olabilir ve anlık görüntü çoğaltma bitirmeden birincil veri merkezi kullanılamaz hale gelirse, ikincil veri merkezi'nden anlık görüntüleri erişebilir olmaz. Bu olasılığını küçüktür.

> [!Note] 
> Yalnızca bir GRS veya RA-GRS hesabı disklere sahip VM olağanüstü durumlarını korumaz. Ayrıca, Azure Yedekleme'yi Eşgüdümlü anlık görüntülerini oluşturma veya gerekir. Bu, bir VM tutarlı bir duruma kurtarmak için gereklidir.

LRS kullanıyorsanız, anlık görüntü hemen oluşturduktan sonra farklı bir depolama hesabı için anlık görüntüleri kopyalamanız gerekir. Kopyalama hedefi uzak bir bölgede olması kopyalama sonuçta bir LRS depolama hesabı farklı bir bölgede olabilir. Ayrıca, anlık görüntü bir RA-GRS depolama hesabı aynı bölgede kopyalayabilirsiniz. Bu durumda, anlık görüntü gevşek uzak ikincil bölge'ye çoğaltılır. Çoğaltma tamamlandıktan ve yedekleme olağanüstü bir kez kopyalama birincil sitede gelen korunmaktadır.

Artımlı anlık DR için verimli bir şekilde kopyalamak için yönergeleri gözden [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Anlık görüntüler kurtarma

Bir anlık görüntü almak için yeni blob yapmak üzere kopyalayın. Anlık görüntü birincil hesabından kopyalıyorsanız, anlık görüntü üzerinden anlık görüntüyü temel blob'a böylece disk anlık görüntüye geri döndürmeyi kopyalayabilirsiniz; Bu anlık görüntü yükseltme olarak bilinir. Anlık görüntü yedekleme (RA-GRS) olması durumunda ikincil bir hesaptan kopyalıyorsanız birincil hesabına kopyalanmalıdır. Bir anlık görüntü kopyalayabilirsiniz [PowerShell kullanarak](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) veya AzCopy yardımcı programını kullanarak. Daha fazla bilgi için bkz: [AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

Birden çok diske sahip sanal makineleri söz konusu olduğunda, aynı Eşgüdümlü geri yükleme noktası parçası olan tüm anlık görüntüleri kopyalamanız gerekir. Yazılabilir VHD BLOB'ları için anlık görüntü kopyalama sonra VM için VM şablonu kullanarak yeniden oluşturmak için BLOB'ları kullanabilirsiniz.

## <a name="other-options"></a>Diğer seçenekleri

### <a name="sql-server"></a>SQL Server

Bir VM içinde çalışan SQL Server, SQL Server veritabanını Azure Blob Depolama veya bir dosya paylaşımı yedeklemek için kendi yerleşik özellikler vardır. GRS veya RA-GRS depolama hesabı ise, depolama hesabının ikincil veri merkezinde aynı kısıtlamalara sahip bir olağanüstü durum durumunda bu yedekleri daha önce açıklandığı gibi erişebilirsiniz. Daha fazla bilgi için bkz: [yedekleme ve Azure Virtual Machines'de SQL Server için geri yükleme](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Yedekleme ve geri yükleme, ek olarak [SQL Server Always On kullanılabilirlik grupları](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) olağanüstü durum kurtarma süresini önemli ölçüde azaltan veritabanlarını ikincil çoğaltmaların koruyabilirsiniz.

## <a name="other-considerations"></a>Diğer konular

Bu makalede, nasıl yedekleme veya Vm'lerinizi ve bunların diskleri olağanüstü durum kurtarma desteği için anlık görüntülerini almak ve bu kurtarmak için nasıl kullanılacağını ele. Azure Resource Manager modeli ile birçok kişi Azure'da Vm'leri ve diğer altyapıya oluşturmak için şablon kullanın. Her zaman aynı yapılandırmaya sahip bir VM oluşturmak için bir şablon kullanın. Vm'leriniz oluşturmak için özel resimler kullanırsanız, ayrıca bunları depolamak için bir RA-GRS hesabı kullanarak görüntülerinizi korumalı emin olmalısınız.

Sonuç olarak, yedekleme işlemi iki şey birleşimi olabilir:

1. Yedekleme verileri (diskler)
2. Yapılandırma (şablonlar, özel resimler) yedekleme

Seçtiğiniz yedekleme seçeneği bağlı olarak hem verileri hem de yapılandırma yedeğini işlemeye sahip olabilir veya yedekleme hizmeti tümünü sizin için işleyebilir.

## <a name="appendix---understanding-the-impact-of-lrs-grs-and-ra-grs"></a>Ek - LRS, GRS ve RA-GRS etkisini anlama

Azure depolama hesapları için olağanüstü durum kurtarma ile ilgili – yerel olarak yedekli (LRS), coğrafi olarak yedekli (GRS), göz önünde bulundurmalısınız veri artıklığı üç tür vardır veya coğrafi olarak yedekli ile okuma erişimi (RA-GRS). 

Yerel olarak yedekli depolama (LRS) aynı veri merkezinde verilerin üç kopyasını tutar. Aynı bilmesi başarı çağırana döndürülmeden önce verileri yazarken, tüm üç kopyaları güncelleştirilir. Tüm üç kopyalarını aynı anda etkilenen son derece düşüktür olduğundan diskinizin yerel hatalarından korunur. LRS durumunda olmadığından hiçbir coğrafi yedeklilik, tüm veri merkezi veya depolama birimi etkileyebilir yıkıcı hatalarından disk korumalı değil.

GRS ve RA-GRS, verilerinizin üç kopyasını (sizin tarafınızdan seçili) birincil bölgede korunur ve verilerinizin üç ek kopya (Azure tarafından ayarlanır) karşılık gelen bir ikincil bölge korunur. Örneğin, Batı ABD veri depolarsanız, verileri Doğu ABD çoğaltılır. Bu zaman uyumsuz olarak yapılır ve güncelleştirmeler için birincil ve ikincil arasında kısa bir gecikme olur. İkincil site disklerde çoğaltmalarının (gecikmeyle) bir disk başına temelinde tutarlı ancak birden fazla etkin diskleri çoğaltmalarının eşitlenmiş olmayabilir **birbirleriyle**. Birden çok diskte tutarlı çoğaltmaları için tutarlı anlık görüntüleri gereklidir.

GRS ve RA-GRS arasındaki temel fark, RA-GRS ile ikincil kopya herhangi bir zamanda okuyabildiğini ' dir. Birincil bölge verileri erişilemeyen işleyen bir sorun varsa, Azure ekibi erişimi geri yüklemek için tüm çabayı göstereceğiz. Birincil çalışmadığında RA-GRS etkin varsa, ikincil veri merkezine verilerine erişebilir. Birincil erişilemediği durumda çoğaltmasından okuma planlıyorsanız, bu nedenle, ardından RA-GRS dikkate alınmalıdır.

Önemli bir kesinti olmasını Öyle değilse Azure ekibi bir coğrafi yük devretme tetiklemek ve ikincil depolama birimine işaret edecek şekilde birincil DNS girdilerini değiştirin. Bu noktada, ya da GRS veya RA-GRS etkin varsa, ikincil kullanılan bölgede bulunan verilere erişebilir. Diğer bir deyişle, GRS depolama hesabınız ise ve bir sorun olduğundan, yalnızca bir yük devretme coğrafi ise ikincil depolama erişebilir.

Daha fazla bilgi için bkz: [bir Azure Storage kesinti oluşursa yapmanız gerekenler](storage-disaster-recovery-guidance.md). 

Microsoft bir yük devretme oluşup oluşmadığını denetimleri unutmayın. Yük devretme depolama hesabı denetlenmeyen, bu nedenle, tekil müşteriler tarafından belirlenir değil. Belirli bir depolama hesapları veya sanal makine disklerini için olağanüstü durum kurtarma uygulamak için bu makalede daha önce açıklanan teknikleri kullanmanız gerekir.

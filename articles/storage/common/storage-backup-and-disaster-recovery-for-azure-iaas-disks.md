---
title: "Azure Iaas disklerini aaaBackup ve olağanüstü durum kurtarma | Microsoft Docs"
description: "Bu makalede, biz anlatılmıştır nasıl tooplan yedekleme ve olağanüstü durum kurtarma (DR) Iaas sanal makineleri (VM'ler) ve Azure diskleri. Bu belge hem yönetilen hem de yönetilmeyen diskler kapsar"
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
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Azure Iaas diskler için yedekleme ve olağanüstü durum kurtarma

Bu makalede, biz anlatılmıştır nasıl tooplan yedekleme ve olağanüstü durum kurtarma (DR) Iaas sanal makineleri (VM'ler) ve Azure diskleri. Bu belge, yönetilen ve yönetilmeyen diskleri kapsar.

Biz öncelikle yerel arızaya karşı koruma sağlamak yardımcı olan hello yerleşik hata toleransı özellikleri hakkında hello Azure platformu konuşun. Biz sonra tam olarak hello ana konuya göre bu belgede ele olduğu hello yerleşik özellikleri tarafından kapsanan hello olağanüstü durum senaryolar ele alacağız. Burada farklı yedekleme ve kurtarma konuları uygulayabilir iş yükü senaryoları bazı örnekleri de göstereceğiz. Biz ardından olası çözümler için Iaas disklerini DR gözden geçirin. 

## <a name="introduction"></a>Giriş

Hello Azure platformu artıklık için çeşitli yöntemler kullanır ve hataya dayanıklılık toohelp oluşabilir yerelleştirilmiş donanım hatalarından müşteriler koruyun. Yerel hatalar, bir sanal disk için hello verilerin bir kısmını ya da bir SSD veya HDD hatalarının o sunucuda depolayan bir Azure depolama sunucu makinesindeki sorunlar içerebilir. Bu tür yalıtılmış donanım bileşeni arızalarına normal işlemler sırasında oluşabilir ve tasarlanmış toobe dayanıklı toothese hataları hello platformudur. Ana afetler hataları veya depolama sunucuları veya tam bir veri merkezinde çok sayıda inaccessibility neden olabilir. VM'ler ve diskleri yerelleştirilmiş hatalarından normalde korunur, ancak ek adımlar gerekli tooprotect olan yükünüzü hatalardan VM ve diskleri etkileyebilecek bölge çapında geri dönülemez (örneğin, büyük bir felaket).

Ayrıca platform hataları olasılığını toohello, Merhaba müşteri uygulaması veya veri sorunlar oluşabilir. Örneğin, uygulamanızın yeni bir sürümünü yanlışlıkla toohello verileri değiştirme sonu kalmasına neden olabilir. Bu durumda, toorevert hello uygulama ve hello veri tooa önceki sürümünü içeren hello bilinen son iyi duruma isteyebilirsiniz. Bu, düzenli yedeklemeler koruma gerektirir.

Bölgesel olağanüstü durum kurtarma için Iaas VM diskleri tooa farklı bölgenizi yedeklemeniz gerekir. 

Şimdi biz yedekleme ve kurtarma seçeneklerini Ara önce yerelleştirilmiş hata işleme için birkaç yöntem kullanılabilir olduðunu.

### <a name="azure-iaas-resiliency"></a>Azure Iaas dayanıklılık

*Dayanıklılık* donanım bileşenleri ortaya normal hataları için toohello dayanıklılık başvuruyor. Dayanıklılık hello özelliği toorecover hatalardan olduğu ve toofunction devam edin. Hataları önleme, ancak toofailures kapalı kalma süresi veya veri kaybı önler şekilde yanıt hakkında değil. Hello dayanıklılık tooreturn hello uygulama tooa tam olarak işlevsel durumu bir hatasının ardından hedefidir. Azure sanal makineleri ve diskleri tasarlanmış toobe dayanıklı toocommon donanım hatalarıdır. Bize hello Azure Iaas platform bu dayanıklılık nasıl sağladığını adresindeki arayın.

Bir sanal makine çoğunlukla iki bölümden oluşur: (1) bir işlem sunucusu ve (2) hello kalıcı diskler. Her ikisi de hello hata toleransı, bir sanal makinenin etkiler.

VM barındırıldığı hello Azure işlem ana bilgisayar sunucusu (Bu nadir) bir donanım hatası yaşarsa, Azure başka bir sunucuda tasarlanmış tooautomatically geri yükleme hello VM ' dir. Bu durumda, yeniden başlatma yaşar ve hello VM yedekleme bir süre sonra olacaktır. Azure otomatik olarak bu tür donanım hataları algılar ve kurtarmaları yürütür toohelp hello müşteri VM kullanılabilir mümkün olan en kısa sürede emin olun.

Iaas disklerini ilgili veri dayanıklılığı hello kalıcı depolama platform için kritik öneme sahiptir. Azure müşterilerin önemli iş uygulamaları Iaas'da çalışan sahip ve hello veri hello sürekliliği bağlıdır. Bu üç yedek kopyaları Iaas diskleri için Azure tasarımları koruma yerel olarak depolanan verilerin yerel hatalarına karşı yüksek dayanıklılık sağlama. Diskinizin tutan hello donanım bileşenleri biri başarısız olursa, iki ek kopyalarını toosupport disk istekleri olduğundan, VM etkilenmez. Merhaba aynı disk destekleyen iki farklı donanım bileşenlerini başarısız olsa bile düzgün çalışır (çok nadir olur) süresi. toohelp biz her zaman üç çoğaltmaları korumak, hello üç kopyaları biri kullanılamaz hale gelirse otomatik olarak çoğaltılır hello arka planda verileri yeni bir kopyasını hello Azure depolama hizmeti emin olun. Bu nedenle, gerekli toouse RAID hataya dayanıklılık için Azure disklerine sahip olmamalıdır. Yapılandırma, hello diskleri bölmek için yeterli basit bir RAID 0 gerekli toocreate daha büyük birimleri.

Bu mimari nedeniyle **Azure Kurumsal düzeyde tutarlı bir şekilde teslim Iaas için dayanıklılık diskleri, bir endüstri lideri ile sıfır % [değer yıllık hata oranı](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Yerelleştirilmiş donanım hataları hello üzerinde işlem ana bilgisayar veya hello depoda platform bazen hello hello tarafından ele VM geçici olarak kullanım dışı kalması sonuçlanabilir [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) VM kullanılabilirlik. Azure, endüstri lideri SLA Premium depolama diski kullanan tek VM örnekleri için de sağlar.

toosafeguard uygulama kapalı kalma süresi toohello geçici olarak kullanım dışı kalması bir disk veya VM son iş yüklerini, müşterilerin yararlanabilir [kullanılabilirlik kümeleri](../../virtual-machines/windows/manage-availability.md). Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makine Merhaba uygulaması için artıklık sağlar. Azure daha sonra bu sanal makineleri ve diskleri ayrı hata etki alanlarında farklı güç, ağ ve sunucu bileşenleri ile oluşturur. Bu nedenle, yerelleştirilmiş donanım hataları genellikle hello ayarlamak hello içinde birden çok VM etkilemez aynı zamanda, uygulamanız için yüksek kullanılabilirlik sağlar. Yüksek kullanılabilirlik gerekli olduğunda iyi bir uygulama toouse kullanılabilirlik kümeleri kabul edilir. Daha fazla bilgi için aşağıdaki ayrıntılı hello olağanüstü durum kurtarma yönlerini bakın.

### <a name="backup-and-disaster-recovery"></a>Yedekleme ve olağanüstü durum kurtarma

Olağanüstü Durum Kurtarma (DR) olan hello özelliği toorecover nadir ancak önemli olayları gelen: tüm bölgeyi etkiler hizmet kesintisi gibi geçici olmayan, geniş ölçekli hataları. Olağanüstü durum kurtarma, veri yedekleme ve arşivleme içerir ve bir veritabanını yedekten geri yükleme gibi el ile müdahale içerebilir.

Merhaba yerelleştirilmiş hatalarına karşı yerleşik koruma Azure platformun tam olarak hello VM'ler/diskleri büyük ölçekli kesintileri neden önemli afetler hello durumda koruma. Bu bir hortum, deprem, yangın veya büyük ölçekli donanım birim hataları tarafından ziyaret bir veri merkezi gibi geri dönülemez olaylarını içerir. Ayrıca, hataları tooapplication veya veri sorunları nedeniyle karşılaşabilirsiniz.

toohelp Iaas iş yüklerinizi kesintilere karşı korumak, artıklık ve yedeklemeleri tooenable kurtarma için planlamanız gerekir. Olağanüstü durum kurtarma için artıklık ve yedekleme hello birincil sitesinden farklı bir coğrafi konumda planlamanız gerekir. Bu yedekleme tarafından hello etkilenmez sağlamaya yardımcı olur. başlangıçta hello VM veya diskleri etkilenen aynı olay. Daha fazla bilgi için bkz: [olağanüstü durum kurtarma uygulamaları için Azure üzerinde oluşturulmuş](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

DR konularınızdan yönlerini aşağıdaki hello içerebilir:

1. Yüksek kullanılabilirlik (HA) hello önemli kapalı kalma süresi olmadan sağlıklı bir durumda çalışan hello uygulama toocontinue özelliğidir. "Sağlıklı durumuna göre" biz Merhaba uygulaması esnek ve kullanıcılar toohello uygulama bağlanabilir ve onlarla etkileşime anlamına gelir. Belirli olduğunda bile hataları hello platform gerekli toobe kullanılabilir kritik uygulamaların ve veritabanlarının her zaman, olabilir. Bu iş yükleri için tooplan artıklık hello veri yanı sıra Merhaba uygulaması için gerekebilir.

2. Veri dayanıklılığı: Bazı durumlarda, hello bir olağanüstü durumda hello verilerin korunduğundan hello ana göz önünde bulundurarak emin olmaktır. Bu nedenle, bir yedekleme verilerinizin farklı bir sitede gerekebilir. Bu tür iş yükleri için hello uygulama için tam yedekleme, ancak normal yedekleme hello disklerin gerekmeyebilir.

## <a name="backup-and-dr-scenarios"></a>Yedekleme ve kurtarma senaryoları

Uygulama iş yükü senaryoları ve olağanüstü durum kurtarma planlama konuları hello bazı tipik örnekler bakalım.

### <a name="scenario-1-major-database-solutions"></a>Senaryo 1: Birincil veritabanı çözümleri

Bir üretim veritabanı sunucusuna SQL Server veya yüksek kullanılabilirlik destekleyebilir Oracle gibi göz önünde bulundurun. Kritik üretim uygulamaların ve kullanıcıların bu veritabanında bağlıdır. Bu sistem için Hello olağanüstü durum kurtarma planı toosupport hello gereksinimleri aşağıdaki gerekebilir:

1. Verilerin korunan ve kurtarılabilir olması gerekir.
2.  Sunucusunun kullanılabilir olması gerekir.

Bu, yedek olarak farklı bir bölgede hello veritabanının bir kopyasını koruyarak gerektirebilir. Sunucu kullanılabilirliği ve veri kurtarma Hello gereksinimlerine bağlı olarak, hello çözüm etkin-etkin veya etkin-pasif kopya site tooperiodic çevrimdışı yedeklemeler hello veri aralığında. SQL Server ve Oracle gibi ilişkisel veritabanları çoğaltma için çeşitli seçenekler sağlar. SQL Server için [SQL Server Always On kullanılabilirlik grupları](https://msdn.microsoft.com/library/hh510230.aspx) yüksek kullanılabilirlik için kullanılabilir.

MongoDB gibi NoSQL veritabanlarını da destek [çoğaltmaları](https://docs.mongodb.com/manual/replication/) artıklık için. Merhaba çoğaltmaları yüksek kullanılabilirlik için kullanılabilir.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Senaryo 2: Küme yedek VM'ler

Artıklık sağlamak ve Yük Dengeleme sanal makineleri bir küme tarafından işlenen bir iş yükü göz önünde bulundurun. Bir örnek bir bölgeye dağıtılmış bir Cassandra kümesi olabilir. Bu tür bir mimari zaten bu bölgedeki artıklık yüksek düzeyde sağlar. Ancak, iki bölgeler arasında hello küme yayılmak veya düzenli yedeklemeler tooanother bölge oluşturma'da, bir tooprotect hello iş yükü bölgesel düzeyinde hatasından düşünmelisiniz.

### <a name="scenario-3-iaas-application-workload"></a>Senaryo 3: Iaas uygulama iş yükü

Bu, bir Azure VM üzerinde çalışan bir tipik bir üretim iş yükünü olabilir. Örneğin, bir web sunucusu veya dosya sunucusu hello içerik ve diğer kaynakların bir sitenin bulunduran olabilir. Ayrıca, verileri, kaynaklar ve uygulama durumunu hello VM disklerinde depolanan bir VM üzerinde çalışan bir özel olarak geliştirilmiş iş uygulaması de olabilir. Bu durumda, önemli toomake düzenli yedeklemeler ele emin olur. Yedekleme sıklığı hello VM iş yükü hello doğasına bağlı olmalıdır. Örneğin, Merhaba uygulaması her gün çalışır ve veri değiştirir, hello yedekleme saatte gerçekleştirilmelidir.

Başka bir örnek diğer kaynaklardan veri çekmek raporlama sunucusudur ve birleşik raporları oluşturur. Bu VM veya diskleri kaybı hello raporları toohello kaybedilmesine neden olacaktır. Ancak, bu işlemi ve yeniden oluşturma hello çıkış raporlama olası toorerun hello olabilir. Bu durumda, Raporlama sunucusu hello hello verileri parçası kaybetme dayanıklılık daha yüksek düzeyde olabilir şekilde hello raporlama sunucusu olağanüstü durum ile bile ulaşılırsa veri kaybı gerçekten yok. Bu durumda, daha az sık gerçekleştirilen yedeklemeler, bir seçenek tooreduce hello maliyetini olur.

### <a name="scenario-4-iaas-application-data-issues"></a>Senaryo 4: Iaas uygulama verileri sorunları

Hesaplar, korur ve fiyatlandırma bilgileri gibi kritik ticari verileri hizmet veren bir uygulamaya sahip. Uygulamanızı yeni bir sürümü yanlış hello fiyatlandırma hesaplanan ve hello platformu tarafından sunulan hello varolan ticaret verileri bozuk bir yazılım hata vardı. Merhaba iyi davranış biçimini toorevert toohello burada olacaktır önceki sürümünü hello uygulama ve hello veri ilk. tooenable sisteminizin Bu, Al düzenli yedeklemeler.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Olağanüstü durum kurtarma çözümü: Azure yedekleme hizmeti

[Azure Backup hizmeti](https://azure.microsoft.com/services/backup/) ile çalışır ve yedekleme ve kurtarma için kullanılabilir olan [yönetilen diskleri](../../virtual-machines/windows/managed-disks-overview.md) yanı [yönetilmeyen diskleri](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). Bir yedekleme işi zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri oluşturabilirsiniz. 

Kullanırsanız [Premium depolama diskleri](storage-premium-storage.md), [yönetilen diskleri](../../virtual-machines/windows/managed-disks-overview.md), veya diğer disk türleri hello ile [yerel olarak yedekli depolama (LRS)](storage-redundancy.md#locally-redundant-storage) seçeneği, özellikle önemli tooleverage olduğu Dönemsel DR yedeklemeler. Azure yedekleme kurtarma Hizmetleri kasanız uzun vadeli bekletme için hello verileri depolar. Merhaba seçin [coğrafi olarak yedekli depolama (GRS)](storage-redundancy.md#geo-redundant-storage) hello yedekleme kurtarma Hizmetleri kasası için seçenek. Yedeklemeler için bölgesel olağanüstü durumlarını koruma çoğaltılmış tooa farklı Azure bölgesi olan ilişkilendirilmesini sağlar.

İçin [yönetilmeyen diskleri](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), Iaas disklerini hello LRS depolama türü kullanır, ancak Azure Backup ile Merhaba GRS seçeneği hello kurtarma Hizmetleri kasası için etkinleştirildiğinden emin olun.

**Merhaba kullanırsanız [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) seçeneği yönetilmeyen disklerinizi, yine için yedekleme ve kurtarma için tutarlı anlık görüntüler gerekir.** Ya da kullanmalıdır [Azure Backup hizmeti](https://azure.microsoft.com/services/backup/) veya [tutarlı anlık görüntüleri](#alternative-solution-consistent-snapshots).

Merhaba, DR çözümleri özeti aşağıdadır.

| Senaryo | Otomatik çoğaltma | DR çözümü |
| --- | --- | --- |
| *Premium depolama diskleri* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilen Diskler* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilmeyen LRS diskleri* | Yerel ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Yönetilmeyen GRS diskleri* | Çapraz bölge ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Tutarlı anlık görüntüler](#alternative-solution-consistent-snapshots) |
| *Yönetilmeyen RA-GRS diskleri* | Çapraz bölge ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Tutarlı anlık görüntüler](#alternative-solution-consistent-snapshots) |

Yüksek kullanılabilirlik en iyi göre karşılanmış bir kullanılabilirlik kümesi Azure yedekleme ile birlikte yönetilen diskleri hello kullanımı aracılığıyla. Yönetilmeyen diskler kullanıyorsanız, Azure Backup DR için kullanmaya devam edebilirsiniz. Yüklenemiyor toouse Azure Backup varsa, ardından alma [tutarlı anlık görüntüleri](#alternative-solution-consistent-snapshots) açıklandığı gibi daha sonraki bir bölüme bir alternatif için yedekleme ve kurtarma çözümüdür.

Seçimlerinizi yüksek kullanılabilirlik için yedekleme ve uygulama veya altyapı düzeylerinde DR temsil olarak aşağıda:

| *Düzeyi* | Yüksek kullanılabilirlik   | Yedekleme / DR |
| --- | --- | --- |
| *Uygulama* | Her zaman açık SQL | Azure Backup |
| *Altyapı*  | Kullanılabilirlik Kümesi  | GRS ile tutarlı anlık görüntüler |

### <a name="using-hello-azure-backup-service"></a>Hello Azure Backup hizmeti kullanma

[Azure yedekleme](../../backup/backup-azure-vms-introduction.md) Windows veya Linux toohello Azure kurtarma Hizmetleri kasası çalıştıran, sanal makineleri yedekleyebilirsiniz. Yedekleme ve geri yükleme iş açısından kritik verilerin karmaşık iş açısından kritik verilerin veri çalıştıran hello üretmek hello uygulamaları sırasında yedeklenmesi hello olgu tarafından. tooaddress Bu, Azure Backup uygulamayla tutarlı yedeklemeler Microsoft iş yükleri için veri toostorage doğru yazıldığından emin hello birim gölge hizmeti (VSS) tooensure kullanarak sağlar. Linux işlevleri eşdeğer tooVSS olmadığından Linux VM'ler için yalnızca dosya tutarlı yedeklemeler olasılığı vardır.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Azure Backup, zamanlanmış başlangıç zamanında bir yedekleme işi başlattığında, hello yedekleme uzantı hello VM tootake zaman içinde nokta anlık görüntü yüklü tetikler. Bir anlık görüntü VSS tooget tutarlı bir anlık görüntü ile koordinasyon halinde hello sanal makine hello diskin tooshut gerek kalmadan, oluşturulduğunda kapalı. Merhaba VM Hello yedekleme uzantısına tüm hello disklerin hello tutarlı anlık önce tüm yazma işlemlerini aktarır. Başlangıç anlık görüntüsü alınır sonra hello verileri Azure yedekleme toohello yedekleme kasası tarafından aktarılır. toomake hello yedekleme işlemini daha verimli hello hizmeti tanımlar ve yalnızca hello hello son yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.


toorestore, Azure Backup aracılığıyla kullanılabilir yedeklemeleri hello görüntüleyin ve geri yüklemeyi başlatmak. Oluşturma ve Azure yedeklemeleri hello aracılığıyla geri [Azure portal](https://portal.azure.com/), [PowerShell kullanarak](../../backup/backup-azure-vms-automation.md ), veya hello kullanarak [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install). Daha fazla bilgi için Azure yedekleme konusuna bakın.

### <a name="steps-tooenable-backup"></a>Adımları tooEnable yedekleme

Merhaba aşağıdaki hello kullanarak, Vm'lerde genellikle kullanılan tooenable yedeklerini adımlardır [Azure Portal](https://portal.azure.com/). Tam senaryonuza bağlı olarak bazı farklılıklar olacaktır. Toohello başvuran [Azure Backup](../../backup/backup-azure-vms-introduction.md) tam Ayrıntılar için belgelerine bakın. Azure ayrıca yedekleme [yönetilen diske sahip sanal makineleri destekleyen](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Merhaba aşağıdaki adımları kullanarak bir VM için bir kurtarma Hizmetleri kasası oluşturun:

    a.  Hello kullanarak [Azure portal](https://portal.azure.com/)tüm kaynaklara göz atın ve "Kurtarma Hizmetleri kasalarının" bulunamıyor.

    b.  Merhaba üzerinde menü kurtarma Hizmetleri kasaları, Ekle ve hello adımları toocreate hello yeni bir kasada izleyin hello VM ile aynı bölgeye. Örneğin, VM'yi Batı ABD bölgesi ise, Batı ABD hello kasası için seçin.

2.  Merhaba depolama çoğaltma için yeni kasa oluşturulan hello doğrulayın. toodo Bu, erişim hello kasadan hello kurtarma Hizmetleri kasaları dikey penceresinde ve Git toohello ayarları/yedekleme yapılandırması. Merhaba GRS seçeneği varsayılan olarak seçili olduğundan emin olun. Bu, kasa adınız otomatik olarak çoğaltılmış tooa ikincil veri merkezi olduğunu güvence altına alır. Örneğin, Batı ABD, kasaya otomatik olarak çoğaltılmış tooEast ABD olacaktır.

3.  Merhaba yedekleme ilkesi yapılandırın ve hello hello VM seçin aynı kullanıcı Arabirimi.

4.  Yedekleme aracısının hello VM üzerinde yüklü olduğundan emin hello olun. VM Azure galerisinde görüntü kullanarak oluşturulursa hello Backup Aracısı zaten yüklüdür. (Diğer bir deyişle, özel bir görüntü kullanıyorsanız) Aksi durumda, yönergeleri çok kullanın[hello sanal makineye yükleme hello VM Aracısı](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Bu hello VM hello yedekleme hizmeti toofunction için ağ bağlantısı izin verdiğinden emin olun. Bu yönergeleri izleyin [ağ bağlantınızı](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Hello yukarıdaki adımları tamamlandıktan sonra yedekleme İlkesi hello belirtildiği gibi düzenli aralıklarla hello yedekleme çalıştırın. Gerekirse, hello ilk yedek hello kasa Panosu hello Azure portalı üzerinde kaynağından el ile tetikleyebilirsiniz.

Azure komut dosyalarını kullanarak yedekleme otomatikleştirmek için çok başvurun[VM yedekleme için PowerShell cmdlet'leri](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Kurtarma için adımları

Toorepair gerekir veya VM yeniden herhangi birinden hello yedekleme kurtarma noktalarının hello kasasında hello VM geri yükleyebilirsiniz. Birkaç hello kurtarma gerçekleştirmek için farklı seçenekler vardır:

1.  Yeni bir VM, yedeklenen VM olarak zaman içinde nokta gösterimini oluşturabilirsiniz.

2.  Hello diskleri geri yükleyebilir ve sonra hello VM toocustomize hello şablonu kullanın ve yeniden hello VM geri. 

Yönergeler çok bkz[kullanım Azure portal toorestore sanal makineleri](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). Merhaba belge ayrıca yedeklenen VM'ler toohello eşleştirilmiş veri merkezi hello birincil veri merkezindeki bir olağanüstü durum hello durumda coğrafi olarak yedekli yedekleme kasanızı kullanarak geri yüklemek için belirli adımlar hello açıklar. Bu durumda, Azure Backup hello ikincil bölge toocreate geri hello sanal makineden hello işlem hizmeti kullanır.

PowerShell için de kullanabilirsiniz [VM geri](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) veya [yeni bir sanal makineden oluşturma geri diskleri](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatif çözüm: Tutarlı anlık görüntüler

%S toouse hello Azure yedekleme hizmeti varsa, anlık görüntülerini kullanarak kendi yedekleme mekanizması uygulayabilirsiniz. Bu karmaşık toocreate bir VM tarafından kullanılan tüm diskler için tutarlı anlık görüntüler ve bu anlık görüntüleri tooanother bölgeye çoğaltılır. Bu nedenle, Azure yararlanmayı hello Backup hizmeti özel çözüm oluşturma değerinden daha iyi bir seçenek olarak değerlendirir. RA-GRS/GRS depolama diskleri için kullanıyorsanız, anlık görüntüleri otomatik olarak çoğaltılmış tooa ikincil veri merkezi değildir. LRS depolama için diskleri kullanırsanız, kendiniz tooreplicate hello verilere ihtiyaç duyarsınız. Daha fazla bilgi için bkz: [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](../../virtual-machines/windows/incremental-snapshots.md).

Bir nesne belirli bir noktada bir gösterimini zaman içinde bir anlık görüntüdür. Anlık isteğe bağlı olarak hello artımlı hello verilerin boyutu için ayrı tutma faturalama uygulanabilir. Daha fazla bilgi için bkz: [blob anlık görüntü](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>VM çalıştıran hello anlık görüntüler oluşturma

Merhaba VM çalışıyorsa, herhangi bir zamanda bir anlık görüntü alabilir, ancak hala toohello diskleri akıtılan veri yoktur ve hello anlık görüntüleri uçuş modunda olan kısmi işlemleri içerebilir. Söz konusu birden çok disk varsa, ayrıca, farklı disklerin anlık görüntüleri hello farklı zamanlarda bu anlık görüntüleri Eşgüdümlü olmayabilir anlamına gelir oluşmuş olabilir. Bu değişikliği yedekleme sırasında yapılmışsa, dosya bozuk şeritli birimler için özellikle sorunlu oluşturur.

tooavoid bu durum hello yedekleme işlemi hello aşağıdaki adımları uygulamanız gerekir:

1.  Tüm hello diskleri dondurma

2.  Tüm yazma hello temizleme

3.  Ardından, [blob anlık görüntü](../blobs/storage-blob-snapshots.md) tüm diskleri hello için

SQL Server gibi bazı Windows uygulamaları VSS toocreate uygulamayla tutarlı yedeklemeler aracılığıyla koordineli bir yedekleme mekanizması sağlar. Linux üzerinde dosya tutarlı yedeklemeler, ancak değil uygulamayla tutarlı anlık görüntüleri sağlayacak hello diskleri düzenlemekten fsfreeze gibi bir araç kullanabilirsiniz. Bu karmaşık bir işlemdir, bu nedenle ve kullanmayı düşünmelisiniz [Azure yedekleme](../../backup/backup-azure-vms-introduction.md) veya bu zaten uygulayan bir üçüncü taraf yedekleme çözümünün.

işlem yukarıda Hello hello VM belirli bir zaman içinde nokta görünümünü temsil eden tüm hello VM diskleri için Eşgüdümlü anlık görüntü koleksiyonu neden olur. Merhaba VM için bir yedekleme geri yükleme noktası budur. Zamanlanmış aralıklarla toocreate düzenli yedeklemeler hello işlemi yineleyebilirsiniz. Aşağıda başlangıç adımları için çok bkz[kopyalama hello yedeklemeleri tooanother bölge](#copy-the-snapshots-to-another-region) DR için.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Anlık görüntüler var ve hello oluşturma VM çevrimdışı

Başka bir seçenek toocreate tutarlı yedeklemeler kapanıyor hello VM ve alma blob aşağı her disk anlık görüntüler. Bu denetleyici çalışan bir VM anlık kolaydır, ancak birkaç dakika kalma süresi gerekir. Bu işlem, şu adımları izleyin:

1. Kapatma hello VM.

2. Bir anlık görüntü yalnızca birkaç saniye sürer her VHD BLOB oluşturun.

    kullanabileceğiniz bir anlık görüntü toocreate [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), hello [Azure Storage Rest API'sini](https://msdn.microsoft.com/library/azure/ee691971.aspx), [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install), veya hello Azure Storage istemcisi kitaplıklarını gibi [ .NET için depolama istemci kitaplığı Hello](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Merhaba hello kapalı kalma süresi sona VM başlatın. Genellikle hello tüm işlemi birkaç dakika içinde tamamlanır.

Bu işlem tutarlı anlık görüntüleri hello VM için bir yedekleme geri yükleme noktası sağlama tüm hello disklerin koleksiyonu verir. Aşağıda hello adımları toocopy hello anlık görüntüleri tooanother bölge için DR için bkz.

### <a name="copy-hello-snapshots-tooanother-region"></a>Merhaba anlık görüntüleri tooanother bölge kopyalayın

Tek başına hello anlık görüntü oluşturmaya DR için yeterli olmayabilir. Ayrıca hello anlık görüntüsü yedekleri tooanother bölge çoğaltılması gerekir.

Ardından, disklerin GRS veya RA-GRS kullanıyorsanız, hello anlık görüntüler otomatik olarak çoğaltılmış toohello ikincil bölge değildir. Gecikme hello çoğaltma önce birkaç dakika olabilir ve hello anlık görüntü çoğaltma bitirmeden hello birincil veri merkezi kullanılamaz hale gelirse hello ikincil veri merkezi alınan mümkün tooaccess hello anlık olmaz. Bu Hello olasılığını küçüktür.

> [!Note] 
> Yalnızca bir GRS veya RA-GRS hesabı hello disklere sahip hello VM olağanüstü durumlarını korumaz. Ayrıca, Azure Yedekleme'yi Eşgüdümlü anlık görüntülerini oluşturma veya gerekir. Gerekli toorecover VM tooa tutarlı bir duruma budur.

LRS kullanıyorsanız, hemen hello anlık görüntü oluşturduktan sonra hello anlık görüntüleri tooa farklı depolama hesabı kopyalamanız gerekir. Merhaba kopyalama hedefi uzak bir bölgede olması hello kopyalama sonuçta bir LRS depolama hesabı farklı bir bölgede olabilir. Başlangıç anlık görüntü tooan RA-GRS depolama hesabı hello kopyalayabilirsiniz aynı bölgede. Bu durumda, hello anlık görüntü gevşek çoğaltılmış toohello uzak ikincil bölge olacaktır. Merhaba kopyalama ve çoğaltma olduğunda tam yedekleme hello birincil sitede afetler korumalı değildir.

toocopy, artımlı anlık görüntüleri DR için verimli bir şekilde hello yönergeleri gözden [artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleme](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Anlık görüntüler kurtarma

tooretrieve bir anlık görüntü toomake yeni blob kopyalayın. Merhaba birincil hesabından hello anlık görüntü kopyalıyorsanız toohello temel blob hello anlık görüntünün, böylece dönüştürülüyor hello disk toohello anlık görüntü anlık görüntü hello kopyalayabilirsiniz; Bu işlem, başlangıç anlık görüntü yükseltme olarak bilinir. (RA-GRS, hello durumda) ikincil bir hesaptan hello anlık görüntü yedekleme kopyalıyorsanız olmalıdır tooa birincil hesap kopyalanır. Bir anlık görüntü kopyalayabilirsiniz [PowerShell kullanarak](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) veya hello AzCopy yardımcı programını kullanarak. Daha fazla bilgi için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

Merhaba durumda VM'lerin birden çok diske sahip, tüm kopyalamalısınız aynı Eşgüdümlü hello parçası olan hello anlık görüntü geri yükleme noktası. Merhaba anlık görüntüleri toowritable VHD BLOB kopyalama sonra Merhaba VM hello şablonu kullanarak, VM hello BLOB'lar toorecreate kullanabilirsiniz.

## <a name="other-options"></a>Diğer seçenekleri

### <a name="sql-server"></a>SQL Server

Bir VM içinde çalışan SQL Server, SQL Server veritabanı tooAzure Blob Depolama veya bir dosya paylaşımı kendi yerleşik özellikleri toobackup sahiptir. Merhaba depolama hesabı GRS veya RA-GRS ise, ile Merhaba depolama hesabının ikincil veri merkezinde bir olağanüstü durum hello olayı içinde bu yedekleri erişebilmeniz için daha önce açıklandığı gibi hello aynı kısıtlamalara. Daha fazla bilgi için bkz: [yedekleme ve Azure Virtual Machines'de SQL Server için geri yükleme](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Ayrıca toobackup ve geri yükleme, [SQL Server Always On kullanılabilirlik grupları](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) veritabanları toogreatly ikincil çoğaltmaları hello olağanüstü durum kurtarma süresini azaltmak koruyabilirsiniz.

## <a name="other-considerations"></a>Diğer konular

Bu makalede ele alınan nasıl Vm'leriniz ve bunların diskleri toosupport olağanüstü durum kurtarma toobackup veya Al anlık görüntüler ve nasıl toouse bu toorecover. Hello Azure Resource Manager modeli ile çoğu kişi şablonları toocreate Vm'leri ve diğer altyapı Azure'da kullanır. Bir şablon toocreate hello sahip bir VM kullanabilirsiniz aynı yapılandırmayı her zaman. Vm'leriniz oluşturmak için özel resimler kullanırsanız, da görüntülerinizi RA-GRS hesabı toostore kullanarak korunan emin olmanız gerekir bunları.

Sonuç olarak, yedekleme işlemi iki şey birleşimi olabilir:

1. Yedekleme hello verileri (diskler)
2. Yedekleme hello yapılandırma (şablonlar, özel resimler)

Merhaba yedekleme seçeneği seçerseniz seçin, bağlı olarak toohandle hello yedeğini hello verileri ve hello yapılandırma olabilir veya hello yedekleme hizmeti tümünü sizin için işleyebilir.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Ek - LRS, GRS ve RA-GRS Hello etkisini anlama

Azure depolama hesapları için olağanüstü durum kurtarma ile ilgili – yerel olarak yedekli (LRS), coğrafi olarak yedekli (GRS), göz önünde bulundurmalısınız veri artıklığı üç tür vardır veya coğrafi olarak yedekli ile okuma erişimi (RA-GRS). 

Yerel olarak yedekli depolama (LRS) hello hello verileri üç kopyasını tutar aynı veri merkezinde. Aynı bilmesi başarı toohello çağıran döndürülmeden önce hello veri yazarken, tüm üç kopyaları güncelleştirilir. Tüm üç kopyaları hello etkilenen son derece düşüktür olduğundan diskinizin yerel hatalarından korumalı aynı anda. LRS Hello durumda olmadığından hiçbir coğrafi yedeklilik, tüm veri merkezi veya depolama birimi etkileyebilir yıkıcı hatalarından hello disk korumalı değil.

GRS ve RA-GRS, verilerinizin üç kopyasını hello birincil bölgede (sizin tarafınızdan seçili) korunur ve verilerinizin üç ek kopya (Azure tarafından ayarlanır) karşılık gelen bir ikincil bölge korunur. Örneğin, Batı ABD veri depolarsanız hello veri çoğaltılmış tooEast ABD olur. Bu zaman uyumsuz olarak yapılır ve birincil ve ikincil güncelleştirmeleri toohello arasında küçük bir gecikme olur. Merhaba ikincil site hello disklerde çoğaltmalarının (Merhaba gecikmeyle) bir disk başına temelinde tutarlı ancak birden fazla etkin diskleri çoğaltmalarının eşitlenmiş olmayabilir **birbirleriyle**. birden çok disk, tutarlı anlık görüntüleri genelinde tutarlı çoğaltma toohave gereklidir.

Merhaba GRS ve RA-GRS arasındaki temel fark, RA-GRS ile hello ikincil kopya herhangi bir zamanda okuyabildiğini ' dir. Hello Azure ekibi, hello veri hello birincil bölgede erişilemez işleyen bir sorun varsa, her çaba toorestore erişim hale getirir. Merhaba birincil çalışmadığında RA-GRS etkin varsa, hello ikincil veri merkezi hello verilerine erişebilir. Merhaba birincil erişilemediği durumda tooread hello çoğaltmadan planlıyorsanız, bu nedenle, ardından RA-GRS dikkate alınmalıdır.

Önemli bir kesinti toobe kapatırsa hello Azure ekibi bir coğrafi yük devretme tetiklemek ve hello birincil DNS girişlerini toopoint toosecondary depolama değiştirin. Bu noktada, iki GRS veya RA-GRS etkin varsa toobe hello ikincil kullanılan hello bölge hello verilerine erişebilir. Diğer bir deyişle, GRS depolama hesabınız ise ve bir sorun olduğundan, yalnızca bir yük devretme coğrafi ise hello ikincil depolama erişebilir.

Daha fazla bilgi için bkz: [bir Azure Storage kesinti oluşursa hangi toodo](storage-disaster-recovery-guidance.md). 

Microsoft bir yük devretme oluşup oluşmadığını denetimleri unutmayın. Yük devretme depolama hesabı denetlenmeyen, bu nedenle, tekil müşteriler tarafından belirlenir değil. Olağanüstü durum kurtarma tooimplement belirli depolama hesapları veya sanal makine diskleri için daha önce bu makalede açıklanan hello teknikleri kullanmanız gerekir.

---
title: "Azure Site Recovery ile siteler arasında Hyper-V çoğaltma için aaaTest sonuçları | Microsoft Docs"
description: "Bu makale, Azure Site Recovery kullanarak Hyper-V sanal makineleri, şirket içi tooon içi çoğaltma için sınama performansı hakkında bilgi sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Site Recovery ile şirket içi tooon içi Hyper-V çoğaltma için test sonuçları

Microsoft Azure Site Recovery tooorchestrate kullanın ve sanal makineleri ve fiziksel sunucuları tooAzure veya tooa ikincil veri merkezine çoğaltılmasını yönetin. Bu makale, Hyper-V sanal makineleri iki arasında çoğaltma şirket içi veri merkezi zaman yaptığımız performansı test sonuçlarını hello sağlar.

## <a name="test-goals"></a>Test amaçları

sınama hello hedef Azure Site Recovery kararlı durum çoğaltma sırasında nasıl gerçekleştireceğini tooexamine oluştu. Sanal makinelerin başlangıç çoğaltmasını tamamlamış olmanız ve delta değişiklikler eşitleniyor kararlı durum çoğaltma oluşur. Bu, beklenmeyen kesintiler sürece, çoğu sanal makine kalır hello durumu olduğundan kararlı durum kullanarak önemli toomeasure performans gösterir.

Her sitede bir VMM sunucusuyla iki şirket içi sitenin Hello sınama dağıtımı içermektedir. Bu test dağıtımını hello birincil site ve hello şube hello ikincil veya kurtarma sitesi olarak davranan merkez ofis ile baş office/şube office dağıtımını normaldir.

## <a name="what-we-did"></a>Ne yaptığımız

Ne biz hello testinde başarılı olmadı aşağıda verilmiştir:

1. VMM şablonları kullanarak sanal makineleri oluşturulur.
2. Sanal makineler ve yakalama temel performans ölçümlerini üzerinde 12 saat başlatıldı.
3. Birincil ve kurtarma VMM sunucularında oluşturulan bulut.
4. Azure Site kurtarma, kaynak ve kurtarma bulut eşleme dahil olmak üzere yapılandırılmış bulut koruma.
5. Sanal makineler için koruma etkin ve toocomplete ilk çoğaltma sağlar.
6. Birkaç saat sistem sabitlemeyi beklendi.
7. Performans ölçümleri, tüm sanal makineler için bu 12 saat içinde beklenen çoğaltma durumunda kalan sağlama üzerinde 12 saat yakalandı.
8. Ölçü hello delta hello temel performans ölçümlerini hello çoğaltma performans ölçümleri arasındaki.


## <a name="primary-server-performance"></a>Birincil sunucu performansı

* Hyper-V çoğaltma, Itanium tabanlı sistemler için değişiklikleri tooa günlük dosyası en az depolama ek yükü ile Merhaba birincil sunucuda zaman uyumsuz olarak izler.
* Hyper-V çoğaltma, kendi kendine tutulan bellek önbelleği toominimize IOPS yükünü izlemek için kullanır. Bellek ve bunları hello önce hello günlük dosyasına, hello günlük zaman Boşaltılma VHDX toohello kurtarma sitesini gönderilen yazma toohello depolar. Merhaba yazma önceden belirlenmiş bir sınırına bir disk temizleme de olur.
* Merhaba grafiği aşağıdaki hello kararlı durum IOPS yükü çoğaltma için gösterir. IOPS yükü son tooreplication yaklaşık 5 oldukça düşük olan % olduğundan bu hello görebiliriz.

![Birincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Hyper-V çoğaltma hello birincil sunucu toooptimize disk performansı bellek kullanır. Hello grafiği aşağıdaki gösterildiği gibi ek yükü hello birincil kümedeki tüm sunucuların bellek Marjinal olur. Merhaba Bellek Yükü gösterilen hello karşılaştırıldığında çoğaltma yüklü toohello toplam bellek hello Hyper-V sunucusu tarafından kullanılan bellek yüzdesidir.

![Birincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Hyper-V çoğaltma minimum CPU yüke sahiptir. Merhaba grafikte gösterildiği gibi çoğaltma ek yükünü hello 2-%3 de aralığındadır.

![Birincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>İkincil (Kurtarma) sunucusu performansı

Hyper-V çoğaltma hello kurtarma sunucusu toooptimize hello sayısına depolama işlemleri az miktarda bellek kullanır. Merhaba grafik hello kurtarma sunucusundaki hello bellek kullanımını özetler. Merhaba Bellek Yükü gösterilen hello karşılaştırıldığında çoğaltma yüklü toohello toplam bellek hello Hyper-V sunucusu tarafından kullanılan bellek yüzdesidir.

![İkincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

g/ç işlemleri hello kurtarma sitesinde Hello miktarını hello birincil site yazma işlemlerinin hello sayısının bir işlevdir. Şimdi hello toplam g/ç işlemleri hello toplam g/ç işlemleri karşılaştırıldığında hello kurtarma sitesindeki bakın ve yazma işlemlerini hello birincil sitede. Bu hello toplam IOPS hello kurtarma sitesinde olduğu Hello grafikleri Göster

* Yaklaşık 1,5 katı hello hello birincil IOPS yazma.
* Yaklaşık hello % 37'si IOPS hello birincil sitede toplam sayısı.

![İkincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![İkincil sonuçlar](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Ağ kullanımı etkisi

275 MB ağ bant genişliğinin saniyedeki ortalama hello birincil ve kurtarma düğümler arasında bir var olan 5 Gb bant genişliği saniye başına karşı (etkin sıkıştırma ile) kullanıldı.

![Sonuçlar ağı kullanımı](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>VM performans üzerindeki etkisi

Önemli bir konu hello sanal makinelerde çalışan üretim iş yükleri üzerindeki çoğaltma hello etkisidir. Merhaba birincil site çoğaltma için yeterli sağlandığında, hello iş yükleri üzerinde hiçbir etkisi olması döndürmemelidir. Hyper-V çoğaltma'nın basit mekanizması izleme hello sanal makinelerde çalışan iş yükleri kararlı durum çoğaltma sırasında etkilenmez sağlar. Bu grafik aşağıdaki hello gösterilmiştir.

Bu grafik, farklı iş yükleri önce çalışan sanal makineler tarafından ve çoğaltma etkinleştirildikten sonra gerçekleştirilen IOPS gösterir. Merhaba iki arasında fark olduğunu görebilirsiniz.

![Çoğaltma efekti sonuçları](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Merhaba aşağıdaki grafik hello verimlilik önce farklı iş yüklerini çalıştıran sanal makinelerin ve çoğaltma etkinleştirildikten sonra gösterir. Çoğaltmanın önemli bir etkisi yoktur görebilirsiniz.

![Sonuçlar çoğaltma etkileri](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Sonuç

Azure Site Recovery, Hyper-V çoğaltma ile birlikte ek yükü büyük bir küme için en az ile iyi ölçeklenir Hello sonuçları açıkça gösterir.  Azure Site Recovery, basit dağıtım, çoğaltma, yönetim ve izleme sağlar. Hyper-V çoğaltma, başarılı çoğaltma ölçekleme için hello gerekli altyapıyı sağlar. En iyi dağıtım planlama hello indirdiğiniz öneririz [Hyper-V çoğaltma kapasite Planlayıcısı](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Sınama ortamı ayrıntıları

### <a name="primary-site"></a>Birincil site

* Merhaba birincil site 470 sanal makineleri çalıştıran beş Hyper-V sunucuları içeren bir küme var.
* farklı iş yükleri Hello sanal makineleri çalıştırmak ve tüm Azure Site Recovery koruması etkin sahip.
* Depolama hello küme düğümü için iSCSI SAN tarafından sağlanır. Model – Hitachi HUS130.
* Her küme sunucusu bir Gbps dört ağ kartı (NIC) sahiptir.
* İki hello ağ kartları bağlı tooan iSCSI özel ağ ve iki bağlı tooan dış kurumsal ağ. Merhaba dış ağlara birini yalnızca küme iletişimi için ayrılmıştır.

![Birincil donanım gereksinimleri](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Sunucu | RAM | modeli | İşlemci | İşlemci sayısı | NIC | Yazılım |
| --- | --- | --- | --- | --- | --- | --- |
| Kümede Hyper-V sunucuları: <br />ESTLAB HOST11<br />ESTLAB HOST12<br />ESTLAB HOST13<br />ESTLAB HOST14<br />ESTLAB HOST25 |256 128ESTLAB HOST25 sahip |Dell™ PowerEdge™ R820 |Intel(r) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 |I x 4 GB/sn |Windows Server Datacenter 2012 R2 (x64) + Hyper-V rolü |
| VMM sunucusu |2 | | |2 |1 Gbps |Windows Server 2012 veritabanı R2 (x 64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>İkincil (Kurtarma) sitesi

* Merhaba ikincil sitenin altı düğümlü yük devretme kümesi vardır.
* Depolama hello küme düğümü için iSCSI SAN tarafından sağlanır. Model – Hitachi HUS130.

![Birincil donanım belirtimi](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Sunucu | RAM | modeli | İşlemci | İşlemci sayısı | NIC | Yazılım |
| --- | --- | --- | --- | --- | --- | --- |
| Kümede Hyper-V sunucuları: <br />ESTLAB HOST07<br />ESTLAB HOST08<br />ESTLAB HOST09<br />ESTLAB HOST10 |96 |Dell™ PowerEdge™ R720 |Intel(r) Xeon(R) CPU E5-2630 0 @ 2.30GHz |2 |I x 4 GB/sn |Windows Server Datacenter 2012 R2 (x64) + Hyper-V rolü |
| ESTLAB HOST17 |128 |Dell™ PowerEdge™ R820 |Intel(r) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V rolü |
| ESTLAB HOST24 |256 |Dell™ PowerEdge™ R820 |Intel(r) Xeon(R) CPU E5-4620 0 @ 2.20GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V rolü |
| VMM sunucusu |2 | | |2 |1 Gbps |Windows Server 2012 veritabanı R2 (x 64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Sunucu iş yükleri

* Test amaçları için Kurumsal müşteri senaryolarda yaygın olarak kullanılan iş yükleri Çekildi.
* Kullanırız [IOMeter](http://www.iometer.org) benzetimi için hello tabloda özetlenen hello iş yükü özelliği ile.
* Tüm IOMeter profilleri toowrite rastgele bayt toosimulate en kötü durum yazma desenleri iş yükleri için ayarlanır.

| İş yükü | G/ç boyutu (KB) | % Erişim | % Okuma | Bekleyen g/ç | G/ç düzeni |
| --- | --- | --- | --- | --- | --- |
| Dosya sunucusu |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |% Rastgele tüm 100 |
| SQL Server (birim 1) SQL Server (2 birimi) |864 |100%100% |70%0% |88 |% 100 random100% sıralı |
| Exchange |32 |100% |67% |8 |% 100 rastgele |
| İş istasyonu/VDI |464 |66%34% |70%95% |11 |Her iki % 100 rastgele |
| Web dosya sunucusu |4864 |33%34%33% |95%95%95% |888 |Tüm %75 rastgele |

### <a name="vm-configuration"></a>VM yapılandırması

* Merhaba birincil kümesinde 470 sanal makineler.
* Tüm sanal makinelerle VHDX disk.
* Merhaba tabloda özetlenen iş yüklerini çalıştıran sanal makineler. Tüm VMM şablonları ile oluşturulmuş.

| İş yükü | # VM'ler | En düşük RAM (GB) | En fazla RAM (GB) | VM başına mantıksal disk boyutu (GB) | Maksimum IOPS |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| Dosya sunucusu |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Web sunucusu |149 |.5 |1 |80 |6 |
| TOPLAM |470 | | |96.83 TB |4108 |

### <a name="site-recovery-settings"></a>Site Recovery ayarları

* Azure Site Recovery şirket içi tooon içi koruma için yapılandırılmış
* Merhaba VMM Sunucu hello Hyper-V küme sunucuları ve sanal makinelerinin içeren yapılandırılan, dört Bulutlar sahiptir.

| Birincil VMM Bulutu | Korunan hello bulutta sanal makineler | Çoğaltma sıklığı | Ek kurtarma noktaları |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 dakika |None |
| PrimaryCloudRpo30s |47 |30 saniye |None |
| PrimaryCloudRpo30sArp1 |47 |30 saniye |1 |
| PrimaryCloudRpo5m |235 |5 dakika |None |

### <a name="performance-metrics"></a>Performans ölçümleri

Merhaba tablo hello performans ölçümleri ve hello dağıtımında ölçülen sayaçları özetler.

| Ölçüm | Sayaç |
| --- | --- |
| CPU |\Processor(_Total)\% Processor Time |
| Kullanılabilir bellek |\Memory\Available MBayt |
| IOPS |\PhysicalDisk (_Total) \Disk aktarımı/sn |
| VM okuma (IOPS) işlemleri/sn |\Hyper-V sanal depolama aygıtı (<VHD>) \Read işlemi/sn |
| VM yazma (IOPS) işlemi/sn |\Hyper-V sanal depolama aygıtı (<VHD>) \Write Operations/S |
| VM üretilen işi okuma |\Hyper-V sanal depolama aygıtı (<VHD>) \Read bayt/sn |
| VM yazma üretimi |\Hyper-V sanal depolama aygıtı (<VHD>) \Write bayt/sn |

## <a name="next-steps"></a>Sonraki adımlar

[İki şirket içi VMM siteler arasında çoğaltmayı ayarlama](site-recovery-vmm-to-vmm.md)

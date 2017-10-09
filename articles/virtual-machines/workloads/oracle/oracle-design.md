---
title: "Azure üzerinde veritabanı aaaDesign ve uygulama bir Oracle | Microsoft Docs"
description: "Tasarım ve Azure ortamınızda bir Oracle veritabanına uygulayın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Bir Oracle veritabanına Azure'da tasarlayıp

## <a name="assumptions"></a>Varsayımlar

- Şirket içi tooAzure Oracle veritabanından toomigrate planlamanız durumunda.
- Oracle AWR raporlarda çeşitli ölçümleri hello bilgiye sahip.
- Uygulama performansı ve platform kullanımı bir temel bilgilere sahipsiniz.

## <a name="goals"></a>Hedefleri

- Anlamak nasıl toooptimize Oracle dağıtımınızda Azure.
- Bir Oracle veritabanına bir Azure ortamı için seçenekleri ayarlama performans keşfedin.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Merhaba şirket içi arasındaki farklar ve Azure uygulaması 

Bazı şeyleri tookeep geçirilirken aklınızda içi uygulamaları tooAzure önemli şunlardır. 

Bir önemli fark, bir Azure uygulamasında VM'ler, diskler ve sanal ağlar gibi kaynakları diğer istemciler arasında paylaşılır kaynaklanır. Ayrıca, kaynakları hello gereksinimlerine göre kısıtlanan. (MTBF) başarısız önleme odaklanan yerine Azure daha hello hatası (MTTR) geri kalan odaklanmıştır.

Merhaba aşağıdaki tabloda bazı hello bir şirket içi uygulama ve Oracle veritabanına Azure uygulaması arasındaki farklar listelenmektedir.

> 
> |  | **Şirket içi uygulama** | **Azure uygulama** |
> | --- | --- | --- |
> | **Ağ** |LAN VE WAN  |SDN (yazılım tanımlı ağ)|
> | **Güvenlik grubu** |IP/bağlantı noktasına kısıtlama araçları |[Ağ güvenlik grubu (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Esnekliği** |MTBF (hataları arasındaki ortalama süre) |MTTR (saati toorecovery)|
> | **Planlı bakım** |Düzeltme eki uygulama yükseltme|[Kullanılabilirlik kümeleri](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (düzeltme eki uygulama/Azure tarafından yönetilen yükseltme) |
> | **Kaynak** |Adanmış  |Diğer istemcilerle paylaşılan|
> | **Bölgeler** |Veri merkezleri |[Bölge çiftleri](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Depolama** |SAN/fiziksel diskleri |[Azure tarafından yönetilen depolama](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Ölçeklendirme** |Dikey Ölçek |Yatay ölçeklendirme|


### <a name="requirements"></a>Gereksinimler

- Başlangıç veritabanı boyutu ve büyüme oranını belirler.
- Oracle AWR raporları veya diğer ağ izleme araçları göre tahmin hello IOPS gereksinimlerini belirleyin.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

Bir Azure ortamı tooimprove performans ayarlayabilirsiniz dört olası alanları şunlardır:

- Sanal makine boyutu
- Ağ verimliliği
- Disk türleri ve yapılandırmalar
- Disk önbelleği ayarları

### <a name="generate-an-awr-report"></a>Bir AWR raporu oluşturun

Varolan bir Oracle veritabanına varsa ve toomigrate tooAzure planlama, birkaç seçeneğiniz vardır. Merhaba Oracle AWR rapor tooget hello ölçümleri (IOPS, MB/sn, GiBs ve benzeri) çalıştırabilirsiniz. Ardından hello VM topladığınız hello ölçülerine bağlı olarak seçin. Veya, altyapı takım tooget benzer bilgilerinizi başvurun.

Karşılaştırabileceğiniz normal ve yoğun saatler iş yükleri sırasında AWR raporunuzu çalıştıran düşünebilirsiniz. Bu raporlarda bağlı olarak, sanal makineleri hello ortalama iş yükü veya hello en fazla iş yükünü dayanarak hello boyutlandırabilirsiniz.

Aşağıdaki nasıl örneğidir toogenerate AWR raporu:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Anahtar ölçümleri

Hello AWR raporu ' edinebilirsiniz hello ölçümler şunlardır:

- Çekirdek toplam sayısı
- CPU saat hızı
- GB cinsinden toplam bellek
- CPU kullanımı
- En yüksek veri aktarım hızı
- G/ç değişiklikleri (okuma/yazma) oranı
- Günlük oranı (MBPs) Yinele
- Ağ verimliliği
- Ağ gecikmesi hızı (düşük/yüksek)
- Veritabanı boyutu GB
- SQL ile alınan bayt sayısı * ağı birbirinden / tooclient

### <a name="virtual-machine-size"></a>Sanal makine boyutu

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. VM boyutu hello CPU, bellek ve g/ç kullanımdan AWR rapor temel tahmin etme

Bakmak bir hello sistem performans sorunlarının nerede belirten hello üst beş zamanlanmış ön plan olayları şeydir.

Örneğin, diyagram aşağıdaki hello hello günlük dosyası eşitleme hello tepesinde bulunur. Merhaba LGWR hello günlük arabellek toohello Yinele günlük dosyasına yazar önce gerekli olan bekler hello sayısını gösterir. Bu sonuçları, daha iyi performanslı depolama veya diskleri gerekli olduğunu gösterir. Ayrıca, hello diyagramı CPU (çekirdekler) hello sayısını ve hello bellek miktarını gösterir.

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/cpu_memory_info.png)

Merhaba Aşağıdaki diyagramda hello toplam g/ç okuma ve yazma gösterilmektedir. 59 okuma GB ve 247.3 hello rapor hello süre boyunca yazılmış GB vardı.

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Bir VM seçin

Merhaba AWR rapor ' toplanan hello bilgilere dayanarak, hello sonraki toochoose gereksinimlerinizi karşılayan benzer bir boyutu VM'i adımdır. Kullanılabilir sanal makineleri listesini hello makalesinde bulabilirsiniz [bellek için iyileştirilmiş](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Merhaba ACU üzerinde temel benzer bir VM dizisi ile Merhaba VM boyutlandırma ince ayar yapma

Merhaba VM seçtikten sonra dikkat toohello ACU hello VM için ödeme yaparsınız. Gereksinimlerinize daha iyi uyacak ACU değeri hello üzerinde göre farklı bir VM seçebilirsiniz. Daha fazla bilgi için bkz: [Azure işlem birimi](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Merhaba ACU birimleri sayfasının ekran görüntüsü](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Ağ verimliliği

Diyagram aşağıdaki hello hello verimlilik ve IOPS arasındaki ilişki gösterilmektedir:

![Üretilen iş ekran görüntüsü](./media/oracle-design/throughput.png)

Merhaba toplam ağ verimini aşağıdaki bilgilerle hello göre tahmini:
- SQL * Net trafiği
- MB/sn x sunucularını (Oracle Data Guard gibi giden akış) sayısı
- Uygulama çoğaltma gibi diğer faktörlere

![Ekran görüntüsü hello SQL * Net işleme](./media/oracle-design/sqlnet_info.png)

Ağ bant genişliği gereksinimlerine bağlı olarak, çeşitli ağ geçidi türleri, toochoose için vardır. Bunlar, temel, VpnGw ve Azure ExpressRoute içerir. Daha fazla bilgi için bkz: Merhaba [VPN ağ geçidi fiyatlandırma sayfası](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Öneriler**

- Ağ gecikmesi yüksek karşılaştırılan tooan şirket içi dağıtımıdır. Ağ dönüşleri can round önemli ölçüde azaltan performansı artırır.
- tooreduce gidiş dönüş birleştirmek yüksek işlemler veya "chatty" uygulamalar üzerinde hello olan uygulamalar aynı sanal makine.

### <a name="disk-types-and-configurations"></a>Disk türleri ve yapılandırmalar

- *Varsayılan işletim sistemi disk*: kalıcı veri ve önbelleğe alma bu disk türleri sunar. Başlangıçta OS erişimi için optimize ve için tasarlanmamış işlemsel veya veri ambarı (analitik) iş yükleri.

- *Yönetilmeyen diskleri*: Bu disk türleriyle tooyour VM diskleri karşılık hello sanal sabit disk (VHD) dosyaları depolamak hello depolama hesaplarını yönetme. VHD dosyaları, Azure storage hesapları sayfa bloblarını olarak depolanır.

- *Yönetilen diskleri*: Azure VM diskleriniz için kullandığınız hello depolama hesapları yönetir. Merhaba disk türünü (premium veya standart) ve hello ihtiyacınız hello diskin boyutunu belirtin. Azure oluşturur ve hello disk tarafından yönetilir.

- *Premium depolama diskleri*: Bu disk türleri üretim iş yükleri için uygundur. Olabilir premium depolama destekler VM diskleri ekli toospecific boyutu-serisi VM, DS, DSv2, GS ve F serisi VM'ler gibi. farklı boyutlarda ile Merhaba premium disk gelir ve 096 GB 32 GB too4 arasında değişen diskleri arasından seçim yapabilirsiniz. Her disk boyutu, kendi performans özellikleri vardır. Uygulama gereksinimlerinize bağlı olarak, bir veya daha fazla disk tooyour VM ekleyebilirsiniz.

Merhaba portalından yeni bir yönetilen disk oluşturduğunuzda, hello seçebilirsiniz **hesap türü** hello disk türünün toouse istiyor. Tüm kullanılabilir diskleri hello açılır menüde gösterilmiştir aklınızda bulundurun. Belirli bir VM boyutu seçtikten sonra hello menüsü yalnızca hello kullanılabilir premium storage bu VM boyutuna göre SKU'ları gösterir.

![Merhaba yönetilen disk sayfasının ekran görüntüsü](./media/oracle-design/premium_disk01.png)

Daha fazla bilgi için bkz: [yüksek performanslı Premium depolama ve VM'ler için yönetilen diskleri](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Depolama alanınızın bir VM üzerinde yapılandırdıktan sonra bir veritabanı oluşturmadan önce tooload test hello diskleri isteyebilirsiniz. Gecikme süresi ve Verimlilik açısından Hello g/ç oranı hello VM'ler hello destekliyorsa belirlemenize yardımcı olacak bilerek işleme gecikmesi hedefleri ile bekleniyordu.

Uygulama yükleme, Oracle Orion, Sysbench ve Fio gibi test araçları mevcuttur.

Bir Oracle veritabanına dağıtıldıktan sonra hello yük testi yeniden çalıştırın. Normal ve yoğun saatler iş yükleri başlatın ve temel ortamınızın hello sonuçları göster hello.

Merhaba depolama boyutu yerine hello IOPS oranı göre daha önemli toosize hello depolama olabilir. Hello IOPS 5.000 olmakla birlikte, 200 GB yeterlidir gerekirse, birden fazla ile 200 GB depolama gelse de Örneğin, hala hello P30 sınıfı premium disk alabilirsiniz.

Merhaba IOPS oranı AWR rapor hello elde edilebilir. Merhaba Yinele günlük, fiziksel okuma ve yazma hızı tarafından belirlenir.

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/awr_report.png)

Örneğin, hello Yinele boyutuna eşit too11.63 MB / sn'dir saniye başına 12,200,000 bayt'tır.
Merhaba IOPS olan 12,200,000 / 2,358 = 5,174.

NET bir resim hello g/ç gereksinimlerinin aldıktan sonra bu gereksinimleri en iyi uygun toomeet sürücülerinin bir birleşimini seçebilirsiniz.

**Öneriler**

- Veri tablo alanı için yönetilen depolama veya Oracle ASM kullanarak hello g/ç iş yükü disk sayısı arasında yayılır.
- Merhaba g/ç blok boyutu yoğun okuma ve yazma yoğunluklu işlemleri için arttıkça, daha fazla veri diski ekleyin.
- Büyük sıralı işlemler için Hello blok boyutunu artırın.
- Veri sıkıştırma tooreduce g/ç (veri ve dizinler için) kullanın.
- Yinele günlükleri, sistem ve temps ayrı ve farklı veri disklerinde TS geri.
- Varsayılan işletim sistemi diskleri (/ dev/sda) tüm uygulama dosyalarını koymayın. Bu diskleri en iyi duruma getirilmiş olmayan için hızlı VM önyükleme zamanları ve uygulamanız için iyi bir performans sağlamayabilir.

### <a name="disk-cache-settings"></a>Disk önbelleği ayarları

Ana bilgisayar önbelleğe almayı için üç seçenek vardır:

- *Salt okunur*: gelecekteki okuma için tüm istekleri önbelleğe alınır. Tüm yazma işlemlerini kalıcı doğrudan tooAzure Blob Depolama.

- *Okuma-yazma*: "İleri okuma" algoritma budur. Hello okuma ve yazma işlemleri için gelecekteki okuma önbelleğe alınır. Olmayan yazma aracılığıyla yazma olan toohello yerel önbelleği ilk kalıcı. Yazma aracılığıyla kullandığı için SQL Server için yazma kalıcı tooAzure depolama var. Hafif iş yükleri için hello düşük disk gecikme süresi de sağlar.

- *Hiçbiri* (devre dışı): Bu seçeneği kullanarak, hello önbellek atlayabilir. Tüm hello veriler aktarılan toodisk ve tooAzure depolama kalıcı. G/ç yoğun iş yükleri için yüksek g/ç oranı hello bu yöntemi sağlar. Ayrıca dikkate tootake "Maliyet" gerekir.

**Öneriler**

toomaximize hello verimlilik öneririz başlamanız **hiçbiri** ana bilgisayar önbelleğe almayı için. Premium Storage için hello hello dosya sistemiyle bağladığınızda, hello "engelleri" devre dışı bırakmalısınız olduğunu aklınızda bulundurun **ReadOnly** veya **hiçbiri** seçenekleri. Merhaba /etc/fstab dosyasını hello UUID toohello diskler ile güncelleştirin.

Daha fazla bilgi için bkz: [Linux VM'ler için Premium depolama](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Merhaba yönetilen disk sayfasının ekran görüntüsü](./media/oracle-design/premium_disk02.png)

- Varsayılan işletim sistemi disklerinde kullanmak **okuma/yazma** önbelleğe alma.
- Sistem, TEMP ve geri alma için kullanmak **hiçbiri** önbelleğe alma için.
- VERİLERİN kullanmanız **hiçbiri** önbelleğe alma için. Ancak, veritabanı salt okunur veya okuma açısından yoğun ise, **salt okunur** önbelleğe alma.

Veri diski ayarınız kaydedildikten sonra hello işletim sistemi düzeyinde hello sürücü çıkarın ve hello değişiklik yaptıktan sonra yeniden sürece hello konağı önbellek ayarı değiştiremezsiniz.


## <a name="security"></a>Güvenlik

Ayarlama ve Azure ortamınıza yapılandırdıktan sonra hello sonraki toosecure adımdır ağınıza. Bazı öneriler şunlardır:

- *NSG İlkesi*: NSG bir alt ağ veya NIC tarafından tanımlanabilir Bu daha basit toocontrol erişim hello alt ağ düzeyinde hem de güvenlik ve uygulama güvenlik duvarları gibi şeyler için zorla yönlendirme olur.

- *Jumpbox*: daha güvenli erişim için Yöneticiler doğrudan toohello uygulama hizmeti veya veritabanı bağlanmayacak. Bir jumpbox hello yönetici makine ve Azure kaynakları arasında bir ortam olarak kullanılır.
![Merhaba Jumpbox topoloji sayfasının ekran görüntüsü](./media/oracle-design/jumpbox.png)

    Hello Yöneticisi Makine IP kısıtlı erişim toohello yalnızca jumpbox sunmaktadır. Merhaba jumpbox erişim toohello uygulama ve veritabanı olmalıdır.

- *Özel ağ* (alt ağlar): daha iyi denetim NSG İlkesi tarafından ayarlanabilir böylece, hello uygulama hizmeti ve veritabanı farklı alt ağlarda sahip olmasını öneririz.


## <a name="additional-reading"></a>Ek kaynaklar

- [Oracle ASM’yi yapılandırma](configure-oracle-asm.md)
- [Oracle Data Guard yapılandırın](configure-oracle-dataguard.md)
- [Oracle Golden kapısı yapılandırın](configure-oracle-golden-gate.md)
- [Oracle yedekleme ve kurtarma](oracle-backup-recovery.md)

## <a name="next-steps"></a>Sonraki adımlar

- [Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma](../../linux/create-cli-complete.md)
- [VM dağıtımı Azure CLI örnekleri keşfedin](../../linux/cli-samples.md)

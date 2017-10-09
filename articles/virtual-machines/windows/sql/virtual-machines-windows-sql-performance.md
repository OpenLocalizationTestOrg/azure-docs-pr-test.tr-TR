---
title: "Azure SQL Server için en iyi uygulamaları aaaPerformance | Microsoft Docs"
description: "Microsoft Azure vm'lerinde SQL Server performansını iyileştirmek için en iyi yöntemler sağlar."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Azure Sanal Makinelerde SQL Server için performansa yönelik en iyi yöntemler

## <a name="overview"></a>Genel Bakış

Bu konu, Microsoft Azure sanal makinesi'nın SQL Server performansını iyileştirmek için en iyi yöntemler sağlar. Azure sanal makinelerde SQL Server çalıştırılırken kullanmaya devam öneririz hello aynı veritabanı performans şirket içi bir sunucu ortamında uygulanabilir tooSQL sunucu seçenekleri ayarlama. Ancak, genel bulut ilişkisel bir veritabanında hello performansını hello boyutunu bir sanal makine ve hello veri diski hello yapılandırması gibi birçok faktöre bağlıdır.

SQL Server görüntülerini oluştururken [Vm'leriniz hello Azure portal'ın sağlama göz önünde bulundurun](virtual-machines-windows-portal-sql-server-provision.md). SQL Server hello Portal Resource Manager ile sağlanan VM'ler hello depolama yapılandırması dahil olmak üzere tüm bu en iyi yöntemler, uygular.

Bu makalede hello odaklanmıştır *en iyi* Azure Vm'lerde SQL Server için performans. İş yükünüzün daha az yoğun ise, aşağıda listelenen her iyileştirme gerektirmeyebilecek. Bu öneriler değerlendirirken yükünün desenleri ve performans gereksinimlerini göz önünde bulundurun.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Hızlı onay listesi

Merhaba, Azure Virtual Machines'de SQL Server'ın en iyi performans için bir hızlı onay listesi aşağıdadır:

| Alan | En iyi duruma getirme |
| --- | --- |
| [VM boyutu](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) veya SQL Enterprise edition için daha yüksek.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) veya SQL Standard ve Web sürümleri için daha yüksek. |
| [Depolama](#storage-guidance) |Kullanım [Premium depolama](../../../storage/common/storage-premium-storage.md). Standart depolama yalnızca geliştirme ve test için önerilir.<br/><br/>Merhaba tutmak [depolama hesabı](../../../storage/common/storage-create-storage-account.md) ve SQL Server VM hello ile aynı bölgede.<br/><br/>Azure devre dışı [coğrafi olarak yedekli depolama](../../../storage/common/storage-redundancy.md) (coğrafi çoğaltma) hello depolama hesabı üzerinde. |
| [Diskleri](#disks-guidance) |En az 2 kullanmak [P30 diskleri](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (günlük dosyaları için 1; veri dosyaları ve TempDB için 1).<br/><br/>Veritabanı depolama veya günlük için işletim sistemi veya geçici diskleri kullanmaktan kaçının.<br/><br/>Merhaba veri dosyaları ve TempDB barındırma hello diskler üzerinde okuma önbelleğe almayı etkinleştir.<br/><br/>Merhaba günlük dosyası barındırma diskler üzerinde önbelleğe alma etkinleştirmeyin.<br/><br/>Önemli: hello önbellek ayarlarını bir Azure VM diski değiştirirken hello SQL Server hizmetini durdurun.<br/><br/>Birden çok Azure veri diskleri artan tooget g/ç işleme şeritler.<br/><br/>Belgelenen ayırma boyutlarıyla biçimlendirin. |
| [G/Ç](#io-guidance) |Veritabanı Sayfa sıkıştırmayı etkinleştirin.<br/><br/>Veri dosyaları için anında dosya başlatma etkinleştirin.<br/><br/>Sınırlamak veya hello veritabanı otomatik büyüme devre dışı bırakın.<br/><br/>Merhaba veritabanında daralma devre dışı bırakın.<br/><br/>Sistem veritabanları dahil olmak üzere tüm veritabanları toodata diskleri taşıyın.<br/><br/>SQL Server hata günlüğü ve izleme dosyası dizin toodata diskleri taşıyın.<br/><br/>Varsayılan yedekleme ve veritabanı dosyası konumlarını ayarlayın.<br/><br/>Kilitli sayfalar etkinleştirin.<br/><br/>SQL Server performans düzeltmeleri uygulayın. |
| [Özel özellik](#feature-specific-guidance) |Doğrudan tooblob depolama alanı yedekleyin. |

Daha fazla bilgi için *nasıl* ve *neden* toomake bu en iyi duruma getirme, lütfen inceleyin hello Ayrıntılar ve aşağıdaki bölümlerde verilen Kılavuzu.

## <a name="vm-size-guidance"></a>VM boyutu Kılavuzu

Performans hassas uygulamalar için hello aşağıdakileri kullanmanız önerilir [sanal makine boyutları](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 veya üzeri
* **SQL Server Standard ve Web sürümleri**: DS2 veya üzeri

## <a name="storage-guidance"></a>Depolama Kılavuzu

DS serisi (birlikte, DSv2 serisi ve GS serisi) VM'ler Destek [Premium depolama](../../../storage/common/storage-premium-storage.md). Premium depolama tüm üretim iş yükleri için önerilir.

> [!WARNING]
> Standart depolama değişen gecikmeleri ve bant genişliği vardır ve yalnızca geliştirme ve test iş yükleri için önerilir. Premium Storage üretim iş yükleri kullanmanız gerekir.

Ayrıca, Azure depolama hesabınızın hello oluşturmanızı öneririz, SQL Server sanal makineleri tooreduce aktarımı gecikmeler olarak aynı veri merkezinde. Birden çok disk arasında tutarlı yazma sipariş yıkıcıları gibi bir depolama hesabı oluştururken, coğrafi çoğaltma devre dışı bırakın. Bunun yerine, bir SQL Server olağanüstü durum kurtarma teknoloji iki Azure veri merkezleri arasında yapılandırmayı göz önünde bulundurun. Daha fazla bilgi için bkz: [yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Diskleri Kılavuzu

Azure VM temelinde üç ana disk türleri şunlardır:

* **İşletim sistemi diski**: bir Azure sanal makine oluşturduğunuzda, en az bir disk hello platform ekleyecek (hello etiketlenen **C** sürücü) toohello VM, işletim sistemi diski. Bu disk, depolama birimindeki bir sayfa blob'u olarak kaydedilen bir vhd'dir.
* **Geçici disk**: Azure sanal makineleri içeren hello geçici disk adlı başka bir diske (hello etiketlenen **D**: sürücü). Bir disk için boş alanın kullanılabilir hello düğüm üzerinde budur.
* **Veri diskleri**: ek diskleri tooyour sanal makine veri diski iliştirebilirsiniz ve bu sayfa blobları depolama alanında depolanır.

Merhaba aşağıdaki bölümlerde bu farklı diskler kullanarak önerileri açıklanmaktadır.

### <a name="operating-system-disk"></a>İşletim sistemi diski

Bir işletim sistemi diski, önyükleme ve bağlama çalışan bir işletim sistemi sürümü olarak bir VHD olduğunu ve olarak etiketli **C** sürücü.

Varsayılan ilke hello işletim sistemi disk üzerinde önbelleğe alma **okuma/yazma**. Performans hassas uygulamalar için veri diski hello işletim sistemi diski yerine kullanmanızı öneririz. Aşağıdaki veri diskler üzerinde Hello bölümüne bakın.

### <a name="temporary-disk"></a>Geçici disk

Merhaba hello etiketlenen geçici depolama sürücüsü **D**: sürücü, kalıcı tooAzure blob depolama birimi değil. Kullanıcı veritabanı dosyaları veya kullanıcı işlem günlüğü dosyalarını hello depolamayın **D**: sürücü.

D-serisi, Dv2-serisi ve G-serisi VM'ler için hello geçici bu vm'lerde SSD tabanlı sürücüdür. İş yükünüzün TempDB yoğun olarak kullanılır (örneğin geçici nesneler veya karmaşık birleştirmeler) yaparsa TempDB üzerinde hello depolama **D** sürücü neden yüksek TempDB performansı ve TempDB gecikme süresini azaltın.

Premium depolama (DS serisi, DSv2 serisi ve GS serisi) desteği VM'ler için etkinleştirilmiş okuma önbelleği ile Premium Storage destekleyen bir diskte TempDB depolamanızı öneririz. Bir özel durum toothis öneri yoktur; TempDB kullanımınızı yazma yoğunluklu ise, TempDB hello yerel depolayarak daha yüksek performans elde edebilirsiniz **D** de bu makine boyutlarına SSD tabanlı sürücü.

### <a name="data-disks"></a>Veri diskleri

* **Veri diskleri veri ve günlük dosyaları için kullanan**: en az 2 Premium depolama kullanan [P30 diskleri](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) burada bir disk hello günlük dosyalarını ve hello diğer hello veri ve TempDB dosyaları içerir. Aşağıdaki makaleye bakın hello açıklandığı gibi bir dizi IOPS ve bant genişliği (MB/sn) boyutuna bağlı olarak her Premium depolama diski sağlar: [diskler için Premium depolama alanını kullanarak](../../../storage/common/storage-premium-storage.md).

* **Disk şeritleme**: daha fazla verimlilik için ek veri disklerinin ekleyebilir ve Disk şeritleme kullanabilirsiniz. veri diski toodetermine hello sayısı, IOPS ve günlük dosyalarınızı ve verilerinizi ve TempDB dosyalar için gereken bant sayısını tooanalyze hello gerekir. Farklı VM boyutları hello sayısına IOP ve desteklenen bant farklı sınırlar olduğunu fark, hello tablo başına IOPS bakın [VM boyutu](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Yönergeleri izleyerek hello kullan:

  * Windows 8/Windows Server 2012 veya daha sonra kullanmak [depolama alanları](https://technet.microsoft.com/library/hh831739.aspx) yönergeleri izleyerek hello ile:

      1. Set hello Interleave (stripe boyutu) OLTP iş yükleri ve veri ambarı iş yükleri tooavoid performans etkisi toopartition uyuşmazlığın son için 256 KB (262144 bayt) too64 KB (65536 bayt). PowerShell ile ayarlamanız gerekir.
      1. Ayarlama sütun sayısı = fiziksel disk sayısı. Birden fazla 8 disk (Sunucu Yöneticisi kullanıcı Arabirimi olmayan) yapılandırırken PowerShell kullanın. 

    Örneğin, aşağıdaki PowerShell hello yeni oluşturur hello sahip depolama havuzuna Interleave boyutu too64 KB ve hello sayısı sütunları too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Windows 2008 R2 veya önceki sürümleri, hello Şerit boyutunun her zaman 64 KB'tır ve dinamik diskler (işletim sistemi şeritli birimler) kullanabilirsiniz. Bu seçenek Windows 8/Windows sürümünden itibaren Server 2012 kullanım dışıdır unutmayın. Merhaba destek ifadesine bilgi için bkz [Sanal Disk Hizmeti tooWindows Depolama Yönetimi API'si geçiş](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * İş yükünüzün günlük yoğun değil ve ayrılmış IOPS gerekli değildir, yalnızca bir depolama havuzu yapılandırabilirsiniz. Aksi takdirde, iki depolama havuzları, biri hello günlük dosyalarını ve hello veri dosyaları ve TempDB için başka bir depolama havuzu oluşturun. Yük beklentileri üzerine her depolama havuzu ile ilişkili disk Hello sayısını belirler. Farklı VM boyutları eklenen veri disklerini farklı sayıda izin göz önünde bulundurun. Daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Premium depolama (dev/test senaryoları) kullanmıyorsanız, hello tooadd hello maksimum tarafından desteklenen veri diski sayısı önerilir, [VM boyutu](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve Disk şeritleme kullanın.

* **İlke önbelleği**: için Premium depolama veri diskler, veri dosyaları ve TempDB yalnızca barındırma hello veri disklerde okuma önbelleği sağlar. Premium depolama kullanmıyorsanız, tüm veri disklerde önbelleğe alma etkinleştirmeyin. Disk önbelleği, yapılandırma yönergeleri görmek için aşağıdaki konularda hello: [kümesi AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) ve [kümesi AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Azure VM diskleri tooavoid hello veritabanında bozulma olasılığını hello önbellek ayarını değiştirirken Hello SQL Server hizmetini durdurun.

* **NTFS ayırma birimi boyutu**: hello veri diski biçimlendirme sırasında TempDB yanı sıra veri ve günlük dosyaları için 64 KB ayırma birimi boyutu kullanmanız önerilir.

* **Disk Yönetimi en iyi uygulamaları**: bir veri diski kaldırabilir veya önbelleğinde değiştirme yazdığınızda, hello değişiklik sırasında hello SQL Server hizmetini durdurun. Merhaba önbelleğe alma ayarlarını hello işletim sistemi disk üzerinde değişip Azure hello VM durdurur, hello önbellek türü değiştirir ve hello VM yeniden başlatır. Bir veri diski Hello önbellek ayarlarını değiştirildiğinde hello VM durdurulmadı ancak hello veri diski VM hello sırasında değiştirin ve sonra yeniden hello ayrılmış.

  > [!WARNING]
  > Hata toostop hello bu işlemleri sırasında SQL Server hizmeti veritabanında bozulmaya neden olabilir.

## <a name="io-guidance"></a>G/ç Kılavuzu

* Uygulama ve istekleri paralel hale zaman hello Premium depolama alanına sahip en iyi sonuçlar elde edilir. Premium depolama (depolama yoğun olan olsa bile) tek iş parçacıklı seri istekler için çok az kayıpla veya hiç performans artışı göreceğiniz şekilde hello GÇ sıra derinliği 1'den büyük olduğu senaryolar için tasarlanmıştır. Örneğin, bu performans çözümleme araçları SQLIO gibi hello tek iş parçacıklı test sonuçlarının etkileyebilir.

* Kullanmayı [veritabanı sayfa sıkıştırma](https://msdn.microsoft.com/library/cc280449.aspx) olarak g/ç yoğun iş yüklerinin performansını artırmaya yardımcı olabilir. Ancak, hello veri sıkıştırma hello CPU tüketimi hello veritabanı sunucusunda artırabilir.

* İlk dosya ayırma için gerekli olan anında dosya başlatma tooreduce hello zamanı etkinleştirmeyi düşünün. tootake avantajı anında dosya başlatma hello SQL Server (MSSQLSERVER) hizmeti hesabı SE_MANAGE_VOLUME_NAME ile vermek ve toohello ekleyin **Birim bakım görevlerini gerçekleştirme** güvenlik ilkesi. Azure için bir SQL Server platform görüntüsü kullanıyorsanız, hello varsayılan hizmet hesabı (NT Service\MSSQLSERVER) toohello eklenmez **Birim bakım görevlerini gerçekleştirme** güvenlik ilkesi. Diğer bir deyişle, anında dosya başlatma bir SQL Server Azure platform görüntüsünde etkin değil. Merhaba SQL Server hizmet hesabı toohello ekledikten sonra **Birim bakım görevlerini gerçekleştirme** güvenlik ilkesi, hello SQL Server hizmetini yeniden başlatın. Bu özelliği kullanmak için güvenlik konuları olabilir. Daha fazla bilgi için bkz: [veritabanı dosyası başlatma](https://msdn.microsoft.com/library/ms175935.aspx).

* **otomatik büyüme** toobe beklenmeyen büyüme için yalnızca bir yedek olarak kabul edilir. Veri ve günlük büyüme otomatik büyüme ile günlük aralıklarla yönetmez. Otomatik büyüme kullanılırsa, hello dosyası başlangıç boyutu anahtar kullanılarak önceden artar.

* Emin olun **daralma** performansını olumsuz yönde etkileyebilir devre dışı tooavoid gereksiz getirdiği yüktür.

* Sistem veritabanları dahil olmak üzere tüm veritabanları toodata diskleri taşıyın. Daha fazla bilgi için bkz: [sistem veritabanlarını taşıma](https://msdn.microsoft.com/library/ms345408.aspx).

* SQL Server hata günlüğü ve izleme dosyası dizin toodata diskleri taşıyın. Bu SQL Server Configuration Manager'ın SQL Server örneğinizi sağ tıklatıp Özellikler'i seçerek yapılabilir. Merhaba hata günlüğü ve izleme dosyası ayarlarını hello değiştirilebilir **başlangıç parametreleri** döküm dizini hello belirtilen sekmesini hello **Gelişmiş** ekran aşağıdaki sekmesini hello gösterir nereye toolook için Merhaba hata günlüğü başlangıç parametresi.

    ![SQL hata günlüğüne ekran görüntüsü](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Varsayılan yedekleme ve veritabanı dosyası konumlarını ayarlayın. Bu konudaki Hello önerileri kullanın ve hello sunucu özellikleri penceresinde hello değişiklikleri yapın. Yönergeler için bkz: [görüntüleme veya değiştirme hello veri ve günlük dosyaları (SQL Server Management Studio) için varsayılan konumları](https://msdn.microsoft.com/library/dd206993.aspx). Merhaba aşağıdaki ekran görüntüsü gösterilmektedir nereye toomake bu değişiklikler.

    ![SQL veri günlüğü ve yedekleme dosyaları](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Etkinleştirme sayfaları tooreduce GÇ ve disk belleği etkinlikler kilitli. Daha fazla bilgi için bkz: [etkinleştirmek hello kilit bellek seçeneği (Windows) sayfalarında](https://msdn.microsoft.com/library/ms190730.aspx).

* SQL Server 2012 çalıştırıyorsanız, Service Pack 1 Cumulative Update 10 yükleyin. SQL Server 2012'de geçici table deyimi içinde seçin yürüttüğünüzde Bu güncelleştirme performansın g/ç üzerinde için hello düzeltmeyi içerir. Bu bilgi için [Bilgi Bankası makalesi](http://support.microsoft.com/kb/2958012).

* Tüm veri dosyalarını Azure içeri/dışarı aktarılırken sıkıştırmayı göz önünde bulundurun.

## <a name="feature-specific-guidance"></a>Özellik özel yönergeler

Bazı dağıtımlarda daha gelişmiş yapılandırma teknikleri kullanarak ek performans avantajı elde edebilirsiniz. Merhaba aşağıdaki listede tooachieve daha iyi performans yardımcı olabilecek bazı SQL Server özelliklerini vurgular:

* **Yedekleme tooAzure depolama**: Azure sanal makinelerinde çalışan SQL Server için yedeklemeleri gerçekleştirirken kullanabileceğiniz [SQL Server Yedekleme tooURL](https://msdn.microsoft.com/library/dn435916.aspx). Bu, kullanılabilir SQL Server 2012 SP1 CU2 ile başlayan ve bağlı toohello veri diskleri yedekleme için önerilen özelliğidir. Ne zaman verilen hello önerileri izleyin, yedekleme/geri yükleme/Azure depolama biriminden [SQL Server Yedekleme tooURL en iyi yöntemler ve sorun giderme ve geri yükleme yedeklemeleri saklanmasını Azure storage'da](https://msdn.microsoft.com/library/jj919149.aspx). Ayrıca bu yedeklemeler kullanarak otomatikleştirebilirsiniz [Azure Virtual Machines'de SQL Server için otomatik yedekleme](virtual-machines-windows-sql-automated-backup.md).

    Önceki tooSQL Server 2012, kullanabileceğiniz [SQL Server Yedekleme tooAzure aracı](https://www.microsoft.com/download/details.aspx?id=40740). Bu araç, birden çok yedek stripe hedef kullanarak tooincrease yedekleme işleme yardımcı olabilir.

* **SQL Server veri dosyaları azure'da**: Bu yeni özellik [azure'da SQL Server veri dosyaları](https://msdn.microsoft.com/library/dn385720.aspx), SQL Server 2014 ile başlayarak kullanılabilir. Azure veri dosyaları ile SQL Server çalıştıran Azure veri diskleri kullanarak olarak karşılaştırılabilir performans özellikleri gösterir.

## <a name="next-steps"></a>Sonraki Adımlar

En iyi yöntemler için bkz: [Azure Virtual Machines'de SQL Server için güvenlik konuları](virtual-machines-windows-sql-security.md).

Diğer SQL Server sanal makine konuları gözden [Azure sanal makineleri genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

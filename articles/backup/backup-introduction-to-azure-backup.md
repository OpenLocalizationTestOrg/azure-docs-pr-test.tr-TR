---
title: Azure Backup aaaWhat mi? | Microsoft Belgeleri
description: "Azure Backup tooback kullanır ve verileri ve iş yükleri Windows sunucuları, Windows iş istasyonları, System Center DPM sunucuları ve Azure sanal makineleri geri yükleyin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "yedekleme ve geri yükleme; kurtarma hizmetleri; yedekleme çözümleri"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Azure yedekleme hello özelliklerine genel bakış
Azure yedekleme tooback kullanır (veya koruma) hello Azure tabanlı hizmeti nedir ve verilerinizi hello Microsoft bulut geri yükleyin. Azure Backup, var olan şirket içi veya şirket dışı yedekleme çözümünüzün yerine, güvenilir, güvenli ve maliyet açısından rekabetçi bir bulut tabanlı çözüm sunar. Azure yedekleme sunar indirin ve hello uygun bilgisayarda dağıtan birden çok bileşen sunucusu veya hello bulutta. Hello bileşeni ya da dağıttığınız aracısına bağlıdır, istediğiniz üzerinde tooprotect. Tüm Azure Backup bileşenleri (koruduğunuz verileri şirket içi olsun veya hello bulutta) veri Azure kurtarma Hizmetleri kasasına tooa yukarı kullanılan tooback olabilir. Merhaba bkz [Azure Backup bileşenleri tablo](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (Bu makalenin ilerisinde yer) hangi bileşen toouse tooprotect belirli verileri, uygulamalar veya iş yükleri hakkında bilgi için.

[Azure Backup'a genel bakış videosunu izleyin](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Azure Backup'ı neden kullanmalısınız?
Geleneksel yedekleme çözümleri tootreat hello bulut bir uç nokta ya da statik bir depolama hedefi, benzer toodisks veya bant olarak gelişim göstermiştir. Bu yaklaşım basit olmakla birlikte, sınırlıdır ve tooan pahalı, verimsiz çözüm çeviren bir alttaki bulut platformundan tam anlamıyla yararlanabilmek değil. Merhaba yanlış türde depolama ya da gerekli olmayan depolama için ödeme sonlandırmak için diğer çözümlerin maliyetlidir. Bunlar hello tür veya gereksinim duyduğunuz depolama miktarını önerme çünkü diğer çözümleri genellikle verimsiz ya da yönetim görevleri çok fazla zaman gerektirir. Buna karşılık Azure Backup şu önemli avantajlara sahiptir:

**Otomatik Depolama Yönetimi** - karma ortamlar, heterojen depolama - bazı şirket içi genellikle gerektirir ve bazı durumlarda hello bulut. Azure Backup çözümünde, şirket içi depolama cihazlarının kullanımıyla ilişkili maliyetler yoktur. Azure Backup, yedekleme alanını otomatik olarak ayırıp yönetir ve "kullandıkça öde" modelini kullanır. Ödeme olarak,-kullanımlı yalnızca tükettiğiniz hello depolama alanı için ödeme anlamına gelir. Daha fazla bilgi için bkz: Merhaba [Azure makale fiyatlandırma](https://azure.microsoft.com/pricing/details/backup).

**Sınırsız ölçekleme** - Azure yedekleme güç temel hello kullanır ve hello Azure sınırsız ölçeğini toodeliver yüksek kullanılabilirlik - herhangi bir bakım veya izleme ek yükü ile bulut. Olaylar hakkında uyarılar tooprovide bilgi ayarlayabilirsiniz ancak hello bulutta verileriniz için yüksek kullanılabilirlik hakkında tooworry gerekmez.

**Birden çok depolama seçeneği** - Yüksek kullanılabilirliğin bir özelliği de depolama çoğaltmadır. Azure Backup iki tür çoğaltma sunar: [Yerel olarak yedekli depolama](../storage/common/storage-redundancy.md#locally-redundant-storage) ve [coğrafi olarak yedekli depolama](../storage/common/storage-redundancy.md#geo-redundant-storage). Gereksinimleri temelinde hello yedekleme depolama seçeneği seçin:

* Yerel olarak yedekli depolama (LRS) çoğaltır, verilerinizi hello eşleştirilmiş bir veri merkezinde üç kez (verilerinizin üç kopyasını oluşturur) aynı bölgede. LRS, verilerinizi yerel donanım hatalarına karşı korumak için düşük maliyetli bir seçenektir.

* Coğrafi olarak yedekli depolama (GRS), veri tooa ikincil bölge (Merhaba birincil hello kaynak verilerin konumunu çıktığınızda mil yüzlerce) çoğaltır. GRS’nin maliyeti LRS’den yüksektir ancak bölgesel kesintiler olsa bile daha yüksek veri dayanıklılık düzeyi sunar.

**Sınırsız veri aktarımı** - Azure yedekleme gelen hello miktarını sınırlamaz veya giden veri aktarımı. Azure yedekleme de aktarılır hello veri için ücret değil. Ancak, hello Azure içeri/dışarı aktarma hizmeti tooimport büyük miktarlarda verinin kullanırsanız, gelen verilerle ilişkili bir maliyeti yoktur. Bu maliyet hakkında daha fazla bilgi için bkz. [Azure Backup’ta çevrimdışı yedekleme iş akışı](backup-azure-backup-import-export.md). Giden veri kurtarma Hizmetleri Kasası'nı geri yükleme işlemi sırasında aktarılan toodata başvuruyor.

**Veri şifreleme** -güvenli şekilde iletilmesini ve verilerinizin hello genel bulut depolama veri şifreleme sağlar. Merhaba şifreleme parolası yerel olarak depolamak ve onu hiçbir zaman aktarılan veya Azure'da depolanan. Gerekli toorestore herhangi ise hello verilerin yalnızca, şifreleme parolası yüklüyse veya anahtar.

**Uygulama tutarlı yedekleme** -bir dosya sunucusu, sanal makine ya da SQL veritabanı yedekleme, bir kurtarma noktası tüm olduğunu tooknow ihtiyacınız olup olmadığını gerekli veri toorestore hello yedek kopya. Azure Backup ek düzeltmeler gerekli toorestore hello veri olmayan güvence altına uygulamayla tutarlı yedeklemeler sağlar. Uygulama tutarlı verileri geri yükleme tooquickly dönüş tooa çalışır durumda izin verme hello geri yükleme zamanı azaltır.

**Uzun vadeli bekletme** -disk tootape ve taşıma hello bant tooan yerde sakladığınızdan yedek kopyaları geçiş yerine Azure kısa vadeli ve uzun vadeli bekletme için kullanabilirsiniz. Azure hello süreyi veriler bir yedekleme veya kurtarma Hizmetleri kasasına kalır sınırlamak değil. Verileri bir kasada dilediğiniz süre boyunca bekletebilirsiniz. Azure Backup, korunan her örnek için 9999 kurtarma noktası sınırına sahiptir. Merhaba bkz [yedekleme ve bekletme](backup-introduction-to-azure-backup.md#backup-and-retention) bu sınırı yedekleme ihtiyaçlarınız nasıl etkileyebilir bir açıklama için bu makalenin bölümünde.  

## <a name="which-azure-backup-components-should-i-use"></a>Hangi Azure Backup bileşenlerini kullanmalıyım?
Emin değilseniz, gereksinimleriniz için hangi Azure yedekleme bileşeni çalışır, hello aşağıdaki tablonun her bileşeni ile koruyabilmeniz için hakkında bilgi için bkz. Hello Azure portal hello portalda, bileşen toodownload hello ve dağıtma şeklinizi seçme aracılığıyla tooguide yerleşik bir sihirbaz sağlar. hello kurtarma Hizmetleri kasası oluşturma bir parçası olan hello Sihirbazı yedekleme hedefi seçilerek ve hello veri veya uygulama tooprotect hello adımlarında yol gösterir.

| Bileşen | Avantajlar | Sınırlar | Neler korunuyor? | Yedekler nerede saklanıyor? |
| --- | --- | --- | --- | --- |
| Azure Backup (MARS) aracısı |<li>Fiziksel veya sanal Windows işletim sistemi üzerindeki dosya ve klasörleri yedekler (VM’ler şirket içinde veya Azure’da olabilir)<li>Ayrı bir yedekleme sunucusu gerekli değildir. |<li>Günde 3 kez yedekleme <li>Uygulamayı algılamaz; yalnızca dosya, klasör ve birim düzeyinde geri yükleme, <li>  Linux desteği yok. |<li>Dosyalar, <li>Klasörler |Kurtarma Hizmetleri kasası |
| System Center DPM |<li>Uygulama kullanan anlık görüntüler (VSS)<li>Tam esneklik için ne zaman tootake yedeklemeler<li>Kurtarma ayrıntı düzeyi (tümü)<li>Kurtarma Hizmetleri kasasını kullanabilir<li>Hyper-V ve VMware VM’lerinde Linux desteği <li>DPM 2012 R2 kullanarak VMware WM’lerini yedekleme ve geri yükleme |Oracle iş yükü yedeklenemiyor.|<li>Dosyalar, <li>Klasörler,<li> Birimler, <li>VM’ler,<li> Uygulamalar,<li> İş yükleri |<li>Kurtarma Hizmetleri kasası,<li> Yerel olarak bağlı disk,<li>  Bant (yalnızca şirket içi) |
| Azure Backup Sunucusu |<li>Uygulama kullanan anlık görüntüler (VSS)<li>Tam esneklik için ne zaman tootake yedeklemeler<li>Kurtarma ayrıntı düzeyi (tümü)<li>Kurtarma Hizmetleri kasasını kullanabilir<li>Hyper-V ve VMware VM’lerinde Linux desteği<li>VMware VM’lerini yedekleme ve geri yükleme <li>System Center lisansı gerektirmez |<li>Oracle iş yükü yedeklenemiyor.<li>Her zaman canlı Azure aboneliği gerektirir<li>Bant yedekleme desteği yoktur |<li>Dosyalar, <li>Klasörler,<li> Birimler, <li>VM’ler,<li> Uygulamalar,<li> İş yükleri |<li>Kurtarma Hizmetleri kasası,<li> Yerel olarak bağlı disk |
| Azure IaaS VM Backup |<li>Windows/Linux için yerel yedeklemeler<li>Belirli bir aracı yüklemesi gerekmez<li>Yedekleme altyapısı gerekmeden yapı düzeyinde yedekleme |<li>VM’leri günde bir kez yedekleme <li>VM’leri yalnızca disk düzeyinde geri yükleme<li>Şirket içi yedekleme gerçekleştirilemez |<li>VM’ler, <li>Tüm diskler (PowerShell kullanarak) |<p>Kurtarma Hizmetleri kasası</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Merhaba dağıtım senaryoları her bileşen için nelerdir?
| Bileşen | Azure'da dağıtılabilir mi? | Şirket içinde dağıtılabilir mi? | Hedef depolama desteklenir |
| --- | --- | --- | --- |
| Azure Backup (MARS) aracısı |<p>**Evet**</p> <p>Hello Azure Yedekleme aracısı, Azure'da çalışan tüm Windows Server VM üzerinde dağıtılabilir.</p> |<p>**Evet**</p> <p>Merhaba Yedekleme aracısı, herhangi bir Windows Server VM veya fiziksel makinesi üzerinde dağıtılabilir.</p> |<p>Kurtarma Hizmetleri kasası</p> |
| System Center DPM |<p>**Evet**</p><p>Daha fazla bilgi edinmek [nasıl System Center DPM kullanarak tooprotect azure'da iş yüklerini](backup-azure-dpm-introduction.md).</p> |<p>**Evet**</p> <p>Daha fazla bilgi edinmek [nasıl tooprotect iş yüklerini ve Vm'leri, veri merkezinizdeki](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Yerel olarak bağlı disk,</p> <p>Kurtarma Hizmetleri kasası,</p> <p>bant (yalnızca şirket içi)</p> |
| Azure Backup Sunucusu |<p>**Evet**</p><p>Daha fazla bilgi edinmek [nasıl Azure yedekleme sunucusu kullanarak tooprotect azure'da iş yüklerini](backup-azure-microsoft-azure-backup.md).</p> |<p>**Evet**</p> <p>Daha fazla bilgi edinmek [nasıl Azure yedekleme sunucusu kullanarak tooprotect azure'da iş yüklerini](backup-azure-microsoft-azure-backup.md).</p> |<p>Yerel olarak bağlı disk,</p> <p>Kurtarma Hizmetleri kasası</p> |
| Azure IaaS VM Backup |<p>**Evet**</p><p>Azure yapısının parçası</p><p>[Hizmet olarak Azure altyapısı (IaaS) sanal makinelerinin yedeklemesine](backup-azure-vms-introduction.md) yöneliktir.</p> |<p>**Hayır**</p> <p>System Center DPM tooback sanal makineleri yedeklemek, veri merkezinizde kullanın.</p> |<p>Kurtarma Hizmetleri kasası</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Hangi uygulamalar ve iş yükleri yedeklenebilir?
Aşağıdaki tablonun hello hello veri ve Azure Yedekleme'yi kullanarak korumalı iş yükü bir matris sağlar. Bu çözüm için bağlantılar toohello dağıtım belgelerine Hello Azure Backup çözümü sütun vardır. Her bir Azure Backup bileşeni Klasik (Service Manager dağıtımı) veya Resource Manager dağıtım modeli ortamında dağıtılabilir.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Veri veya İş Yükü | Kaynak ortamı | Azure Backup çözümü |
| --- | --- | --- |
| Dosyalar ve klasörler |Windows Server |<p>[Azure Backup aracısı](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Dosyalar ve klasörler |Windows bilgisayar |<p>[Azure Backup aracısı](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Hyper-V sanal makine (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Hyper-V sanal makine (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup Aracısı)</p> <p>[Azure yedekleme sunucusu](backup-azure-microsoft-azure-backup.md) (hello Azure Backup aracısını içerir)</p> |
| Azure IaaS VM'ler (Windows) |Azure’da çalışan |[Azure Backup (VM uzantısı)](backup-azure-vms-introduction.md) |
| Azure IaaS VM'ler (Linux) |Azure’da çalışan |[Azure Backup (VM uzantısı)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Linux desteği
Merhaba aşağıdaki tabloda Linux için desteğe sahip hello Azure Backup bileşenleri gösterir.  

| Bileşen | Linux (Azure destekli) Desteği |
| --- | --- |
| Azure Backup (MARS) aracısı |Hayır (Yalnızca Windows tabanlı aracı) |
| System Center DPM |<li> Hyper-V ve VMWare üzerinde Linux Konuk VM’lerinin dosyayla tutarlı yedeklemesi<br/> <li> Hyper-V ve VMWare Linux Konuk VM’lerinin VM geri yüklemesi </br> </br>  *Tutarlı dosya yedekleme Azure VM için kullanılamaz* <br/> |
| Azure Backup Sunucusu |<li>Hyper-V ve VMWare üzerinde Linux Konuk VM’lerinin dosyayla tutarlı yedeklemesi<br/> <li> Hyper-V ve VMWare Linux Konuk VM’lerinin VM geri yüklemesi </br></br> *Tutarlı dosya yedekleme Azure VM için kullanılamaz*  |
| Azure IaaS VM Backup |[betik öncesi ve betik sonrası çerçeve](backup-azure-linux-app-consistent.md) kullanılarak uygulamada tutarlı yedekleme<br/> [Ayrıntılı dosya kurtarma](backup-azure-restore-files-from-vm.md)<br/> [Tüm VM disklerini geri yükleme](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [VM geri yükleme](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Azure Backup ile Premium Depolama VM’leri
Azure Backup, Premium Depolama VM'leri koruma altına alır. Azure Premium Storage olan katı hal sürücüsü (SSD)-tasarlanmış depolama toosupport g/Ç kullanımı yoğun iş yükleri temel. Premium Depolama, sanal makine (VM) iş yükleri için idealdir. Premium depolama hakkında daha fazla bilgi için hello makalesine bakın [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Premium Storage VM'lerini yedekleme
Premium Storage Vm'lerini hello Backup hizmeti yedekleme geçici bir hazırlama konumu oluşturur, ancak "AzureBackup-" Merhaba Premium depolama hesabı adı. Hazırlama konumuna hello Hello boyutuna eşit toohello hello kurtarma noktası anlık görüntüsünü boyutudur. Yeterli boş alanı tooaccommodate hello geçici hazırlama konumu Hello Premium depolama hesabı bulunduğundan emin olun. Daha fazla bilgi için bkz: hello makale [premium Depolama Sınırlamaları](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Hazırlama konumuna hello Hello yedekleme işi tamamlandıktan sonra silinir. Merhaba hazırlama konumuna hello için kullanılan depolama alanının fiyatı tüm ile tutarlıdır [Premium depolama fiyatlandırması](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Değiştirmeyin veya hazırlama konumuna hello düzenleyin.
>
>

### <a name="restore-premium-storage-vms"></a>Premium Storage VM'lerini geri yükleme
Premium Storage Vm'lerini geri yüklenen tooeither Premium depolama veya toonormal depolama olabilir. Bir Premium Storage VM'si kurtarma noktası geri tooPremium depolama geri hello tipik geri yükleme işlemidir. Ancak, düşük maliyetli toorestore Premium Storage VM'si kurtarma noktası toostandard depolama olabilir. Bu tür bir geri yükleme hello VM dosyalardan bir kısmı ihtiyacınız varsa kullanılabilir.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Yönetilen disk sanal makinelerini Azure Backup ile kullanma
Azure Backup, yönetilen disk sanal makinelerini korur. Yönetilen diskler, sanal makinelerin depolama hesaplarını yönetme sorumluluğunuzu ortadan kaldırır ve VM sağlama işlemini önemli ölçüde kolaylaştırır.

### <a name="back-up-managed-disk-vms"></a>Yönetilen disk sanal makinelerini yedekleme
Yönetilen diskler üzerindeki VM'lerin yedeklenmesi, Resource Manager VM'lerin yedeklenmesinden farklı değildir. Hello Azure portal, hello yedekleme işinden doğrudan hello sanal makine görünümünü yapılandırma ya da Görünüm hello kurtarma Hizmetleri kasası. Yönetilen diskler üzerindeki VM'ler, yönetilen diskler üzerinde oluşturulmuş RestorePoint koleksiyonları ile yedeklenebilir. Azure Backup ayrıca Azure Disk şifrelemesi (ADE) kullanılarak şifrelenmiş yönetilen disk VM'lerinin yedeklenmesini destekler.

### <a name="restore-managed-disk-vms"></a>Yönetilen disk sanal makinelerini geri yükleme
Azure yedekleme toorestore yönetilen disklerle tam bir VM izin verir veya geri yükleme tarafından yönetilen diskleri tooa depolama hesabı. Azure yönetilen hello diskleri hello geri yükleme işlemi sırasında yönetir. Sizin (Merhaba müşteri) hello geri yükleme işleminin bir parçası oluşturulan hello storage hesabı yönetme. Geri yükleme şifrelenmiş VM'ler yönetildiğinde hello VM'in anahtarları ve gizli anahtarları hello anahtar kasası önceki toostarting hello geri yükleme işleminde var olmalıdır.

## <a name="what-are-hello-features-of-each-backup-component"></a>Her bir yedekleme bileşen hello özellikleri nelerdir?
Aşağıdaki bölümlerde hello hello kullanılabilirlik veya her Azure Backup bileşeninde çeşitli özelliklerine yönelik destek özetlemek tablolar sağlar. Her tablo için ek destek veya Ayrıntılar aşağıdaki hello bilgi bakın.

### <a name="storage"></a>Depolama
| Özellik | Azure Backup aracısı | System Center DPM | Azure Backup Sunucusu | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| Kurtarma Hizmetleri kasası |![Evet][green] |![Evet][green] |![Evet][green] |![Evet][green] |
| Disk depolama | |![Evet][green] |![Evet][green] | |
| Bant depolama | |![Evet][green] | | |
| Sıkıştırma <br/>(Kurtarma hizmetleri kasasında) |![Evet][green] |![Evet][green] |![Evet][green] | |
| Artımlı yedekleme |![Evet][green] |![Evet][green] |![Evet][green] |![Evet][green] |
| Disk için yinelenenleri kaldırma | |![Kısmi][yellow] |![Kısmi][yellow] | | |

![tablo anahtarı](./media/backup-introduction-to-azure-backup/table-key.png)

Merhaba kurtarma Hizmetleri kasası tüm bileşenler genelinde hello tercih edilen depolama hedefidir. System Center DPM ve Azure yedekleme sunucusu da yerel disk kopyası hello seçeneği toohave sağlar. Ancak, yalnızca System Center DPM hello seçeneği toowrite veri tooa bant depolama aygıtı sağlar.

#### <a name="compression"></a>Sıkıştırma
Yedeklemeler sıkıştırılır tooreduce hello depolama alanı gerekli. sıkıştırma kullanmayan tek bileşen hello hello VM uzantısıdır. içindeki tüm yedekleme verileri depolama hesabı toohello kurtarma Hizmetleri kasası hello VM uzantısı kopyaları aynı bölgede hello. Sıkıştırma hello veri aktarırken kullanılmaz. Merhaba veri sıkıştırma olmadan biraz aktarırken kullanılan hello depolama Şişir. Ancak, daha hızlı geri yükleme için sıkıştırma sağlar olmadan hello verilerin depolanması, bu kurtarma noktası gerekir.


#### <a name="disk-deduplication"></a>Disk İçin Yinelenenleri Kaldırma
[Hyper-V sanal makinesinde](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx) System Center DPM veya Azure Backup Sunucusu dağıttığınızda disk için yinelenenleri kaldırma özelliğinden faydalanabilirsiniz. Windows Server yinelenen verileri kaldırma (Merhaba konak düzeyinde) sanal sabit disklerde ekli toohello sanal makine yedekleme depolama alanı olarak olan (VHD) gerçekleştirir.

> [!NOTE]
> Yinelenenleri kaldırma, Azure Backup bileşenlerinden herhangi biri için kullanılamaz. System Center DPM ve Backup sunucusu Azure'da dağıtıldığında, hello depolama diskleri VM yinelenenler kaldırılamaz toohello bağlı.
>
>

### <a name="incremental-backup-explained"></a>Artımlı yedekleme açıklaması
Her Azure yedekleme bileşeni hello hedef depolama (disk, bant, Kurtarma Hizmetleri kasası) bağımsız olarak artımlı yedeklemeyi destekler. Artımlı yedekleme yedeklemelerin depolama ve zaman açısından verimli, yalnızca hello son yedeklemeden sonra yapılan değişiklikleri aktararak olmasını sağlar.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Tam Yedekleme, Değişiklik Yedeği ve Artımlı Yedekleme karşılaştırması

Her yedekleme yönteminin depolama alanı tüketimi, kurtarma süresi hedefi (RTO) ve ağ tüketimi diğerinden farklıdır. tookeep hello yedekleme toplam sahip olma maliyetini (TCO), gereksinim duyduğunuz toounderstand nasıl toochoose hello en iyi yedekleme çözümü. Görüntü aşağıdaki hello tam yedekleme, farklı yedekleme ve artımlı yedekleme karşılaştırır. Hello görüntüde A 10 depolama oluşan veri kaynağı, aylık yedeklenen A1-A10 engeller. Blokları A2, A3, A4 ve A9 hello ilk ay değiştirin ve hello A5 değişiklikler bir sonraki ay engelleyin.

![yedekleme yöntemlerinin karşılaştırmasını gösteren görüntü](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

İle **tam yedekleme**, her yedek kopya hello tüm veri kaynağı içeriyor. Tam yedeklemede her yedek kopyası aktarımında çok fazla ağ bant genişliği ve depolama alanı kullanılır.

**Değişiklik yedeklemesi** hello daha az miktarda ağ ve depolama tüketimini içinde sonuçları hello ilk tam yedekleme, bu yana değişen blokları yalnızca depolar. Değişiklik yedekleri, değişmeyen verilerin gereksiz kopyalarını tutmaz. Ancak, sonraki yedeklemeler arasında değişmeden hello veri blokları transfer ve depolanan çünkü yedekleri verimsiz değildir. Hello ikinci ay değişen blokları A2, A3, A4 ve A9 yedeklenir. Hello üçüncü ay, bu aynı blokları yeniden değiştirilen blok A5 birlikte yedeklenir. Değiştirilen blokları hello hello sonraki tam yedekleme olur kadar yedeklenen toobe devam edin.

**Artımlı yedekleme** hello önceki yedeklemeden sonra değiştirilen verileri yalnızca hello bloklarını depolayarak yüksek depolama ve ağ verimliliği sağlar. Artımlı yedekleme ile tootake düzenli tam yedeklemeler gerek yoktur. Hello örnekte hello tam yedekleme için hello ilk ay alınır sonra değişen blokları A2, A3, A4 ve A9 olarak işaretlenmiş değişti ve ikinci ay Merhaba aktarılan. Hello üç ayda yalnızca A5 olarak işaretlenmiş ve aktarılan blok değiştirildi. Daha az verinin taşınması depolama ve ağ kaynaklarından tasarruf edilmesini ve TCO'nun düşürülmesini sağlar.   

### <a name="security"></a>Güvenlik
| Özellik | Azure Backup aracısı | System Center DPM | Azure Backup Sunucusu | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| Ağ güvenliği<br/> (tooAzure) |![Evet][green] |![Evet][green] |![Evet][green] |![Kısmi][yellow] |
| Veri güvenliği<br/> (Azure’da) |![Evet][green] |![Evet][green] |![Evet][green] |![Kısmi][yellow] |

![tablo anahtarı](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Ağ güvenliği
Kurtarma Hizmetleri kasası, sunucuları toohello giden tüm yedekleme trafiği, Gelişmiş Şifreleme Standardı 256 kullanılarak şifrelenir. Merhaba yedekleme verileri güvenli bir HTTPS bağlantısı üzerinden gönderilir. Merhaba yedekleme verileri de hello kurtarma Hizmetleri kasası şifreli biçimde depolanır. Yalnızca, hello Azure müşteri hello parola toounlock bu veri içeriyor. Microsoft hello herhangi bir noktada yedekleme verilerinin şifresini çözemez.

> [!WARNING]
> Yalnızca hello kurtarma Hizmetleri kasası oluşturduktan sonra erişim toohello şifreleme anahtarı gerekir. Microsoft hiçbir zaman şifreleme anahtarınızın bir kopyasını tutar ve erişim toohello anahtarı yok. Merhaba anahtarın kaybedilmesi durumunda Microsoft hello yedekleme verilerini kurtaramaz.
>
>

#### <a name="data-security"></a>Veri güvenliği
Azure VM'lerin yedeklenmesi şifreleme ayarlanması gerekir *içinde* hello sanal makine. Windows sanal makinelerde BitLocker'ı ve Linux sanal makinelerde **dm-crypt** özelliğini kullanın. Azure Backup, bu yol üzerinden gelen yedekleme verilerini otomatik olarak şifrelemez.

### <a name="network"></a>Ağ
| Özellik | Azure Backup aracısı | System Center DPM | Azure Backup Sunucusu | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| Ağ sıkıştırma <br/>(çok**yedekleme sunucusu**) | |![Evet][green] |![Evet][green] | |
| Ağ sıkıştırma <br/>(çok**kurtarma Hizmetleri kasası**) |![Evet][green] |![Evet][green] |![Evet][green] | |
| Ağ protokolü <br/>(çok**yedekleme sunucusu**) | |TCP |TCP | |
| Ağ protokolü <br/>(çok**kurtarma Hizmetleri kasası**) |HTTPS |HTTPS |HTTPS |HTTPS |

![tablo anahtarı](./media/backup-introduction-to-azure-backup/table-key-2.png)

Böylece gerekli toocompress hello VM uzantısı ('hello Iaas VM) bu trafiği hello depolama ağ üzerinden doğrudan hello Azure depolama hesabı ' hello verileri okur.

Bir System Center DPM sunucusu veya Azure yedekleme sunucusu ikincil bir yedekleme sunucusu olarak kullanıyorsanız, hello birincil sunucu toohello yedekleme sunucusundan giderek hello verileri sıkıştırın. TooDPM veya Azure yedekleme sunucusu yedeklemeden önce verileri sıkıştırma, bant genişliğinden tasarruf eder.

#### <a name="network-throttling"></a>Ağ Kapasitesi Azaltma
Hello Azure Yedekleme aracısı ağ azaltma, veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını toocontrol sağlayan sunar. İş saatleri sırasında verileri tooback gerekiyorsa ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz azaltma yararlı olabilir. Verileri azaltma aktarımı yukarıya tooback uygular ve geri yükleme etkinlikleri.

## <a name="backup-and-retention"></a>Yedekleme ve bekletme

Azure Backup’ta, *korumalı örnek* başına 9999 kurtarma noktası (yedekleme kopyası veya anlık görüntü olarak da bilinir) sınırı vardır. Bir korumalı bir bilgisayar, sunucu (fiziksel veya sanal) veya yapılandırılmış iş yükü tooback veri tooAzure yukarı örneğidir. Daha fazla bilgi için hello bölümüne bakın [korumalı bir örneği nedir](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Verilerin yedek kopyası kaydedildiğinde örnek, korumalı hale gelir. veri yedek kopyasını Hello hello korumadır. Merhaba kaynak veriler kesildi veya bozuk hale geldi, hello yedek kopya hello kaynak verileri geri yüklenemedi. Merhaba aşağıdaki tabloda her bileşen için en fazla yedekleme sıklığı hello gösterilmektedir. Yedekleme İlkesi yapılandırmanızı hello kurtarma noktaları tüketen nasıl hızlı bir şekilde belirler. Örneğin, her gün bir kurtarma noktası oluşturursanız; kurtarma noktalarınızı 27 yıl boyunca bitmeden tutabilirsiniz. Aylık bir kurtarma noktası izlerseniz, çalıştırmadan önce 833 yıl için kurtarma noktası tutabilirsiniz. Merhaba Backup hizmeti, bir kurtarma noktasında bir sona erme süresi sınırı ayarlı değil.

|  | Azure Backup aracısı | System Center DPM | Azure Backup Sunucusu | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| Yedekleme sıklığı<br/> (tooRecovery Hizmetleri kasası) |Günde üç yedekleme |Günde iki yedekleme |Günde iki yedekleme |Günde bir yedekleme |
| Yedekleme sıklığı<br/> (toodisk) |Uygulanamaz |<li>SQL Server için 15 dakikada bir <li>Diğer iş yükleri için saatte bir |<li>SQL Server için 15 dakikada bir <li>Diğer iş yükleri için saatte bir</p> |Uygulanamaz |
| Bekletme seçenekleri |Günlük, haftalık, aylık, yıllık |Günlük, haftalık, aylık, yıllık |Günlük, haftalık, aylık, yıllık |Günlük, haftalık, aylık, yıllık |
| Korumalı örnek başına en fazla kurtarma noktası |9999|9999|9999|9999|
| En uzun bekletme süresi |Yedekleme sıklığına bağlıdır |Yedekleme sıklığına bağlıdır |Yedekleme sıklığına bağlıdır |Yedekleme sıklığına bağlıdır |
| Yerel diskteki kurtarma noktaları |Uygulanamaz |<li>Dosya Sunucuları için 64<li>Uygulama Sunucuları için 448 |<li>Dosya Sunucuları için 64<li>Uygulama Sunucuları için 448 |Uygulanamaz |
| Banttaki kurtarma noktaları |Uygulanamaz |Sınırsız |Uygulanamaz |Uygulanamaz |

## <a name="what-is-a-protected-instance"></a>Korumalı örnek nedir?
Bir korumalı bir genel başvuru tooa Windows bilgisayarı, sunucu (fiziksel veya sanal) veya yapılandırılmış tooback tooAzure yukarı bırakıldı SQL veritabanı örneğidir. Merhaba bilgisayar, sunucu veya veritabanı için bir yedekleme ilkesi yapılandırın ve hello veri yedek bir kopyasını oluşturun sonra örneği korunur. Sonraki kopyaları hello yedekleme (hangi kurtarma noktaları olarak adlandırılır) bu korumalı örnek için kullanılan depolama hello miktarını artırın. Korumalı bir örnek için too9999 kurtarma noktası oluşturabilirsiniz. Depolama biriminden bir kurtarma noktası silerseniz, hello 9999 kurtarma noktası toplam karşı sayılmaz.
Bazı ortak korumalı örnekler sanal makineler, uygulama sunucuları, veritabanları ve kişisel hello Windows işletim sistemi çalıştıran bilgisayarları gösterilebilir. Örneğin:

* Merhaba Hyper-V ya da Azure Iaas hiper yönetici doku çalışan bir sanal makine. Merhaba hello sanal makine için konuk işletim sistemleri, Windows Server veya Linux olabilir.
* Bir uygulama sunucusu: hello uygulama sunucusu, bir fiziksel veya yedeklenen toobe gereken veri ile Windows Server ve iş yüklerini çalıştıran sanal makine olabilir. Ortak iş yükleri, Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server ve Windows Server'da dosya sunucusu rolü hello ' dir. tooback bu iş yüklerini System Center Data Protection Manager (DPM) veya Azure yedekleme sunucusu gerekir.
* Kişisel bilgisayar, iş istasyonu veya dizüstü hello Windows işletim sistemi çalıştırıyor.


## <a name="what-is-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası nedir?
Kurtarma Hizmetleri kasası Azure çevrimiçi depolama varlık toohold veri yedek kopyaları, Kurtarma noktaları ve yedekleme ilkeleri gibi kullanılır. Kurtarma Hizmetleri kasaları toohold yedekleme verilerini Azure Hizmetleri ve şirket içi sunucular ve iş istasyonları için kullanabilirsiniz. Kurtarma Hizmetleri kasaları kolay tooorganize sunun yönetim yükünü en aza çalışırken, yedekleme verilerinizi. Bir abonelik dahilinde dilediğiniz sayıda Kurtarma Hizmetleri kasası oluşturabilirsiniz.

Azure hizmet yöneticiyi temel alan, yedekleme kasaları hello ilk sürüm hello kasasının yoktu. Hello Azure Resource Manager modeli özellikleri eklemek, Kurtarma Hizmetleri kasaları hello ikinci hello kasa sürümü var. Merhaba bkz [kurtarma Hizmetleri kasası genel bakış makalesi](backup-azure-recovery-services-vault-overview.md) hello özellik farklılıkları tam bir açıklaması. Yedekleme kasaları artık kullanım hello portal toocreate oluşturabilirsiniz, ancak yedekleme kasaları hâlâ destekleniyor.

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> **15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır. <br/> **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Azure Backup'ın Azure Site Recovery'den farkı nedir?
Azure Backup ve Azure Site Recovery, veri yedekleme ve geri yükleme özelliklerine sahip olmaları açısından aynıdır. Ancak, bu hizmetler işletmenizde iş sürekliliği sağlama ve olağanüstü durum kurtarma konularında farklı amaçlara hizmet eder. Azure Backup tooprotect ve daha ayrıntılı bir düzeyde veri geri yükleme. Örneğin, bir dizüstü bilgisayar sunu bozulmasından, Azure Backup toorestore hello sunu kullanın. Başka bir veri merkezi üzerinden tooreplicate hello yapılandırma ve veriler bir VM'de istediyseniz, Azure Site Recovery kullanın.

Azure yedekleme verileri şirket içi korur ve hello bulutta. Azure Site Recovery, sanal makine ve fiziksel sunucu çoğaltma, yük devretme ve yeniden çalışma işlemlerini düzenler. Olağanüstü durum kurtarma çözümünüzün verilerinizin güvenli ve kurtarılabilir (Yedekleme) tookeep gerektiğinden her iki hizmet önemli *ve* kesintiler meydana geldiğinde, iş yüklerini kullanılabilir (Site Recovery) tutun.

kavramlar aşağıdaki hello yedekleme ve olağanüstü durum kurtarma önemli kararları vermenize yardımcı olabilir.

| Kavram | Ayrıntılar | Backup | Olağanüstü durum kurtarma (DR) |
| --- | --- | --- | --- |
| Kurtarma noktası hedefi (RPO) |Merhaba kurtarma bitti toobe gerekiyorsa kabul edilebilir veri kaybı miktarı. |Backup çözümleri, kabul edilebilir RPO değerlerinde büyük bir değişkenliğe sahiptir. Sanal makine yedeklemeleri genellikle bir günlük bir RPO'ya sahipken, veritabanı yedeklemelerinin RPO değerleri 15 dakika kadar düşük olabilir. |Olağanüstü durum kurtarma çözümleri düşük RPO'lara sahiptir. Merhaba DR kopyalama arkasında birkaç saniye veya birkaç dakika olabilir. |
| Kurtarma süresi hedefi (RTO) |Merhaba kurtarma veya geri yükleme toocomplete geçen süre miktarı. |Merhaba nedeniyle daha büyük RPO, hello bir yedekleme çözümüne tooprocess gereken veri miktarı genellikle çok daha yüksektir toolonger Rto'lara yol açar. Örneğin, bunu toorestore veri tootransport hello bant yerde sakladığınızdan hello süresini bağlı olarak, bantlardan gün sürebilir. |Daha hello kaynağı ile eşitlenmiş olduklarından olağanüstü durum kurtarma çözümleri daha küçük Rto'lara sahiptir. Daha az değişiklikleri işlenen toobe gerekir. |
| Bekletme |Ne kadar süreyle verilerinin depolanan toobe gerekir. |İşletimsel kurtarma gerektiren senaryolar (veri bozulması, yanlışlıkla dosya silme, işletim sistemi arızası) için, yedekleme verileri genellikle 30 gün veya daha kısa süreyle elde tutulur.<br>Uyumluluk açısından, veri toobe için aylarca ve hatta yıllarca depolanması gerekebilir. Bu gibi durumlarda arşivleme için yedekleme verileri ideal niteliktedir. |Olağanüstü durum kurtarma, genellikle birkaç saat veya tooa gün sürer işletimsel kurtarma verilerine gerekir. DR çözümlerinde kullanılan hello ayrıntılı veri yakalama işlemi nedeniyle, uzun vadeli bekletme için DR verilerinin kullanılması önerilmez. |

## <a name="next-steps"></a>Sonraki adımlar
Azure'da hello Windows Server verilerini koruma veya bir sanal makine (VM) koruma için öğreticileri ayrıntılı, adım adım yönergeler için aşağıdaki birini kullanın:

* [Dosya ve Klasörleri yedekleme](backup-try-azure-backup-in-10-mins.md)
* [Azure Sanal Makinelerini yedekleme](backup-azure-vms-first-look-arm.md)

Diğer iş yüklerini koruma hakkında ayrıntılı bilgi için şu makaleleri inceleyin:

* [Windows Server verilerinizi yedekleme](backup-configure-vault.md)
* [Uygulama iş yüklerini yedekleme](backup-azure-microsoft-azure-backup.md)
* [Azure IaaS VM'lerini yedekleme](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png

---
title: "aaaHigh performans Premium depolama ve Azure VM'ler için diskleri yönetilen | Microsoft Docs"
description: "Azure VM'ler için yüksek performanslı Premium depolama ve yönetilen diskler hakkında bilgi edinin. Azure DS serisi, DSv2 serisi, GS serisi ve Fs-serisi VM'ler Premium depolama destekler."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Yüksek performanslı Premium depolama ve VM'ler için yönetilen diskleri
Azure Premium Storage giriş/çıkış (g/ç) ile sanal makineleri (VM'ler) için yüksek performanslı, düşük gecikmeli disk desteği sunar-yoğun iş yükleri. Premium depolama kullanan VM diskleri verileri katı hal sürücüleri (SSD) depolar. tootake avantajı hello hızı ve performansı premium depolama disklerinin var olan VM diskleri tooPremium depolama geçirebilirsiniz.

Azure'da, birkaç premium depolama diskleri tooa VM ekleyebilirsiniz. Birden çok disk kullanarak too256 TB uygulamalarınızı VM başına depolama sağlar. Premium depolama ile uygulamalarınızı 80.000 g/ç işlemi (IOPS) saniyede VM ve too2, 000 megabayt (MB/sn) saniyede VM oluşturan bir disk verimini elde edebilirsiniz. Okuma işlemleri çok düşük gecikme sağlar.

Premium Storage ile Azure tootruly yükseltme shift zorlu kurumsal uygulamalar Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite ve SharePoint grupları toohello bulut gibi hello olanak sağlar. SQL Server, Oracle, MongoDB, MySQL ve Redis, tutarlı yüksek performans ve düşük gecikme gerektiren gibi uygulamalarda, veritabanı performansı yoğun iş yükleri çalıştırabilirsiniz.

> [!NOTE]
> Merhaba en iyi performans için uygulamanız için yüksek IOPS tooPremium depolama gerektiren herhangi bir VM disk geçirmek öneririz. Diskinizin yüksek IOPS gerektirmiyorsa, standart Azure depolama alanında tutarak sınırı maliyetleri yardımcı olabilir. Standart depolama biriminde, sabit disk sürücülerinin (HDD'ler) yerine ssd'lerde VM disk veriler depolanır.
> 

Azure VM'ler için toocreate premium depolama diskleri iki yol sunar:

* **Yönetilmeyen diskler**

    Merhaba özgün yönetilmeyen toouse diskleri yöntemidir. Yönetilmeyen bir disk tooyour VM diskleri karşılık toostore hello sanal sabit disk (VHD) dosyaları kullanan hello depolama hesaplarını yönetin. VHD dosyaları, Azure storage hesapları sayfa bloblarını olarak depolanır. 

* **Yönetilen diskleri**

    Seçtiğinizde [Azure yönetilen diskleri](storage-managed-disks-overview.md), Azure VM diskleriniz için kullandığınız hello depolama hesapları yönetir. Merhaba disk türünü (Premium veya standart) ve hello ihtiyacınız hello diskin boyutunu belirtin. Azure oluşturur ve hello disk tarafından yönetilir. Depolama hesapları için ölçeklenebilirlik sınırları içinde kalmasını birden çok depolama hesapları tooensure hello diskleri yerleştirmekten hakkında tooworry yok. Azure, sizin için işler.

Yönetilen diskler, tootake kendi birçok özelliğinden seçmenizi öneririz.

Premium Storage'ı kullanmaya tooget [ücretsiz Azure hesabınızı oluşturmak](https://azure.microsoft.com/pricing/free-trial/). 

Var olan sanal makineleri tooPremium depolama geçirme hakkında daha fazla bilgi için bkz [Windows VM yönetilmeyen diskleri toomanaged diskleri dönüştürme](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) veya [bir Linux VM yönetilmeyen diskleri toomanaged diskleri dönüştürme](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Premium depolama çoğu bölgede kullanılabilir. Kullanılabilir bölgelerin hello listesi için [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services), hangi hello bölgelerde bakma desteklenen Premium destek boyutu-serisi VM'ler (DS serisi, DSV2 serisi, GS serisi ve Fs-serisi VM'ler) desteklenir.
> 

## <a name="features"></a>Özellikler

Premium Storage hello özelliklerden bazıları şunlardır:

* **Premium depolama diskleri**

    Olabilir premium depolama destekler VM diskleri ekli toospecific boyutu-serisi VM'ler. Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi, Ls-serisi ve Fs-serisi VM'ler. Yedi disk boyutları seçmesini: P4 (32GB), P6 (64GB), P10 (128GB), P20 (512GB), P30 (1024GB), P40 (2048GB), P50 (4095GB). P4 ve P6 disk boyutları henüz yalnızca yönetilen diskler için desteklenir. Her disk boyutu, kendi performans özellikleri vardır. Uygulama gereksinimlerinize bağlı olarak, bir veya daha fazla disk tooyour VM ekleyebilirsiniz. Biz hello belirtimleri daha ayrıntılı olarak açıklayan [Premium Storage ölçeklenebilirlik ve performans hedefleri](#scalability-and-performance-targets).

* **Premium sayfa BLOB'ları**

    Premium depolama sayfa bloblarını destekler. Premium depolama VM'ler için sayfa, BLOB'ları toostore kalıcı, yönetilmeyen diskleri kullanın. Standart Azure depolama, Premium depolama yok blok bloblarını destekler, BLOB'lar, dosyalar, tabloların veya kuyrukların ekleyin. Premium sayfa bloblarını P10 tooP50 ve P60 altı boyutlarını destekler (8191GiB). P60 Premium sayfa blobu desteklenen toobe VM diskleri olarak bağlı değil. 

    Premium depolama hesabı yerleştirilen herhangi bir nesne bir sayfa blob'u olacaktır. Merhaba sayfa blobu hello tooone sağlanan boyutları desteklenen tutturur. Premium depolama hesabı toobe toostore küçük BLOB'lar kullanılan amaçlanmamıştır nedeni budur.

* **Premium depolama hesabı**

    toostart Premium Storage kullanarak yönetilmeyen diskler bir premium depolama hesabı oluşturun. Merhaba, [Azure portal](https://portal.azure.com), toocreate bir premium depolama hesabı seçin hello **Premium** performans katmanı. Select hello **yerel olarak yedekli depolama (LRS)** çoğaltma seçeneği. Premium depolama hesabı hello türü çok ayarlayarak oluşturabilirsiniz**Premium_LRS** hello aşağıdaki konumlardan birinde:
    * [Storage REST API'sini](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (2014-02-14 sürümünü veya sonraki bir sürümünü)
    * [Hizmet Yönetimi REST API'si](http://msdn.microsoft.com/library/azure/ee460799.aspx) (sürüm 2014-10-01 veya sonraki bir sürümünü; Azure Klasik dağıtımlar için)
    * [Azure depolama kaynak sağlayıcısı REST API](https://docs.microsoft.com/rest/api/storagerp) (için Azure Resource Manager dağıtımları)
    * [Azure PowerShell](../powershell-install-configure.md) (sürüm 0.8.10 veya sonraki bir sürümünü)

    premium depolama hesabı sınırları hakkında toolearn bkz [Premium Storage ölçeklenebilirlik ve performans hedefleri](#premium-storage-scalability-and-performance-targets).

* **Premium yerel olarak yedekli depolama**

    Premium depolama hesabı yalnızca yerel olarak yedekli depolama hello çoğaltma seçeneği olarak destekler. Yerel olarak yedekli depolama tek bir bölge içinde hello veri üç kopyasını tutar. Bölgesel olağanüstü durum kurtarma için farklı bir bölgede, VM diskleri kullanarak yedeklemelisiniz [Azure Backup](../backup/backup-introduction-to-azure-backup.md). Ayrıca hello yedekleme kasası olarak coğrafi olarak yedekli depolama (GRS) hesabı kullanmanız gerekir. 

    Azure depolama hesabınızın yönetilmeyen diskleriniz için bir kapsayıcı olarak kullanır. Bir Azure DS serisi, DSv2 serisi, GS serisi, oluşturduğunuzda veya Fs-serisi VM yönetilmeyen disklerle ve premium depolama hesabı, işletim sisteminizi seçin ve veri diskleri bu depolama hesabında depolanır.

## <a name="supported-vms"></a>Desteklenen VM'ler
Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi, Ls-serisi ve Fs-serisi VM'ler. Bu VM türleriyle standart ve premium depolama diskleri kullanabilirsiniz. Premium depolama diskleri depolama uyumlu Premium olmayan VM dizisi ile kullanamazsınız.

VM türler ve Windows için Azure boyutları hakkında daha fazla bilgi için bkz: [Windows VM boyutları](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Linux VM türler ve Azure boyutları hakkında bilgi için bkz: [Linux VM boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bazı hello özelliklerini hello DS serisi, DSv2 serisi, GS serisi, bunlar Ls-serisi ve Fs-serisi VM'ler:

* **Bulut hizmeti**

    Yalnızca DS serisi vm'lere DS serisi VM'ler tooa bulut hizmeti ekleyebilirsiniz. DS serisi VM'ler dışındaki herhangi bir türü sahip DS serisi VM'ler tooan mevcut bulut hizmeti eklemeyin. Yalnızca DS serisi VM'ler çalıştıran mevcut VHD tooa yeni bulut hizmetiniz geçirebilirsiniz. İsterseniz toouse hello kullan sizin DS serisi VM'ler barındıran hello yeni bulut hizmeti için aynı sanal IP adresi [ayrılmış IP adresi](../virtual-network/virtual-networks-instance-level-public-ip.md). GS serisi VM'ler yalnızca GS serisi VM'ler sahip tooan mevcut bulut hizmeti eklenebilir.

* **İşletim sistemi diski**

    Premium veya standart işletim sistemi diski, Premium Storage VM'si toouse ayarlayabilirsiniz. Merhaba en iyi deneyim için Premium depolama-tabanlı işletim sistemi diski kullanmanızı öneririz.

* **Veri diskleri**

    Standart diskleri aynı Premium Storage VM'si hello ve premium kullanabilirsiniz. Premium depolama ile bir VM sağlamak ve birkaç kalıcı veri diskleri toohello VM ekleyin. Tooincrease hello kapasite ve performans hello biriminin gerekirse, disklerde şeritler.

    > [!NOTE]
    > Premium depolama veri diskleri kullanarak şeritler varsa [depolama alanları](http://technet.microsoft.com/library/hh831739.aspx), kullandığınız her disk için 1 sütun ile depolama alanları ayarlayın. Aksi takdirde, genel hello şeritli birim performansını trafiği düzensiz dağıtım nedeniyle hello disklerde beklenenden daha düşük olabilir. Varsayılan olarak, Sunucu Yöneticisi ' nde too8 diskleri için sütunları ayarlayabilirsiniz. 8'den çok disk varsa, PowerShell toocreate hello birimi kullanın. Sütun sayısı Hello el ile belirtin. Aksi takdirde, daha fazla disk olsa bile hello Sunucu Yöneticisi kullanıcı Arabirimi toouse 8 sütunları devam eder. Örneğin, tek kümesi 32 diskiniz varsa, 32 sütunları belirtin. toospecify hello sütun sayısı hello sanal diski kullanır, hello [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) PowerShell cmdlet'ini kullanın hello *NumberOfColumns* parametresi. Daha fazla bilgi için bkz: [depolama alanlarına genel bakış](http://technet.microsoft.com/library/hh831739.aspx) ve [depolama alanları sık sorulan sorular](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Önbellek**

    Premium Storage destekleyen hello boyutu serideki VM'ler yüksek düzeyde üretilen iş ve gecikmeyi için benzersiz bir önbelleğe alma özelliğine sahip. önbelleğe alma yeteneğini hello temel premium depolama disk performansı aşıyor. Premium depolama diskleri ilkesindeki çok önbelleğe alma hello disk ayarlayabilirsiniz**ReadOnly**, **ReadWrite**, veya **hiçbiri**. ilke önbelleği hello varsayılan disk **ReadOnly** tüm premium veri diskleri için ve **ReadWrite** işletim sistemi diskler için. Uygulamanız için en iyi performans için hello doğru önbellek ayarını kullanın. Örneğin, SQL Server veri dosyaları gibi okunur ağır veya salt okunur veri diskleri için ilke çok önbelleğe alma hello disk ayarlayın**salt okunur**. Ağır yazma ya da salt yazılır veri diskleri için SQL Server günlük dosyaları gibi ilke çok önbelleğe alma hello disk ayarlamak**hiçbiri**. Premium depolama ile tasarımınızı en iyi duruma getirme hakkında daha fazla toolearn bkz [tasarım performans için Premium depolama ile](storage-premium-storage-performance.md).

* **Analizler**

    Premium depolama biriminde diskleri kullanarak tooanalyze VM performans hello VM tanılamada Aç [Azure portal](https://portal.azure.com). Daha fazla bilgi için bkz: [Azure VM ile Azure tanılama uzantısını izleme](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    Kullanım tabanlı işletim sistemi araçları toosee disk performansı, ister [Windows Performans İzleyicisi'ni](https://technet.microsoft.com/library/cc749249.aspx) Windows sanal makineleri ve hello [iostat](http://linux.die.net/man/1/iostat) Linux VM'ler için komutu.

* **VM ölçek sınırlarını ve performans**

    Ölçek sınırlarını ve performans özelliklerini IOPS, bant genişliği ve VM başına bağlı diskler hello sayısı için her Premium depolama desteklenen VM boyutu vardır. Premium depolama diskleri VM ile birlikte kullandığınızda, yeterli IOPS ve VM toodrive disk trafiğinizi üzerindeki bant genişliği olduğundan emin olun.

    Örneğin, bir STANDARD_DS1 VM 32 MB/sn premium depolama disk trafiği için olan ayrılmış bir bant genişliğine sahiptir. P10 premium depolama diskini bir bant genişliği 100 MB/sn sağlayabilir. P10 premium depolama diskini ekli toothis VM ise, yalnızca too32 MB/sn gidebilirsiniz. En fazla 100 MB/sn, hello P10 disk sağlayabilir hello kullanamazsınız.

    Şu anda hello en büyük VM hello DS serisi, hello Standard_DS15_v2'dir. Merhaba Standard_DS15_v2 too960 MB/sn tüm disklerde sağlayabilir. Merhaba en büyük VM hello GS serisi içinde hello Standard_GS5'dir. Merhaba Standard_GS5 too2, 000 MB/sn tüm diskler boyunca yukarı sağlayabilir.

    Bu sınırlar yalnızca disk trafiği olduğunu unutmayın. Bu sınırlar İsabetli Önbellek okuma sayısı ve ağ trafiğini eklemeyin. VM ağ trafiği için ayrı bir bant genişliği kullanılabilir. Ağ trafiği için bant genişliği, premium depolama diskleri tarafından kullanılan ayrılmış hello bant genişliği farklıdır.

    Merhaba en güncel hakkında bilgi için maksimum IOPS ve üretilen işi (bant) Premium depolama desteklenen VM'ler için bkz: [Windows VM boyutları](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Linux VM boyutları](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Premium depolama disklerini ve bunların IOPS ve üretilen iş sınırları hakkında daha fazla bilgi için sonraki bölümde hello hello tabloya bakın.

## <a name="scalability-and-performance-targets"></a>Ölçeklenebilirlik ve performans hedefleri
Premium depolama kullandığınızda bu bölümde, biz hello ölçeklenebilirlik ve performans hedefleri tooconsider açıklanmaktadır.

Premium depolama hesapları ölçeklenebilirlik hedeflerini izleyerek hello vardır:

| Toplam hesabı kapasitesi | Yerel olarak yedekli depolama hesabı için toplam bant genişliği |
| --- | --- | 
| Disk kapasitesi: 35 TB <br>Kapasite anlık görüntü: 10 TB | Too50 Gigabit için saniye başına gelen<sup>1</sup> + giden<sup>2</sup> |

<sup>1</sup> tooa depolama hesabı gönderilen tüm veriler (istek sayısı)

<sup>2</sup> bir depolama hesabından alınan tüm verileri (yanıtlar)

Daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).

Yönetilmeyen diskler için premium depolama hesapları kullanıyorsanız ve uygulamanızın tek bir depolama hesabına hello ölçeklenebilirlik hedefleri aşarsa, toomigrate toomanaged diskleri isteyebilirsiniz. Toomigrate toomanaged diskleri istemiyorsanız, uygulama toouse birden çok depolama hesabı oluşturun. Ardından, bu depolama hesaplarında verilerinizi bölüm. Örneğin, tooattach 51 TB diskler arasında birden çok VM istiyorsanız, bunları iki depolama hesapları arasında yayılır. 35 TB tek premium depolama hesabı için hello sınırı vardır. Tek premium depolama hesabı hiçbir zaman birden fazla 35 TB sağlanan diskleri sahip olduğundan emin olun.

### <a name="premium-storage-disk-limits"></a>Premium depolama disk sınırları
Premium depolama disk hello hello diskin boyutunu sağlama belirlediğinde maksimum IOPS ve üretilen işi (bant) hello. Azure premium depolama disklerinin yedi türleri sunar: P4 (yönetilen diskler yalnızca), P6 (yönetilen diskler yalnızca), P10, P20, P30, P40 ve P50. Her premium depolama disk türü IOPS ve üretilen iş için belirli sınırları vardır. Sınırları hello disk türleri için aşağıdaki tablonun hello açıklanmaktadır:

| Premium diskler türü  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Disk boyutu           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Disk başına IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Disk başına aktarım hızı | Saniye başına 25 MB  | Saniye başına 50 MB  | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye | Saniye başına 250 MB | Saniye başına 250 MB | 

> [!NOTE]
> Bölümünde açıklandığı gibi yeterli bant genişliği VM toodrive disk trafiği üzerinde kullanılabilir olduğundan emin olun [Premium depolama desteklenen VM'ler](#premium-storage-supported-vms). Aksi takdirde, disk verimlilik ve IOPS, kısıtlanmış toolower değerleri olur. En yüksek verimlilik ve IOPS hello VM sınırları, değil, tablo önceki hello açıklanan hello disk sınırlarını dayanır.  
> 
> 

Premium Storage ölçeklenebilirlik ve performans hedefleri hakkında bazı önemli noktalar tooknow şunlardır:

* **Sağlanan kapasite ve performans**

    Standart depolama, farklı bir premium depolama diskini sağladığınızda hello kapasite, IOPS ve bu disk verimini sağlanır. Örneğin, bir P50 disk oluşturursanız, Azure 4.095 GB depolama kapasitesi, 7.500 IOPS ve bu disk için 250 MB/sn üretilen iş sağlar. Uygulamanız hello kapasite ve performans bölümünü veya tümünü kullanabilir.

* **Disk boyutu**

    Disk boyutu (yuvarlanan) toohello bölüm önceki hello hello tabloda belirtildiği gibi premium depolama diski seçeneği en yakın Azure eşlemeleri hello. Örneğin, 100 GB disk boyutunu P10 seçeneği olarak sınıflandırılır. Bu too500 IOPS ile too100 MB/sn'ye gerçekleştirebilir. Benzer şekilde, bir disk boyutu 400 GB P20 sınıflandırılır. Too2, 150 MB/sn üretilen iş ile 300 IOPS yukarı gerçekleştirebilirsiniz.
    
    > [!NOTE]
    > Kolayca hello var olan disklerin boyutunu artırabilirsiniz. Örneğin, bir 30 GB disk too128 GB ya da hatta too1 TB boyutunu tooincrease hello isteyebilirsiniz. Ya da daha fazla kapasite ya da daha fazla IOPS ve üretilen iş gerektiğinden tooconvert P20 disk tooa P30 diskinizin isteyebilirsiniz. 
    > 
 
* **G/ç boyutu**

    bir g/ç Hello boyutu 256 KB'tır. Aktarılan hello verilerin 256 KB'den az ise, 1 g/ç birim olarak kabul edilir. Daha büyük g/ç boyutları olarak birden çok g/ç boyutu sayılır 256 KB. Örneğin, 1.100 KB g/ç 5 g/ç birimleri kabul edilir.

* **Üretilen iş**

    yazma toohello disk Hello üretilen iş sınırı içerir ve hello önbellekten hizmet olmayan disk okuma işlemleri içerir. Örneğin, 100 MB/sn'ye disk başına P10 disk vardır. Aşağıdaki tablonun hello P10 diskin geçerli verimliliğini bazı örnekler gösterilmektedir:

    | P10 disk başına en fazla üretilen işi | Diskten olmayan önbelleğini okur | Toodisk olmayan önbellek Yazar |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/sn | 40 MB/sn |

* **İsabetli Önbellek okuma sayısı**

    IOPS veya hello disk verimini ayrılmış hello tarafından İsabetli Önbellek okuma sayısı sınırlı değildir. Örneğin, bir veri diski ile kullandığınızda bir **ReadOnly** önbellek ayarı Premium depolama, hello önbellekten sunulan okuma tarafından desteklenen bir VM'de konu toohello IOPS ve üretilen iş caps hello diskin değildir. Bir disk Hello iş yükünü daha ise okur, çok yüksek performans alabilirsiniz. Merhaba konu tooseparate IOPS ve üretilen iş sınırları hello VM boyutu üzerinde temel hello VM düzeyi en önbelleğidir. DS serisi VM'ler yaklaşık 4.000 IOPS ve çekirdek önbelleği ve yerel SSD g/ç için başına 33 MB/sn üretilen iş vardır. GS serisi VM'ler 5.000 IOPS'yi ve çekirdek önbelleği ve yerel SSD g/ç için başına 50 MB/sn üretilen iş sınırı vardır. 

## <a name="throttling"></a>Azaltma
Uygulamanızı IOPS veya verimlilik premium depolama diski için ayrılan hello sınırlarını aşıyor azaltma, meydana gelebilir. Toplam disk trafiğinizi hello VM üzerindeki tüm diskleri arasında hello hello VM için kullanılabilir disk bant genişliği sınırını aşarsa azaltma de oluşabilir. tooavoid kısıtlama, bekleyen hello disk g/ç istekleri hello sayısı sınırı öneririz. Sağlanan hello disk için ölçeklenebilirlik ve performans hedefleri ve hello disk bant genişliği kullanılabilir toohello VM dayalı bir sınır kullanın.  

Bunu tasarlarken, uygulamanızın hello en düşük gecikme süresi elde edebilirsiniz tooavoid azaltma. Ancak, Hello bekleyen hello disk g/ç istek sayısı kadar küçükse, uygulamanızın kullanılabilir toohello diski maksimum IOPS ve üretilen iş düzeyler hello avantajlarından alamıyor.

Örnek hello nasıl toocalculate azaltma düzeyleri gösterilmektedir. Tüm hesaplamalar 256 KB üzerinde bir g/ç birim boyutunu temel alır.

### <a name="example-1"></a>Örnek 1
Uygulamanızı bir P10 diskte bir saniye içinde 16 KB boyutunu 495 g/ç birimleri işledi. Merhaba g/ç birimleri 495 IOPS sayılır. Bir 2 MB g/ç çalışırsanız aynı ikinci Merhaba, g/ç birimleri hello toplam eşit too495 + 8 IOPS. Bunun nedeni, 2 MB g/ç 2.048 KB / 256 KB = 8 g/ç birimleri = hello g/ç birim boyutu 256 KB'dir olduğunda. 495 + 8 Hello toplamını hello disk için 500 IOPS sınırı hello aştığından azaltma oluşur.

### <a name="example-2"></a>Örnek 2
Uygulamanızı bir P10 diskte 256 KB boyutunu 400 g/ç birimleri işledi. tüketilen hello toplam bant genişliği (400 &#215; 256) / 1.024 KB = 100 MB/s. P10 disk, 100 MB/sn üretilen iş sınırı vardır. Uygulamanız bu saniye içinde birden çok g/ç işlemleri tooperform çalışırsa, ayrılan hello üst sınırını aştığı için kısıtlanır.

### <a name="example-3"></a>Örnek 3
Bağlı iki P30 disklerle DS4 VM var. Her P30 disk 200 MB/sn verimini yeteneğine sahiptir. Ancak, bir DS4 VM 256 MB/sn toplam disk bant genişliği kapasitesine sahiptir. Bu DS4 VM'de Merhaba, iki bağlı disklerde toohello en yüksek verimlilik sürücü olamaz aynı anda. tooresolve Bu, 200 MB trafiğinin karşılayabilir/s bir diske ve 56 MB/s hello diğer disk. Disk trafiğinizi Hello toplamı 256 MB/sn kalırsa, disk trafiği azaltılır.

> [!NOTE]
> Disk trafiğinizi çoğunlukla küçük g/ç boyutlarını oluşuyorsa, büyük olasılıkla, uygulamanızın hello IOPS sınırı hello üretilen iş sınırı önce karşılaşır. Merhaba disk trafiği çoğunlukla büyük g/ç boyutlarını oluşuyorsa, ancak, büyük olasılıkla, uygulamanızın hello üretilen iş sınırı ilk olarak, hello IOPS sınırı yerine karşılaşır. Uygulamanızın IOPS ve işleme kapasitesi en iyi g/ç boyutları kullanarak en üst düzeye çıkarabilirsiniz. Ayrıca, bekleyen bir disk g/ç istekleri hello sayısını sınırlayabilirsiniz.
> 

Premium depolama kullanarak yüksek performans için tasarlama hakkında daha fazla toolearn bkz [tasarım performans için Premium depolama ile](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Anlık görüntüler ve kopyalama Blob

toohello Depolama Birimi hizmetini hello VHD dosyasını sayfa blob ' dir. Sayfa bloblarını anlık görüntülerini almak ve bunları tooa farklı depolama hesabı gibi tooanother konuma kopyalayın.

### <a name="unmanaged-disks"></a>Yönetilmeyen diskler

Oluşturma [artımlı anlık görüntüleri](storage-incremental-snapshots.md) yönetilmeyen premium diskleri aynı hello için yolu ile standart depolama anlık görüntüleri kullanın. Premium depolama yalnızca yerel olarak yedekli depolama hello çoğaltma seçeneği olarak destekler. Anlık görüntüler oluşturmak ve hello anlık görüntüleri tooa standart coğrafi olarak yedekli depolama hesabı kopyalama öneririz. Daha fazla bilgi için bkz: [Azure depolama artıklığı seçeneği](storage-redundancy.md).

Bir disk ekli tooa VM ise, bazı API işlemleri hello diskteki izin verilmez. Örneğin, gerçekleştiremezsiniz bir [kopyalama Blob](/rest/api/storageservices/Copy-Blob) hello disk ise, blob işlemi tooa VM bağlı. Bunun yerine, önce bir anlık görüntüsünü o blob hello kullanarak oluşturmak [anlık görüntü Blob](/rest/api/storageservices/Snapshot-Blob) REST API. Ardından, hello gerçekleştirin [kopyalama Blob](/rest/api/storageservices/Copy-Blob) hello anlık görüntü toocopy Merhaba disk eklendi. Alternatif olarak, hello disk ayırma ve gerekli işlemleri gerçekleştirin.

sınırları aşağıdaki hello toopremium depolama blob anlık görüntüleri Uygula:

| Premium depolama sınırı | Değer |
| --- | --- |
| Maksimum sayıda anlık görüntü blob başına | 100 |
| Anlık görüntüler için depolama hesabı kapasitesi<br>(Verileri yalnızca anlık görüntülerini içerir. Veri temel blob dahil değildir.) | 10 TB |
| Art arda gelen anlık görüntüleri arasındaki en kısa süre | 10 dakika |

toomaintain coğrafi olarak yedekli, anlık görüntü kopyalarını, AzCopy veya kopya Blob kullanarak bir premium depolama hesabı tooa standart coğrafi olarak yedekli depolama hesabından anlık görüntüleri kopyalayabilirsiniz. Daha fazla bilgi için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) ve [kopyalama Blob](/rest/api/storageservices/Copy-Blob).

Premium depolama hesabı sayfa bloblarını karşı REST işlemlerini gerçekleştirme hakkında ayrıntılı bilgi için bkz: [Blob Azure Premium Storage ile hizmet işlemleri](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Yönetilen diskler

Yönetilen bir disk için bir anlık görüntü hello yönetilen diskin salt okunur bir kopyasıdır. Başlangıç anlık görüntü standart yönetilen disk olarak depolanır. Şu anda [artımlı anlık görüntüleri](storage-incremental-snapshots.md) yönetilen disklerde desteklenmez. tootake yönetilen bir disk için bir anlık görüntü nasıl görürüm toolearn [Azure yönetilen olarak depolanan VHD bir kopyasını oluşturmak Windows'da yönetilen anlık görüntülerini kullanarak disk](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) veya [Azure yönetilen olarak depolanan VHD bir kopyasını oluşturmak yönetilen kullanarak disk Linux anlık görüntüleri](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Yönetilen bir disk ekli tooa VM ise, bazı API işlemleri hello diskteki izin verilmez. Örneğin, Hello disk ekli tooa VM olsa da bir paylaşılan erişim imzası (SAS) tooperform bir kopyalama işlemi oluşturulamıyor. Bunun yerine, önce hello diskin anlık görüntüsünü oluşturabilir ve sonra hello anlık görüntü hello kopyasını gerçekleştirin. Alternatif olarak, hello disk ayırma ve bir SAS tooperform hello kopyalama işlemi oluşturur.


## <a name="premium-storage-for-linux-vms"></a>Premium depolama Linux VM'ler
Merhaba, Linux VM'ler için Premium depolama ayarlama bilgi toohelp aşağıdaki kullanabilirsiniz:

tooachieve ölçeklenebilirlik hedefler Premium depolama biriminde, tüm premium depolama disklerle kümesi çok önbelleği**ReadOnly** veya **hiçbiri**, hello dosya sistemi bağladığınızda "engelleri" devre dışı bırakmanız gerekir. Merhaba toopremium depolama diskleri için bu önbellek ayarlarını dayanıklı yazdığından Bu senaryoda engelleri gerekmez. Merhaba yazma isteği başarıyla tamamlandığında, veri toohello kalıcı depoya yazılmış. toodisable "engelleri," hello yöntemler aşağıdaki birini kullanın. Dosya sistemi için Hello seçin:
  
* İçin **reiserFS**, toodisable engelleri kullanmak hello `barrier=none` bağlama seçeneği. (tooenable engelleri kullanmak `barrier=flush`.)
* İçin **ext3/ext4**, toodisable engelleri kullanmak hello `barrier=0` bağlama seçeneği. (tooenable engelleri kullanmak `barrier=1`.)
* İçin **XFS**, toodisable engelleri kullanmak hello `nobarrier` bağlama seçeneği. (tooenable engelleri kullanmak `barrier`.)
* Premium depolama diskleri önbellek çok ayarlamak için**ReadWrite**, engelleri yazma dayanıklılık için etkinleştirin.
* Birim etiketleri toopersist hello VM'yi yeniden başlattıktan sonra hello evrensel benzersiz tanımlayıcı (UUID) başvuruları toohello disklerle /etc/fstab güncelleştirmelisiniz. Daha fazla bilgi için bkz: [yönetilen disk tooa Linux VM eklemek](../virtual-machines/linux/add-disk.md).

Linux dağıtımları aşağıdaki hello Azure Premium Storage için doğrulandı. Daha iyi performans ve kararlılık Premium depolama alanına sahip en az bu sürümlerinin, VM'ler tooone yükseltmenizi öneririz (veya tooa sonraki bir sürümü). Bazı sürümlerini gerektirir hello son Linux Tümleştirme hizmetleri (LIS), v4.0, Azure için hello. toodownload ve yükleme bir dağıtım, aşağıdaki tablonun hello listelenen hello bağlantıyı izleyin. Biz doğrulama tamamlarken biz görüntüleri toohello listeye ekleyin. Bizim doğrulamaları performans için her görüntü değişir Göster unutmayın. Performans, iş yükü özellikleri ve görüntü ayarlarınızı bağlıdır. Farklı görüntüleri farklı türde iş yükleri için ayarlanmıştır.

| Dağıtım | Sürüm | Desteklenen çekirdek | Ayrıntılar |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-Server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-Server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| SuSE-sles-12-öncelik-v20150213 <br> sles 12 v20150213 SuSE |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [Gerekli LIS4](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Merhaba sonraki bölümde nota bakın* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [Önerilen LIS4](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Merhaba sonraki bölümde nota bakın* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 veya RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 veya RHCK içeren[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 veya RHCK içeren[LIS 4.1 +](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>OpenLogic CentOS için LIS sürücüleri

OpenLogic CentOS VM'ler çalıştırıyorsanız, komut tooinstall hello en son sürücülere aşağıdaki hello çalıştırın:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello yeni sürücülerin, hello bilgisayarı yeniden başlatın.

## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama

Premium depolama kullandığınızda, aşağıdaki fatura değerlendirmeleri hello uygulayın:

* **Premium depolama diski ve blob boyutu**

    Premium depolama diskini veya blob için fatura hello diski veya blob sağlanan hello boyutuna bağlıdır. Azure eşlemeleri (yuvarlanan) sağlanan boyutu toohello premium depolama diski seçeneği en yakın hello. Merhaba tabloda Ayrıntılar için bkz [Premium Storage ölçeklenebilirlik ve performans hedefleri](#premium-storage-scalability-and-performance-targets). Desteklenen her disk eşlemeleri tooa sağlanan disk boyutu ve buna göre faturalandırılır. Sağlanan herhangi bir disk için fatura, saatlik hello Premium depolama teklif için hello aylık fiyat kullanarak eşit olarak bölünür. Örneğin, bir P10 disk sağlanan ve 20 saat sonra silinir, eşit olarak bölünmüş too20 saatleri sunumu Merhaba P10 faturalandırılır. Merhaba toohello disk veya hello IOPS ve üretilen iş kullanılan yazılan gerçek veri miktarı bağımsız olarak budur.

* **Premium yönetilmeyen disklerin anlık görüntüleri**

    Yönetilmeyen premium diskleri anlık görüntü hello anlık görüntüleri tarafından kullanılan hello ek kapasite için faturalandırılır. Anlık görüntüler hakkında daha fazla bilgi için bkz: [blob görüntüsünü](/rest/api/storageservices/Snapshot-Blob).

* **Yönetilen premium disklerin anlık görüntüleri**

    Yönetilen bir disk görüntüsünü hello diskin salt okunur bir kopyasıdır. Merhaba disk standart yönetilen disk olarak depolanır. Standart yönetilen disk olarak bir anlık görüntü maliyetleri aynı hello. 128 GB premium yönetilen diskin bir anlık görüntüsünü alırsanız, örneğin, hello hello anlık görüntü eşdeğer tooa 128 GB standart yönetilen disk maliyetidir.  

* **Giden veri aktarımları**

    [Giden veri aktarımları](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure veri merkezleri dışında giderek veri) bant genişliği kullanımı için fatura doğurur.

Premium depolama, Premium depolama desteklenen VM'ler ve yönetilen diskleri için fiyatlandırma hakkında ayrıntılı bilgi için bu makalelere bakın:

* [Azure Depolama fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/)
* [Sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Fiyatlandırma yönetilen diskleri](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Azure yedekleme desteği 

Bölgesel olağanüstü durum kurtarma için farklı bir bölgede, VM diskleri kullanarak yedeklemelisiniz [Azure yedekleme](../backup/backup-introduction-to-azure-backup.md) ve bir yedekleme kasası olarak GRS depolama hesabı.

toocreate bir yedekleme işi zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri, Azure yedekleme kullanın. Yönetilen ve yönetilmeyen disklerle yedekleme hem de kullanabilirsiniz. Daha fazla bilgi için bkz: [yönetilmeyen diskleri olan VM'ler için Azure Backup](../backup/backup-azure-vms-first-look-arm.md) ve [yönetilen diskleri olan VM'ler için Azure Backup](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Sonraki adımlar
Premium depolama hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın.

### <a name="design-and-implement-with-premium-storage"></a>Premium depolama ile tasarlayıp
* [Premium depolama alanına sahip bir performans için tasarlama](storage-premium-storage-performance.md)
* [Premium depolama alanına sahip BLOB Depolama işlemleri](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>İşlemsel kılavuz
* [Premium depolama tooAzure geçirme](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Premium Storage genel olarak kullanılabilir](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Merhaba GS serisi tanışın: Vm'lerde hello genel bulut Premium depolama destek toohello en büyük ekleme](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)

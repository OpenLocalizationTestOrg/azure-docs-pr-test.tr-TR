---
title: "StorSimple sanal dizini aaaBest yöntemler | Microsoft Docs"
description: "Dağıtma ve yönetme hello StorSimple sanal dizinin hello en iyi uygulamaları açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>StorSimple sanal dizinin en iyi uygulamalar
## <a name="overview"></a>Genel Bakış
Microsoft Azure StorSimple sanal dizinin bir hiper yönetici ve Microsoft Azure bulut depolama çalıştıran bir şirket içi sanal aygıt arasında depolama görevleri yöneten bir tümleşik depolama çözümüdür. StorSimple sanal verimli ve ekonomik alternatif toohello 8000 serisi fiziksel dizi dizisidir. Merhaba sanal dizi varolan hiper yönetici altyapınızda çalıştırabilirsiniz, hello iSCSI ve hello SMB protokollerini destekler ve uzak office/şube ofisi senaryolarında için de çok uygundur. Merhaba StorSimple çözümleri hakkında daha fazla bilgi için çok Git[Microsoft Azure StorSimple genel bakış](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

Bu makalede hello ilk Kurulum, dağıtımı ve Yönetimi hello StorSimple sanal dizinin sırasında uygulanan hello en iyi yöntemleri kapsar. Bu en iyi uygulamaları hello Kurulum ve Yönetim sanal dizinin için doğrulanmış yönergeleri sağlar. Bu makalede hedeflenen BT hello dağıtmak ve yönetmek yöneticiler kendi veri merkezlerini sanal dizilerde hello.

Merhaba en iyi yöntemler toohelp periyodik olarak İnceleme toohello Kurulum veya işlem akış değişiklik yapıldığında, cihazınız hala uyumlu olduğundan emin olun öneririz. Karşılaştığınız sorunları sanal dizinizi üzerinde uygulama çalışırken bu en iyi yöntemler [Microsoft Support başvurun](storsimple-virtual-array-log-support-ticket.md) Yardım için.

## <a name="configuration-best-practices"></a>Yapılandırma en iyi uygulamalar
Bu en iyi uygulamaları ardından hello ilk kurulum ve dağıtım hello sanal dizi sırasında toobe gereksinim hello yönergeleri kapsar. Bu en iyi uygulamaları hello sanal makineye, Grup İlkesi ayarları, boyutlandırma, sağlama ayarlama hello ağ, depolama hesaplarını yapılandırma ve paylaşımlar oluşturma ve birimler için sanal dizinin hello ilgili bu toohello içerir. 

### <a name="provisioning"></a>Sağlama
StorSimple sanal hello hiper yöneticide (Hyper-V veya VMware) sağlanan sanal makine (VM), ana bilgisayar sunucusu dizidir. Merhaba sanal makine sağlanırken, ana bilgisayarınız mümkün toodedicate yeterli kaynağı olduğundan emin olun. Daha fazla bilgi için çok Git[düşük kaynak gereksinimlerini](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision bir dizi.

Hello sanal dizinin sağlamada en iyi uygulamaları izleyerek hello uygulayın:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Sanal makine türü** |**2. nesil** Windows Server 2012 veya daha sonra kullanmak için VM ve *.vhdx* görüntü. <br></br> **1. nesil** VM için bir Windows Server 2008 veya sonraki sürümünü kullanın ve *.vhd* görüntü. |Kullanırken sanal makine sürüm 8-11 *.vmdk* görüntü. |
| **Bellek türü** |Olarak yapılandırma **statik bellek**. <br></br> Merhaba kullanmayın **dinamik bellek** seçeneği. | |
| **Veri disk türü** |Olarak sağlamak **dinamik olarak genişletilen**.<br></br> **Boyutu sabit** uzun sürüyor. <br></br> Merhaba kullanmayın **fark kayıt** seçeneği. |Kullanım hello **ince provizyon** seçeneği. |
| **Veri diski değişikliği** |Genişletme veya küçültme izin verilmiyor. Bir girişim toodo şekilde hello cihazdaki tüm hello yerel verilerin kaybedilmesine sonuçlanır. |Genişletme veya küçültme izin verilmiyor. Bir girişim toodo şekilde hello cihazdaki tüm hello yerel verilerin kaybedilmesine sonuçlanır. |

### <a name="sizing"></a>Boyutlandırma
StorSimple sanal dizinizi boyutlandırma, Etkenler aşağıdaki hello göz önünde bulundurun:

* Birimler veya paylaşımlar için yerel ayırma. Merhaba alanı yaklaşık % 12 hello yerel katmanda her sağlanan katmanlı birim veya paylaşım için ayrılmıştır. Kabaca hello alanın % 10 da yerel olarak sabitlenmiş bir birim dosya sistemi için ayrılmış.
* Ek yükü anlık görüntüsünü alın. Kabaca % 15 alanı hello yerel katmanında anlık görüntüler için ayrılmıştır.
* Geri yüklemeler için gerekli. Yeni bir işlem olarak geri yükleme yapılması boyutlandırma geri yüklemek için gereken hello alanı için hesap. Geri yükleme yapılır tooa paylaşımı veya birimi Merhaba, aynı boyutu.
* Bazı arabellek herhangi beklenmeyen büyüme için ayrılmalıdır.

Etkenler önceki hello üzerinde bağlı olarak, gereksinimleri boyutlandırma hello eşitlik aşağıdaki hello tarafından gösterilebilir:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Merhaba aşağıdaki örneklerde gereksinimlerinize göre sanal bir dizi nasıl boyut gösterilmektedir.

#### <a name="example-1"></a>Örnek 1:
Sanal dizinizi üzerinde toobe için istediğiniz

* 2 TB sağlamak katmanlı birim veya paylaşım.
* 1 TB sağlamak katmanlı birim veya paylaşım.
* yerel olarak sabitlenmiş birimin 300 GB sağlamak ya da paylaşabilirsiniz.

Merhaba önceki birimler veya paylaşımlar, izin bize hello yerel katmanında hello alanı gereksinimlerini hesaplamak.

İlk olarak, her katmanlı birim/paylaşımı için yerel ayırma hello birim/paylaşma boyutunun eşit too12% olacaktır. Yerel olarak sabitlenmiş hello birim/için yerel ayırma (Ayrıca toohello boyutu sağlanan) birim/paylaşımı boyutu % 10'hello yerel olarak sabitlenmiş paylaşımıdır. Bu örnekte, gerekir

* 240 GB yerel ayırma (için 2 TB katmanlı birim/paylaşım)
* 120 GB yerel ayırma (1 TB katmanlı birim/paylaşma)
* Yerel olarak sabitlenmiş bir birim veya paylaşım (yerel ayırma toohello sağlanan 300 GB boyutunun % 10 ekleme) için 330 GB

Merhaba toplam alan hello yerel katmanında kadarki gerekli olduğu: 240 GB + 120 GB + 330 GB = 690 GB.

İkincisi, en az olarak kadar alan hello yerel katmanında hello en büyük tek ayırma ihtiyacımız var. Bu ek miktar bir bulut anlık toorestore gerektiğinde kullanılır. Bu örnekte, hello en büyük yerel ayırma 330 (dosya sistemi için ayırma dahil), GB'dir bu toohello eklediğiniz şekilde 690 GB: 690 GB + 330 GB = 1020 GB.
Biz sonraki ek geri yükleme gerçekleştirdiyseniz, biz her zaman hello önceki geri yükleme işleminden hello alanı boşaltabilirsiniz.

Toplam yerel % 15 üçüncü ihtiyacımız % 85'yalnızca bunu kullanılabilir olmasını sağlamak toostore yerel anlık görüntüler, o ana kadarki boşluk. Bu örnekte, olacaktır geçici 1020 GB = 0.85&ast;sağlanan veri TB disk. Bu nedenle, hello sağlanan veri diski olacaktır (1020&ast;(1/0.85)) 1200 GB = 1.20 TB = ~ 1,25 TB (yuvarlama toonearest DÖRTTEBİRLİK devre dışı)

Beklenmeyen büyüme ve yeni geri yüklemeler Finansman, geçici bir yerel disk sağlamanız 1,25 - 1, 5 TB.

> [!NOTE]
> Ayrıca bu hello yerel diski ölçülü kaynak öneririz. Bu öneri, beş günden eski toorestore veri istediğinizde hello geri yükleme alanı yalnızca gerekli olmasıdır. Öğe düzeyinde kurtarma verir toorestore veri hello için son beş gün gerek kalmadan hello geri yüklemek için ek boşluk.


#### <a name="example-2"></a>Örnek 2:
Sanal dizinizi üzerinde toobe için istediğiniz

* 2 TB sağlamak katmanlı birim
* yerel olarak sabitlenmiş 300 GB birimi sağlamak

İhtiyacımız katmanlı birimlerin/paylaşımları için yerel alanı ayırma ve yerel olarak sabitlenmiş birimleri/paylaşımları için % %10 12 bağlı olarak,

* 240 GB yerel ayırma (2 TB katmanlı birim/paylaşım)
* Yerel olarak sabitlenmiş bir birim veya paylaşım (yerel ayırma toohello sağlanan 300 GB alanın % 10 ekleme) için 330 GB

Merhaba yerel katmanında gerekli toplam alan: 240 GB + 330 GB = 570 GB

Merhaba en düşük yerel alan geri yüklemek için gereken 330 GB'dir.

Toplam disk % 15 kullanılan toostore anlık görüntüler, böylelikle yalnızca 0.85 kullanılabilir. Bu nedenle, hello disk boyutudur (900&ast;(1/0.85)) 1.06 TB = ~ 1,25 TB (yuvarlama toonearest DÖRTTEBİRLİK devre dışı)

Beklenmeyen bir artışa Finansman, yerel bir 1,25-1,5 TB disk sağlayabilirsiniz.

### <a name="group-policy"></a>Grup İlkesi
Grup İlkesi, kullanıcılar ve bilgisayarlar için belirli yapılandırmalar tooimplement sağlayan bir altyapıdır. Bağlantılı toohello olan Grup İlkesi nesneleri (GPO'lar), Grup İlkesi ayarları yer alan Active Directory etki alanı Hizmetleri (AD DS) kapsayıcıları aşağıdaki: siteleri, etki alanları veya kuruluş birimlerini (OU). 

Sanal dizinizi etki alanına katılmış ise, GPO'ları uygulanan tooit olabilir. Bu GPO'ları hello StorSimple sanal dizinin hello işlemi olumsuz yönde etkileyebilir bir virüsten koruma yazılımı gibi uygulamaları yükleyebilirsiniz.

Bu nedenle, öneririz:

* Sanal dizinizi Active Directory için kendi kuruluş biriminde (OU) olduğundan emin olun.
* Hiçbir Grup İlkesi nesneleri (GPO'lar) uygulanan tooyour sanal dizi olduğundan emin olun. Devralmayı engelleyebilirsiniz sanal dizinin (alt düğümü) hello tooensure hello üst öğeden herhangi bir GPO otomatik olarak devralmaz. Daha fazla bilgi için çok Git[engelleme devralma](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Ağ
Sanal dizinizi Hello ağ yapılandırması hello yerel web kullanıcı Arabirimi gerçekleştirilir. Bir sanal ağ arabirimi hello sanal dizinin sağlandı hello hiper yönetici etkinleştirilir. Kullanım hello [ağ ayarlarını](storsimple-virtual-array-deploy3-fs-setup.md) sayfa tooconfigure hello sanal ağ arabirimi IP adresi, alt ağ ve ağ geçidi.  Cihazınız için hello birincil ve ikincil DNS sunucusu, saat ayarlarını ve isteğe bağlı proxy ayarlarını da yapılandırabilirsiniz. Çoğu hello ağ yapılandırması, bir kerelik Kurulum olur. Gözden geçirme hello [ağ gereksinimleri StorSimple](storsimple-ova-system-requirements.md#networking-requirements) önceki toodeploying hello sanal dizi.

Sanal dizinizi dağıtırken bu en iyi uygulamaları izlemeniz önerilir:

* Hangi hello sanal dizinin her zaman dağıtılır, hello ağ hello kapasite toodedicate 5 MB/sn Internet bant genişliği (veya daha fazla) olduğundan emin olun.
  
  * Internet bant genişliği gereksinimi, iş yükü özellikleri ve veri değişim oranı hello bağlı olarak değişir.
  * işlenebilir hello veri değişikliği orantılı tooyour Internet bant genişliği ' dir. Bir yedekleme duruma getirirken örnek olarak, 5 MB/sn bant genişliği 18 GB yaklaşık 8 saat içindeki bir veri değişikliği barındırabilir. Dört kez daha fazla bant genişliği ile (20 MB/sn), dört kat daha fazla veri değişikliği (72 GB) işleyebilir.
* Internet bağlantısı toohello her zaman kullanılabilir olduğundan emin olun. Aralıklı ya da güvenilir olmayan Internet bağlantıları toohello aygıtları erişim toodata hello bulutta kaybına neden ve desteklenmeyen bir yapılandırmada neden olabilir.
* Cihazınızı bir iSCSI sunucusu olarak toodeploy düşünüyorsanız:
  
  * Merhaba devre dışı bırakmanızı öneririz **IP adresini otomatik olarak almak** seçeneği (DHCP).
  * Statik IP adreslerini yapılandırın. Birincil ve ikincil bir DNS sunucusu yapılandırmanız gerekir.
  * Birden çok ağ arabirimi sanal dizinizi tanımlanıyorsa, yalnızca ilk ağ arabirimi hello (varsayılan olarak, bu arabirimidir **Ethernet**) hello bulut ulaşabilirsiniz. toocontrol hello türü trafiği birden çok sanal ağ arabirimi (iSCSI sunucusu olarak yapılandırılmış) sanal dizinizi oluşturun ve bu arabirimleri toodifferent alt ağlardan bağlanın.
* toothrottle hello bulut bant genişliği yalnızca (Merhaba sanal dizisi tarafından kullanılır), hello yönlendirici veya hello güvenlik duvarı azaltma yapılandırın. Hiper yöneticide azaltma tanımlarsanız, iSCSI ve SMB yalnızca hello bulut bant yerine dahil olmak üzere tüm hello protokolleri kısıtlama.
* Hiper yöneticilerin etkin o zaman eşitleme emin olun. Hyper-V kullanarak seçin, sanal dizinizi hello Hyper-V Yöneticisi'ni çok gidin**ayarları &gt; Integration Services**ve bu hello olun **zaman eşitleme** denetlenir.

### <a name="storage-accounts"></a>Depolama hesapları
StorSimple sanal dizinin tek bir depolama hesabıyla ilişkili olabilir. Bu depolama hesabının otomatik olarak oluşturulan depolama hesabı, hesap hello içinde olabilir hello hizmet ya da depolama hesabı aynı abonelik ilgili tooanother abonelik. Daha fazla bilgi için bkz. nasıl çok[sanal dizinizi depolama hesaplarını yönetme](storsimple-virtual-array-manage-storage-accounts.md).

Aşağıdaki önerileri sanal dizinizi ile ilişkili depolama hesapları için kullanım hello.

* Merhaba maksimum kapasite (64 TB) bir sanal dizinin ve bir depolama hesabı için hello maksimum boyut (500 TB) için tek bir depolama hesabına birden çok sanal dizilerle bağlanırken öğeli. Bu, bu depolama hesabı tooabout 7 ile ilişkilendirilebilir tam boyutlu sanal diziler hello sayısını sınırlar.
* Yeni bir depolama hesabı oluştururken
  
  * StorSimple sanal dizinizi dağıtılan toominimize gecikmeleri olduğu hello bölgeye en yakın toohello uzak office/şube ofisinde oluşturmanızı öneririz.
  * Farklı bölgelerdeki depolama hesabı taşıyamazsınız aklınızda size aittir. Ayrıca bir hizmet abonelikler arasında taşınamaz.
  * Artıklık hello veri merkezleri arasında uygulayan bir depolama hesabı kullanın. Coğrafi olarak yedekli depolama (GRS), bölge olarak yedekli depolama (ZRS) ve yerel olarak yedekli depolama (LRS) tüm sanal dizinizi ile kullanım için desteklenir. Merhaba farklı türlerde depolama hesapları hakkında daha fazla bilgi için çok Git[Azure storage çoğaltma](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Paylaşımları ve birimler
StorSimple sanal dizinizi için bir dosya sunucusu ve bir iSCSI sunucusu olarak yapılandırıldığında birimleri olarak yapılandırıldığında paylaşımları sağlayabilirsiniz. paylaşımları ve birimler oluşturmak için en iyi uygulamalar hello toohello boyutunu ve hello türünü yapılandırılmış ilişkilidir.

#### <a name="volumeshare-size"></a>Birim/paylaşımı
Bir dosya sunucusu ve bir iSCSI sunucusu olarak yapılandırıldığında birimleri olarak yapılandırıldığında, sanal dizinizi üzerinde paylaşımları sağlayabilirsiniz. paylaşımları ve birimler oluşturmak için en iyi uygulamalar hello toohello boyutu ilgili ve yapılandırılmış türü hello. 

Paylaşımlar veya birimler, sanal Cihazınızda sağlamada en iyi uygulamaları izleyerek göz hello unutmayın.

* Merhaba dosya boyutları sağlanan göreli toohello katmanlı bir paylaşımı boyutunu hello katmanlama performansı etkileyebilir. Büyük dosyaları ile çalışma yavaş katmanı genişletmek neden olabilir. Büyük dosyaları ile çalışırken, o hello en büyük dosya hello paylaşım boyutu %3 küçük öneririz.
* En fazla 16 birimleri/paylaşımları hello sanal dizisinde oluşturulabilir. Merhaba Hello boyutu sınırları yerel olarak sabitlenmiş ve katmanlı birimlerin/paylaşımları, her zaman toohello bakın [StorSimple sanal dizinin sınırlar](storsimple-ova-limits.md).
* Bir birim oluştururken, Gelecekteki büyümeyi yanı sıra beklenen hello veri tüketim faktörü. Merhaba birim daha sonra genişletilemiyor.
* Merhaba birim oluşturulduktan sonra StorSimple hello birimde hello boyutu küçültülemez.
* Merhaba birim verilerini belirli bir eşiği (göreli toohello yerel alan hello birimi için ayrılan) ulaştığında tooa yazma StorSimple, birimde katmanlı, hello GÇ kısıtlanır. Toowrite toothis birim etmeden GÇ hello önemli ölçüde yavaşlatır. Tooa yazabilirsiniz ancak katmanlı birim kapasitesinin (biz değil etkin bir şekilde Durdur yazma hello sağlanan kapasite ötesinde hello kullanıcıdan) sağlanan, talep bir uyarı bildirimi toohello efekti bakın. Merhaba uyarısı gördüğünüzde, silme hello birim verilerini gibi düzeltici önlemleri almasını kesinlik temelli (Birim genişletme şu anda desteklenmiyor).
* Olağanüstü durum kurtarma kullanım örnekleri için hello sayısı izin verilen paylaşımları/16 ve en fazla hello gibi paralel olarak işlenebilir paylaşımları/birim sayısı ayrıca 16, paylaşımları/birim hello sayısı şifrelemeyle RPO ve Rto'lara yok.

#### <a name="volumeshare-type"></a>Birim/paylaşım türü
StorSimple hello kullanımına bağlı iki birim/paylaşma türlerini destekler: yerel olarak sabitlenmiş ve katmanlı. Merhaba katmanlı birimlerin/paylaşımları ölçülü kaynak ancak yerel olarak sabitlenmiş birimleri/paylaşımları sıkı sağlanır. Yerel olarak sabitlenmiş birim/paylaşma tootiered dönüştürülemiyor veya *tersi* oluşturulduktan sonra.

StorSimple birimlerini/paylaşımları yapılandırırken en iyi uygulamaları izleyerek hello uygulamak öneririz:

* Bir birim oluşturmadan önce toodeploy düşündüğünüz hello iş yükleri üzerinde temel hello birim türünü tanımlayın. Yerel olarak sabitlenmiş birimlerin (hatta sırasında bulut kesinti) veri yerel GARANTİLERİN gerektiren ve düşük bulut gecikme süreleri gerektiren iş yükleri için kullanın. Bir birim üzerinde sanal dizinizi oluşturduktan sonra yerel olarak sabitlenmiş tootiered hello birim türü değiştirilemiyor veya *tam tersini*. Örnek olarak, yerel olarak sabitlenmiş birimlerin SQL iş yükleri veya iş yükleri barındıran sanal makineleri (VM'ler); dağıtırken oluşturma Katmanlı birimler, dosya paylaşımı iş yükleri için kullanın.
* Daha az sık kullanılan arşiv verileri için Hello seçeneği büyük dosya boyutlarına sahip ilgilenirken denetleyin. Bu seçenek etkinleştirildiğinde, daha büyük bir yinelenenleri kaldırma öbek boyutu 512 k kullanılan tooexpedite hello veri aktarımı toohello bulut.

#### <a name="volume-format"></a>Birim biçimi
StorSimple birimlerini iSCSI sunucunuzda oluşturduktan sonra tooinitialize, bağlama ve biçiminde hello gereksinim birimler. Bu işlem hello bağlı ana bilgisayar tooyour StorSimple cihazında gerçekleştirilir. Aşağıdaki en iyi uygulamaları oluşturma ve hello StorSimple konaktaki birimleri biçimlendirme önerilir.

* Hızlı biçimlendirme tüm StorSimple birimlerde gerçekleştirin.
* Bir StorSimple biriminin biçimlendirme sırasında 64 KB ayırma birimi boyutu (Avustralya) kullanın (varsayılan değer 4 KB). Merhaba 64 KB Avustralya ortak StorSimple iş yükleri ve diğer iş yükleri için şirket içinde yapılır testlerine dayanır.
* Ne zaman hello StorSimple sanal bir iSCSI sunucusu olarak yapılandırılmış dizi kullanarak kullanmayın Dağıtılmış birimler veya dinamik diskleri bu birimleri veya diskleri StorSimple tarafından desteklenmez.

#### <a name="share-access"></a>Paylaşım erişimi
Sanal dizinin dosya sunucunuzda paylaşımları oluştururken, aşağıdaki yönergeleri izleyin:

* Bir paylaşımı oluştururken, tek bir kullanıcı yerine bir paylaşım yönetici olarak bir kullanıcı grubuna atayın.
* Merhaba paylaşımı hello paylaşımları Windows Gezgini üzerinden düzenleyerek oluşturulduktan sonra hello NTFS izinlerini yönetebilir.

#### <a name="volume-access"></a>Birim erişimi
Merhaba iSCSI birimleri, StorSimple sanal dizisinde yapılandırılırken, gerekli olan her yerde önemli toocontrol erişim sağlar. sunucuları barındıran toodetermine birimlere erişmek, oluşturun ve erişim denetimi kayıtları (ACRs) StorSimple birimleri ile ilişkilendirin.

En iyi yöntemler ACRs StorSimple birimlerini yapılandırırken aşağıdaki hello kullan:

* Her zaman en az bir ACR bir birimle ilişkilendirin.

* Birden fazla ACR tooa birim atarken hello birim Burada, aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişilebilir bir biçimde gösterilmez emin olun. Birden çok ACRs tooa birim atanmışsa, bir uyarı iletisi, tooreview yapılandırmanızı açılır.

### <a name="data-security-and-encryption"></a>Veri güvenliği ve şifreleme
StorSimple sanal dizinizi hello gizlilik ve veri bütünlüğünü sağlamak veri güvenlik ve şifreleme özelliklere sahiptir. Bu özellikler kullanırken, bu en iyi uygulamaları izlemeniz önerilir: 

* Sanal dizinin toohello buluttan Hello veri gönderilmeden önce bir bulut depolama şifreleme anahtarı toogenerate AES 256 şifreleme tanımlayın. Verilerinizi ile şifrelenmiş toobegin ise bu anahtar gerekli değildir. Merhaba anahtar oluşturulabilir ve anahtar yönetimi sistemi kullanarak güvenli kalmasını [Azure anahtar kasası](../key-vault/key-vault-whatis.md).
* Merhaba StorSimple Yöneticisi hizmeti üzerinden Hello depolama hesabı yapılandırma yaptığınızda hello SSL modu toocreate etkinleştirdiğinizden emin StorSimple cihazı ile Merhaba arasındaki ağ iletişimi için güvenli bir kanal bulut.
* (Erişerek hello Azure depolama hizmeti), depolama hesaplarınıza üretme hello tuşları tooaccount herhangi temelinde Yöneticiler değiştirilen hello listesi tooaccess düzenli olarak değiştirir.
* Sanal dizinizi verileri sıkıştırılır ve tooAzure gönderilmeden önce yinelenenleri kaldırılmış. Merhaba yinelenen verileri kaldırma rol hizmetini Windows Server ana bilgisayarında kullanmanızı öneririz yok.

## <a name="operational-best-practices"></a>İşletimsel en iyi uygulamalar
Merhaba işletimsel en iyi yöntemler hello günlük yönetim veya hello sanal dizinin işlemi sırasında izlenmesi gereken yönergelerdir. Bu yöntemler yedeklemeler, bir yedekleme kümesi, bir yük devri gerçekleştirmek, devre dışı bırakma ve silme hello dizi, izleme sistem kullanımı ve sistem durumu, geri alma gibi belirli yönetim görevleri kapsar ve virüs çalıştıran sanal dizinizi tarar.

### <a name="backups"></a>Yedeklemeler
Sanal dizinizi Hello verileri iki yolla toohello bulut yedeklenen, varsayılan otomatik 22:30 veya el ile talep üzerine yedekleme aracılığıyla tüm aygıt hello başlatma günlük yedekleme. Varsayılan olarak, hello cihaz üzerinde bulunan tüm hello verilerin günlük bulut anlık görüntüleri otomatik olarak oluşturur. Daha fazla bilgi için çok Git[StorSimple sanal dizinizi yedekleme](storsimple-virtual-array-backup.md).

Merhaba sıklığı ve bekletme hello varsayılan yedekleme ile ilişkili değiştirilemez, ancak hangi hello günlük yedeklemeler her gün başlatılan hello zaman yapılandırabilirsiniz. Otomatik yedeklemeler hello için Hello başlangıç saati yapılandırırken, öneririz:

* Yedeklemeleriniz için yoğun olmayan saatler zamanlayın. Yedekleme başlangıç zamanı çok sayıda konak g/ç ile çakıştığı değil.
* El ile talep üzerine yedekleme aygıtı yük devretme veya önceki toohello bakım penceresi, sanal dizinizi tooprotect hello verileri tooperform planlarken başlatır.

### <a name="restore"></a>Geri Yükleme
İki şekilde ayarlanmış bir yedekten geri yükleyebilirsiniz: tooanother birimi veya paylaşımı geri yükleyin veya (yalnızca dosya sunucusu olarak yapılandırılmış bir sanal dizisinde kullanılabilir) bir öğe düzeyinde kurtarma gerçekleştirin. Öğe düzeyinde kurtarma hello StorSimple cihazında toodo tüm hello paylaşımları bulut yedeğini dosya ve klasörlerin ayrıntılı bir kurtarma sağlar. Daha fazla bilgi için çok Git[bir yedekten geri yükleme](storsimple-virtual-array-clone.md).

Bir geri yükleme gerçekleştirirken aklınızda yönergeleri izleyerek hello tutun:

* StorSimple sanal dizinizi yerinde geri yükleme işlemlerini desteklemiyor. Ancak bu yedeğe olabilir iki adımlı bir işlem tarafından elde: hello sanal alan dizi ve tooanother biriminin/paylaşımını geri yükleme yapın.
* Yerel bir birimden geri yüklerken göz hello Restore Koru uzun süren bir işlem olacaktır. Merhaba Birim hızlı bir şekilde çevrimiçi duruma ancak hello veri hello arka planda hydrated toobe devam eder.
* Merhaba birim türü kalır aynı hello geri yükleme işlemi sırasında hello. Katmanlı birim geri tooanother katmanlı birim ve yerel olarak sabitlenmiş birim tooanother yerel olarak sabitlenmiş birim.
* Ne zaman hello geri yükleme işi başarısız olursa bir birim veya bir yedekleme kümesi paylaşımından toorestore çalışırken, bir hedef birim veya paylaşım hala hello portalda oluşturulabilir. Bu kullanılmayan hedef birimde silin veya bu öğesinden kaynaklanan gelecekteki sorunlar hello portal toominimize içinde paylaşmak önemlidir.

### <a name="failover-and-disaster-recovery"></a>Yük devretme ve olağanüstü durum kurtarma
Cihaz yük devretme toomigrate verir verilerinizden bir *kaynak* hello datacenter tooanother aygıtı *hedef* aygıt bulunan hello aynı veya farklı bir coğrafi konum. Merhaba aygıt yük devretme hello tüm cihaz için olduğunu. Yük devretme sırasında hello bulut verilerini hello kaynak cihaz için sahipliği toothat hello hedef aygıt değiştirir.

Yalnızca Yük devretme tooanother sanal dizinin hello tarafından aynı yönetilen yapabilecekleriniz, StorSimple sanal dizinin için StorSimple Yöneticisi hizmeti. Bir yük devretme tooan 8000 serisi aygıtı veya (Merhaba bir hello kaynak cihaz için)'den farklı bir StorSimple Yöneticisi hizmet yöneten bir dizi izin verilmiyor. Merhaba yük devretme hakkında önemli noktalar hakkında daha fazla toolearn Git çok[hello aygıt yük devretme için Önkoşullar](storsimple-virtual-array-failover-dr.md).

Bir başarısız üzerinden sanal dizinizi gerçekleştirirken, hello aşağıdakileri göz önünde bulundurun:

* Planlanmış bir yük devretme için önerilen en iyi uygulamadır tootake tüm hello birimleri/paylaşımları çevrimdışı önceki tooinitiating hello yük devretme olur. Tootake hello birimleri/paylaşımlarında çevrimdışı hello ilk barındırmak ve ardından bu sanal Cihazınızda çevrimdışına hello işletim sistemine özgü yönergeleri izleyin.
* Bir dosya sunucusu olağanüstü durum kurtarma için (DR), paylaşım izinleri hello hello kaynağı aynı etki alanında otomatik olarak çözülen hello hedef aygıt toohello katılma öneririz. Yalnızca hello yük devretme tooa hedef aygıtı hello aynı etki alanında bu sürümde desteklenmiyor.
* Merhaba DR başarıyla tamamlandıktan sonra hello kaynak cihaz otomatik olarak silinir. Merhaba aygıt artık kullanılabilir olsa da, hello ana bilgisayar sisteminde sağlanan hello sanal makine hala kaynakları tüketilmesine neden olabilir. Herhangi bir ücret tahakkuk öğesinden, ana bilgisayar sistemi tooprevent bu sanal makineyi Sil öneririz.
* Merhaba yük devretme başarısız olsa bile Not **hello verileri her zaman güvenli hello bulutta**. Hangi hello yük devretme başarıyla tamamlanmadı üç senaryo aşağıdaki hello göz önünde bulundurun:
  
  * Merhaba ilk aşamaları hello DR ön denetimleri zaman gerçekleştirilir gibi hello yük devretme, bir hata oluştu. Bu durumda, hedef Cihazınızı hala kullanılabilir. Merhaba hello Yük Devretmesini deneyebilirsiniz aynı hedef aygıt.
  * Merhaba gerçek yük devretme işlemi sırasında bir hata oluştu. Bu durumda, hello hedef aygıta kullanılamaz olarak işaretlenmiş. Sağlamak ve başka bir hedef sanal dizi yapılandırmak ve yük devretme için kullanmanız gerekir.
  * Merhaba yük devretme hangi hello kaynak aygıt silindi aşağıdaki tamamlandı ancak hello hedef aygıt sorunları vardır ve herhangi bir veri erişemez. Hello veriler hello bulutta hala güvenli ve kolay bir başka sanal dizi oluşturma ve hello DR için bir hedef cihaz olarak kullanılarak alınabilir.

### <a name="deactivate"></a>Devre dışı bırakma
StorSimple sanal dizinin devre dışı bıraktığınızda, hello bağlantı hello karşılık gelen StorSimple Yöneticisi hizmeti ile Merhaba aygıt arasında sever. Devre dışı bırakma olan bir **kalıcı** işlemi ve geri alınamaz. Devre dışı bırakılmış bir aygıt ile Merhaba StorSimple Yöneticisi hizmeti yeniden kaydedilemedi. Daha fazla bilgi için çok Git[devre dışı bırakın ve StorSimple sanal dizinizi silme](storsimple-virtual-array-deactivate-and-delete-device.md).

Sanal dizinizi devre dışı bırakırken aklınızda en iyi uygulamaları izleyerek hello tutun:

* Tüm hello veri önceki toodeactivating sanal cihazı bir bulut anlık görüntüsünü. Sanal bir dizi devre dışı bıraktığınızda, tüm hello yerel cihaz verileri kaybolur. Bir bulut anlık daha sonraki bir aşamada toorecover veri izin verir.
* StorSimple sanal dizinin devre dışı bırakmadan önce toostop emin olun veya istemciler ve bu cihazda bağımlı konakları silin.
* Böylece ücretler tahakkuk değil artık kullanıyorsanız devre dışı bırakılmış bir aygıtı silme.

### <a name="monitoring"></a>İzleme
StorSimple sanal dizinizi sürekli sağlam durumda olup tooensure toomonitor ihtiyacınız hello dizi ve Uyarıları da dahil olmak üzere hello sistemden bilgi aldığından emin olmak. toomonitor genel sistem durumu hello sanal dizinin, en iyi uygulamaları izleyerek uygulama hello hello:

* İzleme tootrack hello disk kullanımı, sanal dizinin veri diski yanı sıra hello işletim sistemi diski yapılandırın. Hyper-V çalıştıran, sanallaştırma konakları System Center Virtual Machine Manager (SCVMM) ve System Center Operations Manager (SCOM) toomonitor bir birleşimini kullanabilirsiniz.
* E-posta bildirimleri sanal dizinin toosend uyarılarınızı belirli kullanım düzeylerinde yapılandırın.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Dizin araması ve virüs uygulamaları tarama
StorSimple sanal dizinin hello yerel katmanı toohello Microsoft Azure bulut verilerinden otomatik olarak katmanı. Bir uygulama dizin araması veya bir virüs taraması gibi StorSimple üzerinde depolanan kullanılan tooscan hello verileri olduğunda hello bulut verilerini değil erişilen alıp toohello yerel katmanı geri çekilen olduğunu tootake dikkatli gerekir.

En iyi yöntemler hello dizin arama veya virüs taraması sanal dizinizi yapılandırırken aşağıdaki hello uygulamak öneririz:

* Otomatik olarak yapılandırılan tam tarama işlemleri devre dışı bırakın.
* Katmanlı birimler için hello dizin arama veya virüs taraması uygulama tooperform artımlı tarama yapılandırın. Bu, yalnızca hello yeni veriler büyük olasılıkla hello yerel katmanda bulunan tarama. Katmanlı toohello bulut hello veri artımlı bir işlem sırasında erişilebilir değil.
* Doğru arama filtreleri hello ve böylece dosya yalnızca hedeflenen hello türlerini taranan ayarları yapılandırıldığından emin olun. Örneğin, resim dosyaları (JPEG, GIF ve TIFF) ve çizimler mühendislik hello artımlı veya tam dizini yeniden oluşturma sırasında taranmalıdır değil.

Dizin oluşturma işlemi Windows kullanıyorsanız, aşağıdaki yönergeleri izleyin:

* Merhaba dizin sık sık yeniden toobe gerekiyorsa hello buluttan büyük miktarlarda verinin (TBs) çeker gibi hello Windows Dizin Oluşturucu katmanlı birimler için kullanmayın. Merhaba dizinini yeniden oluşturmayı tüm dosya türlerini tooindex içeriklerini almak.
* Bu yalnızca hello yerel katmanlarda toobuild hello dizini (Merhaba bulut veri değil erişilir) verilerine erişir gibi dizin oluşturma işlemi yerel olarak sabitlenmiş birimler için Windows hello kullanın.

### <a name="byte-range-locking"></a>Bayt aralığı kilitleme
Uygulamaları hello dosyaları içinde belirtilen bayt aralığı kilitleyebilirsiniz. Bayt aralığı kilitleme tooyour StorSimple yazma hello uygulamalarda etkinse, ardından katmanlama sanal dizinizi çalışmaz. Merhaba katmanlama toowork erişilen hello dosyaların tüm alanları kilidi olması gerekir. Sanal dizinizi katmanlı birimlerin bayt aralığı kilitleme desteklenmiyor.

Önerilen önlemleri tooalleviate bayt aralığı kilitleme içerir:

* Uygulama mantığınızın kilitleme bayt aralığı kapatın.
* Kullanım yerel olarak sabitlenmiş birimler (yerine katmanlı) bu uygulamayla ilişkili hello veriler için. Yerel olarak sabitlenmiş birimlerin hello bulutunu katmanı değil.
* Kullanarak yerel olarak birimler bayt aralığı kilitleme etkin sabitlenmiş zaman hello geri yükleme tamamlanmadan önce hello birim çevrimiçi gelebilir. Bu gibi durumlarda hello geri yükleme toobe için tam beklemeniz gerekir.

## <a name="multiple-arrays"></a>Birden çok diziler
Birden çok sanal dizisi böylece hello aygıt hello performansını etkileyen hello bulut sığdırmaya veri büyüyen bir çalışma kümesi için dağıtılan toobe tooaccount gerekebilir. Merhaba çalışma kümesi büyüdükçe bu gibi durumlarda, en iyi tooscale cihazlarda desteklenir. Bu hello şirket içi veri merkezinde eklenen bir veya daha fazla aygıtları toobe gerektirir. Merhaba aygıtlar eklerken, olabilir:

* Bölünmüş hello geçerli veri kümesi.
* Yeni iş yükleri toonew aygıtlara dağıtın.
* Birden çok sanal dizileri dağıtma, yük dengeleyici gelen öneririz açısından, hello dizi farklı hiper yönetici ana bilgisayarlara dağıtın.
* (Dosya sunucusu veya bir iSCSI sunucu olarak yapılandırıldığında) birden çok sanal diziler bir dağıtılmış dosya sistemi Namespace içinde dağıtılabilir. Ayrıntılı adımlar için çok Git[dağıtılmış dosya sistemi Namespace çözümüyle karma bulut depolama Dağıtım Kılavuzu](https://www.microsoft.com/download/details.aspx?id=45507). Dağıtılmış dosya sistemi çoğaltma, şu anda hello sanal dizinin ile kullanım için önerilmez. 

## <a name="see-also"></a>Ayrıca bkz.
Nasıl çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-virtual-array-manager-service-administration.md) hello StorSimple Yöneticisi hizmeti aracılığıyla.


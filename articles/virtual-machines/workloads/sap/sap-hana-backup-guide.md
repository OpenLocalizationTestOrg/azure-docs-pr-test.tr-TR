---
title: "SAP HANA için Azure sanal makineler üzerinde aaaBackup Kılavuzu | Microsoft Docs"
description: "SAP HANA için yedekleme kılavuz SAP HANA için iki ana yedekleme olasılık, Azure sanal makinelerde sağlar."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Azure Sanal Makineler’de SAP HANA için yedekleme kılavuzu

## <a name="getting-started"></a>Başlarken

SAP HANA Azure sanal makinelerde çalışan yedekleme Kılavuzu Hello yalnızca Azure özel konular anlatmaktadır. Genel SAP HANA yedekleme ilgili öğeler için hello SAP HANA belgelerine bakın (bkz _SAP HANA yedekleme belgelerine_ bu makalenin ilerisinde yer).

iki ana yedekleme olasılıklarını SAP HANA Azure sanal makinelerinde bu makalenin Hello odak açıktır:

- HANA yedekleme toohello dosya sistemi içinde bir Azure Linux sanal makine (bkz [SAP HANA Azure yedekleme dosya düzeyinde](sap-hana-backup-file-level.md))
- HANA yedekleme tabanlı depolama anlık görüntüleri hello Azure storage blobu anlık görüntü özelliği kullanılarak el ile veya Azure yedekleme hizmeti üzerinde (bkz [tabanlı depolama anlık görüntü SAP HANA yedeklemeyi](sap-hana-backup-storage-snapshots.md))

SAP HANA yedekleme üçüncü taraf yedekleme araçları toointegrate SAP HANA ile doğrudan veren API sunar. (Bu hello bu kılavuz kapsamında değil.) SAP HANA kullanılabilir sağ bu API artık temel Azure Backup hizmeti ile doğrudan hiçbir tümleştirilmesi yoktur.

SAP HANA resmi olarak desteklenen GS5 Azure VM türüne ek kısıtlama tooOLAP iş yükleri ile tek örnek olarak (bkz [sertifikalı Iaas platformları Bul](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) hello SAP Web sitesinde). Bu makalede, SAP HANA kullanılabilir hale azure'da için yeni sunumu olarak güncelleştirilir.

Ayrıca SAP HANA karma çözümünü mevcut değil SAP HANA fiziksel sunucularda sanallaştırılmamış çalıştığı azure'da. Ancak, bu SAP HANA Azure yedekleme Kılavuzu SAP HANA çalıştığı bir Azure VM'de, çalışan değil SAP HANA saf bir Azure ortamı kapsayan &quot;büyük örnekleri.&quot; Bkz: [SAP HANA (büyük örnekler) genel bakış ve Azure ile ilgili mimari](hana-overview-architecture.md) Bu yedekleme çözümü hakkında daha fazla bilgi için &quot;büyük örnekleri&quot; depolama anlık görüntü tabanlı.

Azure üzerinde desteklenen SAP ürünler hakkında genel bilgiler bulunabilir [SAP Not 1928533](https://launchpad.support.sap.com/#/notes/1928533).

Hello aşağıdaki üç rakamı şu anda yerel Azure özelliklerini kullanarak SAP HANA yedekleme seçeneklerini hello genel bir bakış sağlar ve ayrıca üç olası gelecekteki yedekleme senaryoları gösterir. Merhaba ilgili makaleler [SAP HANA Azure yedekleme dosya düzeyinde](sap-hana-backup-file-level.md) ve [tabanlı depolama anlık görüntü SAP HANA yedeklemeyi](sap-hana-backup-storage-snapshots.md) Bu seçenekler için SAP boyutu ve performans konuları dahil olmak üzere daha ayrıntılı açıklanır Çoklu terabayt boyutu olan HANA yedeklemeler.

![Bu şekilde hello geçerli VM durumunu kaydetmek için iki olasılık gösterilmektedir](media/sap-hana-backup-guide/image001.png)

Bu şekilde hello geçerli VM durumunu, VM diskleri el ile anlık görüntüsünü veya Azure Backup hizmeti üzerinden kaydetme hello olasılığını gösterilmektedir. Bu yaklaşım, bir belirlemeden #39; ile t toomanage SAP HANA yedeklemeler vardır. Merhaba hello disk anlık görüntü senaryonun dosya sistemi tutarlılığı ve bir uygulamayla tutarlı disk durumu iştir. Merhaba tutarlılık konu hello bölümünde tartışılır _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_ bu makalenin ilerisinde yer. Özellikleri ve Azure Backup hizmeti kısıtlamalarını tooSAP HANA yedeklemeler de bu makalenin sonraki bölümlerinde açıklanan ilgili.

![Bu şekilde hello VM içinde yedek dosya SAP HANA ayırdığınız için seçenekleri gösterilmektedir.](media/sap-hana-backup-guide/image002.png)

Bu şekilde bir SAP HANA dosya yedekleme hello VM içinde alma ve sonra onu HANA yedekleme dosyaları farklı araçlarla başka bir yerde depolamak için seçenekler gösterilmektedir. Anlık görüntü tabanlı bir yedekleme çözümü daha uzun bir HANA Yedekleme yapmayı gerektirir, ancak bütünlük ve tutarlılık ilgili avantajları vardır. Bu makalenin sonraki bölümlerinde daha ayrıntılı bilgi sağlanır.

![Bu şekilde olası bir gelecekteki SAP HANA yedekleme senaryo gösterilmektedir](media/sap-hana-backup-guide/image003.png)

Bu şekilde olası bir gelecekteki SAP HANA yedekleme senaryosu gösterilmiştir. SAP HANA ikincil bir çoğaltma yedek almak izin veriliyorsa, yedekleme stratejilerini için ek seçenekler eklersiniz. Şu anda olası değil hello SAP HANA Wiki tooa postasına göre:

_&quot;Bu, olası tootake yedeklemeler hello ikincil tarafında mi?_

_Hayır, şu anda yalnızca verileri alabilir ve günlük yedeklemelerine hello birincil tarafındaki. Otomatik günlük yedekleme etkinse devralma toohello ikincil yan sonra hello günlüğü yedeklemeleri otomatik olarak var. yazılır.&quot;_

## <a name="sap-resources-for-hana-backup"></a>SAP HANA yedekleme için kaynaklar

### <a name="sap-hana-backup-documentation"></a>SAP HANA yedekleme belgeleri

- [Giriş tooSAP HANA Yönetim](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Yedekleme ve kurtarma stratejisini planlama](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [HANA ABAP DBACOCKPIT kullanarak yedeklemeyi zamanlama](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Veri yedeklemeleri zamanlamanın (SAP HANA Pilot)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- SAP HANA hakkında SSS yedekleme [SAP Not 1642148](https://launchpad.support.sap.com/#/notes/1642148)
- SAP HANA veritabanına ve depolama anlık görüntüleri hakkında SSS [SAP Not 2039883](https://launchpad.support.sap.com/#/notes/2039883)
- Yedekleme ve kurtarma için uygun ağ dosya sistemleri [SAP Not 1820529](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Neden HANA yedekleme SAP?

Azure depolama alanı kullanılabilirliği ve güvenilirliği hello kutusu dışında sağlar (bkz [giriş tooMicrosoft Azure Storage](../../../storage/common/storage-introduction.md) Azure storage hakkında daha fazla bilgi için).

Hello için minimum &quot;yedekleme&quot; toorely hello Azure SLA, tutma hello üzerinde Azure VHD'ler ekli toohello SAP HANA sunucusundaki VM SAP HANA veri ve günlük dosyaları olduğu. Bu yaklaşım, VM hataları, ancak değil potansiyel hasarı toohello SAP HANA veri ve günlük dosyalarını veya veri veya dosyaları yanlışlıkla silme gibi mantıksal hataları kapsar. Yedeklemeler de uyumluluğu veya yasal nedenlerle için gereklidir. Kısacası, gerçek her zaman bir gereksinimi SAP HANA yedeklemeler için.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Nasıl tooverify doğruluk SAP HANA yedekleme
Depolama anlık görüntüleri kullanarak, bir test geri yükleme farklı bir sistem üzerinde çalışan önerilir. Bu yaklaşım, bir yedekleme beklendiği gibi yedekleme ve geri yükleme iş için doğru ve iç işlemleri olduğunu şekilde tooensure sağlar. Bu önemli bir durumdayken hurdle şirket içi, gerekli kaynakları geçici olarak bu amaçla sağlayarak çok daha kolay tooaccomplish hello bulutta değil.

Göz önünde, basit bir geri yükleme yapmaya devam ve HANA çalışır durumda olup olmadığı denetleniyor ve çalıştıran yeterli değil. İdeal olarak, aşağıdakilerden bir tabloyu tutarlılık denetimi toobe geri hello veritabanı yolunda olduğundan emin çalıştırmanız gerekir. SAP HANA sunar tutarlılık denetimleri açıklanan çeşitli türlerde [SAP Not 1977584](https://launchpad.support.sap.com/#/notes/1977584).

Merhaba tablo tutarlılık denetimi hakkında bilgi de bulunabilir hello SAP Web sitesinde bulunan [tablo ve Katalog tutarlılık denetimleri](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Standart dosya yedeklemeler için bir test geri yükleme gerekli değildir. Hangi yedekleme geri yükleme için kullanılabilir toocheck Yardım iki SAP HANA araç vardır: hdbbackupdiag ve hdbbackupcheck. Bkz: [el ile denetimi olup olmadığını bir kurtarma mümkün olduğundan](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) Bu araçlar hakkında daha fazla bilgi için.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Artıları ve eksileri HANA yedekleme depolama anlık görüntü karşılaştırması

SAP belirlemeden #39; t verin tercih tooeither HANA yedekleme depolama anlık görüntü karşılaştırması. Böylece bir hello durum ve kullanılabilir depolama teknolojisi bağlı olarak hangi toouse belirleyebilir kendi Artıları ve eksileri, listeler (bkz [planlama bilgisayarınızı yedekleme ve kurtarma stratejisini](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

Üzerinde Azure, Azure blob anlık görüntü özelliği mevcut değil & #39 hello hello olgu unutmayın; dosya sistemi tutarlılığı garanti t (bkz [PowerShell ile kullanma blob anlık görüntüleri](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Merhaba sonraki bölümde _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_, bu özellik ile ilgili bazı hususlar anlatılmaktadır.

Ayrıca, bu makalede anlatıldığı gibi sık blob anlık görüntüleri ile çalışırken, fatura etkileri hello toounderstand varsa: [anlama nasıl anlık görüntüleri tahakkuk ücretleri](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— bu olmayan &#39; Azure kullanarak olarak olarak belirgin t sanal diskler.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığı

Dosya sistemi ve uygulama tutarlılığı bir karmaşık depolama anlık görüntüleri alırken bir sorundur. Merhaba en kolay yolu tooavoid sorunları SAP HANA aşağı tooshut olması ve hatta belki de hello tüm sanal makine. Bir kapanma demo veya prototip veya geliştirme sistemi ortak olabilir, ancak bir üretim sistem için bir seçenek değil.

Azure üzerinde sahip tookeep Azure blob anlık görüntü özelliği mevcut değil & #39 hello unutmayın; dosya sistemi tutarlılığı garanti t. Var olduğu sürece yalnızca tek bir sanal disk dahil edilen ancak hello kullanarak SAP HANA özelliği, anlık görüntü düzgün çalışır. Ancak bile tek bir diske sahip, ek öğelere toobe kullanıma sahip. [SAP Not 2039883](https://launchpad.support.sap.com/#/notes/2039883) SAP HANA yedeklemeler depolama anlık görüntüleri aracılığıyla hakkında önemli bilgiler vardır. Merhaba XFS dosya sistemi ile bunun gerekli toorun olduğunu, örneğin, değinmektedir **xfs\_Dondur** tooguarantee tutarlılık anlık görüntü depolama başlatmadan önce (bkz [xfs\_freeze(8) - Linux adam Sayfa](https://linux.die.net/man/8/xfs_freeze) hakkında ayrıntılı bilgi için **xfs\_Dondur**).

Merhaba konu tutarlılık daha zor olduğu tek bir dosya sistemi birden çok disk/birim yayılan bir durumda olur. Örneğin, mdadm veya LVM kullanarak ve bölümlemesine tarafından. Merhaba SAP durumları bahsedilen Not:

_&quot;Ancak SAP HANA veri birim başına bir depolama anlık görüntü oluşturulurken hello depolama sistemi tooguarantee g/ç tutarlılık olduğunu aklınızda bulundurun, yani atomik bir işlem olarak bir SAP HANA hizmete özgü veriler biriminin anlık görüntüsünün alınması olmalıdır.&quot;_

Dört Azure sanal diskler yayılan bir XFS dosya sistemi varsayıldığında, hello aşağıdaki adımlar hello HANA veri alanını temsil tutarlı bir anlık görüntü sağlar:

- HANA anlık görüntü hazırlama
- Merhaba dosya sistemi donmasına (örneğin, **xfs\_Dondur**)
- Azure üzerinde tüm gerekli blob anlık görüntülerini oluşturma
- Merhaba dosya sistemi Çöz
- Merhaba HANA anlık görüntü onaylayın

Tüm durumlarda toobe hangi dosya sistemi olsun hello güvenli tarafında yukarıda toouse hello yordamda önerilir. Veya tek bir disk veya mdadm veya birden çok disklere LVM üzerinden şeritleme ise.

Önemli tooconfirm hello HANA anlık görüntüsüdür. Son toohello &quot;kopyalama yazarken,&quot; SAP HANA bu sırada ek disk alanı yok gerekebilir modu anlık görüntü hazırlayın. &#39; hello SAP HANA anlık görüntü onaylandıktan kadar s de mümkün değildir toostart yeni yedeklemeler.

Azure Backup hizmeti Azure VM uzantıları tootake hello dosya sistemi tutarlılığı care of kullanır. Bu VM uzantıları, tek başına kullanım için kullanılamaz. Hala toomanage SAP HANA tutarlılık sahip. Merhaba ilgili makaleye bakın [SAP HANA Azure Backup dosya düzeyinde](sap-hana-backup-file-level.md) daha fazla bilgi için.

### <a name="sap-hana-backup-scheduling-strategy"></a>SAP HANA Yedekleme Zamanlama stratejisi

Merhaba SAP HANA makale [planlama bilgisayarınızı yedekleme ve kurtarma stratejisini](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) durumları temel bir plan toodo yedekler:

- (Günlük) anlık görüntü depolama
- Dosya veya bacint biçimi (haftada bir kez) kullanarak tam yedekleme
- Otomatik günlük yedekleri

İsteğe bağlı olarak, bir depolama anlık görüntülerini kullanmadan tamamen gidebilir; Artımlı ya da fark yedeklemeler gibi HANA değişim yedeklemeleri yerini (bakın [değişim yedeklemeleri](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Merhaba HANA Yönetim Kılavuzu bir örnek listesi sağlar. Bu, bir SAP HANA tooa belirli noktası yedeklemeleri dizisini aşağıdaki hello kullanarak sürede kurtarmak önerir:

1. Tam yedekleme
2. Değişiklik yedeklemesi
3. Artımlı Yedekleme 1
4. Artımlı yedekleme 2
5. Günlük yedekleri

Toowhen ve belirli bir yedekleme türü ne sıklıkta olacağını olarak bir tam zamanlama ile ilgili olası toogive genel bir kural değil — çok müşteriye özgü ve kaç tane veri değişikliklerini hello sistemde ortaya bağlıdır. Bir temel genel rehberlik görülebilir, SAP taraftan toomake bir tam HANA yedekleme haftada bir kez önerilir.
İlgili günlük yedeklerini hello SAP HANA belgelerine bakın [günlük yedeklerini](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP de önerir hello yedekleme kataloğu tookeep, bazı temizlik yapılması sonsuz büyüyen buradan (bkz [yedekleme kataloğu ve yedekleme depolama için Housekeeping](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>SAP HANA yapılandırma dosyaları

Merhaba SSS bölümünde belirtildiği gibi [SAP Not 1642148](https://launchpad.support.sap.com/#/notes/1642148), hello SAP HANA yapılandırma dosyaları standart HANA yedeklemenin bir parçası değil. Bunlar gerekli toorestore bir sistem değildir. Merhaba HANA yapılandırma el ile Merhaba geri yüklendikten sonra değiştirilemedi. Bir istersiniz durumda tooget hello aynı özel yapılandırma hello geri yükleme işlemi sırasında gerekli tooback hello HANA yapılandırma dosyalarını ayrı olarak öyledir.

Standart HANA yedeklemeler kullanacaksanız tooa ayrılmış HANA yedek dosya sistemi, bir ayrıca Kopyala hello yapılandırma dosyaları toohello aynı yedekleme dosya sistemi ve her şeyi birlikte toohello son bir depolama hedefi gibi kopyalama seyrek erişimli blob depolama.

### <a name="sap-hana-cockpit"></a>SAP HANA yönetim ekranı

SAP HANA Pilot izleme ve SAP HANA bir tarayıcı yoluyla yönetme hello olanağı sunar. SAP HANA yedeklemeler işlenmesini de sağlar ve bu nedenle bir alternatif tooSAP HANA Studio ve ABAP DBACOCKPIT olarak kullanılabilir (bkz [SAP HANA Pilot](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) daha fazla bilgi için).

![Bu şekilde hello SAP HANA Pilot veritabanı yönetim ekran gösterilmektedir](media/sap-hana-backup-guide/image004.png)

Bu şekil gösterir hello SAP HANA Pilot veritabanı yönetim ekran ve sol hello hello yedekleme kutucuğu. Görme hello yedekleme döşeme için oturum açma hesabı uygun kullanıcı izinleri gerektirir.

![SAP HANA Pilot yedeklemeler devam eden sağlarken izlenebilir](media/sap-hana-backup-guide/image005.png)

Yedeklemeler, devam eden ve bu işlem tamamlandıktan sonra tüm hello yedekleme ayrıntıları kullanılabilir olsa da, SAP HANA Pilot izlenebilir.

![Bir Azure SLES 12 VM Gnome masaüstüyle Firefox kullanma örneği](media/sap-hana-backup-guide/image006.png)

Merhaba önceki ekran görüntüleri bir Azure Windows sanal makineden yapıldı. Bunu bir Azure SLES 12 VM Gnome masaüstüyle Firefox kullanarak bir örnektir. Bu, SAP HANA Pilot hello seçeneği toodefine SAP HANA yedekleme zamanlamaları gösterir. Biri de görüldüğü gibi hello yedekleme dosyaları için tarih/saat öneki olarak önerir. SAP HANA Studio'da hello varsayılan önektir &quot;tam\_veri\_yedekleme&quot; bir tam dosya yedeğini yaparken. Benzersiz bir önek kullanılması önerilir.

### <a name="sap-hana-backup-encryption"></a>SAP HANA yedek şifreleme

SAP HANA veri ve günlük şifrelenmesini sağlar. SAP HANA veri ve günlük şifrelenmezse hello yedeklemeler de şifrelenmez. Bu toohello müşteri toouse bazı üçüncü taraf çözümü tooencrypt hello SAP HANA yedeklemeler biçimidir. Bkz: [veri ve günlük birimi şifreleme](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind SAP HANA şifreleme hakkında daha fazla bilgi.

Microsoft Azure üzerinde bir müşteri hello Iaas VM şifreleme özelliği tooencrypt kullanabilirsiniz. Örneğin, bir özel veri diskleri ekli toohello VM, SAP HANA yedeklemeler kullanılan toostore olan, sonra bu diskler kopyalarını kullanabilirsiniz.

Azure Backup hizmeti, şifrelenen VM'ler/disklere işleyebilir (bkz [tooback yedeklemek ve geri yükleme Azure yedekleme ile sanal makineleri nasıl şifrelenmiş](../../../backup/backup-azure-vms-encryption.md)).

Başka bir seçenek toomaintain hello SAP HANA VM ve şifreleme olmadan, disklerini ve şifreleme etkinleştirildiğini bir depolama hesabında hello SAP HANA yedekleme dosyalarının depolanacağı (bkz [bekleyen veri için Azure depolama hizmeti şifrelemesi](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Test Kurulumu

### <a name="test-virtual-machine-on-azure"></a>Azure üzerinde test sanal makinesi

SAP HANA yüklemenin Azure GS5 VM'deki yedekleme/geri yükleme testleri aşağıdaki hello için kullanıldı.

![Bu şekilde hello hello HANA test VM için Azure portalına genel bakış parçası gösterilmektedir](media/sap-hana-backup-guide/image007.png)

Bu şekilde hello hello HANA test VM için Azure portalına genel bakış parçası gösterilmektedir.

### <a name="test-backup-size"></a>Test yedekleme boyutu

![Bu şekil HANA Studio'da hello yedekleme konsolundan alındığı ve hello HANA dizini sunucusunun 229 GB hello yedekleme dosyası boyutunu gösterir](media/sap-hana-backup-guide/image008.png)

Sahte bir tablo ile veri tooget toplam veri yedekleme boyutu 200 GB tooderive gerçekçi performans verilerinin doldurulmuş. Hello şekil HANA Studio'da hello yedekleme konsolundan alındığı ve hello HANA dizini sunucusunun 229 GB hello yedekleme dosyası boyutunu gösterir. Merhaba varsayılan yedekleme önek SAP HANA Studio'da "COMPLETE_DATA_BACKUP" Merhaba testler için kullanıldı. Gerçek üretim sistemlerinde, daha kullanışlı bir önek tanımlanması gerekir. SAP HANA Pilot tarih önerir.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Test aracı toocopy doğrudan tooAzure depolama dosyaları

hem hedef hem de bu desteklediğinden doğrudan tooAzure blob depolama veya Azure dosya paylaşımları hello blobxfer aracı kullanılan tootransfer SAP HANA yedek dosyaları kolayca Otomasyon betikleri tooits komut satırı arabirimi nedeniyle içine tümleştirilebilir. Merhaba blobxfer aracı edinilebilir [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Yedekleme boyutu tahmin test

Bu önemli tooestimate hello yedekleme SAP HANA boyutudur. Bu tahmin, yedekleme dosyalarının sayısı için hello max yedek dosya boyutu tanımlayarak tooimprove performans yardımcı olan bir dosya kopyalama sırasında son tooparallelism. (Bu ayrıntıları bu makalenin sonraki bölümlerinde açıklanmıştır.) Gereken bir ayrıca karar toodo tam bir yedekleme veya delta (artımlı ya da fark) yedekleme.

Neyse ki, hello yedekleme dosyalarının hello boyutunu tahminleri basit bir SQL deyimi yoktur: **seçin \* M gelen\_yedekleme\_BOYUTU\_TAHMİNLER** (bkz: [ Tahmin hello alanı, hello dosya sistemi için bir veri yedekleme](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![Bu SQL deyimini Hello çıktısını hemen hemen gerçek boyutunu diskteki hello tam veri yedek hello eşleşir](media/sap-hana-backup-guide/image009.png)

Merhaba test sisteminde, bu SQL deyimini hello çıktısını hemen hemen gerçek boyutunu diskteki hello tam veri yedek hello eşleşir.

### <a name="test-hana-backup-file-size"></a>Test HANA yedek dosya boyutu

![bir toorestrict hello en fazla dosya boyutunu HANA yedekleme dosyalarını Hello HANA Studio yedekleme Konsolu sağlar](media/sap-hana-backup-guide/image010.png)

Merhaba HANA Studio yedekleme konsolu bir toorestrict hello en fazla dosya boyutunu HANA yedek dosyaları sağlar. Merhaba örnek ortamında, bu özellik bir 230 GB yedekleme dosyası yerine birden çok daha küçük yedekleme dosyalarını olası tooget kolaylaştırır. Daha küçük dosya boyutu performans üzerinde önemli bir etkisi vardır (Merhaba ilgili makaleye bakın [SAP HANA Azure Backup dosya düzeyinde](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Özet

Merhaba tabloları aşağıdaki avantajları ve dezavantajları çözümleri tooback Azure sanal makinelerde çalışan bir SAP HANA veritabanından Göster hello test sonuçlarına dayanarak.

**SAP HANA toohello dosya sistemi ve kopyalama geri yedekleme daha sonra toohello son yedekleme hedefi dosyaları**

|Çözüm                                           |Uzmanları                                 |Simgeler                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|VM disklerde HANA yedekleri koru                      |Hiçbir ek Yönetimi çalışmalarını     |Yerel VM disk alanını eats           |
|Blobxfer aracı toocopy yedekleme dosyalarını tooblob depolama |Paralellik toocopy birden çok dosya, seçim toouse cool blob depolama | Ek aracı Bakım ve özel komut dosyaları | 
|Powershell veya CLI yoluyla BLOB kopyalama                    |Gerekirse, hiçbir ek araç Azure Powershell veya CLI gerçekleştirilebilir |el ile işlem müşteri tootake komut dosyası oluşturma ve geri yükleme için kopyalanan BLOB yönetim care of sahiptir.|
|Kopya tooNFS paylaşımı                                  |Diğer VM hello HANA sunucudaki etkisi olmadan yedekleme dosyaları sonrası işlenmesi|Yavaş kopyalama işlemi|
|Blobxfer kopyalama tooAzure dosya hizmeti                |Yerel VM disk alanı yemek değil|Hiçbir doğrudan HANA yedekleme, boyutu kısıtlaması şu anda 5 TB adresindeki dosya paylaşımının tarafından destek yazma|
|Azure Yedekleme aracısı                                 | Tercih edilen bir çözüm olacaktır         | Şu anda kullanılamıyor Linux    |



**Yedekleme SAP HANA depolama anlık görüntü tabanlı**

|Çözüm                                           |Uzmanları                                 |Simgeler                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Azure yedekleme hizmeti                               | Blob anlık görüntü tabanlı VM yedeklemeyi sağlar | Dosya düzeyinde geri yükleme kullanmadığınızda, yeni bir SAP HANA lisans anahtar hello gerek gelir hello geri yükleme işlemi için yeni bir VM hello oluşturulmasını gerektirir|
|El ile blob anlık görüntüler                              | VM kimliği değiştirmeden esneklik toocreate ve geri yükleme belirli VM diskleri hello|Merhaba müşteri tarafından yapılan toobe sahip el ile çalışma|

## <a name="next-steps"></a>Sonraki adımlar
* [SAP HANA Azure yedekleme dosya düzeyinde](sap-hana-backup-file-level.md) hello dosya tabanlı yedekleme seçeneği açıklar.
* [SAP HANA yedekleme depolama anlık görüntü tabanlı](sap-hana-backup-storage-snapshots.md) hello depolama anlık görüntü tabanlı yedekleme seçeneği açıklar.
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).

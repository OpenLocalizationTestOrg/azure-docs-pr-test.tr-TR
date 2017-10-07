---
title: "SAP HANA azure'da (büyük örnekler) üzerinde SAP HANA aaaInstall | Microsoft Docs"
description: "Nasıl tooinstall SAP HANA SAP HANA azure'da (büyük örneği) üzerinde."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Nasıl tooinstall ve Azure üzerinde SAP HANA (büyük örnekler) yapılandırma

Bu kılavuzu okumadan önce bazı önemli tanımları tooknow aşağıda verilmiştir. İçinde [SAP HANA (büyük örnekler) genel bakış ve Azure ile ilgili mimari](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) ile HANA büyük örneği birimlerin farklı iki sınıf gösterdiğimizi:

- S72, S72m, S144, S144m, S192 ve tooas hello 'ı sınıf türü' adlandırdığımız S192m SKU.
- S384, S384m, S384xm, S576, S768 ve adlandırdığımız S960 tooas SKU ' Type II class' hello.

Merhaba sınıfı tanımlayıcısı hello HANA büyük belge tooeventually başvuran toodifferent özellikleri ve gereksinimleri HANA büyük örneği SKU'larında tabanlı örneği genelinde kullanılan giderek toobe ' dir.

Sık kullandığınız diğer tanımların şunlardır:
- **Büyük örneği damga:** SAP HANA TDI olan bir donanım altyapı yığını sertifikalı ve ayrılmış Azure içindeki toorun SAP HANA örnekleri.
- **SAP HANA azure'da (büyük örnekler):** Azure toorun HANA örneklerinde SAP HANA büyük örneği Damgalar farklı Azure bölgelerinde dağıtılmış donanım sertifikalı TDI hello teklif resmi adı. Merhaba ilgili terim **HANA büyük örneği** azure'da (büyük örnekler) kısaltması SAP HANA ve yaygın olarak kullanılan bu teknik dağıtım kılavuzu.


SAP HANA Hello yükleme sizin sorumluluğunuzdadır ve Azure (büyük örnekler) sunucuda yeni bir SAP HANA Aktarmadan sonra hello etkinlik başlatabilirsiniz. Ve sonra Azure VNet(s) ve hello HANA büyük örneği birimleri arasında hello bağlantısı kuruldu. 

> [!Note]
> SAP ilke SAP HANA hello yüklemesini tooperform SAP HANA yüklemeleri sertifikalı bir kişi tarafından gerçekleştirilmesi gerekir. Merhaba sertifikalı SAP teknolojisi ilişkilendirmek incelemesi, SAP HANA yükleme sertifika incelemesi, geçmiş bir kişi, veya bir SAP Sertifikalı Sistem Tümleştirici (SI).

Yeniden, özellikle tooinstall HANA 2.0 planlarken denetlemek [SAP destek Not #2235581 - SAP HANA: desteklenen işletim sistemleri](https://launchpad.support.sap.com/#/notes/2235581/E) sırada toomake OS desteklenir, hello hello SAP HANA ile yayın emin tooinstall karar. HANA 2.0 kısıtlı daha için desteklenen işletim Sistemleri HANA 1.0 için desteklenen işletim sistemi hello bu hello unutmayın. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Merhaba HANA büyük örneği birimlerinin aldıktan sonra ilk adımlar

**İlk adım** HANA büyük örnek alındıktan sonra hello ve erişim ve bağlantı toohello örnekleri kurulmuş, işletim sistemi sağlayıcınızla hello örneğinin tooregister hello işletim sistemi ise. Bu adım, SUSE Linux işletim sistemi Azure VM'deki dağıtılan toohave ihtiyacınız SUSE SMT örneğindeki kaydetme dahildir. Merhaba HANA büyük örneği birim toothis SMT örneği (Bu belgede daha sonra bakın) bağlanabilir. Veya, RedHat OS hello Red Hat Abonelik Yöneticisi'ni tooconnect için gereksinim duyduğunuz kayıtlı toobe gerekiyor. Bkz: de açıklamalar bu [belge](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bu adım ayrıca gerekli toobe mümkün toopatch hello OS bağlıdır. Merhaba hello müşteri içinde sorumluluğundadır bir görev. SUSE, belgeleri tooinstall bulmak ve SMT yapılandırma [burada](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**İkinci adım** toocheck yeni düzeltme ekleri ve düzeltmeleri hello belirli işletim sistemi sürüm/sürüm değil. Merhaba HANA büyük örneği Hello düzeltme eki düzeyi hello son durumuna olup olmadığını denetleyin. Zamanlama Microsoft dağıtabilmeniz için işletim sistemi düzeltme eki/serbest bırakır ve değişiklik toohello görüntüye bağlı olarak, burada hello en son düzeltme eklerinin dahil edilmemiş olabilir durumlar olabilir. Bu nedenle, zorunlu düzeltme ekleri güvenlik, işlevselliği, kullanılabilirlik ve performans için ilgili bu sırada hello belirli Linux satıcı tarafından yayımlanan ve uygulanan toobe gerek olup olmadığını HANA büyük örneği birimi üzerinde toocheck aldıktan sonra bir adımdır.

**Üçüncü adım** hello çıkışı toocheck ilgili SAP notları yükleme ve SAP HANA hello belirli işletim sistemi sürüm/sürümünde yapılandırma içindir. Toochanging öneriler ya da değişiklikleri tooSAP son notlar veya tek tek yükleme senaryoları bağımlı yapılandırmaları, Microsoft her zaman olmayacak mümkün toohave kusursuz şekilde yapılandırılmış bir HANA büyük örneği birim. Bu nedenle onu sizin için tooread hello SAP notları ilgili tooSAP HANA tam Linux sürüm üzerinde bir müşteri olarak zorunludur. Ayrıca hello işletim sistemi/sürümü gerekli hello yapılandırmalarını denetleyin ve hello yapılandırma ayarlarının uygulanacağı zaten yapılmadı burada.

Özel şu parametreler ve sonunda göre ayarlanmış hello denetleyin:

- NET.Core.rmem_max 16777216 =
- NET.Core.wmem_max 16777216 =
- NET.Core.rmem_default 16777216 =
- NET.Core.wmem_default 16777216 =
- NET.Core.optmem_max 16777216 =
- NET.ipv4.tcp_rmem 65536 16777216 16777216 =
- NET.ipv4.tcp_wmem 65536 16777216 16777216 =

RHEL 7.2 SLES12 SP1 ile başlayarak, bu parametreler hello /etc/sysctl.d dizindeki yapılandırma dosyasında ayarlanmalıdır. Örneğin, bir yapılandırma dosyası hello adı 91-NetApp-HANA.conf ile oluşturulması gerekir. Eski SLES ve RHEL sürümler için bu parametre kümesi in/etc/sysctl.conf olması gerekir.

İçin tüm RHEL serbest bırakır ve SLES12 ile başlayarak, hello 
- sunrpc.tcp_slot_table_entries = 128

parametre in/etc/modprobe.d/sunrpc-local.conf ayarlamanız gerekir. Hello dosya mevcut değilse, önce girdiyi izleyen hello ekleyerek oluşturulmalıdır: 
- Seçenekler sunrpc tcp_max_slot_table_entries = 128

**Dördüncü adım** toocheck hello sistem zamanı, HANA büyük örneği birimi. Merhaba örnekleri HANA büyük örneği damgası bulunan hello Azure bölgesi hello hello konumunu temsil eden bir sistem saat dilimi ile dağıtılır. Ücretsiz toochange hello sistem saati veya sahip olduğunuz hello örneklerinin saat dilimi var. Bunun yapılması ve Kiracı daha fazla örneği sıralama, yeni örnekleri teslim hello tooadapt hello saat dilimini gereksinim hazırlıklı olun. Microsoft operations hello sistem saat dilimi hello örnekleriyle hello handover sonra ayarladığınız hiçbir Öngörüler vardır. Bu nedenle yeni dağıtılan örnekleri hello aynı ayarlanmamış olabilir bir değiştirdiğiniz için hello gibi bir saat dilimi. Sonuç olarak, müşteri toocheck olarak sizin sorumluluğunuzdadır olduğu ve gerekirse karmalayan hello örnekler hello saat dilimini uyarlayabilirsiniz. 

**Beşinci adım** toocheck etc/hosts değil. Hello Kanatlar karmalayan gibi farklı amaçlar için (sonraki bölüme bakın) atanmış farklı IP adreslerini sahiptirler. Merhaba etc/hosts dosyasını denetleyin. Birimler mevcut bir kiracı burada eklenen durumlarda toohave vb./ana bilgisayarlar ile daha önce teslim edilen sistemlerin hello IP adreslerinin doğru yönetilmesini yeni dağıtılan hello sistemlerinin beklemeyen. Bu nedenle üzerinde müşteri toocheck hello ayarlarının doğru olduğunu, yeni dağıtılan bir örneği etkileşim ve daha önce Dağıtılmış birimler kiracınızda hello adlarını çözmek. 

## <a name="networking"></a>Ağ
Azure Vnet'ler tasarlanması ve bu belgelerinde açıklandığı gibi bu sanal ağlar toohello HANA büyük örnekleri bağlanma hello önerileri uyguladığınız varsayılmaktadır:

- [SAP HANA (büyük örneği) genel bakış ve Azure üzerinde mimarisi](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Bazı ayrıntılar toomention hello tek birim hello ağla ilgili değer vardır. Her HANA büyük örneği birim tootwo veya hello biriminin üç NIC bağlantı noktalarını atanmış olan iki veya üç IP adresleri ile birlikte gelir. Üç IP adresi HANA genişleme yapılandırmaları ve hello HANA sistem çoğaltma senaryo kullanılır. Merhaba IP adreslerinden biri atanan hello biriminin nıc'dir hello hello açıklanan sunucu IP havuzu dışında toohello [SAP HANA (büyük örneği) genel bakış ve Azure ile ilgili mimari](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

iki IP adresi atanmış birimleriyle Hello dağıtım gibi görünmelidir:

- eth0.xx hello tooMicrosoft gönderilen sunucu IP havuzu adres aralığı dışında atanmış bir IP adresi olmalıdır. Bu IP adresi/etc/hosts hello işletim sistemi, içinde sürdürmek için kullanılır.
- eth1.xx iletişim tooNFS için kullanılan bir IP adresi olmalıdır. Bu nedenle, bu adresleri yapmak **değil** vb./ana sipariş tooallow örneği tooinstance trafiğinin hello Kiracı içinde tutulur toobe gerekir.

Dağıtım durumlarda HANA sistem çoğaltma veya HANA genişleme, dikey yapılandırması atanan iki IP adreslerine sahip uygun değil. Azure Hizmet Yönetimi tooget üzerinde SAP HANA yalnızca atanmış iki IP adreslerine sahip olmasına ve bu tür bir yapılandırma toodeploy isteyen başvurursanız, üçüncü bir IP adresi üçüncü VLAN atanmış. Üç NIC noktalarına atanan üç IP adreslerine sahip olmasına HANA büyük örneği birimleri için hello aşağıdaki kullanım kurallar geçerlidir:

- eth0.xx hello tooMicrosoft gönderilen sunucu IP havuzu adres aralığı dışında atanmış bir IP adresi olmalıdır. Bu nedenle bu IP adresi/etc/hosts hello işletim sistemi, içinde sürdürmek için kullanılacak işaretçi yok.
- eth1.xx iletişim tooNFS depolama için kullanılan atanmış bir IP adresi olmalıdır. Bu nedenle bu tür adresleri etc/hosts saklanması gereken değil.
- eth2.xx özel olarak saklanır. etc/hosts hello farklı örnekleri arasında iletişim için kullanılan toobe olmalıdır. Bu adresler ayrıca HANA hello düğümler arası yapılandırmasını kullanan IP adresleri olarak genişleme HANA yapılandırmalarında tutulan toobe gereksinim hello IP adresleri olacaktır.



## <a name="storage"></a>Depolama

Merhaba SAP HANA azure'da (büyük örnekler) için depolama düzeni SAP HANA kılavuz çizgileri açıklandığı gibi önerilen SAP aracılığıyla Azure Hizmet Yönetimi tarafından yapılandırılan [SAP HANA depolama gereksinimleri](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) teknik incelemesi. Merhaba farklı birimler kaba boyutlarını farklı HANA büyük örnekleri SKU belgelenen hello Hello [SAP HANA (büyük örneği) genel bakış ve Azure ile ilgili mimari](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Merhaba adlandırma kuralları hello depolama birimleri, aşağıdaki tablonun hello listelenmiştir:

| Depolama kullanımı | Takma adı | Birim adı | 
| --- | --- | ---|
| HANA veri | /hana/Data/SID/mnt0000<m> | Depolama IP: / hana_data_SID_mnt00001_tenant_vol |
| HANA günlük | /hana/log/SID/mnt0000<m> | Depolama IP: / hana_log_SID_mnt00001_tenant_vol |
| HANA günlük yedeği | /hana/log/Backups | Depolama IP: / hana_log_backups_SID_mnt00001_tenant_vol |
| Paylaşılan HANA | /hana/Shared/SID | Depolama IP: / hana_shared_SID_mnt00001_tenant_vol/paylaşılan |
| usr/sap | /usr/SAP/SID | Depolama IP: / hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Burada SID hello HANA örneğinin sistem kimliği = 

Ve Kiracı işlemlerinin iç numaralandırması Kiracı dağıtırken =.

Gördüğünüz gibi paylaşılan HANA ve usr/sap paylaşımı hello aynı birim. Merhaba terminolojisi hello bağlama, hello sistem Kimliğini hello bağlama numarası yanı sıra hello HANA örnekleri içermez. Büyütme dağıtımlarında yalnızca var. mnt00001 gibi bir bağlama Genişleme dağıtımı'nda farklı sayıda başlatmalar görür ancak çalışan ve ana düğümlerin vardır. Merhaba genişleme ortam, veri, günlük için günlük yedekleme birimleri hello genişletme yapılandırma paylaşılan ve ekli tooeach düğümünde ' dir. Birden çok SAP örneği çalıştıran yapılandırmaları için birimleri farklı bir dizi oluşturulur ve ekli toohello HAN büyük örneği birimdir.

Merhaba incelemeyi okuyun ve HANA büyük örneği birim arayın gibi hello birimleri HANA/verileri yerine geniştir disk birimi ile gelir ve toplu günlük/HANA/yedekleme sahibiz unutmayın. neden biz hello HANA/veri çok büyük boyutlu hello hello depolama anlık görüntüleri, bir müşteri olarak kullandığınız için sunuyoruz aynı disk birimi hello nedenidir. Merhaba, gerçekleştirmeniz, daha fazla depolama anlık görüntüleri daha fazla alan atanan depolama birimlerinizi anlık görüntülerini tarafından mı tüketiliyor hello anlamına gelir. Merhaba günlük/HANA/yedekleme birimi değil düşünce toobe hello tooput veritabanı yedeklemeleri birimdir. Merhaba HANA işlem günlüğü yedeklemeleri için yedekleme birimi olarak kullanılan boyutlu toobe olur. Gelecekte hello depolama sürümleri self servis size daha fazla bu özel birim toohave hedeflediğini sık anlık görüntüleri anlık görüntüsünü alın. Ve toooption bileşenini hello HANA büyük örneği altyapısı tarafından sağlanan hello olağanüstü durum kurtarma işlevi için üzerinde isterse ile daha fazla çoğaltma toohello olağanüstü durum kurtarma sitesi sık. Ayrıntıları görmek [SAP HANA (büyük örnekler) yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure ile ilgili](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 

Ayrıca toohello depolama sağlanan, 1 TB artışlarla ek depolama kapasitesi satın alabilirsiniz. Bu ek depolama alanı yeni birimleri tooa HANA büyük örnekleri eklenebilir.

SAP HANA Azure Hizmet Yönetimi onboarding işlemi sırasında hello müşteri bir kullanıcı kimliği (UID) ve Grup Kimliği (GID) için hello sidadm kullanıcı ve sapsys grubunu belirtir (örn: 1000,500) hello SAP HANA sistemi yüklemesi sırasında aynı bu değerler kullanılır gereklidir. Bir birim birden çok HANA örneklerinde toodeploy istediğiniz gibi birden çok kümesi birimlerin (her örneği için bir küme) alın. Sonuç olarak, dağıtım sırasında toodefine gerekir:

- Merhaba hello (sidadm dışında türetilmiş) farklı HANA örnekleri SID'si.
- Merhaba farklı HANA örneklerinin bellek boyutları. Merhaba bellek boyutu örnekleri başına her tek tek birim kümesi hello hello birimlerin boyutunu tanımladığından.

Bağlama seçenekleri aşağıdaki hello tüm takılı birimleri için yapılandırılmış olan depolama sağlayıcısı önerilerine göre (önyükleme LUN hariç):

- NFS rw sürücüleri = 4, sabit, timeo 600, rsize = 1048576, wsize = 1048576, giriş, noatime, kilitleme 0 0

Bu bağlama noktaları/etc/fstab gösterildiği hello grafik aşağıdaki gibi yapılandırılır:

![bağlanan birimlerin HANA büyük örneği biriminde fstab](./media/hana-installation/image1_fstab.PNG)

Merhaba komutu df -h S72m HANA büyük örneği biriminde Hello çıktısı gibi görünür:

![bağlanan birimlerin HANA büyük örneği biriminde fstab](./media/hana-installation/image2_df_output.PNG)


Merhaba depolama denetleyicisi ve hello büyük örneği Damgalar düğümler eşitlenmiş tooNTP sunucularıdır. Sizinle hello SAP HANA Azure (büyük örnekler) birimleri ve Azure Vm'leri üzerinde bir NTP sunucusuna karşı eşitleme, olmamalıdır hiçbir önemli zaman kayması oluşmasını hello altyapısı ve Azure veya büyük örnek Damgalar hello işlem birimleri arasında.

Sipariş toooptimize altında kullanılan SAP HANA toohello depolama, SAP HANA yapılandırma parametreleri aşağıdaki hello ayarlamanız gerekir:

- max_parallel_io_requests 128
- üzerinde async_read_submit
- üzerinde async_write_submit_active
- Tüm async_write_submit_blocks
 
TooSPS12 yukarı SAP HANA 1.0 sürümleri için bu parametreler hello SAP HANA veritabanına hello yüklemesi sırasında açıklandığı gibi ayarlanabilir [SAP Not #2267798 - hello SAP HANA veritabanı yapılandırması](https://launchpad.support.sap.com/#/notes/2267798)

Merhaba parametreleri hello SAP HANA veritabanına yüklendikten sonra hello hdbparam framework kullanarak da yapılandırabilirsiniz. 

SAP HANA 2.0 ile Merhaba hdbparam framework kullanım dışıdır. Sonuç olarak hello parametreleri SQL komutlarını kullanarak ayarlanmalıdır. Ayrıntılar için bkz [SAP Not #2399079: HANA 2'deki hdbparam ortadan kaldırılması](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>İşletim sistemi

İşletim sistemi görüntüsü teslim hello takas alanı too2 GB toohello göre ayarlanmış [SAP destek Not #1999997 - SSS: SAP HANA bellek](https://launchpad.support.sap.com/#/notes/1999997/E). Tüm farklı istenen ihtiyaçlarını toobe sizin tarafınızdan bir müşteri olarak ayarlamak.

[SUSE Linux Enterprise Server 12 SP1 SAP uygulamaları için](https://www.suse.com/products/sles-for-sap/hana) hello dağıtım Linux SAP HANA Azure (büyük örnekler) üzerinde yüklü olduğu. Bu belirli dağıtım SAP özgü özellikleri sağlayan &quot;hello kutusu dışında&quot; (SAP SLES üzerinde etkili bir şekilde çalıştırmak için önceden ayarlanmış parametreleri de dahil olmak üzere).

Bkz: [Kaynak Kitaplığı/tanıtım yazıları](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) hello SUSE Web sitesinde ve [SUSE üzerinde SAP](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) üzerinde birkaç kullanışlı kaynaklar toodeploying SAP HANA SLES (dahil olmak üzere hello Kurulum üzerinde ilgili SAP topluluk ağ (SCN) hello Yüksek kullanılabilirlik, güvenlik sağlamlaştırma belirli tooSAP işlemleri ve daha fazla).

SUSE ilgili bağlantıların üzerinde ek ve kullanışlı SAP:

- [SAP HANA SUSE Linux sitesinde](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [En iyi yöntemi için SAP: Enqueue çoğaltma – SUSE Linux Enterprise 12 üzerinde SAP NetWeaver](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).
- [ClamSAP – SAP SLES virüs koruması](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (SLES 12 SAP uygulamaları dahil).

Destek Notes uygun tooimplementing SAP HANA SLES 12 üzerinde SAP:

- [SAP destek Not #1944799 – SLES işletim sistemi yüklemesi için SAP HANA yönergeleri](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).
- [SAP destek Not #2205917 – SAP HANA DB önerilen SLES 12 SAP uygulamaları için işletim sistemi ayarlarını](https://launchpad.support.sap.com/#/notes/2205917/E).
- [SAP destek Not #1984787 – SUSE Linux Enterprise Server 12: Yükleme notları](https://launchpad.support.sap.com/#/notes/1984787).
- [SAP destek Not #171356 – SAP yazılım Linux'ta: genel bilgiler](https://launchpad.support.sap.com/#/notes/1984787).
- [SAP destek Not #1391070 – Linux UUID çözümleri](https://launchpad.support.sap.com/#/notes/1391070).

[Red Hat Enterprise Linux SAP HANA için](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) HANA büyük örneklerinde SAP HANA çalıştırmak için başka bir teklifidir. RHEL 6.7 ve 7.2 sürümlerinde kullanılabilir. 

Red Hat üzerinde ek ve kullanışlı SAP bağlantıları ile ilgili:
- [SAP HANA üzerinde Red Hat Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

Destek Notes uygun tooimplementing SAP HANA Red Hat üzerinde SAP:

- [SAP destek Not #2009879 - SAP HANA yönergeleri Red Hat Enterprise Linux (RHEL) işletim sistemi için](https://launchpad.support.sap.com/#/notes/2009879/E).
- [SAP destek Not #2292690 - SAP HANA DB: RHEL 7 için önerilen işletim sistemi ayarlarını](https://launchpad.support.sap.com/#/notes/2292690).
- [SAP destek Not #2247020 - SAP HANA DB: Önerilen işletim sistemi ayarlarını RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).
- [SAP destek Not #1391070 – Linux UUID çözümleri](https://launchpad.support.sap.com/#/notes/1391070).
- [SAP destek Not #2228351 - Linux: SAP HANA veritabanına SP'ler 11 düzeltme 110 (veya üstü) RHEL 6 veya SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [SAP destek Not #2397039 - SSS: RHEL üzerinde SAP](https://launchpad.support.sap.com/#/notes/2397039).
- [SAP destek Not #1496410 - Red Hat Enterprise Linux 6.x: yükleme ve yükseltme](https://launchpad.support.sap.com/#/notes/1496410).
- [SAP destek Not #2002167 - Red Hat Enterprise Linux 7.x: yükleme ve yükseltme](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Zaman eşitleme

Merhaba oluşturan çeşitli bileşenler hello SAP sistem için SAP NetWeaver mimarisi hello üzerinde oluşturulan SAP uygulamalar üzerinde saat farklılıklarını duyarlıdır. SAP ABAP kısa dökümleri ile ZDATE hello hata başlığı\_büyük\_zaman\_fark olan büyük olasılıkla alışılmış, bu kısa dökümleri hello farklı sunucular veya VM'ler sistem saati çok fazla ara drifting atandıklarında gibi.

SAP HANA azure'da (büyük örnekler), Azure içermiyor &#39; bitti zaman eşitleme için t hello büyük örneği Damgalar toohello işlem birimleri uygulayın. Bir sistem & #39 Azure sağlar gibi bu eşitleme yerel Azure Vm'lerde SAP uygulamaları çalıştırmak için geçerli değildir; s zaman düzgün eşitlenir. Sonuç olarak, Azure Vm'lerinde çalışan SAP uygulama sunucuları tarafından kullanılan ve SAP HANA hello sunucu ayarlanmalıdır ayrı birer veritabanı HANA büyük örneklerinde çalışan örnekleri. Büyük örneği Damgalar Hello depolama altyapısında NTP sunucuları ile eşitlenen saattir.

## <a name="setting-up-smt-server-for-suse-linux"></a>SUSE Linux için SMT sunucusu kurma
SAP HANA büyük örnekleri doğrudan bağlantı toohello Internet yok. Bu nedenle basit işlem tooregister böyle bir birimle hello işletim sistemi sağlayıcısı ve toodownload değil ve düzeltme eklerini uygulayın. SUSE Linux Hello durumda tooset SMT sunucusu Azure VM'deki bir çözüm olabilir. Hello Azure VM gerekiyor ancak toobe HANA büyük örneği bağlı toohello olan bir Azure VNet içinde barındırılan. Bu tür bir SMT sunucusuyla, hello HANA büyük örneği birim kaydetmek ve düzeltme eklerini indirmek. 

SUSE sağlar içeren büyük bir kılavuzun kendi [SLES 12 SP2 için Abonelik Yönetim Aracı](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Merhaba görev HANA büyük örneği için uygun bir SMT sunucusu hello yüklemesi için daha fazla önkoşulu olarak ihtiyacınız:

- Bağlı toohello HANA büyük örneği ER devresini olan bir Azure VNet.
- Bir kuruluşla ilişkili bir SUSE hesabı. Merhaba kuruluş bazı geçerli SUSE abonelik toohave gerekir ancak.

### <a name="installation-of-smt-server-on-azure-vm"></a>Azure VM SMT sunucusu yükleme

Bu adımda, bir Azure VM hello SMT sunucusuna yükleyin. Merhaba ilk ölçüdür toohello toolog [SUSE Müşteri merkezi](https://scc.suse.com/)

Oturum açtığınız gibi Git tooOrganization--> kuruluş kimlik. Bu bölümde hello gerekli tooset hello SMT sunucusu kimlik bilgileri bulmanız gerekir.

Merhaba üçüncü adım tooinstall SUSE Linux VM hello Azure VNet ile aynıdır. toodeploy hello VM, Azure SLES 12 SP2 galeri görüntüsü alın. Merhaba dağıtım işlemi, bir DNS adı tanımlayın yoktur ve bu ekran görüntüsü görüldüğü gibi statik IP adresleri kullanmayın

![VM dağıtımı için SMT sunucu](./media/hana-installation/image3_vm_deployment.png)

Merhaba dağıtılan VM daha küçük bir VM olan ve hello iç IP adresi hello 10.34.1.4 Azure VNet aldı. Merhaba VM adını smtserver oluştu. Merhaba yükleme sonrasında, hello bağlantı toohello HANA büyük örneği birimlerinin denetlendi. Ad çözümlemesi nasıl organize bağımlı hello HANA büyük örneği vb./ana bilgisayarları hello Azure VM birimlerinde tooconfigure çözünürlüğü gerekebilir. Bir ek disk toohello toobe toohold hello düzeltme ekleri kullanılan geçiyor VM ekleyin. Merhaba önyükleme diski kendisi çok küçük olabilir. Gösterilen hello durumda hello disk hello ekran aşağıdaki gösterildiği gibi takılı çok/srv/www/htdocs aldı. 100 GB disk yeterli olacaktır.

![VM dağıtımı için SMT sunucu](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Toohello HANA büyük örneği birimlerinin oturum, / etc/hosts korumak ve hello toorun hello SMT sunucu hello ağ üzerinden beklenen Azure VM ulaşmak olup olmadığını denetleyin.

Bu denetimi başarıyla tamamlandıktan sonra toohello hello SMT sunucu çalışması gerektiğini Azure VM toolog gerekir. Putty toolog toohello VM kullanıyorsanız, tooexecute bash pencerenizde bu komutları dizisini gerekir:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Bu komutlar yürüttükten sonra bash tooactivate hello ayarlarınızı yeniden başlatın. Daha sonra YAST başlatın.

YAST içinde tooSoftware Bakım ve smt araması gidin. Aşağıda gösterildiği gibi tooyast2 smt otomatik olarak geçer smt seçin

![Yast SMT](./media/hana-installation/image5_smt_in_yast.PNG)


Merhaba seçimi hello smtserver yükleme için kabul etme. Bir kez yüklendikten sonra toohello SMT sunucu yapılandırması gidin ve SUSE müşteri, daha önce aldığınız merkezi hello hello kuruluş kimlik bilgilerini girin. Ayrıca, Azure VM ana bilgisayar adı hello SMT sunucu URL'si girin. Bu örnekte, https://smtserver hello sonraki grafiklerde görüntülenen kaydedildi.

![SMT sunucusunun yapılandırması](./media/hana-installation/image6_configuration_of_smtserver1.png)

Sonraki adım olarak, Hello bağlantı toohello SUSE Müşteri merkezi çalışır olup olmadığını tootest gerekir. Grafikler, hello tanıtım durumda, aşağıdaki hello içinde gördüğünüz gibi çalışmamış.

![Test tooSUSE Müşteri merkezi Bağlan](./media/hana-installation/image7_test_connect.png)

Merhaba SMT Kurulumu başlar, bu kez tooprovide bir veritabanı parolası gerekir. Yeni bir yükleme olduğuna göre sonraki grafik hello gösterildiği gibi bu parolayı toodefine gerekir.

![Veritabanının parolası tanımlayın](./media/hana-installation/image8_define_db_passwd.PNG)

bir sertifika oluşturulur hello sonraki etkileşim sahip olduğunuz durumdur. Sonraki gösterildiği gibi Hello iletişim kutusundan gidin ve hello adım devam etmelisiniz.

![SMT sunucu için sertifika oluşturun.](./media/hana-installation/image9_certificate_creation.PNG)

Merhaba hello yapılandırma sonunda 'Çalıştır eşitleme onay' hello adımda harcanan bazı dakika olabilir. Merhaba yükleme ve yapılandırma hello SMT sunucusunun sonra hello dizin depodaki hello bağlama noktası /srv/www/htdocs altında bulmalısınız/depodaki altında bazı alt dizinleri artı. 

Merhaba SMT sunucusu ve bu komutları ile ilgili hizmetlerini yeniden başlatın.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Paketlerin SMT sunucuya indirme

Tüm hello hizmetleri yeniden başlatılır, uygun SMT Yast kullanarak yönetim paketlerinde seçin hello. Merhaba paket seçimi hello HANA büyük örnek sunucusunun hello işletim sistemi görüntüsü ve SLES sürüm hello veya hello VM çalışan hello SMT server sürümü üzerinde değil bağlıdır. Merhaba seçim ekranına örneği aşağıda verilmiştir.

![Paketleri seçin](./media/hana-installation/image10_select_packages.PNG)

Merhaba paket seçimi bittiğinde, toostart hello ilk kopyasını ayarladığınız hello select paketleri toohello SMT sunucu gerekir. Bu kopyalama hello komutu smt-aşağıda gösterildiği gibi yansıtma kullanarak hello kabuğunda tetiklenir


![Paketleri tooSMT sunucu yükle](./media/hana-installation/image11_download_packages.PNG)

Yukarıda gördüğünüz gibi hello paketleri hello bağlama noktası /srv/www/htdocs altında oluşturulan hello dizinleri kopyalanır. Bu işlem biraz zaman alabilir. Seçtiğiniz kaç paketin bağımlı, onu tooone saat veya daha fazla ele geçirebilir.
Bu işlem bitirdiğinde, toomove toohello SMT istemci kurulumu gerekir. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Merhaba SMT istemci HANA büyük örneği birimlerdeki ayarlama

Merhaba istemci bu durumda hello HANA büyük örneği birimleridir. Hello SMT Sunucusu Kurulumu hello betik clientSetup4SMT.sh hello Azure VM kopyalanır. Bu komut dosyası tooconnect tooyour SMT sunucu istediğiniz HANA büyük örneği birimi toohello kopyalayın. Merhaba betik hello -h seçeneğiyle başlatın ve parametre hello SMT sunucunuzun adını verin. Bu örnek smtserver.

![SMT istemcisini yapılandırma](./media/hana-installation/image12_configure_client.PNG)

Burada hello hello istemci tarafından hello sunucusundan hello sertifikayı yükleme başarılı oldu, ancak aşağıda gösterildiği gibi hello kaydı başarısız oldu bir senaryo olabilir.

![İstemci kaydı başarısız](./media/hana-installation/image13_registration_failed.PNG)

Merhaba kayıt başarısız olursa bu okuma [SUSE destek belge](https://www.suse.com/de-de/support/kb/doc/?id=7006024) ve orada açıklanan başlangıç adımları yürütün.

> [!IMPORTANT] 
> Sunucu adı olarak tooprovide hello hello tam etki alanı adı olmadan bu servis talebi smtserver hello VM adını gerekir. Yalnızca hello VM adı çalışır. 

Bu adımları yürütülen sonra hello HANA büyük örneği biriminde komutu aşağıdaki tooexecute hello gerekir.

```
SUSEConnect –cleanup
```

> [!Note] 
> Bizim testlerinde biz her zaman bu adımından sonra birkaç dakika toowait vardı. Merhaba düzeltici önlemleri açıklanan hello SUSE makale sonra hello hemen yürütme clientSetup4SMT.sh bu hello sertifika henüz geçerli olmaz iletileri ile sona erdi. Genellikle 5-10 dakika bekleyen ve clientSetup4SMT.sh yürütme başarılı istemci yapılandırmasında sona erdi.

Merhaba SUSE makalenin hello adımları temel toofix gerekli hello sorunu içine çalıştırdıysanız, toorestart clientSetup4SMT.sh hello HANA büyük örneği biriminde yeniden gerekir. Şimdi, aşağıda gösterildiği gibi başarıyla tamamlanmalıdır.

![İstemci kaydı başarılı](./media/hana-installation/image14_finish_client_config.PNG)

Bu adımda, hello HANA büyük örneği birim tooconnect hello Azure VM yüklü hello SMT sunucusuna karşı hello SMT istemcisi yapılandırılmış. Şimdi 'zypper Yukarı' veya 'ın zypper' tooinstall OS düzeltme ekleri tooHANA büyük örnekleri alın veya ek paketler yükleyin. Merhaba SMT sunucuda önce indirilen eklerini yalnızca alabilir anlaşılır.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>SAP HANA yüklemenin HANA büyük örneklerinde örneği
Bu bölümde nasıl tooinstall SAP anlatılacaktır HANA HANA büyük örneği birim üzerinde. sahibiz hello başlangıç durumu şuna benzer:

- Microsoft tüm hello veri toodeploy sağlanan, SAP HANA büyük örneği.
- Microsoft'tan hello SAP HANA büyük örneği aldı.
- Bağlı tooyour şirket içi ağ bir Azure sanal oluşturuldu.
- Merhaba ExpressRotue hattı HANA büyük örnekleri toohello için bağlı aynı Azure sanal ağı.
- Bir atlama kutu olarak HANA büyük örnekleri için kullandığınız bir Azure VM yüklü.
- Merhaba atlama kutusunu tooyour HANA büyük örneği biriminden ve bağlanabilir emin olun.
- Tüm gerekli paketleri hello ve düzeltme ekleri yüklenmemiş denetimi.
- Merhaba SAP notlar ve hello kullanıyorsanız ve hello HANA yayın tercih hello işletim sistemi sürüm üzerinde desteklendiğinden emin yapılan işletim sistemi HANA yüklemede ilgili belgeleri okuyun.

Merhaba sonraki sıralarında gösterilen hello yükleme hello HANA yükleme paketleri toohello atlama kutusunun bu durumda bir Windows işletim sistemlerinde, hello paketleri toohello HANA büyük örneği birim hello kopyasını ve hello Kurulum hello dizisini çalıştıran VM içindir.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Merhaba SAP HANA yükleme bit indirme
Merhaba HANA büyük örneği birimleri doğrudan bağlantı toohello yoksa bu yana Internet, doğrudan yükleyemiyor hello yükleme paketleri SAP toohello HANA büyük örneği VM. tooovercome hello eksik doğrudan internet bağlantısı, hello atlama kutusunu gerekir. Merhaba paketleri toohello atlama kutusunu VM indirin.

Sipariş toodownload hello HANA yükleme paketleri içinde bir SAP S-kullanıcı veya, SAP Market tooaccess hello sağlayan başka bir kullanıcı, gerekir. Oturum açtıktan sonra bu ekranlar sırası gidin:

Çok Git[SAP hizmet Market](https://support.sap.com/en/index.html) > yazılım indir'e tıklayın > yüklemeleri ve yükseltme > göre alfabetik dizini > altında H – SAP HANA Platform Edition > SAP HANA Platform sürüm 2.0 > yükleme > indirme hello Aşağıdaki dosyaları

![HANA yükleme indirin](./media/hana-installation/image16_download_hana.PNG)

Merhaba tanıtım durumda SAP HANA 2.0 yükleme paketleri indirilir. Hello Azure atlama kutusunda VM, aşağıda gösterildiği gibi hello dizine hello kendiliğinden açılan arşivler genişletin.

![HANA yükleme Ayıkla](./media/hana-installation/image17_extract_hana.PNG)

Merhaba arşivler ayıklanır gibi hello durumda 51052030, oluşturduğunuz bir dizine hello /hana/shared birim toohello HANA büyük örneği birimine yukarıda hello ayıklama tarafından oluşturulan hello dizin kopyalayın.

> [!Important]
> Merhaba yükleme paketleri hello kök kopyalamayın veya LUN alanı sınırlıdır ve diğer işlemler tarafından kullanılan toobe gereken önyükleme.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>SAP HANA hello HANA büyük örneği biriminde yükleyin
Sipariş tooinstall SAP HANA'da, kullanıcının kök toolog de gerekir. Yalnızca kök yeterli izinleri tooinstall SAP HANA vardır.
toodo gereken hello ilk şey, üzerinden/hana paylaşılan / kopyaladığınız hello dizinindeki tooset izinleridir. tooset gibi Hello izinlerine sahip olmanız gerekir

```
chmod –R 744 <Installation bits folder>
```

SAP HANA tooinstall istiyorsanız hello grafik kullanarak Kurulum, hello HANA büyük örneklerinde yüklü gtk2 paket gereksinimlerini toobe hello. Merhaba komutuyla yüklü olup olmadığını denetleyin

```
rpm –qa | grep gtk2
```

Daha fazla adımlarda biz hello SAP HANA Kurulum hello grafik kullanıcı arabirimi ile gösteren. Sonraki adım olarak hello yükleme dizinine gidin ve HDB_LCM_LINUX_X86_64 hello alt dizinine gidin. Başlatma

```
./hdblcmgui 
```
Bu dizine dışında. Şimdi, ekranlar bir dizi nerede tooprovide hello veri hello yüklemesi için gerekli rehberlik sağlanır. Gösterilen hello durumda biz hello SAP HANA veritabanı sunucusu ve hello SAP HANA istemci bileşenlerini yüklüyorsunuz. Bu nedenle bizim 'SAP HANA veritabanına' aşağıda gösterildiği gibi seçimdir

![Yüklemede HANA seçin](./media/hana-installation/image18_hana_selection.PNG)

Merhaba sonraki ekranda, 'Yeni sistemini Yükle' hello seçeneği seçin

![Yeni yükleme HANA seçin](./media/hana-installation/image19_select_new.PNG)

Bu adımdan sonra ek olarak yüklenebilen birkaç ek bileşenler arasındaki tooselect gerek toohello SAP HANA veritabanı sunucusu.

![Ek HANA bileşenleri seçin](./media/hana-installation/image20_select_components.PNG)

Merhaba amaçla bu belgelerin hello SAP HANA istemci seçtiyseniz ve SAP HANA Studio hello. Biz de büyütme örneğinin yüklü. Bu nedenle toochoose 'Tek konak System' ihtiyacınız hello sonraki ekranda, 

![Büyütme yükleme seçin](./media/hana-installation/image21_single_host.PNG)

Merhaba sonraki ekranda, bazı veriler tooprovide gerekir

![SAP HANA SID sağlayın](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Tooprovide ihtiyacınız HANA sistem kimliği (SID) olarak aynı SID hello HANA büyük örnek dağıtım sıralı zaman Microsoft sağlandığı şekilde hello. Farklı bir SID seçme hello yükleme hello farklı birimlerde tooaccess izin sorunları nedeniyle başarısız kılar

Yükleme dizini olarak hello /hana/shared dizin kullanın. Merhaba sonraki adımda, tooprovide hello konumları hello HANA veri dosyaları ve hello HANA günlük dosyaları için gerekli


![HANA günlük konumunu belirtin](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Veri ve günlük dosyaları zaten hello Merhaba ekranında seçimi bu ekran önce seçtiğiniz SID içeren hello bağlama noktaları ile birlikte gelen birimleri hello olarak tanımlamanız gerekir. Hello SID ile uyuşmazlık varsa, daha önce Merhaba ekranında yazdığınız hello bir geri dönün ve hello hello bağlama noktalarında sahip SID toohello değerini ayarlayın.

Merhaba sonraki adımda hello ana bilgisayar adını gözden geçirin ve sonunda düzeltin. 

![Gözden geçirme ana bilgisayar adı](./media/hana-installation/image24_review_host_name.PNG)

Merhaba sonraki adımda hello HANA büyük örnek dağıtım sıralı zaman tooMicrosoft vermiş tooretrieve verileri de gerekir. 

![Sistem kullanıcısı sağlamak UID ve GID](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Tooprovide ihtiyacınız hello birim dağıtım sipariş gibi Microsoft koşuluyla aynı sistem kullanıcı kimliği ve kullanıcı grubu kimliği hello. Toogive hello çok başarısız olursa aynı kimlikleri, SAP HANA hello yükleme hello HANA büyük örneği biriminde başarısız olur.

Bu belgede görünmüyorsa, hello sonraki iki ekranları, hello SAP HANA veritabanına ve hello parçası olarak yüklenen SAP konak aracısı için kullanılan hello sapadm kullanıcı hello parola hello Sistem kullanıcısı için tooprovide hello parolası gerekir Merhaba SAP HANA veritabanı örneği.

Merhaba parola tanımladıktan sonra bir onay ekranı başlanan bir uyarıdır. Tüm hello veri listelenir ve hello yükleme işlemine devam denetleyin. Yükleme ilerleme durumu hello gibi belgeleri hello ilerleme ekranı ulaşmak

![Yükleme ilerleme durumunu denetleme](./media/hana-installation/image27_show_progress.PNG)

Hello yükleme bitirdiğinde, bir resim hello bir aşağıdaki gibi olmalıdır

![Yükleme tamamlandı](./media/hana-installation/image28_install_finished.PNG)

Bu noktada, hello SAP HANA örnek kullanım için hazır ve çalışır ve hazır olmalıdır. SAP HANA Studio'dan mümkün tooconnect tooit olmalıdır. Ayrıca hello en son düzeltme ekleri SAP HANA için denetleyin ve bu yamalar uygulama emin olun.
























































 







 





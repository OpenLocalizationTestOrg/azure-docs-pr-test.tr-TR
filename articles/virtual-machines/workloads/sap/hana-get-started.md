---
title: "Hızlı Başlangıç: Tek Örnekli SAP HANA Azure sanal makineler üzerinde el ile yükleme | Microsoft Docs"
description: "Tek Örnekli SAP HANA el ile yüklenmesi için Azure sanal makineler üzerinde Hızlı Başlangıç Kılavuzu"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Hızlı Başlangıç: Azure vm'lerinde Tek Örnekli SAP HANA el ile yükleme
## <a name="introduction"></a>Giriş
Bu kılavuzda, tek örnek SAP HANA Azure sanal makinelerde (VM'ler) SAP NetWeaver 7.5 ve SAP HANA 1.0 SP12 el ile yüklediğinizde kurmanıza yardımcı olur. SAP HANA Azure üzerinde dağıtma bu kılavuzun Hello odak noktasıdır. SAP belgelerine değiştirmez. 

>[!Note]
>Bu kılavuzda, SAP HANA dağıtımları Azure VM'ler içine açıklanmaktadır. SAP HANA HANA büyük örneği dağıtma hakkında daha fazla bilgi için bkz: [kullanarak SAP Azure sanal makinelerde (VM'ler)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, böyle bir altyapı (ıaas) temel olarak aşina olduğunuzu varsayar:
 * Nasıl toodeploy sanal makine ya da aracılığıyla sanal ağlar Azure portal veya PowerShell hello.
 * Hello Azure platformlar arası komut satırı hello seçeneği toouse JavaScript nesne gösterimi (JSON) şablonları dahil olmak üzere arabirimi (CLI).

Bu kılavuz, ayrıca aşina olduğunuzu varsayar:
* SAP HANA ve SAP NetWeaver ve nasıl tooinstall bunları şirket içi.
* Yükleme ve işletim SAP HANA ve Azure üzerinde SAP uygulama örnekleri.
* kavramlar ve yordamlar hello:
   * Azure sanal ağ planlaması ve Azure depolama alanı kullanımı dahil olmak üzere Azure üzerinde SAP dağıtımını planlama. Bkz: [SAP NetWeaver Azure Virtual Machines'de (VM'ler) - planlama ve Uygulama Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Dağıtım ilkeleri ve yolları toodeploy azure'da Vm'leri. Bkz: [SAP için Azure sanal makineler dağıtımı](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Yüksek kullanılabilirlik için SAP NetWeaver ASCS (ABAP SAP merkezi Hizmetleri), SCS (SAP merkezi hizmetlerinin) ve Azure üzerinde ERS (alındı kapatma hesaplanan). Bkz: [yüksek kullanılabilirlik için SAP NetWeaver Azure vm'lerinde](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Hakkında ayrıntılar ASCS/SCS Azure üzerinde çoklu SID yüklemesini yararlanarak içinde tooimprove verimliliği. Bkz: [SAP NetWeaver çoklu SID yapılandırması oluşturma](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Linux tabanlı sanal makineleri Azure üzerinde SAP NetWeaver çalışan kurallara göre. Bkz: [SAP NetWeaver Microsoft Azure SUSE Linux VM'ler üzerinde çalıştırılan](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Bu kılavuz, nasıl tooproperly ekleme üzerinde Azure depolama diskleri tooLinux VM'ler Linux Azure Vm'leri ve Ayrıntılar için belirli ayarları sağlar.

Şu anda, Azure sanal makineleri yalnızca SAP HANA büyütme yapılandırmaları SAP tarafından onaylandı. SAP HANA iş yükleri ile genişleme yapılandırmaları henüz desteklenmiyor. SAP HANA yüksek kullanılabilirlik için büyütme yapılandırmalarının durumlarda bkz [SAP HANA yüksek kullanılabilirlik Azure sanal makinelerde (VM'ler)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

SAP HANA örneği veya S/4HANA veya çok hızlı zamanında dağıtılan BW/4HANA sistem tooget arıyorsanız, hello kullanımını düşünmelisiniz [SAP bulut Gereci Kitaplığı](http://cal.sap.com). Örneğin, Azure üzerinde SAP CAL S/4HANA sisteminde dağıtma hakkında bulabilirsiniz [bu kılavuzda](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). Tüm toohave ihtiyacınız olan bir Azure aboneliği ve SAP bulut Gereci kitaplıkla kayıtlı bir SAP kullanıcı.

## <a name="additional-resources"></a>Ek kaynaklar
### <a name="sap-hana-backup"></a>SAP HANA yedekleme
Azure Vm'lerinde SAP HANA veritabanlarını yedekleme hakkında daha fazla bilgi için bkz:
* [SAP HANA için yedekleme Kılavuzu Azure sanal makineler üzerinde](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Dosya düzeyinde bir SAP HANA Azure yedekleme](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [SAP HANA yedekleme depolama anlık görüntü tabanlı](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP bulut Gereci kitaplığı
SAP bulut Gereci kitaplığı toodeploy S/4HANA veya BW/4HANA kullanma hakkında daha fazla bilgi için bkz: [dağıtmak SAP S/4HANA veya BW/4HANA Microsoft Azure üzerinde](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>SAP HANA desteklenen işletim sistemleri
SAP HANA desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz: [SAP destek Not #2235581 - SAP HANA: desteklenen işletim sistemleri](https://launchpad.support.sap.com/#/notes/2235581/E). Azure VM'ler, yalnızca bir alt kümesini bu işletim sistemlerini destekler. Merhaba aşağıdaki işletim sistemlerinde desteklenen toodeploy Azure üzerinde SAP HANA şunlardır: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

SAP HANA ve farklı Linux işletim sistemleri hakkında ek SAP belgeler için bkz:

* [SAP destek Not #171356 - Linux SAP yazılımı: genel bilgiler](https://launchpad.support.sap.com/#/notes/1984787)
* [Destek Not #1944799 - SLES işletim sistemi yüklemesi için SAP HANA yönergeleri SAP](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [SAP destek Not #2205917 - SAP HANA DB işletim sistemi için SLES 12 SAP uygulamaları için önerilen ayarları](https://launchpad.support.sap.com/#/notes/2205917/E)
* [SAP destek Not #1984787 - SUSE Linux Enterprise Server 12: Yükleme notları](https://launchpad.support.sap.com/#/notes/1984787)
* [SAP destek Not #1391070 - Linux UUID çözümleri](https://launchpad.support.sap.com/#/notes/1391070)
* [Destek Not #2009879 - SAP HANA yönergeleri Red Hat Enterprise Linux (RHEL) işletim sistemi için SAP](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - SAP HANA DB: RHEL 7 için önerilen işletim sistemi ayarları](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>SAP Azure'da izleme
SAP Azure'da izleme hakkında daha fazla bilgi için bkz:

* [SAP Not 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). Bu Not SAP "Gelişmiş izleme" ile Linux sanal makineleri Azure üzerinde açıklanır. 
* [SAP Not 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Bu Not Linux SAPOSCOL hakkındaki bilgiler açıklanmaktadır. 
* [SAP Not 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Bu Not Microsoft Azure üzerinde için SAP anahtar izleme ölçümleri açıklanır.

### <a name="azure-vm-types"></a>Azure VM türleri
Azure VM türleri ve iş yükü SAP desteklenen senaryolar SAP HANA ile kullanılan konusunda belgelenir [SAP sertifikalı Iaas platformları](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

SAP tarafından SAP NetWeaver için sertifikalı veya S/4HANA uygulama katmanı hello azure VM türleri konusunda belgelenir [SAP Not 1928533 - Azure SAP uygulamaları: desteklenen ürünler ve Azure VM türleri](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>SAP Linux Azure tümleştirme yalnızca Azure Resource Manager ve hello Klasik dağıtım modeli üzerinde desteklenir. 

## <a name="manual-installation-of-sap-hana"></a>SAP HANA el ile yükleme
Bu kılavuzda, nasıl toomanually yükleme SAP HANA Azure Vm'lerinde iki farklı şekilde açıklanır:

* "Veritabanı örneği Yükle" Merhaba adımda dağıtılmış NetWeaver yüklemesinin parçası olarak SAP yazılım sağlama Yöneticisi (SWPM) kullanarak
* SAP HANA Hello kullanarak veritabanı lifecycle manager aracı, HDBLCM ve NetWeaver yükleme

Ayrıca SWPM tooinstall tüm bileşenlerde (SAP HANA, hello SAP uygulama sunucusu ve hello ASCS örnek) tek tek VM, bu konuda açıklandığı gibi kullanabilirsiniz [SAP HANA blog duyuru](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Bu seçenek Bu Hızlı Başlangıç Kılavuzu'nda açıklanan değil, ancak göz önünde bulundurmalıdır sorunlardır hello hello aynı.

Yükleme başlamadan önce hello okumanızı öneririz "hazırlama Azure VM'ler SAP HANA el ile yüklenmesi için" bölümünde bu kılavuzda daha sonra. Bunun yapılması, yalnızca bir varsayılan Azure VM yapılandırması kullandığınızda oluşabilecek çeşitli temel hataları önlenmesine yardımcı olabilir.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>SAP SWPM kullandığınızda SAP HANA yükleme için anahtar adımları
SAP SWPM tooperform dağıtılmış bir SAP NetWeaver 7.5 yüklemesini kullandığınızda hello anahtar adımları el ile tek örnekli bir SAP HANA yüklemesi için bu bölümde listelenmektedir. Merhaba tek tek adımları bu kılavuzun ilerleyen bölümlerindeki ekran görüntüleri daha ayrıntılı açıklanmıştır.

1. İki test sanal makineleri içeren Azure sanal ağı oluşturun.
2. Merhaba iki Azure sanal makineleri (örneğimizde, SUSE Linux Enterprise Server (SLES) ve SLES SAP uygulamaları 12 SP1), işletim sistemleriyle toohello Azure Resource Manager modeli göre dağıtın.
3. İki Azure standart veya premium depolama diskler (örneğin, 75 GB ya da 500 GB disk) toohello uygulama sunucusu VM ekleyin.
4. Premium depolama diskleri toohello HANA DB sunucusu VM ekleyin. Ayrıntılar için bu kılavuzda daha sonra hello "Disk Kurulum" bölümüne bakın.
5. Boyutu veya üretilen iş gereksinimlerine bağlı olarak birden çok disk ekleyin ve sonra hello VM içinde hello işletim sistemi düzeyinde mantıksal birim yönetimi ya da cihazları birden çok yönetim aracı (MDADM) kullanarak şeritli birimler oluşturun.
6. XFS dosya sistemleri hello bağlı diskleri veya mantıksal birimleri oluşturun.
7. Merhaba yeni XFS dosya sistemleri hello işletim sistemi düzeyinde bağlayın. Bir dosya sistemi için tüm hello SAP yazılımı kullanın. Merhaba hello /sapmnt dizin ve yedeklemeler için diğer dosya sistemi örneğin kullanın. Merhaba SAP HANA DB sunucuda hello XFS dosya sistemleri disklerde hello premium depolama /hana ve /usr/sap olarak bağlayın. Bu işlem doldurmasını Linux Azure Vm'lerinde büyük olmayan gerekli tooprevent hello kök dosya sistemidir.
8. Merhaba/etc/hosts dosyasında hello test sanal makineleri Hello yerel IP adreslerini girin.
9. Merhaba girin **nofail** dosyasında parametresi hello/etc/fstab.
10. Kullanmakta olduğunuz toohello Linux işletim sistemi sürüm göre Linux çekirdek parametrelerini ayarlayın. Daha fazla bilgi için HANA ve hello "Çekirdek parametreleri" bölümüne bu kılavuzda ele hello uygun SAP notlarına bakın.
11. Takas alanı ekleyin.
12. İsteğe bağlı olarak, bir grafik Masaüstü hello test sanal makineleri yükleyin. Aksi takdirde uzaktan SAPinst yükleme kullanın.
13. Merhaba SAP yazılım SAP hizmet Market hello indirin.
14. Merhaba SAP ASCS örneği VM hello uygulama sunucuya yükleyin.
15. Paylaşım hello /sapmnt dizin hello arasında NFS kullanarak sanal makineleri sınayın. Merhaba uygulama sunucusu VM hello NFS sunucusudur.
16. Merhaba DB sunucuda VM SWPM kullanarak HANA, de dahil olmak üzere hello veritabanı örneğini yükleyin.
17. Merhaba uygulama sunucusuna VM Hello birincil uygulama sunucusu (PAS) yükleyin.
18. SAP Yönetim Konsolu'nu (SAP MC) başlatın. SAP GUI veya HANA Studio, örneğin bağlayın.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>HDBLCM kullandığınızda SAP HANA yükleme için anahtar adımları
SAP HDBLCM tooperform dağıtılmış bir SAP NetWeaver 7.5 yüklemesini kullandığınızda hello anahtar adımları el ile tek örnekli bir SAP HANA yüklemesi için bu bölümde listelenmektedir. Merhaba tek tek adımları ekran görüntüleri bu kılavuzda daha ayrıntılı açıklanmıştır.

1. İki test sanal makineleri içeren Azure sanal ağı oluşturun.
2. İşletim sistemleri (örneğimizde, SLES ve SLES SAP uygulamaları 12 SP1) ile iki Azure sanal makineleri dağıtmak toohello Azure Resource Manager modeli göre.
3. İki Azure standart veya premium depolama diskler (örneğin, 75 GB ya da 500 GB disk) toohello uygulama sunucusu VM ekleyin.
4. Premium depolama diskleri toohello HANA DB sunucusu VM ekleyin. Ayrıntılar için bu kılavuzda daha sonra hello "Disk Kurulum" bölümüne bakın.
5. Boyutu veya üretilen iş gereksinimlerine bağlı olarak birden çok disk ekleme ve hello VM içinde hello işletim sistemi düzeyinde mantıksal birim yönetimi ya da cihazları birden çok yönetim aracı (MDADM) kullanarak şeritli birimler oluşturabilirsiniz.
6. XFS dosya sistemleri hello bağlı diskleri veya mantıksal birimleri oluşturun.
7. Merhaba yeni XFS dosya sistemleri hello işletim sistemi düzeyinde bağlayın. Bir dosya sistemi için tüm hello SAP yazılımı kullanabilir ve kullanım hello diğeri hello /sapmnt dizin ve yedeklemeler, örneğin. Merhaba SAP HANA DB sunucuda hello XFS dosya sistemleri disklerde hello premium depolama /hana ve /usr/sap olarak bağlayın. Bu işlem gereklidir toohelp doldurmasını Linux Azure Vm'lerinde büyük değil, hello kök dosya sistemi engelleme.
8. Merhaba/etc/hosts dosyasında hello test sanal makineleri Hello yerel IP adreslerini girin.
9. Merhaba girin **nofail** dosyasında parametresi hello/etc/fstab.
10. Kullanmakta olduğunuz toohello Linux işletim sistemi sürüm göre çekirdek parametrelerini ayarlayın. Daha fazla bilgi için HANA ve hello "Çekirdek parametreleri" bölümüne bu kılavuzda ele hello uygun SAP notlarına bakın.
11. Takas alanı ekleyin.
12. İsteğe bağlı olarak, bir grafik Masaüstü hello test sanal makineleri yükleyin. Aksi takdirde uzaktan SAPinst yükleme kullanın.
13. Merhaba SAP yazılım SAP hizmet Market hello indirin.
14. Grup Kimliği 1001 hello HANA DB sunucusu VM ile sapsys, bir grup oluşturun.
15. SAP HANA HANA veritabanına Lifecycle Manager (HDBLCM) kullanarak VM hello DB sunucuya yükleyin.
16. Merhaba SAP ASCS örneği VM hello uygulama sunucuya yükleyin.
17. Paylaşım hello /sapmnt dizin hello arasında NFS kullanarak sanal makineleri sınayın. Merhaba uygulama sunucusu VM hello NFS sunucusudur.
18. Merhaba HANA DB sunucuda VM SWPM kullanarak HANA, de dahil olmak üzere hello veritabanı örneğini yükleyin.
19. Merhaba uygulama sunucusuna VM Hello birincil uygulama sunucusu (PAS) yükleyin.
20. SAP MC başlatın. SAP GUI veya HANA Studio bağlayın.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Azure VM'ler el ile bir SAP HANA yükleme için hazırlama
Bu bölüm aşağıdaki konularda hello kapsar:

* İşletim sistemi güncelleştirmeleri
* Disk Kurulumu
* Çekirdek parametreleri
* Dosya sistemleri
* Merhaba/etc/hosts dosyasını
* Merhaba/etc/fstab dosyası

### <a name="os-updates"></a>İşletim sistemi güncelleştirmeleri
Linux işletim sistemi güncelleştirmelerini ve ek yazılım yüklemeden önce düzeltmeleri denetleyin. Bir düzeltme eki yükleyerek mümkün tooavoid çağrısı toohello destek masasını olabilir.

Kullanmakta olduğunuz emin olun:
* SUSE Linux Enterprise Server SAP uygulamaları için.
* Red Hat Enterprise Linux SAP uygulamaları veya Red Hat Enterprise Linux SAP HANA için. 

Henüz yapmadıysanız, Linux aboneliğinize hello Linux satıcıdan hello işletim sistemi dağıtımı kaydedin. SUSE zaten hizmetleri içeren ve otomatik olarak kayıtlı SAP uygulamaları için işletim sistemi görüntüleri olduğuna dikkat edin.

İşte bir örnek için kullanılabilir düzeltme ekleri hello kullanarak SUSE Linux için denetleme **zypper** komutu:

 `sudo zypper list-patches`

Sorunun Hello türüne bağlı olarak, düzeltme ekleri kategorisi ve önem derecesini tarafından sınıflandırılır. Kategori için yaygın olarak kullanılan değerler şunlardır: **güvenlik**, **önerilen**, **isteğe bağlı**, **özelliği**, **belge**, veya **yast**.
Önem derecesi için yaygın olarak kullanılan değerler şunlardır: **kritik**, **önemli**, **orta**, **düşük**, veya **belirtilmemiş**.

Merhaba **zypper** komutu yalnızca hello güncelleştirmeleri için yüklü paketleri arar. Örneğin, bu komutu kullanabilirsiniz:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Merhaba parametresi ekleyebilirsiniz `--dry-run` hello sistem gerçekte güncelleştirmeden tootest hello güncelleştirme.


### <a name="disk-setup"></a>Disk Kurulumu
Merhaba kök dosya sistemi azure'da bir Linux VM boyutu kısıtlaması vardır. Bu nedenle, SAP çalıştırmak için gerekli tooattach ek disk alanı tooan Azure VM değil. SAP uygulama sunucusu Azure VM'ler için standart Azure depolama diskleri hello kullanımını yeterli olabilir. Ancak, SAP HANA DBMS Azure VM'ler için üretim ve üretim dışı uygulamaları için Azure Premium Storage diskleri hello kullanımı zorunludur.

Merhaba üzerinde temel [SAP HANA TDI depolama gereksinimlerini](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), Azure Premium depolama yapılandırması aşağıdaki hello önerilir: 

| VM SKU | RAM |  / hana/veri ve/hana/günlük <br /> LVM veya MDADM şeritli | / hana/paylaşılan | / root birim | / usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Merhaba önerilen disk yapılandırmasını hello HANA veri hacmi ve günlük birimi aynı LVM veya MDADM şeritli Azure premium depolama diskleri kümesi hello yerleştirilir. Tüm RAID artıklık düzey Azure Premium Storage hello diskler artıklık için üç görüntülerini tuttuğundan gerekli toodefine değil. toomake yeterli depolama alanı yapılandırdığınızdan emin başvurun hello [SAP HANA TDI depolama gereksinimlerini](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) ve [SAP HANA sunucusu yükleme ve güncelleştirme Kılavuzu](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Açıklandığı gibi hello farklı sanal sabit disk (VHD) üretilen iş birimleri hello farklı Azure premium depolama disklerini de dikkate [yüksek performanslı Premium depolama ve VM'ler için yönetilen diskleri](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Veritabanı veya işlem günlüğü yedeklemeleri depolamak için toohello HANA DBMS VM'ler daha fazla premium depolama disklerini ekleyebilirsiniz.

Merhaba kullanılan iki ana araçları tooconfigure bölümlemesine hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Yazılım RAID Linux üzerinde yapılandırma](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure'da bir Linux VM LVM yapılandırın](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Konuk işletim sistemi Linux çalıştıran tooAzure VM'ler ekleme hakkında daha fazla bilgi diskler için bkz: [disk tooa Linux VM eklemek](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Azure Premium Storage modları önbelleğe alma toodefine disk sağlar. /Hana/Data ve /hana/log bulunduran şeritli hello kümesi için disk önbelleği devre dışı bırakılması gerekir. Merhaba diğer birimlerin (disk) hello için önbelleğe alma modunu çok ayarlayın**salt okunur**.

Daha fazla bilgi için bkz: [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../../storage/common/storage-premium-storage.md).

VM oluşturmak için toofind örnek JSON şablonları Git çok[Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates).
Merhaba vm basit sles şablonu temel bir şablondur. Ek 100 GB veri diski ile bir depolama bölüm içerir. Bu şablon, temel olarak kullanılabilir. Merhaba şablonu tooyour belirli yapılandırma uyarlayabilirsiniz.

>[!Note]
>Açıklandığı gibi bir UUID kullanarak önemli tooattach hello Azure depolama diski olduğundan [Microsoft Azure SUSE Linux sanal makineleri üzerinde çalışan SAP NetWeaver](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello test ortamında hello ekran aşağıdaki gösterildiği gibi ekli toohello SAP uygulama sunucusu VM, iki standart Azure depolama diskleri yoktu. Bir disk (NetWeaver 7.5, SAP GUI ve SAP HANA dahil) tüm hello SAP yazılım yüklemesi için depolanır. Merhaba ikinci disk güvence altına yeterli boş alana ek gereksinimler (örneğin, yedekleme ve test veri) için kullanılabilir olur ve toohello ait tüm sanal makineler arasında paylaşılan hello /sapmnt dizin (diğer bir deyişle, SAP profilleri) toobe için aynı SAP yatay.

![SAP HANA uygulama sunucusu diskleri penceresine iki veri diskleri ve boyutlarının görüntüleme](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Çekirdek parametreleri
SAP HANA hello standart Azure galeri görüntüleri parçası olmayan ve el ile ayarlamanız gerekir belirli Linux çekirdek ayarları gerektirir. SUSE veya Red Hat kullanmadığınıza bağlı olarak, hello parametreler farklı olabilir. Merhaba SAP daha önce listelenen notları bu parametreleri hakkında bilgi verin. Gösterilen hello ekran görüntülerinde SUSE Linux 12 SP1 kullanıldı. 

SAP uygulamaları 12 GA SLES ve SLES SAP uygulamaları 12 SP1 için sahip yeni bir aracı **ayarlanmış adm**, değiştirir eski hello **sapconf** aracı. Özel SAP HANA profil kullanılabilir **ayarlanmış adm**. SAP HANA için tootune hello sistem kök kullanıcı olarak hello aşağıdakileri girin:

   `tuned-adm profile sap-hana`

Hakkında daha fazla bilgi için **ayarlanmış adm**, hello bkz [ayarlanmış adm SUSE belgelerine](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

Aşağıdaki ekran görüntüsü hello gördüğünüz nasıl **ayarlanmış adm** değiştirilen hello `transparent_hugepage` ve `numa_balancing` toohello göre değerler, gerekli SAP HANA ayarları.

![SAP HANA ayarları toorequired göre değerlerini Hello ayarlanmış adm aracı değiştirir](./media/hana-get-started/image005.jpg)

toomake hello SAP HANA çekirdek ayarlarını kalıcı kullanmak **grub2** SLES 12 üzerinde. Hakkında daha fazla bilgi için **grub2**, Git toohello [yapılandırma dosyası yapısı](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE belgelerine bölümü.

Merhaba aşağıdaki ekran görüntüsünde nasıl hello çekirdek ayarlarını hello yapılandırma dosyasında değişti ve kullanarak derlenmiş gösterir **grub2 mkconfig**:

![Merhaba yapılandırma dosyasında değişti ve grub2 mkconfig kullanarak derlenmiş çekirdek ayarları](./media/hana-get-started/image006.jpg)

Başka bir seçenek toochange hello YaST ve hello kullanarak ayarlarıdır **önyükleyici** > **çekirdek parametreleri** ayarları:

![Merhaba çekirdek parametreleri ayarlar sekmesinde YaST önyükleme yükleyicisi](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Dosya sistemleri
Merhaba aşağıdaki ekran görüntüsü hello SAP uygulama sunucusundaki VM hello iki bağlı Azure standart depolama diskleri en üstünde oluşturulan iki dosya sistemleri gösterir. Her iki dosya sistemleri türü XFS ve takılı çok/sapdata ve /sapsoftware.

Bu, dosya sistemleri bu şekilde zorunlu toostructure olduğu. Merhaba disk alanı yapılandırılması için diğer seçeneğiniz vardır. Merhaba en önemli konu boş alanı çalışmasını tooprevent hello kök dosya sistemidir.

![Merhaba SAP uygulama sunucusunda VM oluşturulan iki dosya sistemleri](./media/hana-get-started/image008.jpg)

Merhaba SAP HANA DB VM SAPinst (SWPM) kullandığınızda, bir veritabanı yüklemesi sırasında ve hello ilgili **tipik** yükleme seçeneği her şeyi /hana ve /usr/sap altında yüklenir. Merhaba varsayılan hello SAP HANA günlük yedekleme için /usr/sap altında konumdur. Depolama alanının tükenmesinden gelen önemli tooprevent hello kök dosya sistemi olduğu için yeniden SWPM kullanarak SAP HANA yüklemeden önce /hana ve /usr/sap altında yeterli boş alan olduğundan emin olun.

Merhaba SAP HANA hello standart dosya sistemi düzenini açıklaması için bkz: [SAP HANA sunucusu yükleme ve güncelleştirme Kılavuzu](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Merhaba SAP uygulama sunucusunda VM oluşturulan ek dosya sistemleri](./media/hana-get-started/image009.jpg)

SAP NetWeaver SAP uygulamaları 12 Azure galeri görüntüsü için standart bir SLES/SLES yüklediğinizde hello ekran aşağıdaki gösterildiği gibi hiçbir takas alanı bildiren bir ileti görüntülenir. toodismiss bu iletiyi, bir takas dosyası kullanarak el ile ekleyebilirsiniz **GG**, **mkswap**, ve **swapon**. toolearn nasıl aramak için "el ile ekleme hello takas dosyası" [kullanma hello YaST Bölümleyici](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE belgelerine bölümü.

Başka bir seçenek tooconfigure takas alanı hello Linux VM aracısı tarafından kullanmaktır. Daha fazla bilgi için bkz: Merhaba [Azure Linux Aracısı Kullanıcı Kılavuzu](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Yetersiz takas alanı olduğunu bildiren bir açılır ileti](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>Merhaba/etc/hosts dosyasını
Tooinstall SAP başlamadan önce hello/Etc/Hosts dosyasında hello ana bilgisayar adları ve IP adreslerini hello SAP VM'ler eklediğinizden emin olun. Bir Azure sanal ağı içindeki tüm hello SAP VM'ler dağıtabilir ve ardından hello iç IP adresleri, aşağıda gösterildiği gibi kullanın:

![Ana bilgisayar adlarını ve IP adreslerini hello SAP VM'lerin hello/Etc/Hosts dosyasında listelenen](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>Merhaba/etc/fstab dosyası

Yararlı tooadd hello olan **nofail** parametre toohello fstab dosyası. Bir hello disklerle sorun yaşanırsa bu şekilde hello VM hello önyükleme işleminde askıda değil. Ancak ek disk alanı kullanılamayabilir ve işlemler hello kök dosya sistemini doldurun unutmayın. /Hana eksikse, SAP HANA başlatılamıyor.

![Merhaba nofail parametre toohello fstab dosyası ekleme](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>SLES 12/SLES SAP uygulamaları 12 için grafik GNOME masaüstünde
Bu bölüm aşağıdaki konularda hello kapsar:

* Merhaba GNOME Masaüstü ve xrdp SLES 12/SLES üzerinde SAP uygulamaları 12 için yükleme
* Firefox SLES 12/SLES üzerinde için SAP uygulamaları 12 kullanarak Java tabanlı SAP MC çalıştırma

Xterminal veya VNC (Bu kılavuzda açıklanan değil) gibi alternatifleri de kullanabilirsiniz.

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Merhaba GNOME Masaüstü ve xrdp SLES 12/SLES üzerinde SAP uygulamaları 12 için yükleme
Windows arka plan varsa, size kolayca grafik Masaüstü doğrudan hello SAP Linux VM'ler toorun Firefox, SAPinst, SAP GUI, SAP MC veya HANA Studio içinde kullanıp hello Uzak Masaüstü Protokolü (RDP) bir Windows bilgisayardan aracılığıyla toohello VM bağlanın. Tooproduction ve üretim dışı Linux tabanlı sistemleri ekleme hakkında şirket ilkelerinizi bağımlı grafik kullanıcı arabirimleri, sunucunuzda tooinstall GNOME isteyebilirsiniz. tooinstall hello GNOME masaüstünde bir listelenen SAP uygulamaları 12 VM için Azure SLES 12/SLES:

1. Merhaba GNOME Masaüstü komutu (örneğin, bir pencerede PuTTY) aşağıdaki hello girerek yükleyin:

   `zypper in -t pattern gnome-basic`

2. Xrdp tooallow bağlantı toohello VM RDP üzerinden yükleyin:

   `zypper in xrdp`

3. /Etc/sysconfig/windowmanager düzenleyin ve hello varsayılan Pencere Yöneticisi tooGNOME ayarlayın:

   `DEFAULT_WM="gnome"`

4. Çalıştırma **chkconfig** toomake emin bu xrdp bir yeniden başlatmadan sonra otomatik olarak başlar:

   `chkconfig -level 3 xrdp on`

5. Merhaba RDP bağlantısı ile ilgili bir sorun varsa (bir pencereden PuTTY, örneğin) toorestart deneyin:

   `/etc/xrdp/xrdp.sh restart`

6. Adım işe yaramazsa hello önceki xrdp yeniden belirtildiği için .pid dosyasını kontrol edin:

   `check /var/run` 

   Ara `xrdp.pid`. Bulursanız, kaldırmak ve toorestart yeniden deneyin.

### <a name="starting-sap-mc"></a>SAP MC başlatılıyor
Merhaba GNOME Masaüstü yükledikten sonra hello grafik başlangıç Java tabanlı SAP MC SAP uygulamaları 12 VM için bir listelenen içinde Azure SLES 12/SLES çalışırken Firefox gelen bir hata nedeniyle tarayıcı eklentisi Java eksik hello görüntülenebilir.

SAP MC olduğu hello URL toostart hello `<server>:5<instance_number>13`.

Daha fazla bilgi için bkz: [başlangıç hello SAP Yönetim Konsolu Web tabanlı](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Merhaba aşağıdaki ekran görüntüsü hello Java-tarayıcı eklentisi eksik olduğunda görüntülenen hello hata iletisi gösterir:

![Tarayıcı eklentisi eksik Java grafiği belirten hata iletisi](./media/hana-get-started/image013.jpg)

Tek yönlü toosolve hello sorun YaST, kullanarak hello ekran aşağıdaki gösterildiği gibi eksik eklenti tooinstall hello şudur:

![Eksik eklenti YaST tooinstall kullanma](./media/hana-get-started/image014.jpg)

Merhaba SAP Yönetim Konsolu URL'si yeniden girdiğinizde soran, tooactivate hello eklenti bir ileti görüntülenir:

![Eklenti etkinleştirme isteyen iletişim kutusu](./media/hana-get-started/image015.jpg)

Eksik dosya ile ilgili bir hata iletisi de alabilirsiniz javafx.properties. Bu ilgili toohello Oracle Java 1.8 SAP GUI 7.4 için gereksinimdir. (Bkz [SAP Not 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Merhaba IBM Java Sürüm ne için SAP uygulamaları 12 SLES/SLES ile teslim hello openjdk paket hello gerekli javafx.properties dosyası içerir. Hello çözüm toodownload olduğu ve Oracle kaynağından Java SE 8'i yükleyin.

Merhaba tartışma iş parçacığı openSUSE üzerinde openjdk ile benzer bir sorun hakkında ek bilgi için bkz [SAPGui 7.4 Java openSUSE 42.1 için Leap](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>SAP HANA el ile yükleme: SWPM
Bu bölümdeki ekran görüntüleri Hello dizi SWPM (SAPinst) kullandığınızda, SAP NetWeaver 7.5 ve SAP HANA SP12 yüklemek için hello anahtar adımları gösterir. NetWeaver 7.5 yüklemesinin bir parçası olarak SWPM tek bir örneği olarak hello HANA veritabanına de yükleyebilirsiniz.

Bir örnek test ortamında tek bir Gelişmiş iş uygulama programlama (ABAP) uygulama sunucusu yüklü. Hello ekran aşağıdaki gösterildiği gibi hello kullandık **dağıtılmış sistemi** seçeneği tooinstall hello ASCS ve birincil uygulama sunucusu örneklerinin bir Azure VM ve SAP HANA hello veritabanı sistemi başka bir Azure VM olarak.

![ASCS ve hello dağıtılmış sistemi seçeneği kullanılarak yüklenen birincil uygulama sunucu örnekleri](./media/hana-get-started/image012.jpg)

Merhaba ASCS örneği hello uygulama sunucusuna VM yüklenir ve sonra "çok hello SAP Yönetim Konsolu (ekran aşağıdaki hello gösterilir), yeşil" ayarlayın (Merhaba SAP profil dizini dahil) hello /sapmnt dizin hello SAP HANA DB sunucusu VM paylaşılması gerekir. Merhaba DB yükleme adımı toothis bilgi erişimi gerektirir. Merhaba en iyi şekilde tooprovide toouse YaST kullanarak yapılandırılabilir NFS erişimidir.

![SAP Yönetim Konsolu gösteren hello ASCS örneği VM hello uygulama sunucuda yüklü ve "Yeşil" çok ayarlama](./media/hana-get-started/image016.jpg)

Merhaba uygulama sunucusu üzerinde VM hello/sapmnt paylaşılan dizin NFS hello kullanarak **rw** ve **no_root_squash** seçenekleri. Merhaba varsayılan değerler **ro** ve **root_squash**, hangi neden tooproblems hello veritabanı örneğini yüklediğinizde.

![Merhaba rw ve no_root_squash seçeneklerini kullanarak Hello /sapmnt directory NFS ile paylaşma](./media/hana-get-started/image017b.jpg)

Hello sonraki ekran görüntüsü gösterildiği gibi hello /sapmnt hello uygulama sunucusu VM paylaşımından hello SAP HANA DB sunucusu üzerinde VM kullanarak yapılandırılmalıdır **NFS İstemcisi** (ve YaST).

![NFS İstemcisi kullanılarak yapılandırılan hello /sapmnt paylaşımı](./media/hana-get-started/image018b.jpg)

tooperform dağıtılmış NetWeaver 7.5 yükleme (**veritabanı örneği**), aşağıdaki ekran görüntüsü gösterildiği hello olarak toohello SAP HANA DB sunucusu VM oturum ve SWPM başlatın.

![Bir veritabanı örneği toohello SAP HANA DB sunucusu VM imzalama ve SWPM başlangıç yükleme](./media/hana-get-started/image019.jpg)

Siz seçtikten sonra **tipik** yükleme ve hello yolu toohello yükleme medyasında DB SID, hello ana bilgisayar adı, hello örnek numarasını ve hello DB sistem yöneticisi parolasını girin.

![Merhaba SAP HANA veritabanına sistem yönetici oturum açma sayfası](./media/hana-get-started/image035b.jpg)

Merhaba DBACOCKPIT şeması Hello parolayı girin:

![Merhaba DBACOCKPIT şeması için Hello parola giriş kutusu](./media/hana-get-started/image036b.jpg)

Merhaba SAPABAP1 şema parola için bir soru girin:

![Merhaba SAPABAP1 şema parolası için bir soru girin](./media/hana-get-started/image037b.jpg)

Her görev tamamlandıktan sonra hello DB yükleme işleminin sonraki tooeach aşaması yeşil bir onay işareti görüntülenir. Selamlama iletisine ", yürütme... Veritabanı örneği tamamlandı"görüntülenir.

![Onay iletisi penceresiyle görev tamamlandı](./media/hana-get-started/image023.jpg)

Başarılı yüklemeden sonra hello SAP Yönetim Konsolu ayrıca hello DB örneği "Yeşil" olarak göstermek ve SAP HANA işlemler (hdbindexserver, hdbcompileserver ve benzeri) hello tam listesini görüntüleyebilirsiniz.

![SAP HANA işlemlerin listesini SAP Yönetim Konsolu penceresi](./media/hana-get-started/image024.jpg)

Merhaba aşağıdaki ekran görüntüsünde hello dosya yapısı SWPM hello HANA yükleme sırasında oluşturulan hello /hana/shared dizini altındaki hello parçaları gösterilmektedir. Farklı bir yol hiçbir seçeneği toospecify olduğundan SWPM kullanarak önemli toomount ek disk alanı hello SAP HANA yükleme önce hello /hana dizini altında değildir. Bu, hello kök dosya sistemi boş alan çalışmasını önler.

![HANA yükleme işlemi sırasında oluşturulan hello /hana/shared directory dosya yapısı](./media/hana-get-started/image025.jpg)

Bu ekran hello dosya hello /usr/sap dizin yapısını gösterir:

![Merhaba /usr/sap directory dosya yapısı](./media/hana-get-started/image026.jpg)

dağıtılan hello ABAP yüklemesinin son adımı Hello tooinstall hello birincil uygulama sunucusu örneği verilmiştir:

![Merhaba son adım olarak ABAP yükleme gösteren birincil uygulama sunucusu örneği](./media/hana-get-started/image027b.jpg)

Merhaba birincil uygulama sunucusu örneği ve SAP GUI yüklendikten sonra hello kullanılacak **DBA Pilot** SAP HANA yükleme hello işlem tooconfirm doğru bir şekilde tamamlandı:

![DBA Pilot penceresi başarılı yüklemesini onaylamak](./media/hana-get-started/image028b.jpg)

Son adım olarak, toofirst yüklemek HANA Studio hello SAP uygulama sunucusu VM için istediğiniz ve ardından hello DB sunucusu VM üzerinde çalışan toohello SAP HANA bağlanın:

![SAP HANA Studio hello SAP uygulama sunucusu VM yükleme](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>SAP HANA el ile yükleme: HDBLCM
Toplama tooinstalling SAP HANA SWPM kullanarak dağıtılmış bir yüklemede bir parçası olarak, hello HANA tek başına ilk olarak, HDBLCM kullanarak yükleyebilirsiniz. SAP NetWeaver 7.5, örneğin daha sonra yükleyebilirsiniz. Bu bölümdeki Hello ekran görüntüleri bu işlemi nasıl çalıştığını gösterir.

Merhaba HANA HDBLCM aracı hakkında daha fazla bilgi için bkz:

* [Seçme hello doğru SAP HANA HDBLCM bilgisayarınızı görev için](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA yaşam döngüsü yönetimi araçları](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA sunucusu yükleme ve güncelleştirme Kılavuzu](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

Varsayılan tooavoid sorunları Grup Kimliği ayarında hello için `\<HANA SID\>adm user` (Merhaba HDBLCM aracı tarafından oluşturulan) adlı yeni bir grup tanımlayın `sapsys` grup kimliği kullanarak `1001` SAP HANA HDBLCM aracılığıyla yüklemeden önce:

!["Yeni Grup sapsys kullanılarak tanımlanmış" kimliği 1001 Grup](./media/hana-get-started/image030.jpg)

HDBLCM hello ilk kez başlattığınızda, basit Başlat menüsü görüntülenir. Öğe Seç 1, **yükleme yeni sistem**hello ekran aşağıdaki gösterildiği gibi:

![Merhaba HDBLCM başlangıç penceresinde "yeni sistem Yükle" seçeneği](./media/hana-get-started/image031.jpg)

Merhaba aşağıdaki ekran görüntüsünde, daha önce seçtiğiniz tüm hello anahtar seçeneklerini görüntüler.

> [!IMPORTANT]
> HANA günlük ve veri birimlerini yanı sıra hello yükleme yolu (Bu örnekte paylaşılan / hana /) ve /usr/sap, adlı dizinleri hello kök dosya sisteminin bir parçası olmamalıdır. Bu dizinleri ekli toohello (Merhaba "Disk Kurulumu" bölümünde açıklanan) VM olan toohello Azure veri diski ait. Bu yaklaşım hello kök dosya sistemi alanı yetersiz çalışmasını engeller. Aşağıdaki ekran görüntüsü hello bu hello HANA sistem yöneticisinin kullanıcı kimliği olduğundan görebilirsiniz `1005` ve hello parçası olan `sapsys` grubu (kimliği `1001`) hello yüklemeden önce tanımlanmıştı.

![Daha önce seçtiğiniz tüm anahtar SAP HANA bileşenlerin listesi](./media/hana-get-started/image032.jpg)

Merhaba denetleyebilirsiniz `\<HANA SID\>adm user` (`azdadm` ekran aşağıdaki hello içinde) hello/etc/parola directory ayrıntıları:

![HANA \<HANA SID\>adm kullanıcı ayrıntıları hello/etc/parola dizininde listelenen](./media/hana-get-started/image033.jpg)

SAP HANA HDBLCM kullanarak yükledikten sonra hello ekran aşağıdaki gösterildiği gibi hello dosya yapısı SAP HANA Studio'da görebilirsiniz. Tüm hello SAP NetWeaver tabloları içerir, hello SAPABAP1 şema henüz kullanılamıyor.

![SAP HANA Studio'da SAP HANA dosya yapısı](./media/hana-get-started/image034.jpg)

SAP HANA yükledikten sonra SAP NetWeaver üzerine yükleyebilirsiniz. Aşağıdaki ekran görüntüsü gösterildiği hello hello yükleme (Merhaba önceki bölümde açıklandığı gibi) SWPM kullanarak dağıtılmış bir yükleme olarak gerçekleştirildi. SWPM kullanarak hello veritabanı örneğini yüklediğinizde hello girin (örneğin, ana bilgisayar adı, HANA SID ve örnek numarasını) HDBLCM kullanarak aynı veri. SWPM hello varolan HANA yükleme kullanır ve başka şemalar ekler.

![SWPM kullanılarak gerçekleştirilen bir dağıtılmış yükleme](./media/hana-get-started/image035b.jpg)

Merhaba aşağıdaki ekran görüntüsü hello SWPM yükleme adımı hello DBACOCKPIT şeması hakkında veri girdiğiniz gösterir:

![DBACOCKPIT şema verileri girildiği hello SWPM yükleme adımı](./media/hana-get-started/image036b.jpg)

Merhaba SAPABAP1 şeması hakkında verileri girin:

![Merhaba SAPABAP1 şeması hakkında veri girme](./media/hana-get-started/image037b.jpg)

Merhaba SWPM veritabanı örneği yüklemesi tamamlandıktan sonra SAP HANA Studio'da hello SAPABAP1 şema görebilirsiniz:

![SAP HANA Studio'da Hello SAPABAP1 şeması](./media/hana-get-started/image038b.jpg)

Merhaba SAP uygulama sunucusu ve SAP GUI yükleme tamamlandıktan sonra son olarak, hello HANA DB örneği hello kullanarak doğrulayabilirsiniz **DBA Pilot** işlem:

![Merhaba HANA DB örneği ile Merhaba DBA Pilot işlem doğrulandı.](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>SAP yazılım yüklemeleri
Hello ekran görüntüleri aşağıdaki gösterildiği gibi yazılım SAP hizmet Market hello yükleyebilirsiniz.

NetWeaver 7.5 Linux/HANA yükleyin:

 ![NetWeaver 7.5 indirme SAP hizmeti yükleme ve yükseltme penceresi](./media/hana-get-started/image001.jpg)

HANA SP12 Platform Edition'ı yükleyin:

 ![SAP hizmeti yükleme ve yükseltme penceresi HANA SP12 Platform sürümü karşıdan yüklemek için](./media/hana-get-started/image002.jpg)


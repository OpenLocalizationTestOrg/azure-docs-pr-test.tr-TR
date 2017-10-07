---
title: Azure Site Recovery kullanarak koruma aaaExclude disklerden | Microsoft Docs
description: "Neden ve nasıl Çoğaltmada VMware tooAzure ve Hyper-V tooAzure senaryoları için tooexclude VM diskleri açıklar."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma
Bu makalede nasıl tooexclude Çoğaltmada diskler açıklanmaktadır. Bu dışlama tüketilen hello çoğaltma bant genişliğini iyileştirmek veya böyle diskleri kullanan hello hedef tarafı kaynakları en iyi duruma getirme. Merhaba özelliği VMware tooAzure ve Hyper-V tooAzure senaryoları için desteklenir.

## <a name="prerequisites"></a>Ön koşullar

Varsayılan olarak, bir makinedeki tüm diskler çoğaltılır. VMware tooAzure çoğaltıyorsanız çoğaltma etkinleştirmeden önce çoğaltma diskten tooexclude, el ile Merhaba Mobility hizmeti hello makinede yüklemeniz gerekir.


## <a name="why-exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma nedenleri nelerdir?
Disklerin çoğaltmanın dışında tutulması, çoğu zaman aşağıdaki nedenlerden dolayı gereklidir:

- Dışlanan hello diskte churned hello verileri önemli değildir veya yinelenmiş toobe gerek yoktur.

- Bu karmaşası çoğaltmamasının toosave depolama ve ağ kaynaklarını istiyor.

## <a name="what-are-hello-typical-scenarios"></a>Merhaba tipik senaryolar nelerdir?
Dışarıda tutmak için çok iyi adaylar olan belirli veri değişim sıklığı örnekleri tanımlayabilirsiniz. Örnekler içerebilir tooa disk belleği dosyası (pagefile.sys) yazar ve Microsoft SQL Server'ın toohello tempdb dosyasına yazar. Merhaba iş yükü ve hello depolama alt sistemi bağlı olarak, Başlangıç disk belleği dosyası karmaşası önemli miktarda kaydedebilirsiniz. Ancak, bu verileri hello birincil site tooAzure çoğaltma yoğun kaynak olacaktır. Bu nedenle, aşağıdaki adımları toooptimize çoğaltma hello işletim sistemi ve Başlangıç disk belleği dosyası sahip tek bir sanal diskten bir sanal makinenin hello kullanabilirsiniz:

1. Bölünmüş hello tek sanal diske iki sanal disk. Bir sanal disk hello işletim sistemi, ve Başlangıç disk belleği dosyası hello diğer sahiptir.
2. Başlangıç disk belleği dosyası disk çoğaltmanın dışında tutabilir.

Benzer şekilde, aşağıdaki adımları toooptimize hem hello Microsoft SQL Server tempdb lanı sahip bir disk hello kullanın ve sistem veritabanı dosyasının hello:

1. Merhaba sistem veritabanı ve tempdb iki farklı disklerde tutun.
2. Merhaba tempdb disk çoğaltmanın dışında tutabilir.

## <a name="how-tooexclude-disks-from-replication"></a>Nasıl tooexclude Çoğaltmada diskler?

### <a name="vmware-tooazure"></a>VMware tooAzure
Merhaba izleyin [çoğaltmasını etkinleştir](site-recovery-vmware-to-azure.md) iş akışı tooprotect hello Azure Site kurtarma portalından bir sanal makine. Merhaba Dördüncü adımda hello iş akışının, hello kullanmanız **DISK tooREPLICATE** sütun tooexclude diskleri çoğaltma. Varsayılan olarak, tüm diskler çoğaltma için seçilir. Çoğaltma ve ardından tam hello adımları tooenable çoğaltma tooexclude istediğiniz disklerin Hello onay kutusunu temizleyin.

![Diskleri çoğaltmanın dışında tutabilir ve VMware tooAzure yeniden çalışma için çoğaltmayı etkinleştirme](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Merhaba Mobility hizmeti zaten yüklü diskleri hariç tutabilirsiniz. Merhaba Mobility hizmeti yalnızca çoğaltma etkinleştirildikten sonra hello zorlama mekanizmasını kullanarak yüklü olduğundan toomanually yükleme hello Mobility hizmeti gerekir.
> * Yalnızca temel diskler çoğaltma dışı bırakılabilir. İşletim sistemi veya dinamik diskler dışarıda tutulamaz.
> * Çoğaltmayı etkinleştirdikten sonra, diskleri çoğaltma ekleyemez veya kaldıramazsınız. Tooadd istediğiniz veya bir disk hariç, toodisable koruma hello makine için ihtiyaç ve yeniden etkinleştirin.
> * Yük devretme tooAzure sonra bir uygulama toooperate için gerekli olan bir disk bıraksanız çoğaltılan Merhaba uygulaması çalıştırabilmeniz için toocreate hello diski el ile azure'da gerekir. Alternatif olarak, bir kurtarma planı toocreate hello diskine hello makinenin yük devretme sırasında Azure Otomasyon tümleştirebilirsiniz.
> * Windows sanal makine: Azure'da elle oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üç disk için yük devretme gerçekleştirirseniz ve iki diski doğrudan Azure Sanal Makineler'de oluşturursanız, yalnızca yük devretme gerçekleştirilen üç disk yeniden çalışır duruma getirilir. Yeniden çalışma veya şirket içi tooAzure gelen yeniden koruma el ile oluşturulan diskleri ekleyemezsiniz.
> * Linux sanal makinesi: Azure’da ele oluşturduğunuz diskler yenide çalışır duruma getirilir. Örneğin, üç disk için yük devretme gerçekleştirirseniz ve iki diski doğrudan Azure'da oluşturursanız, beş diskin tümü yeniden çalışır duruma getirilir. El ile oluşturulmuş diskleri, yeniden çalışmanın dışında tutamazsınız.
>

### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Merhaba izleyin [çoğaltmasını etkinleştir](site-recovery-hyper-v-site-to-azure.md) iş akışı tooprotect hello Azure Site kurtarma portalından bir sanal makine. Merhaba Dördüncü adımda hello iş akışının, hello kullanmanız **DISK tooREPLICATE** sütun tooexclude diskleri çoğaltma. Varsayılan olarak, tüm diskler çoğaltma için seçilir. Çoğaltma ve ardından tam hello adımları tooenable çoğaltma tooexclude istediğiniz disklerin Hello onay kutusunu temizleyin.

![Diskleri çoğaltmanın dışında tutabilir ve Hyper-V tooAzure yeniden çalışma için çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Yalnızca temel diskler çoğaltma dışında bırakılabilir. İşletim sistemi diskleri dışarıda tutulamaz. Dinamik diskleri dışarıda tutmamanızı öneririz. Azure Site Recovery, temel veya dinamik hello Konuk sanal makinesinde sanal sabit disk (VHD) tanımlanamıyor.  Tüm bağımlı dinamik birimi disklerinin dışarıda bırakılmazsa hello korumalı dinamik disk başarısız disk, bir yük devretme sanal makinede olur ve Merhaba, disk üzerindeki verileri erişilebilir değil.
> * Çoğaltmayı etkinleştirdikten sonra, diskleri çoğaltma ekleyemez veya kaldıramazsınız. Tooadd istediğiniz veya bir disk hariç, toodisable koruma hello sanal makine için ihtiyaç ve yeniden etkinleştirin.
> * Bir uygulama toooperate için gerekli olan bir disk bıraksanız çoğaltılan Merhaba uygulaması çalıştırabilmeniz için yük devretme tooAzure sonra toocreate hello diski el ile azure'da ihtiyacınız vardır. Alternatif olarak, bir kurtarma planı toocreate hello diskine hello makinenin yük devretme sırasında Azure Otomasyon tümleştirebilirsiniz.
> * Azure'da elle oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üzerinde üç disk başarısız ve doğrudan Azure sanal makineleri iki disk oluşturursanız, üzerinden başarısız yalnızca üç disk geri Azure tooHyper-V ile başarısız. Yeniden çalışma veya Hyper-V tooAzure ters çoğaltmayı el ile oluşturulan diskleri ekleyemezsiniz.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Disk dışarıda bırakmaya ilişkin uçtan uca senaryolar
Şimdi iki senaryo toounderstand hello dışlama disk özelliği göz önünde bulundurun:

- SQL Server tempdb diski
- Disk belleği dosyası (pagefile.sys) diski

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Merhaba SQL Server tempdb disk Dışla
Dışlanabilecek bir tempdb’si olan bir SQL Server sanal makinesi düşünelim.

Merhaba hello sanal disk SalesDB adıdır.

Diskleri hello kaynak sanal makinede aşağıdaki gibidir:


**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1| Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
DB-Disk2 (korumadan dışlanan hello disk) | Disk2 | E:\ | Geçici dosyalar
DB-Disk3 (korumadan dışlanan hello disk) | Disk3 | F:\ | SQL tempdb veritabanı (klasör yolu (F:\MSSQL\Data\) < /br/>< /br/> Yük devretme önce hello klasör yolunu not alın.
DB-Disk4 | Disk4 |G:\ |Kullanıcı Veritabanı2

Merhaba SalesDB sanal makine korurken hello sanal makinenin iki disk üzerindeki verileri karmaşıklığı geçici, olduğundan Disk2 ve Disk3 çoğaltmanın dışında tutabilir. Azure Site Recovery bu diskleri çoğaltmaz. Yük devretme, bu disklerin hello yük devretme üzerindeki sanal makinede Azure mevcut olmaz.

Merhaba yük devretme sonrasında Azure sanal makinesi disklerde aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | E:\ | Geçici depolama < /br / >< /br / > Azure hello ilk kullanılabilir sürücü harfi atar ve bu disk ekler.
Disk2 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk3 | G:\ | Kullanıcı Veritabanı2

Disk2 ve Disk3 hello SalesDB sanal makineden dışlandığından E: hello ilk sürücü harfi hello kullanılabilir listeden ' dir. Azure E: toohello geçici depolama birimi atar. Tüm çoğaltılan hello disklerde hello sürücü harfleri kalır hello aynı.

Merhaba SQL tempdb disk Disk3 (tempdb klasör yolu F:\MSSQL\Data\), çoğaltmadan dışlandı. Merhaba disk hello yük devretme sanal makinede kullanılabilir değil. Sonuç olarak, hello SQL hizmeti durdurulmuş bir durumda olduğundan ve hello F:\MSSQL\Data yolu gerekiyor.

Bu yol iki yolu toocreate vardır:

- Yeni bir disk ekleyin ve tempdb klasör yolunu atayın.
- Varolan bir geçici depolama diski hello tempdb klasör yolu için kullanın.

#### <a name="add-a-new-disk"></a>Yeni bir disk ekleme:

1. SQL tempdb.mdf ve yük devretme önce tempdb.ldf hello yollarını aşağı yazın.
2. Azure portal Hello yeni disk toohello yük devretme sahip bir sanal makine hello aynı veya daha fazla boyutu, hello kaynak SQL tempdb disk (Disk3) ekleyin.
3. İçinde toohello Azure sanal makinesinde oturum açın. Merhaba disk Yönetimi'ni (diskmgmt.msc) konsolundan başlatamadı ve biçiminde hello disk yeni eklenen.
4. Aynı sürücü hello SQL tempdb disk (F:) tarafından kullanılan harfi atama hello.
5. Merhaba F: birimini (F:\MSSQL\Data) üzerinde bir tempdb klasör oluşturun.
6. Merhaba hizmet konsolundan Hello SQL hizmetini başlatın.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Varolan bir geçici depolama diski hello SQL tempdb klasör yolu için kullanın:

1. Bir komut istemi açın.
2. SQL Server kurtarma modunda hello komut isteminden çalıştırın.

        Net start MSSQLSERVER /f / T3608

3. SQLCMD toochange hello tempdb yol toohello yeni yol aşağıdaki hello çalıştırın.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Merhaba Microsoft SQL Server hizmetini durdurun.

        Net stop MSSQLSERVER
5. Merhaba Microsoft SQL Server hizmetini başlatın.

        Net start MSSQLSERVER

Geçici depolama diskini Azure Kılavuzu izleyerek toohello bakın:

* [Azure VM'ler toostore SQL Server TempDB ve arabellek havuzu uzantıları SSD kullanma](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Azure Sanal Makineler’de SQL Server için performansa yönelik en iyi uygulamalar](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Yeniden çalışma (konaktan Azure tooan şirket içi)
Artık Azure tooyour şirket içi VMware veya Hyper-V ana bilgisayarından üzerinden başarısız olduğunda, çoğaltılan hello diskleri anlayalım. Azure'da elle oluşturduğunuz diskler çoğaltılmaz. Örneğin, üç disk için yük devretme gerçekleştirir ve iki diski doğrudan Azure Sanal Makinelerinde oluşturursanız, yalnızca yük devretme gerçekleştirilen üç disk yeniden çalışır hale getirilir. Yeniden çalışma veya şirket içi tooAzure gelen yeniden koruma el ile oluşturulan diskleri ekleyemezsiniz. Ayrıca hello geçici depolama disk tooon içi konakları yinelemez.

#### <a name="failback-toooriginal-location-recovery"></a>Yeniden çalışma toooriginal konum kurtarma

Merhaba önceki örnekte hello Azure sanal makinesinin disk yapılandırması aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | E:\ | Geçici depolama < /br / >< /br / > Azure hello ilk kullanılabilir sürücü harfi atar ve bu disk ekler.
Disk2 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk3 | G:\ | Kullanıcı Veritabanı2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Yeniden çalışma toohello özgün konumuna yapıldığında hello geri dönme sanal makine disk yapılandırması dışlanan diskleri yok. VMware tooAzure dışlanan diskleri hello geri dönme sanal makinede kullanılabilir olmaz.

Planlı yük devretmeyi sonra Azure tooon içi VMware, hello VMWare sanal makinesi (özgün konum) disklerde aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk2 | G:\ | Kullanıcı Veritabanı2

#### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Yeniden çalışma toohello özgün konumuna olduğunda hello geri dönme sanal makine disk yapılandırma kalır aynı Hyper-V için özgün sanal makine disk yapılandırma olarak hello. Hyper-V sitesi tooAzure dışlanan diskleri hello geri dönme sanal makinede kullanılabilir.

Azure tooon içi Hyper-V'ye planlı yük devretme sonrasında hello Hyper-V sanal makinesi (özgün konum) disklerde aşağıdaki gibidir:

**Disk Adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
DB-Disk2 (Dışlanan disk) | Disk2 | E:\ | Geçici dosyalar
DB-Disk3 (Dışlanan disk) | Disk3 | F:\ | SQL tempdb veritabanı (klasör yolu (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Kullanıcı Veritabanı2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Başlangıç disk belleği dosyası (pagefile.sys) disk Dışla

Dışarıda tutulabilecek bir disk belleği dosyası diski olan bir sanal makine düşünelim.
İki durum vardır.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Durum 1: Başlangıç disk belleği dosyası hello D: sürücü üzerinde yapılandırılmış
Merhaba disk yapılandırması şöyledir:


**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB disk 1 (Merhaba korumadan dışlanan hello disk) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Başlangıç disk belleği dosyası ayarlarını hello kaynak sanal makinede şunlardır:

![Kaynak sanal makinedeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


VMware tooAzure veya Hyper-V tooAzure hello sanal makinenin yük devretme sonrasında Azure sanal makinesi hello disklerde aşağıdaki gibidir:

**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | Geçici depolama</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Disk 1 (D:) dışlandığından D: hello ilk sürücü harfi hello kullanılabilir listeden olabilir. Azure D: toohello geçici depolama birimi atar. D: hello Azure sanal makinesi üzerinde mevcut olduğundan, Başlangıç disk belleği dosyası ayarı hello sanal makine kalır aynı hello.

Başlangıç disk belleği dosyası ayarlarını hello Azure sanal makinesi üzerinde şunlardır:

![Azure sanal makinesindeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Durum 2: Başlangıç disk belleği dosyası (dışında D: sürücüsü) başka bir sürücüde yapılandırılmış

Merhaba kaynak sanal makine disk yapılandırması şöyledir:

**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB disk 1 (korumadan dışlanan hello disk) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Başlangıç disk belleği dosyası ayarlarını hello şirket içi sanal makine üzerinde şunlardır:

![Dosya ayarlarını hello şirket içi sanal makinedeki disk belleği](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

VMware/Hyper-V tooAzure gelen hello sanal makinenin yük devretme sonrasında Azure sanal makinesi hello disklerde aşağıdaki gibidir:

**Disk adı**| **Konuk işletim sistemi disk no.**| **Sürücü harfi** | **Merhaba diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | Geçici depolama</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

D: hello ilk sürücü harfi kullanılabilir hello listeden olduğundan, Azure D: toohello geçici depolama birimi atar. Tüm çoğaltılan hello disklerde hello sürücü harfi kalır aynı hello. Merhaba G: disk kullanılabilir olmadığından hello sistem hello C: sürücüsündeki disk belleği dosyası başlangıç için kullanın.

Başlangıç disk belleği dosyası ayarlarını hello Azure sanal makinesi üzerinde şunlardır:

![Azure sanal makinesindeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Sonraki adımlar
Dağıtımınız ayarlandıktan ve çalışmaya başladıktan sonra farklı türdeki yük devretmeler hakkında [daha fazla bilgi edinebilirsiniz](site-recovery-failover.md).

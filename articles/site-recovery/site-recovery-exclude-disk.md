---
title: "Azure Site Recovery kullanarak disk korumasını hariç tutma | Microsoft Docs"
description: "VMware’den Azure’a ve Hyper-V’den Azure’a senaryolarında VM disklerinin çoğaltma işleminden nasıl ve neden hariç tutulacağı açıklanmaktadır."
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
ms.openlocfilehash: fccbe88e3c0c2b2f3e9958f5f2f27adc017e4d03
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma
Bu makalede, disklerin çoğaltmanın dışında nasıl tutulacağı açıklanmaktadır. Bu dışında tutma, kullanılan çoğaltma bant genişliğini iyileştirebilir veya bu gibi disklerin kullandığı hedef tarafı kaynakları iyileştirebilir. Bu özellik, VMware’den Azure’a ve Hyper-V’den Azure’a senaryoları için desteklenir.

## <a name="prerequisites"></a>Ön koşullar

Varsayılan olarak, bir makinedeki tüm diskler çoğaltılır. Bir diski çoğaltmanın dışında tutmak için, VMware’den Azure’a çoğaltma yapıyorsanız çoğaltmayı etkinleştirmeden önce Mobility hizmetini makineye el ile yüklemeniz gerekir.


## <a name="why-exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma nedenleri nelerdir?
Disklerin çoğaltmanın dışında tutulması, çoğu zaman aşağıdaki nedenlerden dolayı gereklidir:

- Hariç tutulan diskteki değişen veriler önemli değildir veya çoğaltılmaları gerekmez.

- Bu dalgalanmayı çoğaltmayarak depolama ve ağ kaynaklarından tasarruf sağlamak istersiniz.

## <a name="what-are-the-typical-scenarios"></a>Tipik senaryolar nelerdir?
Dışarıda tutmak için çok iyi adaylar olan belirli veri değişim sıklığı örnekleri tanımlayabilirsiniz. Örnekler, disk belleği dosyasına (pagefile.sys) yazma ve Microsoft SQL Server tempdb dosyasına yazmayı içerebilir. İş yüküne ve depolama alt sistemine bağlı olarak, disk belleği dosyasında önemli miktarda dalgalanma kaydedebilir. Ancak bu verilerin birincil siteden Azure'a çoğaltılması yoğun bir kaynak kullanımına neden olacaktır. Bu nedenle, hem işletim sistemi hem de disk belleği dosyası bulunan tek bir sanal diske sahip bir sanal makinenin çoğaltılmasını iyileştirmek üzere aşağıdaki adımları kullanabilirsiniz:

1. Tek sanal diski iki sanal diske bölün. Bir sanal diskte işletim sistemi ve diğerinde disk belleği dosyası vardır.
2. Disk belleği dosyasını çoğaltmanın dışında tutun.

Benzer şekilde, Microsoft SQL Server tempdb dosyasına ve sistem veritabanı dosyasına sahip bir diski en iyi duruma getirmek için aşağıdaki adımları kullanabilirsiniz:

1. Sistem veritabanını ve tempdb dosyasını iki farklı diskte tutabilirsiniz.
2. Tempdb diskini çoğaltmanın dışında tutabilirsiniz.

## <a name="how-to-exclude-disks-from-replication"></a>Diskler nasıl çoğaltmanın dışında tutulur?

### <a name="vmware-to-azure"></a>Vmware’den Azure’a
Azure Site Recovery portalından bir sanal makineyi korumak için [Çoğaltmayı etkinleştir](site-recovery-vmware-to-azure.md) iş akışını izleyin. İş akışının dördüncü adımında, diskleri çoğaltmanın dışında tutmak için **DISK TO REPLICATE** sütununu kullanın. Varsayılan olarak, tüm diskler çoğaltma için seçilir. Çoğaltmanın dışında tutmak istediğiniz disklerin onay kutusunu temizleyin ve ardından çoğaltmayı etkinleştirme adımlarını tamamlayın.

![Diskleri çoğaltmanın dışında tutma ve VMware’den Azure’a yeniden çalışma için çoğaltmayı etkinleştirin](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Yalnızca Mobility hizmetinin zaten yüklü olduğu diskleri dışarıda tutabilirsiniz. Mobility hizmeti yalnızca, çoğaltma etkinleştirildikten sonra gönderim mekanizması kullanılarak yüklendiğinden Mobility hizmetini elle yüklemeniz gerekir.
> * Yalnızca temel diskler çoğaltma dışı bırakılabilir. İşletim sistemi veya dinamik diskler dışarıda tutulamaz.
> * Çoğaltmayı etkinleştirdikten sonra, diskleri çoğaltma ekleyemez veya kaldıramazsınız. Disk eklemek veya dışarıda tutmak istiyorsanız, makinenin korumasını devre dışı bırakmanız ve ardından yeniden etkinleştirmeniz gerekir.
> * Bir uygulamanın çalışması için gerekli olan bir diski hariç tutarsanız, Azure'a yük devretme gerçekleştirildikten sonra, çoğaltılan uygulamanın çalışabilmesi için diski Azure'da el ile oluşturmanız gerekir. Alternatif olarak, makinenin yük devri esnasında diski oluşturmak için Azure otomasyonunu bir kurtarma planıyla tümleştirebilirsiniz.
> * Windows sanal makine: Azure'da elle oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üç disk için yük devretme gerçekleştirirseniz ve iki diski doğrudan Azure Sanal Makineler'de oluşturursanız, yalnızca yük devretme gerçekleştirilen üç disk yeniden çalışır duruma getirilir. Elle oluşturduğunuz diskleri, yeniden çalışır duruma getirmeye veya şirket içinden Azure'a yeniden koruma uygulama işlemlerine dahil edemezsiniz.
> * Linux sanal makinesi: Azure’da ele oluşturduğunuz diskler yenide çalışır duruma getirilir. Örneğin, üç disk için yük devretme gerçekleştirirseniz ve iki diski doğrudan Azure'da oluşturursanız, beş diskin tümü yeniden çalışır duruma getirilir. El ile oluşturulmuş diskleri, yeniden çalışmanın dışında tutamazsınız.
>

### <a name="hyper-v-to-azure"></a>Hyper-V’den Azure’a
Azure Site Recovery portalından bir sanal makineyi korumak için [Çoğaltmayı etkinleştir](site-recovery-hyper-v-site-to-azure.md) iş akışını izleyin. İş akışının dördüncü adımında, diskleri çoğaltmanın dışında tutmak için **DISK TO REPLICATE** sütununu kullanın. Varsayılan olarak, tüm diskler çoğaltma için seçilir. Çoğaltmanın dışında tutmak istediğiniz disklerin onay kutusunu temizleyin ve ardından çoğaltmayı etkinleştirme adımlarını tamamlayın.

![Diskleri çoğaltmanın dışında tutun ve Hyper-V’den Azure’a yeniden çalışma için çoğaltmayı etkinleştirin](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Yalnızca temel diskler çoğaltma dışında bırakılabilir. İşletim sistemi diskleri dışarıda tutulamaz. Dinamik diskleri dışarıda tutmamanızı öneririz. Azure Site Recovery, konuk sanal makinede hangi sanal sabit diskin (VHD) temel veya dinamik olduğunu tanımlayamaz.  Bağımlı dinamik birim disklerin tümü dışlanmazsa, korumalı dinamik disk yük devredilen bir sanal makinede hatalı disk haline gelir ve bu diskteki verilere erişim sağlanamaz.
> * Çoğaltmayı etkinleştirdikten sonra, diskleri çoğaltma ekleyemez veya kaldıramazsınız. Disk eklemek veya dışarıda tutmak istiyorsanız, sanal makine için korumayı devre dışı bırakmanız ve ardından yeniden etkinleştirmeniz gerekir.
> * Bir uygulamanın çalışması için gerekli olan bir diski hariç tutarsanız, Azure'a yük devretme gerçekleştirildikten sonra, çoğaltılan uygulamanın çalışabilmesi için diski Azure'da el ile oluşturmanız gerekir. Alternatif olarak, makinenin yük devri esnasında diski oluşturmak için Azure otomasyonunu bir kurtarma planıyla tümleştirebilirsiniz.
> * Azure'da elle oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üç disk için yük devretme gerçekleştirir ve iki diski doğrudan Azure Sanal Makinelerinde oluşturursanız, yalnızca yük devretme gerçekleştirilen üç disk Azure'dan Hyper-V'ye yeniden çalışır hale getirilir. Yeniden çalışır hale getirilirken veya Hyper-V’den Azure’a ters çoğaltmada elle oluşturulmuş diskler dahil edilemez.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Disk dışarıda bırakmaya ilişkin uçtan uca senaryolar
Disk dışarıda tutma özelliğini daha iyi anlamak için iki senaryoyu düşünelim:

- SQL Server tempdb diski
- Disk belleği dosyası (pagefile.sys) diski

### <a name="exclude-the-sql-server-tempdb-disk"></a>SQL Server tempdb diskini dışarıda tutma
Dışlanabilecek bir tempdb’si olan bir SQL Server sanal makinesi düşünelim.

Sanal disk adı SalesDB şeklindedir.

Kaynak sanal makinedeki diskler aşağıdaki gibidir:


**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1| Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
DB-Disk2 (Disk, korumanın dışında tutuldu) | Disk2 | E:\ | Geçici dosyalar
DB-Disk3 (Disk, korumanın dışında tutuldu) | Disk3 | F:\ | SQL tempdb veritabanı (klasör yolu (F:\MSSQL\Data\) </br /> </br />Yük devretmeden önce klasör yolunu yazın.
DB-Disk4 | Disk4 |G:\ |Kullanıcı Veritabanı2

Sanal makinenin iki diskindeki veri değişim sıklığı geçici olduğundan, SalesDB sanal makinesini korurken Disk2 ve Disk3’ü çoğaltmanın dışında tutun. Azure Site Recovery bu diskleri çoğaltmaz. Yük devretmede, bu diskler Azure’da yük devretme sanal makinesinde mevcut olmaz.

Yük devretme sonrasında Azure sanal makinesindeki diskler aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | E:\ | Geçici depolama</br /> </br />Azure bu diski ekler ve kullanılabilir ilk sürücü harfini buna atar.
Disk2 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk3 | G:\ | Kullanıcı Veritabanı2

Disk2 ve Disk3, SalesDB sanal makinesinin dışında tutulduğundan, kullanılabilir sürücü harfleri listesindeki ilk harf E: olur. Azure, geçici depolama birimine E: harfini atar. Tüm çoğaltılan diskler için, sürücü harfleri aynı kalır.

SQL tempdb diski olan Disk3 (tempdb klasör yolu F:\MSSQL\Data\), çoğaltmadan dışlanmıştır. Disk yük devretme sanal makinesinde kullanılabilir değildir. Sonuç olarak, SQL hizmeti durdurulmuş durumdadır ve F:\MSSQL\Veri yolu gerekir.

Bu yolu oluşturmanın iki yöntemi vardır:

- Yeni bir disk ekleyin ve tempdb klasör yolunu atayın.
- tempdb klasör yolu için var olan geçici bir depolama diski kullanın.

#### <a name="add-a-new-disk"></a>Yeni bir disk ekleme:

1. Yük devretme öncesinde SQL tempdb.mdf ve tempdb.ldf yollarını yazın.
2. Azure portalında, yük devretme sanal makinesine, kaynak SQL tempdb diskiyle (Disk3) aynı boyutta veya daha büyük yeni bir disk ekleyin.
3. Azure sanal makinesinde oturum açın. Disk yönetimi (diskmgmt.msc) konsolundan yeni eklenen diski başlatıp biçimlendirin.
4. SQL tempdb diski tarafından kullanılan sürücü harfinin aynısını (F:) atayın.
5. F: biriminde bir tempdb klasörü (F:\MSSQL\Data) oluşturun.
6. Hizmet konsolundan SQL hizmetini başlatın.

#### <a name="use-an-existing-temporary-storage-disk-for-the-sql-tempdb-folder-path"></a>SQL tempdb klasör yolu için var olan geçici bir depolama diski kullanın:

1. Bir komut istemi açın.
2. Komut isteminden kurtarma modunda SQL Server çalıştırın.

        Net start MSSQLSERVER /f / T3608

3. tempdb yolunu yeni yola değiştirmek için aşağıdaki sqlcmd’yi çalıştırın.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Microsoft SQL Server hizmetini durdurun.

        Net stop MSSQLSERVER
5. Microsoft SQL Server hizmetini başlatın.

        Net start MSSQLSERVER

Geçici depolama diski için aşağıdaki Azure kılavuzuna bakın:

* [SQL Server TempDB’yi ve Arabellek Havuzu Uzantılarını depolamak için Azure sanal makinelerde SSD kullanma](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Azure Sanal Makineler’de SQL Server için performansa yönelik en iyi uygulamalar](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-to-an-on-premises-host"></a>Yeniden çalışır hale getirme (Azure'dan şirket içi bir ana bilgisayara)
Şimdi, Azure'dan şirket içi VMware veya Hyper-V ana bilgisayarınıza yük devretme yaptığınızda çoğaltılan disklere bakalım. Azure'da elle oluşturduğunuz diskler çoğaltılmaz. Örneğin, üç disk için yük devretme gerçekleştirir ve iki diski doğrudan Azure Sanal Makinelerinde oluşturursanız, yalnızca yük devretme gerçekleştirilen üç disk yeniden çalışır hale getirilir. Elle oluşturduğunuz diskleri, yeniden çalışır duruma getirmeye veya şirket içinden Azure'a yeniden koruma uygulama işlemlerine dahil edemezsiniz. Ayrıca, geçici depolama diskini şirket içi ana bilgisayarlarına da çoğaltmaz.

#### <a name="failback-to-original-location-recovery"></a>Özgün konum kurtarması için yeniden çalışma

Önceki örnekte, Azure sanal makinesinin disk yapılandırması aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | E:\ | Geçici depolama</br /> </br />Azure bu diski ekler ve kullanılabilir ilk sürücü harfini buna atar.
Disk2 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk3 | G:\ | Kullanıcı Veritabanı2


#### <a name="vmware-to-azure"></a>Vmware’den Azure’a
Yeniden çalışma özgün konumda gerçekleştirildiğinde, yeniden çalışma sanal makinesi disk yapılandırmasında dışarıda tutulan diskler olmaz. VMware’den Azure'a çoğaltmanın dışında tutulan diskler, yeniden çalışır hale getirme sanal makinesinde mevcut olmayacaktır.

Azure'dan şirket içi VMware’e planlı yük devretmenin ardında, VMWare sanal makinesindeki (özgün konum) diskler aşağıdaki gibidir:

**Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | ---
DISK0 | C:\ | İşletim sistemi diski
Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
Disk2 | G:\ | Kullanıcı Veritabanı2

#### <a name="hyper-v-to-azure"></a>Hyper-V’den Azure’a
Yeniden çalışma özgün konum için olduğunda, yeniden çalışma sanal makinesi disk yapılandırması, Hyper-V’ye ait özgün sanal makine disk yapılandırması ile aynı kalır. Hyper-V sitesinden Azure'a çoğaltmanın dışında tutulan diskler, yeniden çalışır hale getirme sanal makinesinde mevcut olacaktır.

Azure'dan şirket içi Hyper-V’ye planlı yük devretmenin ardından, Hyper-V sanal makinesindeki (özgün konum) diskler aşağıdaki gibidir:

**Disk Adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | SQL sistem veritabanı ve Kullanıcı Veritabanı1
DB-Disk2 (Dışlanan disk) | Disk2 | E:\ | Geçici dosyalar
DB-Disk3 (Dışlanan disk) | Disk3 | F:\ | SQL tempdb veritabanı (klasör yolu (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Kullanıcı Veritabanı2


#### <a name="exclude-the-paging-file-pagefilesys-disk"></a>Disk belleği dosyası (pagefile.sys) diskini dışarıda tutma

Dışarıda tutulabilecek bir disk belleği dosyası diski olan bir sanal makine düşünelim.
İki durum vardır.

#### <a name="case-1-the-paging-file-is-configured-on-the-d-drive"></a>Durum 1: Disk belleği dosyası D: sürücüsünde yapılandırılmıştır
Disk yapılandırması aşağıdaki gibidir:


**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1 (Disk, korumanın dışında tutuldu) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Kaynak sanal makinedeki disk belleği dosyası ayarları şunlardır:

![Kaynak sanal makinedeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Sanal makinenin VMware’den Azure’a veya Hyper-V’den Azure’a yük devretmesi yapıldıktan sonra, Azure sanal makinesindeki diskler aşağıdaki gibi olur:

**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | Geçici depolama</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Disk1 (D:) dışarıda tutulduğundan, D: kullanılabilir listedeki ilk sürücü harfidir. Azure, geçici depolama birimine D: harfini atar. D: Azure sanal makinesinde kullanılabilir olduğundan, sanal makinenin disk belleği dosyası ayarı aynı kalır.

Azure sanal makinesindeki disk belleği dosyası ayarları şunlardır:

![Azure sanal makinesindeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-the-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Durum 2: Disk belleği dosyası başka bir sürücüde (D: sürücüsü dışında) yapılandırılmıştır

Kaynak sanal makine disk yapılandırması şöyledir:

**Disk adı** | **Konuk işletim sistemi disk no.** | **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | İşletim sistemi diski
DB-Disk1 (Disk, korumanın dışında tutuldu) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

Şirket içi sanal makinedeki disk belleği dosyası ayarları şunlardır:

![Şirket içi sanal makinedeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Sanal makinenin VMware’den/Hyper-V’den Azure’a yük devretmesi yapıldıktan sonra, Azure sanal makinesindeki diskler aşağıdaki gibi olur:

**Disk adı**| **Konuk işletim sistemi disk no.**| **Sürücü harfi** | **Diskteki veri türü**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |İşletim sistemi diski
DB-Disk1 | Disk1 | D:\ | Geçici depolama</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Kullanıcı verileri 1
DB-Disk3 | Disk3 | F:\ | Kullanıcı verileri 2

D: kullanılabilir sürücü harfleri listesindeki ilk harf olduğundan, Azure geçici depolama birimine D: harfini atar. Tüm çoğaltılan diskler için, sürücü harfi aynı kalır. G: disk kullanılabilir olmadığından, sistem disk belleği dosyası için C: sürücüsünü kullanır.

Azure sanal makinesindeki disk belleği dosyası ayarları şunlardır:

![Azure sanal makinesindeki disk belleği dosyası ayarları](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Sonraki adımlar
Dağıtımınız ayarlandıktan ve çalışmaya başladıktan sonra farklı türdeki yük devretmeler hakkında [daha fazla bilgi edinebilirsiniz](site-recovery-failover.md).

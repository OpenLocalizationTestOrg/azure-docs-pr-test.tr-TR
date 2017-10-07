---
title: "aaaAzure yedekleme sunucusu sistem durumu korur ve toobare metal yükler | Microsoft Docs"
description: "Azure yedekleme sunucusu tooback sistem durumu yedeklemesi kullanın ve tam kurtarma (BMR) koruması sağlar."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Sistem durumunu yedekleme ve Azure yedekleme sunucusu ile toobare geri yükleme

Azure yedekleme sunucusu sistem durumu yedeklemesi yedekler ve tam kurtarma (BMR) koruma sağlar.

*   **Sistem durumu yedeklemesi**: bilgisayar başlatıldığında, ancak sistem dosyalarını ve kayıt defteri hello kayboluyor kurtarmak için işletim sistemi dosyalarını yedekler. Bir sistem durumu yedeği içerir:
    * Etki alanı üyesi: önyükleme dosyaları, COM + sınıf kaydı veritabanı, kayıt defteri
    * Etki alanı denetleyicisi: Windows Server Active Directory (NTDS), önyükleme dosyaları, COM + sınıf kaydı veritabanı, kayıt defteri, sistem birimi (SYSVOL)
    * Küme hizmetlerini çalıştıran bilgisayar: küme sunucusu meta verilerini
    * Sertifika Hizmetleri çalıştıran bilgisayar: sertifika verileri
* **Tam yedekleme**: (kullanıcı veriler hariç) kritik birimlerdeki işletim sistemi dosyalarını ve tüm verileri yedekler. Tanımına göre bir BMR yedeklemesi bir sistem durumu yedeği içerir. Bir bilgisayar başlatılamıyor ve toorecover her şeyi koruma sağlar.

Aşağıdaki tablonun hello yedekleme ve kurtarma özetler. BMR ve sistem durumu ile korunan uygulama sürümleri hakkında ayrıntılı bilgi için bkz: [Azure yedekleme sunucusu yaptığı yedekleme?](backup-mabs-protection-matrix.md).

|Backup|Sorun|Azure yedekleme sunucusu yedeklemeden Kurtar|Sistem durumu yedeklemesinden kurtarma|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**Dosya verileri**<br /><br />Normal veri yedekleme<br /><br />BMR/sistem durumu yedeklemesi|Kayıp dosya verileri|E|N|N|
|**Dosya verileri**<br /><br />Dosya verileri Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Kayıp veya bozuk işletim sistemi|N|E|E|
|**Dosya verileri**<br /><br />Dosya verileri Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Kayıp sunucu (veri birimleri bozulmamış)|N|N|E|
|**Dosya verileri**<br /><br />Dosya verileri Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Kayıp sunucu (veri birimleri kayıp)|E|Hayır|Evet (yedeklenen dosya verilerinin normal kurtarması BMR'den)|
|**SharePoint verilerini**:<br /><br />Grup verilerini Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Kayıp site, listeler, liste öğelerini, belgeleri|E|N|N|
|**SharePoint verilerini**:<br /><br />Grup verilerini Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Kayıp veya bozuk işletim sistemi|N|E|E|
|**SharePoint verilerini**:<br /><br />Grup verilerini Azure yedekleme sunucusu yedeği<br /><br />BMR/sistem durumu yedeklemesi|Olağanüstü durum kurtarma|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Hyper-V ana bilgisayar veya konuk Azure yedekleme sunucusu yedekleme<br /><br />BMR/sistem durumu yedeklemesi konağının|Kayıp VM|E|N|N|
|Hyper-V<br /><br />Hyper-V ana bilgisayar veya konuk Azure yedekleme sunucusu yedekleme<br /><br />BMR/sistem durumu yedeklemesi konağının|Kayıp veya bozuk işletim sistemi|N|E|E|
|Hyper-V<br /><br />Hyper-V ana bilgisayar veya konuk Azure yedekleme sunucusu yedekleme<br /><br />BMR/sistem durumu yedeklemesi konağının|Kayıp Hyper-V Konağı (VM'ler bozulmamış)|N|N|E|
|Hyper-V<br /><br />Hyper-V ana bilgisayar veya konuk Azure yedekleme sunucusu yedekleme<br /><br />BMR/sistem durumu yedeklemesi konağının|Kayıp Hyper-V Konağı (VM'ler kayıp)|N|N|E<br /><br />Normal Azure yedekleme sunucusu kurtarma BMR'den|
|SQL Server/Exchange<br /><br />Azure yedekleme sunucusu uygulama yedekleme<br /><br />BMR/sistem durumu yedeklemesi|Kayıp uygulama verileri|E|N|N|
|SQL Server/Exchange<br /><br />Azure yedekleme sunucusu uygulama yedekleme<br /><br />BMR/sistem durumu yedeklemesi|Kayıp veya bozuk işletim sistemi|N|Y|E|
|SQL Server/Exchange<br /><br />Azure yedekleme sunucusu uygulama yedekleme<br /><br />BMR/sistem durumu yedeklemesi|Kayıp sunucu (veritabanı/işlem günlüklerini bozulmamış)|N|N|E|
|SQL Server/Exchange<br /><br />Azure yedekleme sunucusu uygulama yedekleme<br /><br />BMR/sistem durumu yedeklemesi|Kayıp sunucu (veritabanı/işlem günlüklerini kayıp)|N|N|E<br /><br />Normal Azure yedekleme sunucusu kurtarma tarafından izlenen BMR kurtarma|

## <a name="how-system-state-backup-works"></a>Sistem Durumu yedeğini nasıl çalışır

Bir sistem durumu yedeklemesi çalıştığında, yedekleme sunucusu ile Windows Server Yedekleme toorequest hello sunucunun sistem durumunun bir yedeğini iletişim kurar. Varsayılan olarak, yedekleme sunucusu ve Windows Server Yedekleme hello en fazla kullanılabilir boş alana sahip hello sürücü kullanın. Bu sürücü hakkında bilgi hello PSDataSourceConfig.xml dosyasına kaydedilir. Bu yedeklemeler için Windows Server Yedekleme kullanan hello sürücüdür.

Yedekleme sunucusu hello sistem durumu yedeklemesi için kullandığı hello sürücüyü özelleştirebilirsiniz. Korumalı hello sunucuda tooC:\Program Files\Microsoft veri koruma Manager\MABS\Datasources gidin. Merhaba PSDataSourceConfig.xml dosyasını düzenlemek için açın. Değişiklik hello \<Korunacakdosyalar\> hello sürücü harfi için değer. Merhaba dosyasını kaydedip kapatın. Varsa hello bilgisayarın tooprotect hello sistem durumunu koruma grubu ayarlayın, bir tutarlılık denetimi çalıştırın. Bir uyarı üretilir, seçin **koruma grubunu değiştir** hello uyarı ve ardından tam hello Sihirbazı'nda. Ardından, başka bir tutarlılık denetimi çalıştırın.

Merhaba koruma sunucu bir kümede ise, onu hello sürücü hello en fazla boş alana sahip olarak bir küme sürücüsünün seçilmiş olması olası olduğuna dikkat edin. Sürücü sahipliğinin anahtarlı tooanother düğümü bırakıldı ve bir sistem durumu yedeklemesinin çalışması durumunda hello sürücü kullanılamıyor ve hello yedekleme başarısız olur. Bu senaryoda, PSDataSourceConfig.xml toopoint tooa yerel sürücüsüne değiştirin.

Ardından, Windows Server Yedekleme hello hello geri yükleme klasörü kökünde WindowsImageBackup adında bir klasör oluşturur. Windows Server Yedekleme hello yedekleme oluşturduğu tüm hello veriler bu klasöre yerleştirilir. Merhaba Yedekleme tamamlandığında hello aktarılan toohello yedekleme sunucusu bilgisayar dosyasıdır. Aşağıdaki bilgilerle hello dikkat edin:

* Merhaba yedekleme veya aktarımı tamamlandığında, bu klasörü ve içeriği temizlenmesini değil. Bu en iyi şekilde toothink Hello hello alanı hello için bir yedekleme tamamlandıktan sonraki sefer ayrılan emin olur.
* bir yedekleme yapılan her zaman hello klasör oluşturulur. Merhaba saat ve tarih damgası, son sistem durumu yedeklemesi hello süresini yansıtır.

## <a name="bmr-backup"></a>BMR yedekleme

(Bir sistem durumu yedeklemesi dahil) BMR için hello yedekleme işi hello yedekleme sunucusu bilgisayarında tooa paylaşım doğrudan kaydedilir. Korumalı hello sunucuda tooa klasörü kaydedilmez.

Yedek sunucu Windows Server Yedekleme çağırır ve bu BMR yedekleme için çoğaltma birimi hello çıkışı paylaşır. Bu durumda, Windows Server Yedekleme toouse hello sürücü hello en fazla boş alana sahip bildirmez. Bunun yerine, oluşturulan hello paylaşımı hello işi için kullanır.

Merhaba Yedekleme tamamlandığında hello aktarılan toohello yedekleme sunucusu bilgisayar dosyasıdır. Günlükler, C:\Windows\Logs\WindowsServerBackup dizininde depolanır.

## <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar

-   BMR, Windows Server 2003 çalıştıran bilgisayarlar için veya bir istemci işletim sistemi çalıştıran bilgisayarlar için desteklenmiyor.

-   BMR koruyamaz ve sistem durumu Merhaba aynı bilgisayar farklı koruma gruplarındaki.

-   Bir yedekleme sunucusu bilgisayar kendisini BMR için korunamıyor.

-   BMR için kısa vadeli koruma tootape (diskin teyp veya D2T) desteklenmiyor. Uzun vadeli depolama tootape (disk-disk-için-banda veya D2D2T) desteklenir.

-   BMR koruma için Windows Server Yedekleme hello korumalı bilgisayara yüklenmesi gerekir.

-   BMR koruma için farklı sistem durumu koruması için yedekleme sunucusu herhangi bir alan gereksinimi hello korumalı bilgisayarda yok. Windows Server Yedekleme, yedekleme toohello yedekleme sunucusu bilgisayar doğrudan aktarır. Merhaba yedekleme aktarım işi hello yedekleme sunucusu görünmüyor **işleri** görünümü.

-   Yedekleme sunucusu, BMR için 30 GB alan hello çoğaltma biriminde saklı tutar. Bu üzerinde hello değiştirebilirsiniz **Disk ayırmayı** sayfasında hello koruma grubunu Değiştirme Sihirbazı'nı veya hello Get-DatasourceDiskAllocation ve Set-DatasourceDiskAllocation PowerShell cmdlet'lerini kullanarak. Merhaba kurtarma noktası birimde BMR koruması, beş gün bekletme için yaklaşık 6 GB gerektirir.
    * Merhaba çoğaltma birimi boyutu tooless 15 GB'tan olamayacağını unutmayın.
    * Yedek sunucu hello hello BMR veri kaynağının boyutunu hesaplamaz. Tüm sunucular için 30 GB olduğunu varsayar. Merhaba ortamınızda beklenen BMR yedeklemelerinin boyutuna göre hello değerini değiştirin. bir BMR yedeklemesi Hello boyutu kabaca tüm kritik birimlerdeki hello kullanılan alanın toplamı olarak hesaplanabilir. Kritik birimler = önyükleme birimi + sistem birimi + Active Directory gibi sistem durumu verilerini barındıran birim.

-   Sistem durumu koruması tooBMR korumasından değiştirirseniz, BMR koruması hello daha az alan gerektirir. *kurtarma noktası birimi*. Ancak, hello hello birimdeki ek alan geri alınmaz. El ile hello hello birim boyutunu küçültebilirsiniz **Disk ayırmayı Değiştir** sayfasında hello koruma grubunu Değiştirme Sihirbazı'nın veya hello Get-DatasourceDiskAllocation ve Set-DatasourceDiskAllocation PowerShell cmdlet'lerini kullanarak.

    Sistem durumu koruması tooBMR korumasından değiştirirseniz, BMR koruması hello hakkında daha fazla alan gerektiren *çoğaltma birimi*. Merhaba birim otomatik olarak genişletilir. Toochange hello varsayılan alan ayırmalarını istiyorsanız hello Modify-DiskAllocation PowerShell cmdlet'ini kullanın.

-   BMR koruması toosystem durumu korumasından değiştirirseniz, hello kurtarma noktası biriminde daha fazla alan gerekir. Yedekleme sunucusu tooautomatically artış hello birim deneyebilirsiniz. Merhaba depolama havuzunda yeterli alan yoksa hata oluşur.

    BMR koruması toosystem durumu korumasından değiştirirseniz, hello korumalı bilgisayardaki alan gerekir. Sistem durumu koruması ilk hello çoğaltma toohello yerel bilgisayar yazar ve toohello yedekleme sunucusu bilgisayar aktarır olmasıdır.

## <a name="before-you-begin"></a>Başlamadan önce

1.  **Azure Backup sunucusu dağıtmak**. Yedekleme sunucusu doğru şekilde dağıtıldığını doğrulayın. Daha fazla bilgi için bkz.
    * [Azure yedekleme sunucusu için sistem gereksinimleri](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Yedek sunucu koruma Matrisi](backup-mabs-protection-matrix.md)

2.  **Depolama ayarlama**. Diskte, bantta ve Azure ile Merhaba bulutta yedekleme verilerini depolayabilirsiniz. Daha fazla bilgi için bkz: [veri depolama alanı hazırlama](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Merhaba koruma aracısını ayarlama**. Merhaba koruma aracısını kurma tooback istediğiniz hello bilgisayara yükleyin. Daha fazla bilgi için bkz: [dağıtma hello DPM koruma Aracısı](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Sistem durumu ve tam yedekleme
Bölümünde açıklandığı gibi bir koruma grubu ayarlayın [koruma gruplarını dağıtmak](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). BMR koruyamaz ve sistem durumu Merhaba aynı Not farklı gruplardaki bilgisayar. Ayrıca, BMR'yi seçtiğinizde sistem durumu otomatik olarak etkinleştirilir.


1.  tooopen hello yeni koruma grubu oluşturma Sihirbazı'nda hello yedekleme Sunucu Yöneticisi konsolu, select **koruma** > **Eylemler** > **oluşturma koruma Grup**.

2.  Merhaba üzerinde **koruma grubu türünü seçin** sayfasında **sunucuları**ve ardından **sonraki**.

3.  Merhaba üzerinde **grup üyelerini seçin** sayfasında, hello bilgisayarı genişletin ve ardından ya da seçin **BMR** veya **sistem durumu**.

    Hello için BMR'yi ve sistem durumunu koruyamazsınız unutmayın farklı gruplarındaki aynı bilgisayar. Ayrıca, BMR'yi seçtiğinizde sistem durumu otomatik olarak etkinleştirilir. Daha fazla bilgi için bkz: [koruma gruplarını dağıtmak](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, nasıl toohandle kısa vadeli ve uzun vadeli yedekleme istediğinizi seçin. Kısa vadeli yedekleme her zaman toodisk önce Azure Backup (kısa veya uzun süreli) kullanarak hello seçeneği hello disk toohello ' Azure yedekleme ile bulut. Bir alternatif toolong vadeli yedekleme toohello bulut tooBackup sunucu bağlanan uzun vadeli yedekleme tooa tek başına bant aygıt veya bant kitaplığını yukarı tooset ' dir.

5.  Merhaba üzerinde **kısa vadeli hedefleri seçin** sayfasında, nasıl tooshort vadeli depolamayı disk üzerindeki tooback istediğinizi seçin:
    1. İçin **bekletme aralığı**, disk üzerindeki tookeep hello verileri ne kadar süreyle istediğinizi seçin. 
    2. İçin **eşitleme sıklığı**, ne sıklıkta toorun bir artımlı yedekleme toodisk istediğinizi seçin. Tooset yedekleme aralığını istemiyorsanız hello denetleyebilirsiniz **bir kurtarma noktasından hemen önce** seçeneği. Yalnızca her kurtarma noktası zamanlanmadan önce yedekleme sunucusu express, tam bir yedekleme çalıştırın.

6.  Merhaba, uzun vadeli depolama için bantta toostore verilerin istiyorsanız **uzun vadeli hedefleri belirtin** sayfasında, ne kadar süreyle tookeep bant verilerini (1-99 yıl) istediğinizi seçin. 
    1. İçin **yedekleme sıklığı**, yedekleme tootape çalışmalı ne sıklıkta seçin. Merhaba sıklığı seçtiğiniz hello bekletme aralığına dayalıdır:
        * Merhaba bekletme aralığı 1-99 yıl arası olduğunda, yedeklemelerin günlük, haftalık, iki haftada, aylık, üç aylık, altı aylık veya yıllık toooccur seçebilirsiniz.
        * Merhaba bekletme aralığı 1-11 ay arası olduğunda, yedeklemelerin günlük, haftalık, iki haftada veya aylık toooccur seçebilirsiniz.
        * Merhaba bekletme aralığı 1-4 hafta arası olduğunda, günlük veya haftalık yedeklemeler toooccur seçebilirsiniz.

    2. Merhaba üzerinde **bant ve kitaplık ayrıntılarını seçin** sayfası, select hello bant ve kitaplık toouse ve olup veri sıkıştırılmış şifrelenmiş.

7.  Merhaba üzerinde **Disk ayırmayı gözden** sayfasında, hello koruma grubu için ayrılmış hello depolama havuzu disk alanını gözden geçirin.

    1. **Toplam veri boyutu** yukarı tooback istediğiniz hello veri hello boyutudur.
    2. **Azure yedekleme sunucusu üzerinde sağlanan disk alanı toobe** hello koruma grubu için yedekleme sunucusu önerir hello alanıdır. Yedek sunucu hello ideal yedekleme birimi hello ayarlarınızı temel alan seçer. Ancak, hello yedekleme birimi seçenek düzenleyebilirsiniz **Disk ayırması ayrıntıları**. 
    3. İş yükleri için tercih edilen hello depolama hello açılır menüde seçin. Düzenlemeleriniz hello değerlerini değiştirmek **toplam depolama** ve **boş depolama** hello içinde **kullanılabilir Disk Depolama** bölmesi. Yedekleme sunucusu toohello birim, tooensure kesintisiz yedeklemeler eklemek öneren depolama hello miktarını underprovisioned alanıdır.

8.  Merhaba üzerinde **çoğaltma oluşturma yöntemini seçin** sayfasında, nasıl toohandle hello ilk tam veri çoğaltma istediğinizi seçin. Hello ağ üzerinden tooreplicate seçerseniz yoğun olmayan bir zamanı seçmeniz önerilir. Büyük miktarlarda veri veya en iyi durumda olmayan ağ koşulları için Çıkarılabilir medya kullanarak çevrimdışı hello veri çoğaltmayı düşünebilirsiniz.

9. Merhaba üzerinde **tutarlılık denetimi seçenekleri seçin** sayfasında, tooautomate tutarlılık denetimlerinin nasıl istediğinizi seçin. Yalnızca çoğaltma verileri tutarsız, veya bir zamanlamaya göre olduğunda bir onay toorun seçebilirsiniz. Tooconfigure otomatik tutarlılık denetimini istemiyorsanız, el ile denetim herhangi bir zamanda çalıştırabilirsiniz. toorun bir el ile denetleyin hello **koruma** hello yedekleme Sunucu Yöneticisi konsolu alanı hello koruma grubunun ve ardından sağ **tutarlılık denetimi gerçekleştir**.

10. Azure yedekleme, üzerinde hello kullanarak toohello bulut yukarı tooback seçtiyseniz **çevrimiçi koruma verilerini belirtin** sayfasında, tooback tooAzure yedeklemek istediğiniz hello iş yükleri seçtiğinizden emin olun.

11. Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, ne sıklıkta artımlı yedeklemeler tooAzure gerçekleşeceği seçin. Yedeklemeleri toorun her gün, hafta, ay ve yıl zamanlayabilir ve hangi çalışacakları başlangıç saati ve tarihi seçin. Yedekleme günde tootwice yukarı ortaya çıkabilir. Her bir yedekleme çalıştırılana bir veri kurtarma noktası Azure'da hello yedekleme sunucusu diskte depolanmış hello yedekleme verileri hello kopyasından oluşturulur.

12. Merhaba üzerinde **çevrimiçi bekletme ilkesini belirtin** sayfasında, Azure'da hello günlük, haftalık, aylık ve yıllık yedeklemelerden oluşturulan hello kurtarma noktaları nasıl korunur.

13. Merhaba üzerinde **seçin çevrimiçi çoğaltma** sayfasında, hello ilk tam veri çoğaltmasının nasıl gerçekleştiğini seçin. Merhaba ağ üzerinden çoğaltmasına veya çevrimdışı yapmak (çevrimdışı dengeli) yedekleme. Çevrimdışı Yedekleme hello Azure içeri aktarma özelliğini kullanır. Daha fazla bilgi için bkz: [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md).

14. Merhaba üzerinde **Özet** sayfasında, ayarlarınızı gözden geçirin. Siz seçtikten sonra **Grup Oluştur**, ilk hello veri çoğaltma işlemi gerçekleşir. Veri çoğaltma tamamlandığında, üzerinde hello **durum** sayfasıdır, hello koruma grubunun durumu **Tamam**. Yedekleme sonra başına hello koruma grubu ayarları gerçekleşir.

## <a name="recover-system-state-or-bmr"></a>Sistem durumu veya BMR kurtarma
BMR veya sistem durumu tooa ağ konumuna kurtarabilir. BMR'yi yedeklediyseniz, sisteminizi Windows Kurtarma Ortamı'nı (WinRE) toostart kullanın ve toohello ağ bağlanın. Ardından, Windows Server Yedekleme toorecover hello ağ konumundan kullanın. Yalnızca sistem durumunu yedeklediyseniz, Windows Server Yedekleme toorecover hello ağ konumundan kullanabilir.

### <a name="restore-bmr"></a>BMR'yi geri yükleme
Kurtarma hello yedekleme sunucusu bilgisayarda çalıştırın:

1.  Merhaba, **kurtarma** bölmesi, toorecover istediğiniz ve ardından Bul hello bilgisayar **tam kurtarma**.

2.  Kullanılabilir kurtarma noktaları gösterilir hello Takvim üzerinde kalın yazı. Toouse istediğiniz hello kurtarma noktası için başlangıç tarihi ve saati seçin.

3.  Merhaba üzerinde **kurtarma türünü seçin** sayfasında **tooa ağ klasörüne kopyala.**

4.  Merhaba üzerinde **hedef belirtin** toocopy hello verileri istediğiniz sayfasında, seçin. Bu hello seçili hedef toohave yeterli alan gerekiyor. unutmayın. Yeni bir klasör oluşturmanızı öneririz.

5.  Merhaba üzerinde **kurtarma seçeneklerini belirtin** sayfası, select hello güvenlik ayarları tooapply. Toouse depolama alanı ağı (SAN) istediğinizi seçin, ardından-daha hızlı kurtarma için donanım anlık görüntülerini tabanlı. (Yalnızca kullanılabilir, bu işlev bir SAN varsa ve yeteneği toocreate hello ve bir kopya toomake bölme bu bir seçenek ise, yazılabilir. İn addition, hello korumalı bilgisayar ve yedekleme sunucusu bilgisayar bağlı toohello olmalıdır aynı ağ.)

6.  Bildirim seçeneklerini ayarlayın. Merhaba üzerinde **onay** sayfasında, **kurtarmak**.

Hello paylaşım konumunu ayarlayın:

1.  Merhaba geri yükleme konumunda, hello yedekleme içeren toohello klasörüne gidin.

2.  Merhaba hello paylaşılan klasörün kökünde hello WindowsImageBackup klasörü; böylece bir düzeyi WindowsImageBackup yukarıda hello klasörü paylaşın. Bunu yapmazsanız, geri yükleme hello yedeği bulmaz. Windows Kurtarma Ortamı'nı (WinRE) kullanarak tooconnect oluşturulması hello doğru IP adresi ve kimlik bilgileriyle erişebileceğiniz bir paylaşımı gerekir.

Merhaba sistem geri yükleme:

1.  Toorestore hello görüntü hello sisteminizin geri yüklemekte olduğunuz hello Windows DVD'sini kullanarak istediğiniz hello bilgisayarınızı yeniden başlatın.

2.  Merhaba ilk sayfasında, dil ve yerel ayarları doğrulayın. Merhaba üzerinde **yükleme** sayfasında, **Bilgisayarınızı onarın**.

3.  Merhaba üzerinde **Sistem Kurtarma Seçenekleri** sayfasında, **daha önce oluşturduğunuz sistem görüntüsünü kullanarak bilgisayarınızı geri**.

4.  Merhaba üzerinde **sistem yansıması yedeği Seç** sayfasında **Sistem Görüntüsü Seç** > **Gelişmiş** > **bir sistem arayın Görüntü hello ağdaki**. Bir uyarı görünürse seçin **Evet**. Toohello yoluna gidin, hello kimlik bilgilerini girin ve ardından hello kurtarma noktasını seçin. Bu, Kurtarma noktasında kullanılabilir belirli yedeklemelerinize tarar. Toouse istediğiniz hello kurtarma noktası seçin.

5.  Merhaba üzerinde **nasıl toorestore hello yedekleme seçin** sayfasında, **diskleri Biçimlendir ve yeniden bölümle**. Merhaba sonraki sayfasında, ayarları doğrulayın. 

6.  toobegin hello geri yükleme, select **son**. Yeniden başlatma gereklidir.

### <a name="restore-system-state"></a>Sistem durumunu geri yükle

Kurtarma, yedekleme sunucusunda çalıştırın:

1.  Merhaba, **kurtarma** bölmesinde, toorecover istediğiniz ve ardından Bul hello bilgisayar **tam kurtarma**.

2.  Kullanılabilir kurtarma noktaları gösterilir hello Takvim üzerinde kalın yazı. Toouse istediğiniz hello kurtarma noktası için başlangıç tarihi ve saati seçin.

3.  Merhaba üzerinde **kurtarma türünü seçin** sayfasında **kopyalama tooa ağ klasörüne**.

4.  Merhaba üzerinde **hedef belirtin** toocopy hello veri istediğiniz sayfasında, seçin. Bu hello seçilen hedef yeterli alan gereken unutmayın. Yeni bir klasör oluşturmanızı öneririz.

5.  Merhaba üzerinde **kurtarma seçeneklerini belirtin** sayfası, select hello güvenlik ayarları tooapply. Ardından, toouse SAN tabanlı donanım anlık görüntülerini daha hızlı kurtarma için isteyip istemediğinizi seçin. (Yalnızca bu işlev bir SAN varsa ve yeteneği toocreate hello ve bir kopya toomake bölme bu bir seçenek ise, yazılabilir. İn addition, hello korumalı bilgisayar ve yedekleme sunucusu bağlı toohello olmalıdır aynı ağ.)

6.  Bildirim seçeneklerini ayarlayın. Merhaba üzerinde **onay** sayfasında, **kurtarmak**.

Windows Server Yedekleme çalıştırın:

1.  Seçin **Eylemler** > **kurtarmak** > **bu sunucu** > **sonraki**.

2.  Seçin **başka bir sunucuya**seçin hello **konum türünü belirtin** sayfasında ve ardından **uzaktan paylaşılan klasörünü**. Merhaba kurtarma noktası içeren hello yolu toohello klasörü girin.

3.  Merhaba üzerinde **kurtarma türünü seçin** sayfasında **sistem durumu**. 

4. Merhaba üzerinde **sistem durumu kurtarma için konum seçin** sayfasında **özgün konumuna**.

5.  Merhaba üzerinde **onay** sayfasında, **kurtarmak**. Merhaba geri yüklendikten sonra hello sunucuyu yeniden başlatın.

6.  Bir komut isteminde hello sistem durumu geri yüklemesi de çalıştırabilirsiniz. toodo Bu, başlangıç Windows Server Yedekleme hello bilgisayarda toorecover istiyor. bir komut isteminde tooget hello sürüm tanımlayıcı girin:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Merhaba sürüm tanımlayıcısı toostart hello sistem durumu geri kullanın. Merhaba komut isteminde girin:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Toostart hello kurtarma istediğinizi onaylayın. Merhaba işlem hello komut istemi penceresinde görebilirsiniz. Geri yükleme günlüğü oluşturulur. Merhaba geri yüklendikten sonra hello sunucuyu yeniden başlatın.


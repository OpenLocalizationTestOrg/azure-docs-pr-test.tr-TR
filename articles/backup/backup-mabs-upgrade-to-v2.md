---
title: Azure yedekleme sunucusu v2 aaaInstall | Microsoft Docs
description: "Azure yedekleme sunucusu v2, VM'ler, dosyalar ve klasörler, iş yükleri ve daha fazla korunması için geliştirilmiş yedekleme özellikleri sunar. Bilgi nasıl tooinstall veya yükseltme tooAzure yedekleme sunucusu v2."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Azure Backup sunucusu v2 yükleyin

Azure yedekleme sunucusu sanal makineleri (VM'ler), iş yükleri, dosyaları ve klasörleri ve daha fazla korunmasına yardımcı olur. Azure yedekleme sunucusu v2 üzerinde Azure yedekleme sunucusu v1 oluşturur ve v1 kullanılabilir değil yeni özellikleri sağlar. Özellikler v1 ve v2 arasındaki karşılaştırması için bkz: [Azure yedekleme sunucusu koruma matris](backup-mabs-protection-matrix.md). 

Merhaba ek yedekleme sunucusu v2 olarak yedekleme sunucusu v1'den yükseltme özellikleridir. Ancak, yedekleme sunucusu v1 yedekleme sunucusu v2 yüklemek için bir önkoşul değil. Yedekleme sunucusu v1 tooBackup sunucu v2'den tooupgrade istiyorsanız, yedekleme sunucusu v2 hello yedekleme sunucusu koruma sunucusuna yükleyin. Var olan yedekleme sunucusu ayarlarınızı değişmeden kalır.

Windows Server 2012 R2 veya Windows Server 2016 yedekleme sunucusu v2 yükleyebilirsiniz. yeni özelliklerden tootake ister System Center 2016 veri koruma Yöneticisi Modern yedekleme depolama, Windows Server 2016 yedekleme sunucusu v2 yüklemeniz gerekir. Tooor yükleme yedekleme sunucusu v2 yükseltmeden önce hello hakkında okuyun [yükleme önkoşulları](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Azure yedekleme sunucusu hello sahip System Center Data Protection Manager olarak temel aynı kodu. Yedek sunucu v1 eşdeğer tooData Protection Manager 2012 R2 ve yedekleme sunucusu v2 eşdeğer tooData Protection Manager 2016 şeklindedir. Bu makalede, bazen hello Data Protection Manager belge başvurur.
>
>

## <a name="upgrade-backup-server-toov2"></a>Yedekleme sunucusu toov2 yükseltme
Yedekleme sunucusu v1 tooBackup sunucu v2'den tooupgrade hello gerekli güncelleştirmeleri yüklemenizi sahip olduğundan emin olun:

- [Merhaba koruma aracılarını güncelleştirme](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) üzerinde hello korumalı sunucuları.
- Windows Server 2012 R2 tooWindows Server 2016 yükseltin.
- Azure yedekleme sunucusu uzak yönetici tüm üretim sunucularında yükseltin.
- Üretim sunucunuzu yeniden başlatmanıza gerek kalmadan yedeklemeleri toocontinue ayarlandığından emin olun.


### <a name="upgrade-steps-for-backup-server-v2"></a>Yedekleme sunucusu v2 yükseltme adımları

1. Merhaba İndirme Merkezi olarak [hello yükseltme yükleyici indirmek](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Merhaba Kurulum Sihirbazı'nı ayıkladıktan sonra olduğundan emin olun **setup.exe yürütme** seçili ve ardından **son**.

  ![Kurulum Yükleyici - Çalıştır kurulum](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. Merhaba Microsoft Azure Yedekleme Sunucusu Sihirbazı'nda altında **yükleme**seçin **Microsoft Azure yedekleme sunucusu**.

  ![Kurulum Yükleyici - Select yükleme](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Merhaba üzerinde **Hoş Geldiniz** sayfasında hello uyarılarını gözden geçirin ve ardından **sonraki**.

  ![Kurulum Yükleyici - Karşılama sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Merhaba Kurulum Sihirbazı'nı önkoşul denetimleri toomake ortamınızı yükseltebilirsiniz emin gerçekleştirir. Merhaba üzerinde **önkoşul denetler** sayfasında, **denetleyin**.

  ![Kurulum Yükleyici - önkoşul denetler sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. Ortamınız önkoşul denetimleri hello geçmesi gerekir. Ortamınızı hello denetimleri geçmiyor hello sorunlara dikkat edin ve düzeltin. Ardından, seçin **yeniden denetle**. Merhaba önkoşul denetimlerini geçemedi sonra seçin **sonraki**.

  ![Kurulum Yükleyici - yeniden denetle düğmesi](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Merhaba üzerinde **SQL ayarlarını** sayfasında hello SQL yüklemeniz için ilgili seçeneği seçin ve ardından **denetle ve Yükle**.

  ![Kurulum Yükleyici - SQL Ayarları sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  Merhaba denetimleri birkaç dakika sürebilir. Tamamlanan, select hello denetimleri olduğunda **sonraki**.

  ![Kurulum Yükleyici - SQL ayarlarını denetleyin ve Yükle düğmesini](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Merhaba üzerinde **yükleme ayarları** sayfasında, yedekleme sunucusu yüklü olduğu herhangi bir değişiklik toohello konumu ya da toohello karalama konumu olun. Seçin **sonraki**.

  ![Kurulum Yükleyici - yükleme ayarları sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello Kurulum Sihirbazı'nı seçin **son**.

  ![Kurulum Yükleyici - bitiş](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Modern yedekleme depolama için depolama ekleme

tooimprove yedekleme depolama verimliliği, yedekleme sunucusuna v2 birimler için destek ekler. Yedekleme sunucusu v1 gibi yedekleme sunucusu v2 diskleri destekler.

### <a name="add-volumes-and-disks"></a>Birimler ve diskleri ekleme
Windows Server 2016 yedekleme sunucusu v2 çalıştırırsanız, birimleri toostore yedekleme verilerini kullanabilirsiniz. Birimleri depolama alanından tasarruf etmenizi ve daha hızlı yedekleme sunar. Birimleri yeni tooBackup sunucusu olduğundan, bunları eklemeniz gerekir. 

Bir birim tooBackup sunucusu eklediğinizde, hello birim kolay bir ad verin. Merhaba tıklatın **kolay ad** sütun hello hacmi tooname istiyor. Gerekirse, hello adı daha sonra değiştirebilirsiniz. Ayrıca PowerShell tooadd kullanın veya birimler için kolay adlar değiştirebilirsiniz.

Merhaba Yönetici Konsolu biriminde tooadd:

1. Hello Azure yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **Disk Depolama** > **Ekle**.

    ![Açık hello Disk Depolama Alanı Ekle Sihirbazı](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Merhaba Disk Depolama Alanı Ekle Sihirbazı açılır.

2. Merhaba üzerinde **Disk Depolama Alanı Ekle** sayfasında hello **kullanılabilir birimleri** kutusunda, bir birim seçin ve ardından **Ekle**.
3. Merhaba, **seçili birimleri** kutusuna hello birim için kolay bir ad girin ve ardından **Tamam**.

      ![Disk depolama alanı Ekle Sihirbazı - birim ekleme](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Tooadd bir disk istiyorsanız hello disk eski depolama olan tooa koruma grubuna ait olmalıdır. Bu diskleri yalnızca bu koruma grupları için kullanılabilir. Yedekleme sunucusu eski koruma kaynakları yoksa, hello disk listelenmiyor.

  Diskleri ekleme hakkında daha fazla bilgi için bkz: [diskleri tooincrease eski depolama ekleme](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). Kolay bir ad bir disk veremez.


### <a name="assign-workloads-toovolumes"></a>İş yükleri toovolumes atayın

Yedekleme Server'da hangi iş yüklerini toowhich birimleri atanan belirtin. Örneğin, çok sayıda sık, yüksek hacimli yedeklemeler gerektiren ikinci (IOPS) toostore yalnızca iş yükleri başına girdi/çıktı işlemleri destekleyen pahalı birimler ayarlayabilirsiniz. SQL Server ile işlem günlükleri örneğidir.

#### <a name="update-dpmdiskstorage"></a>Güncelleştirme DPMDiskStorage

Yedekleme sunucusu hello depolama havuzundaki bir birimin tooupdate hello özelliklerini hello PowerShell cmdlet'ini güncelleştirme DPMDiskStorage kullanın.

Sözdizimi:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

PowerShell kullanarak yaptığınız tüm değişiklikler hello UI yansıtılır.


## <a name="protect-data-sources"></a>Veri kaynaklarını korumak
veri kaynaklarını koruma toobegin, bir koruma grubu oluşturun. adımları Vurgu değişiklikler veya eklemeler toohello yeni koruma grubu Sihirbazı'nı aşağıdaki hello.

bir koruma grubu toocreate:

1. Hello yedekleme Sunucu Yöneticisi konsolu, seçin **koruma**.

2. Merhaba araç şeridinde seçin **yeni**.

    Merhaba yeni koruma grubu oluşturma Sihirbazı açılır.

  ![Yeni koruma grubu oluşturma Sihirbazı](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Merhaba üzerinde **Hoş Geldiniz** sayfasında, **sonraki**.
4. Merhaba üzerinde **koruma grubu türünü seçin** sayfasında, hello toocreate istediğiniz ve ardından koruma grubu türünü seçin **sonraki**.

  ![Koruma grubu seç türü sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Merhaba üzerinde **grup üyelerini seçin** sayfasında hello **kullanılabilir üyeler** bölmesinde, koruma aracılarını listelenen hello üyeleriyle. Bu örnekte, D:\ birimi seçin ve E:\ ve bunları toohello Ekle **seçili üyeleri** bölmesi. Seçin **sonraki**.

  ![Grup Seç üyeleri sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Merhaba üzerinde **veri koruma yöntemini seçin** want bir **koruma grubu adı**hello koruma yöntemini seçin ve ardından **sonraki**. Kısa vadeli koruma istiyorsanız hello seçmelisiniz **Disk** yedekleme yöntemi.

  ![Veri koruma yöntemini sayfa seçin](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfası, select hello ayrıntılarını **bekletme aralığı** ve **eşitleme sıklığı**. Ardından, seçin **sonraki**. Kurtarma noktalarının ne zaman çekildiği, select için isteğe bağlı olarak, toochange hello zamanlama **Değiştir**.

  ![Kısa vadeli hedefleri sayfasında belirtin](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Merhaba üzerinde **Disk Depolaması ayırmasını gözden** sayfasında, seçtiğiniz hello veri kaynakları ile ilgili ayrıntıları, boyutu ve sağlanan hello alanı toobe değerleri gözden geçirin ve hello hedef depolama birimi.

  ![Gözden geçirme Disk Depolaması ayırması sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Depolama birimleri hello iş yükü birim ayırma (PowerShell kullanarak ayarlayın) dayanır ve kullanılabilir depolama alanı hello. Merhaba depolama birimleri hello açılan menüsünde diğer birimleri'i seçerek değiştirebilirsiniz. Merhaba değeri değiştirirseniz **hedef depolama**, hello için değer **kullanılabilir disk depolama** altında tooreflect değerleri dinamik olarak değişir **boş alan** ve **Underprovisioned alanı**.

  Merhaba veri kaynakları planlı olarak büyüyecek, hello için değer hello **Underprovisioned alanı** sütununda **kullanılabilir disk depolama** hello gerekli olan ek depolama alanı miktarını gösterir. Bu değer toohelp planı kesintisiz yedeklemeler için depolama alanı ihtiyaçlarınızı kullanın. Merhaba değer sıfırsa hello öngörülebilir gelecekte depolama alanı hiçbir olası sorunları vardır. Merhaba değer sıfır dışındaki bir sayı ise, ayrılmış yeterli depolama alanı yok (sizin koruma İlkesi ve hello veri boyutuna, korumalı üyeleri göre).

  ![Eksik yüklenmiş disk depolama](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   koruma grubu, tam hello Sihirbazı'nı oluşturma toofinish.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Eski depolama tooModern yedekleme depolama geçirme
Yedekleme sunucusu v2 tooor yükleme ve yükseltme hello işletim sistemi tooWindows Server 2016 yükselttikten sonra koruma grupları toouse Modern yedekleme depolama güncelleştirin. Varsayılan olarak, koruma grupları değiştirilmez. Bunlar başlangıçta kurulmuş gibi toofunction devam eder. 

Koruma grupları toouse Modern yedekleme depolama güncelleştirme isteğe bağlıdır. hello kullanarak tüm veri kaynaklarının korumasını durdurun tooupdate hello koruma grubu, veri seçeneği korur. Ardından, hello veri kaynakları tooa yeni koruma grubu ekleyin.

1. Hello Yöneticisi konsolu, hello seçin **koruma** özelliği. Merhaba, **koruma grubu üyesi** listesinde, hello üye sağ tıklayın ve ardından **üyenin korumasını Durdur**.

  ![Üyenin korumasını Durdur](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. Merhaba, **grubundan** iletişim kutusu, gözden geçirme hello kullanılan disk alanı ve hello kullanılabilir boş alanı hello depolama havuzu için. Hello varsayılan tooleave hello kurtarma noktaları hello diskteki ve bunların ilişkili bekletme ilkesi başına tooexpire izin. **Tamam** düğmesine tıklayın.

  Merhaba tooimmediately dönüş hello kullanılan disk alanı toohello boş depolama havuzunu istiyorsanız seçin **diskteki çoğaltmayı Sil** onay kutusu toodelete hello yedekleme verileri (ve kurtarma noktaları) Bu üye ile ilişkili.

  ![Grup iletişim kutusundan Kaldır](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Modern yedekleme depolama kullanan bir koruma grubu oluşturun. Merhaba korunmayan veri kaynaklarını içerir.


## <a name="add-disks-tooincrease-legacy-storage"></a>Diskleri tooincrease eski depolama ekleme

Yedekleme sunucusu ile toouse eski depolama istiyorsanız tooadd diskleri tooincrease eski depolama gerekebilir. 

tooadd disk depolaması:

1. Hello Yöneticisi konsolu, seçin **Yönetim** > **Disk Depolama** > **Ekle**.

    ![Disk depolama iletişim ekleyin](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. Merhaba, **Disk Depolama Alanı Ekle** iletişim kutusunda **eklemek diskleri**.

5. Kullanılabilir diskler Hello listesinde tooadd, select istediğiniz hello diskleri seçin **Ekle**ve ardından **Tamam**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Merhaba Data Protection Manager koruma aracısını güncelleştirin

Yedek sunucu hello System Center Data Protection Manager koruma Aracısı güncelleştirmeleri için kullanır. Bağlı toohello ağ bir koruma Aracısı yükseltme yapıyorsanız, hello Data Protection Manager Yönetici Konsolu toocomplete bağlı aracı yükseltme kullanamazsınız. Etkin olmayan etki alanı ortamında hello koruma aracısını yükseltmeniz gerekir. Merhaba istemci bilgisayara bağlı toohello ağ olana kadar bu hello koruma Aracısı güncelleştirmesi Data Protection Manager Yönetici Konsolu gösterilir hello beklemede.

Merhaba aşağıdaki bölümlerde nasıl tooupdate koruma aracılarını bağlı istemci bilgisayarları ve bağlı olmayan istemci bilgisayarlar için.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Bağlantılı bir istemci bilgisayarda koruma aracısını güncelleştir

1. Hello yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **aracıları**.

2. Merhaba görüntü bölmesinde tooupdate hello koruma Aracısı istediğiniz hello istemci bilgisayarları seçin.

  > [!NOTE]
  > Merhaba **aracı güncelleştirmeleri** sütun gösteren bir koruma Aracısı güncelleştirmesi her korumalı bilgisayar için kullanılabilir olduğunda. Merhaba, **Eylemler** bölmesi, hello **güncelleştirme** eylem, yalnızca korumalı bir bilgisayarın seçili olduğundan ve kullanılabilir güncelleştirmeler olduğunda kullanılabilir.
  >
  >

3. tooinstall koruma aracılarını hello içinde hello seçili bilgisayarlara güncelleştirilmiş **Eylemler** bölmesinde, **güncelleştirme**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Bağlı olmayan bir istemci bilgisayarda koruma aracısını güncelleştirin

1. Hello yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **aracıları**.

2. Merhaba görüntü bölmesinde tooupdate hello koruma Aracısı istediğiniz hello istemci bilgisayarları seçin.

  > [!NOTE]
   > Merhaba **aracı güncelleştirmeleri** sütun gösteren bir koruma Aracısı güncelleştirmesi her korumalı bilgisayar için kullanılabilir olduğunda. Merhaba, **Eylemler** bölmesi, hello **güncelleştirme** eylemi kullanılabilir değil korumalı bir bilgisayar seçildiğinde kullanılabilir güncelleştirme yoksa.
  >
  >

3. tooinstall koruma aracılarını select hello seçili bilgisayarlara güncelleştirilmiş **güncelleştirme**.

4. Merhaba bilgisayar bağlı toohello ağ kadar toohello ağ olmayan bir istemci bilgisayara bağlı için hello **aracı durumu** sütun durumunu gösterir **güncelleştirme Beklemede**.

  Bir istemci bilgisayara bağlı toohello ağ sonra hello **aracı güncelleştirmeleri** sütun hello istemci bilgisayar için bir durumu gösterir **güncelleştirme**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Eski sürümünü ve Azure ile eşitleme hello yeni sürümü eski koruma grupları taşıma

Azure yedekleme sunucusu ve hello işletim sistemi hem de güncelleştirilmiştir verdikten sonra hazır tooprotect Modern yedekleme depolama kullanarak yeni veri kaynakları demektir. Ancak zaten korumalı veri kaynakları şekilde Azure yedekleme sunucusu olan, ancak tüm yeni koruması Modern yedekleme depolama kullanacak şekilde hello eski korumalı toobe devam eder.

Aşağıdaki adımları toomigrate veri koruma tooModern yedekleme depolama eski modundan kaynaklarıdır.

• Hello yeni birimlerin toohello DPM depolama havuzu ekleyin ve isterseniz kolay adlarını ve veri kaynağı etiketleri atayın.
• Eski modda durdurma hello veri kaynakları ve "Korumalı verileri Koru" olan her veri kaynağı için.  Bu kurtarma eski kurtarma noktaları geçişten sonra olanak tanır.

• Yeni PG oluşturun ve yeni biçimi kullanarak depolanan toobe olan hello veri kaynaklarını seçin.
• DPM Modern yedekleme depolama birimi yerel olarak hello hello eski yedekleme depolama biriminden çoğaltma kopyasını yapın.
Not: Bu görülür tüm yeni eşitleme ve kurtarma noktalarını sonra Modern yedekleme depolama alanında depolanacak kurtarma sonrası işlemi iş • olarak.
Süresi dolacak ve sonunda hello disk alanını boşaltmanız • eski kurtarma noktalarını kullanıma ayıklanır.
Tüm hello eski birimleri hello eski depolama biriminden, hello disk silindikten sonra • Azure yedekleme ve hello sistemden kaldırılabilir.
• Hello Azure DPMDB yedeklemesini alın.

2. Kısım:-Önemli öğeleri > merhaba yeni sunucu, aynı adlı hello özgün Azure yedekleme sunucusu toobe gerekir. Toouse eski depolama havuzu istiyorsanız ve DPMDB tooretain kurtarma noktaları - geri toobe ihtiyaç duyacağınız DPMDB yedeklemesini olmalıdır hello yeni Azure yedekleme sunucusu hello adı değiştirilemiyor

1) Kapatma özgün Azure yedekleme sunucusu hello veya devre dışı hello kablo alır.
2) Merhaba makine hesabının active Directory'de sıfırlayın.
3) Yeni bir makine ve hello özgün Azure yedekleme sunucusu olarak aynı makine adı hello adı Server 2016 yükleyin.
4) Merhaba etki alanına katılma
5) Azure yedekleme sunucusu V2 yükleyin (taşıma DPM depolama havuzu diskleri eski sunucu ve içeri aktarma)
6) Merhaba Kısım 2 sonundan itibaren geçen DPMDB geri yükleme
7) Merhaba depolama hello özgün yedekleme sunucusu toohello yeni sunucudan ekleyin.
8) DPMDB hello SQL geri yükleme
9) Yönetici komut satırından yeni sunucu cd tooMicrosoft Azure yedekleme konumu ve depo klasörüne yükleyin

Yol örnek: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
tooAzure yedekleme çalıştırmak DPMSYNC-SYNC

10) Dpmsync aracını çalıştırın-eşitleme Not hello eskilerle, taşıma yerine yeni diskler toohello DPM depolama havuzu eklediyseniz ardından çalıştırın DPMSYNC - reallocatereplica öğesini

## <a name="new-powershell-cmdlets-in-v2"></a>V2 yeni PowerShell cmdlet'leri

Azure yedekleme sunucusu v2 yüklediğinizde, iki yeni cmdlet'leri kullanılabilir: 
* [Bağlama DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Çıkarma DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak:
- [Yedekleme sunucusu iş yükleri hazırlama](backup-azure-microsoft-azure-backup.md)
- [Bir VMware sunucusu yedekleme sunucusu tooback kullanın](backup-azure-backup-server-vmware.md)
- [SQL Server Yedekleme Sunucusu tooback kullanın](backup-azure-sql-mabs.md)
- [Yedekleme sunucusu ile modern yedekleme depolama alanı kullanın](backup-mabs-add-storage.md)


---
title: "Azure tooon içi VMware sanal makinelerini aaaFailback | Microsoft Docs"
description: "VMware Vm'lerini ve fiziksel sunucuları tooAzure yük devretme sonrasında geri toohello şirket içi site başarısız hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Geri VMware sanal makineleri ve fiziksel sunucuları toohello şirket içi site başarısız


Bu makalede nasıl toofailback Azure sanal makineleri Azure toohello şirket içi siteden. Merhaba yönergeleri burada hazır olduğunuzda toofail geri VMware sanal makineleri veya Windows veya Linux fiziksel sunucuları bu kullanarak makinelerinizi yeniden koruduktan sonra [başvuru](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Merhaba Klasik Azure portalını kullanıyorsanız, Lütfen belirtilen tooinstructions başvurun [burada](site-recovery-failback-azure-to-vmware-classic.md) Gelişmiş VMware tooAzure mimarisi için ve [burada](site-recovery-failback-azure-to-vmware-classic-legacy.md) hello eski mimari

## <a name="overview"></a>Genel Bakış
Bu bölümdeki Hello diyagramları hello geri dönme mimarisi bu senaryo için gösterir.

Merhaba işlem sunucusu şirket içi ve Azure ExpressRoute bağlantısı kullanarak bu mimarinin kullanın:

![ExpressRoute için mimarisi diyagramı](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Azure ve üzerinde işlem sunucusudur hello olduğunda bir VPN ya da bu mimarisi kullanan bir ExpressRoute bağlantısı:

![VPN mimarisi diyagramı](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Bağlantı noktaları ve hello geri dönme mimarisi diyagramı tam listesi için görüntü aşağıdaki toohello bakın:

![Yük devretme yeniden çalışma tüm bağlantı noktalarının listesi](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

TooAzure başarısız sonra üç aşamada geri tooyour şirket içi site başarısız olur:

* **Aşama 1**: şirket içi sitenizi çalıştıran arka toohello VMware Vm'lerini çoğaltma başlatılması hello Azure Vm'leri koruyun.
* **Aşama 2**: Azure Vm'leriniz çoğaltılmış tooyour şirket içi site olduktan sonra bir yük devretme toofail geri Azure'dan çalıştırın.
* **3. Aşama**: verilerinizi geri başarısız oldu sonra böylece bunlar tooAzure çoğaltma işlemi başlatma, başarısız şirket içi sanal makineleri yedeklemek için hello koruyun.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Geri toohello özgün konuma veya alternatif bir konuma başarısız
VMware VM başarısız olduktan sonra geri toohello edilemeyebilir aynı kaynak VM hala şirket içi varsa. Bu senaryoda, yalnızca hello farkları geri başarısız olan.

Fiziksel sunucuları üzerinde başarısız oldu, yeniden çalışma her zaman tooa ise yeni VMware VM. Geri başarısız olan bir fiziksel makine önce dikkat edin:
* Bu geri Azure tooVMware devredildiğinde korumalı bir fiziksel makine bir sanal makine olarak geri gelecektir. Korumalı ise ve tooAzure, başarısız bir Windows Server 2008 R2 SP1 fiziksel makine geri başarısız olamaz. Bir sanal makine şirket içi olarak başlatılan bir Windows Server 2008 R2 SP1 makine mümkün toofail geri olacaktır.
* En az bir ana hedef sunucusu bulma olun toofail gereken gerekli ESX/ESXi konaklarının dön hello yanı sıra.

Geri toohello başarısız olursa özgün VM hello aşağıdaki gereklidir:

* Merhaba VM bir vCenter sunucusu tarafından yönetiliyorsa, hello ana hedefin ESX konak erişim toohello VM'ler veri deposu olması gerekir.
* Merhaba VM bir ESX konağında olduğu, ancak vCenter tarafından yönetilmiyor hello hello sabit diskin VM hello MT'ın ana bilgisayar tarafından erişilebilen bir veri deposu olması gerekir.
* VM'yi bir ESX konağında ise ve vCenter kullanmaz, koruyun önce hello MT, hello ESX konağının bulma tamamlamanız gerekir. Geri fiziksel sunucuları çok çalıştırma işlemini gerçekleştiriyorsanız bu geçerlidir.
* Toodelete (Merhaba VM mevcut şirket içi ise) başka bir seçenek olan bir yeniden çalışma bunu önce. Yeniden çalışma sonra yeni bir VM hello hello ana hedef ESX konağı olarak aynı ana bilgisayar oluşturur.

Geri tooan alternatif bir konum başarısız olduğunda hello kurtarılan toohello verilerdir aynı veri deposu ve hello aynı ESX konak hello şirket içi ana hedef sunucusu tarafından kullanılan olarak.

## <a name="prerequisites"></a>Ön koşullar
* toofail geri VMware Vm'lerini ve fiziksel sunucuları, bir VMware ortamı gerekir. Başarısız olan geri tooa fiziksel sunucu desteklenmiyor.
* koruma ayarlama başlangıçta ayarladığınızda geri toofail, size bir Azure ağı oluşturmuş olmanız gerekir. Yeniden çalışma hello Azure VPN ya da ExpressRoute bağlantı gereken ağ içinde hello Azure VM'ler için bulunduğu toohello şirket içi site.
* Merhaba toofail istediğiniz sanal makineleri bir vCenter sunucusu tarafından yönetilen tooare yedeklerseniz, VM'ler bulma vCenter sunucuları üzerinde hello gerekli izinlere sahip olduğundan emin olun. Daha fazla bilgi için bkz: [çoğaltmak VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile](site-recovery-vmware-to-azure-classic.md).
* Bir VM anlık görüntüler varsa, yükü başarısız olur. Merhaba anlık görüntülere veya hello diskleri silebilirsiniz.
* Geri dönecek önce bu bileşenlerin oluşturun:
  * **Bir işlem sunucusu oluşturma**. Oluşturun ve yeniden çalışma sırasında çalışmaya devam bir Azure VM bileşendir. Yeniden çalışma işlemi tamamlandıktan sonra hello VM silebilirsiniz.
  * **Bir ana hedef sunucusu oluşturmak**: hello ana hedef sunucusuna gönderir ve yeniden çalışma verilerini alır. Şirket içi oluşturulan hello yönetim sunucusu varsayılan olarak yüklenen bir ana hedef sunucusu vardır. Ancak, başarısız geri trafik hacmi hello bağlı olarak, toocreate ayrı ana hedef sunucusu yeniden çalışma için gerekebilir.
  * toocreate Linux üzerinde çalışan bir ek ana hedef sunucusu, daha sonra açıklandığı gibi hello ana hedef sunucusu yüklemeden önce Linux VM hello ayarlayın.
* Bir yeniden çalışma işlemi yaptığınızda yapılandırma şirket içi sunucusudur. Yeniden çalışma sırasında hello sanal makine hello yapılandırma sunucusu veritabanında mevcut olması gerekir. Merhaba yapılandırma sunucusu veritabanı hiçbir VM içeriyorsa, yeniden çalışma başarısız olması. Bu nedenle, sunucunuzun düzenli zamanlanmış yedeklemeler yaptığınızdan emin olun. Bir olağanüstü durumda toorestore gereksinim duyduğunuz aynı IP adresi geri dönme işleminin çalıştığı şekilde hello ile.
* Merhaba disk.enableUUID=true ayarı kümesinde **yapılandırma parametrelerini** VMware VM hello ana hedef. Bu satır mevcut değilse, bunu ekleyin. Bu ayar gerekli tooprovide tutarlı evrensel benzersiz tanımlayıcı (UUID) toohello sanal makine disk (VMDK) dosyasını, böylelikle doğru şekilde oluşturulmuş.
* Haberdar bir "ana hedef sunucu, depolama vMotioned olamaz" Merhaba geri dönme toofail neden olabilir koşulu. Merhaba diskleri kullanılabilir tooit yapılan değil çünkü hello VM çıkarılamıyor.
* Bir bekletme sürücüye hello ana hedef sunucusu adı verilen bir sürücü ekleyin. Bir disk ekleyip hello sürücüyü biçimlendirin.

## <a name="failback-policy"></a>Yeniden çalışma ilkesi
tooreplicate geri tooon içi yeniden çalışma ilkesi gerekir. Hello İlkesi, bir iletme yönü ilkesi oluşturduğunuzda ve hello yapılandırma sunucusu ile otomatik olarak ilişkilendirilir otomatik olarak oluşturulur. Düzenlenebilir değil. Hello ilkenin hello çoğaltma ayarları aşağıdaki gibidir:

* RPO eşiği = 15 dakika
* Kurtarma noktası bekletme = 24 saat
* Uygulama ile tutarlı anlık görüntü sıklığı = 60 dakika

 ![Merhaba geri dönme ilkesini çoğaltma ayarları](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Azure'da bir işlem sunucusu kurma
Böylece Hello Azure VM'ler hello veri geri toohello şirket içi ana hedef sunucusu gönderebilir Azure'da bir işlem sunucusu yükleyin.

Korunan Klasik kaynaklar olarak, sanal makine varsa (yani, VM kurtarılan Azure'da hello hello Klasik dağıtım modeli kullanılarak oluşturulmuş bir VM olan) Azure işlem sunucusu gerekir. Merhaba VM'ler hello dağıtım türü olarak Azure Resource Manager ile kurtardı, hello işlem Sunucusu Kaynak Yöneticisi'ni hello dağıtım türü olarak olması gerekir. Merhaba dağıtım türünün seçili hello Azure tarafından dağıttığınız sanal ağ hello işlem sunucusuna.

1. İçinde **kasa** > **ayarları** > **Site Recovery altyapısı** (altında **yönetmek**) > **Yapılandırma sunucularına** (altında **için VMware ve fiziksel makineleri**), select hello yapılandırma sunucusu.
2. Tıklatın **işlem sunucusu**.

  ![İşlem sunucusu düğmesi](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Toodeploy seçin işlem sunucusu olarak hello **yeniden çalışma işlem sunucusu azure'da dağıtmak**.
4. Merhaba VM'ler kurtardı hello aboneliği seçin.
5. Merhaba hello VM'ler kurtardı Azure ağını seçin. Merhaba işlem sunucusu aynı hello VM'ler kurtarıldı ve hello işlem sunucusu iletişim kurabilir ağ hello toobe gerekir.
6. Seçtiyseniz, bir *Klasik dağıtım modeli* ağ, hello Azure Market üzerinden bir VM oluşturun ve içine hello işlem sunucusu yükleyin.

 ![Merhaba "İşlem Sunucu Ekle" penceresi](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Merhaba işlem sunucusu oluşturuyorsanız gibi dikkat toohello aşağıdaki ödeme:
 * Merhaba görüntü Hello adıdır *Microsoft Azure Site kurtarma işlemi Server V2*. Seçin **Klasik** hello dağıtım modeli olarak.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Merhaba işlem sunucusu according toohello yönergeleri yüklemek [çoğaltmak VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile](site-recovery-vmware-to-azure-classic.md).
7. Merhaba seçerseniz *Resource Manager* Azure ağ, aşağıdaki bilgilerle hello sağlayarak hello işlem sunucusu Dağıt:

  * Merhaba toodeploy hello sunucuya istediğiniz hello kaynak grubunun adını
  * Merhaba sunucusunun Hello adı
  * Bir kullanıcı adı ve parola toohello Server'da imzalama
  * toodeploy hello sunucuya istediğiniz hello depolama hesabı
  * Merhaba alt ağı ve tooconnect tooit istediğiniz hello ağ arabirimi
   >[!NOTE]
   >Kendi oluşturmalısınız [ağ arabirimi](../virtual-network/virtual-networks-multiple-nics.md) (NIC) ve hello işlem sunucusu dağıtırken seçin.

    ![Bilgi hello "İşlem Sunucu Ekle" iletişim kutusuna girin](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. **Tamam** düğmesine tıklayın. Bu eylemin hello işlem Sunucusu Kurulum sırasında bir Resource Manager dağıtım türü sanal makine oluşturan bir işi tetikler. tooregister hello sunucu toohello yapılandırma sunucusu, çalışma hello Kurulum içinde hello yönergeleri takip ederek VM hello [çoğaltmak VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile](site-recovery-vmware-to-azure-classic.md). Bir iş toodeploy hello işlem sunucusu da tetiklenir.

  Merhaba işlem sunucusu üzerinde hello listelenen **yapılandırma sunucularına** > **sunucular ilişkilendirilen** > **işlem sunucuları** sekmesi.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Merhaba işlem sunucusu altında görünmeyen **VM özelliklerini**. Yalnızca hello üzerinde görünürdür **sunucuları** için kayıtlı hello yönetim sunucusu sekmesindedir. Merhaba işlem sunucusu tooappear 10 too15 dakika sürebilir.


## <a name="set-up-hello-master-target-server-on-premises"></a>Merhaba ana hedef sunucusu şirket içi ayarlayın
Merhaba ana hedef sunucusu hello geri dönme veri alır. Hello sunucusu hello şirket içi yönetim sunucusunda otomatik olarak yüklenir, ancak çok fazla veri yeniden çalıştırma işlemini gerçekleştiriyorsanız, ek ana hedef sunucusu tooset gerekebilir. Asıl yukarı tooset şirket içi server hedeflemek için aşağıdaki hello:

> [!NOTE]
> Linux üzerinde bir ana hedef sunucusu tooset toohello bir sonraki yordamı atlayın. Yalnızca CentOS 6.6 en düşük işletim sistemi ana hedef işletim sistemi hello olarak kullanın.

1. Windows hello ana hedef sunucusunda ayarlıyorsanız, hello üzerinde hello ana hedef sunucusu yüklüyorsanız VM gelen hello hızlı başlangıç sayfasını açın.
2. Hello Azure Site kurtarma birleşik Kurulum Sihirbazı'nı Hello yükleme dosyasını indirin.
3. Merhaba Kurulumu'nu çalıştırın ve buna **başlamadan önce**seçin **dağıtım out ek işlem sunucuları tooscale eklemek**.
4. Merhaba tam hello sihirbazında ne zaman yaptığınız aynı şekilde, [hello yönetimi sunucusunu ayarlama](site-recovery-vmware-to-azure-classic.md). Merhaba üzerinde **yapılandırma sunucusu ayrıntılarını** sayfasında hello ana hedef sunucusunun hello IP adresi belirtin ve bir parola tooaccess hello VM girin.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Bir Linux VM hello ana hedef sunucusu olarak ayarla
Merhaba ana hedef sunucusunda bir Linux VM çalışan hello yönetim sunucusu tooset hello CentOS 6.6 en düşük işletim sistemi yükleyin. Ardından, hello her SCSI sabit disk için SCSI kimliklerini almak, bazı ek paketler yükleme ve özel bazı değişiklikler uygulanır.

#### <a name="install-centos-66"></a>CentOS 6.6 yükleyin

1. Merhaba CentOS 6.6 en düşük işletim sistemi hello yönetim sunucusuna VM yükleyin. Bir DVD sürücüsünde ISO Hello tutmak ve hello sistem önyüklemesi. Medya Hello sınama atlayın. Seçin **ABD İngilizcesi** hello dili olarak seçin **temel depolama aygıtları**, sabit sürücü hello onay herhangi bir önemli veri yoksa, tıklatın **Evet**ve herhangi bir veri atın. Merhaba hello yönetim sunucusunun ana bilgisayar adını girin ve hello sunucu ağ bağdaştırıcısı seçin.  Merhaba, **düzenleme sistem** iletişim kutusunda **otomatik olarak bağlan**ve ardından statik bir IP adresi, ağ ve DNS ayarlarını ekleyin. Bir saat dilimini belirtin. tooaccess hello yönetim sunucusu hello kök parolasını girin.
2. Hangi tür yükleme istediğiniz sorulduğunda, seçin **oluşturma özel yerleşim** hello bölüm olarak. **İleri**’ye tıklayın. Seçin **serbest**ve ardından **oluşturma**. Oluşturma  **/** , **/var/kilitlenme**, ve **/ev bölümleri** ile **FS türü:** **ext4**. Merhaba takas bölümü olarak oluşturma **FS türü: takas**.
3. Önceden var olan aygıtları bulunursa, bir uyarı iletisi görüntülenir. Tıklatın **biçimi** tooformat hello sürücüyle hello bölüm ayarları. Tıklatın **yazma değiştirme toodisk** tooapply hello bölüm değişiklikleri.
4. Seçin **yükleme önyükleyici** > **sonraki** tooinstall hello önyükleyici hello kök bölüm üzerinde.
5. Merhaba yüklemesi tamamlandıktan sonra tıklatın **yeniden**.

#### <a name="retrieve-hello-scsi-ids"></a>Merhaba SCSI kimlikleri alma

1. Hello yüklendikten sonra hello hello VM her SCSI sabit disk için SCSI kimlikleri alma. toodo, bu nedenle, hello yönetim sunucusunu VM kapatın. VMware içinde Hello VM Özellikleri'nde hello VM girişi sağ tıklatın > **ayarlarını Düzenle** > **seçenekleri**.
2. Seçin **Gelişmiş** > **genel öğesi**ve ardından **yapılandırma parametreleri**. Merhaba makine çalışıyorsa, bu seçenek kullanılamaz. Merhaba seçeneği toobe için kullanılabilir, hello makine kapatılmalıdır.
3. Merhaba aşağıdakilerden birini yapın:
 * Merhaba, satır **disk. EnableUUID** yoksa, hello değeri çok ayarlandığından emin olun**True** (büyük küçük harf duyarlı). Hello değeri tooTrue zaten ayarlanmışsa iptal edin ve onu önyüklendiğinde sonra hello SCSI komutu bir konuk işletim sistemi içinde test edin.
 * Merhaba, satır **disk. EnableUUID** mevcut değil, tıklatın **Satır Ekle**ve ile Merhaba ekleyin **True** değeri. Çift tırnak işaretleri kullanmayın.

#### <a name="install-additional-packages"></a>Ek paket yüklemek için
Ek paket yükleyip yeniden açın.

1. Bağlı toohello Internet Hello ana hedef sunucusu olduğundan emin olun.
2. toodownload ve hello CentOS depodan yükleme 15 paketler bu komutu çalıştırın: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Hello kaynak makineleri koruyorsanız Reiser ile Linux çalıştıran veya XFS dosya sistemi hello kök veya önyükleme aygıtı için indirin ve ek paketleri aşağıdaki gibi yükleyin:

   * \#CD /usr/local
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \#RPM – ivh reiserfs 0,0 1.el6.elrepo.x86_64.rpm kmod reiserfs-yardımcı programları-3.6.21-1.el6.elrepo.x86_64.rpm
   * \#wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \#RPM – ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum aygıt Eşleyici çok yollu (Merhaba ana hedef sunucusunda çok yollu paketleri gerekli tooenable) yükleyin

#### <a name="apply-custom-changes"></a>Özel Değişiklikleri Uygula
Merhaba yükleme sonrası adımları ve yüklü hello paketleri tamamladıktan sonra hello aşağıdakileri yaparak özel değişiklikleri uygulayın:

1. Merhaba RHEL 6-64 birleşik aracı ikili toohello VM kopyalayın. toountar hello ikili, bu komutu çalıştırın: `tar –zxvf <file name>`.
2. toogive izinleri, bu komutu çalıştırın: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Çalışma hello betik aşağıdaki: `# ./ApplyCustomChanges.sh`. Çalıştırın yalnızca bir kez. Başarıyla çalıştıktan sonra hello sunucusunu yeniden başlatın.

## <a name="run-hello-failback"></a>Merhaba yeniden çalıştır
### <a name="reprotect-hello-azure-vms"></a>Hello Azure Vm'leri koruyun
1. İçinde **kasa**, **öğeleri çoğaltılan**hello üzerinden başarısız VM sağ tıklayın ve ardından **yeniden koruma**.
2. Merhaba dikey penceresinde, bu koruma hello yönünü görebilirsiniz **Azure tooOn içi** zaten seçilidir.
3. İçinde **ana hedef sunucusu** ve **işlem sunucusu**hello şirket içi ana hedef sunucusunu seçin ve Azure VM işlem sunucusu hello.
4. Select hello veri deposu toorecover hello diskleri istediğiniz şirket içi. Merhaba VM silinir ve toocreate yeni diskler gerek şirket içi olduğunda bu seçeneği kullanın. Merhaba seçeneği göz ardı hello diskleri zaten var, ancak yine de toospecify bir değer gerekir.
5. Bir bekletme sürücü toostop hello noktaları hello VM çoğaltılmış geri tooon içi olduğunda zamanında kullanın. Saklama sürücüsünün bazı ölçütü burada listelenir. Bu ölçütler hello sürücü hello ana hedef sunucusu için listelenmeyen.

  * Birim, başka bir amaç için (hedef çoğaltma ve benzeri) kullanımda olmamalıdır.
  * Birim kilit modunda olmamalıdır.
  * Birim önbellek birimi olmamalıdır. (Merhaba ana hedef yükleme bu birimde mevcut döndürmemelidir. İşlem sunucusu artı ana hello hedef özel yükleme birimi bekletme birimi için uygun değil. Burada, işlem sunucusu hello yüklü artı hello önbellek birimi hello ana hedefinin ana hedef birimdir.)
  * Merhaba birim dosya sistemi türü, FAT ve FAT32 olmamalıdır.
  * Merhaba birim kapasitesi sıfır olmalıdır.
  * Windows Hello varsayılan saklama biriminin R birimdir.
  * Merhaba varsayılan saklama Linux için /mnt/retention birimdir.

6. Merhaba geri dönme ilkesini otomatik olarak seçilir.
7. Tıklattıktan sonra **Tamam** toobegin yükü, bir iş tooreplicate hello Azure toohello şirket içi siteden VM başlar. Merhaba üzerinde hello ilerleme durumunu izleyebilirsiniz **işleri** sekmesi.

Toorecover tooan alternatif bir konum istiyorsanız hello bekletme sürücüsü ve hello ana hedef sunucu için yapılandırılmış veri deposu seçin. Geri toohello şirket içi site başarısız olduğunda hello VMware Vm'lerini hello geri dönme koruma planı kullanmak hello hello ana hedef sunucusu olarak aynı veri deposu. Toorecover hello çoğaltma Azure VM toohello istiyorsanız aynı şirket içi VM, hello şirket içi VM zaten olması içinde hello aynı veri deposu hello ana hedef sunucusu olarak. Hiçbir VM içi varsa, yeni bir yükü sırasında oluşturulur.

!["Azure tooon içi" Merhaba açılır menüde seçin](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Ayrıca, bir kurtarma planı düzeyde koruyun. Bir çoğaltma grubu varsa, yalnızca bir kurtarma planı kullanarak koruyun. Bir kurtarma planı kullanarak koruyun, hello önceki değerleri korunan her makine için kullanın.

> [!NOTE]
> Çoğaltma grupları yeniden hello ile korunan aynı ana hedefi. Farklı bir ana hedef sunucularla korunuyorsa kendileri için bir ortak bir noktaya belirlenemiyor.

### <a name="run-a-failover-toohello-on-premises-site"></a>Bir yük devretme toohello şirket içi siteyi çalıştırın
Merhaba VM koruyun sonra Azure tooon içi bir yük devretme işlemi başlatabilirsiniz.

1. Merhaba çoğaltılan öğeler sayfasında hello sanal makineye sağ tıklayın ve ardından **planlanmamış yük devretme**.
2. İçinde **onaylayın yük devretme**hello yük devretme yönünden (Azure) doğrulayın ve ardından hello için yük devretme (son hello veya hello en son uygulamayla tutarlı kurtarma noktası) toouse istediğiniz hello kurtarma noktasını seçin. Bir uygulama tutarlı bir kurtarma noktası süre önce en son noktası hello oluşur ve bazı veri kaybına neden olur.
3. Yük devretme sırasında Site Recovery hello Azure VM'ler kapatır. Bu geri dönme beklendiği gibi tamamlanmış denetledikten sonra hello Azure VM'ler beklendiği gibi kapatılmışsa tooensure kontrol edebilirsiniz.

### <a name="reprotect-hello-on-premises-site"></a>Merhaba şirket içi site koruyun
Yeniden çalışma tamamladıktan sonra sanal makineleri Azure'da kurtarılan hello yürütme hello sanal makine tooensure silinir. toodo bu nedenle, korumalı hello öğeyi sağ tıklatın ve ardından **yürütme**. Bu eylemin hello eski kurtarılan sanal makine Azure'da kaldıran bir işi tetikler.

Hello yürütme tamamlandıktan sonra verilerinizi geri hello şirket içi sitede olmalıdır, ancak korunan olmaz. toostart çoğaltma tooAzure yeniden hello aşağıdaki:

1. İçinde **kasa**, **ayarı** > **öğeleri çoğaltılan**, geri başarısız olmuş ve ardından hello VM'ler seçin **yenidenkoruma**.
2. Merhaba kullanılan toobe toosend veri tooAzure gerektiren bir işlem sunucusu Hello değerini verir.
3. **Tamam** düğmesine tıklayın.

Merhaba yükü tamamlandıktan sonra geri tooAzure hello VM yinelenir ve bir yük devretme yapabilirsiniz.

### <a name="resolve-common-failback-issues"></a>Yeniden çalışma ile ilgili genel sorunları giderin
* Salt okunur kullanıcı vCenter bulma işlemini ve sanal makineleri koruma, başarılı ve yük devretme çalışır. Merhaba datastores bulunan için yükü sırasında yük devretme başarısız olur. Bir belirti yükü sırasında listelenen hello datastores görmezsiniz. tooresolve Bu sorun, izinlere sahip uygun bir hesap ile Merhaba vCenter kimlik bilgileri güncelleştirmek ve hello işi yeniden deneyin. Daha fazla bilgi için bkz: [çoğaltmak VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile](site-recovery-vmware-to-azure-classic.md)
* Bir Linux VM yeniden çalışmak ve şirket içi çalıştırın, o hello ağ yöneticisi paket hello makineden kaldırıldı görebilirsiniz. Azure'da Hello VM kurtarıldığında hello ağ yöneticisi paket kaldırıldığı bu kaldırma işlemi gerçekleşir.
* Bir VM tooAzure üzerinde başarısız oldu ve statik IP adresiyle yapılandırılmış olduğunda, başlangıç IP adresi DHCP yoluyla alınır. Geri tooon içi başarısız olduğunda hello VM toouse DHCP tooacquire başlangıç IP adresi devam eder. El ile toohello makinede oturum açın ve gerekirse, başlangıç IP adresi geri tooa statik adresi ayarlayın.
* ESXi 5.5 ücretsiz sürüm veya 6 vSphere hiper yönetici ücretsiz sürümü kullanıyorsanız, yük devretme başarılı, ancak yeniden çalışma başarısız. tooenable geri dönme, yükseltme tooeither program'ın değerlendirme lisansı.
* Merhaba işlem sunucusunun yapılandırma sunucusundan hello bağlanamazsa, bağlantı toohello yapılandırma sunucusu bağlantı noktası 443 üzerinden Telnet toohello yapılandırma sunucu makinesi tarafından kontrol edin. Merhaba işlem sunucusu makine tooping hello yapılandırma sunucusundan da deneyebilirsiniz. Bağlı toohello yapılandırma sunucusu olduğunda bir işlem sunucusu bir sinyal de olmalıdır.
* Toofail geri tooan alternatif vCenter çalışıyorsanız, yeni bulunduğundan ve bu hello ana hedef sunucusu ayrıca bulunduğundan emin olun. Tipik bir belirti hello datastores erişilebilir veya hello görünür olmamasıdır **koruyun** iletişim kutusu.
* Fiziksel makine şirket içi gibi korunan bir WS2008R2SP1 makine geri Azure tooon içi başarısız olamaz.

## <a name="fail-back-with-expressroute"></a>ExpressRoute ile başarısız
ExpressRoute bağlantısı kullanarak veya bir VPN bağlantısı üzerinden geri başarısız olabilir. Toouse ExpressRoute bağlantısı istiyorsanız hello aşağıdakilere dikkat edin:

* Merhaba ExpressRoute bağlantısı hello hello kaynak makinelerden tooand başarısız Azure sanal ağı üzerinde hello Azure VM'ler bulunduğu hello yük devretme gerçekleştikten sonra ayarlanmalıdır.
* Çoğaltılmış tooan genel bir uç nokta Azure depolama hesabı verilerdir. toouse bir ExpressRoute bağlantı kümesi ortak de ExpressRoute hello hedef veri merkezi Site Recovery çoğaltma ile eşleme ayarlama.

---
title: aaaFail Azure'dan VMware Vm'lerini hello Klasik portalda geri | Microsoft Docs
description: "VMware Vm'lerini ve fiziksel sunucuları tooAzure yük devretme sonrasında geri toohello şirket içi site başarısız hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Geri VMware sanal makineleri ve fiziksel sunucuları toohello şirket içi site (Klasik portalı) başarısız
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klasik Azure Portalı](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klasik Azure portalı (eski)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Bu makaleler nasıl toofail geri Azure sanal makineleri Azure toohello şirket içi siteden açıklar. Toofail hazır olduğunuzda, bu makaledeki hello yönergeleri izleyin, VMware sanal makineleri veya Windows/Linux fiziksel sunucuları bunlar hello şirket içi site tooAzure bu kullanarak devredilir sonra geri [Öğreticisi](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Genel Bakış
Bu senaryo için hello geri dönme mimarisi Bu diyagramda gösterilmektedir.

Bu mimari, şirket içi hello işlem sunucusu olduğunda ve bir expressroute bağlantı kullandığınız kullanın.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Bu mimari, Azure'da hello işlem sunucusu olduğunda ve bir VPN ya da ExpressRoute bağlantısı sahip olduğunuz kullanın.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

toosee hello tam listesi bağlantı noktaları ve hello geri dönme mimarisi diyagramı bakın aşağıdaki toohello görüntü

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Yeniden çalışma şeklini aşağıda verilmiştir:

* TooAzure başarısız sonra birkaç aşamada geri tooyour şirket içi site başarısız olur:
  * **Aşama 1**: şirket içi sitenizdeki çalıştıran arka tooVMware Vm'lerini çoğaltma başlatılması hello Azure Vm'leri koruyun. Yükü etkinleştirme hello VM başlangıçta hello yük devretme koruma grubu oluşturduğunuzda, otomatik olarak oluşturulan bir yeniden çalışma koruma grubuna taşınır. Yük devretme koruma grubu tooa kurtarma planı eklediyseniz hello geri dönme koruma grubu da otomatik olarak toohello planı eklendi.  Yeniden koruma sırasında nasıl tooplan toofail geri belirtin.
  * **Aşama 2**: Azure Vm'leriniz tooyour şirket içi siteye çoğaltma yapıyorsanız sonra bir hata toofail yeniden çalıştırın.
  * **3. Aşama**: verilerinizi geri başarısız oldu sonra böylece bunlar tooAzure çoğaltma işlemi başlatma, başarısız şirket içi sanal makineleri yedeklemek için hello koruyun.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Yeniden çalışma toohello özgün veya alternatif konumu
VMware VM başarısız olursa geri toohello edilemeyebilir aynı kaynak VM hala şirket içi varsa. Bu senaryoda yalnızca hello delta değişiklikleri geri başarısız. Şunlara dikkat edin:

* Fiziksel sunucuları üzerinde başarısız sonra yeniden çalışma alanındaki her zaman tooa yeni VMware VM.
  * Fiziksel makine geri başarısız olmadan önce unutmayın
  * Fiziksel makine korumalı üzerinden geri Azure tooVMware başarısız olduğunda bir sanal makine olarak geri gelir
  * En az bir ana hedef sunucusu hello gerekli ESX/ESXi konakları toowhich birlikte Bul olun toofailback gerekir.
* Geri başarısız olursa toohello özgün VM hello aşağıdakiler gereklidir:

  * Merhaba VM bir vCenter sunucusu tarafından yönetiliyorsa hello ana hedefin ESX konak erişim toohello VM'ler veri deposu olması gerekir.
  * Merhaba VM bir ESX konağında ancak vCenter tarafından yönetilmeyen hello hello sabit diskin hello MT'ın ana bilgisayar tarafından erişilebilir bir veri VM olmalıdır.
  * VM'yi bir ESX konağında ise ve vCenter kullanmaz, koruyun önce hello MT hello ESX konağının keşfinin tamamlamanız gerekir. Geri fiziksel sunucuları çok çalıştırma işlemini gerçekleştiriyorsanız bu geçerlidir.
  * Toodelete (Merhaba VM mevcut şirket içi ise) başka bir seçenek olan bir yeniden çalışma bunu önce. Daha sonra yeniden çalışma sonra yeni bir VM aynı hello ana hedef ESX konağına hello oluşturun.
* Ne zaman yeniden çalışma tooan alternatif bir konum hello verileri olacaktır kurtarılan toohello aynı veri deposu ve hello aynı ESX konak hello şirket içi ana hedef sunucusu tarafından kullanılan olarak.

## <a name="prerequisites"></a>Ön koşullar
* Sipariş toofail geri VMware Vm'lerini ve fiziksel sunucuları VMware ortamında gerekir. Başarısız olan geri tooa fiziksel sunucu desteklenmiyor.
* Koruma ayarlama başlangıçta ayarladığınızda sipariş toofail geri, bir Azure ağı oluşturmuş olmalıdır. Yeniden çalışma hello Azure VPN ya da ExpressRoute bağlantı gereken ağ içinde hello Azure VM'ler için bulunduğu toohello şirket içi site.
* Merhaba VM'ler toofail geri tooare bir vCenter sunucusu tarafından yönetilen istiyorsanız toomake VM'ler bulma vCenter sunucuları üzerinde hello gerekli izinlere sahip olduğundan emin gerekir. [Daha fazla bilgi edinin](site-recovery-vmware-to-azure-classic.md).
* Bir VM anlık görüntüler varsa yükü başarısız olur. Merhaba anlık görüntülere veya hello diskleri silebilirsiniz.
* Geri dönecek önce toocreate bir dizi bileşen gerekir:
  * **Bir işlem sunucusu oluşturma**. Bir Azure toocreate gerekir ve yeniden çalışma sırasında çalışmaya devam VM budur. Yeniden çalışma işlemi tamamlandıktan sonra hello makine silebilirsiniz.
  * **Bir ana hedef sunucusu oluşturmak**: hello ana hedef sunucusuna gönderir ve yeniden çalışma verilerini alır. Şirket içi oluşturulan hello yönetim sunucusu varsayılan olarak yüklenen bir ana hedef sunucusu vardır. Ancak, başarısız geri trafik hacmi hello bağlı olarak toocreate ayrı ana hedef sunucusu yeniden çalışma için gerekebilir.
  * Linux üzerinde çalışan bir ek ana hedef sunucusu toocreate istiyorsanız, aşağıda açıklandığı gibi hello ana hedef sunucusu yüklemeden önce hello Linux VM yukarı tooset gerekir.
* Yapılandırma sunucusu şirket içi olduğunda bir yeniden çalışma yapın. Yeniden çalışma sırasında hello sanal makine yapılandırma sunucusu veritabanı paylaşmıyor hangi geri dönme başarılı başarısız hello'nda mevcut olması gerekir. Bu nedenle normal zamanlanmış yedekleme sunucunuzun ele emin olun. Olağanüstü bir durumda toorestore gerekir durumda hello ile aynı IP adresi böylece geri dönme çalışır.

## <a name="set-up-hello-process-server-in-azure"></a>Azure'da hello işlem sunucusunu ayarlama
Böylece Hello Azure VM'ler hello veri geri tooon içi ana hedef sunucusu gönderebilir tooinstall Azure işlem sunucusu gerekir.

1. Merhaba Site Recovery portalında > **yapılandırma sunucularına** tooadd yeni bir işlem sunucusu seçin.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. İşlem sunucusu adını belirtin ve bir ad ve bir yönetici olarak tooconnect toohello Azure VM kullanacağınız parola girin. İçinde **yapılandırma sunucusu** hello şirket içi yönetim sunucusunu seçin ve hello Azure belirtin ağ hangi hello işlem sunucusu dağıtılmalıdır. Bu hello Azure Vm'lerde bulunan hello ağ olmalıdır. Merhaba select alt ağdan benzersiz bir IP adresi belirtin ve dağıtım başlayın.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Bir iş toodeploy hello işlem sunucusu tetiklenir

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Merhaba sonra belirttiğiniz hello kimlik bilgilerini kullanarak oturum Azure işlem sunucusu dağıtılır. Merhaba hello işlem sunucusu iletişim kutusunda oturum ilk kez çalışır. Hello hello şirket içi yönetim sunucusu ve onun parola IP adresini yazın. Merhaba varsayılan 443 numaralı bağlantı noktası ayarını bırakın. Merhaba şirket içi yönetimi sunucusunu ayarlama ayarladığınızda, bu ayar özellikle değiştiren sürece, hello veri çoğaltma için varsayılan 9443 bağlantı noktası bırakabilirsiniz.

   > [!NOTE]
   > Merhaba sunucu altında görünür olmayacak **VM özelliklerini**. Yalnızca hello altında görünür **sunucuları** onu kayıtlı hello yönetim sunucusu toowhich sekmesinde. İlgili sürebilir hello işlem sunucusu tooappear için 10-15 dakika.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Merhaba ana hedef sunucusu şirket içi ayarlayın
Merhaba ana hedef sunucusu hello geri dönme veri alır. Bir ana hedef sunucusu hello şirket içi yönetim sunucusunda otomatik olarak yüklenir ancak çok miktarda veri yeniden çalıştırma işlemini gerçekleştiriyorsanız ek ana hedef sunucusu tooset gerekebilir. Bunu şu şekilde yapabilirsiniz:

> [!NOTE]
> Tooinstall Linux ana hedef sunucusunda istiyorsanız hello sonraki yordamda hello yönergeleri izleyin.
>
>

1. Windows hello ana hedef sunucusu yüklüyorsanız, üzerinde hello ana hedef sunucusu yüklüyorsanız ve hello Azure Site kurtarma birleşik Kurulum Sihirbazı'nı hello yükleme dosyasını indirin hello VM'den hello hızlı başlangıç sayfasını açın.
2. Kur'u çalıştırın ve **başlamadan önce** seçin **ek işlem sunucuları tooscale dağıtım çıkışı eklemek**.
3. Merhaba tam hello sihirbazında ne zaman yaptığınız aynı şekilde, [hello yönetimi sunucusunu ayarlama](site-recovery-vmware-to-azure-classic.md). Merhaba üzerinde **yapılandırma sunucusu ayrıntılarını** sayfasında, bu ana hedef sunucu ve bir parola tooaccess hello VM hello IP adresini belirtin.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Bir Linux VM hello ana hedef sunucusu olarak ayarla
tooset bir Linux VM tooinstall hello Sent gerekir hello ana hedef sunucusu çalıştıran hello yönetim sunucusu) S 6.6 en düşük işletim sistemi, hello her SCSI sabit disk için SCSI kimliklerini almak, bazı ek paketler yükleme ve özel bazı değişiklikler uygulanır.

#### <a name="install-centos-66"></a>CentOS 6.6 yükleyin
1. Merhaba CentOS 6.6 en düşük işletim sistemi hello yönetim sunucusuna VM yükleyin. Merhaba ISO bir DVD sürücüsü ve önyükleme hello sistemi tutun. Test, Atla hello medyayı seçin ABD İngilizcesi hello dil desteğini, select **temel depolama aygıtları**, sabit sürücü hello onay herhangi önemli verilere sahip değil ve tıklatın **Evet**, tüm verileri at. Merhaba hello yönetim sunucusunun ana bilgisayar adını girin ve hello sunucu ağ bağdaştırıcısı seçin.  Merhaba, **düzenleme sistem** iletişim seçin ** bağlanmak otomatik olarak ** ve statik bir IP adresi, ağ ve DNS ayarlarını ekleyin. Bir saat dilimi ve bir kök parola tooaccess hello yönetim sunucusu belirtin.
2. Ne zaman sorulan hello yükleme türünü seç istediğinizi **oluşturma özel yerleşim** hello bölüm olarak. Tıklattıktan sonra **sonraki** seçin **serbest** Oluştur'u tıklatın. Oluşturma  **/** , **/var/kilitlenme** ve **/ev bölümleri** ile **FS türü:** **ext4**. Merhaba takas partion olarak oluşturma **FS türü: takas**.
3. Önceden var olan aygıtları bulunursa bir uyarı iletisi görüntülenir. Tıklatın **biçimi** tooformat hello sürücüyle hello bölüm ayarları. Tıklatın **yazma değiştirme toodisk** tooapply hello bölüm değişiklikleri.
4. Seçin **yükleme önyükleyici** > **sonraki** tooinstall hello önyükleyici hello kök bölüm üzerinde.
5. Yükleme tamamlandığında tıklatın **yeniden**.

#### <a name="retrieve-hello-scsi-ids"></a>Merhaba SCSI kimlikleri alma
1. Yükleme sonrasında hello hello VM her SCSI sabit disk için SCSI kimlikleri alma. toodo, bu bilgisayarı hello yönetim sunucusu VM, hello VM VMware özelliklerinde hello VM girişi sağ tıklatın > **ayarlarını Düzenle** > **seçenekleri**.
2. Seçin **Gelişmiş** > **genel öğesi** tıklatıp **yapılandırma parametreleri**. Merhaba makine çalışıyorsa, bu seçenek de-active olacaktır. toomake etkin hello makineyi kapatın, aşağı BT.
3. Merhaba, satır **disk. EnableUUID** var. hello değeri çok ayarlandığından emin olun**True** (büyük küçük harf duyarlı). Zaten varsa iptal edin ve onu önyüklendiğinde sonra hello SCSI komutu bir konuk işletim sistemi içinde test edin.
4. Merhaba satır varolan içermiyorsa **Satır Ekle** – ile Merhaba ekleyin **True** değeri. Çift tırnak kullanmayın.

#### <a name="install-additional-packages"></a>Ek paket yüklemek için
Toodownload gerekir ve bazı ek paketler yükleme.

1. Merhaba ana hedef sunucusuna bağlı toohello olduğundan emin olun Internet.
2. Bu komut toodownload çalıştırın ve 15 paketleri hello CentOS depodan yükleyin: **# yum yüklemek – y xfsprogs perl lsscsi rsync wget kexec-tools**.
3. Koruduğunuz hello kaynak makine çalıştırıyorsanız, Linux WIT Reiser veya XFS dosya sistemi hello kök ya da indirmeli ve aşağıdaki gibi ek paketler yükleme sonra cihaz, önyükleme:

   * # <a name="cd-usrlocal"></a>CD /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>RPM – ivh reiserfs 0,0 1.el6.elrepo.x86_64.rpm kmod reiserfs-yardımcı programları-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>RPM – ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Özel Değişiklikleri Uygula
Merhaba tam hello yükleme sonrası adımları ve yüklü hello paketleri sonra aşağıdaki tooapply özel değişiklikler yapın:

1. Merhaba RHEL 6-64 birleşik aracı ikili toohello VM kopyalayın. Bu komut toountar hello ikili çalıştırın: **– zxvf hedef<file name>**
2. Bu komut toogive izinleri çalıştırın: **# chmod 755./ApplyCustomChanges.sh**
3. Merhaba komut dosyasını çalıştırın: **#./ApplyCustomChanges.sh**. Yalnızca hello komut dosyası bir kez çalıştırmanız gerekir. Merhaba komut dosyası başarıyla çalıştıktan sonra hello sunucusunu yeniden başlatın.

## <a name="run-hello-failback"></a>Merhaba yeniden çalıştır
### <a name="reprotect-hello-azure-vms"></a>Hello Azure Vm'leri koruyun
1. Merhaba Site Recovery portalında > **makineler** sekmesini seçin devredilen VM hello ve tıklayın **yeniden koruma**.
2. İçinde **ana hedef sunucusu** ve **işlem sunucusu** hello şirket içi ana hedef sunucusu ve hello Azure VM işlem sunucusunu seçin.
3. Toohello VM bağlanmak için yapılandırılmış hello hesabı seçin.
4. Merhaba geri dönme sürümünü hello koruma grubunu seçin. Örneğin, tooselect PG1_Failback gerekir sonra hello VM içinde PG1 korumalı değilse.
5. Toorecover tooan alternatif bir konum istiyorsanız hello bekletme sürücüsü ve hello ana hedef sunucu için yapılandırılmış veri deposu seçin. Merhaba geri dönme koruma planına geri toohello şirket içi site hello VMware Vm'lerini başarısız olduğunda hello kullanacağı hello ana hedef sunucusu olarak aynı veri deposu. Aynı VM hello VM zaten gereken şirket içi sonra şirket içi toorecover hello çoğaltma Azure VM toohello istiyorsanız olması hello olarak ana hello aynı veri deposu hedef sunucu. Bir VM şirket içi ise yükü sırasında yeni bir tane oluşturulur.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Tıklattıktan sonra **Tamam** toobegin yükü bir iş tooreplicate hello Azure toohello şirket içi siteden VM başlar. Merhaba üzerinde hello ilerleme durumunu izleyebilirsiniz **işleri** sekmesi.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Bir yük devretme toohello şirket içi siteyi çalıştırın
Yükü hello sonra VM taşınan toohello geri dönme sürüm, koruma grubunun ve toohello kurtarma planı varsa hello yük devretme tooAzure için kullanılan otomatik olarak eklenir.

1. Merhaba, **kurtarma planları** hello yeniden çalışma grubu ve tıklatın içeren sayfa seç hello kurtarma planı **yük devretme** > **planlanmamış yük devretme**.
2. İçinde **onaylayın yük devretme** hello yük devretme yönü (tooAzure) doğrulayın ve toouse (son) hello yük devretme için hello kurtarma noktasını seçin. Etkinleştirmiş olmanız durumunda **çoklu VM** çoğaltma özellikleri yapılandırıldığında toohello en son uygulama ya da kilitlenme tutarlı bir kurtarma noktası kurtarabilirsiniz. Merhaba onay işareti toostart hello yük devretme'ı tıklatın.
3. Yük devretme sırasında Site Recovery hello Azure VM'ler kapanır. Beklediğiniz gibi yeniden çalışma tamamlandı denetledikten sonra Azure Vm'lerinin beklendiği gibi kapatılmışsa, hello kontrol edebilirsiniz.

### <a name="reprotect-hello--on-premises-site"></a>Merhaba şirket içi site koruyun
Yeniden çalışma işlemi tamamlandıktan sonra verilerinizi geri hello şirket içi sitede olacaktır, ancak korunan olmaz. toostart çoğaltma tooAzure yeniden hello aşağıdaki:

1. Merhaba Site Recovery portalında > **makineler** geri başarısız olmuş ve tıklatın select hello VM'ler sekmesinde **yeniden koruma**.
2. Bu çoğaltma tooAzure beklendiği şekilde çalıştığını doğruladıktan sonra Azure'da hello Azure (şu anda çalışmıyorsa) geri başarısız VM'ler silebilirsiniz.

### <a name="common-issues-in-failback"></a>Yeniden çalışma ile ilgili genel sorunları
1. Salt okunur kullanıcı vCenter keşfi gerçekleştirmek ve sanal makineleri koruma, başarılı ve yük devretme çalışır. Yeniden koruma hello anda Hello datastores bulunan bu yana başarısız olur. Bir belirti yeniden korurken listelenen hello datastores görmezsiniz. tooresolve bu izinlere sahip uygun hesabıyla hello vCenter kimlik bilgileri güncelleştirmek ve hello işi yeniden deneyin. [Daha fazla bilgi edinin](site-recovery-vmware-to-azure-classic.md)
2. Olduğunda, bir Linux VM yeniden çalışma ve şirket içi, çalıştırmak, hello ağ yöneticisi paketin hello makineden kaldırıldı görürsünüz. Azure'da Hello VM kurtarılan hello ağ yöneticisi paket kaldırılır olmasıdır.
3. TooAzure üzerinde başarısız oldu ve statik IP adresi ile yapılandırılmış bir VM olduğunda, başlangıç IP adresi DHCP yoluyla alınır. Geri tooOn içi başarısız olduğunda hello VM toouse DHCP tooacquire başlangıç IP adresi devam eder. Merhaba makinesine toomanually oturum açma gerekir ve gerekirse tooStatic adres yedekleme kümesi hello IP adresi.
4. ESXi 5.5 ücretsiz sürüm veya 6 vSphere hiper yönetici ücretsiz sürümü kullanıyorsanız, yük devretme başarılı, ancak yeniden çalışma başarısız olur. Ned tooupgrade tooeither değerlendirme lisans tooenable geri dönme olur.

## <a name="failing-back-with-expressroute"></a>ExpressRoute ile başarısız olan geri
Bir VPN bağlantısı veya Azure ExpressRoute üzerinden geri başarısız olabilir. Toouse ExpressRoute Not hello aşağıdaki istiyorsanız:

* ExpressRoute üzerinden ve hello yük devretme gerçekleştikten sonra Azure Vm'lerinin bulunduğu hello Azure sanal ağı toowhich kaynak makineleri başarısız üzerinde ayarlanmalıdır.
* Çoğaltılmış tooan genel bir uç nokta Azure depolama hesabı verilerdir. Ortak de ExpressRoute hello hedef veri merkezi için Site Recovery çoğaltma toouse ExpressRoute ile eşleme yukarı ayarlamanız gerekir.

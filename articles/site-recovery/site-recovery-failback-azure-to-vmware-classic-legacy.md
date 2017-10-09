---
title: aaaFail Azure'dan VMware Vm'lerini hello eski Klasik portalda geri | Microsoft Docs
description: "Bu makalede, Azure Site Recovery ile tooAzure toofail geri boyunca VMware sanal makinesinin nasıl yinelendiğini açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Geri VMware sanal makineleri ve fiziksel sunuculardan Azure Site Recovery (eski) ile Azure tooVMware başarısız
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klasik Azure Portalı](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klasik Azure portalı (eski)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Nasıl toofail geri VMware sanal makineleri Windows/Linux fiziksel sunucuları, şirket içi çoğaltılan sonra Azure tooyour şirket içi siteden tooAzure kullanarak site ve bu makalede [Azure Site Recovery?](site-recovery-overview.md).

Bu makalede eski bir yapılandırma ve yeni kasa için kullanılmaması gerekir.

## <a name="architecture"></a>Mimari
Bu diyagramda hello yük devretme ve yeniden çalışma senaryosu temsil eder. Merhaba mavi satırları, yük devretme sırasında kullanılan hello bağlantılardır. Merhaba kırmızı satırları yeniden çalışma sırasında kullanılan hello bağlantılardır. Merhaba satırlara oklarla Git hello Internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Başlamadan önce
* VMware Vm'lerini veya fiziksel sunucular üzerinden başarısız ve Azure'da çalıştırıyor olmalıdır.
* Yalnızca arka VMware sanal makinelerini ve Windows/Linux fiziksel sunucuları hello şirket içi birincil sitedeki Azure tooVMware sanal makinelerden yük devredebildiğini unutmamalısınız.  Fiziksel makinenin yeniden çalıştırma işlemini gerçekleştiriyorsanız, yük devretme tooAzure tooan Azure VM dönüştürür ve yeniden çalışma tooVMware tooa VMware VM dönüştürür.

Yeniden çalışma nasıl ayarlanacağını aşağıda verilmiştir:

1. **Yeniden çalışma bileşenleri ayarlamak**: tooset vContinuum sunucusu gerekir şirket içi ve Azure'da toohello yapılandırma sunucusu VM gelin. Ayrıca bir Azure VM toosend veri geri toohello şirket içi ana hedef sunucusu gibi bir işlem sunucusu da ayarlarız. Merhaba işlem sunucusu hello yük devretme işlenen hello yapılandırma sunucusuna kaydedin. Bir şirket içi ana hedef sunucusu yükleyin. Bir Windows ana hedef sunucusu gerekiyorsa vContinuum yüklediğinizde bu otomatik olarak ayarlanır. Linux gerekiyorsa tooset gerekir, Yukarı el ile ayrı bir sunucu üzerinde.
2. **Koruma ve yeniden etkinleştirme**: hello bileşenlerini ayarladıktan sonra vContinuum tooenable koruma Azure vm'lerinde ihtiyacınız vardır. Bir hazırlık denetimi hello VM'ler üzerinde çalıştırın ve bir yük devretme Azure tooyour şirket içi siteden çalıştırma. Yeniden çalışma sona erdikten sonra bunlar tooAzure çoğaltma işlemi başlatma böylece şirket içi makineler koruyun.

## <a name="step-1-install-vcontinuum-on-premises"></a>1. adım: vContinuum şirket içi yükleme
VContinuum sunucusu şirket içi tooinstall gerekir ve toohello yapılandırma sunucusu noktası.

1. [VContinuum karşıdan](http://go.microsoft.com/fwlink/?linkid=526305).
2. Merhaba karşıdan [vContinuum güncelleştirme](http://go.microsoft.com/fwlink/?LinkID=533813) sürümü.
3. Merhaba vContinuum en son sürümünü yükleyin. Merhaba üzerinde **Hoş Geldiniz** sayfasında **sonraki**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Merhaba'hello Sihirbazı'nın ilk sayfasında hello CX sunucusu IP adresi ve hello CX sunucu bağlantı noktası belirtin. Seçin **HTTPS kullanmak**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Merhaba yapılandırma sunucusu IP adresi üzerinde hello Bul **Pano** hello yapılandırma sunucusu Azure VM'de sekmesinde.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Genel bağlantı noktası hello üzerinde Hello yapılandırma sunucusu HTTPS bulmak **uç noktaları** hello yapılandırma sunucusu Azure VM'de sekmesinde.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Merhaba üzerinde **CS parola ayrıntıları** sayfasında hello yapılandırma sunucusu kaydolurken aşağı ettiğiniz hello parolayı belirtin. Hatırlamıyorsanız iade onu **C:\\Program Files (x86)\\Inmage sistemleri\\özel\\connection.passphrase** hello yapılandırma sunucusundaki VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. Merhaba, **hedef konum seçin** sayfasında belirtin burada tooinstall hello vContinuum sunucusu istediğiniz ve tıklatın **yükleme**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Yükleme tamamlandıktan sonra vContinuum başlatabilirsiniz.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>2. adım: Azure üzerinde bir işlem sunucusu yükleme
Böylece Hello VM'ler için Azure'da hello veri geri tooan şirket içi ana hedef sunucusu gönderebilir tooinstall Azure işlem sunucusu gerekir.

1. Merhaba üzerinde **yapılandırma sunucularına** select tooadd Azure içinde yeni bir işlem sunucusu sayfa.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. İşlem sunucusu adı ve adı ve parola tooconnect toohello sanal makine yönetici olarak belirtin. Merhaba yapılandırma sunucusu toowhich tooregister hello işlem sunucusu istediğiniz seçin. Bu hello olmalıdır tooprotect kullanıyorsanız ve sanal makinelerinizi başarısız aynı sunucu.
3. Hello Azure belirtin ağ hangi hello işlem sunucusu dağıtılmalıdır. Aynı hello olmalıdır ağ hello yapılandırma sunucusu olarak. Dağıtımına başlamak ve benzersiz bir IP adresi seçilen alt ağ belirtin.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Bir işi tetiklenen toodeploy hello işlem sunucusudur.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Azure'da Hello işlem sunucusu dağıtıldıktan sonra belirttiğiniz hello kimlik bilgilerini kullanarak hello Server'a oturum açabilir. Merhaba işlem sunucusunu kaydetmek hello hello kayıtlı aynı şekilde işlem sunucusu şirket.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> yeniden çalışma sırasında kayıtlı hello sunucu, Site kurtarma VM Özellikleri'nin altında görünmeyecektir. Yalnızca hello altında görünür **sunucuları** kayıtlı hello yapılandırma sunucusu toowhich sekmesinde. Yaklaşık 10-15 işlem hello kadar dakika sürebilir sunucu hello sekmesinde görünür.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>3. adım: şirket içi ana hedef server yükleme
Kaynak sanal makine işletim sistemine bağlı olarak tooinstall bir Linux gerekir veya bir Windows ana hedef sunucusu şirket içi.

### <a name="deploy-a-windows-master-target-server"></a>Bir Windows ana hedef sunucusu dağıtma
Bir Windows ana hedef zaten vContinuum Kurulum paketlenebilir. Merhaba vContinuum yüklediğinizde, ana sunucu da hello üzerinde dağıtılan aynı makineye ve kayıtlı toohello yapılandırma sunucusu.

1. toobegin dağıtımı, boş bir oluşturma makine şirket içi toorecover hello Azure VM'lerin istediğiniz hello ESX konağındaki.
2. En az iki disk toohello VM ekli – bir hello işletim sistemi için kullanılan vardır ve hello diğer hello bekletme sürücüsü için kullanılan emin olun.
3. Merhaba işletim sistemini yükleyin.
4. Merhaba vContinuum hello sunucuya yükleyin. Bu ayrıca hello ana hedef sunucusunun yüklemesini tamamlar.

### <a name="deploy-a-linux-master-target-server"></a>Bir Linux ana hedef sunucusu dağıtma
1. toobegin dağıtımı, boş bir oluşturma makine şirket içi toorecover hello Azure VM'lerin istediğiniz hello ESX konağındaki.
2. En az iki disk toohello VM ekli – bir hello işletim sistemi için kullanılan vardır ve hello diğer hello bekletme sürücüsü için kullanılan emin olun.
3. Merhaba Linux işletim sistemini yükleyin. Merhaba Linux ana hedef sistem LVM kök veya bekletme depolama alanları için kullanmamanız gerekir. Bir Linux ana hedef sunucusudur tooavoid LVM bölümleri/diskleri bulma varsayılan olarak yapılandırılır.
4. Oluşturabileceğiniz bölümler:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Merhaba ana hedef yüklemeye başlamadan önce aşağıdaki post yükleme adımları hello gerçekleştiremeyen.

#### <a name="post-os-installation-steps"></a>İşletim sistemi yükleme adımlarını sonrası
Her bir Linux sanal makine SCSI sabit disk için SCSI ID tooget hello etkinleştirmek hello parametresi "disk. EnableUUID = TRUE "gibi:

1. Sanal makineyi kapatın.
2. Merhaba VM girişi hello sol panelinde sağ tıklayın > **ayarlarını Düzenle**.
3. Merhaba tıklatın **seçenekleri** sekmesi. Seçin **Gelişmiş\>genel öğesi** > **yapılandırma parametreleri**. Merhaba **yapılandırma parametrelerini** seçenek, yalnızca kullanılabilir hello makine kapatıldığında.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Olan bir satır olup olmadığını denetler **disk. EnableUUID** bulunmaktadır. Yapar ve çok ayarlanırsa**False** çok ayarlamak**True** (büyük/küçük harfe duyarlı değildir). Varsa var ve ayarlama tootrue, seçeneğini tıklatın **iptal** ve yukarı önyükleme sonra test hello konuk işletim sistemi içinde hello SCSI komutu. Varsa tıklatın yok **Satır Ekle**.
5. Disk ekleyin. Merhaba EnableUUID **adı** sütun. Değerini TRUE olarak ayarlayın. Merhaba değerleri çift tırnak birlikte yukarıda eklemeyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Merhaba ek paketleri yükleyip kurun
Not: indirme ve hello ek paketler yükleme önce hello Sistem internet bağlantısı olduğundan emin olun.

\#yum -y xfsprogs perl lsscsi rsync wget kexec-araçları yükleme

Bu komut, CentOS 6.6 depodan 15 bu paketleri yükler ve bunları yükler:

BC 1.06.95 1.el6.x86\_64. rpm

busybox 1.15.1 20.el6.x86\_64. rpm

kitaplıklar 0.158 3.2.el6.x86 elfutils\_64. rpm

Araçlar 2.0.0 280.el6.x86 kexec\_64. rpm

lsscsi 0.23 2.el6.x86\_64. rpm

lzo 2.03 3.1.el6\_5.1.x86\_64. rpm

Perl 5.10.1 136.el6\_6.1.x86\_64. rpm

Perl-modül-takılabilir-3.90-136.el6\_6.1.x86\_64. rpm

Perl-Pod-çıkışları-1,04-136.el6\_6.1.x86\_64. rpm

Perl-Pod-Basit-3.13-136.el6\_6.1.x86\_64. rpm

Perl kitaplıklar 5.10.1 136.el6\_6.1.x86\_64. rpm

Perl sürüm 0.77 136.el6\_6.1.x86\_64. rpm

rsync 3.0.6 12.el6.x86\_64. rpm

1.1.0 1.el6.x86 snappy\_64. rpm

wget 1.12 5.el6\_6.1.x86\_64. rpm

Aşağıdaki paketler indirilebilen ve Linux yöneticisinde yüklü hello kaynak makine Reiser veya XFS filesystem hello kök veya önyükleme cihazı için kullanırsa, önceki tooprotection hedefleyin.

\#CD /usr/local

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\#RPM - ivh kmod-reiserfs-0,0-1.el6.elrepo.x86\_64. rpm reiserfs-yardımcı programları-3.6.21-1.el6.elrepo.x86\_64. rpm

\#wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\#RPM - ivh xfsprogs-3.1.1-16.el6.x86\_64. rpm

#### <a name="apply-custom-configuration-changes"></a>Özel yapılandırma değişikliklerini uygula
Bu değişiklikleri uygulamadan önce hello önceki bölümde tamamladıktan sonra aşağıdaki adımları izleyin emin olun:

1. Yeni işletim sistemi oluşturulan hello RHEL 6-64 birleşik aracı ikili toohello kopyalayın.
2. Bu komut toountar hello ikili çalıştırın: **- zxvf hedef \<dosya adı\>**
3. Bu komut toogive izinleri çalıştırın: \# **chmod 755./ApplyCustomChanges.sh**
4. Merhaba komut dosyasını çalıştırın:  **\# ./ApplyCustomChanges.sh**. Yalnızca bir kez Hello betik hello sunucusunda çalıştırın. Merhaba betik çalıştıktan sonra hello sunucuyu yeniden başlatın.

### <a name="install-hello-linux-server"></a>Merhaba Linux sunucusu yükleme
1. [Karşıdan](http://go.microsoft.com/fwlink/?LinkID=529757) hello yükleme dosyası.
2. Merhaba dosya toohello tercih ettiğiniz bir sftp istemci yardımcı programını kullanarak Linux ana hedef sanal makineyi kopyalayın. Bunun yerine hello Linux ana hedef sanal makineye yüklenmesi oturum ve wget toodownload hello yükleme paketindeki sağlanan bağlantıyı kullanabilirsiniz
3. Merhaba Linux ana hedef sunucusu kullanarak sanal makineyi üzerine günlük bir ssh istemcisi tercih ettiğiniz
4. Bağlı toohello Azure Linux ana hedef sunucunuzu bir VPN bağlantısı üzerinden dağıtılan sonra iç IP adresi sanal makinede bulabilirsiniz hello sunucunun kullandığı ağ **Pano** sekmesi ve bağlantı noktası 22 tooconnect toohello Linux ana hedef sunucusunda güvenli Kabuğu'nu kullanarak.
5. Bağlantı kurduğunuz toohello Linux ana hedef sunucusunda genel bir Internet bağlantısı üzerinden kullanırsanız hello Linux ana hedef sunucunun ortak sanal IP adresi (Merhaba sanal makinelerden **Pano** sekmesinde) ve ortak uç nokta hello için ssh toologin toohello Linux servder oluşturulur.
6. Çalıştırarak hello gzip'li Linux ana hedef sunucu yükleyicisi tar arşivinden Hello dosyaları ayıklayın: *"– xvzf Microsoft ASR hedef\_UA\_8.2.0.0\_RHEL6 64\"* hello dizininden, Merhaba yükleyicisini içerir.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Ayıklanan hello yükleyici dosyaları tooa farklı dizini değiştirirseniz toohello directory toowhich Merhaba içeriğine hello tar arşiv ayıklanan. Bu dizin yolundan Çalıştır "sudo. / install.sh".

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. İstendiğinde toochoose birincil rolü seçtiğinizde **2 (ana hedef)**. Merhaba diğer etkileşimli yükleme seçenekleri varsayılan değerlerinde bırakın.
9. Yükleme toocontinue ve hello ana bilgisayar yapılandırma arabirimi tooappear için bekleyin. Merhaba konak Yapılandırması yardımcı programını hello Linux ana hedef sunucusu için bir komut satırı yardımcı programıdır. Merhaba ssh istemcisi yardımcı programı penceresinde yeniden boyutlandırma. Kullanım hello ok tuşları tooselect hello **genel** seçeneği ve ENTER tuşuna BASIN klavyenizde.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. Merhaba alanında **IP** hello yapılandırma sunucusu hello iç IP adresini girin (hello Bul **Pano** hello yapılandırma sunucusu VM sekmesinde) ve ENTER tuşuna basın. İçinde **bağlantı noktası** girin **22** ve ENTER tuşuna basın.
11. Bırakın **HTTPS kullan** olarak **Evet**, ve ENTER tuşuna basın.
12. Merhaba hello yapılandırma sunucusunda oluşturulan parola girin. Windows makine toossh toohello Linux sanal makine PUTTY bir istemciden kullanıyorsanız, üst karakter + INSERT toopaste hello hello Pano içeriğini kullanabilirsiniz. Merhaba parola toohello Yerel Pano CTRL-C kullanarak kopyalayın ve üst karakter + INSERT toopaste kullanın. ENTER tuşuna basın.
13. Merhaba sağ ok anahtar toonavigate tooquit kullanın ve ENTER tuşuna basın. Yükleme toocomplete bekleyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Herhangi bir nedenden dolayı tooregister başarısız olursa, Linux ana hedef sunucusu toohello yapılandırma sunucusu şekilde yeniden ana bilgisayar yapılandırması yardımcı programını (önce tooset erişim izinleri toothis gerekir /usr/local/ASR/Vx/bin/hostconfigcli çalıştırarak bunu yapabilirsiniz Dizin) süper kullanıcı olarak chmod çalıştırarak.

#### <a name="validate-master-target-registration"></a>Ana hedef kayıt doğrula
Bu hello doğrulayabilirsiniz ana hedef sunucusu başarıyla kaydedildi toohello yapılandırma sunucusu Azure Site Recovery kasasına > **yapılandırma sunucusu** > **sunucu ayrıntıları**.

> [!NOTE]
> Hello rağmen ana hedef yapılandırma algılandığında hello ana hedef sunucusu, sanal makine hello yapılandırma hataları alırsanız kaydetme Azure'dan silinmiş olabilir veya uç noktalar düzgün yapılandırılmadı sonra bunun nedeni Azure'da Hello ana hedef dağıtıldığında hello Azure dndpoints tarafından bu şirket içi ana hedef sunucusu şirket içi için doğru değil. Bu yeniden çalışma etkilemez ve bu hatalar yoksayabilirsiniz.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>4. adım: hello sanal makineleri toohello şirket içi site koruma
Geri dönecek tooprotect VM'ler toohello şirket içi site olması gerekir.

### <a name="before-you-begin"></a>Başlamadan önce
Bir VM üzerinde tooAzure başarısız olduğunda, sayfa dosyası için fazladan geçici bir sürücü ekler. Bu, genellikle gerekli değildir, ek bir sürücüdür başarısız, sayfa dosyası için adanmış bir sürücü zaten sahip olabilir olduğundan VM üzerinde tarafından. Hello sanal makinelerin ters koruma başlamadan önce böylece koruma bu sürücüyü çevrimdışı duruma getirmenizi sağlamak gerekir. Bunu şu şekilde yapabilirsiniz:

1. Bilgisayar Yönetimi'ni açın ve böylece hello disklerin çevrimiçi ve ekli toohello makine listeler Depolama Yönetimi'ni seçin.
2. Merhaba geçici disk ekli toohello makine seçip toobring çevrimdışı.

### <a name="protect-hello-vms"></a>Merhaba Vm'leri koruma
1. Hello Azure portal, devredilen hello sanal makine tooensure hello durumunu denetleyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. VContinuum makinenizde başlatın.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Tıklatın **yeni koruma** ve hello işlemi sistem türünü seçin
4. Select hello açmak hello yeni pencerede **işletim sistemi türü** > **Al ayrıntıları** hello VM'ler için geri toofail istiyor. İçinde **birincil sunucu ayrıntıları**tanımlamak ve hello tooprotect istediğiniz sanal makineleri seçin. VM'ler üzerindeki yük devretme önce oldukları hello vCenter ana bilgisayar adı altında listelenir.
5. Bir sanal makine tooprotect seçin (ve zaten tooAzure üzerinde başarısız oldu) bir açılır pencere iki giriş hello sanal makine için sunar. Merhaba yapılandırma sunucusu hello sanal makineleri kayıtlı tooit iki örneğini algılar olmasıdır. Merhaba VM, koruyabilmeniz için doğru VM hello şirket için tooremove hello girişi gerekir. tooidentify hello doğru Azure VM Buraya giriş, hello Azure VM ve Git tooC:\Program dosyaları (x86) \Microsoft Azure Site Recovery\Application Data\etc olarak oturum açabilir. Merhaba ana bilgisayar kimliği Hello dosya drscout.conf içinde tanımlayın Merhaba vContinuum iletişim kutusunda, hello girdisi hello VM üzerinde hello ana bilgisayar kimliği öğrenmek bulundu tutun. Diğer tüm girişleri silin. tooselect hello tooits IP adresine başvurabilir VM düzeltin. Başlangıç IP adresi aralığı şirket içi olması hello şirket içi VM.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Merhaba vCenter sunucusunda hello sanal makineyi durdurun. Merhaba VM'ler şirket içi silebilirsiniz.
7. Ardından hello şirket içi MT sunucu toowhich tooprotect hello VM'ler istediğiniz belirtin. toodo Bu, geri toofail istediğiniz toohello vCenter server toowhich bağlanın.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Select hello ana hedef sunucusu tabanlı hello konak toowhich üzerinde toorecover hello VM istiyor.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Merhaba sanal makinelerin her biri için Hello çoğaltma seçeneği sağlar. toodo bu tooselect hello kurtarma tarafı veri deposu toowhich hello VM'ler kurtarılması gerekir. Merhaba tablo hello farklı seçenekler tooprovide her VM için gereksinim duyduğunuz özetler.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Seçeneği** | **Önerilen değer seçeneği** |
   | --- | --- |
   |  İşlem sunucusu IP adresi |Azure üzerinde dağıtılan hello işlem sunucusunu seçin |
   |  Bekletme boyutu (MB) | |
   |  Bekletme değeri |1 |
   |  Gün/saat |Gün |
   |  Tutarlılık aralığı |1 |
   |  Hedef veri deposu seçin |Merhaba kurtarma sitesinde Hello datastore kullanılabilir. Merhaba veri deposu yeterli alana sahip ve kullanılabilir toohello ESX ana toorestore hello sanal makine istediğiniz olması gerekir. |
10. Sanal makine hello özellikleri sonra Yük devretme tooon içi site alacağı hello yapılandırın. Aşağıdaki tablonun hello Hello özellikler özetlenmiştir.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Özellik** | **Ayrıntılar** |
    | --- | --- |
    | Ağ yapılandırması |Algılanan her ağ bağdaştırıcısı seçin ve **değişiklik** hello sanal makine için tooconfigure hello geri dönme IP adresi. |
    | Donanım yapılandırması |Merhaba CPU ve bellek hello VM hello belirtin. Ayarları uygulanan tooall hello tooprotect çalıştığınız VM'ler olabilir. tooidentify Merhaba hello CPU ve bellek için doğru değerleri, toohello IAAS Vm'leri rol boyutu bakın ve hello çekirdek sayısı ve atanan bellek bakın. |
    | Görünen ad |Yeniden çalışma tooon içi sonra hello vCenter envanterinde görüntülenir gibi hello sanal makineleri adlandırabilirsiniz. Merhaba sanal makine bilgisayar konak adı Hello varsayılan addır. tooidentify hello VM adı, toohello VM listesi hello koruma grubundaki başvurabilir. |
    | NAT yapılandırma |Aşağıda ayrıntılı olarak ele alınan |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>NAT ayarlarını yapılandırma
1. Merhaba sanal makinelerin korumasını tooenable, iki iletişim kanalı kurulan toobe gerekir. Merhaba ilk hello sanal makine ile Merhaba işlem sunucusu arasında kanalıdır. Bu kanal VM hello hello verileri toplar ve veri toohello ana hedef sunucusu sonra hangi gönderir hello toohello işlem sunucusuna gönderir. Merhaba işlem sunucusu ve korumalı hello sanal makine toobe hello üzerinde olup olmadığını daha sonra aynı Azure sanal ağı toouse NAT ayarlarını gerek yoktur. Aksi takdirde NAT ayarlarını belirtin. Azure'da hello işlem sunucusu Hello genel IP adresini görüntüleyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. Merhaba ikinci hello işlem sunucusu ve hello ana hedef sunucusu kanalıdır. seçenek toouse NAT hello veya tabanlı VPN bağlantısı kullanarak veya hello iletişim kurmasını bağımlı değil Internet. NAt, VPN kullanıyorsanız, ancak yalnızca bir Internet bağlantısı kullanıyorsanız seçmeyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Merhaba şirket içi sanal makineleri belirtilen silinmiş henüz ve hello veri deposu kullanıyorsanız tooensure gerekir başarısız geri toostill hello eski VMDK's içeriyorsa bu hello geri dönme yeni bir yerde VM oluşturulan. toodo bu select hello **Gelişmiş** ayarları ve alternatif bir klasör toorestore tooin belirtin **klasör adı ayarları**. Merhaba varsayılan ayarlarına sahip diğer seçenekleri bırakın. Merhaba klasör adı ayarları tooall hello sunucularını uygulayın.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Hazırlık denetimi Çalıştır hello sanal makinelerin hazır toobe olduğunu tooensure geri tooon içi korumalı.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Bekleyin toocomplete. Tüm sanal makinelerin başarıyla ise hello koruma planı için bir ad belirtebilirsiniz. Ardından **koruma** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. VContinuum ediyor izleyebilirsiniz.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Merhaba adımından sonra **korumayı etkinleştirme planlama** sonlandığında VM koruma hello Site Recovery portalında izleyebilirsiniz.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Merhaba VM üzerinde tıklayarak ve ilerleme durumunu izleme hello tam durumunu görebilirsiniz.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Merhaba geri dönme planı hazırlama
Merhaba uygulaması herhangi bir zamanda başarısız geri toohello şirket içi site olabilmesi vContinuum kullanarak bir yeniden çalışma planı hazırlayabilirsiniz. Site Recovery çok benzer toohello kurtarma planları bu kurtarma planlarının.

1. VContinuum başlatın ve seçin **yönetmek planları** > **kurtarın.** Kullanılan toofail VM'ler kaldırılmış tüm hello planlarını listesinin görebilirsiniz. Merhaba kullanabilirsiniz aynı planları toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Merhaba koruma planı ve tüm hello toorecover da istediğiniz sanal makineleri seçin. Her VM seçtiğinizde hello hedef ESX sunucusu ve hello kaynak VM disk dahil olmak üzere daha fazla ayrıntı görebilirsiniz. Tıklatın **sonraki** toobegin Kurtarma Sihirbazı'nı hello ve toorecover istediğiniz hello sanal makineleri seçin.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Birden çok seçenek göre kurtarabilirsiniz ancak şunu kullanmanızı öneririz **son etiket** seçip **tüm VM'ler için Uygula** hello sanal makineyi en son verileri hello tooensure kullanılır.
4. Merhaba çalıştırmak **hazır olma durumunu kontrol edin.** Bu, hello doğru parametreleri yapılandırılmış tooenable VM kurtarma olup olmadığını kontrol eder. Tıklatın **sonraki** tüm hello denetimler başarılı olursa. Aksi takdirde hello günlüğünü denetleyin ve hello hataları çözümleyin.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. İçinde **VM Yapılandırması** hello kurtarma ayarları doğru şekilde ayarlandığından emin olun. Gerekirse hello VM ayarlarını değiştirebilirsiniz.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Kurtarılacak ve bir kurtarma düzeni sanal makineleri Hello listesini gözden geçirin. Sanal makineleri hello bilgisayarın ana bilgisayar adını kullanarak listelendiğine dikkat edin. Zor toomap hello bilgisayar konak adı toohello sanal makine olabilir.
   toomap hello adları, Git toohello sanal makineleri **Pano** Azure ve onay hello VM konak adı.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Plan adı belirtin ve seçin **daha sonra kurtarmak**. Merhaba ilk koruma tam olmayabilir bu yana toorecover daha sonra öneririz.
8. Tıklayın **kurtarmak** toorecover şimdi ve daha sonra değil seçtiyseniz toosave hello plan veya tetikleyici hello kurtarma. Merhaba planı kaydedilen olmadığını hello Kurtarma durumu toosee kontrol edebilirsiniz.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Sanal makineleri kurtarma
Merhaba planı oluşturulduktan sonra hello sanal makineleri kurtarabilirsiniz. Bu sanal hello teslim etmeden önce makineleri eşitleme tamamladınız. Çoğaltma durumunu Tamam gösteriyorsa hello koruma tamamlandıktan ve hello RPO eşik geçildikten. Sistem durumu hello VM Özellikleri'nde doğrulayabilirsiniz.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Merhaba kurtarma başlatmadan önce devre dışı hello Azure sanal makineleri kapatın. Bu bölme beyin yoktur ve kullanıcılar yalnızca bir kopyasını hello uygulama erişimi sağlar.

1. Plan kaydedilmiş hello başlatın. VContinuum içinde seçin **İzleyici** hello planları. Bu çalıştırılmış tüm hello planlarını listeler.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Select hello planında **kurtarma** tıklatıp **Başlat**. Kurtarma izleyebilirsiniz. Sanal makineleri açtıktan sonra vcenter toothem üzerinde bağlanabilir.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>TooAzure yeniden geri dönme sonra koruma
Yeniden çalışma tamamlandıktan sonra büyük olasılıkla tooprotect hello sanal makineleri yeniden isteyeceksiniz. Bunu şu şekilde yapabilirsiniz:

1. Merhaba sanal makineleri şirket içi çalışıyorsanız ve uygulamaların erişilebilir olduğunu denetleyin.
2. Hello Azure Site Recovery portalındaki hello sanal makineleri seçin ve silebilirsiniz. Merhaba sanal makinelerin toodisable hello korumasını seçin. Bu, hello VM'ler daha fazla korunan sağlar.
3. Azure'da hello devredilen Azure sanal makinelerin Sil
4. Merhaba eski sanal makinede vSpehere silin. TooAzure daha önce başarısız hello VM'ler bunlar.
5. Merhaba Site Recovery portalında hello üzerinden kısa süre önce başarısız Vm'leri koruyun. Korumalı olup olmadıklarını sonra tooa kurtarma planı ekleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Hakkında bilgi edinin](site-recovery-vmware-to-azure-classic.md) VMware sanal makineleri ve fiziksel sunucuları tooAzure hello gelişmiş dağıtım kullanarak çoğaltma.

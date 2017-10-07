---
title: "aaaHow tooinstall Azure tooon içi yük devretme için bir Linux ana hedef sunucusu | Microsoft Docs"
description: "Linux sanal makine yeniden korumayı önce bir Linux ana hedef sunucusu gerekir. Bilgi nasıl tooinstall biri."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Bir Linux ana hedef sunucu yükle
Sanal makinelerinizi başarısız olduktan sonra geri hello sanal makineleri toohello şirket içi site başarısız olabilir. geri toofail, tooreprotect hello sanal makine Azure toohello şirket içi siteden gerekir. Bu işlem için bir şirket içi ana hedef sunucusu tooreceive hello trafiği gerekir. 

Windows sanal makinesi korumalı sanal makineniz olması durumunda, bir Windows ana hedef gerekir. Bir Linux sanal makine için bir Linux ana hedef gerekir. Okuma hello aşağıdaki adımları toolearn nasıl hedef toocreate ve yükleme bir Linux ana.

> [!IMPORTANT]
> Merhaba 9.10.0 ana hedef sunucusu sürümünden itibaren hello son ana hedef sunucusu, yalnızca bir Ubuntu 16.04 sunucusunda yüklenebilir. Yeni yüklemeler CentOS6.6 sunucularda izin verilmez. Ancak, tooupgrade eski ana hedef sunucularınızı hello 9.10.0 sürümünü kullanarak devam edebilirsiniz.

## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooinstall bir Linux ana hedef için yönergeler sağlar.

POST yorumlarınızı ve sorularınızı bu makalenin veya hello hello sonunda [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Ön koşullar

* toochoose hello hangi toodeploy hello ana hedef konakta belirlemek hello geri dönme toobe tooan mevcut şirket içi sanal makine ya da tooa yeni bir sanal makine geçiyor durumunda. 
    * Mevcut bir sanal makine için erişim toohello veri depolarına hello sanal makinenin hello ana hedefinin hello konak olması gerekir.
    * Merhaba şirket içi sanal makine yoksa hello geri dönme sanal makine aynı hello ana hedefi olarak konağı hello oluşturulur. Herhangi bir ESXi ana tooinstall hello ana hedef seçebilirsiniz.
* Merhaba ana hedef hello işlem sunucusu ve hello yapılandırma sunucusu ile iletişim kurabilen bir ağ üzerinde olmalıdır.
* Merhaba ana hedef Hello sürümü eşit tooor önceki sürümlerinden hello hello işlem sunucusu ve hello yapılandırma sunucusu olması gerekir. Örneğin, hello yapılandırma sunucusu Hello sürümü 9,4 ise hello ana hedef hello sürümü 9,4 veya 9.3 ancak değil 9.5 olabilir.
* Merhaba ana hedef yalnızca bir VMware sanal makine ve bir fiziksel sunucuya yüklenebilir.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Merhaba ana hedef toohello boyutlandırma yönergelerine göre oluşturma

Merhaba ana hedef boyutlandırma yönergeleri izleyerek hello uygun şekilde oluşturun:
- **RAM**: 6 GB veya daha fazla
- **İşletim sistemi disk boyutu**: 100 GB veya daha fazla (tooinstall CentOS6.6)
- **Saklama sürücüsünün için ek disk boyutu**: 1 TB
- **CPU çekirdekleri**: 4 çekirdek ya da daha fazla bilgi

Merhaba aşağıdaki tekrar desteklenen Ubuntu desteklenir.


|Çekirdek serisi  |Yukarı çok desteği |
|---------|---------|
|4.4      |4.4.0-81-Generic         |
|4.8      |4.8.0-56-Generic         |
|4.10     |4.10.0-24-Generic        |


## <a name="deploy-hello-master-target-server"></a>Merhaba ana hedef sunucusu dağıtma

### <a name="install-ubuntu-16042-minimal"></a>Ubuntu 16.04.2 yükleme en az

Merhaba adımları tooinstall hello Ubuntu 16.04.2 64-bit işletim sistemi aşağıdaki hello alın.

**1. adım:** Git toohello [bağlantı karşıdan](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) ve hello en yakın yansıtma seçin, bir Ubuntu 16.04.2 en az 64-bit ISO indirme alanından.

Merhaba DVD sürücüsüne bir Ubuntu 16.04.2 en az 64-bit ISO tutmak ve hello sistem başlatın.

**2. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.

![Dil Seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**3. adım:** seçin **yükleme Ubuntu Server**ve ardından **Enter**.

![Ubuntu Server yüklemesi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**4. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.

![İngilizce tercih ettiğiniz dili seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**5. adım:** seçin hello hello uygun seçeneği **saat dilimi** Seçenekler listesinde ve ardından **Enter**.

![Merhaba doğru saat dilimini seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**6. adım:** seçin **Hayır** (varsayılan seçenek hello) ve ardından **Enter**.


![Merhaba klavye yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**7. adım:** seçin **İngilizce (ABD)** gibi hello hello klavye kaynak ülke ve ardından **Enter**.

![ABD kaynak hello ülkeyi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**8. adım:** seçin **İngilizce (ABD)** hello klavye düzeni ve ardından olarak **Enter**.

![ABD İngilizcesi hello klavye düzeni seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**9. adım:** sunucunuzun hello için hello ana bilgisayar adı girin **ana bilgisayar adı** kutusuna ve ardından **devam**.

![Sunucunuz için Hello ana bilgisayar adı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**10. adım:** toocreate bir kullanıcı hesabı hello kullanıcı adı girin ve ardından **devam**.

![Bir kullanıcı hesabı oluşturun](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**11. adım:** hello yeni kullanıcı hesabının hello parolasını girin ve ardından **devam**.

![Merhaba parolayı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**12. adım:** hello hello yeni bir kullanıcı parolasını onaylayın ve ardından **devam**.

![Merhaba parolaları onaylayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**13. adım:** seçin **Hayır** (varsayılan seçenek hello) ve ardından **Enter**.

![Kullanıcılar ve parolaları ayarlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**14. adım:** görüntülenen hello saat dilimi doğru ise, seçin **Evet** (varsayılan seçenek hello) ve ardından **Enter**.

tooreconfigure seçin, saat dilimi **Hayır**.

![Başlangıç saati yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**15. adım:** bölümleme yöntemi seçenekleri hello seçin **destekli - tüm disk kullanmak**ve ardından **Enter**.

![Yöntem seçeneği bölümleme hello seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**16. adım:** seçin hello hello uygun diskten **seçin disk toopartition** seçenekleri ve ardından **Enter**.


![Başlangıç diski seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**17. adım:** seçin **Evet** toowrite hello değişiklikleri toodisk ve ardından **Enter**.

![Merhaba değişiklikleri toodisk yazma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Adım 18:** hello varsayılan seçeneği seçin, **devam**ve ardından **Enter**.

![Merhaba varsayılan seçeneği seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**19. adım:** hello sisteminizdeki yükseltmeler yönetmek için uygun seçeneği belirleyin ve ardından **Enter**.

![Yükseltme nasıl toomanage seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Hello Azure Site Recovery ana hedef sunucusu hello Ubuntu çok belirli bir sürümünü gerektirdiğinden, tooensure hello sanal makine için yükseltme devre dışı bırakıldı, hello çekirdek gerekir. Etkinleştirilirse, normal bir yükseltme hello ana hedef sunucusu toomalfunction neden. Merhaba seçtiğinizden emin olun **otomatik güncelleştirme** seçeneği.


**20. adım:** varsayılan seçenekleri seçin. SSH bağlantısı için openSSH istiyorsanız hello seçin **OpenSSH server** seçeneğini ve ardından **devam**.

![Yazılımı seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**21. adım:** seçin **Evet**ve ardından **Enter**.

![Yükleme oturumu hello kaz önyükleme yükleyicisi](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**22. adım:** seçin hello hello önyükleme yükleyicisi yükleme için uygun aygıt (tercihen **/dev/sda**) ve ardından **Enter**.

![Önyükleme yükleyicisi yükleme için bir cihaz seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**23. adım:** seçin **devam**ve ardından **Enter** toofinish hello yükleme.

![Merhaba yüklemeyi tamamlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Hello yükleme tamamlandıktan sonra toohello VM hello yeni kullanıcı kimlik bilgileriyle oturum açın. (Çok başvuran**adım 10** daha fazla bilgi için.)

Ekran tooset hello kök aşağıdaki hello açıklanan hello kullanıcı parolası adımlar. Ardından kök kullanıcı olarak oturum açın.

![Merhaba kök kullanıcı parolasını ayarlayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Merhaba makine yapılandırması için bir ana hedef sunucusu olarak hazırlama
Ardından, bir ana hedef sunucusu gibi hello makine yapılandırması için hazırlayın.

bir Linux sanal makinedeki her bir SCSI sabit disk için tooget hello ID'yi etkinleştirmek hello **disk. EnableUUID = TRUE** parametre.

Bu parametre, Al hello aşağıdaki adımları tooenable:

1. Sanal makineyi kapatın.

2. Merhaba sanal makine hello sol bölmede Hello girişini sağ tıklatın ve ardından **ayarlarını Düzenle**.

3. Select hello **seçenekleri** sekmesi.

4. Merhaba sol bölmesinde seçin **Gelişmiş** > **genel**seçip hello **yapılandırma parametrelerini** hello hello ekranın sağ alt bölümünün düğmesinde.

    ![Seçenekler sekmesi](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Merhaba **yapılandırma parametrelerini** seçeneği kullanılamaz hello makine çalışırken. Bu sekme etkin toomake hello sanal makineyi kapatın.

5. Olan bir satır olup olmadığını görmek **disk. EnableUUID** zaten mevcut.

    - Başlangıç değeri varsa ve çok ayarlanır**False**, hello değeri çok değiştirmek**doğru**. (Merhaba değerleri büyük küçük harfe duyarlı değildir.)

    - Başlangıç değeri varsa ve çok ayarlanır**True**seçin **iptal**.

    - Merhaba değer yoksa seçin **Satır Ekle**.

    - Merhaba Ad sütununda eklemek **disk. EnableUUID**ve ardından hello değeri çok**doğru**.

    ![Olup olmadığını denetleme disk. EnableUUID zaten var.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Çekirdek yükseltmeler devre dışı bırak

Azure Site Recovery ana hedef sunucusu hello Ubuntu çok belirli bir sürümünü gerektirir, hello çekirdek yükseltmeler hello sanal makine için devre dışı emin olun.

Çekirdek yükseltmeler etkinleştirilirse, normal bir yükseltme hello ana hedef sunucusu toomalfunction neden.

#### <a name="download-and-install-additional-packages"></a>İndirme ve ek paketler yükleme

> [!NOTE]
> Internet bağlantısı toodownload varsa ve ek paketler yükleme emin olun. Internet bağlantısı yoksa, toomanually gereken bu RPM paketleri bulun ve bunları yükleyin.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Kurulum için Hello yükleyici Al

Ana hedef Internet bağlantısı varsa, aşağıdaki adımları toodownload hello yükleyici hello kullanabilirsiniz. Aksi takdirde hello yükleyici hello işlem sunucusundan kopyalayın ve ardından yükleyin.

#### <a name="download-hello-master-target-installation-packages"></a>Merhaba ana hedef yükleme paketleri indirin

[Merhaba son Linux ana hedef yükleme BITS karşıdan yükleme](https://aka.ms/latestlinuxmobsvc).

toodownload Linux, türü kullanarak:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Karşıdan yükle ve giriş dizininizde hello yükleyici sıkıştırmasını emin olun. Çok sıkıştırmasını açın,**/usr/yerel**, sonra da hello yükleme başarısız olur.


#### <a name="access-hello-installer-from-hello-process-server"></a>Merhaba işlem sunucusundan erişim hello yükleyici

1. Merhaba işlem sunucusunda çok Git**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Merhaba işlem sunucusundan Hello gerekli yükleyici dosyasını kopyalayın ve kaydedileceği **latestlinuxmobsvc.tar.gz** giriş dizininizdeki.


### <a name="apply-custom-configuration-changes"></a>Özel yapılandırma değişikliklerini uygula

tooapply özel yapılandırma değişiklikleri, hello aşağıdaki adımları kullanın:


1. Aşağıdaki komut toountar hello ikili hello çalıştırın.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Merhaba komutu toorun ekran görüntüsü](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Çalışma hello aşağıdaki toogive izni komutu.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Toorun hello komut aşağıdaki hello çalıştırın.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Yalnızca bir kez Hello betik hello sunucusunda çalıştırın. Merhaba sunucuyu kapatın. Bir disk ekledikten sonra ardından hello sunucu hello sonraki bölümde açıklandığı gibi yeniden başlatın.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Bir bekletme disk toohello Linux ana hedef sanal makine Ekle

Aşağıdaki adımları toocreate saklama diskinin hello kullan:

1. Yeni bir 1 TB disk toohello Linux ana hedef sanal makine ekleyin ve sonra hello makine başlatın.

2. Kullanım hello **çok yollu -üm** toolearn hello çok yollu kimliği hello saklama diskinin komutu.

    ```
    multipath -ll
    ```
    ![Merhaba saklama diskinin Hello çok yollu kimliği](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Merhaba sürücüyü biçimlendirmek ve ardından bir dosya sistemi hello yeni sürücüde oluşturun.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Merhaba sürücüsünde bir dosya sistemi oluşturma](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Merhaba dosya sistemi oluşturduktan sonra hello saklama diskinin bağlayın.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Bağlama hello saklama diskinin](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Merhaba oluşturma **fstab** hello sistem her başlatıldığında giriş toomount hello bekletme sürücüsü.
    ```
    vi /etc/fstab
    ```
    Seçin **Ekle** hello dosyasını düzenleyerek toobegin. Yeni bir satır oluşturun ve ardından metin aşağıdaki hello ekleyin. Merhaba disk çok yollu kimliği vurgulanmış hello çok yollu kimliği hello önceki komutundan göre düzenleyin.

    ** /dev/Eşleyici/ <Retention disks multipath id> /mnt/bekletme ext4 rw 0 0**

    Seçin **Esc**ve ardından **: wq** (yazma ve çıkın) tooclose hello Düzenleyicisi penceresini.

### <a name="install-hello-master-target"></a>Merhaba ana hedef yükleyin

> [!IMPORTANT]
> Merhaba ana hedef sunucusu Hello sürümü eşit tooor önceki sürümlerinden hello hello işlem sunucusu ve hello yapılandırma sunucusu olması gerekir. Bu koşul karşılanmazsa, yeniden koruma başarılı olur, ancak çoğaltma başarısız olur.


> [!NOTE]
> Merhaba ana hedef sunucusunu yüklemeden önce bu hello denetleyin **/etc/hosts** dosya hello sanal makinedeki tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı toohello IP adreslerini eşlemek giriş içerir.

1. Merhaba parola alanından kopyalama **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** hello yapılandırma sunucusundaki. Olarak Kaydet **passphrase.txt** hello çalıştırarak aynı yerel dizine hello komutu aşağıdaki:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Örnek: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Merhaba yapılandırma sunucunun IP adresini not edin. Merhaba sonraki adımda ihtiyaç.

3. Komut tooinstall hello ana hedef sunucusu aşağıdaki hello çalıştırın ve hello sunucu hello yapılandırma sunucusuna kaydedin.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Örnek: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Merhaba betik tamamlanana kadar bekleyin. Merhaba ana hedef başarıyla kaydederse, hello ana hedef üzerinde hello listelenen **Site Recovery altyapısı** hello portal sayfası.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Merhaba ana hedef etkileşimli bir yükleme kullanarak yükleme

1. Çalışma hello aşağıdaki tooinstall hello ana hedef komutu. Merhaba Aracısı rolü için seçin **ana hedef**.

    ```
    ./install
    ```

2. Yükleme için Hello varsayılan konum seçin ve ardından **Enter** toocontinue.

    ![Ana hedef yüklemesi için varsayılan konumu seçme](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Merhaba yükleme tamamlandıktan sonra hello yapılandırma sunucusu hello komut satırını kullanarak kaydedin.

1. Hello hello yapılandırma sunucusu IP adresini not alın. Merhaba sonraki adımda ihtiyaç.

2. Komut tooinstall hello ana hedef sunucusu aşağıdaki hello çalıştırın ve hello sunucu hello yapılandırma sunucusuna kaydedin.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Örnek: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Merhaba betik tamamlanana kadar bekleyin. Merhaba ana hedef kayıtlı başarıyla ise, hello ana hedef üzerinde hello listelenen **Site Recovery altyapısı** hello portal sayfası.


### <a name="upgrade-hello-master-target"></a>Merhaba ana hedef yükseltme

Merhaba yükleyiciyi çalıştırın. Bu hello aracı hello ana hedefte yüklü otomatik olarak algılar. tooupgrade, select **Y**.  Merhaba Kurulum tamamlandıktan sonra komutu aşağıdaki hello kullanarak yüklü hello ana hedef hello sürümünü denetleyin.

    ```
    cat /usr/local/.vx_version
    ```

Bu hello görebilirsiniz **sürüm** alan hello sürüm hello ana hedef sayısını verir.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>VMware araçları hello ana hedef sunucusuna yükleyin

Böylece hello veri depolarına bulabilir tooinstall VMware araçları hello ana hedefte gerekir. Merhaba Araçlar yüklü değilse hello yeniden koruma ekran hello veri depolarında listelenmiyor. Merhaba VMware araçları yüklendikten sonra toorestart gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba yükleme ve kaydetme hello ana hedefinin finsihed olduğunda hello ana hedef üzerinde hello görünür görebilirsiniz **ana hedef** bölümüne **Site Recovery altyapısı**, hello altında yapılandırma sunucusu genel bakış.

Şimdi devam edebilmeniz [yükü](site-recovery-how-to-reprotect.md), ardından yeniden çalışma.

## <a name="common-issues"></a>Genel sorunlar

* Bir ana hedef gibi tüm yönetim bileşenleri üzerinde depolama VMotion'ı kapatmanız emin olun. Merhaba ana hedef sonra başarılı bir yeniden koruma taşınırsa hello sanal makine disklerini (VMDKs) ayrılamıyor. Bu durumda, yeniden çalışma başarısız olur.

* Merhaba ana hedef tüm anlık görüntüleri hello sanal makineye sahip olmamalıdır. Anlık görüntüler varsa, yeniden çalışma başarısız olur.

* Toosome özel NIC yapılandırmaları bazı müşterilerin en son başlatma sırasında hello ağ arabirimi devre dışıdır ve hello ana hedef Aracısı başlatılamıyor. Aşağıdaki özelliklere bu hello doğru ayarladığınızdan emin olun. Bu özellikler hello Ethernet, dosyanın /etc/sysconfig/network-scripts/ifcfg kartı denetleyin-eth *.
    * BOOTPROTO dhcp =
    * ONBOOT = Evet

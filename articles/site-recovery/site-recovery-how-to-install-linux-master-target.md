---
title: "Yük devretme için bir Linux ana hedef sunucusu Azure'dan şirket içi yükleme | Microsoft Docs"
description: "Linux sanal makine yeniden korumayı önce bir Linux ana hedef sunucusu gerekir. Bir yüklemeyi öğrenin."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 11/22/2017
ms.author: rajanaki
ms.openlocfilehash: 7b2416617696e1df30b08f039ab39bfe7b57e093
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2017
---
# <a name="install-a-linux-master-target-server"></a>Bir Linux ana hedef sunucu yükle
Sanal makinelerinizi başarısız olduktan sonra sanal makineler şirket içi siteye geri başarısız olabilir. Yeniden çalışmak için Azure sanal makineden şirket içi siteye koruyun gerekir. Bu işlem için trafiği almak için bir şirket içi ana hedef sunucusu gerekir. 

Windows sanal makinesi korumalı sanal makineniz olması durumunda, bir Windows ana hedef gerekir. Bir Linux sanal makine için bir Linux ana hedef gerekir. Oluşturun ve Linux ana hedefinin yüklemek hakkında bilgi almak için aşağıdaki adımları okuyun.

> [!IMPORTANT]
> 9.10.0 sürümünden itibaren ana hedef sunucusu, en son ana hedef sunucusu yalnızca bir Ubuntu 16.04 sunucusuna yüklenebilir. Yeni yüklemeler CentOS6.6 sunucularda izin verilmez. Ancak, eski ana hedef sunucularınızı 9.10.0 kullanarak yükseltmeye devam edebilirsiniz sürümü.

## <a name="overview"></a>Genel Bakış
Bu makalede, bir Linux ana hedef yükleme için yönergeler sağlar.

POST yorumlarınızı ve sorularınızı bu makalenin veya sonunda [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Ön koşullar

* Ana hedef dağıtmak için konakta seçmek için yeniden çalışma var olan bir şirket içi sanal makine veya yeni bir sanal makine olacağını durumunda belirleyin. 
    * Mevcut bir sanal makine için ana hedef konağı sanal makinenin veri depolarına erişimine sahip olmalıdır.
    * Şirket içi sanal makine mevcut değilse geri dönme sanal makine ana hedef olarak aynı ana bilgisayardaki oluşturulur. Ana hedef yüklemek için herhangi bir ESXi ana seçebilirsiniz.
* Ana hedef işlem sunucusu ve yapılandırma sunucusu ile iletişim kurabilen bir ağ üzerinde olmalıdır.
* Ana hedef sürümüne eşit veya daha önceki sürümlerinden işlem sunucusu ve yapılandırma sunucusu olması gerekir. Örneğin, yapılandırma sunucusu sürümü 9,4 ise, ana hedef sürümü 9,4 veya 9.3 ancak değil 9.5 olabilir.
* Ana hedef yalnızca bir VMware sanal makine ve bir fiziksel sunucuya yüklenebilir.

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a>Ana hedef boyutlandırma yönergelerine göre oluşturma

Ana hedef aşağıdaki boyutlandırma yönergelere uygun olarak oluşturun:
- **RAM**: 6 GB veya daha fazla
- **İşletim sistemi disk boyutu**: 100 GB veya daha fazla (CentOS6.6 yüklemek için)
- **Saklama sürücüsünün için ek disk boyutu**: 1 TB
- **CPU çekirdekleri**: 4 çekirdek ya da daha fazla bilgi

Aşağıdaki desteklenen Ubuntu tekrar desteklenir.


|Çekirdek serisi  |En fazla desteği  |
|---------|---------|
|4.4      |4.4.0-81-Generic         |
|4.8      |4.8.0-56-Generic         |
|4.10     |4.10.0-24-Generic        |


## <a name="deploy-the-master-target-server"></a>Ana hedef sunucusu dağıtma

### <a name="install-ubuntu-16042-minimal"></a>Ubuntu 16.04.2 yükleme en az

Aşağıdaki ele Ubuntu 16.04.2 64-bit işletim sistemi yüklemek için adımları.

**1. adım:** Git [bağlantı karşıdan](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) ve en yakın yansıtma hangi Merkezi'nden bir Ubuntu 16.04.2 en az 64-bit ISO'i seçin.

DVD sürücüsüne bir Ubuntu 16.04.2 en az 64-bit ISO tutmak ve sistem başlatın.

**2. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.

![Dil Seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**3. adım:** seçin **yükleme Ubuntu Server**ve ardından **Enter**.

![Ubuntu Server yüklemesi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**4. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.

![İngilizce tercih ettiğiniz dili seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**5. adım:** uygun seçeneği seçin **saat dilimi** Seçenekler listesinde ve ardından **Enter**.

![Doğru saat dilimini seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**6. adım:** seçin **Hayır** (varsayılan seçenek) ve ardından **Enter**.


![Klavye yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**7. adım:** seçin **İngilizce (ABD)** klavye ve ardından ülkeyi olarak **Enter**.

![ABD ülkeyi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**8. adım:** seçin **İngilizce (ABD)** klavye düzeni ve ardından olarak **Enter**.

![ABD İngilizcesi klavye düzeni seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**9. adım:** sunucunuzun için ana bilgisayar adı girin **ana bilgisayar adı** kutusuna ve ardından **devam**.

![Sunucunuz için ana bilgisayar adı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**10. adım:** bir kullanıcı hesabı oluşturmak için kullanıcı adını girin ve ardından **devam**.

![Bir kullanıcı hesabı oluşturun](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**11. adım:** yeni kullanıcı hesabı için parolayı girin ve ardından **devam**.

![Parolayı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**12. adım:** yeni kullanıcı için parolayı onaylayın ve ardından **devam**.

![Parolalar onaylayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**13. adım:** seçin **Hayır** (varsayılan seçenek) ve ardından **Enter**.

![Kullanıcılar ve parolaları ayarlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**14. adım:** görüntülenen saat dilimi doğru ise, seçin **Evet** (varsayılan seçenek) ve ardından **Enter**.

Saat dilimini yapılandırılacağını seçin **Hayır**.

![Saatin yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**15. adım:** bölümleme yöntemi seçeneklerinden birini **destekli - tüm disk kullanmak**ve ardından **Enter**.

![Bölümleme yöntemi seçeneğini belirleyin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**16. adım:** uygun disk seçin **Select disk bölümü** seçenekleri ve ardından **Enter**.


![Disk seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**17. adım:** seçin **Evet** disk ve ardından değişiklik yazmak için **Enter**.

![Değişiklikleri diske yazma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Adım 18:** varsayılan seçeneği seçin, **devam**ve ardından **Enter**.

![Varsayılan seçenek seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**19. adım:** sisteminize yükseltmeler yönetmek için uygun seçeneği belirleyin ve ardından **Enter**.

![Yükseltmeler yönetme seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Azure Site Recovery ana hedef sunucusu Ubuntu çok belirli bir sürümünü gerektirdiğinden, yükseltmeler sanal makine için devre dışı bırakılır çekirdek emin olmak gerekir. Etkinleştirilirse, normal bir yükseltme ana hedef sunucusunda çalışmasına neden. Seçtiğinizden emin olun **otomatik güncelleştirme** seçeneği.


**20. adım:** varsayılan seçenekleri seçin. SSH bağlantısı için openSSH istiyorsanız seçin **OpenSSH server** seçeneğini ve ardından **devam**.

![Yazılımı seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**21. adım:** seçin **Evet**ve ardından **Enter**.

![Yükleme oturumu kaz önyükleme yükleyicisi](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**22. adım:** önyükleme yükleyicisi yükleme için uygun aygıt seçin (tercihen **/dev/sda**) ve ardından **Enter**.

![Önyükleme yükleyicisi yükleme için bir cihaz seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**23. adım:** seçin **devam**ve ardından **Enter** yüklemenin tamamlanması için.

![Yüklemeyi tamamlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Yükleme tamamlandıktan sonra VM yeni kullanıcı kimlik bilgileriyle oturum açın. (Başvurmak **adım 10** daha fazla bilgi için.)

KÖK kullanıcı parolasını ayarlamak için aşağıdaki ekran görüntüsünde açıklanan adımları uygulayın. Ardından kök kullanıcı olarak oturum açın.

![KÖK kullanıcı parolasını ayarlayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a>Makine Yapılandırması için bir ana hedef sunucusu olarak hazırlama
Ardından, makine yapılandırması için bir ana hedef sunucusu olarak hazırlayın.

Bir Linux sanal makinedeki her bir SCSI sabit disk için kimliği almak için etkinleştirme **disk. EnableUUID = TRUE** parametre.

Bu parametre etkinleştirmek için aşağıdaki adımları uygulayın:

1. Sanal makineyi kapatın.

2. Sol bölmede sanal makine için girişe sağ tıklatın ve ardından **ayarlarını Düzenle**.

3. Seçin **seçenekleri** sekmesi.

4. Sol bölmede seçin **Gelişmiş** > **genel**ve ardından **yapılandırma parametrelerini** ekranın sağ alt bölümünde bulunan düğmesi.

    ![Seçenekler sekmesi](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    **Yapılandırma parametrelerini** seçeneği kullanılamaz makine çalışırken. Bu sekme etkin hale getirmek için sanal makineyi kapatın.

5. Olan bir satır olup olmadığını görmek **disk. EnableUUID** zaten mevcut.

    - Değeri varsa ve ayarlamak **False**, değerini değiştirin **doğru**. (Değerleri büyük küçük harfe duyarlı değildir.)

    - Değeri varsa ve ayarlamak **True**seçin **iptal**.

    - Değer yoksa seçin **Satır Ekle**.

    - Ad sütununda eklemek **disk. EnableUUID**ve ardından değeri **doğru**.

    ![Olup olmadığını denetleme disk. EnableUUID zaten var.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Çekirdek yükseltmeler devre dışı bırak

Azure Site Recovery ana hedef sunucusu Ubuntu belirli bir sürümünü gerektirir, çekirdek yükseltmeleri sanal makine için devre dışı emin olun.

Çekirdek yükseltmeler etkinleştirilirse, normal bir yükseltme ana hedef sunucusunda çalışmasına neden.

#### <a name="download-and-install-additional-packages"></a>İndirme ve ek paketler yükleme

> [!NOTE]
> Karşıdan yüklemek ve ek paketleri yüklemek için Internet bağlantısı olduğundan emin olun. Internet bağlantısı yoksa, el ile bu RPM paketleri bulun ve bunları yüklemeniz gerekir.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a>İçin Kurulum Yükleyici Al

Ana hedef Internet bağlantısı varsa, yükleyici indirmek için aşağıdaki adımları kullanabilirsiniz. Aksi takdirde, yükleyici işlem sunucusundan kopyalayın ve ardından yükleyin.

#### <a name="download-the-master-target-installation-packages"></a>Ana hedef yükleme paketleri indirin

[En son Linux ana hedef yükleme BITS karşıdan yükleme](https://aka.ms/latestlinuxmobsvc).

Linux kullanarak indirmek için şunu yazın:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Karşıdan yükle ve giriş dizininizde yükleyici sıkıştırmasını emin olun. İçin sıkıştırmasını açın, **/usr/yerel**, sonra da yükleme başarısız olur.


#### <a name="access-the-installer-from-the-process-server"></a>İşlem sunucusundan yükleyici erişim

1. İşlem sunucusunda Git **C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. İşlem sunucusundan gerekli yükleyici dosyasını kopyalayın ve kaydedileceği **latestlinuxmobsvc.tar.gz** giriş dizininizdeki.


### <a name="apply-custom-configuration-changes"></a>Özel yapılandırma değişikliklerini uygula

Özel yapılandırma değişiklikleri uygulamak için aşağıdaki adımları kullanın:


1. İkili untar için aşağıdaki komutu çalıştırın.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Çalıştırılacak komut ekran görüntüsü](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. İzin vermek için aşağıdaki komutu çalıştırın.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Komut dosyasını çalıştırmak için aşağıdaki komutu çalıştırın.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Komut dosyası yalnızca bir kez sunucusunda çalıştırın. Sunucuyu kapatın. Bir disk ekledikten sonra sunucu bir sonraki bölümde açıklandığı gibi yeniden.

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a>Saklama diskinin Linux ana hedef sanal makineye ekleyin

Saklama diskinin oluşturmak için aşağıdaki adımları kullanın:

1. Linux ana hedef sanal makine için yeni bir 1 TB disk ekleyin ve sonra makineyi başlatmak.

2. Kullanım **çok yollu -üm** saklama diskinin çok yollu kimliği öğrenmek için komutu.

    ```
    multipath -ll
    ```
    ![Saklama diskinin çok yollu kimliği](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Sürücüyü biçimlendirmek ve ardından yeni sürücüsünde bir dosya sistemi oluşturun.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Bir dosya sistemi sürücüsünde oluşturma](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Dosya sistemi oluşturduktan sonra saklama diskinin bağlayın.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Saklama diskinin bağlama](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Oluşturma **fstab** sistem her başlatıldığında saklama sürücüsünün bağlamak için girişi.
    ```
    vi /etc/fstab
    ```
    Seçin **Ekle** Dosya düzenlemeye başlamak için. Yeni bir satır oluşturun ve sonra aşağıdaki metni ekleyin. Önceki komutu vurgulanan çok yollu Kimliğinden temel disk çok yollu kimliği düzenleyin.

    **/dev/Eşleyici/ <Retention disks multipath id> /mnt/bekletme ext4 rw 0 0**

    Seçin **Esc**ve ardından **: wq** (yazma ve çıkın) Düzenleyicisi penceresini kapatın.

### <a name="install-the-master-target"></a>Ana hedef yükleyin

> [!IMPORTANT]
> Ana hedef sunucusu sürümüne eşit veya daha önceki sürümlerinden işlem sunucusu ve yapılandırma sunucusu olması gerekir. Bu koşul karşılanmazsa, yeniden koruma başarılı olur, ancak çoğaltma başarısız olur.


> [!NOTE]
> Ana hedef sunucusu yüklemeden önce denetleyin **/etc/hosts** dosya sanal makinedeki tüm ağ bağdaştırıcıları ile ilişkili IP adreslerini yerel ana bilgisayar adı Eşle giriş içerir.

1. Parola alanından kopyalama **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** yapılandırma sunucusundaki. Olarak Kaydet **passphrase.txt** aşağıdaki komutu çalıştırarak aynı yerel dizine:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Örnek: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Yapılandırma sunucusunun IP adresini not edin. Sonraki adımda ihtiyaç.

3. Ana hedef sunucusu yükleme ve yapılandırma sunucusuyla sunucuyu kaydetmek için aşağıdaki komutu çalıştırın.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Örnek: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Komut dosyası tamamlanana kadar bekleyin. Ana hedef başarıyla kaydederse, ana hedef listelendiğini **Site Recovery altyapısı** portal sayfası.


#### <a name="install-the-master-target-by-using-interactive-installation"></a>Ana hedef etkileşimli bir yükleme kullanarak yükleme

1. Ana hedef yüklemek için aşağıdaki komutu çalıştırın. Aracı, bu rolün seçin **ana hedef**.

    ```
    ./install
    ```

2. Yükleme için varsayılan konum seçin ve ardından **Enter** devam etmek için.

    ![Ana hedef yüklemesi için varsayılan konumu seçme](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Yükleme tamamlandıktan sonra komut satırını kullanarak yapılandırma sunucusuna kaydedin.

1. Yapılandırma sunucusu IP adresini not alın. Sonraki adımda ihtiyaç.

2. Ana hedef sunucusu yükleme ve yapılandırma sunucusuyla sunucuyu kaydetmek için aşağıdaki komutu çalıştırın.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Örnek: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Komut dosyası tamamlanana kadar bekleyin. Ana hedef başarıyla kaydedildi, ana hedef listelendiğini **Site Recovery altyapısı** portal sayfası.


### <a name="upgrade-the-master-target"></a>Ana hedefe yükseltme

Yükleyiciyi çalıştırın. Aracı ana hedef sunucudaki yüklendi otomatik olarak algılar. Yükseltmek için seçin **Y**.  Kurulum tamamlandıktan sonra aşağıdaki komutu kullanarak yüklü ana hedef sürümünü kontrol edin:

    ```
    cat /usr/local/.vx_version
    ```

Görebilirsiniz **sürüm** alan ana hedef sürüm sayısını verir.

### <a name="install-vmware-tools-on-the-master-target-server"></a>Ana hedef sunucusunda VMware Araçları'nı yüklemek

Böylece veri depolarına bulabilmesi için ana hedef sunucudaki VMware araçları yüklemeniz gerekir. Araçlar yüklü değilse, yeniden koruma ekran veri depolarında listelenen değil. VMware araçları yüklendikten sonra yeniden başlatmanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Yükleme ve ana hedef kaydı tamamladıktan sonra görünür ana hedef görebilirsiniz **ana hedef** bölümüne **Site Recovery altyapısı**, yapılandırma bölümünde sunucusuna genel bakış.

Şimdi devam edebilmeniz [yükü](site-recovery-how-to-reprotect.md), ardından yeniden çalışma.

## <a name="common-issues"></a>Genel sorunlar

* Bir ana hedef gibi tüm yönetim bileşenleri üzerinde depolama VMotion'ı kapatmanız emin olun. Ana hedef sonra başarılı bir yeniden koruma geçerse, sanal makine disklerini (VMDKs) ayrılamıyor. Bu durumda, yeniden çalışma başarısız olur.

* Ana hedef sanal makinedeki tüm anlık görüntüleri olmamalıdır. Anlık görüntüler varsa, yeniden çalışma başarısız olur.

* Bazı özel NIC yapılandırmaları bazı müşteriler, nedeniyle ağ arabirimini başlatma sırasında devre dışıdır ve ana hedef Aracısı'nı başlatamıyor. Aşağıdaki özellikler doğru ayarlandığından emin olun. Bu özellikler, Ethernet kartı dosyanın /etc/sysconfig/network-scripts/ifcfg denetleyin-eth *.
    * BOOTPROTO dhcp =
    * ONBOOT = Evet

---
title: "StorSimple Linux konağında MPIO aaaConfigure | Microsoft Docs"
description: "CentOS 6.6 çalıştıran bağlı StorSimple tooa Linux konağında MPIO yapılandırma"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>CentOS çalıştıran bir StorSimple konakta MPIO'yu yapılandırın
Bu makalede, Centos 6.6 ana bilgisayar sunucusunda hello adımları gerekli tooconfigure çoklu yol oluşturma g/ç (MPIO) açıklanmaktadır. iSCSI başlatıcıları aracılığıyla yüksek kullanılabilirlik için bağlı tooyour Microsoft Azure StorSimple cihaz Hello konak sunucusudur. Ayrıntı hello otomatik bulma çok yollu cihazların ve yalnızca StorSimple birimler için özel kurulum hello açıklar.

Bu yordam, StorSimple 8000 serisi cihazlar geçerli tooall hello modellerinin kullanılır.

> [!NOTE]
> Bu yordam, StorSimple sanal cihaz için kullanılamaz. Nasıl tooconfigure konak sunucuları sanal cihazınız için daha fazla bilgi için bkz.
> 
> 

## <a name="about-multipathing"></a>Çoklu yol oluşturma hakkında
Merhaba çoklu yol oluşturma özelliği sağlar, tooconfigure ana sunucu ile bir depolama aygıtı arasında birden çok g/ç yollar. Bu g/ç yolları ayrı kablo, anahtarlar, ağ arabirimleri ve denetleyicileri dahil edebileceğiniz fiziksel SAN bağlantılardır. Çoklu yol oluşturma hello g/ç yolu, tooconfigure tüm toplanan hello yollar ile ilişkili yeni bir cihaz toplar.

Çoklu yol oluşturma Hello amacı iki Katlama şöyledir:

* **Yüksek kullanılabilirlik**: hello g/ç yolu (örneğin, bir kablo, anahtar, ağ arabirimi veya denetleyicisi) herhangi bir öğeyi başarısız olursa alternatif bir yol sağlar.
* **Yük Dengeleme**: depolama Cihazınızı hello yapılandırmasına bağlı olarak bu hello hello g/ç yolları yükleri algılama ve dinamik olarak bu yükleri dengelenmesi performansı artırabilir.

### <a name="about-multipathing-components"></a>Çoklu yol oluşturma bileşenleri hakkında
Çoklu yol oluşturma Linux içindeki çekirdek bileşenleri ve aşağıdaki tabloda gibi kullanıcı alanı bileşenleri oluşur.

* **Çekirdek**: hello ana bileşendir hello *aygıt Eşleyici* g/ç yeniden yönlendirmeler ve yolları ve yol grupları için yük devretmeyi destekler.

* **Kullanıcı alanı**: Bunlar *çok yollu Araçları* , multipathed cihazları yönetme hello aygıt Eşleyici çok yollu modülü yönlendirerek hangi toodo. Merhaba araçları şunlardan oluşur:
   
   * **Çok yollu**: listeler ve multipathed cihazları yapılandırır.
   * **Multipathd**: arka plan programı çok yollu ve izleyiciler hello yolları yürütür.
   * **Devmap adı**: devmaps için anlamlı bir aygıt adı tooudev sağlar.
   * **Kpartx**: Doğrusal devmaps toodevice bölümleri toomake çok yollu eşlemeleri bölümlenebilir eşler.
   * **MultiPath.conf**: kullanılan toooverwrite hello yerleşik yapılandırma tablosu çok yollu arka plan programı için yapılandırma dosyası.

### <a name="about-hello-multipathconf-configuration-file"></a>Merhaba multipath.conf yapılandırma dosyası hakkında
Merhaba yapılandırma dosyası `/etc/multipath.conf` hello çoğunu çoklu yol oluşturma özellikleri kullanıcı tarafından yapılandırılabilir hale getirir. Merhaba `multipath` komut ve hello çekirdek arka plan programı `multipathd` bu dosyada bulunan bilgileri kullanın. Merhaba dosya yalnızca hello çok yollu cihazların Merhaba yapılandırması sırasında alınmadığında. Merhaba çalıştırmadan önce tüm değişiklikleri yapıldığından emin olun `multipath` komutu. Daha sonra hello dosyasını değiştirirseniz toostop gerekir ve multipathd hello değişiklikleri tootake etkisi için yeniden başlatma.

Merhaba multipath.conf beş bölümü vardır:

- **Sistem düzeyinde varsayılanlarını** *(varsayılan)*: sistem düzeyinde varsayılanlarını geçersiz kılabilirsiniz.
- **Kara listede aygıtları** *(kara liste)*: cihaz Eşleyicisi tarafından denetlenmeyen cihazların Merhaba listesi belirtebilirsiniz.
- **Özel durumlar kara listeye** *(blacklist_exceptions)*: hello kara listeye listelenen olsa bile çok yollu cihazlar kabul belirli aygıtları toobe tanımlayabilirsiniz.
- **Depolama denetleyicisi belirli ayarları** *(aygıtlar)*: Satıcı ve ürün bilgilerine sahip uygulanan toodevices olacaktır yapılandırma ayarları belirtebilirsiniz.
- **Aygıt belirli ayarları** *(multipaths)*: Bu bölümde toofine ayarlama hello yapılandırma ayarlarını tek tek LUN'larını kullanabilirsiniz.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Çoklu yol oluşturma StorSimple bağlı tooLinux ana bilgisayarda yapılandırma
Bir StorSimple cihazı bağlı tooa Linux ana yüksek kullanılabilirlik için yapılandırılabilir ve Yük Dengeleme. Örneğin, iki arabirim toohello SAN bağlı bağlı toohello SAN ve hello aygıtın iki arabirim Hello Linux ana bilgisayar varsa, bu arabirimleri olan gibi hello aynı alt ağda sonra olacaktır 4 yolları kullanılabilir. Her veri arabirimi hello cihaz ve ana bilgisayar arabirimde farklı bir IP alt ağ (ve değil yönlendirilebilir) varsa, ancak sonra yalnızca 2 yolları kullanılabilir. Çoklu yol oluşturma tooautomatically yapılandırabileceğiniz tüm hello kullanılabilir yolları Bul, bu yollar için bir Yük Dengeleme algoritması seçin, yalnızca StorSimple birimler için belirli yapılandırma ayarları uygulamak ve ardından etkinleştirmek ve çoklu yol oluşturma doğrulayın.

Merhaba aşağıdaki yordamı nasıl tooconfigure olması bir StorSimple cihaz kaydedildiğinde iki ağ arabirimi ile iki ağ arabirimi ile bağlı tooa konak açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde, CentOS sunucu ve StorSimple cihazınız için yapılandırma önkoşulları hello ayrıntıları verilmektedir.

### <a name="on-centos-host"></a>CentOS konakta
1. CentOS ana bilgisayar 2 ağ arabirimleri etkin olduğundan emin olun. Şunu yazın:
   
    `ifconfig`
   
    iki ağ arabirimleri hello aşağıdaki örnek hello çıkış gösterir (`eth0` ve `eth1`) hello konakta yok.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Yükleme *iSCSI-Başlatıcı-yardımcı programları* CentOS sunucunuzda. Aşağıdaki adımları tooinstall hello gerçekleştirmek *iSCSI-Başlatıcı-yardımcı programları*.
   
   1. Oturum açma `root` CentOS ana bilgisayarınızın INTO.
   2. Merhaba yüklemek *iSCSI-Başlatıcı-yardımcı programları*. Şunu yazın:
      
       `yum install iscsi-initiator-utils`
   3. Merhaba sonra *iSCSI-Başlatıcı-yardımcı programları* başarıyla yüklenmiş hello iSCSI hizmetini başlatın. Şunu yazın:
      
       `service iscsid start`
      
       Olaylar üzerinde `iscsid` gerçekten başlatmak ve hello Mayıs `--force` seçeneği gerekebilir
   4. iSCSI başlatıcısı kullanım hello önyükleme süre boyunca etkin olduğunu tooensure `chkconfig` tooenable hello hizmet komutu.
      
       `chkconfig iscsi on`
   5. düzgün şekilde olan Kurulum, tooverify hello komutu çalıştırın:
      
       `chkconfig --list | grep iscsi`
      
       Örnek çıktı aşağıda gösterilmiştir.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Yukarıdaki örnek Hello iSCSI ortamınızı önyükleme zamanında çalışma Düzey 2, 3, 4 ve 5 çalışacağını görebilirsiniz.
3. Yükleme *aygıt-Eşleyici-çok yollu*. Şunu yazın:
   
    `yum install device-mapper-multipath`
   
    Merhaba yüklemesi başlatılır. Tür **Y** onaylamanız istendiğinde toocontinue.

### <a name="on-storsimple-device"></a>StorSimple cihazında
StorSimple Cihazınızı olmalıdır:

* İSCSI için iki arabirimin en az. iki arabirim StorSimple Cihazınızda iSCSI etkin tooverify hello StorSimple cihazınız için Klasik Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:
  
  1. StorSimple cihazınız için hello Klasik portalında oturum açın.
  2. StorSimple Yöneticisi hizmetiniz seçin, **aygıtları** ve hello belirli StorSimple cihazı seçin. Tıklatın **yapılandırma** ve hello ağ arabirimi ayarlarını doğrulayın. İki iSCSI etkin ağ arabirimlerine sahip bir ekran görüntüsü aşağıda gösterilmiştir. Burada veri 2 ve veri 3, her iki 10 GbE arabirimleri iSCSI için etkinleştirilir.
     
      ![MPIO StorsSimple veri 2 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple veri 3 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      Merhaba, **yapılandırma** sayfası
     
     1. Her iki ağ arabirimleri iSCSI etkin olduğundan emin olun. Merhaba **iSCSI etkin** alan çok ayarlanmalıdır**Evet**.
     2. Merhaba ağ arabirimleri hello sahip olduğundan emin olun aynı hızı, ikisi de 1 GbE veya 10 GbE olmalıdır.
     3. Merhaba iSCSI etkin arabirimlerin Hello IPv4 adreslerini not edin ve hello ana bilgisayarda daha sonra kullanmak için kaydedin.
* StorSimple Cihazınızda Hello iSCSI arabirimleri hello CentOS sunucusundan erişilebilir olmalıdır.
      tooverify Bu, ana bilgisayar sunucusunda tooprovide hello IP adresleri, StorSimple iSCSI etkin ağ arabirimlerinin gerekir. Merhaba kullanılan komutlar ve karşılık gelen çıktı veri2 ile Merhaba (10.126.162.25) ve DATA3 (10.126.162.26) aşağıda gösterilmiştir:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Donanım yapılandırması
Merhaba iki iSCSI ağ arabirimleri artıklık için ayrı yazmalar bağlanmak öneririz. Aşağıdaki Hello şekilde hello yüksek kullanılabilirlik için önerilen donanım yapılandırması ve CentOS sunucunuz ve StorSimple cihazı için çoklu yol oluşturma Yük Dengeleme gösterilmektedir.

![StorSimple tooLinux ana bilgisayar için MPIO donanım yapılandırması](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Şekil önceki hello gösterildiği gibi kullanın:

* StorSimple Cihazınızı iki denetleyicileri Aktif-Pasif yapılandırmayla kullanılıyor.
* İki SAN anahtarları bağlı tooyour aygıt denetleyicileri etkilenir.
* StorSimple Cihazınızda iki iSCSI başlatıcıları etkinleştirilir.
* İki ağ arabirimi, CentOS ana bilgisayarda etkin.

Merhaba ana bilgisayar ve veri arabirimleri yönlendirilebilir olması durumunda yapılandırma yukarıda hello cihaz ve hello ana bilgisayar arasında 4 ayrı yollar sunacak.

> [!IMPORTANT]
> * 1 GbE ve çoklu yol oluşturma için 10 GbE ağ arabirimleri karıştırmamanızı öneririz. İki ağ arabirimleri kullanılırken, her iki hello arabirimleri hello aynı türde olmalıdır.
> * Veri2 ve DATA3 10 GbE ağ arabirimleri ise, StorSimple Cihazınızda DATA0, Veri1, DATA4 ve DATA5 1 GbE arabirimlerdir. |
> 
> 

## <a name="configuration-steps"></a>Yapılandırma adımları
Merhaba yapılandırma adımları için çoklu yol oluşturma hello kullanılabilir yollar çoklu yol oluşturma etkinleştirme ve son olarak hello yapılandırmasını doğrulama hello Yük Dengeleme algoritması toouse, belirtme, otomatik bulma için yapılandırmayı içerir. Bu adımların her biri aşağıdaki bölümlerde hello ayrıntılı ele alınmıştır.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>1. adım: çoklu yol oluşturma otomatik bulma için yapılandırma
Merhaba çok yollu desteklenen cihazları otomatik olarak bulunan ve yapılandırılmış.

1. Initialize `/etc/multipath.conf` dosya. Şunu yazın:
   
     `mpathconf --enable`
   
    Merhaba komutu yukarıda oluşturacak bir `sample/etc/multipath.conf` dosyası.
2. Çok yollu hizmetini başlatın. Şunu yazın:
   
    `service multipathd start`
   
    Çıktı aşağıdaki hello görürsünüz:
   
    `Starting multipathd daemon:`
3. Multipaths otomatik olarak bulmayı etkinleştirin. Şunu yazın:
   
    `mpathconf --find_multipaths y`
   
    Bunu hello Varsayılanları bölümünü değiştirmek, `multipath.conf` aşağıda gösterildiği gibi:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>2. adım: StorSimple birimler için çoklu yol oluşturmayı yapılandırma
Varsayılan olarak, tüm cihazların Merhaba multipath.conf dosyasında listelenen siyah ve atlanır. StorSimple cihazları birimlerin toocreate kara liste özel durumları tooallow olması gerekir.

1. Merhaba Düzenle `/etc/mulitpath.conf` dosya. Şunu yazın:
   
    `vi /etc/multipath.conf`
2. Merhaba multipath.conf dosyasında Hello blacklist_exceptions bölümünü bulun. StorSimple Cihazınızı Bu bölümde bir kara liste özel olarak listelenen toobe gerekir. İlgili bu dosya toomodify bunu (kullanımı yalnızca hello belirli modelinin kullanmakta olduğunuz hello aygıt) gösterildiği gibi satırları açıklamadan çıkarın:
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>3. adım: hepsini çoklu yol oluşturmayı yapılandırma
Bu Yük Dengeleme algoritması tüm hello kullanılabilir multipaths toohello etkin denetleyicisi Dengeli, hepsini bir biçimde kullanır.

1. Merhaba Düzenle `/etc/multipath.conf` dosya. Şunu yazın:
   
    `vi /etc/multipath.conf`
2. Merhaba altında `defaults` bölümü, kümesi hello `path_grouping_policy` çok`multibus`. Merhaba `path_grouping_policy` hello varsayılan yolu gruplandırma İlkesi tooapply toounspecified multipaths belirtir. Merhaba Varsayılanları bölümü, aşağıda gösterildiği gibi görünecektir.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Merhaba en yaygın değerlerini `path_grouping_policy` içerir:
> 
> * Yük devretme öncelik grubu başına 1 yolu =
> * multibus 1 önceliği grubundaki tüm geçerli yolu =
> 
> 

### <a name="step-4-enable-multipathing"></a>4. adım: Etkinleştirme çoklu yol oluşturma
1. Merhaba yeniden `multipathd` arka plan programı. Şunu yazın:
   
    `service multipathd restart`
2. Merhaba çıktı aşağıda gösterildiği gibi olacaktır:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>5. adım: çoklu yol oluşturma doğrulayın
1. Önce iSCSI bağlantı hello StorSimple aygıtla şu şekilde kurulduğundan emin olun:
   
   a. StorSimple Cihazınızı bulur. Şunu yazın:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    Aşağıda gösterildiği gibi 10.126.162.25 DATA0 için IP adresi olduğundan ve bağlantı noktası 3260 hello StorSimple cihazı giden iSCSI trafiği için açıldığında hello çıktısı şöyledir:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Kopya hello StorSimple Cihazınızı IQN `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, çıktı önceki hello gelen.

   b. Toohello aygıt hedef IQN kullanarak bağlanın. Merhaba StorSimple cihaz burada hello iSCSI hedefi değil. Şunu yazın:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Merhaba aşağıdaki örnek çıkış hedefiyle IQN gösterir, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. Merhaba çıkış aygıtınızda toohello iki iSCSI etkin ağ arabirimi başarıyla bağlandıysanız gösterir.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Yalnızca bir ana bilgisayar arabirimi ve iki yollarını burada görürseniz, sonra tooenable ana bilgisayar üzerindeki her iki hello arabirimleri iSCSI için yeterlidir. Merhaba izleyebilirsiniz [ayrıntılı Linux belgelerindeki yönergeleri](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Gösterilen toohello CentOS hello StorSimple cihazı sunucusundan bir birimdir. Daha fazla bilgi için bkz: [6. adım: birim oluşturma](storsimple-deployment-walkthrough.md#step-6-create-a-volume) Merhaba, StorSimple Cihazınızda Klasik Azure Portalı aracılığıyla.

3. Merhaba kullanılabilir yollar doğrulayın. Şunu yazın:

      ```
      multipath –l
      ```

      Aşağıdaki örneğine hello hello çıktı iki ağ arabirimi için bir StorSimple cihazı bağlı tooa tek ana bilgisayar ağ arabiriminde iki kullanılabilir yollar ile gösterilir.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Çoklu yol oluşturma sorunlarını giderme
Çoklu yol oluşturma yapılandırması sırasında herhangi bir sorunla çalıştırırsanız, bu bölümde bazı yararlı ipuçları sağlanır.

Q. Merhaba değişiklikleri görüntülenmemesini `multipath.conf` etkisi alma dosyası.

A. Tüm değişiklikleri toohello yaptıysanız `multipath.conf` dosyası toorestart hello çoklu yol oluşturma hizmeti gerekir. Merhaba aşağıdaki komutu yazın:

    service multipathd restart

Q. Merhaba StorSimple cihazı iki ağ arabirimlerindeki ve iki ağ arabirimi hello ana bilgisayarda etkin. Merhaba kullanılabilir yollar listelediğinizde, yalnızca iki yolu bakın. I toosee dört kullanılabilir yollar bekleniyordu.

A. Merhaba iki yolları hello üzerinde olduğundan emin olun aynı alt ağ ve yönlendirilebilir. Merhaba ağ arabirimleri farklı VLAN'ları ve değil yönlendirilebilir varsa, yalnızca iki yolu görürsünüz. Tek yönlü tooverify bu toomake hello StorSimple cihazı bir ağ arabiriminde hem hello konak arabirimlerden ulaşabildiğimizden emin olur. Çok gerekir[Microsoft Support başvurun](storsimple-contact-microsoft-support.md) gibi bu doğrulama yalnızca bir destek oturumu yapılabilir.

Q. Kullanılabilir yollar listelediğinizde, herhangi bir çıktı görmezsiniz.

A. Genellikle, öneren hello çoklu yol oluşturma arka plan programı ile ilgili bir sorun multipathed yollar görmesini değil ve bu büyük olasılıkla herhangi bir sorun burada hello arasındadır `multipath.conf` dosya.

Hello çok yollu listelerini yanıt ayrıca herhangi bir diski yok anlamına gelebilir gibi aslında bazı disklerin toohello hedef bağlandıktan sonra görebileceğini denetleme değer olacaktır.

* Komut toorescan hello SCSI veri yolu izleyerek hello kullan:
  
    `$ rescan-scsi-bus.sh `(sg3_utils paketinin bir parçası)
* Merhaba aşağıdaki komutları yazın:
  
    `$ dmesg | grep sd*`
     
     Veya
  
    `$ fdisk –l`
  
    Bu yakın zamanda eklenen diskler ayrıntılarını döndürür.
* toodetermine bir StorSimple disk olup olmadığını hello aşağıdaki komutları kullanın:
  
    `cat /sys/block/<DISK>/device/model`
  
    Bu, bir StorSimple disk olup olmadığını belirleyen bir dize döndürür.

Büyük olasılıkla ancak olası nedeni daha az A eski iscsid da olabilir PID. Merhaba iSCSI oturumunu kapatmak komutu toolog aşağıdaki hello kullan:

    iscsiadm -m node --logout -p <Target_IP>

StorSimple cihazınız hello iSCSI hedef tüm bağlı hello ağ arabirimleri için bu komutu yineleyin. Tüm hello iSCSI oturumlardan kapattınız sonra hello iSCSI hedef IQN tooreestablish hello iSCSI oturumu kullanın. Merhaba aşağıdaki komutu yazın:

    iscsiadm -m node --login -T <TARGET_IQN>


Q. Cihazımı Güvenilenler listesine olup olmadığından emin değilim.

A. tooverify Cihazınızı Güvenilenler listesine, olup, sorun giderme etkileşimli komutunu aşağıdaki hello kullanın:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Daha fazla bilgi için çok Git[etkileşimli komutu çoklu yol oluşturma için sorun giderme kullanmak](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Yararlı komutların listesi
| Tür | Komut | Açıklama |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |İSCSI Hizmeti |
| &nbsp; |`service iscsid stop` |İSCSI hizmetini durdurun |
| &nbsp; |`service iscsid restart` |İSCSI hizmetini yeniden başlatın |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Belirtilen hello kullanılabilir hedeflerde Bul adresi |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Toohello iSCSI hedef oturum |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Merhaba iSCSI hedefi Oturumu Kapat |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |İSCSI Başlatıcı adı yazdırma |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Merhaba iSCSI oturumu ve hello konakta bulunan birim Hello durumunu denetleyin |
| &nbsp; |`iscsi –m session` |Merhaba StorSimple cihazı Hello konak arasında kurulan tüm hello iSCSI oturumları gösterir |
|  | | |
| **Çoklu yol oluşturma** |`service multipathd start` |Çok yollu arka plan programı Başlat |
| &nbsp; |`service multipathd stop` |Çok yollu arka plan programı durdurun |
| &nbsp; |`service multipathd restart` |Çok yollu arka plan programı yeniden başlatın |
| &nbsp; |`chkconfig multipathd on` </br> OR </br> `mpathconf –with_chkconfig y` |Çok yollu arka plan programı toostart önyükleme sırasında etkinleştir |
| &nbsp; |`multipathd –k` |Sorun giderme için hello etkileşimli konsolunu başlatın |
| &nbsp; |`multipath –l` |Liste çok yollu bağlantıları ve cihazlar |
| &nbsp; |`mpathconf --enable` |Bir örnek mulitpath.conf dosya oluşturma`/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Sonraki adımlar
Linux ana bilgisayarına MPIO yapılandırma gibi CentoS 6.6 belgeleri aşağıdaki toorefer toohello de gerekebilir:

* [CentOS MPIO ayarlama](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Linux eğitim Kılavuzu](http://linux-training.be/files/books/LinuxAdm.pdf)


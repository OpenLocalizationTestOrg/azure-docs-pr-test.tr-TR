---
title: VMware sanal dizisinde StorSimple aaaProvision | Microsoft Docs
description: "StorSimple sanal dizinin dağıtım serisi ikinci Bu öğreticide, bir VMware sanal aygıt sağlama içerir."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>StorSimple sanal dizinin - VMware sağlama dağıtma
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Genel Bakış
Bu öğretici açıklar nasıl tooprovision ve tooa StorSimple sanal dizinin VMware ESXi 5.5 çalıştıran bir konak sistemi ve üstü bağlanın. Bu makale, Azure portalında ve Microsoft Azure kamu bulut hello StorSimple sanal dizi toohello dağıtım geçerlidir.

Tooa sanal cihaza bağlanmak ve yönetici ayrıcalıkları tooprovision gerekir. Merhaba sağlama ve ilk kurulum yaklaşık 10 dakika toocomplete alabilir.

## <a name="provisioning-prerequisites"></a>Sağlama önkoşulları
Önkoşullar tooprovision sanal cihazı VMware ESXi 5.5 çalıştıran konak sisteminde hello ve yukarıdaki aşağıdaki gibidir.

### <a name="for-hello-storsimple-device-manager-service"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti
Başlamadan önce aşağıdakilerden emin olun:

* Tüm hello adımları tamamlamış [hazırlama hello portal StorSimple sanal dizini](storsimple-virtual-array-deploy1-portal-prep.md).
* Azure portal hello için VMware hello sanal cihaz görüntüsü yüklediniz. Daha fazla bilgi için bkz: **adım 3: indirme hello sanal aygıt resmi** , [StorSimple sanal dizinin kılavuzu için hazırlama hello portalı](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Merhaba StorSimple sanal cihaz için
Sanal cihazı dağıtmadan önce emin olun:

* Hyper-V çalıştıran erişim tooa ana bilgisayar sistemi sahip (2008 R2 veya sonrası) olması kullanılan tooa hazırlayabilirsiniz, bir cihaz.
* Merhaba ana bilgisayar sistemidir mümkün toodedicate kaynakları tooprovision sanal Cihazınızı hello:

  * 4 çekirdek en az.
  * En az 8 GB RAM. Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler. 16 GB RAM toosupport 2-4 milyon dosyaları gerekir.
  * Bir ağ arabirimi.
  * Sistem verileri için 500 GB sanal disk.

### <a name="for-hello-network-in-datacenter"></a>Veri merkezinde Hello ağ için
Başlamadan önce aşağıdakilerden emin olun:

* Merhaba ağ gereksinimleri toodeploy StorSimple sanal cihazı ve yapılandırılmış hello veri merkezi ağ hello gereksinimlerine uygun geçirdikten. 

## <a name="step-by-step-provisioning"></a>Adım adım sağlama
tooprovision ve tooa sanal cihaza bağlanmak, aşağıdaki adımları tooperform hello gerekir:

1. Merhaba ana bilgisayar sistemi yeterli kaynakları toomeet hello minimum sanal cihaz gereksinimleri olduğundan emin olun.
2. Sanal cihazı, hipervizörde sağlayın.
3. Merhaba sanal cihazı başlatmak ve başlangıç IP adresi alın.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>1. adım: ana bilgisayar sistemi minimum sanal cihaz gereksinimlerini karşıladığından emin olun.
Sanal cihazı toocreate, şunları yapmanız gerekir:

* VMware ESXi Server 5.5 çalışan erişim tooa ana bilgisayar sistemi ve üstü.
* VMware vSphere istemci sistem toomanage hello ESXi ana bilgisayar üzerinde.

  * 4 çekirdek en az.
  * En az 8 GB RAM. Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler. 16 GB RAM toosupport 2-4 milyon dosyaları gerekir.
  * Bir ağ arabirimi yönlendirme trafiği tooInternet özellikli toohello ağa bağlı. Merhaba en düşük Internet bant genişliği hello cihazın en iyi çalışmak için 5 MB/sn tooallow olmalıdır.
  * Veri için 500 GB sanal disk.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>2. adım: hiper yönetici sanal bir aygıt sağlama
Aşağıdaki adımları tooprovision, hiper yönetici sanal bir aygıt hello gerçekleştirin.

1. Sisteminizde Hello sanal cihaz görüntüsü kopyalayın. Bu sanal görüntü hello Azure portal aracılığıyla indirilir.

   1. Merhaba son görüntü dosyasını karşıdan emin olun. Merhaba görüntü daha önce yüklediyseniz, hello son görüntüsüne sahip tooensure yeniden yükleyin. Merhaba son görüntü (yerine bir) iki dosya vardır.
   2. Merhaba yordamda daha sonra bu görüntüyü kullanma gibi hello görüntü kopyaladığınız hello konumunu not edin.

2. İçinde toohello hello vSphere istemci kullanarak ESXi sunucusunda oturum açın. Toohave yönetici ayrıcalıkları toocreate bir sanal makine gerekir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. Hello sol bölmede hello stok bölümdeki hello vSphere İstemcisi'nde hello ESXi sunucu seçin.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Merhaba VMDK toohello ESXi sunucusunda yükleyin. Toohello gidin **yapılandırma** hello sağ bölmedeki sekmesi. Altında **donanım**seçin **depolama**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. Hello bölmesini altında sağ **Datastores**, hello tooupload hello VMDK istediğiniz veri deposu seçin. Merhaba veri deposu, yeterli boş alan hello işletim sistemi ve veri diskleri olması gerekir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Sağ tıklatıp **Gözat veri deposu**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. A **veri deposu tarayıcı** penceresi görüntülenir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Merhaba araç çubuğunda, ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) simgesi toocreate yeni bir klasör. Merhaba klasör adı belirtin ve bunu not edin. Bu klasör adı (en iyisi önerilir) bir sanal makine oluştururken daha sonra kullanacaksınız. **Tamam** düğmesine tıklayın.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Merhaba yeni klasör hello'hello ' nin sol bölmesinde görünür **veri deposu tarayıcı**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Merhaba karşıya yükleme simgesini ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) seçip **dosyasını karşıya yükle**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Gözat ve indirdiğiniz toohello VMDK dosyaları gelin. İki dosya vardır. Bir dosya tooupload seçin.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Tıklatın **açık**. Merhaba VMDK dosya toohello Hello karşıya veri deposu başlatır belirtilmiş. Merhaba dosya tooupload için birkaç dakika sürebilir.
13. Merhaba karşıya yükleme tamamlandıktan sonra oluşturduğunuz hello klasördeki hello veri deposu hello dosyasına bakın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Şimdi hello ikinci VMDK dosya toohello karşıya aynı veri deposu.
14. Toohello vSphere istemci penceresine dönün. Seçili ESXi sunucusuyla sağ tıklatıp **yeni bir sanal makine**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. A **yeni sanal makine oluşturma** penceresi görünür. Merhaba üzerinde **yapılandırma** sayfası, select hello **özel** seçeneği. **İleri**’ye tıklayın.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Merhaba üzerinde **ad ve konum** sayfasında, sanal makinenize hello adını belirtin. Bu adı daha önce adım 8'de belirtilen hello klasörü (önerilen en iyi yöntem) adıyla aynı olmalıdır.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Merhaba üzerinde **depolama** sayfasında, istediğiniz toouse tooprovision VM'nizi bir veri deposu seçin.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Merhaba üzerinde **sanal makine sürüm** sayfasında, **sanal makine sürüm: 8**. Sürüm 8 too11 tüm desteklenir.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Merhaba üzerinde **konuk işletim sistemi** sayfası, select hello **konuk işletim sistemi** olarak **Windows**. İçin **sürüm**, hello açılır listeden seçin **Microsoft Windows Server 2012 (64 bit)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Merhaba üzerinde **CPU** sayfasında, hello ayarlamak **sanal Yuva sayısını** ve **çekirdek sanal yuva sayısı** , hello şekilde **çekirdektoplamsayısı**4 (veya daha fazla). **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Merhaba üzerinde **bellek** sayfasında, 8 GB (veya daha fazla) RAM belirtin. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Merhaba üzerinde **ağ** sayfasında, hello hello ağ arabirimlerinin sayısını belirtin. Merhaba en az bir ağ arabirimi gereksinimdir.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Merhaba üzerinde **SCSI denetleyicisi** sayfasında, hello varsayılanı kabul **LSI mantığı SAS Denetleyici**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Merhaba üzerinde **bir Disk seçin** sayfasında, **varolan bir sanal disk kullanmak**. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Merhaba üzerinde **mevcut Disk seçin** sayfasında **Disk dosya yolu**, tıklatın **Gözat**. Bu açılır bir **Gözat Datastores** iletişim. Merhaba VMDK karşıya nerede toohello konuma gidin. Başlangıçta karşıya hello iki dosya birleştirilmiş gibi hello veri deposu içinde yalnızca bir dosya artık bakın. Hello dosyasını tıklatıp **Tamam**. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Merhaba üzerinde **Gelişmiş Seçenekler** sayfasında hello varsayılanı kabul etmek ve tıklayın **sonraki**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Merhaba üzerinde **hazır tooComplete** sayfasında, hello yeni sanal makine ile ilişkili tüm hello ayarları gözden geçirin. Denetleme **tamamlanmadan önce hello sanal makine ayarlarını Düzenle**. Tıklatın **devam**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Merhaba üzerinde **sanal makineleri özellikleri** sayfasında hello **donanım** sekmesinde, hello aygıt donanım bulun. Seçin **yeni Sabit Disk**. **Ekle**'ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Gördüğünüz bir **Donanım Ekle** penceresi. Merhaba üzerinde **aygıt türü** sayfasında **Seç hello cihaz türünün tooadd istediğiniz**seçin **Sabit Disk**, tıklatıp **sonraki**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Merhaba üzerinde **bir Disk seçin** sayfasında, **yeni bir sanal disk oluşturma**. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Merhaba üzerinde **bir Disk oluşturmak** sayfasında, hello değiştirme **Disk boyutu** too500 GB (veya daha fazla). 500 GB hello minimum gereksinim olsa da, her zaman daha büyük bir disk sağlayabilirsiniz. Olamaz genişletmek veya bir kez sağlanan hello diski küçültmeye unutmayın. Disk tooprovision hello boyutu hakkında daha fazla bilgi için hello hello boyutlandırma bölümünde gözden [en iyi yöntemler belge](storsimple-ova-best-practices.md). Altında **Disk sağlama**seçin **ince provizyon**. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Merhaba üzerinde **Gelişmiş Seçenekler** sayfasında, hello varsayılanı kabul edin.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Merhaba üzerinde **hazır tooComplete** sayfasında, hello disk seçeneklerini gözden geçirin. **Son**'a tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Toohello sanal makine özellikleri sayfasına dönün. Yeni bir sabit disk tooyour sanal makineye eklenir. **Son**'a tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Sanal hello sağ bölmede seçili makinenizle, toohello gidin **Özet** sekmesi. Sanal makineniz Hello ayarlarını gözden geçirin.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Sanal makineniz şimdi sağlanır. Merhaba sonraki adımı toopower bu makinede ve başlangıç IP adresi alın.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Adım 3: hello sanal cihazı başlatmak ve hello IP Al
Sanal cihazınız adımları toostart aşağıdaki hello gerçekleştirmek ve tooit bağlanın.

#### <a name="toostart-hello-virtual-device"></a>toostart hello sanal cihaz
1. Merhaba sanal aygıt başlatın. Merhaba sol bölmede hello vSphere Configuration Manager, Cihazınızı seçin ve hello bağlam menüsü yukarı toobring sağ tıklatın. Seçin **güç** ve ardından **üzerinde güç**. Bu, sanal makinenizde güç. Merhaba alt hello durumunu görüntüleyebilirsiniz **son kullanılan görevler** hello vSphere istemci bölmesi.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. Merhaba kurulum görevlerini birkaç dakika toocomplete olur. Merhaba aygıt çalışmaya başladıktan sonra toohello gidin **konsol** sekmesi. Ctrl + Alt + Delete toolog toohello aygıtı gönderin. Alternatif olarak, hello konsol penceresinde hello imleç noktası ve Ctrl + Alt + INSERT tuşuna basın. Merhaba varsayılan kullanıcı *StorSimpleAdmin* ve hello varsayılan parola *Parola1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Güvenlik nedenleriyle hello ilk oturum açmada hello cihaz Yönetici parolasının süresi dolar. İstendiğinde toochange hello parola olur.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. En az 8 karakter içeren bir parola girin. Merhaba parola 3 çıkışı 4'ün bu gereksinimlerden birini içermelidir: büyük harf, küçük harfler, sayısal ve özel karakter. Merhaba parola tooconfirm yeniden girin. Bu hello parolanın değiştirilmesi bildirilir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Merhaba parola başarıyla değiştirildikten sonra hello sanal aygıt yeniden başlatabilirsiniz. Merhaba yeniden başlatma toocomplete bekleyin. Merhaba aygıt Hello Windows PowerShell konsolunda bir ilerleme çubuğu birlikte görüntülenebilir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Adım 6-8 yalnızca yukarı DHCP olmayan ortamda önyüklemesi sırasında uygulanır. Bir DHCP ortamında varsa, bu adımları atlayın ve toostep 9 gidin. Cihazınızı DHCP olmayan ortamda yukarı önyüklendiğinde ekran aşağıdaki hello görürsünüz.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Ardından, hello ağ yapılandırın.
7. Kullanım hello `Get-HcsIpAddress` sanal Cihazınızda etkin toolist hello ağ arabirimleri komutu. Cihazınızı etkin tek bir ağ arabirimi varsa, hello varsayılan atanan ad toothis arabirimidir `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Kullanım hello `Set-HcsIpAddress` cmdlet tooconfigure hello ağ. Bir örnek aşağıda verilmiştir:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Merhaba ilk Kurulum tamamlandıktan ve hello aygıt yukarı önyüklendikten sonra hello aygıt başlık metni görürsünüz. Başlangıç IP adresi ve hello başlık metni toomanage hello aygıtı görüntülenen hello URL'sini not edin. Bu IP adresi tooconnect toohello web kullanıcı Arabirimi, sanal cihaz ile tam hello yerel kurulumu ve kayıt kullanır.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (İsteğe bağlı) Yalnızca Cihazınızı hello Bulutu dağıtıyorsanız bu adımı gerçekleştirin. Şimdi Cihazınızda hello Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) mod olanak sağlar. Merhaba FIPS 140 standardı, gizli verilerin hello koruma için BİZE Federal hükümeti bilgisayar sistemleri tarafından kullanım için onaylanan şifreleme algoritmalarını tanımlar.

    1. cmdlet aşağıdaki hello çalıştırmak tooenable hello FIPS modunda:

        `Enable-HcsFIPSMode`
    2. Böylece Hello şifreleme doğrulama etkili hello FIPS modunda etkinleştirdikten sonra Cihazınızı yeniden başlatın.

       > [!NOTE]
       > Etkinleştirmek veya FIPS modundayken, Cihazınızda devre dışı. FIPS ve FIPS olmayan mod arasında değişen hello aygıt desteklenmiyor.
       >
       >

Cihazınızı hello en düşük yapılandırma gereksinimlerini karşılamıyor hello başlık metni (aşağıda gösterilen) bir hata görürsünüz. Yeterli kaynaklara toomeet hello en düşük gereksinimler sahip olması toomodify hello aygıt yapılandırması gerekir. Ardından, yeniden başlatın ve toohello aygıtı bağlayın. Toohello en düşük yapılandırma gereksinimlerini başvuran [1. adım: hello ana bilgisayar sistemi minimum sanal cihaz gereksinimlerini karşıladığından emin olmak](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Başka bir hata hello yerel web kullanıcı Arabirimi kullanılarak hello başlangıç yapılandırması sırasında yüz, iş akışları şu toohello başvurun:

* Tanılama çok testler[web kullanıcı Arabirimi Kurulumu sorunlarını giderme](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Günlük paketi oluşturmak ve günlük dosyalarını görüntülemek](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Sonraki adımlar
* [Dosya sunucusu olarak StorSimple sanal dizinizi ayarlama](storsimple-virtual-array-deploy3-fs-setup.md)
* [StorSimple sanal dizinizi bir iSCSI sunucusu olarak ayarla](storsimple-virtual-array-deploy3-iscsi-setup.md)

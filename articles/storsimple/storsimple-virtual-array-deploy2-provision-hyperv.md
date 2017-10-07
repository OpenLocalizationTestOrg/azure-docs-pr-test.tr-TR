---
title: Hyper-V sanal dizisinde StorSimple aaaProvision | Microsoft Docs
description: "StorSimple sanal dizinin dağıtım ikinci Bu öğreticide, Hyper-V sanal bir dizide sağlama içerir."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>StorSimple sanal dizinin - sağlama Hyper-v dağıtma
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Genel Bakış
Bu öğretici, StorSimple sanal nasıl tooprovision dizisi Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde açıklar. Bu makale, Azure portalında ve Microsoft Azure kamu bulut toohello dağıtım StorSimple sanal dizi geçerlidir.

Sanal bir dizi yapılandırma ve yönetici ayrıcalıkları tooprovision gerekir. Merhaba sağlama ve ilk kurulum yaklaşık 10 dakika toocomplete alabilir.

## <a name="provisioning-prerequisites"></a>Sağlama önkoşulları
Burada Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 üzerinde Hyper-V çalıştıran bir konak sisteminde, sanal bir dizi hello Önkoşullar tooprovision bulacaksınız.

### <a name="for-hello-storsimple-device-manager-service"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti
Başlamadan önce aşağıdakilerden emin olun:

* Tüm hello adımları tamamlamış [hazırlama hello portal StorSimple sanal dizini](storsimple-virtual-array-deploy1-portal-prep.md).
* Hyper-V için Azure portal hello hello sanal dizinin görüntü yüklediniz. Daha fazla bilgi için bkz: **adım 3: indirme hello sanal dizinin resmi** , [StorSimple sanal dizinin kılavuzu için hazırlama hello portalı](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > StorSimple sanal dizinin Hello üzerinde çalışan hello yazılımı yalnızca StorSimple cihaz Yöneticisi hizmeti hello ile kullanılabilir.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>StorSimple sanal dizinin Hello için
Sanal bir dizi dağıtmadan önce emin olun:

* Olması kullanılan tooa hazırlayabilirsiniz, bir cihaz Hyper-V Windows Server 2008 R2 veya sonraki sürümlerde çalışan erişim tooa ana bilgisayar sistemine sahiptir.
* Merhaba ana bilgisayar sistemidir mümkün toodedicate kaynakları tooprovision sanal dizinizi hello:

  * 4 çekirdek en az.
  * En az 8 GB RAM. Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler. 16 GB RAM toosupport 2-4 milyon dosyaları gerekir.
  * Bir ağ arabirimi.
  * Veri için 500 GB sanal disk.

### <a name="for-hello-network-in-hello-datacenter"></a>Merhaba veri merkezinde Hello ağ için
Başlamadan önce gereksinimleri toodeploy bir StorSimple sanal dizi ağ hello gözden geçirin ve hello veri merkezi ağ uygun şekilde yapılandırın. Daha fazla bilgi için bkz: [StorSimple sanal ağ gereksinimleri dizi](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Adım adım sağlama
tooprovision ve tooa sanal dizinin bağlanmak, aşağıdaki adımları tooperform hello gerekir:

1. Merhaba ana bilgisayar sistemi yeterli kaynakları toomeet hello minimum sanal dizinin gereksinimleri olduğundan emin olun.
2. Hiper yönetici sanal bir dizide sağlayın.
3. Merhaba sanal dizinin başlatın ve başlangıç IP adresi alın.

Bu adımların her biri aşağıdaki bölümlerde hello açıklanmıştır.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>1. adım: hello ana bilgisayar sistemi minimum sanal dizinin gereksinimleri karşıladığından emin olun
sanal bir dizi toocreate, şunlar gerekir:

* Windows Server 2012 R2, Windows Server 2012 veya Windows Server 2008 R2 SP1 yüklü hello Hyper-V rolü.
* Bir Microsoft Windows İstemcisi üzerindeki Microsoft Hyper-V Yöneticisi'ni toohello ana bağlı.

Merhaba sanal dizinin oluşturmakta olduğunuz donanım (ana bilgisayar sistemi) temel bu hello kaynakları tooyour sanal dizinin aşağıdaki mümkün toodedicate hello olduğundan emin olun:

* 4 çekirdek en az.
* En az 8 GB RAM. Dosya sunucusu olarak tooconfigure hello sanal dizinin planlıyorsanız, 8 GB 2 milyondan az dosyalarını destekler. 16 GB RAM toosupport 2-4 milyon dosyaları gerekir.
* Bir ağ arabirimi.
* Sistem verileri için 500 GB sanal disk.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>2. adım: hiper yönetici sanal bir dizide sağlama
Aşağıdaki adımları tooprovision bir aygıt, hiper yönetici hello gerçekleştirin.

#### <a name="tooprovision-a-virtual-array"></a>sanal bir dizi tooprovision
1. Windows Server ana bilgisayarında hello sanal dizinin görüntü tooa yerel sürücüye kopyalayın. Bu görüntü (VHD veya VHDX) hello Azure portal indirilir. Merhaba yordamda daha sonra bu görüntüyü kullanma gibi hello görüntü kopyaladığınız hello konumunu not edin.
2. Açık **Sunucu Yöneticisi'ni**. Merhaba sağ üst köşeden, tıklatın **Araçları** seçip **Hyper-V Yöneticisi'ni**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Windows Server 2008 R2 çalıştırıyorsanız, hello Hyper-V Yöneticisi'ni açın. Sunucu Yöneticisi'nde **rolleri > Hyper-V > Hyper-V Yöneticisi'ni**.
3. İçinde **Hyper-V Yöneticisi'ni**hello kapsam bölmesinde sistem düğümü tooopen hello bağlam menüsü sağ tıklayın ve ardından **yeni** > **sanal makine**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. Merhaba üzerinde **başlamadan önce** hello yeni sanal makine Sihirbazı sayfasını tıklatın **sonraki**.
5. Hello üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** sanal dizini. **İleri**’ye tıklayın.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. Merhaba üzerinde **nesil** sayfasında, hello aygıt resim türünü seçin ve ardından **sonraki**. Windows Server 2008 R2 kullanıyorsanız, bu sayfa görünmez.

   * Seçin **2. nesil** Windows Server 2012 veya sonraki bir .vhdx görüntüsü yüklediyseniz.
   * Seçin **1. nesil** Windows Server 2008 R2 veya sonraki bir .vhd görüntüsü yüklediyseniz.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. Merhaba üzerinde **atamak bellek** sayfasında, belirtin bir **başlangıç belleği** , en az **8192 MB**olmayan dinamik belleği etkinleştirme ve ardından **sonraki**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. Merhaba üzerinde **ağ yapılandırma** sayfasında, bağlı toohello Internet olan hello sanal anahtar belirtin ve ardından **sonraki**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. Merhaba üzerinde **sanal sabit diski bağlayın** sayfasında, **varolan bir sanal sabit diski kullanmak**hello sanal dizinin görüntü (.vhdx veya .vhd) hello konumunu belirtin ve ardından **sonraki**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Gözden geçirme hello **Özet** ve ardından **son** toocreate hello sanal makine.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. toomeet hello en düşük gereksinimler, 4 çekirdek gerekir. tooadd 4 sanal işlemci, ana bilgisayar sisteminizin hello seçin **Hyper-V Yöneticisi'ni** penceresi. Merhaba hello listesi bölümündeki sağ bölmede **sanal makineleri**, az önce oluşturduğunuz hello sanal makine bulun. Seçin ve hello makine adını sağ tıklatın ve seçin **ayarları**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. Merhaba üzerinde **ayarları** sayfasında hello sol bölmede, tıklatın **İşlemci**. Merhaba sağ bölmede, ayarlamak **sanal işlemcilerin sayısı** too4 (veya daha fazla). **Uygula**'ya tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. toomeet hello en düşük gereksinimler, tooadd 500 GB sanal veri diski de gerekir. Merhaba, **ayarları** sayfa:

    1. Merhaba sol bölmesinde seçin **SCSI denetleyicisi**.
    2. Merhaba sağ bölmede seçin **sabit sürücü** tıklatıp **Ekle**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. Merhaba üzerinde **sabit sürücü** sayfası, select hello **sanal sabit disk** seçeneğini ve tıklayın **yeni**. Merhaba **Yeni Sanal Sabit Disk Sihirbazı** başlatır.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. Merhaba üzerinde **başlamadan önce** hello Yeni Sanal Sabit Disk Sihirbazı, sayfasını tıklatın **sonraki**.
16. Merhaba üzerinde **Disk biçimi seçin sayfasında**, hello varsayılan seçeneği kabul **VHDX** biçimi. **İleri**’ye tıklayın. Bu ekran, Windows Server 2008 R2 çalıştıran, sunulan değil.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. Merhaba üzerinde **Disk türünü seçin sayfasında**, sanal sabit disk türü olarak ayarlamak **dinamik olarak genişletilen** (önerilen). **Boyutu sabit** disk çalışır ancak toowait uzun bir süre gerekebilir. Merhaba kullanmamanızı öneririz **Differencing** seçeneği. **İleri**’ye tıklayın. Windows Server 2012 R2 ve Windows Server 2012'de, **dinamik olarak genişletilen** Windows Server 2008 R2'de hello varsayılan iken hello varsayılan seçenektir **boyutu sabit**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. Merhaba üzerinde **ad ve konum belirtin** sayfasında, sağlayan bir **adı** yanı **konumu** (tooone göz atabilirsiniz) hello veri diski için. **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. Merhaba üzerinde **Disk yapılandırma** sayfası, select hello seçeneği **bir yeni boş sanal sabit disk Oluştur** ve hello boyutu olarak belirtin **500 GB** (veya daha fazla). 500 GB hello minimum gereksinim olsa da, her zaman daha büyük bir disk sağlayabilirsiniz. Olamaz genişletmek veya bir kez sağlanan hello diski küçültmeye unutmayın. Disk tooprovision hello boyutu hakkında daha fazla bilgi için hello hello boyutlandırma bölümünde gözden [en iyi yöntemler belge](storsimple-ova-best-practices.md). **İleri**’ye tıklayın.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. Merhaba üzerinde **Özet** sayfasında, sanal veri diskinizi hello ayrıntılarını gözden geçirin ve memnun tıklatmak **son** toocreate hello disk. Merhaba sihirbaz kapanır ve bir sanal sabit disk tooyour makine eklenir.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Toohello iade **ayarları** sayfası. Tıklatın **Tamam** tooclose hello **ayarları** sayfasında ve tooHyper-V Yöneticisi'ni penceresine dönün.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>3. adım: hello sanal dizinin başlatın ve hello IP Al
Aşağıdaki adımları toostart hello sanal dizinizi gerçekleştirmek ve tooit bağlanın.

#### <a name="toostart-hello-virtual-array"></a>toostart hello sanal dizinin
1. Merhaba sanal dizinin başlatın.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Hello aygıt çalıştırdıktan sonra hello cihaz seçin, sağ tıklayın ve seçin **Bağlan**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Merhaba aygıt toobe hazır 5-10 dakika toowait olabilir. Bir durum iletisi hello konsol tooindicate hello ilerleme görüntülenir. Merhaba cihaz hazır olduktan sonra çok Git**eylem**. Tuşuna `Ctrl + Alt + Delete` toohello sanal dizinin toolog. Merhaba varsayılan kullanıcı *StorSimpleAdmin* ve hello varsayılan parola *Parola1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Güvenlik nedenleriyle hello ilk oturum açmada hello cihaz Yönetici parolasının süresi dolar. İstendiğinde toochange hello parola olur.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   En az 8 karakter içeren bir parola girin. Merhaba parola en az 3 4 gereksinimlerine hello dışında karşılaması gerekir: büyük harf, küçük harfler, sayısal ve özel karakter. Merhaba parola tooconfirm yeniden girin. Bu hello parolanın değiştirilmesi bildirilir.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Merhaba parola başarıyla değiştirildikten sonra hello sanal dizinin yeniden başlatılabilir. Merhaba aygıt toostart bekleyin.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    Merhaba cihazın Hello Windows PowerShell konsolu ile birlikte bir ilerleme çubuğu görüntülenir.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Adım 6-8 yalnızca yukarı DHCP olmayan ortamda önyüklemesi sırasında uygulanır. Bir DHCP ortamında varsa, bu adımları atlayın ve toostep 9 gidin. Cihazınızı DHCP olmayan ortamda yukarı önyüklendiğinde ekran aşağıdaki hello görürsünüz.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Ardından, hello ağ yapılandırın.
7. Kullanım hello `Get-HcsIpAddress` sanal dizinizi etkin toolist hello ağ arabirimleri komutu. Cihazınızı etkin tek bir ağ arabirimi varsa, hello varsayılan atanan ad toothis arabirimidir `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Kullanım hello `Set-HcsIpAddress` cmdlet tooconfigure hello ağ. Aşağıdaki örnek hello bakın:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Merhaba ilk Kurulum tamamlandıktan ve hello aygıt yukarı önyüklendikten sonra hello aygıt başlık metni görürsünüz. Başlangıç IP adresi ve hello başlık metni toomanage hello aygıtı görüntülenen hello URL'sini not edin. Bu IP adresi tooconnect toohello web sanal dizinin ve tam hello yerel kurulumu ve kayıt kullanıcı arabirimini kullanın.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (İsteğe bağlı) Yalnızca Cihazınızı hello Bulutu dağıtıyorsanız bu adımı gerçekleştirin. Şimdi Cihazınızda hello Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) mod olanak sağlar. Merhaba FIPS 140 standardı, gizli verilerin hello koruma için BİZE Federal hükümeti bilgisayar sistemleri tarafından kullanım için onaylanan şifreleme algoritmalarını tanımlar.

    1. cmdlet aşağıdaki hello çalıştırmak tooenable hello FIPS modunda:

        `Enable-HcsFIPSMode`
    2. Böylece Hello şifreleme doğrulama etkili hello FIPS modunda etkinleştirdikten sonra Cihazınızı yeniden başlatın.

       > [!NOTE]
       > Etkinleştirmek veya FIPS modundayken, Cihazınızda devre dışı. FIPS ve FIPS olmayan mod arasında değişen hello aygıt desteklenmiyor.
       >
       >

Cihazınızı hello en düşük yapılandırma gereksinimlerini karşılamıyorsa, aşağıdaki hata hello Başlık metin (aşağıda gösterilen) hello bakın. Merhaba makine sahip en düşük gereksinimler hello yeterli kaynakları toomeet olması hello aygıt yapılandırmasını değiştirin. Ardından, yeniden başlatın ve toohello aygıtı bağlayın. Toohello en düşük yapılandırma gereksinimlerini başvuran [1. adım: hello ana bilgisayar sistemi minimum sanal dizinin gereksinimlerini karşıladığından emin olmak](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Başka bir hata hello yerel web kullanıcı Arabirimi kullanılarak hello başlangıç yapılandırması sırasında yüz, iş akışları şu toohello başvurun:

* Tanılama çok testler[web kullanıcı Arabirimi Kurulumu sorunlarını giderme](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Günlük paketi oluşturmak ve günlük dosyalarını görüntülemek](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Sonraki adımlar
* [Dosya sunucusu olarak StorSimple sanal dizinizi ayarlama](storsimple-virtual-array-deploy3-fs-setup.md)
* [StorSimple sanal dizinizi bir iSCSI sunucusu olarak ayarla](storsimple-virtual-array-deploy3-iscsi-setup.md)

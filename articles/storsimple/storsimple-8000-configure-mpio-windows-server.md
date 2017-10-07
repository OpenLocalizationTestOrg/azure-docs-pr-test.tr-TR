---
title: "StorSimple cihazınız için MPIO aaaConfigure | Microsoft Docs"
description: "StorSimple cihazınız için çok yollu g/ç (MPIO) tooconfigure tooa ana bilgisayar Windows Server 2012 R2 çalıştıran nasıl bağlanacağını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7796524edc739826ba1e977161fc9988c6d316e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Çok yollu g/ç StorSimple cihazınız için yapılandırma

Bu öğretici tooinstall izleyin ve Windows Server 2012 R2 ve bağlı tooa StorSimple fiziksel cihazı çalıştıran bir konakta hello çok yollu g/ç (MPIO) özelliğini kullanmanız gerekir hello adımlar açıklanmaktadır. Bu makalede Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar yalnızca geçerlidir. MPIO, StorSimple bulut uygulaması üzerinde şu anda desteklenmiyor.

Microsoft Windows Server toohelp hello çok yollu g/ç (MPIO) özelliği için destek yerleşik yüksek oranda kullanılabilir, hataya dayanıklı SAN yapılandırmaları oluşturun. MPIO yedek fiziksel yol bileşenlerini kullanır — bağdaştırıcılar, kablolar ve anahtarlar — toocreate hello sunucu ile Merhaba depolama cihazı arasında mantıksal yollar. Bileşen hatası varsa, böylece uygulamaların verilerine erişmeye devam mantıksal yolu toofail neden çoklu yol oluşturma mantığı alternatif bir yol g/ç için kullanır. Ayrıca yapılandırmanıza bağlı olarak, MPIO de bu yollar genelinde hello yük dengelenmesi olarak performansı artırabilir. Daha fazla bilgi için bkz: [MPIO genel bakış](https://technet.microsoft.com/library/cc725907.aspx "MPIO genel bakış ve özellikleri").

Merhaba yüksek kullanılabilirlik için StorSimple çözümünüzün, MPIO, StorSimple Cihazınızda yapılandırılması gerekir. Windows Server 2012 R2 çalıştıran, ana bilgisayar sunucuları üzerinde MPIO yüklendiğinde hello sunucuları bağlantı, ağ veya arabirim hatalarına sonra dayanabilir.

## <a name="mpio-configuration-summary"></a>MPIO Yapılandırma Özeti

MPIO Windows Server'da isteğe bağlı bir özelliktir ve varsayılan olarak yüklenmez. Sunucu Yöneticisi aracılığıyla bir özellik olarak yüklenmesi gerekir.

Bu adımları tooconfigure MPIO, StorSimple Cihazınızda izleyin:

* 1. adım: Yükleme hello Windows Server konağında MPIO
* 2. adım: StorSimple birimler için MPIO yapılandırma
* 3. adım: Bağlama StorSimple birimlerini hello ana bilgisayarda
* 4. adım: Yüksek kullanılabilirlik için MPIO yapılandırma ve Yük Dengelemesi

Her adımları önceki hello hello aşağıdaki bölümlerde ele alınmıştır.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>1. adım: Yükleme hello Windows Server konağında MPIO

Bu özellik, Windows Server konağında tooinstall tamamlamak hello yordamı izleyerek.

#### <a name="tooinstall-mpio-on-hello-host"></a>Merhaba konağında MPIO tooinstall

1. Windows Server ana bilgisayarında Sunucu Yöneticisi'ni açın. Merhaba Yöneticiler grubunun üyesi olan Windows Server 2012 R2 veya Windows Server 2012 çalıştıran tooa bilgisayarda oturum açtığında varsayılan olarak, Sunucu Yöneticisi'ni başlatır. Merhaba Sunucu Yöneticisi'ni zaten açık değilse tıklatın **Başlat > Sunucu Yöneticisi'ni**.
   
   ![Sunucu Yöneticisi](./media/storsimple-configure-mpio-windows-server/IC740997.png)

2. Tıklatın **Sunucu Yöneticisi'ni > Pano > Rol ve Özellik Ekle**. Bu hello başlatır **rol ve Özellik Ekle** Sihirbazı.
   
   ![Roller ve Özellikler Sihirbazı 1 ekleme](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. Merhaba, **rol ve Özellik Ekle** Sihirbazı'nı hello aşağıdaki adımları gerçekleştirin:
   
   1. Merhaba üzerinde **başlamadan önce** sayfasında, **sonraki**.
   2. Merhaba üzerinde **yükleme türünü seçin** sayfasında, hello varsayılan ayarı kabul **rol tabanlı veya özellik tabanlı** yükleme. **İleri**’ye tıklayın.
   
       ![Rol ve Özellik Ekleme Sihirbazı 2 Ekle](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   3. Merhaba üzerinde **Select hedef sunucu** sayfasında, **hello sunucu havuzundan bir sunucu seçin**. Ana bilgisayar sunucunuz otomatik olarak bulunması gerekir. **İleri**’ye tıklayın.
   4. Merhaba üzerinde **sunucu rollerini seçin** sayfasında, **sonraki**.
   5. Hello üzerinde **seçin özellikleri** sayfasında **çok yollu g/ç**, tıklatıp **sonraki**.
   
       ![Rol ve Özellik Ekleme Sihirbazı 5 Ekle](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   6. Merhaba üzerinde **Yükleme Seçimlerini Onayla** sayfasında hello seçimini onaylayın ve ardından **otomatik olarak yeniden başlatma hello hedef sunucu**, aşağıda gösterildiği gibi. **Yükle**'ye tıklayın.
   
       ![Rol ve Özellik Ekleme Sihirbazı 8 Ekle](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   7. Merhaba yükleme tamamlandığında, size bildirilir. Tıklatın **Kapat** tooclose hello Sihirbazı.
   
       ![Rol ve Özellik Ekleme Sihirbazı 9 Ekle](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>2. adım: StorSimple birimler için MPIO yapılandırma

MPIO yapılandırılmış tooidentify StorSimple birimlerini olması gerekir. tooconfigure MPIO toorecognize StorSimple birimlerini hello aşağıdaki adımları gerçekleştirin.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>StorSimple birimler için MPIO tooconfigure

1. Açık hello **MPIO Yapılandırması**. Tıklatın **Sunucu Yöneticisi'ni > Pano > Araçlar > MPIO**.
2. Merhaba, **MPIO Özellikleri** iletişim kutusu, select hello **çoklu yolları Bul** sekmesi.
3. Seçin **iSCSI aygıtları için destek eklemek**ve ardından **Ekle**.  
   ![MPIO özellikleri çoklu yolları Bul](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. İstendiğinde hello sunucusunu yeniden başlatın.
5. Merhaba, **MPIO Özellikleri** iletişim kutusunda, hello **MPIO cihazları** sekmesi. **Ekle**'ye tıklayın.
    </br>![MPIO özellikleri MPIO cihazları](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. Merhaba, **MPIO desteği Ekle** iletişim kutusunda **aygıt donanım kimliği**, cihaz seri numarasını girin. StorSimple cihaz Yöneticisi hizmetinize tooget hello cihaz seri numarası, erişim. Çok gidin**cihazlar > Pano**. Merhaba cihaz seri numarasını hello sağ görüntülenen **Hızlı Bakış** hello cihaz Pano bölmesi.
    </br>
    ![MPIO desteği Ekle](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. İstendiğinde hello sunucusunu yeniden başlatın.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>3. adım: Bağlama StorSimple birimlerini hello ana bilgisayarda

Windows Server'da MPIO yapılandırıldıktan sonra hello StorSimple cihazında oluşturulan birimlerin bağlanabilir ve ardından MPIO artıklığı avantajından yararlanabilirsiniz. bir birim toomount hello aşağıdaki adımları gerçekleştirin.

#### <a name="toomount-volumes-on-hello-host"></a>Merhaba ana bilgisayar üzerindeki toomount birimleri

1. Açık hello **iSCSI başlatıcısı özellikleri** hello Windows Server ana penceresinde. Tıklatın **Sunucu Yöneticisi'ni > Pano > Araçlar > iSCSI başlatıcısı**.
2. Merhaba, **iSCSI başlatıcısı özellikleri** iletişim kutusu, hello bulma sekmesini tıklatın ve ardından **Hedef Portal Bul**.
3. Merhaba, **Hedef Portal Bul** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   1. Merhaba StorSimple Cihazınızı veri bağlantı noktası Hello IP adresini girin (örneğin, veri 0 girin).
   2. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu.
     
     > [!IMPORTANT]
     > **İSCSI bağlantıları için bir özel ağ kullanıyorsanız, bağlı toohello özel ağ hello veri bağlantı noktası hello IP adresini girin.**
    
4. Cihazınızda ikinci bir ağ arabirimi (örneğin, veri 1) için 2-3 adımları yineleyin. Bu arabirimleri için iSCSI etkin olması gerektiğini aklınızda bulundurun. Daha fazla bilgi için bkz: [ağ arabirimleri değiştirme](storsimple-8000-modify-device-config.md#modify-network-interfaces).
5. Select hello **hedefleri** hello sekmesinde **iSCSI başlatıcısı özellikleri** iletişim kutusu. Merhaba StorSimple cihazı görmelisiniz IQN altında hedef **bulunan hedefler**.

   ![iSCSI Başlatıcı özellikleri hedefler sekmesi](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Tıklatın **Bağlan** tooestablish StorSimple Cihazınızı ile iSCSI oturumu bir. A **tooTarget bağlanmak** iletişim kutusu görüntülenir.
7. Merhaba, **tooTarget bağlanmak** iletişim kutusu, select hello **etkinleştir çok yollu** onay kutusu. Tıklatın **Gelişmiş**.
8. Merhaba, **Gelişmiş ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
   1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinden, **Microsoft iSCSI başlatıcısı**.
   2. Merhaba üzerinde **Başlatıcı IP** açılan listesinden, hello konağının select hello IP adresi.
   3. Merhaba üzerinde **hedef portalı** IP aşağı açılan listesinde, select hello IP aygıt arabirimi.
   4. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu.
9. **Özellikler**'e tıklayın. Merhaba, **özellikleri** iletişim kutusu, tıklatın **oturum Ekle**.
10. Merhaba, **tooTarget bağlanmak** iletişim kutusu, select hello **etkinleştir çok yollu** onay kutusu. Tıklatın **Gelişmiş**.
11. Merhaba, **Gelişmiş ayarları** iletişim kutusunda:

    1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinde, select Microsoft iSCSI başlatıcısı.
    2. Merhaba üzerinde **Başlatıcı IP** aşağı açılan listesinden, select hello IP adresine karşılık gelen toohello ana. Bu durumda, iki ağ arabirimi hello aygıt tooa tek bir ağ arabiriminde hello konaktaki bağlanırsınız. Bu nedenle, bu arabirimi olan hello ilk oturumun hello için sağlanan aynıdır.
    3. Merhaba üzerinde **Hedef Portal IP** açılan listesinden, hello cihazda etkin hello ikinci veri arabirimi için select hello IP adresi.
    4. Tıklatın **Tamam** tooreturn toohello iSCSI Başlatıcı Özellikleri iletişim kutusu. İkinci oturum toohello hedef eklediniz.
12. Açık **Bilgisayar Yönetimi** çok gezinme tarafından**Sunucu Yöneticisi'ni > Pano > Bilgisayar Yönetimi**. Merhaba sol bölmede **depolama > Disk Yönetimi**. altında görünür toothis konak olan hello StorSimple cihazında oluşturulan hello birim görünür **Disk Yönetimi** yeni diskler olarak.
13. Başlangıç diski başlatın ve yeni bir birim oluşturun. Merhaba biçimlendirme işlemi sırasında 64 KB blok boyutunu seçin.
    
    ![Disk Yönetimi](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. Altında **Disk Yönetimi**, sağ hello **Disk** seçip **özellikleri**.
15. Merhaba StorSimple Model içinde ### **çok yollu Disk cihaz özellikleri** iletişim kutusunda, hello **MPIO** sekmesi.
    
    ![StorSimple 8100 çok yollu Disk DeviceProp.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. Merhaba, **DSM adı** 'yi tıklatın **ayrıntıları** ve hello parametreleri toohello varsayılan parametreleri ayarlandığını doğrulayın. Merhaba varsayılan parametreler şunlardır:
    
    * Yolunu doğrulayın süresi = 30
    * Yeniden deneme sayısı = 3
    * PDO kaldırma süresi 20 =
    * Yeniden deneme aralığı = 1
    * Yolunu doğrulayın etkin = işaretli.

> [!NOTE]
> **Merhaba varsayılan parametreleri değiştirmeyin.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>4. adım: Yüksek kullanılabilirlik için MPIO yapılandırma ve Yük Dengelemesi

Yüksek kullanılabilirlik için çok yollu dayalı ve Yük Dengeleme, birden çok oturumu toodeclare hello farklı yollar kullanılabilir el ile eklenmesi gerekir. Merhaba konak bağlı iki arabirim varsa yeniden (her bir veri arabirimi ve ana bilgisayar arabirimi ise yalnızca iki oturumları gerekli olacaktır uygun yolu permütasyon ile yapılandırılmış dört oturumları gerekiyor Örneğin, tooSAN ve hello aygıt iki arabirimler bağlı tooSAN, vardır farklı bir IP alt ağda bulunan ve yönlendirilebilir değil).

**Merhaba cihaz ve uygulama ana bilgisayarı arasındaki en az 8 etkin paralel oturumları sahip olmasını öneririz.** Bu, Windows Server sisteminizdeki 4 ağ arabirimleri etkinleştirerek elde edilebilir. Merhaba donanım veya işletim sistemi düzeyinde, Windows Server ana bilgisayardaki fiziksel ağ arabirimlerine veya sanal arabirimleri aracılığıyla ağ sanallaştırma teknolojileri kullanın. Merhaba iki ağ arabirimi ile Merhaba cihazda, bu yapılandırma 8 etkin oturumlarını neden olur. Bu yapılandırma hello cihaz ve bulut verimliliği en iyi duruma getirme yardımcı olur.

> [!IMPORTANT]
> **1 GbE ve 10 GbE ağ arabirimleri karıştırmamanızı öneririz. İki ağ arabirimi kullanırsanız, her iki arabirimde hello aynı türde olmalıdır.**

Merhaba aşağıdaki yordamda açıklanmıştır nasıl iki ağ arabirimi ile bir StorSimple cihazına bağlı tooa olduğunda tooadd ana bilgisayar oturumları ile iki ağ arabirimi. Bu, yalnızca 4 oturumları sağlar. Dört ağ arabirimlerine sahip iki ağ arabirimleri bağlı tooa ana bilgisayarla bir StorSimple cihazı ile aynı bu yordamı kullanın. Burada açıklanan 4 oturumları tooconfigure 8 hello yerine gerekir.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>yüksek kullanılabilirlik ve Yük Dengeleme için MPIO tooconfigure

1. Merhaba hedefinin bir bulma gerçekleştir: hello içinde **iSCSI başlatıcısı özellikleri** iletişim kutusunda, hello **bulma** sekmesini tıklatın, **Portal Bul**.
2. Merhaba, **tooTarget bağlanmak** iletişim kutusunda, hello aygıt ağ arabirimlerinden biri, başlangıç IP adresi girin.
3. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu.
4. Merhaba, **iSCSI başlatıcısı özellikleri** iletişim kutusu, select hello **hedefleri** sekmesinde bulunan hello hedef vurgulayın ve ardından **Bağlan**. Merhaba **tooTarget bağlanmak** iletişim kutusu görüntülenir.
5. Merhaba, **tooTarget bağlanmak** iletişim kutusunda:
   
   1. Bırakın hello varsayılan hedef ayarı seçili **Bu bağlantı Ekle** sık kullanılan hedefler toohello listesi. Bu, bu bilgisayarı yeniden başlatır her zaman otomatik olarak toorestart hello bağlantı girişimi hello aygıt hale getirir.
   2. Select hello **etkinleştir çok yollu** onay kutusu.
   3. Tıklatın **Gelişmiş**.
6. Merhaba, **Gelişmiş ayarları** iletişim kutusunda:
   
   1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinden, **Microsoft iSCSI başlatıcısı**.
   2. Merhaba üzerinde **Başlatıcı IP** açılan listesinden, hello konağının select hello IP adresi.
   3. Merhaba üzerinde **Hedef Portal IP** açılan listesinden, hello cihazda etkin hello veri arabiriminin select hello IP adresi.
   4. Tıklatın **Tamam** tooreturn toohello iSCSI Başlatıcı Özellikleri iletişim kutusu.
7. Tıklatın **özellikleri**ve hello **özellikleri** iletişim kutusu, tıklatın **oturum Ekle**.
8. Merhaba, **tooTarget bağlanmak** iletişim kutusu, select hello **etkinleştir çok yollu** onay kutusunu işaretleyin ve ardından **Gelişmiş**.
9. Merhaba, **Gelişmiş ayarları** iletişim kutusunda:
   
   1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinden, **Microsoft iSCSI başlatıcısı**.
   2. Merhaba üzerinde **Başlatıcı IP** açılan listesinden, select hello IP adresi karşılık gelen toohello ikinci arabirimde hello ana bilgisayar.
   3. Merhaba üzerinde **Hedef Portal IP** açılan listesinden, hello cihazda etkin hello ikinci veri arabirimi için select hello IP adresi.
   4. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu. Şimdi bir ikinci oturum toohello hedef eklediniz.
10. Adım 8-10 tooadd ek oturumlar (yol) toohello hedef yineleyin. Merhaba ana bilgisayarda iki arabirim ve iki hello cihazda, dört oturumları toplam ekleyebilirsiniz.
11. İstenen hello oturumları (yol) hello ekledikten sonra **iSCSI başlatıcısı özellikleri** iletişim kutusu, select hello hedef ve tıklatın **özellikleri**. Merhaba hello oturumları sekmesinde **özellikleri** iletişim kutusu, toohello olası yolu permütasyon karşılık gelen Not hello dört oturum tanımlayıcıları. bir oturumu, toocancel hello onay kutusunu sonraki tooa oturum tanımlayıcısı seçin ve ardından **Bağlantıyı Kes**.
12. select hello oturumları içinde sunulan tooview aygıtları **aygıtları** sekmesini tooconfigure hello seçili cihaz için MPIO İlkesi tıklatın **MPIO**. Merhaba **cihaz ayrıntıları** iletişim kutusu görüntülenir. Merhaba üzerinde **MPIO** sekmesinde, uygun hello seçebilirsiniz **Yük Dengeleme İlkesi** ayarlar. Merhaba de görüntüleyebilirsiniz **etkin** veya **bekleme** yol türü.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple cihaz yapılandırmanızı hello StorSimple cihaz Yöneticisi hizmeti toomodify kullanarak](storsimple-8000-modify-device-config.md).


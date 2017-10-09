---
title: "ana bilgisayarda aaaConfigure MPIO bağlı tooStorSimple sanal dizinin | Microsoft Docs"
description: "Windows Server 2012 R2 çalıştıran tooa konak tooconfigure, StorSimple sanal dizisi için çok yollu g/ç (MPIO) nasıl bağlanacağını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Windows Server konağında StorSimple sanal dizinin hello için çok yollu g/ç yapılandırın
## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooinstall çok yollu g/ç özelliğini (MPIO), Windows Server konağınızda yalnızca StorSimple birimler için belirli yapılandırma ayarları uygulamak ve MPIO StorSimple birimlerini doğrulayın açıklanmaktadır. Merhaba yordamı StorSimple 1200 sanal dizinizi iki ağ arabirimi ile bağlı tooa Windows Server ana iki ağ arabirimlerine sahip olduğunu varsayar. Bu makalede bulunan hello bilgiler yalnızca toohello sanal bir dizi geçerlidir. StorSimple 8000 serisi cihazlar hakkında daha fazla bilgi için çok gidin[StorSimple ana bilgisayar için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md). 

Windows Server yardımcı derleme yüksek oranda kullanılabilir, hataya dayanıklı bir depolama yapılandırmaları Hello MPIO özelliği. MPIO yedek fiziksel yol bileşenlerini kullanır — bağdaştırıcılar, kablolar ve anahtarlar — toocreate hello sunucu ile Merhaba depolama cihazı arasında mantıksal yollar. Bileşen hatası varsa, böylece uygulamaların verilerine erişmeye devam mantıksal yolu toofail neden çoklu yol oluşturma mantığı alternatif bir yol g/ç için kullanır. Ayrıca yapılandırmanıza bağlı olarak, MPIO de bu yollar genelinde yeniden hello yük dengeleyerek performansı artırabilir. Daha fazla bilgi için bkz: [MPIO genel bakış](https://technet.microsoft.com/library/cc725907.aspx "MPIO genel bakış ve özellikleri").

Merhaba yüksek kullanılabilirlik için StorSimple çözümünüzün, Windows Server konakları bağlı tooyour StorSimple sanal dizinin (modeli 1200) hello üzerinde MPIO'yu yapılandırın. Merhaba ana bilgisayar sunucuları, ardından bağlantı, ağ veya arabirim hatalarına dayanabilir. 

Bu adımları tooconfigure MPIO toofollow gerekir: 

* Yapılandırma önkoşulları
* 1. adım: Yükleme hello Windows Server konağında MPIO
* 2. adım: StorSimple birimler için MPIO yapılandırma
* 3. adım: Bağlama StorSimple birimlerini hello ana bilgisayarda

Her adımları yukarıda hello hello aşağıdaki bölümlerde ele alınmıştır.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde hello yapılandırma önkoşulları hello Windows Server konak ve sanal dizinizi ayrıntılarını verir.

### <a name="on-windows-server-host"></a>Windows Server ana bilgisayarında
* Windows Server konağınızda 2 ağ arabirimleri etkin olduğundan emin olun.

### <a name="on-storsimple-virtual-array"></a>StorSimple sanal dizisinde
* Merhaba sanal dizinin bir iSCSI sunucusu olarak yapılandırılması gerekir. toolearn daha, fazla [sanal bir dizi bir iSCSI sunucu olarak ayarlamak](storsimple-virtual-array-deploy3-iscsi-setup.md). Bir veya daha fazla ağ arabirimine hello dizisinde etkinleştirilmiş olmalıdır.   
* Sanal dizinizi Hello ağ arabirimlerindeki hello Windows Server ana bilgisayardan erişilebilir olmalıdır.
* Bir veya daha fazla birim, StorSimple sanal dizisinde oluşturulmalıdır. toolearn daha, fazla [birim Ekle](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) , StorSimple sanal dizi. Bu yordamda hello sanal dizisinde 3 birimleri (1 yerel olarak sabitlenmiş ve 2 katmanlı gösterildiği gibi aşağıdaki) oluşturduk.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>StorSimple sanal dizinin için donanım yapılandırması
Aşağıdaki Hello şekilde hello yüksek kullanılabilirlik için donanım yapılandırması ve StorSimple sanal bu yordamda kullanılan dizisi ve Windows Server ana bilgisayar için çoklu yol oluşturma Yük Dengeleme gösterilmektedir.

![MPIO donanım yapılandırması](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Şekil önceki hello gösterildiği gibi kullanın:

* StorSimple sanal Hyper-V üzerinde sağlanan dizinizi iSCSI sunucusu olarak yapılandırılmış bir tek düğümlü etkin aygıttır.
* İki sanal ağ arabirimi, dizi etkinleştirilir. Merhaba yerel web kullanıcı Arabirimi, sanal dizinin, iki ağ arabirimi çok giderek etkinleştirildiğini doğrulayın**ağ ayarlarını** aşağıda gösterildiği gibi:
  
    ![1200 üzerinde etkin ağ arabirimleri](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Etkin hello Not hello IPv4 adreslerini ağ arabirimleri (Ethernet, Ethernet 2 varsayılan olarak) ve hello ana bilgisayarda daha sonra kullanmak için kaydedin.
* İki ağ arabirimi, Windows Server ana bilgisayarında etkinleştirilir. Merhaba, bağlı arabirimler dizisi ve ana bilgisayar için bulunan hello aynı alt ağda sonra kullanılabilir 4 yolları olacaktır. Bu yordamı hello durumda, bu. Her bir ağ arabirimine hello dizi ve ana bilgisayar arabirimde farklı bir IP alt ağ (ve değil yönlendirilebilir) varsa, ancak sonra yalnızca 2 yolları kullanılabilir.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>1. adım: Yükleme hello Windows Server konağında MPIO
MPIO Windows Server'da isteğe bağlı bir özelliktir ve varsayılan olarak yüklenmez. Sunucu Yöneticisi aracılığıyla bir özellik olarak yüklenmesi gerekir. Bu özellik, Windows Server konağında tooinstall tamamlamak hello yordamı izleyerek.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>2. adım: StorSimple birimler için MPIO yapılandırma
MPIO yapılandırılmış toobe tooidentify StorSimple birimlerini gerekir. tooconfigure MPIO toorecognize StorSimple birimlerini hello aşağıdaki adımları gerçekleştirin.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>3. adım: Bağlama StorSimple birimlerini hello ana bilgisayarda
Windows Server'da MPIO yapılandırıldıktan sonra hello StorSimple dizisinde oluşturulan birimlerin bağlanabilir ve ardından MPIO artıklığı avantajından yararlanabilirsiniz. bir birim toomount hello aşağıdaki adımları gerçekleştirin.

#### <a name="toomount-volumes-on-hello-host"></a>Merhaba ana bilgisayar üzerindeki toomount birimleri
1. Açık hello **iSCSI başlatıcısı özellikleri** hello Windows Server ana penceresinde. Çok Git**Sunucu Yöneticisi'ni > Pano > Araçlar > iSCSI başlatıcısı**.
2. Merhaba, **iSCSI başlatıcısı özellikleri** iletişim kutusu, tıklatın **bulma**ve ardından **Hedef Portal Bul**.
3. Merhaba, **Hedef Portal Bul** iletişim kutusunda, aşağıdaki hello:
   
    1. StorSimple sanal dizinizi üzerinde Hello hello ilk etkin ağ arabiriminin IP adresini girin. Varsayılan olarak, bu olacaktır **Ethernet**. 
    2. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu.
     
    > [!IMPORTANT]
    > İSCSI bağlantıları için bir özel ağ kullanıyorsanız, bağlı toohello özel ağ hello veri bağlantı noktası hello IP adresini girin.
     
4. Dizinizi üzerinde ikinci bir ağ arabirimi (örneğin, Ethernet 2) için 2-3 adımları yineleyin. 
5. Select hello **hedefleri** hello sekmesinde **iSCSI başlatıcısı özellikleri** iletişim kutusu. Sanal dizinizi için altında hedef olarak her birim yüzeyini görmelisiniz **bulunan hedefler**. Bu durumda, üç hedefleri (karşılık gelen toothree birimleri) bulunması.
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Tıklatın **Bağlan** tooestablish bir StorSimple sanal dizinizi ile iSCSI oturumu. A **tooTarget bağlanmak** iletişim kutusu görüntülenir. Select hello **etkinleştir çok yollu** onay kutusu. Tıklatın **Gelişmiş**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. Merhaba, **Gelişmiş ayarları** iletişim kutusunda, aşağıdaki hello:                                        
   
    1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinden, **Microsoft iSCSI başlatıcısı**.
    2. Merhaba üzerinde **Başlatıcı IP** açılan listesinden, hello konağının select hello IP adresi.
    3. Merhaba üzerinde **hedef portalı** IP aşağı açılan listesinde, select hello IP dizi arabirimi.
    4. Tıklatın **Tamam** tooreturn toohello **iSCSI başlatıcısı özellikleri** iletişim kutusu.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. **Özellikler**'e tıklayın. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. Merhaba, **özellikleri** iletişim kutusu, tıklatın **oturum Ekle**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. Merhaba, **tooTarget bağlanmak** iletişim kutusu, select hello **etkinleştir çok yollu** onay kutusu. Tıklatın **Gelişmiş**.
11. Merhaba, **Gelişmiş ayarları** iletişim kutusunda:                                        
    
    1. Merhaba üzerinde **yerel bağdaştırıcı** aşağı açılan listesinde, select Microsoft iSCSI başlatıcısı.

    2. Merhaba üzerinde **Başlatıcı IP** aşağı açılan listesinden, select hello IP adresine karşılık gelen toohello ana. Bu durumda, iki ağ arabirimi hello dizi tooa tek bir ağ arabiriminde hello konaktaki bağlanırsınız. Bu nedenle, bu arabirimi olan hello ilk oturumun hello için sağlanan aynıdır.

    3. Merhaba üzerinde **Hedef Portal IP** açılan listesinden, hello dizisinde etkin hello ikinci veri arabirimi için select hello IP adresi.

    4. Tıklatın **Tamam** tooreturn toohello iSCSI Başlatıcı Özellikleri iletişim kutusu. İkinci oturum toohello hedef eklediniz.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. İstenen hello oturumları (yol) hello ekledikten sonra **iSCSI başlatıcısı özellikleri** iletişim kutusu, select hello hedef ve tıklatın **özellikleri**. Merhaba hello oturumları sekmesinde **özellikleri** iletişim kutusu, toohello olası yolu permütasyon karşılık gelen Not hello dört oturum tanımlayıcıları. bir oturumu, toocancel hello onay kutusunu sonraki tooa oturum tanımlayıcısı seçin ve ardından **Bağlantıyı Kes**.

    6. select hello oturumları içinde sunulan tooview aygıtları **aygıtları** sekmesini tooconfigure hello seçili cihaz için MPIO İlkesi tıklatın **MPIO**.

    7. Merhaba **ayrıntıları** iletişim kutusu görüntülenir. Merhaba üzerinde **MPIO** sekmesinde, uygun hello seçebilirsiniz **Yük Dengeleme İlkesi** ayarlar. Merhaba de görüntüleyebilirsiniz **etkin** veya **bekleme** yol türü.
12. Adım 8-11 tooadd ek oturumlar (yol) toohello hedef yineleyin. Merhaba ana bilgisayarda iki arabirim ve iki hello sanal dizisindeki, her hedef için dört oturumları toplam ekleyebilirsiniz. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Her birim (yüzeyleri hedefi olarak) için aşağıdaki adımları toorepeat gerekir.
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Açık **Bilgisayar Yönetimi** çok gezinme tarafından**Sunucu Yöneticisi'ni > Pano > Bilgisayar Yönetimi**. Merhaba sol bölmede **depolama > Disk Yönetimi**. Merhaba görünür toothis konak olan StorSimple sanal dizinin hello üzerinde oluşturulan birimlerin altında görünür **Disk Yönetimi** yeni diskler olarak.
15. Başlangıç diski başlatın ve yeni bir birim oluşturun. Merhaba biçimlendirme işlemi sırasında 64 KB ayırma birimi boyutu (Avustralya) seçin. Merhaba işlemi hello kullanılabilir tüm birimleri için yineleyin.
    
    ![Disk Yönetimi](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. Altında **Disk Yönetimi**, sağ hello **Disk** seçip **özellikleri**.
17. Merhaba, **çok yollu Disk cihaz özellikleri** iletişim kutusunda, hello **MPIO** sekmesi.
    
    ![Disk özellikleri](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. Merhaba, **DSM adı** 'yi tıklatın **ayrıntıları** ve hello parametreleri toohello varsayılan parametreleri ayarlandığını doğrulayın. Merhaba varsayılan parametreler şunlardır:
    
    * Yolunu doğrulayın süresi = 30
    * Yeniden deneme sayısı = 3
    * PDO kaldırma süresi 20 =
    * Yeniden deneme aralığı = 1
    * Yolunu doğrulayın etkin = işaretli.
    
    > [!NOTE]
    > **Merhaba varsayılan parametreleri değiştirmeyin.**
   
## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple sanal dizinizi hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-virtual-array-manager-service-administration.md).


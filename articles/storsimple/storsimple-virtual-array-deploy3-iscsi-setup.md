---
title: aaaMicrosoft Azure StorSimple sanal dizinin iSCSI sunucusu Kurulumu | Microsoft Docs
description: "Nasıl tooperform ilk Kurulum, StorSimple iSCSI sunucuyu kaydetmek ve cihaz kurulumunu tamamlayın açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>StorSimple sanal dizinin – kümesi yukarı Azure Portalı aracılığıyla iSCSI sunucusu olarak dağıtma

![iSCSI Kurulum işlem akışı](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Genel Bakış

Bu dağıtım öğretici toohello Microsoft Azure StorSimple sanal dizinin geçerlidir. Bu öğretici nasıl tooperform hello ilk Kurulum, StorSimple iSCSI sunucunuz, tam hello aygıt ayarları kaydedin ve sonra oluşturmak, bağlamak, başlatmak ve StorSimple sanal bir iSCSI sunucusu olarak yapılandırılmış dizinizi birimlerde biçimlendirmek açıklar. 

açıklanan hello yordamları, yaklaşık 30 dakika too1 saat toocomplete buraya yazın. Bu makalede yayımlanmış hello bilgiler tooStorSimple sanal diziler yalnızca geçerlidir.

## <a name="setup-prerequisites"></a>Kurulum Önkoşulları

Yapılandırmak ve StorSimple sanal dizinizi ayarlama önce emin olun:

* Sanal bir dizi sağlanan ve açıklandığı gibi tooit bağlı [dağıtmak StorSimple sanal dizinin - sağlama Hyper-V sanal bir dizide](storsimple-ova-deploy2-provision-hyperv.md) veya [dağıtmak StorSimple sanal dizinin - VMware sanal bir dizide sağlama ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Merhaba, StorSimple sanal dizileriniz toomanage'de oluşturduğunuz StorSimple cihaz Yöneticisi hizmeti gelen hello hizmet kayıt anahtarı var. Daha fazla bilgi için bkz: **2. adım: hello hizmet kayıt anahtarını Al** içinde [StorSimple sanal dizinin dağıtma - hello portal hazırlama](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Mevcut bir StorSimple cihaz Yöneticisi hizmeti ile kaydetme hello ikinci veya sonraki sanal dizi gerekiyorsa hello hizmet verileri şifreleme anahtarı olması gerekir. Merhaba ilk aygıt hizmeti ile başarıyla kaydettirildi olduğunda bu anahtar oluşturuldu. Bu anahtar kaybettiyseniz, bkz: **Get hello hizmet verileri şifreleme anahtarı** içinde [kullanın, StorSimple sanal dizinizi Web kullanıcı arabirimini tooadminister hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Adım adım Kurulumu

Adım adım yönergeler tooset takip hello kullanın ve StorSimple sanal dizinizi yapılandırın:

* [1. adım: hello yerel web kullanıcı Arabirimi Kurulumu tamamlamak ve Cihazınızı kaydedin](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [2. adım: Tam hello cihaz Kurulumu gerekli.](#step-2-complete-the-required-device-setup)
* [3. adım: Birim Ekle](#step-3-add-a-volume)
* [4. adım: Bağlamak, başlatmak ve bir birimi biçimlendirme](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>1. adım: hello yerel web kullanıcı Arabirimi Kurulumu tamamlamak ve Cihazınızı kaydedin

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Kurulum hello ve hello cihaz kaydetme

1. Bir tarayıcı penceresi açın. tooconnect toohello web UI türü:
   
    `https://<ip-address of network interface>`
   
    Merhaba önceki adımda not ettiğiniz hello bağlantı URL'sini kullanın. Merhaba Web sitesinin güvenlik sertifikasında bir sorun olduğunu bildiren bir hata görürsünüz. Tıklatın **devam toothis web sayfası**.
   
    ![güvenlik sertifikası hatası](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Oturum açma toohello web sanal cihazınız olarak UI **StorSimpleAdmin**. Adım 3'te değiştirdiğiniz hello cihaz Yöneticisi parolasını girin: Başlangıç hello sanal cihazı [dağıtmak StorSimple sanal dizinin - sağlama Hyper-V'de sanal cihazı](storsimple-virtual-array-deploy2-provision-hyperv.md) veya [StorSimple sanal dizinin - dağıtma VMware sanal bir aygıtı sağlamak](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Oturum açma sayfası](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Toohello gerçekleştirilecek **giriş** sayfası. Bu sayfayı hello açıklar tooconfigure ve kaydetme sanal aygıt hello StorSimple cihaz Yöneticisi hizmeti ile Merhaba çeşitli ayarları gerekli. Bu hello Not **ağ ayarlarını**, **Web proxy ayarlarını**, ve **saat ayarlarını** isteğe bağlıdır. sadece ayarları gerekli hello **aygıt ayarları** ve **bulut ayarları**.
   
    ![Giriş sayfası](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. Merhaba üzerinde **ağ ayarlarını** altında sayfa **ağ arabirimleri**, DATA 0 otomatik olarak yapılandırılacaktır sizin için. Her ağ arabirimi tarafından varsayılan tooget bir IP adresi otomatik olarak ayarlanır (DHCP). Bu nedenle, bir IP adresi, alt ağ ve ağ geçidi otomatik olarak (IPv4 ve IPv6 için) atanır.
   
    Bir iSCSI sunucusu (tooprovision blok depolama) olarak Cihazınızı toodeploy planlarken, hello devre dışı bırakmanızı öneririz **IP adresini otomatik olarak almak** seçeneği ve statik IP adreslerini yapılandırın.
   
    ![Ağ Ayarları sayfası](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Merhaba hello aygıtı sağlama işlemi sırasında birden fazla ağ arabirimi eklediyseniz, bunları burada yapılandırabilirsiniz. Ağ arabirimi yalnızca veya IPv4 ve IPv6 IPv4 olarak yapılandırabilirsiniz unutmayın. IPv6 yalnızca yapılandırmaları desteklenmez.
5. Cihazınızı bulut depolama hizmeti sağlayıcıları veya tooresolve toocommunicate Cihazınızı denediğinde, dosya sunucusu olarak yapılandırılmışsa, bunlar adıyla kullanıldığından DNS sunucusu gereklidir. Merhaba üzerinde **ağ ayarlarını** sayfasında hello altında **DNS sunucuları**:
   
   1. Bir birincil ve ikincil DNS sunucusu otomatik olarak yapılandırılır. Statik IP adresleri tooconfigure seçerseniz, DNS sunucuları belirtebilirsiniz. Yüksek kullanılabilirlik için birincil ve ikincil bir DNS sunucusuna yapılandırmanızı öneririz.
   2. **Uygula**'ya tıklayın. Bu uygulama ve hello ağ ayarlarını doğrulayın.
6. Merhaba üzerinde **aygıt ayarları** sayfa:
   
   1. Benzersiz bir Ata **adı** tooyour aygıt. Bu ad, 1-15 karakter olabilir ve harf, rakam ve tire içerebilir.
   2. Merhaba tıklatın **iSCSI sunucusu** simgesi ![iSCSI sunucu simgesi](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) hello için **türü** oluşturmakta olduğunuz cihazın. Bir iSCSI sunucusunun tooprovision blok depolama izin verir.
   3. Etki alanına katılmış bu cihaz toobe isteyip istemediğinizi belirtin. Cihazınızı bir iSCSI sunucusuysa, ardından hello etki alanına katılım isteğe bağlıdır. İSCSI sunucu tooa etki alanınızın toonot birleştirme karar verirseniz, tıklatın **Uygula**, uygulanan hello ayarları toobe için bekleyin ve sonra toohello sonraki adıma atlayın.
      
       Toojoin hello aygıt tooa etki istiyorsanız. Girin bir **etki alanı adı**ve ardından **Uygula**.
      
      > [!NOTE]
      > İSCSI sunucu tooa etki alanınız, birleştirme olun sanal dizinizi Microsoft Azure Active Directory ve hiçbir Grup İlkesi nesneleri (GPO) için kendi kuruluş birimi (OU) olduğunu uygulanan tooit demektir.
      > 
      > 
   4. Bir iletişim kutusu görünür. Etki alanı kimlik bilgilerinizi hello belirtilen biçimde girin. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). Merhaba etki alanı kimlik bilgileri doğrulanır. Merhaba kimlik bilgileri yanlışsa, bir hata iletisi görürsünüz.
      
       ![kimlik bilgileri](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. **Uygula**'ya tıklayın. Bu uygulama ve hello aygıt ayarlarını doğrulayın.
7. (İsteğe bağlı) web proxy sunucunuzu yapılandırın. Web proxy yapılandırması isteğe bağlı olsa da, bir web proxy kullanıyorsanız, yalnızca burada yapılandırabilirsiniz olduğunu unutmayın.
   
    ![Web Proxy'yi Yapılandır](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    Merhaba üzerinde **Web proxy** sayfa:
   
   1. Tedarik hello **Web proxy URL'si** şu biçimde: *http://host-IP adresi* veya *FDQN:Port numarası*. HTTPS URL'leri desteklenmez unutmayın.
   2. Belirtin **kimlik doğrulaması** olarak **temel** veya **hiçbiri**.
   3. Kimlik doğrulaması kullanıyorsanız, tooprovide de gerekir bir **kullanıcıadı** ve **parola**.
   4. **Uygula**'ya tıklayın. Bu, doğrulamak ve yapılandırılmış hello web proxy ayarlarını uygulayın.
8. (İsteğe bağlı) saat dilimi gibi cihazınız için hello saat ayarlarını yapılandırın ve birincil ve ikincil NTP sunucuları hello. NTP sunucuları gerekli olduğu bulut hizmeti sağlayıcılarınızın ile doğrulanabilmesi Cihazınızı zaman eşitlemeniz gerekir.
   
    ![Saat ayarları](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    Merhaba üzerinde **saat ayarlarını** sayfa:
   
   1. Merhaba Hello aşağı açılan listeden seçin **saat dilimi** hangi hello aygıt dağıtıldığından hello coğrafi konum temelinde. cihazınız için başlangıç varsayılan saat dilimi PST alınır. Cihazınız zamanlanan tüm işlemler için bu saat dilimini kullanır.
   2. Belirtin bir **birincil NTP sunucusu** cihazınız için veya time.windows.com hello varsayılan değerini kabul edin. Ağınızın, NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun.
   3. İsteğe bağlı olarak belirtmek bir **ikincil NTP sunucusu** cihazınız için.
   4. **Uygula**'ya tıklayın. Bu doğrulamak ve yapılandırılmış hello saat ayarlarını uygulayın.
9. Cihazınızı Hello bulut ayarlarını yapılandırın. Bu adımda, hello yerel aygıt yapılandırmasını tamamlayın ve ardından hello aygıt, StorSimple cihaz Yöneticisi Hizmeti'ne kaydedin.
   
   1. Merhaba girin **hizmet kayıt anahtarını** aldığınız **2. adım: hello hizmet kayıt anahtarını Al** içinde [StorSimple sanal dizinin dağıtma - hello Portal hazırlama](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Bu hizmeti ile kaydetme hello ilk aygıtı değilse, tooprovide hello gerekir **hizmet verileri şifreleme anahtarı**. Hello hizmet kayıt anahtarı tooregister ek cihazlar hello StorSimple cihaz Yöneticisi hizmeti ile birlikte bu anahtar gereklidir. Daha fazla bilgi için çok başvurun[Get hello hizmet verileri şifreleme anahtarı](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) yerel web kullanıcı Arabirimi.
   3. Tıklatın **kaydetmek**. Bu hello aygıt yeniden başlatılır. 2-3 hello cihaz sorunsuz kaydedildikten önce dakika toowait gerekebilir. Merhaba cihaz yeniden başlatıldıktan sonra sayfasında toohello oturum ulaşabilirsiniz.
      
      ![Cihaz kaydetme](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Toohello Azure portalına dönün.
11. Toohello gidin **aygıtları** hizmetinizin dikey. Çok fazla kaynak varsa, tıklatın **tüm kaynakları**, hizmet adınızı (Ara gerekiyorsa) tıklatın ve ardından **aygıtları**.
12. Merhaba üzerinde **aygıtları** dikey penceresinde hello aygıt başarıyla bağlı toohello hizmet hello durumu arayarak doğrulayın. Merhaba Aygıt durumu olmalıdır **yukarı tooset hazır**.
    
    ![Cihaz kaydetme](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Adım 2: hello aygıt iSCSI sunucusu olarak yapılandırın.

Hello Azure portal toocomplete gerekli hello aygıt kurulum adımlarını izleyerek hello gerçekleştirin.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>iSCSI sunucusu olarak tooconfigure hello cihaz

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve çok Git**Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde, az önce oluşturduğunuz select hello cihaz. Bu cihazı olarak görüntülenebilir **yukarı tooset hazır**.
   
    ![Aygıt iSCSI sunucusu olarak yapılandırın](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Tıklatın hello cihaz ve hello cihaz hazır toosetup olduğunu belirten bir başlık iletisi görürsünüz.
   
    ![Aygıt iSCSI sunucusu olarak yapılandırın](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Tıklatın **yapılandırma** hello cihaz komut çubuğunda. Merhaba açılır **yapılandırma** dikey. Merhaba, **yapılandırma** dikey penceresinde, aşağıdaki hello:
   
   * Merhaba iSCSI sunucu adını otomatik olarak doldurulur.
   * Merhaba bulut depolama şifrelemesini çok ayarlandığından emin olun**etkin**. Bu, hello aygıt toohello buluttan gönderilen hello verilerin şifrelenmesini sağlar.
   * Bir 32 karakterlik şifreleme anahtarı belirtin ve daha sonra başvurmak için bir anahtar yönetimi uygulamasında kaydedin.
   * Cihazınızı ile kullanılan bir depolama hesabı toobe seçin. Bu abonelik, mevcut bir depolama hesabını seçebilir veya tıklayabilirsiniz **Ekle** toochoose bir hesaptan farklı bir abonelik.
     
     ![Aygıt iSCSI sunucusu olarak yapılandırın](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Tıklatın **yapılandırma** hello iSCSI sunucusu toocomplete ayarlama.
   
    ![Aygıt iSCSI sunucusu olarak yapılandırın](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Merhaba iSCSI sunucu oluşturma devam ediyor bildirilir. Merhaba iSCSI sunucusu başarıyla oluşturulduktan sonra hello **aygıtları** dikey güncelleştirilir ve hello karşılık gelen cihaz durumu **çevrimiçi**.
   
    ![Aygıt iSCSI sunucusu olarak yapılandırın](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>3. adım: Birim Ekle

1. Merhaba, **aygıtları** dikey penceresinde, yapılandırdığınız bir iSCSI sunucusu olarak select hello cihaz. Tıklatın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **birim ekleme**. Tıklatarak **+ Add birim** hello komut çubuğundan. Merhaba açılır **birim ekleme** dikey.
   
    ![Birim Ekle](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. Merhaba, **birim ekleme** dikey penceresinde, aşağıdaki hello:
   
   * Merhaba, **birim adı** alanında, biriminiz için benzersiz bir ad girin. Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.
   * Merhaba, **türü** açılır listesinde, belirleyin olup olmadığını toocreate bir **katmanlı** veya **yerel olarak sabitlenmiş** birim. Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **yerel olarak sabitlenmiş** **birim**. Diğer tüm veriler için seçin **katmanlı** **birim**.
   * Merhaba, **kapasite** alanında, hello hello birimin boyutunu belirtin. Katmanlı birim 500 GB ile 5 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir birim 50 GB ve 500 GB arasında olması gerekir.
     
     Yerel olarak sabitlenmiş bir birim sıkı hazırlanmıştır ve hello birimdeki birincil veri hello hello aygıtta kalır ve toohello buluta dağıtılmamasını sağlar.
     
     Katmanlı birim üzerinde hello diğer yandan sıkı hazırlanmıştır. Katmanlı birim oluşturduğunuzda, hello alanın % 10'yaklaşık hello yerel katmanında sağlanır ve % 90'hello alanı hello bulutta sağlanır. Örneğin, 1 TB birim sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello. Bu sırayla tüm hello yerel alana hello bir cihazda çalıştırma durumunda anlamına gelir (Merhaba % 10 kullanılamaz çünkü) bir katmanlı paylaşımı sağlayamazsınız.
     
     ![Birim Ekle](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Tıklatın **bağlı Konaklar**, tooconnect toothis birim istediğiniz ve ardından bir erişim denetimi kaydı (ACR) karşılık gelen toohello iSCSI başlatıcısı seçin **seçin**. <br><br> 
3. Yeni bir bağlı konak tooadd tıklatın **yeni Ekle**, hello ana bilgisayarı ve onun iSCSI için bir ad girin tam adını (IQN) ve ardından **Ekle**. Merhaba IQN yoksa, çok Git[ek A: alma hello bir Windows Server konağının IQN'ini](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Birim Ekle](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Biriminiz yapılandırma bittiğinde, tıklatın **Tamam**. Bir birim belirtilen hello ile oluşturulacak ayarları ve bir bildirim görürsünüz. Varsayılan olarak, izleme ve yedekleme hello birim için etkinleştirilecek.
   
     ![Birim Ekle](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. Birim hello tooconfirm edildi başarıyla oluşturuldu, Git toohello **birimleri** dikey. Listelenen hello birim görmeniz gerekir.
   
   ![Birim Ekle](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>4. adım: Bağlamak, başlatmak ve bir birimi biçimlendirme

Merhaba gerçekleştirme adımları toomount aşağıdaki başlatın ve bir Windows Server konağında StorSimple birimlerinizi biçimlendirin.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, başlatın ve bir birimi biçimlendirme

1. Açık hello **iSCSI başlatıcısı** hello uygun sunucusundaki uygulama.
2. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **bulma** sekmesini tıklatın, **Portal Bul**.
   
    ![Portal Bul](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. Merhaba, **Hedef Portal Bul** iletişim kutusu, Merhaba, iSCSI etkin ağ arabiriminin IP adresini girin ve ardından **Tamam**.
   
    ![IP adresi](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **hedefleri** sekmesinde, hello bulun **bulunan hedefler**. (Her birimi bulunan bir hedef olacaktır.) Merhaba Aygıt durumu olarak görünmelidir **devre dışı**.
   
    ![bulunan hedefler](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Hedef cihazı seçin ve ardından **Bağlan**. Merhaba cihaz bağlandıktan sonra hello durumu çok değişmelidir**bağlı**. (Merhaba Microsoft iSCSI başlatıcısını kullanma hakkında daha fazla bilgi için bkz: [yükleme ve yapılandırma Microsoft iSCSI başlatıcısı][1].
   
    ![Hedef cihazı seçin](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. Windows konağında, hello Windows logosu tuşu + X tuşlarına basın ve ardından **çalıştırmak**.
7. Merhaba, **çalıştırmak** iletişim kutusuna **Diskmgmt.msc**. Tıklatın **Tamam**ve hello **Disk Yönetimi** iletişim kutusu görüntülenir. Merhaba sağ bölmede, konaktaki hello birimleri gösterir.
8. Merhaba, **Disk Yönetimi** penceresinde hello takılan birimler görünür hello aşağıdaki çizimde gösterildiği gibi. Merhaba bulunan birime sağ tıklayın (Merhaba disk adına tıklayın) ve ardından **çevrimiçi**.
   
    ![Disk Yönetimi](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Sağ tıklatıp **diski başlatma**.
   
    ![Disk 1 başlatma](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Merhaba iletişim kutusunda, hello diskler tooinitialize seçin ve ardından **Tamam**.
    
    ![Disk 2 başlatılamıyor](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. Merhaba Yeni Basit Birim Sihirbazı'nı başlatır. Bir disk boyutu seçin ve ardından **sonraki**.
    
    ![Yeni Birim Sihirbazı 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Bir sürücü harfi toohello birimini atayın ve ardından **sonraki**.
    
    ![Yeni Birim Sihirbazı'nı 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Merhaba parametreleri tooformat hello birim girin. **Windows Server'da yalnızca NTFS desteklenir.** Merhaba ayırma birimi boyutu too64K ayarlayın. Biriminiz için bir etiket sağlar. Önerilen en iyi yöntem, StorSimple sanal dizisinde sağlanan bu toobe aynı toohello birim adı değil. **İleri**’ye tıklayın.
    
    ![Yeni Birim Sihirbazı'nı 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Biriminiz için başlangıç değerlerini kontrol edin ve ardından **son**.
    
    ![Yeni Birim Sihirbazı'nı 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    Merhaba birimleri olarak görünür **çevrimiçi** hello üzerinde **Disk Yönetimi** sayfası.
    
    ![birimlerin çevrimiçi](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toouse hello yerel web kullanıcı Arabirimi çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Ek A: Get hello bir Windows Server konağının IQN'ini

Aşağıdaki adımları tooget hello iSCSI hello gerçekleştirmek tam adını (IQN) Windows Server 2012 çalıştıran bir Windows konağının.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>bir Windows konağının IQN'sini tooget hello

1. Merhaba Microsoft iSCSI başlatıcısını Windows konağında başlatın.
2. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **yapılandırma** sekmesinde seçin ve hello hello dize kopyalama **Başlatıcı adı** alan.
   
    ![iSCSI başlatıcısı özellikleri](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Bu dizeyi kaydedin.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx




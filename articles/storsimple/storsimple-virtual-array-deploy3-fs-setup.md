---
title: "StorSimple sanal dizisi dosya sunucusu olarak yukarı aaaSet | Microsoft Docs"
description: "StorSimple sanal dizinin dağıtım üçüncü Bu öğreticide, tooset sanal cihazı yukarı dosya sunucusu olarak bildirir."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>StorSimple sanal dizinin - kümesi yukarı Azure portal aracılığıyla dosya sunucusu olarak dağıtma
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Giriş
Bu makalede tooperform ilk Kurulum, StorSimple dosya sunucunuzu, tam hello aygıt ayarları kaydedin ve oluşturma ve tooSMB paylaşımları bağlanmak açıklanmaktadır. Gerekli dağıtım öğreticileri hello serideki makalesinde son hello budur toocompletely sanal dizinizi bir dosya sunucusu veya bir iSCSI sunucu olarak dağıtın.

Merhaba Kurulum ve yapılandırma işlemi yaklaşık 10 dakika toocomplete alabilir. Bu makalede Hello bilgiler yalnızca toohello dağıtımını hello StorSimple sanal dizinin geçerlidir. StorSimple 8000 serisi cihazlar Hello dağıtımı için gidin: [güncelleştirme 2 çalıştıran StorSimple 8000 serisi Cihazınızı dağıtmak](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Kurulum Önkoşulları
Yapılandırmak ve StorSimple sanal dizinizi ayarlama önce emin olun:

* Sanal dizinin ve içinde ayrıntılı hello olarak bağlı tooit sağlamış [Hyper-V StorSimple sanal dizisinde sağlamak](storsimple-virtual-array-deploy2-provision-hyperv.md) veya [VMware StorSimple sanal dizisinde sağlamak](storsimple-virtual-array-deploy2-provision-vmware.md).
* Merhaba hizmet kayıt anahtarını toomanage StorSimple sanal diziler oluşturulan hello StorSimple Aygıt Yöneticisi'ni hizmetinden var. Daha fazla bilgi için bkz: [2. adım: hello hizmet kayıt anahtarını Al](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) StorSimple sanal dizini.
* Mevcut bir StorSimple cihaz Yöneticisi hizmeti ile kaydetme hello ikinci veya sonraki sanal dizi gerekiyorsa hello hizmet verileri şifreleme anahtarı olması gerekir. Merhaba ilk aygıt hizmeti ile başarıyla kaydettirildi olduğunda bu anahtar oluşturuldu. Bu anahtar kaybettiyseniz, bkz: [Get hello hizmet verileri şifreleme anahtarı](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) , StorSimple sanal dizini.

## <a name="step-by-step-setup"></a>Adım adım Kurulumu
Adım adım yönergeler tooset takip hello kullanın ve StorSimple sanal dizinizi yapılandırın.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>1. adım: hello yerel web kullanıcı Arabirimi Kurulumu tamamlamak ve Cihazınızı kaydedin
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Kurulum hello ve hello cihaz kaydetme
1. Bir tarayıcı penceresi açın ve toohello yerel web kullanıcı Arabirimi bağlanın. Şunu yazın:
   
   `https://<ip-address of network interface>`
   
   Merhaba önceki adımda not ettiğiniz hello bağlantı URL'sini kullanın. Merhaba Web sitesinin güvenlik sertifikasında bir sorun olduğunu belirten bir hata görürsünüz. Tıklatın **toothis Web sayfası devam**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Oturum açma toohello web kullanıcı Arabirimi, sanal dizinin **StorSimpleAdmin**. Adım 3'te değiştirdiğiniz hello cihaz Yöneticisi parolasını girin: Başlangıç hello sanal dizisinde [Hyper-V StorSimple sanal dizisinde sağlamak](storsimple-virtual-array-deploy2-provision-hyperv.md) veya [VMware StorSimple sanal dizisinde sağlamak](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Toohello alınır **giriş** sayfası. Bu sayfayı hello açıklar tooconfigure ve kaydetme sanal dizinin hello StorSimple cihaz Yöneticisi hizmeti ile Merhaba çeşitli ayarları gerekli. Merhaba **ağ ayarlarını**, **Web proxy ayarlarını**, ve **saat ayarlarını** isteğe bağlıdır. sadece ayarları gerekli hello **aygıt ayarları** ve **bulut ayarları**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. Merhaba, **ağ ayarlarını** altında sayfa **ağ arabirimleri**, DATA 0 otomatik olarak yapılandırılacaktır sizin için. Her bir ağ arabirimine varsayılan tooget IP adresine göre otomatik olarak ayarlanır (DHCP). Bu nedenle, bir IP adresi, alt ağ ve ağ geçidi otomatik olarak (IPv4 ve IPv6 için) atanır.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Merhaba hello aygıtı sağlama işlemi sırasında birden fazla ağ arabirimi eklediyseniz, bunları burada yapılandırabilirsiniz. Ağ arabirimi yalnızca veya IPv4 ve IPv6 IPv4 olarak yapılandırabilirsiniz unutmayın. IPv6 yalnızca yapılandırmaları desteklenmez.
5. DNS sunucuları, Cihazınızı bulut depolama hizmeti sağlayıcıları veya tooresolve toocommunicate Cihazınızı denediğinde, dosya sunucusu olarak yapılandırılmış ad tarafından kullanıldığı için gereklidir. Merhaba, **ağ ayarlarını** sayfasında hello altında **DNS sunucuları**:
   
   1. Bir birincil ve ikincil DNS sunucusu otomatik olarak yapılandırılır. Statik IP adresleri tooconfigure seçerseniz, DNS sunucuları belirtebilirsiniz. Yüksek kullanılabilirlik için birincil ve ikincil bir DNS sunucusuna yapılandırmanızı öneririz.
   2. Tıklatın **Uygula** tooapply ve hello ağ ayarlarını doğrulayın.
6. Merhaba, **aygıt ayarları** sayfa:
   
   1. Benzersiz bir Ata **adı** tooyour aygıt. Bu ad, 1-15 karakter olabilir ve harf, rakam ve tire içerebilir.
   2. Merhaba tıklatın **dosya sunucusu** simgesi ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) hello için **türü** oluşturmakta olduğunuz cihazın. Bir dosya sunucusunda paylaşılan toocreate klasörleri izin verir.
   3. Cihazınızı bir dosya sunucusu olarak toojoin hello aygıt tooa etki alanı gerekir. Girin bir **etki alanı adı**.
   4. **Uygula**'ya tıklayın.
7. Bir iletişim kutusu görünür. Etki alanı kimlik bilgilerinizi hello belirtilen biçimde girin. Merhaba onay simgesine tıklayın. Merhaba etki alanı kimlik bilgileri doğrulanır. Merhaba kimlik bilgileri yanlışsa, bir hata iletisi görürsünüz.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. **Uygula**'ya tıklayın. Bu uygulama ve hello aygıt ayarlarını doğrulayın.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Sanal dizinizi kendi kuruluş biriminde (OU) için Active Directory ve hiçbir Grup İlkesi nesneleri (GPO) uygulanan tooit olan veya devralınan olduğundan emin olun. Grup İlkesi, StorSimple sanal dizinin hello üzerinde virüsten koruma yazılımı gibi uygulamaları yükleyebilir. Ek yazılım yükleme desteklenmez ve toodata bozulmasına yol açabilir. 
   > 
   > 
9. (İsteğe bağlı) web proxy sunucunuzu yapılandırın. Web proxy yapılandırması isteğe bağlı olsa da, bir web proxy kullanıyorsanız, yalnızca burada yapılandırabilirsiniz olduğunu unutmayın.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   Merhaba, **Web proxy** sayfa:
   
   1. Tedarik hello **Web proxy URL'si** şu biçimde: *http://&lt;ana bilgisayar IP adresi veya FDQN&gt;: bağlantı noktası numarası*. HTTPS URL'leri desteklenmez unutmayın.
   2. Belirtin **kimlik doğrulaması** olarak **temel** veya **hiçbiri**.
   3. Kimlik doğrulamasını kullanıyorsanız, tooprovide de gerekir bir **kullanıcıadı** ve **parola**.
   4. **Uygula**'ya tıklayın. Bu, doğrulamak ve yapılandırılmış hello web proxy ayarlarını uygulayın.
10. (İsteğe bağlı) saat dilimi gibi cihazınız için hello saat ayarlarını yapılandırın ve birincil ve ikincil NTP sunucuları hello. NTP sunucuları gerekli olduğu bulut hizmeti sağlayıcılarınızın ile doğrulanabilmesi Cihazınızı zaman eşitlemeniz gerekir.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    Merhaba, **saat ayarlarını** sayfa:
    
    1. Merhaba Hello açılır listeden seçin **saat dilimi** hangi hello aygıt dağıtıldığından hello coğrafi konum temelinde. cihazınız için başlangıç varsayılan saat dilimi PST alınır. Cihazınız zamanlanan tüm işlemler için bu saat dilimini kullanır.
    2. Belirtin bir **birincil NTP sunucusu** cihazınız için veya time.windows.com hello varsayılan değerini kabul edin. Ağınızın, NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun.
    3. İsteğe bağlı olarak belirtmek bir **ikincil NTP sunucusu** cihazınız için.
    4. **Uygula**'ya tıklayın. Bu doğrulamak ve yapılandırılmış hello saat ayarlarını uygulayın.
11. Cihazınızı Hello bulut ayarlarını yapılandırın. Bu adımda, hello yerel aygıt yapılandırmasını tamamlayın ve ardından hello aygıt, StorSimple cihaz Yöneticisi Hizmeti'ne kaydedin.
    
    1. Merhaba girin **hizmet kayıt anahtarını** aldığınız [2. adım: hello hizmet kayıt anahtarını Al](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) StorSimple sanal dizini.
    2. Bu hizmeti ile kaydetme ilk cihazınız varsa ile Merhaba sunulur **hizmet verileri şifreleme anahtarı**. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin. Hello hizmet kayıt anahtarı tooregister ek cihazlar hello StorSimple cihaz Yöneticisi hizmeti ile birlikte bu anahtar gereklidir. 
       
       Bu hizmeti ile kaydetme hello ilk aygıtı değilse, tooprovide hello hizmet verileri şifreleme anahtarı gerekir. Daha fazla bilgi için tooget hello başvurun [hizmet verileri şifreleme anahtarı](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) yerel web kullanıcı Arabirimi.
    3. Tıklatın **kaydetmek**. Bu hello aygıt yeniden başlatılır. 2-3 hello cihaz sorunsuz kaydedildikten önce dakika toowait gerekebilir. Merhaba cihaz yeniden başlatıldıktan sonra sayfasında toohello oturum ulaşabilirsiniz.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Toohello Azure portalına dönün. Çok Git**tüm kaynakları**, StorSimple Aygıt Yöneticisi'ni hizmetinizi arayın.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Filtre hello listesinde, StorSimple Aygıt Yöneticisi'ni hizmetinizi seçin ve sonra çok gidin**Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde hello aygıt toohello hizmeti başarıyla bağlandı ve hello durumu doğrulayın **yukarı tooset hazır**.
    
    ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>2. adım: hello aygıt dosya sunucusu olarak yapılandırın.
Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/) toocomplete hello cihaz Kurulumu gerekli.

#### <a name="tooconfigure-hello-device-as-file-server"></a>dosya sunucusu olarak tooconfigure hello cihaz
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve çok Git **Yönetim > aygıtları**. Merhaba, **aygıtları** dikey penceresinde, az önce oluşturduğunuz select hello cihaz. Bu cihazı olarak görüntülenebilir **yukarı tooset hazır**.
   
   ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Tıklatın hello cihaz ve hello cihaz hazır toosetup olduğunu belirten bir başlık iletisi görürsünüz.
   
    ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Tıklatın **yapılandırma** hello komut çubuğunda. Merhaba açılır **yapılandırma** dikey. Merhaba, **yapılandırma** dikey penceresinde, aşağıdaki hello:
   
    1. Merhaba dosya sunucusu adı otomatik olarak doldurulur.
    
    2. Merhaba bulut depolama şifrelemesini çok ayarlandığından emin olun**etkin**. Bu toohello bulut gönderilen tüm hello verileri şifreler. 
    
    3. 256 bit AES anahtarını hello kullanıcı tanımlı anahtar şifreleme için kullanılır. Bir 32 karakter anahtarı belirtin ve sonra hello anahtar tooconfirm girin. Merhaba anahtar kaydı bir anahtar yönetimi uygulaması gelecekte başvurmak için.
    
    4. Tıklatın **gerekli ayarları Yapılandır** toospecify depolama hesabı kimlik bilgileri toobe cihazınızla kullanılır. Tıklatın **yeni Ekle** yapılandırılmış depolama hesap kimlik bilgisi olup olmadığını. **Kullandığınız hello depolama hesabı blok blobları desteklediğinden emin olun. Sayfa bloblarını desteklenmez.** Hakkında daha fazla bilgi [engeller blobları ve sayfa bloblarını](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. Merhaba, **bir depolama hesabının kimlik bilgilerini eklemek** dikey penceresinde, aşağıdaki hello: 

    1. Hello Hello depolama hesabı ise, geçerli bir abonelik seçin hello hizmet aynı abonelik. Diğer hello depolama belirtin hello hizmet aboneliği dışında bir hesaptır. 
    
    2. Merhaba açılır listeden mevcut bir depolama hesabını seçin. 
    
    3. Başlangıç konumu otomatik olarak doldurulur belirtilen hello üzerinde temel depolama hesabı. 
    
    4. SSL tooensure hello aygıt hello bulut arasındaki güvenli ağ iletişim kanalını etkinleştirin.
    
    5. Tıklatın **Ekle** tooadd bu depolama hesabı kimlik bilgileri. 
   
        ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Merhaba depolama hesabı kimlik bilgilerini başarıyla oluşturulduktan sonra hello **yapılandırma** dikey pencereyi güncelleştirilmeyecek toodisplay hello belirtilen depolama hesabı kimlik bilgileri. **Yapılandır**'a tıklayın.
   
   ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Bir dosya görürsünüz sunucusu oluşturuluyor. Merhaba dosya sunucusu başarıyla oluşturulduktan sonra size bildirilecek.
   
   ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   Merhaba Aygıt durumu da değiştirir çok**çevrimiçi**.
   
   ![Bir dosya sunucusu yapılandırın](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   Tooadd bir paylaşım devam edebilirsiniz.

## <a name="step-3-add-a-share"></a>3. adım: bir paylaşımı ekleme
Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/) toocreate bir paylaşımı.

#### <a name="toocreate-a-share"></a>toocreate bir paylaşımı
1. Adım önceki hello yapılandırdığınız hello dosya sunucusu aygıtı seçin ve tıklatın **...**  (veya sağ tıklayın). Merhaba bağlam menüsünden seçin **Ekle paylaşımı**. Alternatif olarak, tıklayabilirsiniz **+ paylaşımı eklemek** hello cihaz komut çubuğunda.
   
   ![Paylaşım Ekle](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Paylaşım ayarlarını aşağıdaki hello belirtin:

    1. Paylaşımınıza için benzersiz bir ad. Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.
    
    2. İsteğe bağlı bir **açıklama** hello paylaşımı için. Merhaba açıklama hello paylaşım sahiplerini tanımlamaya yardımcı olur.
    
    3. A **türü** hello paylaşımı için. Merhaba türü olabilir **katmanlı** veya **yerel olarak sabitlenmiş**, katmanlı olan ile Merhaba varsayılan. Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin bir **yerel olarak sabitlenmiş** paylaşın. Diğer tüm veriler için seçin bir **katmanlı** paylaşın.
    Yerel olarak sabitlenmiş bir paylaşımı sıkı hazırlanmıştır ve hello birincil veri hello paylaşımında yerel toohello aygıt kalır ve toohello buluta dağıtılmamasını sağlar. Katmanlı bir paylaşımı üzerinde hello diğer yandan sıkı hazırlanmıştır. Katmanlı bir paylaşım oluşturduğunuzda, hello alanın % 10 hello yerel katmanında sağlanır ve % 90'hello alanı hello bulutta sağlanır. Örneğin, 1 TB birim sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello. Bu sırayla hello cihazda tüm hello yerel alana çalıştırırsanız, bir katmanlı paylaşımı sağlayamazsınız anlamına gelir.
   
    4. Merhaba, **kümesine varsayılan tam izinleri** alan, hello izinleri toohello kullanıcı veya bu paylaşıma erişen hello grubuna atayın. Merhaba kullanıcı veya hello kullanıcı grubunda Hello adını belirtin  *john@contoso.com*  biçimi. Bir kullanıcı grubu (yerine tek bir kullanıcı) tooallow yönetici ayrıcalıkları tooaccess bu paylaşımları kullanmanızı öneririz. Merhaba izinlerini burada atadıktan sonra bu izinleri dosya Gezgini toomodify sonra kullanabilirsiniz.
   
    5. Tıklatın **Ekle** toocreate hello paylaşımı. 
    
        ![Paylaşım Ekle](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Merhaba paylaşımı oluşturma sürüyor bildirilir.
   
        ![Paylaşım Ekle](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Merhaba paylaşımı ile Merhaba oluşturulduktan sonra hello ayarları, belirtilen **paylaşımları** dikey tooreflect hello yeni paylaşım güncelleştirmek. Varsayılan olarak, izleme ve yedekleme hello paylaşımı için etkinleştirilir.
   
    ![Paylaşım Ekle](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>4. adım: toohello paylaşımına bağlanma
Şimdi tooconnect tooone veya hello önceki adımda oluşturduğunuz daha fazla paylaşımları gerekir. Windows Server ana bilgisayar bağlı tooyour StorSimple sanal dizinin üzerinde aşağıdaki adımları gerçekleştirin.

#### <a name="tooconnect-toohello-share"></a>tooconnect toohello paylaşımı
1. Tuşuna ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + r Merhaba Çalıştır penceresinde hello belirtin *&#92; &#92;&lt; dosya sunucusu adı&gt;*  hello yolu olarak değiştirerek *dosya sunucusu adı* , atanan tooyour dosya sunucusunu hello aygıtla adı. **Tamam** düğmesine tıklayın.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Bu dosya Gezgini'ni açar. Artık klasörler olarak oluşturulan mümkün toosee hello paylaşımları olması gerekir. Seçin ve tooview hello içeriğini paylaşın (klasör) çift tıklayın.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Şimdi, dosyaları toothese paylaşımları ekleyin ve yedekleyin.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl toouse hello yerel web kullanıcı Arabirimi çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

